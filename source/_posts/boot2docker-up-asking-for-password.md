title: 碰到`docker@localhost's password`的解决办法
date: 2016-01-21 08:49:39
tags: [docker,boot2docker]
---
执行下面
```
rm ~/.ssh/id_boot2docker* && boot2docker delete && boot2docker -v init
boot2docker up
eval "$(boot2docker shellinit)"
```