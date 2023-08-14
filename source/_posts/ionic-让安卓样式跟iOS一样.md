title: ionic 让安卓样式跟iOS一样
date: 2016-03-13 06:29:24
tags: [ionic]
---
在config里面添加如下代码
``` js
.config(function($stateProvider, $urlRouterProvider, $ionicConfigProvider) {
  $ionicConfigProvider.tabs.style('standard'); // Tab风格
  $ionicConfigProvider.tabs.position('bottom'); // Tab位置
  $ionicConfigProvider.navBar.alignTitle('center'); // 标题位置
  $ionicConfigProvider.navBar.positionPrimaryButtons('left'); // 主要操作按钮位置
  $ionicConfigProvider.navBar.positionSecondaryButtons('right'); //次要操作按钮位置
});
```
