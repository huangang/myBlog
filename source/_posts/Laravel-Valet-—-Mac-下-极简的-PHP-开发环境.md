title: Laravel Valet — Mac 下 极简的 PHP 开发环境
date: 2016-05-09 13:57:05
tags: [laravel,mac,valet,php]
---
## 安装valet
1.使用`brew update`安装或更新[Homebrew](http://brew.sh/index_zh-cn.html)到最新版本    
2.通过运行 `brew services list`确保 `brew services`有效并且能获取到正确的输出，如果无效，则需要添加。   
3.通过Homebrew安装PHP 7.0： `brew install php70`
如果无法安装,可能是确实PHP7的源则执行下面
``` bash
brew tap homebrew/dupes
brew tap homebrew/versions
brew tap homebrew/homebrew-php
```
4.安装composer `brew install composer`   
5.编辑`~/.bash_profile`这个文件,加入`export PATH="~/.composer/vendor/bin:$PATH"`,然后执行`source ~/.bash_profile`   
6.通过[Composer](https://getcomposer.org/)安装Valet： `composer global require laravel/valet`（确保`~/.composer/vendor/bin`在系统路径中）    
7.运行 `valet install`命令，这将会配置并安装Valet和DnsMasq，然后注册Valet后台随机启动。     
8.安装完Valet后，尝试使用命令如 `ping foobar.dev`在终端ping一下任意*.dev域名
<!-- more --> 
## 问题
如果ping不成功
```
rm /usr/local/etc/dnsmasq.conf
valet install
```
## 创建站点
```
cd galactica
valet link galactica
```
这样访问`galactica.dev`就是你新创建的站点

