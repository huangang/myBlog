title: laravel 全局函数配置
date: 2016-03-22 09:40:16
tags: [laravel]
---
1.在“app”目录下创建“helpers.php”文件。
2.修改composer.json文件。添加：
``` json
"autoload": {  
    ...  
    "files": [  
      "app/helpers.php"  
    ]  
  },  
```
3.执行:
`composer dump-autoload`