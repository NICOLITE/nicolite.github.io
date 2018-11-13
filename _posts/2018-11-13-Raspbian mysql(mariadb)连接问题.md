---
title: Raspbian mysql(mariadb)连接问题
date: 2018-11-13 20:17:30
categories:
- Raspbian
tags:
- Raspberry
- Raspbian
- mysql
- mariadb
---
树莓派3B+上安装完mysql只能通过sudo mysql -uroot登录
![](/images/20181113-201730-1.png)

#### 问题
今天在树莓派3B+上安装mysql(安装命令sudo apt install mysql-server mysql-client)出现了如下问题
  * 安装过程没有提示输入root的password
  * 安装成功后，输入指令mysql -uroot，提示Access denied for user ‘root’@’localhost’
  * 输入sudo mysql -uroot可以直接连接成功
  * 输入sudo mysql -uroot -p后回车输入任意password也可以直接连接成功
  * 输入mysql -h 127.0.0.1 -P 3306 -uroot -p提示Access denied for user ‘root’@’localhost’
  * /etc/mysql/debian.cnf文件中pasword没有密码
  
#### 原因
  * 需要给root设置password
  * 需要将用户表中plugin字段由auth_plugin设置成mysql_native_password
  
#### 解决步骤
```
sudo mysql -uroot

use mysql;
update user set password=password('yourpassword') where user='root';
update user set plugin='mysql_native_password' where user='root';
flush privileges;
exit;
```

#### 参考
[树莓派mysql无需密码连接的问题](https://blog.csdn.net/a791693310/article/details/80612573)