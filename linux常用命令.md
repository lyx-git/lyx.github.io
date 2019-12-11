# linux命令

  1. yum 用于各类的下载安装
     - yum search ifconfig 查询是否安装该命令
  2. telnet 用于远程登录其他服务器
  3. su 是switch user 的缩写，表示切换用户
  4. sudo 后面跟其他命令，表示以某个用户的身份执行该命令，一般默认是使用root用户
     - 有些命令只有root用户才能执行的命令，而一般普通用户是没有权限执行该命令的，所以在普通用户环境下，可以使用sudo命令执行只有在root用户下才能执行的命令
  5. netstat 用于判断网络有关的问题
     - netstat -ltpa |grep 3306 根据端口号，查询进程名称和pid
     - netstat -a 列出所有的进程。
