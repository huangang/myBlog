title: centos 安装java,mysql和tomcat
date: 2016-01-10 13:27:24
tags: [java,mysql,tomcat,centos]
---
# 安装JDK  
``` bash
yum list java*     
yum -y install java-1.7.0-openjdk*   
```
<!-- more -->
如果安装不了高版本的java,需要扩展yum源,执行以下命令
``` bash
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm  
wget https://centos6.iuscommunity.org/ius-release.rpm`   
rpm -ivh epel-release-latest-6.noarch.rpm  
rpm -ivh ius-release.rpm
```

# 安装mysql
> 删除已安装的mysql`yum remove mysql-libs`
``` bash
yum list mysql*
yum install mysql55-server* -y
# 第一次启动mysql
service mysqld start #以后启动也是这个
```
### 其他命令
``` bash
service mysqld restart #重启
service mysqld stop #关闭
```
### 配置开机启动
``` bash
chkconfig --list | grep mysqld ＃查看是不是开机启动
> mysqld         	0:关闭	1:关闭	2:关闭	3:关闭	4:关闭	5:关闭	6:关闭
`chkconfig mysqld on`设置开机启动
chkconfig --list | grep mysqld ＃再次查看是不是开机启动
> mysqld         	0:关闭	1:关闭	2:启用	3:启用	4:启用	5:启用	6:关闭
```
### 为root账号设置密码
`mysqladmin -u root password 'new-password'`　　
`mysql -u root -p ##通过这个命令登录我们的mysql数据库了`

###  mysql允许root用户在任何地方进行远程登录(为了本地开发方便)
`mysql -u root -p` ## 用root用户登录
``` bash
mysql> use mysql;
Database changed
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'youpassword' WITH GRANT OPTION; ##进行授权操作
Query OK, 0 rows affected (0.00 sec)
mysql> FLUSH PRIVILEGES; ## 重载授权表
Query OK, 0 rows affected (0.00 sec)
mysql> exit; ## 退出mysql数据库
Bye
```

# 安装tomcat
``` bahs
yum clean all
yum update -y
yum list tomcat*
yum install tomcat tomcat-webapps tomcat-admin-webapps
```
### tomcat 命令
``` bash
tomcat start 开启
tomcat start-security  安全管理器中开启
tomcat stop 关闭
tomcat version 版本号
```
开启后访问http://ip:8080
tomcat配置文件夹 `/etc/tomcat/`
webapps路径： `/usr/share/tomcat/webapps`