title: mac 安装 mysql
date: 2015-12-27 11:45:29
tags: [mac,mysql]
---
## 安装MySQL
`brew install mysql`
MySQL开机启动：
<!-- more -->
```
ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
```
安装完成之后开启MySQL安全机制：
`/usr/local/opt/mysql/bin/mysql_secure_installation`

`> secure enough. Would you like to setup VALIDATE PASSWORD plugin?`
输入y
```
There are three levels of password validation policy:
LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file
Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 0
Please set the password for root here.
```
根据情况选择密码的要求,可以输入`0 or 1 or 2`
`Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No):`
输入n
`Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No):`
输入y
`Remove anonymous users? (Press y|Y for Yes, any other key for No):`
输入y
`Disallow root login remotely? (Press y|Y for Yes, any other key for No): `
输入y
`Remove test database and access to it? (Press y|Y for Yes, any other key for No):`
 输入y
`Reload privilege tables now? (Press y|Y for Yes, any other key for No): `
输入y

## 连接数据库
`mysql -uroot -p`
## 输入root用户的密码,然后你可以看到MySQL console:
```
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
mysql>
```
## 退出MySQL console
```
mysql> \q
Bye
```
## 设置mysql快捷服务控制命令
为了后面管理方便，将命令 alias 下，`vim ~/.bash_aliases` 输入一下内容：
```
alias mysql.start="launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist"
alias mysql.stop="launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist"
alias mysql.restart='mysql.stop && mysql.start'
#让快捷命令生效
echo "[[ -f ~/.bash_aliases ]] && . ~/.bash_aliases" >> ~/.bash_profile     
source ~/.bash_profile
```
参考资料：[Install Nginx, PHP-FPM, MySQL and phpMyAdmin on OS X Mavericks using Homebrew](http://blog.frd.mn/install-nginx-php-fpm-mysql-and-phpmyadmin-on-os-x-mavericks-using-homebrew/)

   


   

