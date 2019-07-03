title: openshift 命令行工具查看日志
date: 2019-07-03 15:53:49
tags: [openshift, mac]
---
> 因为有时候访问oc的web页面比较慢,而且日志只能看5000条
<!-- more -->
## 安装
``` bash
brew install openshift-cli
```

## 登陆
``` bash
oc login https://oc-service:port
```
输入用户名和密码
退出用这个`oc logout`

## 查看项目
``` bash
oc get pods
```
返回    
<details>
``` bash
NAME                        READY     STATUS      RESTARTS   AGE
testservice-6-fh58x          1/1       Running     1          94d
testservice-6-ql5km          1/1       Running     0          94d
```
</details>

## 查看日志
``` bash
oc logs $POD_NAME -f # -f 是为了保持一直查看,如果没有就是一次性把最新的日志返回然后结束了
```
如`oc logs testservice-6-fh58x -f`
> 注:一般看状态是`Running`的pod,状态是`Completed`一般表示构建容器的日志

## 多容器查看
安装 stern `brew install stern`    
查看日志 `stern testservice-`   

