title: mac安装docker-toolbox
date: 2016-08-03 09:41:22
tags: [mac,docker,docker-toolbox]
---
## 安装docker-toolbox
```
brew cask install virtualbox
brew cask install docker-toolbox
```
如果你本地没有`default`虚拟机则执行   
`docker-machine create --driver virtualbox default`
<!-- more -->
## 加速docker
请确认你的 Docker Toolbox 已经启动，并执行下列命令（请将 加速地址 替换为在[加速器](https://www.daocloud.io/mirror#accelerator-doc)页面获取的专属地址）
```
docker-machine ssh default   
sudo sed -i "s|EXTRA_ARGS='|EXTRA_ARGS='--registry-mirror=加速地址 |g" /var/lib/boot2docker/profile
exit   
docker-machine restart default   
docker-machine env   
```