---
title: setTimeout用法
date: 2018-11-06 23:24:21
tags:
---

### 定时器

JS 提供定时执行代码的功能，叫做定时器（timer），主要是由setTimeout() 和 setInterval()两个函数来完成

##### setTimeout()

用来指定某个函数或某段代码，在多少毫秒之后执行。它返回一个整数，表不定时器的编号，以后可以用来取消这个定时器

```javascript
var timerId = setTimeout(func|code,delay)
```

上面代码中，setTimeout函数接受两个参数，第一个参数func|code是将要推迟执行的函数名或一段代码，第二个参数delay是推迟执行的毫秒数

setTimeout方法一般总是采用函数名的形式，像这样子

```javascript
 function f(){
    console.log(2)
}
setTimeout(f,1000)

或

setTimeout(function(){console.log(2)},1000)
```

##### setInterval()

与setTimeout完全一致，区别在于setInterval指定某个任务每隔一段时间就执行一次，也就是无限次的定时执行

```javascript
var i = 1
var timer = setInterval(function(){
    console.log(i++)
},1000)
```

上面代码表示每隔1000豪秒就输出一个i,直到用户点击了停止按钮

##### clearTimeout()、clearInterval() 可以取消对应的定时器





