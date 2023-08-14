title: 解决Xcode10报错library not found for -libstdc++.6.0.9
date: 2019-02-16 10:24:54
tags: [mac,xcode]
---
苹果在XCode10和iOS12中移除了libstdc++这个库，由libc++这个库取而代之，
苹果的解释是libstdc++已经标记为废弃有5年了，建议大家使用经过了llvm优化过并且全面支持C++11的libc++库。
临时解决方法:将xcode9中 libstdc++ 库导入到xcode10中两个位置，一套是模拟器的，一套是设备的

```
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS12.1.sdk/usr/lib/
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/usr/lib/
```
[libstdc++.6.0.9下载地址](https://github.com/MeteoriteMan/Assets/blob/master/Assets/libstdc%2B%2B.6.0.9.tbd)
注意:下载的libstdc++.6.0.9最下面的`...`三个点需要去掉