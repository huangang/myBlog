title: centos7安装docker
date: 2016-01-17 14:06:57
tags: [centos7,docker,centos]
---
阿里云的centos7系统
(不用centos6因为升级内核什么的各种问题和坑)
<!-- more -->
``` bash
yum update
yum install docker
service docker start #启动 Docker 服务
#或者使用`docker -d` 来启动
chkconfig docker on #随系统启动自动加载
```
