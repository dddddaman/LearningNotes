# MySQL

## 01 MySQL概述

sql、DB、DBMS分别是什么，他们之间的关系？

#### DB

DataBase（数据库）

数据库实际上在硬盘上以文件的形式存在

#### DBMS

DataBase Management System（数据库管理系统）

常见的有：MySQL Oracle DB2 Sybase SqlServer...

#### SQL

结构化查询语言，是一门标准通用的语言。标准的sql适合于所有的数据库产品

sql属于高级语言。只要能看懂英语单词的，写出来的sql语句，可以读懂什么意思

sql语句在执行的时候，实际上内部也会先进行编译，然后再执行sql。sql语句的编译由DBMS完成。

#### 关系

DBMS负责执行sql语句，通过执行sql语句来操作DB当中的数据。

DBMS（执行）-> SQL（操作）-> DB

#### 表

table，是数据库的基本组成单元，所有的数据都以表格的形式组织，目的是可读性强

一个表包括行和列

* 行：被称为数据/纪录（data）
* 列：被称为字段（column）

每一个字段包括的属性

* 字段名（学号，姓名，年龄等）
* 数据类型（int，varchar（字符串）等）
* 相关的约束（不能为空等）

#### 基本语法
查看有哪些数据库

show databases;（这个不是SQL语句，属于MySQL的命令）

创建数据库

creat database bjpowernode;（这个不是SQL语句，属于MySQL的命令）

使用bjpowernode数据库的数据

use bjpowernode;（这个不是SQL语句，属于MySQL的命令）

查看当前使用的数据库中有哪些表

show tables;（这个不是SQL语句，属于MySQL的命令）

查看其他数据库中的表

show tables from <database name>;

初始化数据

mysql> sourse D:\course\05-mysql\resources\bjpowernode.sql

sql脚本：一个以.sql结尾的文件，文件中编写了大量的sql语句

使用source命令执行sql脚本，完成初始化



删除数据库

drop database bjpowernode;

查看表结构

```mysql
desc 表名
desc emp;
```

查看表中的数据

```mysql
select * from emp；//实际开发中不建议使用*，效率较低
```

查看mysql版本

C:\Users\Administrator> mysql --version

C:\Users\Administrator> mysql -v

查询当前使用的数据库

select database();

查看数据库版本

select version();

终止一条语句

\c

查看创建表的语句

show create table emp;

#### 简单查询

select 字段 from 表名;

#### 条件查询

```mysql
select 字段 from 表名 where 条件；
select ename from emp where sal = 5000；
select sal from emp where ename = ‘SMITH’；varchar是字符串，需要用单引号
```

执行顺序：先from，然后where，最后select

```mysql
select ename,sal from emp where sal >= 1100 and sal <=3000;
//between and 在使用时候必须左小右大，用在数字上，是闭区间
select ename,sal,from emp where sal between 1100 and 3000;
//between and 用在字符串上，是左闭右开
select ename from emp where ename between 'A' and 'C';
```

在数据库当中NULL不是一个值，代表什么也没有，为空，空不是一个值，不能用等号衡量，必须使用 is null或者is not null

```mysql
//找出哪些人津贴为null？
select ename,sal,comm from emp where comm is null;
select ename,sal,comm from emp where comm is null or comm = 0;
```

in等同于or

```mysql
//找出工作岗位是MANAGER和SALESMAN的员工
select ename,job from emp where job = 'SALESMAN' or job = 'MANAGER';
select ename,job from emp where job in('SALESMAN','MANAGER');
//找出工作岗位不是MANAGER和SALESMAN的员工
select ename,job from emp where job not in('SALESMAN','MANAGER');
```

模糊查询like，%代表任意多个字符，_代表任意一个字符

```mysql
select ename from emp where ename like '%A%'; //查找名字带A的
select ename from emp where ename like '_A%'; //查找名字第二个字母是A的
select ename from emp where ename like '%\_%';//查找名字带_的
```

#### 排序

默认升序排列，asc表示升序，desc表示降序

越靠前的字段越能起到主导作用，只有当前面的字段无法完成排序的时候，才会启用后面的字段。

```mysql
select 字段 from 表名 order by 字段;
select ename，sal from emp order by sal；
select ename，sal from emp order by sal asc；
select ename，sal from emp order by sal desc；
//按照工资的降序排列，当工资相同的时候再按照名字的升序排列，前面的字段占主导作用
select ename，sal from emp order by sal desc，ename asc；
//可以按列排序，不推荐
select ename，sal from emp order by 2；//按第二列排序
```

| 命令语句       | 内部执行顺序 |
| -------------- | ------------ |
| select *       | 3            |
| from tablename | 1            |
| where 条件     | 2            |
| order by ...   | 4            |

#### 分组函数：多行处理函数

分组函数一共5个。所有的分组函数都是对“某一组”数据进行操作的。

多行处理函数的特点：输入多行，最终输出的结果是1行。

**分组函数自动忽略NULL** 

* count 计数
* sum 求和
* avg 平均值
* max 最大值
* min 最小值

```mysql
//找出工资总和
select sum(sal) from emp;
//找出最低工资
select min(sal) from emp;
//找出总人数
select count(ename) from emp;
select count(*) from emp;
```

SQL语句当中有一个语法规则，分组函数不可直接使用在where子句当中

原因：group by是在where执行之后才能执行，分组函数必须在group by分完组后才能执行，因此where语句中还未分组，不能使用分组函数。

```mysql
//找出工资大于平均工资的员工
//错误方法，where后面不能直接用分组函数
select ename,sal from emp where sal > avg(sal);
//ERROR 1111(BY000):Invaalid use of group function，无效的使用了分组函数
//正确方法，使用嵌套方法子查询
select ename,sal from emp where sal > (select avg(sal) from emp);
```

count(*)和count(具体的某个字段)的区别：

* count(*)：不是统计某个字段中数据的个数，而是统计总记录条数
* count(具体的某个字段)：表示统计某个字段中不为NULL的数据总数量

分组函数也能组合起来用：

```mysql
select count(*),sum(sal),avg(sal),max(sal),min(sal) from emp;
```

group by：按照某个字段或者某些字段进行分组

having：是对分组之后的数据进行再次过滤

```mysql
//找出每个工作岗位的最高薪资
select max(sal) from emp group by job;
```

分组函数一般都会和group by联合使用，并且任何一个分组函数（count、sum、avg、min、max）都是在group by语句执行结束之后才会执行的。当一条sql语句没有group by的话，整张表的数据会自成一组。

| 命令语句       | 内部执行顺序 |
| -------------- | ------------ |
| select *       | 5            |
| from tablename | 1            |
| where 条件     | 2            |
| group by       | 3            |
| having         | 4            |
| order by ...   | 6            |



#### 单行处理函数

单行处理函数：输入一行，输出一行。输入多少行，输出多少行。

所有数据库的规定：只要有NULL参与的运算结果一定是NULL。

ifnull（）空处理函数：ifnull(可能为NULL的数据，被当作什么处理)，属于单行处理函数

```mysql
ifnull(comm，0)
select ename,ifnull(comm，0) as comm from emp；
//计算每个员工的年薪，comm是津贴，有可能为NULL
select ename,(sal+ifnull(comm,0))*12 as yearsal from emp; 
```

