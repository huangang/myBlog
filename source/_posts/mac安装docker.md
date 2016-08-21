title: Mac 安装docker  
date: 2015-12-10 18:12:39
tags: [docker,mac]
---
`brew cask install virtualbox`     
`brew install boot2docker`   
<!-- more -->
~~`brew install docker-compose docker-machine docker-swarm`~~    
由于国内被强只能翻墙去下载boot2docker.iso[下载地址](https://github.com/boot2docker/boot2docker/releases)   
下载完成后复制到 `/Users/username/.boot2docker`,然后   
`boot2docker -v init`   
`boot2docker start`   
`eval "$(boot2docker shellinit)"`    
最后查看信息`docker version`

## boot2docker常用命令
`boot2docker init` 初始化   
`boot2docker start` 启动   
`boot2docker stop` 停止   
`boot2docker delete` 删除   
`boot2docker status` 查看状态   
`boot2docker ssh` 登录

## docker常用命令 
`docker version` 查看docker版本   
`docker info` 显示docker系统的信息   
`docker search <镜像名:tag>` 搜索镜像    
`docker run -i -t <容器名orID> sh` 登录容器   
`docker ps`   
`docker ps -a`为查看所有的容器，包括已经停止的。   
`docker attach <容器名orID>` 进入容器            
`docker rm` 删除所有容器   
`docker rm <容器名orID>` 删除所有容器   
`docker stop <容器名orID>` 停止一个容器   
`docker start <容器名orID>` 启动一个容器   
`docker kill <容器名orID>` 杀死一个容器   
`docker images` 查看所有镜像   
`docker rmi` 删除所有镜像   
`docker rmi <镜像名:tag>` 删除一个镜像  
`docker pull <镜像名:tag>` 拉取(下载)镜像