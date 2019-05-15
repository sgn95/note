# 安装

在ubuntu上安装mysql

step1:
``` sudo apt update
    sudo apt install mysql-server
```
设置root 用户密码

配置mysql
...

service mysql start

mysql -uroot -p123456

登录 
show databases;
use <--database-->
show tables;
 ...


远程连接
``` step1 登录服务:
    mysql -uroot -p123456
    step2 授权:
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'yourpassword' WITH GRANT OPTION;
    step3 使修改生效:
    FLUSH PRIVILEGES;
```
遇到的问题
在授权的时候遇到的问题
    ERROR 1819 (HY000): Your password does not satisfy the current policy requirements
    因为密码设置太简单 也可以关闭密码校验
    密码需要包含 大小写字母 数字 特殊字符

https://juejin.im/post/5cd2d57951882540d928c2be

sql连接 ODBC DSN connection strings 
参考 https://www.connectionstrings.com/odbc-dsn/
DSN (Data Source Name)
mysql 连接驱动 连接名字
https://github.com/go-sql-driver/mysql#dsn-data-source-name
```
system DSN
DSN=myDsn;Uid=myUsername;Pwd=;
File DSN
FILEDSN=c:\myDsnFile.dsn;Uid=myUsername;Pwd=;```
