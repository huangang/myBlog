title: 搭建Shadowsocks服务器
date: 2016-01-15 09:20:54
tags: [Shadowsocks]
---
### 操作系统:Centos 6 系统的VPS 
<!-- more -->
## 1. 通过ssh登录你的VPS上。            
## 2.执行以下命令            
``` bash
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```
## 3.输入你想要设置的密码，并回车，再次回车，确认安装        
![3](http://huangang.pupued.com/160C1CBA-6A00-4B8A-AD72-19BC6A44D020.png)   
## 4. 等待2分钟左右，即可安装成功，安装成功之后就会通过屏幕输出，您的IP地址，端口，密码，及加密方式。              
![4](http://huangang.pupued.com/FA580353-24DF-4122-A39C-0C82E1DEB387.png)
现在你就可以使用Shadowsocks了

> 如果想多用户使用,请配置 `/etc/shadowsocks.json` 这个文件。
配置模版：
```
{
    "server":"your_server_ip",
    "local_address": "127.0.0.1",
    "local_port":1080,
    "port_password":{
         "8989":"password0",
         "9001":"password1",
         "9002":"password2",
         "9003":"password3",
         "9004":"password4"
    },
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```

