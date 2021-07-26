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
