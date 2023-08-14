title: centos 7 安装jxcore编译环境
date: 2017-10-30 13:19:13
tags: [centos7,jxcore, jx]
---
# 下载
到这个地址https://github.com/thaliproject/jxbuild/blob/master/distribute.md   
下载最新linux环境的(jx_linux64v8.zip)，然后解压出`jx`，执行`mv jx /usr/bin/`
<!-- more -->
# 问题
执行`jx -v`可能会看到
```
jx: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.20' not found (required by jx)   
jx: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.21' not found (required by jx)
```
这个是很好需要安装高版本的gcc 

# 安装gcc5解决问题
`vi /etc/yum.repos.d/Fedora-Core23.repo`
写入    
```
[warning:fedora]
name=fedora
mirrorlist=http://mirrors.fedoraproject.org/mirrorlist?repo=fedora-23&arch=$basearch
enabled=1
gpgcheck=0
```
这个时候执行`yum install gcc --enablerepo=warning:fedora`就行
安装好后执行`jx -v`可看到`v0.10.40`代表安装成功了
