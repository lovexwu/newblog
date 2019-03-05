---
title: Promise对象
date: 2019-01-13 22:45:00
tags:
---

# 一、定义

异步编程的一种解决方案，ES6 将其写进了语言标准，统一了用法，原生提供了`Promise`对象，**提供统一的 API，各种异步操作都可以用同样的方法进行处理**

简单说就是一个对象，对象里存储一个状态，这个状态是可以随着内部的执行转化的

**三种状态有：pending（进行中）、fulfilled（已成功）和rejected（已失败）**。



# 二、特点

1､ 对象的状态不受外界影响

2､一旦状态改变，就不会再变，任何时候都可以得到这个结果

注： 

a.  有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。

b.  Promise对象提供统一的接口，使得控制异步操作更加容易



# 三、基本用法

ES6 规定，Promise对象是一个**构造函数**，用来生成**Promise实例**

先看一个创造Promise实例的代码

```javascript
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

上面代码解析

1､ Promise构造函数接受**一个函数**作为参数，该函数的两个参数分别是**resolve**和**reject**。其中它们是两个函数，不用自己部署，由 JavaScript 引擎提供。

2､ **resolve**函数作用是，将Promise对象的状态**从“未完成”变为“成功”**（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去

3､ **reject**函数作用是，将Promise对象的状态**从“未完成”变为“失败”**（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。



还是上面的代码，如果Promise实例生成以后，可以用**then**方法分别指定**resolved状态和rejected状态的回调函数**。

```javascript
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```

然后呢！ **then方法可以接受两个回调函数作为参数**。

1､ 第一个回调函数是Promise对象的状态变为resolved时调用

2､ 第二个回调函数是Promise对象的状态变为rejected时调用，是可选的哦

**注：这两个函数都接受Promise对象传出的值作为参数**



再上一个Promise对象的简单例子

```javascript
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}

timeout(100).then((value) => {
  console.log(value);
});
```

上面代码解析

1､ timeout方法返回一个Promise实例，表示一段时间以后才会发生的结果

2､ 过了指定的时间（ms参数）以后，Promise实例的状态变为resolved，就会触发then方法绑定的回调函数



 Ajax 改造成一个返回 Promise对象  http://js.jirengu.com/gunoxosamu/2/edit

更多用法 http://es6.ruanyifeng.com/#docs/promise