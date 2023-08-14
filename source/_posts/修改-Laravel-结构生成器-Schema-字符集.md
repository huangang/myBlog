title: 修改 Laravel 结构生成器 Schema 字符集
date: 2016-06-09 08:09:13
tags: [laravel,schema]
from: http://laravel.so/tricks/d4826dcc49dd47c670623b1acad5c6f4
---
在特定环境或许会碰到有些需要大小写区分的字符串字段，    

通过 Schema 生成的表默认是 utf8_unicode_ci，     

*_ci 结尾的都不区分大小写，在 Schema 中可以这样写来修改 collation：     

修改字段：    
``` php
Schema::create('codes', function (Blueprint $table) {
{
    // ......
    $table->string('key')->unique()->charset('utf8')->collation('utf8_bin');
    // ......
});
```

<!-- more -->
或者修改表：

``` php
Schema::create('codes', function (Blueprint $table) {
    $table->charset = 'utf8';
    $table->collation = 'utf8_bin';
    // ......
});
```