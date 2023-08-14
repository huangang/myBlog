title: 使用yum提示Error:rpmdb open failed
date: 2016-01-01 07:43:40
tags: [yum]
---
最近使用yum update 提示 Error: rpmdb open failed错误
<!-- more -->
原因是RPM数据库被破坏
重建数据库后恢复正常
``` shell
cd /var/lib/rpm/     
for i in `ls | grep 'db.'`;do mv $i $i.bak;done    
rpm --rebuilddb    
yum clean all    
```