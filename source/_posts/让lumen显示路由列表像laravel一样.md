title: 让lumen显示路由列表像laravel一样
date: 2016-04-06 12:37:21
tags: [lumen,laravel]
---
## 安装

##### 1. 执行       
`composer require appzcoder/lumen-routes-list`    
    
    
##### 2. 增加 service provider 到 **bootstrap/app.php** 这个文件.     
`$app->register(Appzcoder\LumenRoutesList\RoutesCommandServiceProvider::class);`     

##### 3. 运行 **composer update**     

## 命令

```
php artisan route:list
```


## 项目地址

<a href="https://github.com/appzcoder/lumen-route-list/">lumen-route-list</a>

