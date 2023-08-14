title: MAMP PRO 3.3 安装phpredis 扩展
date: 2015-6-28 18:28:30
tags: [mac,MAMP,php,redis]
---
phpredis扩展包地址：   
https://github.com/nicolasff/phpredis    
1、下载php源码 (http://php.net/downloads.php 选择php5.6.10)     
<!-- more -->
在 /Applications/MAMP/bin/php/php5.6.10/ 目录下建立include     
/Applications/MAMP/bin/php/php5.6.10/include下建立php目录，并把php源代码放进去     

并在当前目录编译下：     
`./configure`   

2、编译phpredis    

`git clone https://github.com/nicolasff/phpredis.git //随便找个目录把源代码拉下来`    
`cd phpredis // 进入到phpredis目录`    
`phpize //可能会报错，如果需要直接安装 brew install automake`    
`./configure --with-php-config=/Applications/MAMP/bin/php/php5.6.10/bin/php-config`    
`make && make install`

如果安装正常会提示：     
`Installing shared extensions:     /Applications/MAMP/bin/php/php5.6.10/lib/php/extensions/no-debug-non-zts-20131226/`    

3、最后一步，修改php.ini 配置文件    
添加：extension=redis.so     
重启mamp，打开phpinfo() , 会看到phpredis模块。      