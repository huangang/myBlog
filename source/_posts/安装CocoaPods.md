title: 安装CocoaPods
date: 2016-06-19 14:42:52
tags: [pod]
---
## 使用brew安装
最简单的安装方法`brew install Caskroom/cask/cocoapods`,但是这样安装后pod在国内各种慢
<!-- more -->
## 使用gem安装
`gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/`先把gem源切换到淘宝的源    
接着`sudo gem install cocoapods`就ok了,以后`pod install`速度也不会慢
