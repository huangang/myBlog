title: 平滑升级php
date: 2016-01-02 18:40:31
tags: [php]
---
## 添加资源库 - epel, ius
``` shell
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm       
wget https://centos6.iuscommunity.org/ius-release.rpm     
rpm -ivh epel-release-latest-6.noarch.rpm     
rpm -ivh ius-release.rpm
```
## 安装编译源
``` shell
yum install gcc gcc-c++ make cmake autoconf libtool \
openssl-devel libxml2-devel pcre-devel libcurl-devel jpeglib-devel \
db4-devel libjpeg-devel libpng-devel libXpm-devel gmp-devel libc-client-devel \
freetype-devel openldap-devel libmcrypt-devel libxslt-devel
```
<!-- more -->

## 安装php5.5.30
下载php5.5.30
`wget http://ca1.php.net/distributions/php-5.5.30.tar.gz`
解压缩安装包
`tar zxvf php-5.5.30.tar.gz`
进入目录
`cd php-5.5.30`
编译安装
``` shell
./configure \
--prefix=/usr/local/etc/php/php-5.5.30 \
--with-config-file-path=/usr/local/etc/php/php-5.5.30/etc \
--with-config-file-scan-dir=/usr/local/etc/php/php-5.5.30/etc/php.d \
--with-curl=/usr/local/lib \
--with-freetype-dir=/usr/lib64 \
--with-gd \
--with-gettext \
--with-iconv-dir=/usr/local/lib \
--with-jpeg-dir=/usr/lib64 \
--with-kerberos \
--with-ldap \
--with-ldap-sasl \
--with-libdir=lib64 \
--with-libxml-dir=/usr/lib64 \
--with-mcrypt \
--with-mhash \
--with-mysql \
--with-mysqli \
--with-openssl \
--with-pcre-regex=/usr \
--with-pdo-mysql=shared \
--with-pdo-sqlite=shared \
--with-pear=/usr/local/lib/php \
--with-png-dir=/usr/lib64 \
--with-xmlrpc \
--with-xsl \
--with-zlib \
--enable-fpm \
--enable-bcmath \
--enable-libxml \
--enable-inline-optimization \
--enable-gd-native-ttf \
--enable-mbregex \
--enable-mbstring \
--enable-opcache \
--enable-pcntl \
--enable-shmop \
--enable-soap \
--enable-sockets \
--enable-sysvsem \
--enable-xml \
--enable-zip \
--disable-rpath
make && make install
cp php.ini-production /usr/local/etc/php/php-5.5.30/etc/php.ini
cp sapi/fpm/php-fpm.conf /usr/local/etc/php/php-5.5.30/etc/php-fpm.conf
cp sapi/fpm/init.d.php-fpm /usr/local/etc/php/php-5.5.30/etc/php-fpm
```


## 安装phpredis-master
``` shell
wget https://github.com/phpredis/phpredis/archive/2.2.7.zip
unzip 2.2.7.zip 
cd phpredis-2.2.7
/usr/local/etc/php/php-5.5.30/bin/phpize
./configure \
--enable-redis \
--with-php-config=/usr/local/etc/php/php-5.5.30/bin/php-config
make && make install
``` 
## 配置php.ini
``` shell
vim /usr/local/etc/php/php-5.5.30/etc/php.ini
# 找到extension_dir
extension_dir = "/usr/local/etc/php/php-5.5.30/lib/php/extensions/no-debug-non-zts-20121212/"
extension = "pdo_mysql.so"
extension = "redis.so"
# 找到date.timezone
date.timezone = Asia/Shanghai
```

## 启动新安装的php
``` shell
ln -s /usr/local/etc/php/php-5.5.30/bin/php /usr/local/bin
ln -s /usr/local/etc/php/php-5.5.30/sbin/php-fpm  /usr/local/sbin
cp /usr/local/etc/php/php-5.5.30/etc/php-fpm /etc/rc.d/init.d/php-fpm#拷贝php-fpm到启动目录
chmod +x /etc/rc.d/init.d/php-fpm #添加执行权限
chkconfig php-fpm on #设置开机启动
service php-fpm stop
/etc/rc.d/init.d/php-fpm
```

## 备注
不够平滑,还是会有问题,继续探索.    
感觉要从centos安装多版本php,然后可以任意切换入手.
