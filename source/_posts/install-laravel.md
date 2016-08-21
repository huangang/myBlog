title: mac 安装 laravel
date: 2015-12-24 18:46:03
tags: [mac, laravel]
---
先安装composer: `brew install composer`    
通过composer安装laravel: `composer global require "laravel/installer"` 
<!-- more -->
然后编辑.bashrc:         
```` shell   
vim ~/.bash_profile
export PATH="~/.composer/vendor/bin:$PATH"           
source ~/.bash_profile     
````
## PhpStorm代码提示laravel    
`composer require barryvdh/laravel-ide-helper`
然后到找到 `config/app.php` 里面的providers最下面写如`Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,`    
最后执行`php artisan ide-helper:generate`

## composer国内加速
在composer.json添加以下代码
``` json
{
     "repositories": [
            {"type": "composer", "url": "http://packagist.phpcomposer.com"},
            {"packagist": false}
        ]
}

```

## global composer 更新
``` bash
cd /Users/username/.composer
composer update
```


