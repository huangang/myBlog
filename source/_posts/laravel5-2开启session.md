title: laravel5.2开启session
date: 2016-01-29 17:31:43
tags: [laravel]
---
laravel5.2框架中间件默认是没有开启Session的
所以在 App\Http\Kernel 里面的$middleware 加入：
```
\Illuminate\Cookie\Middleware\EncryptCookies::class,
\Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
\Illuminate\Session\Middleware\StartSession::class,
\Illuminate\View\Middleware\ShareErrorsFromSession::class,
\App\Http\Middleware\VerifyCsrfToken::class,
```
ps:找了一下午才解决这个问题...