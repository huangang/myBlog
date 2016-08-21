title: mac 安装mongodb
date: 2016-03-13 19:53:29
tags: [mac,mongodb]
---
`brew install mongodb` 安装mongodb
`ln -sfv /usr/local/opt/mongodb/*.plist ~/Library/LaunchAgents` 这个一定要执行
`launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist` 开机启动
<!-- more -->
### 启动|停止
```
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
```
### 设置快捷命令
``` bash
vim ~/.bash_aliases 
## 写入下面内容
alias mongo.start='launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
alias mongo.stop='launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
alias mongo.restart='mongo.stop && mongo.start'
```
然后
```
vim ~/.bash_profile
[[ -f ~/.bash_aliases ]] && . ~/.bash_aliases  ## 写入这个
source .bash_profile ## 更新bash_profile
```
就可以用`mongo.start` `mongo.stop` `mongo.restart` 来进行开启,关闭,重启 mongodb的服务了
