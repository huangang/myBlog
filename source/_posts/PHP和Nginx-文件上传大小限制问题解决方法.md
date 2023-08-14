title: php和nginx 文件上传大小限制解决方法
date: 2016-05-16 19:34:18
tags: [php,nginx]
---
## 1、修改你的web站对应nginx的配置文件，把 client_max_body_size 的值设置为你想设置的值。比如：
```
server {
    listen       80;
    server_name  app.com;
    client_max_body_size 25m;
    access_log  /var/log/nginx/app.access.log main;  
    location / {
           root   /var/app;
           index  index.html index.htm index.php;
    }
    ...
}
```
<!-- more -->
## ２、修改php.ini
```
upload_max_filesize = 30M 
post_max_size = 20M 
memory_limit = 30M
max_execution_time=300
file_uploads = On
默认允许HTTP文件上传，此选项不能设置为OFF。
upload_tmp_dir =/tmp/www
```