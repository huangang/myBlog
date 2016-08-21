title: mac nginx的问题搜集和解决
date: 2016-03-14 11:24:37
tags:[mac,nginx]
---
`mac nginx: [emerg] bind() to 0.0.0.0:80 failed (13: Permission denied)`
碰到这个问题
lsof -i tcp:80,查看端口号,关闭可能占有端口的程序
还是不行就
``` bash
sudo chown root:wheel /usr/local/Cellar/nginx/1.8.1/bin/nginx 
sudo chmod u+s /usr/local/Cellar/nginx/1.8.1/bin/nginx 
```
