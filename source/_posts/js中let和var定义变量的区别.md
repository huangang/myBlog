title: js中let和var定义变量的区别
date: 2016-10-30 12:57:26
tags: [javascript,严格模式]
---
注:如果要使用`let`声明变量,必须在文件头添加`'use strict'`严格模式的声明,不然会报错.
<!-- more -->
## 1.声明后未赋值，表现相同
``` js
'use strict';

(function() {
  var varTest;
  let letTest;
  console.log(varTest); //输出undefined
  console.log(letTest); //输出undefined
}());
```
## 2.使用未声明的变量，表现不同:
``` js
'use strict';

(function() {
  console.log(varTest); //输出undefined(注意要注释掉下面一行才能运行)
  console.log(letTest); //直接报错: Uncaught ReferenceError: letTest is not defined

  var varTest = 'test var OK.';
  let letTest = 'test let OK.';
}());
```
### 3.重复声明同一个变量时，表现不同：
``` js
'use strict';

(function() {
  var varTest = 'test var OK.';
  var varTest = 'varTest changed.';
  console.log(varTest); //输出varTest changed.
}());

(function() {
  let letTest = 'test let OK.';
  let letTest = 'letTest changed.';
  console.log(letTest); ///直接报错: Uncaught SyntaxError: Identifier 'letTest' has already been declared
}());
```
## 4.变量作用范围，表现不同
``` js
'use strict';

(function() {
  var varTest = 'test var OK.';
  let letTest = 'test let OK.';

  {
    var varTest = 'varTest changed.';
    let letTest = 'letTest changed.';
  }

  console.log(varTest); //输出"varTest changed."，内部"{}"中声明的varTest变量覆盖外部的letTest声明
  console.log(letTest); //输出"test let OK."，内部"{}"中声明的letTest和外部的letTest不是同一个变量
}());
```