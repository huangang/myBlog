title: 升级macOS Ventura git 登录失效
date: 2023-08-14 09:25:34
tags: [git, macOS, Ventura]
---
最近升级到 macOS Ventura 版本, 导致以前的git ssh都失效。    
经过查证，macOS Ventura 内置使用了 OpenSSH_9.0p1，根据 OpenSSH 发行说明 可以得知，从 OpenSSH 8.8/8.8p1 版本开始，就默认关闭了 ssh-rsa 算法。那么 macOS Ventura 内置使用的 OpenSSH_9.0p1 也是默认关闭了 ssh-rsa 算法。

重新启用 RSA/SHA1（临时方案）

```shell
vi ~/.ssh/config
```

写入
``` shell
# 在 ~/.ssh/config 文件的对应主机配置里新增2行：
Host xxx-host
	HostkeyAlgorithms +ssh-rsa
	PubkeyAcceptedAlgorithms +ssh-rsa
```