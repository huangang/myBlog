title: docker容器启动后添加端口映射
date: 2017-01-06 14:00:00
tags: [docker, iptables]
from: https://my.oschina.net/u/266752/blog/541433
---

## 概要

网上有许多人在查找关于容器启动后能否进行端口映射的问题。我曾经也问过度娘，很遗憾我没找到。本文就这个问题给出一个解决方法，旨在抛砖引玉。本文的思路是使用iptables的端口转发，这也是docker端口映射内部的实现机制，只不过我是显示地写出来罢了，为的就是让查找这个问题的人对docker的端口映射有一个直观的了解。
<!-- more --> 
**结论：容器启动后是可以添加端口映射的，但不建议手工添加，最好使用docker提供的功能。**

## 步骤

创建两个容器并进行了端口映射，结果如图所示：

![](http://huangang.pupued.com/131229_OhXt_266752.png)

假如，我start一个容器，其内部IP为172.17.0.5，并在容器内部启动了80端口。

FORWARD规则链我们不用管它，docker已经帮我们写好了，我们只需要关心NAT中的几条链即可。

查看NAT表中的PREROUTING链
```
iptables -t nat --list-rules POSTROUTING
```
![](http://huangang.pupued.com/131753_i0yc_266752.png)

从上面可以看出，iptables将满足条件的数据都转发到了DOCKER链上去了。

查看NAT表中的DOCKER链
```
iptables -t nat --list-rules DOCKER
```
![](http://huangang.pupued.com/132524_5fkC_266752.png)

仿照上图，我们添加一条自己的映射规则，将宿主的8082端口映射到172.17.0.5的80端口上去，规则如下：

``` 
iptables -t nat -A DOCKER ! -i docker0 -p tcp -m tcp --dport 8082 -j DNAT --to-destination 172.17.0.5:80
```
查看NAT表中的POSTROUTING链
![](http://huangang.pupued.com/132027_kvzk_266752.png)

仿照上图中的规则，书写的规则如下：
``` bash
 iptables -t nat -A POSTROUTING -s 172.17.0.5/32 -d 172.17.0.5/32 -p tcp -m tcp --dport 80 -j  MASQUERADE
```
查看FILTER表中的DOCKER链
```
iptables --list-rules DOCKER
```
![](http://huangang.pupued.com/133616_vQYj_266752.png)

仿照上图书写规则如下：
``` 
 iptables -t filter -A DOCKER -d 172.17.0.5/32 ! -i docker0 -o docker0 -p tcp -m tcp --dport 80 -j ACCEPT
```
## 结果

虽然IP为172.17.0.5的容器没有开启端口映射，如下图所示：
![](http://huangang.pupued.com/134008_c2g8_266752.png)

但我们依然能够通过访问宿主机(192.168.78.238)的8082端口来访问172.17.0.5的80端口，效果如下：

![](http://huangang.pupued.com/134500_g6vj_266752.png)


使用此方法有一个缺点，不能访问localhost:8082，也就是说如果想对localhost也进行转发，需要进行额外的配置。

## 结论

建议大家不要像我这样去做端口映射，我这么做只是为了阐述标题。

如果大家在容器中添加了一些东西，并开启了端口，同时呢，又想多复制几个这样的容器。建议大家把容器提交成镜像，然后使用docker提供的端口映射功能。

## 其他
如果上面命令不小心添加错了,把`-A`改成`-D`,如下面
```
iptables -t nat -D DOCKER ! -i docker0 -p tcp -m tcp --dport 8082 -j DNAT --to-destination 172.17.0.5:80
iptables -t nat -D POSTROUTING -s 172.17.0.5/32 -d 172.17.0.5/32 -p tcp -m tcp --dport 80 -j  MASQUERADE
iptables -t filter -D DOCKER -d 172.17.0.5/32 ! -i docker0 -o docker0 -p tcp -m tcp --dport 80 -j ACCEPT
```
这样就能把你写错或者不需要的规则删除