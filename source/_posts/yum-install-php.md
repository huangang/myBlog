title: yum 安装稳定常用的php版本及扩展
date: 2016-01-01 00:01:33
tags: [php,yum]
---
## 添加资源库 - epel, ius(以centos6.5及以上为例)  
<!-- more -->
打开网址`https://ius.io/GettingStarted/`选择适合操作系统的资源库  

``` shell
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm       
wget https://centos6.iuscommunity.org/ius-release.rpm     
rpm -ivh epel-release-latest-6.noarch.rpm     
rpm -ivh ius-release.rpm 
```

接下来用yum命令,可以安装高版本的php,
`yum install php55u php55u-fpm php55u-mysql php55u-redis php55u-mbstring`
用`yum search xxx`来搜索自己所需要的软件如
`yum install php55u-pecl-redis`安装redis
## 安装nginx
访问`http://nginx.org/en/linux_packages.html`可以查看安装nginx最新版本的方法
现在的方法是

``` nginx
To set up the yum repository for RHEL/CentOS, create the file named /etc/yum.repos.d/nginx.repo with the following contents:
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/OS/OSRELEASE/$basearch/
gpgcheck=0
enabled=1
Replace “OS” with “rhel” or “centos”, depending on the distribution used, and “OSRELEASE” with “5”, “6”, or “7”, for 5.x, 6.x, or 7.x versions, respectively.         
```
然后执行以下命令
``` shell
$ yum install nginx
$ service nginx stop
$ service nginx start
```
就安装了最新版本的nginx,且启动了
## 安装swoole扩展
```
pecl install swoole
sudo vim /etc/php.ini #在最后加入extension=swoole.so
service php-fpm reload #查看phpinfo可以看到安装好swoole(php -m)
```
### 备注
用`cat /etc/redhat-release`查看centos系统版本号
`yum repolist`查看操作系统的资源库

