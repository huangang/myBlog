title: centos7 安装 docker-composer
date: 2017-05-13 17:07:19
tags: [centos7,centos,docker,docker-composer]
---
``` bash
yum update
yum install docker
service docker start #启动 Docker 服务
#或者使用`docker -d` 来启动
chkconfig docker on #随系统启动自动加载
curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
接下来就可以愉快的使用`docker-compose`命令了