title: 解决用 pecl 安装 php 扩展的时候 /usr/local/Library/ENV/4.3/sed 报错
date: 2016-09-18 07:38:52
tags: [php,pecl]
---
```
vi `which phpize`   
```
找到 `SED="/usr/local/Library/ENV/4.3/sed"` 改成 `SED="/usr/bin/sed"`