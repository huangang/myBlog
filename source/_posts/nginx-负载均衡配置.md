title: nginx 负载均衡配置
date: 2016-10-17 10:19:03
tags: [nginx,负载均衡]
---
```
upstream api.com {
    ip_hash;
    server 127.0.0.1:81 weight=2 max_fails=3 fail_timeout=15;
    server 127.0.0.1:82 weight=3;
    server 127.0.0.1:83 backup;
    server 127.0.0.1:84 down;
    server 127.0.0.1:85 max_conns=1000;
}
```
<!-- more -->   
## 1.轮循（默认） 
轮询即Round Robin，根据Nginx配置文件中的顺序，
依次把客户端的Web请求分发到不同的后端服务器上

## 2、最少连接 least_conn;
Web请求会被转发到连接数最少的服务器上。

## 3、IP地址哈希 ip_hash;
前述的两种负载均衡方案中，同一客户端连续的Web请求可能会被分发到不同的后端服务器进行处理，
因此如果涉及到会话Session，那么会话会比较复杂。常见的是基于数据库的会话持久化。
要克服上面的难题，可以使用基于IP地址哈希的负载均衡方案。
这样的话，同一客户端连续的Web请求都会被分发到同一服务器进行处理。

## 4、基于权重 weight
基于权重的负载均衡即Weighted Load Balancing，
这种方式下，我们可以配置Nginx把请求更多地分发到高配置的后端服务器上，
把相对较少的请求分发到低配服务器。


`weight` 
默认为1，将请求平均分配给每台server  
`backup` 
备份机，所有服务器挂了之后才会生效   
`down` 
标识某一台server不可用。可能能通过某些参数动态的激活它吧，要不真没啥用。   
`fail_timeout` 
默认为10秒。某台Server达到max_fails次失败请求后，在fail_timeout期间内，nginx会认为这台Server暂时不可用，不会将请求分配给它    
`max_fails`  
默认为1。某台Server允许请求失败的次数，超过最大次数后，在fail_timeout时间内，新的请求将不会分配给这台机器。如果设置为0，Nginx会将这台Server置为永久无效状态，然后将请求发给定义了proxy_next_upstream, fastcgi_next_upstream, uwsgi_next_upstream, scgi_next_upstream, and memcached_next_upstream指令来处理这次错误的请求。   
`max_conns` 
限制分配给某台Server处理的最大连接数量，超过这个数量，将不会分配新的连接给它。默认为0，表示不限制。注意：1.5.9之后的版本才有这个配置

