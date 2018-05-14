title: 修复在macos brew link python 的错误
date: 2018-05-14 13:56:59
tags: [mac, brew, python]
---
最近用brew link python的时候出现这个问题`Linking /usr/local/Cellar/python/2.7.14_3... Error: Permission denied @ dir_s_mkdir - /usr/local/Frameworks`    
解决办法
 ```bash
sudo mkdir /usr/local/Frameworks   
sudo chown -R $(whoami) /usr/local/Frameworks   
brew link python     
```
