title: laravel查看model具体执行的sql语句
date: 2016-06-18 16:05:34
tags: [laravel]
---
``` php
DB::connection()->enableQueryLog(); // 开启查询日志
User::find(1);//查询用户id为1的用户
$queries = DB::getQueryLog(); // 获取查询日志
$last_query = end($queries);
var_dump($last_query); // 即可查看执行的sql，传入的参数等等
```
<!-- more --> 
出现的结果为
``` 
Array
(
    [query] => select * from `users` where `users`.`id` = ? limit 1
    [bindings] => Array
        (
            [0] => 1
        )

    [time] => 86.39
)
```