title: mac卸载dmg安装的mysql
date: 2015-12-27 11:34:41
tags: [mac,mysql]
---
mac下用dmg安装了mysql，却没有卸载文件。只能用命令行进行手动卸载了。
<!-- more -->
``` shell
sudo rm /usr/local/mysql    
sudo rm -rf /usr/local/mysql*    
sudo rm -rf /Library/StartupItems/MySQLCOM      
sudo rm -rf /Library/PreferencePanes/My*     
vim /etc/hostconfig  (and removed the line MYSQLCOM=-YES-)     
rm -rf ~/Library/PreferencePanes/My*     
sudo rm -rf /Library/Receipts/mysql*     
sudo rm -rf /Library/Receipts/MySQL*    
sudo rm -rf /var/db/receipts/com.mysql.*     
```