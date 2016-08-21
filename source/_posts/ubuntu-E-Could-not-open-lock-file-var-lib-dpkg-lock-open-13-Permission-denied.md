title: 解决ubuntu E:Could not open lock file /var/lib/dpkg/lock - open (13:Permission denied)
date: 2016-03-02 09:35:19
tags: [ubuntu]
---
解决方案：

``` bash
sudo rm -rf /var/lib/dpkg/lock    
sudo rm -rf /var/cache/apt/archives/lock     
sudo apt-get update      
sudo dpkg --configure -a      
sudo apt-get upgrade -y    
```
