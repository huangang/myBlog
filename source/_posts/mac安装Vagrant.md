title: mac安装Vagrant
date: 2016-03-11 22:03:50
tags: [mac,vagrant]
---
`brew cask install virtualbox` 安装virtualbox虚拟机
`brew cask install vagrant` 安装vagrant <!-- more -->
### vagrant添加laravel box
`vagrant box add laravel/homestead` 添加laravel官方提供的box
`git clone https://github.com/laravel/homestead.git` Homestead，找一个目录用来存放虚拟机配置的去执行这句命令
`cd Homestead`
`mkdir ~/Code` 创建共享目录
`vagrant up` 启动box
`vagrant ssh` 进入box
`vagrant suspend` 关闭box
