title: 解决MacOS更改打开文件限制
date: 2017-12-18 16:54:17
tags: [mac]
---
最近用node进行文件读写操作的时候碰到   
`Unhandled rejection Error: ENFILE: file table overflow, open ...`   
的问题。
<!-- more -->
最后Google查得解决问题的方法，[这个用户的帖子（和答案）](https://superuser.com/questions/827984/open-files-limit-does-not-work-as-before-in-osx-yosemite/828010#828010)。
```bash
$ echo kern.maxfiles=65536 | sudo tee -a /etc/sysctl.conf
$ echo kern.maxfilesperproc=65536 | sudo tee -a /etc/sysctl.conf
$ sudo sysctl -w kern.maxfiles=65536
$ sudo sysctl -w kern.maxfilesperproc=65536
$ ulimit -n 65536 65536    
```

