---
title: 数组、ES5数组方法
date: 2018-10-04 18:05:14
tags:
---

# 一、数组

### A、创建数组

#### (1)  构造函数

传入一个**数字**参数，则会创建一个长度为参数的数组，如果传入多个，则创建一个数组，参数作为初始化数据加到数组中

```javascript
var a1 = new Array(5);
console.log(a1.length);//5
console.log(a1); //[] ,数组是空的

var a2 = new Array(5,6);
console.log(a2.length);//2
console.log(a2); //[5,6]
```



#### **(2)  字面量**

```javascript
 var b = [1, 2, 'hello'];
```



但是使用字面量方式，无论传入几个参数，都会把参数当作初始化内容

```javascript
var a1 = [5];
console.log(a1.length);//1
console.log(a1); //[5]

var a2 = [5,6];
console.log(a2.length);//2
console.log(a2); //[5,6]
```



使用带初始化参数的方式创建数组的时候，最好最后不要带多余的”,”，在不同的浏览器下对此处理方式不一样

```javascript
var a1 = [1,2,3,]
console.log(a1.length)
console.log(a1)
```

这段脚本在现代浏览器上运行结果和我们设想一样，长度是3，但是在低版本IE下确实长度为4的数组，最后一条数据是`undefined`



### B、元素添加、删除

#### (1)  基本方法

向数组内添加元素方法，直接使用索引就可以（index没必要连续）

```javascript
var a=[1,2,3];
a[3]=4;
console.log(a);//[1, 2, 3, 4]
```

数组也是对象，索引只是特殊的属性，所以我们可以使用删除对象属性的方法,使用delete 删除数组元素

```javascript
delete a[2];
console.log(a[2]); //undefined
```

这样和直接把a[2]赋值为undefined类似，不会改变数组长度，也不会改变其他数据的index和value对应关系



#### (2)  栈方法

上面例子发现了，尤其是其删除方法，并不是我们希望的表现形式，我们很多时候希望删除中间一个元素后，后面元素的index都自动减一，数组length同时减一，就好像在一个堆栈中拿去的一个，数组已经帮我们做好了这种操作方式，`pop`和`push`能够让我们使用堆栈那样先入后出使用数组

```javascript
var a = [1, 2, 3];
a.push(4);
console.log(a);//[1, 2, 3, 4]
console.log(a.length);//4
console.log(a.pop());//4
console.log(a); //[1, 2, 3]
console.log(a.length);//3
```



#### (3)  队列方法

既然栈方法都实现了，先入先出的队列怎么能少，`shift`方法可以删除数组index最小元素，并使后面元素index都减一，length也减一，这样使用shift/push就可以模拟队列了，当然与shift方法对应的有一个`unshift`方法，用于向数组头部添加一个元素

```javascript
var a=[1, 2, 3];
a.unshift(4);
console.log(a);//[4, 1, 2, 3]
console.log(a.length);//4
console.log(a.shift());//4
console.log(a); //[1, 2, 3]
console.log(a.length);//3
```



### C、常用命令

#### (1)  push-----------数组最后添加一个元素

```javascript
var arr = [1,2,3]
arr.push('ok')   //给数组最后添加一个元素
//[1, 2, 3, "ok"] 
```



#### (2)  pop------------数组最后一位踢出来

```javascript
arr.pop() //把数组最后一位踢出来
//[1, 2, 3]
```



#### (3)  pop------------数组最后一位踢出来

```javascript
arr.shift() //把数组第一位踢出来
//[2, 3]
```



#### (4)  unshift------------在数组第一位添加一个元素

```javascript
arr.unshift('haha') //在数组第一位添加一个元素
//["haha", 2, 3]
```



#### (5)  join------------用某个符号连接数组所有的值，生成字符串

```javascript
arr.join('-') //连接
//"2-3"
```



#### (6)  splice------------从数组的第一位开始，替换掉一位

```javascript
arr.splice(1,1,'hello','one','two') //从数组的第一位开始，替换掉一位
//[2, "hello", "one", "two"]
```



#### (7)  sort------------排序

```javascript
arr.sort()  //排序
//[2, "hello", "one", "two"]
```



#### (8)  reverse------------逆序即倒序

```javascript
arr.reverse() //逆序即倒序
//["two", "one", "hello", 2]
```



#### (9)  concat------------拼接数组

```javascript
arr.concat('super') //拼接
//["two", "one", "hello", 2, "super"]
```



### D、ES5 数组拓展

#### (1)  Array.isArray(obj)

Array对象的一个静态函数，用来判断一个对象是不是数组

```
var a = [];
var b = new Date();
console.log(Array.isArray(a)); //true
console.log(Array.isArray(b)); //false
```



####(2)  indexOf(element)
查找数组内指定元素的位置，查找到第一个返回其索引，没有返回-1

```javascript
var arr = [1,2,3,4,5]
console.log(arr.indexOf(3)) //2
console.log(arr.indexOf(9)) //-1
```


#### (3)  forEach(element,index,array)

 遍历数组，参数为一个回调函数，回调函数有三个参数：

1、当前元素
2、当前元素索引
3、整个数组

```javascript
var arr = [1,2,3,4,5]
arr.forEach(function(e,index){
   arr[index] = e + 1      
})
console.log(arr) //[2, 3, 4, 5, 6]
```


####(4)  map (function(element))

与forEach类似，遍历数组，回调函数返回值组成一个新数组返回，新数组索引结构和原数组一致，原数组不变

```javascript
var arr = [1,2,3,4,5]
console.log(arr.map(function(e){
   return e*e // [1, 4, 9, 16, 25]
}))
console.log(arr) //[1, 2, 3, 4, 5]
```
**注：在空数组上调用,every返回true,some 返回false**



#### (5)  every (function(element,index,array))

所有函数的每个回调函数都返回true时才会返回true,当遇到false时终止执行，返回false

```javascript
var arr = [1,2,3,4,5]
arr.every(function(val){
    return val>0?true:false
})//true
```


####(6)  some (function(element,index,array))

只要有一个回调函数返回true时终止执行并返回true,否则返回false 

```javascript
var arr = [1,2,3,4,5]
arr.some(function(val){
   return val>0?true:false
})//true
```


#### (7)  filter(function(element))

返回一个子集，回调函数用于逻辑判断是否返回，返回true则把当前元素加入到返回数组中，false则不加
数组只包含返回true的值，索引缺失的不包括，原数组保持不变

```javascript
var arr = [1,2,3,4,5,6]
console.log(arr.filter(function(val){
    return val > 3
})) // [4, 5, 6]
console.log(arr) // [1,2,3,4,5,6]
```


#### (8)  reduce(function(v1,v2),value)

遍历数组，调用回调函数，将数组元素组合成一个值，从索引最小值开始，方法有两个参数

1、回调函数：把两个值合为一个，返回结果
2、value : 一个初始值，可选

```javascript
var arr = [1,2,3,4,5,6]
arr.reduce(function(v1,v2){
    return v1 + v2
}) //21
```