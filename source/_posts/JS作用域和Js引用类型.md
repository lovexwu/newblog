---
title: JS作用域和Js引用类型
date: 2018-10-11 21:45:40
tags:
---

#### JS作用域链
**题1**

```javascript
var a = 1
function fn1(){
    function fn2(){
        console.log(a)
    }
    function fn3(){
        var a = 4
        fn2()
    }
    var a = 2
    return fn3
}
var fn = fn1()
fn() // 2

分析：
调用fn1()后，返回fn3，而fn3中又调用了fn2()，而fn2输出a，但是fn2中没有定义a，所以在上级作用域找a，即fn1的作用域，所以输出2
```



**题2**

```javascript
var a = 1
function fn1(){
    function fn3(){
        var a = 4
        fn2()
    }
    var a = 2
    return fn3
}
function fn2(){
    console.log(a)
}
var fn = fn1()
fn() // 1

分析：
调用fn1之后，return fn3，而fn3调用了fn2，fn2输出a，而fn2中没有a，所以在fn2的上级作用域中找a，所以输出全局作用域的a，即1
```

**题3**

```javascript
var a = 1
function fn1(){
  function fn3(){
    function fn2(){
      console.log(a)
    }
    fn2()
    var a = 4
  }
  var a = 2
  return fn3
}
var fn = fn1()
fn() // undefined

分析：
调用fn2时，在fn3的作用域下，a被声明了，但是还没被赋值
```



##### 解密

1､函数在执行的过程中，先从自已内部找变量

2､如果找不到，再从创建当前函数所在的作用域去找，以此往上



#### 基本类型、引用类型

- 基本类型值（数值、字符串、布尔值、null和undefine）：指保存在栈内存中的简单数据段

- 引用类型值（对象、数组、函数、正则）:指那些保存在堆内存中的对象，变量中保存的实际上只是一个指针，这个指针执行内存中的另一个位置，由该位置保存对象

```javascript
var a;
var b;
var obj;
var obj2;

a = 1;
b = 2;
var obj = {
    name: 'xwu',
    sex: 'girl',
    age: 18,
    friend :{
        name: 'hello',
        age: 100
    }
}

var newObj = {};

b = a;
console.log(b); //1
var obj2 = obj;
obj //{name: "xwu", sex: "girl", age: 18, friend: {…}}
obj2 //{name: "xwu", sex: "girl", age: 18, friend: {…}}

obj.name = 'xxwu' //"xxwu"
obj2.name  //"xxwu"
// 只有一个东西，取了不同名字，这就是引用类型

var obj3 = {name: 'hello'};
var obj4 = {name: 'hello'};
obj3 === obj4 //false


```

```javascript
function test(m){//m是形参
	m.k = 5;
}
var m = {
	k: 30
}
test(m);//m是实参
console.log(m);
// {k: 5}
因为 对象属于引用类型, 传进去的 m 实际是 m 的地址~ 所以 test 还是对 m 进行操作的

//定义 的时候 参数都是形参 
//调用都是实参调用的
```



![p1.jpg](https://upload-images.jianshu.io/upload_images/9375265-61edb0c547ce4ef6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



```javascript
function sum(){
 console.log('sum.....')   
}
var sum2 = sum
sum2() // sum.....
sum2 === sum //true
```

如下图可知，sum和sum2指向的是同一个地址code，即同一个东西，取了不同名字sum、sum2,这就是引用类型



![p2.jpg](https://upload-images.jianshu.io/upload_images/9375265-51635ec7cc5406df.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 函数的参数传递

```javascript
function inc(n){
    n++;
}
var a = 10;
inc(a);
console.log(a);//10

相当于
function inc(){
    var n = arguments[0]
    n++ //可以使用arguments对象在函数中引用函数的参数,此对象包含传递给函数的每个参数,第一个参数在索引0处
}
var a = 10
inc(a)
console.log(a) //10

function incObj(obj){
    //var obj = o // 0x0001
    obj.n++;
}

var o = {n: 10}; //o = 0x0001
incObj(o);
console.log(o);
```

引用类型存的对象地址,如下图

![p3.jpg](https://upload-images.jianshu.io/upload_images/9375265-43b27d969403eae3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```javascript
function squireArr(arr){
    //var arr = 0x0011
    for(var i = 0; i<arr.length; i++){
        arr[i] = arr[i]*arr[i]
    }
}

function squireArr2(arr){
    var newArr = []
    for(var i = 0; i< arr.length; i++){
        newArr = arr[i]*arr[i]
    }
    return newArr
}

var arr = [2,3,4,5] // arr 0x0011
squireArr(arr)
console.log(arr) // [4,9,16,25] 
//在原数组操作

var arr2 = squireArr2(arr)
console.log(arr2) // [4,9,16,25]
//得到一个新数组，原数组没变
```

#### 对象深拷贝和浅拷贝

//浅拷贝 （即拷贝一层）

```javascript
function shallowCopy(oldObj){
    var newObj = {};
    for (var i in oldObj){
        if(oldObj.hasOwnProperty(i)){
            newObj[i] = oldObj[i];
        }
    }
    return newObj;
}
```



//深拷贝 （）

```javascript
function deepCopy(oldObj){
    var newObj = {};
    for (var key in oldObj){
        if(typeof oldObj[key] === 'object'){
            newObj[key] = deepCopy(oldObj[key]);
        }else{
            newObj[key] = oldObj[key];
        }
    }
    return newObj;
}
```

