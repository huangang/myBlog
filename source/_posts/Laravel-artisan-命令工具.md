title: Laravel5 artisan 命令工具
date: 2016-01-05 13:32:03
tags: [laravel]
---
## Options(选项): 
```shell
php artisan --help (-h)           显示帮助信息      
php artisan --quiet (-q)          不输出任何消息      
php artisan --version (-V)        显示此laravel框架的版本     
php artisan --ansi                强制用ANSI码输出     
php artisan --no-ansi             禁用用ANSI码输出     
php artisan --no-interaction (-n) 不要问任何交互式问题     
php artisan --env[=EVN]           在环境命令下运行  
php artisan --verbose (-v|vv|vvv) 增加冗长的消息：1 正常输出 2 更加详细的输出 3调试输出     
```
<!-- more -->
## Available commands(可用的命令):
``` shell
php artisan clear-compiled  清除编译后的类文件
php artisan down            将站点设为维护状态
php artisan env             显示当前框架环境
php artisan help            显示命令行的帮助
php artisan list            列出命令
php artisan migrate         运行数据库迁移
php artisan optimize        为了更好的框架去优化性能
php artisan serve           使用PHP内置的开发服务器启动应用
php artisan tinker          进入与当前应用环境绑定的 REPL 环境，相当于 Rails 框架的 rails console 命令
php artisan up              将站点设回可访问状态
```
#### app
``` shell
php artisan app:name        设置应用程序命名空间
```
#### cache
```
php artisan cache:clear     清除应用程序缓存
php artisan cache:table     创建一个缓存数据库表的迁移
```
#### config
``` shell
php artisan config:cache    创建一个加载配置的缓存文件 
php artisan config:clear    删除配置的缓存文件
```
#### db
``` shell
php artisan db:seed         对数据库填充种子数据，以用于测试
```
#### event
``` shell
php artisan event:generate  自动生成Artisan全部文件，包括事件和对应的处理程序。
```
#### key
``` shell
php artisan key:generate    设置程序密钥
```
#### make
``` shell
php artisan make:auth       框架基本登录和注册的试图和路由
php artisan make:console    生成一个artisan命令
php artisan make:controller 生成一个控制器
php artisan make:event      生成一个事件类
php artisan make:job        生成一个job类
php artisan make:listener   生成一个event listener类
php artisan make:middleware 生成一个中间件
php artisan make:migration  生成一个迁移文件
php artisan make:model      生成一个模型类
php artisan make:policy     生成一个policy类
php artisan make:provider   生成一个服务提供商的类
php artisan make:request    生成一个表单消息(request)类
```
#### migrate
``` shell
php artisan migrate:install 创建一个迁移库文件
php artisan migrate:refresh 复位并重新运行所有的迁移
php artisan migrate:reset   回滚全部数据库迁移
php artisan migrate:rollback回滚最后一个数据库迁移
php artisan migrate:status  显示列表的迁移 上/下
```
#### queue
``` shell
php artisan queue:failed        列出全部失败的队列工作
php artisan queue:failed-table  创建一个迁移的失败的队列数据库工作表
php artisan queue:flush         清除全部失败的队列工作
php artisan queue:forget        删除一个失败的队列工作
php artisan queue:listen        监听一个确定的队列工作
php artisan queue:restart       重启现在正在运行的所有队列工作
php artisan queue:retry         重试一个失败的队列工作
php artisan queue:table         创建一个迁移的队列数据库工作表
php artisan queue:work          进行下一个队列任务
```
#### route
``` shell
php artisan route:cache    为了更快的路由登记，创建一个路由缓存文件
php artisan route:clear    清除路由缓存文件
php artisan route:list     列出全部的注册路由 
```
#### schedule
``` shell
php artisan schedule:run   运行预定命令
```
#### session
``` shell
php artisan session:table  创建一个迁移的SESSION数据库工作表
```
#### vendor
``` shell
php artisan vendor:publish 发表一些可以发布的有用的资源来自提供商的插件包
```
#### view
``` shell
php artisan view:clear     清除所有已编译的视图文件
```