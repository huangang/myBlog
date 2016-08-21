title: MAC下ssh免密码登录远程服务器
date: 2016-03-17 17:26:29
tags: [mac,ssh,linux]
---
## 生成密钥。
在终端下执行命令：
`ssh-keygen -t rsa -C  'your email@domain.com'`
一路回车，各种提示按默认不要改，等待执行完毕。然后执行：
`ls ~/.ssh`
可以看到两个密钥文件：id_rsa（私钥） id_rsa.pub（公钥）
<!-- more -->
## 将公钥复制到ssh服务器
将前一步骤生成的公钥~/.ssh/id_rsa.pub文件，复制到ssh服务器对应用户下的~/.ssh/authorized_keys文件,没有则新建一个就行.

## 配置本地ssh config文件,实现快捷登录
`vim ~/.ssh/config` 若没有该文件，直接新建即可
添加文件内容格式如下：
```
Host                     server #自定义别名
HostName                 hostname  #替换为你的ssh服务器ip或domain
Port                     port #ssh服务器端口，默认为22
User                     user #ssh服务器用户名
PreferredAuthentications publickey  #有些情况或许需要加入此句，优先验证类型ssh
IdentityFile             ~/.ssh/id_rsa #第一个步骤生成的公钥文件对应的私钥文件
```
ssh server #server 是~/.ssh/config文件配置的别名
就可以直接登陆了

