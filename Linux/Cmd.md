## git

**git clone**、**git push**、**git add** 、**git commit**、**git checkout**、**git pull**



    git reset HEAD                  如果add了的话，全都取消
    git checkout filename           恢复最新版本
    git commit --amend              改变提交的commit message 或者 对同一个提交进行代码上的修改
    git log -p -2                   最近两次的修改详细记录
    
    git reset test.cpp              如果add了test.cpp，要取消add
    git log                         查看提交文件的 logid
    git log -p  filename            查看该文件的提交历史， 可以通过关键字
    git reset --hard ${logid}                       回滚该logid的提交（已经commit，没有push）f you don't care about keeping the changes you made
    git reset --soft ${logid}                       use --soft if you want to keep your changes
    git diff --stat --cached origin/master          看commit但没有push的文件
    git log --graph                                 图形化显示
    git branch -d the_local_branch                  删除对应分支
    git brach tmp                                   创建一个branch分支，把当天提交记录都保存起来
    git co 当前branch
    git lg tmp                                      查看tmp这个分支的日志
    git cherry-pick  commitid                       把tmp上某个分支的commit合并到本分支后面
    git cm --amend                                  把change id 改了，要不把changeid也考到这个分支上，改分支提交合入的时候就会出现问题
    git merge feature-show-create-table-partition   当前分支是feature-show-create-table-partition-info，merge一下feature-show-create-table-partition ，响应的提交也会 merge过来
    git merge feature-show-create-table-partition-info --no-ff
    
    git co develop
    git branch
    git diff develop master
    git pull --rebase
    git branch feature-split-blacklist
    git add fe/src
    git rebase --abort
    git cm
    git branch feature origin/feature               把在本地新建一个feature分支并把远端的分支feature同步下来
    
    // 分支拉的久远了，和develop上差距比较大，先把把本地备份到 tmp分支
     git rebase develop                             rebase 本地develop的分支，（我当前的分支是tmp）·
    
     git format-patch -1                            生成对应的patch文件
     git am 0001-Add-delete-range-http-and-rpc-interface.patch
    
     git branch -d dev                              删除本地分支
     git branch -a                                  显示所有分支
     git push origin --delete dev                   删除远端分支
    
     git show ce8c290d23ebaf5e1348ff74df5c61a0d8185856  看这个commitid属于哪个分支
     git branch -a --contains 5c64d8be4950b0adc9352de848b1edb915c4ccd4  看远端和本地是否有这个分支
     git clone http://github.com/large-repository --depth 1
     cd large-repository
     git fetch --unshallow
     git fetch是将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中。
     git reset --hard origin/hotfix-leader-balance
     git stash
     git stash save "save message"                  执行存储时，添加备注，方便查找，只有git stash 也要可以的，但查找时不方便识别
     git stash pop                                  恢复
     git reset --hard origin/master                 恢复到和远端一致
     git show  commit_id  可以看到每个文件具体的改动内容





## Linux

linux 命令是对 Linux 系统进行管理的命令。对于 Linux 系统来说，无论是中央处理器、内存、磁盘驱动器、键盘、鼠标，还是用户等都是文件， Linux 系统管理的命令是它正常运行的核心，与之前的 DOS 命令类似。linux 命令在系统中有两种类型：内置 Shell 命令和 Linux 命令。

| 命令                        | 功能说明                                                     |
| --------------------------- | ------------------------------------------------------------ |
| 线上查询及帮助命令          |                                                              |
| man                         | 查看命令帮助，命令的词典，更复杂的还有info，但不常用         |
| help                        | 查看linux内置命令的帮助，比如cd命令                          |
| 文件和目录操作命令          |                                                              |
| ls                          | 全拼：list，功能：列出目录的内容及其内容属性信息             |
| cd                          | 全拼：change directory，功能：从当前工作目录切换到指定的工作目录 |
| cp                          | 全拼：copy，功能：复制文件或目录                             |
| find                        | 用于查找目录及目录下的文件                                   |
| mkdir                       | 全拼：make directories，功能：创建目录                       |
| mv                          | 全拼：move，功能：移动或重命名文件                           |
| pwd                         | 全拼：print working directory，功能：显示当前工作目录的绝对路径 |
| rename                      | 用于重命名文件                                               |
| rm                          | 全拼：remove，功能：删除一个或多个文件或目录                 |
| rmdir                       | 全拼：remove empty directories，功能：删除空目录             |
| touch                       | 创建新的空文件，改变已有文件的时间戳属性                     |
| tree                        | 以树形结构显示目录下的内容                                   |
| basename                    | 显示文件或目录名                                             |
| dirname                     | 显示文件或目录路径                                           |
| chattr                      | 改变文件的扩展属性                                           |
| lsattr                      | 查看文件的扩展属性                                           |
| file                        | 显示文件的类型                                               |
| md5sum                      | 计算和校验文件的MD5值                                        |
| 查看文件及内容              |                                                              |
| cat                         | 全拼：concatenate，功能：用于连接多个文件并且打印到屏幕输出或重定向到指定文件中 |
| tac                         | tac是cat的反向拼写，因此命令的功能为反向显示文件内容         |
| more                        | 分页显示文件内容                                             |
| less                        | 分页显示文件内容，more命令的相反用法                         |
| head                        | 显示文件内容的头部                                           |
| tail                        | 显示文件内容的尾部                                           |
| cut                         | 将文件的每一行按指定分隔符分割并输出                         |
| split                       | 分割文件为不同的小片段                                       |
| paste                       | 按行合并文件内容                                             |
| sort                        | 对文件的文本内容排序                                         |
| uniq                        | 去除重复行，oldboy                                           |
| wc                          | 统计文件的行数、单词数、或字节数                             |
| iconv                       | 转换文件的编码格式                                           |
| dos2unix                    | 将DOS格式文件转换成UNIX格式                                  |
| diff                        | 全拼：difference，功能：比较文件的差异，常用于文本文件       |
| vimdiff                     | 命令行可视化文件比较工具，常用于文本文件                     |
| rev                         | 反向输出文件内容                                             |
| grep/egrep                  | 过滤字符串，三剑客老三                                       |
| join                        | 按两个文件的相同字段合并                                     |
| tr                          | 替换或删除字符                                               |
| vi/vim                      | 命令行文本编辑器                                             |
| 文件压缩及解压              |                                                              |
| tar                         | 打包压缩，oldboy                                             |
| unzip                       | 解压文件                                                     |
| gzip                        | gzip压缩工具                                                 |
| zip                         | 压缩工具                                                     |
| 信息显示                    |                                                              |
| uname                       | 显示操作系统相关信息的命令                                   |
| hostname                    | 显示或设置当前系统的主机名                                   |
| dmesg                       | 显示开机信息，用于诊断系统故障                               |
| uptime                      | 显示系统运行时间及负载                                       |
| stat                        | 显示文件或文件系统的状态                                     |
| du                          | 计算磁盘空间使用情况                                         |
| df                          | 报告文件系统磁盘空间的使用情况                               |
| top                         | 实时显示系统资源使用情况                                     |
| free                        | 查看系统内存                                                 |
| date                        | 显示与设置系统时间                                           |
| cal                         | 查看日历等时间信息                                           |
| 搜索文件命令                |                                                              |
| which                       | 查找二进制命令，按环境变量Path路径查找                       |
| find                        | 从磁盘遍历查找文件或目录                                     |
| whereis                     | 查找二进制命令，按环境变量Path路径查找                       |
| locate                      | 从数据库(/var/lib/mlocate/mlocate.db)查找命令，使用update更新库 |
| 用户管理命令                |                                                              |
| useradd                     | 添加用户                                                     |
| usermod                     | 修改系统已经存在的用户属性                                   |
| userdel                     | 删除用户                                                     |
| groupadd                    | 添加用户组                                                   |
| passwd                      | 修改用户密码                                                 |
| chage                       | 修改用户密码有效期限                                         |
| id                          | 查看用户的uid，gid及归属的用户组                             |
| su                          | 切换用户身份                                                 |
| visudo                      | 编辑/etc/sudoers文件的专属命令                               |
| sudo                        | 以另外一个用户身份（默认root用户）执行事先在sudoers文件允许的命令 |
| 基础网络操作                |                                                              |
| telnet                      | 使用telnet协议远程登录                                       |
| ssh                         | 使用ssh加密协议远程登录                                      |
| scp                         | 全拼：secure copy，功能：用于不同主机之间复制文件            |
| wget                        | 命令行下载文件                                               |
| ping                        | 测试主机之间网络的连通性                                     |
| route                       | 显示和设置linux系统的路由表                                  |
| ifconfig                    | 查看、配置、启用或禁用网络接口的命令                         |
| ifup                        | 启动网卡                                                     |
| ifdown                      | 关闭网卡                                                     |
| netstat                     | 查看网络状态                                                 |
| ss                          | 查看网络状态                                                 |
| 深入网络操作                |                                                              |
| nmap                        | 网络扫描命令                                                 |
| lsof                        | 全拼：list open files，功能：列举系统中已经被打开的文件      |
| mail                        | 发送和接收邮件                                               |
| mutt                        | 邮件管理命令                                                 |
| nslookup                    | 交互式查询互联网DNS服务器命令                                |
| dig                         | 查找DNS解析过程                                              |
| host                        | 查询DNS的买那个了                                            |
| traceroute                  | 追踪数据传输路由情况                                         |
| tcpdump                     | 命令行的抓包工具                                             |
| 有关磁盘与文件系统的命令    |                                                              |
| mount                       | 挂载文件系统                                                 |
| umount                      | 卸载文件系统                                                 |
| fsck                        | 检查并修复Linux文件系统                                      |
| dd                          | 转换或复制文件                                               |
| dumpe2fs                    | 导出ext2/ext3/ext4文件系统信息                               |
| dump                        | ext2/3/4文件系统备份工具                                     |
| fdisk                       | 磁盘分区命令，适用于2TB以下磁盘分区                          |
| mkfs                        | 格式化创建Linux文件系统                                      |
| partprobe                   | 更新内核的硬盘分区表信息                                     |
| e2fsck                      | 检查ext2/ext3/ext4类型文件系统                               |
| mkswap                      | 创建Linux交换分区                                            |
| swapon                      | 启用交换分区                                                 |
| swapoff                     | 关闭交换分区                                                 |
| sync                        | 将内存缓冲区内的数据写入磁盘                                 |
| resize2fs                   | 调整ext2/ext3/ext4文件系统大小                               |
| 系统权限及用户授权相关命令  |                                                              |
| chmod                       | 改变文件或目录权限                                           |
| chown                       | 改变文件或目录的属主和属组                                   |
| chgrp                       | 更改文件用户组                                               |
| umask                       | 显示或设置权限掩码                                           |
| 查看系统用户登录信息的命令  |                                                              |
| whoami                      | 显示当前有效的用户名称，相当于执行id -un命令                 |
| who                         | 显示当前登录系统的用户信息                                   |
| w                           | 显示已经登录系统的用户列表，并显示用户正在执行的指令         |
| last                        | 显示登入系统的用户                                           |
| lastlog                     | 显示系统中所有用户最近一次登录信息                           |
| users                       | 显示当前登录系统的所有用户的用户列表                         |
| finger                      | 查找并显示用户信息                                           |
| 内置命令                    |                                                              |
| echo                        | 打印变量，或直接输出指定的字符串                             |
| printf                      | 将结果格式化输出到标准输出                                   |
| rpm                         | 管理rpm包的命令                                              |
| yum                         | 自动化简单化地管理rpm包的命令                                |
| watch                       | 周期性的执行给定的命令，并将命令的输出以全屏方式显示         |
| alias                       | 设置系统别名                                                 |
| unalias                     | 取消系统别名                                                 |
| date                        | 查看或设置系统时间                                           |
| clear                       | 清除屏幕                                                     |
| history                     | 查看命令执行的历史记录                                       |
| eject                       | 弹出光驱                                                     |
| time                        | 计算命令执行时间                                             |
| nc                          | 功能强大的网络工具                                           |
| xargs                       | 将标准输入转换成命令行参数                                   |
| exec                        | 调用并执行指令的命令                                         |
| export                      | 设置或显示环境变量                                           |
| unset                       | 删除变量或函数                                               |
| type                        | 用于判断另外一个命令是否是内置命令                           |
| bc                          | 命令行科学计算器                                             |
| 系统管理与性能监视命令      |                                                              |
| chkconfig                   | 管理Linux系统开机启动项                                      |
| vmstat                      | 虚拟内存统计                                                 |
| mpstat                      | 显示各个可用CPU的状态统计                                    |
| iostat                      | 统计系统IO                                                   |
| sar                         | 全面地获取系统的CPU、运行队列、磁盘I/O、分页（交换区）、内存、CPU中断和网络等性能数据 |
| ipcs                        | 用于报告Linux中进程间通信设施的状态，显示的信息包括消息列表、共享内存和信号量的信息 |
| ipcrm                       | 用来删除一个或更多的消息队列、信号量集或者共享内存标识       |
| strace                      | 用于诊断、调试Linux用户空间追踪器。我们用它来监控用户空间进程和内核的交互，比如系统调用、信号传递、进程状态变更等 |
| ltrace                      | 命令会跟踪进程的库函数调用，会显示出哪个库函数被调用         |
| 关机/重启/注销/查看系统信息 |                                                              |
| shutdown                    | 关机                                                         |
| halt                        | 关机                                                         |
| poweroff                    | 关闭电源                                                     |
| logout                      | 退出当前登录的shell                                          |
| exit                        | 退出当前登录的shell                                          |
| ctrl+d                      | 退出当前登录的shell的快捷键                                  |
| 进程管理相关命令            |                                                              |
| bg                          | 将一个在后台暂停的命令，变成继续执行（在后台执行）           |
| fg                          | 将后台中的命令调至前台继续运行                               |
| jobs                        | 查看当前有多少在后台运行的命令                               |
| kill                        | 终止进程                                                     |
| killall                     | 通过进程名终止进程                                           |
| pkill                       | 通过进程名终止进程                                           |
| crontab                     | 定时任务命令                                                 |
| ps                          | 显示进程的快照                                               |
| pstree                      | 树形显示进程                                                 |
| nice/renice                 | 调整程序运行的优先级                                         |
| nohup                       | 忽略挂起信号运行指令的命令                                   |
| pgrep                       | 查找匹配条件的进程                                           |
| runlevel                    | 查看系统当前运行级别                                         |
| init                        | 切换运行级别                                                 |
| service                     | 启动、停止、重新启动和关闭系统服务，还可以显示所有系统服务的当前状态 |

    tar -zxvf                       解压
    tar -zcvf  output.tar output/   压缩
    tar -cvf  output.tar output/    打包 不压缩
    tar -tvf test.tar.gz            预览压缩文件夹内容
    ldd                             查看一个 应用需要哪些依赖的动态库
    curl url -o obj                 下载该url的文件，类似wget
    curl -vk  https                 验证https
    vim --version | grep clipboard  看vim是否支持系统剪切板
    ls -lht                         看目录下文件大小以K/M/G 单位
    ll -tr                          看修改顺序
    /usr/libexec/java_home -V       java 路径
    nohup cmd &                     在后台运行cmd命令
    ssh -i id_rsa root@ip     使用私钥登录目标机器
    authorized_keys
    file                            查看文件信息
    strings                         查看bin文件下的字符串
    0 stdin，1 stdout，2 stderr
    2>&1                            将标准错误输出到标准输出中tai
    nohup myprogram > myprogram.out 2> myprogram.err &              将标准输出到特定的文件，err分开，后台起线程运行
    ctrl+A/ctrl+E                   定位到行首行未
    ctrl+U/ctrl+K                   删除到行首/行未
    ctrl+R                          查找历史命令
    ctags --list-languages          看ctags支持哪些语言
    find  ./  -name "*.xml"         递归查找一定要加双引号
    cal -3 / cal -y                 查看前一个月后一个月日历/显示全年的
    su - name                       切换到该用户，同时加载一些列环境配置，例如bash_profile
    sudo su                         切root账户
    rsync -av src/ 172.18.188.106:/Users/sunxiuyang/tmp/ 172.18.188.106为目标机器ip，copy src下的文件到目标机器tmp下
    rsync -av src 172.18.188.106:/Users/sunxiuyang/tmp/  把src这个目录copy过去
    for i in `cat gzns01_all`; do ssh -o StrictHostKeyChecking=no $i "cd /root && sh name_env_setup.sh"; done      root 已经是相互信任的
    ln -s jdk-8u161 jdk             软链
    ll | grep taf                   查看文件
    sort -k3 -n filename            按照（k3）第三个列 的数字(-n) 从小到大排序
    for i in `cat ip.list`;do host $i;done > tmp    按行读取ip.list文件, 并执行 host操作
    for i in `cat gzns01_all`; do scp -o no StrictHostKeyChecking `pwd`/home_env_setup.sh $i:/root/; done
    for i in `cat gzns01_all`; do ssh -o StrictHostKeyChecking=no $i "cd /root && sh home_env_setup.sh"; done
    dig www.baidu.com               dig命令可以执行查询域名相关的任务
    crontab
    rm node.log.* node.log.wf.* -f &    起一个进程删掉
    pstack pid                      打印出pid进程下所有的线程栈信息
    jstack -l pid                   打印java进程的堆栈信息
    for i in `echo -e "name1\n name2\n name3"`; do echo $i" "$RANDOM; done > ./tmp; cat ./tmp | sort -nk2        随机排序名字
    cat /proc/version
    cat /etc/issue
    ll /proc/340/fg | grep socket | wc -l       查看fd数量
    uptime                          看机器启动时间
    /etc/security/limits.conf       把core文件打开
    ulimit -c                       看core文件是否打开
    ulimit -c unlimited             不设置core文件大小
    /var/log/messages               看系统日志
    ls -l /proc/15430/fd/ | wc -l   查看这个进程打开的文件描述符的个数
    cat /proc/sys/fs/file-max       查看系统可打开的最大描述符
    lsof -p 24405                   看这个进程打开的fd
    netstat -antp | grep 24405      看该进程的链接的情况
    /var/log/message                系统启动后的信息和错误日志，是Red Hat Linux中最常用的日志之一
    sysctl -a | grep keepalive      看系统内核是不是那tcp得探活关了
    top -Hp 32554                   查看32554进程的线程情况
    lsblk -d -o name,rota           查看磁盘是否是ssd 或者 HDD， 如果ROTA：0 就是ssd
    curl http://test.com:8302/metrics -o tmp 把这个url的内容输出到文本里
    export TMOUT=0                  不超时
    
    asan/pmap                       看内存泄漏
    sed                             正则，各种替换
    fdisk -l                        切换root 账号 看机器链接的磁盘数量
    ls /dev                         看机器设备，看有多少块盘
    useradd name                   机器添加 name 用户
    passwd name                    给name 用户添加密码
    cat /dev/null > fe.log          清空文件
    awk -v RS='' -v ORS='\n\n' '/搜索的词/' 文件名字     搜出关键词所在的段落
