title: laravel migrate 实践
date: 2015-12-29 19:39:11
tags: [laravel]
---
## 运行migrate命令
`php artisan migrate`
## 创建一个叫article的表
`php artisan make:migration create_articles_tables --create=articles`
<!-- more -->
### 编辑定义article需要的字段

```php
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateArticlesTables extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('articles', function (Blueprint $table) {
            $table->increments('id');
            $table->string('title');
            $table->text('content');
            $table->timestamp('published_at');
            $table->timestamps();
        });
    }
    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::drop('articles');
    }
}
```

### 再次运行migrate命令,进行创建
`php artisan migrate`
## 修改article字段
`php artisan make:migration add_intro_column_to_articles --table=articles`

```php
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class AddIntroColumnToArticles extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::table('articles', function (Blueprint $table) {
            $table->string('intro');
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('articles', function (Blueprint $table) {
            $table->dropColumn('intro');
        });
    }
}
```

### 再次运行migrate命令,进行修改
`php artisan migrate`
如果需要运行`$table->dropColumn('intro');`还需要导入一个包运行`composer require doctrine/dbal`

## migrate回滚命令
`php artisan migrate:rollback`

## laravel tinker
`php artisan tinker`
