## 1、基础架构：一条SQL查询语句是如何执行的？

MySQL的基本架构示意图。

SQL语句在MySQL各个功能模块中的执行过程：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831154353799.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA2NTcwOTQ=,size_16,color_FFFFFF,t_70)

大体来说，MySQL 可以分为 Server 层和存储引擎层两部分

- Server层包括：连接器、查询缓存、分析器、优化器、执行器等。
- 存储引擎负责数据的存储和提取。常用的存储引擎InnoDB、MyISAM

#### 连接器

使用长连接有时候MySQL占用内存涨得特别快，因为MySQL在执行过程中临时使用的内存是管理在连接对象里面的。这些资源会在连接断开的时候才释放。长期连接可能导致内存占用太大，被系统强行杀掉（OOM），也就是MySQL异常重启了。

解决方案：

* 定期断开长连接。
* MySQL 5.7后的版本，可以通过执行 mysql_reset_connection 来重新初始化连接资源。该过程不需要重连和重新做权限验证。

#### 查询缓存

执行查询后，执行结果会被存入查询缓存中，如果查询命中缓存，MySQL不需要执行后面的操作，可以直接返回结果。效率高。

但是，查询缓存的失效非常频繁，只要有对一个表的更新，这个表上所有的查询缓存都会被清空。建议大多数情况下不要使用查询缓存。MySQL8.0版本把查询缓存功能已去除。

#### 分析器

```mysql
select * from T where ID = 10;
```

MySQL需要从命令里识别字符串分别是什么，代表什么。

1. 词法分析：识别 “select” 关键字，识别表名 “T” ，识别列ID “ID” 
2. 语法分析：判断该 SQL 语句是否满足 MySQL 语法

#### 优化器

当表里有多个索引，或者一个语句有多表关联（join）的时候，不同方案执行效率不同，优化器决定选择使用哪个方案。

#### 执行器

校验权限后，执行器根据表的引擎定义，去使用这个引擎提供的接口。


## 2、日志系统：一条SQL更新语句是如何执行的？

与查询流程不一样的是，更新流程还涉及两个重要的日志模块：redo log（重做日志）和binlog（归档日志）。

### 日志模块：redo log

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831154516315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA2NTcwOTQ=,size_16,color_FFFFFF,t_70)

在做更新操作时，如果每一次更新操作都立即写进磁盘，那么整个过程IO成本、查找成本都很高。redo log就是为了解决这一问题，MySQL通过WAL（Write-Ahead Logging）技术（先写日志，再写磁盘），先把更新操作写入redo log日志，并更新内存，这时更新操作就完成了，同时InnoDB引擎会在适当的时候（系统比较空闲时），将一批操作更新到磁盘里面。如果redo log写满时，就不能再执行新的更新，得停下来先擦掉redo log一些记录，写入磁盘，再执行新的更新。

有了redo log，InnoDB就可以保证即使数据库发生异常重启，之前提交的记录都不会丢失，这个能力称为crash-safe


### 日志模块：binlog

redo log和binlog不同点：

1. redo log 是 InnoDB 引擎特有的；binlog（归档日志）是MySQL的Server层实现的，所有引擎都可以使用
2. redo log是物理日志，记录的是“在某个数据页上做了什么修改”；binlog是逻辑日志，记录的是这个语句的原始逻辑，比如“给ID=2这一行的c字段加1”。binlog两种模式：statement格式记录SQL语句，row格式记录行的内容，两条（更新前和更新后）。
3. redo log 是循环写的，空间固定会用完；binlog是可以追加写入的。“追加写”是指binlog文件写到一定大小后会切换到下一个，并不会覆盖以前的日志。

update语句执行流程：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190831154617226.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTA2NTcwOTQ=,size_16,color_FFFFFF,t_70)

图中浅色框表示再InnoDB内部执行的，深色框表示在执行器中执行的。

将redo log的写入拆成了两个步骤：prepare 和 commit，这就是“两阶段提交”。

“两阶段提交”的目的是为了让两份日志之间的逻辑一致。保证一致性。


数据恢复过程：

- 首先，找到最近的一次全量备份，从这个备份恢复到临时库；
- 然后，从备份的时间点开始，将备份的binlog依次取出来，重放到中午误删表之前的那个时刻。
- 最后把表数据从临时库取出来，按需要恢复到线上库去。

redo log用于保证crash-safe能力。

innodb_flush_log_at_trx_commit这个参数设置成1，表示每次事物的redo log都直接持久化到磁盘（建议设置为1）。

sync_binlog这个参数设置为1，表示每次事物的binlog都持久化到磁盘（建议设置为1）。


## 3、事务隔离：为什么你改了我还看不见？

事物就是要保证一组数据库操作要么全部成功，要么全部失败。

事物支持是在引擎层实现的，但并不是所有引擎都支持事物，MyISAM引擎就不支持事物。

多事务同时执行的时候，可能会出现的问题：脏读、不可重复读、幻读。

SQL标准的事物隔离级别：

- 读未提交。是指一个事物还没提交时，它做的变更就能够被其他事物看到。
- 读提交。是指一个事物提交之后，它做的变更才会被其他事物看到。
- 可重复读。是指一个事物在执行过程中看到的数据，总是跟这个事物启动时看到的数据是一致的。
- 串行化。串行化，顾名思义是对于同一行记录，“写”会加“写锁”，“读”会加“读锁”。当出现读写锁冲突时，后访问的事物必须等待前一个事物执行完成，才能继续执行。


MySQL事物启动方式：

- 显式启动事务语句， begin 或 start transaction。提交语句commit，回滚语句rollback。
- set autocommit=0，这个命令会将这个线程的自动提交关闭。
