title: 解决mac在QQ视频时候，网页上的视频声音突然变小
date: 2016-10-06 10:57:07
tags: [mac,qq]
---
1. 打开QQ，先不要视频。   
2. 打开Mac自带的终端(Terminal)，输入以下代码然后回车，可能需要输入系统密码
`printf "p *(char*)(void(*)())AudioDeviceDuck=0xc3\nq" | lldb -n QQ`    
3. 然后就可以视频或语音了，拨出和接收视屏声音都不会变小。    
代码最后的QQ是程序的名字，如果你想用在其他程序上，改成其他程序的名字即可。    
