title: angular 懒加载控制器
date: 2016-05-01 10:18:03
tags: [angular]
---
### app.js

``` js
var app = angular.module('app', [
    'ui.router',                    // Routing
    'oc.lazyLoad',                  // ocLazyLoad
]);
app.config(function($controllerProvider, $compileProvider, $filterProvider, $provide) {
    app.register = {
        controller: $controllerProvider.register,
        directive: $compileProvider.directive,
        filter: $filterProvider.register,
        factory: $provide.factory,
        service: $provide.service
    };
});
```
### route.js

``` js
function config($stateProvider, $urlRouterProvider, $ocLazyLoadProvider) {

    $ocLazyLoadProvider.config({
        // Set to true if you want to see what and when is dynamically loaded
        debug: true
    });

    $stateProvider
        .state('index', {
            url: "/index",
            templateUrl: "views/index.html",
            controller: 'IndexController',
            resolve: {
                loadPlugin: function ($ocLazyLoad) {
                    return $ocLazyLoad.load([
                        {
                            files: [ 'js/controllers/IndexController.js']
                        }
                    ]);
                }
            }
        })
    ;

}
app.config(config)
.run(function($rootScope, $state) {$rootScope.$state = $state;});
```

### IndexController.js

``` js
function IndexController($scope) {
    console.log('this is IndexController');
}
app.register.controller('IndexController', IndexController);

```