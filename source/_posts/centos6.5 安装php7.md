title: 安装php7
date: 2015-12-09 12:30:54
tags: [php7,centos6,centos]
---
### 操作系统
centos6.5 cpu 1核 内存1GB(腾讯云)
### 扩展yum源
`wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm`   
`wget https://centos6.iuscommunity.org/ius-release.rpm`   
`rpm -ivh epel-release-latest-6.noarch.rpm`   
`rpm -ivh ius-release.rpm`
<!-- more -->
### 安装依赖
```shell
yum install -y gcc gcc-c++  make zlib zlib-devel pcre pcre-devel  libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel libxml2 libxml2-devel glibc glibc-devel glib2 glib2-devel bzip2 bzip2-devel ncurses ncurses-devel curl curl-devel e2fsprogs e2fsprogs-devel krb5 krb5-devel openssl openssl-devel openldap openldap-devel nss_ldap openldap-clients openldap-servers bison
```

### 下载php7源码
`git clone https://git.php.net/repository/php-src.git`

#### 进入项目
`cd php-src`
#### 先执行
`./buildconf`
#### 在执行
`./configure --prefix=/usr/local/php7 \
--with-config-file-path=/usr/local/php7/etc \
--with-mcrypt=/usr/include \
--with-mysql=mysqlnd \
--with-mysqli=mysqlnd \
--with-pdo-mysql=mysqlnd \
--with-gd \
--with-iconv \
--with-zlib \
--enable-xml \
--enable-bcmath \
--enable-shmop \
--enable-sysvsem \
--enable-inline-optimization \
--enable-mbregex \
--enable-fpm \
--enable-mbstring \
--enable-ftp \
--enable-gd-native-ttf \
--with-openssl \
--enable-pcntl \
--enable-sockets \
--with-xmlrpc \
--enable-zip \
--enable-soap \
--without-pear \
--with-gettext \
--enable-session \
--with-curl \
--with-jpeg-dir \
--with-freetype-dir \
--enable-opcache`

#### 建立软连接把执行程序链到默认目录
`ln -s /usr/local/php/bin/php /usr/bin/php`

### 配置

`cp php.ini-production /usr/local/php/etc/php.ini`
`cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm`
`chmod +x /etc/init.d/php-fpm`
`cp /usr/local/php/etc/php-fpm.conf.default   /usr/local/php/etc/php-fpm.conf`
`cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf`
#### 配置opcache
`vim /usr/local/php/etc/php.ini`
#### 加入
`zend_extension=opcache.so`

### 安装nginx
`wget http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm`   
`rpm ivh nginx-release-centos-6-0.el6.ngx.noarch.rpm `
`yum install nginx `
#### 修改
`vim /usr/local/php/etc/php-fpm.d/www.conf`
`user = nginx`    
`group = nginx`
#### 启动nginx
`/etc/init.d/php-fpm start`


配置php与nginx    
```
server {
  
    listen       80;
    server_name  tx.pupued.com;

    root   /var/www;
    location / {
        index index.html index.htm index.php;
        if (!-e $request_filename) {
            rewrite . /index.php last;
        }
    }

    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    location ~ /\.ht {
        deny  all;
    }
}
```

### 最后 
`service nginx start`




### 安装php7 redis  扩展
`wget https://github.com/phpredis/phpredis/archive/php7.zip`   
`unzip php7`   
`cd phpredis-php7`   
`/usr/local/php/bin/phpize`    
`./configure  --with-php-config=/usr/local/php/bin/php-config`    
`make  &&  make  install`    
#### 然后修改php.ini文件增加一行：
`vim /usr/local/php/etc/php.ini`    
`extension=redis.so`    
`/etc/init.d/php-fpm restart`    
 
 ###### 2015-12-09







