---
title: ES5数组方法的那些事
date: 2018-10-04 18:05:14
tags:
---

# 

indexOf、forEach、map、every、some、filter、reduce的用法

###indexOf 
查找数组内指定元素的位置，查找到第一个返回其索引，没有返回-1

```javascript
var arr = [1,2,3,4,5]
console.log(arr.indexOf(3)) //2
console.log(arr.indexOf(9)) //-1
```
### forEach
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
###map 
与forEach类似，遍历数组，回调函数返回值组成一个新数组返回，新数组索引结构和原数组一致，原数组不变

```javascript
var arr = [1,2,3,4,5]
console.log(arr.map(function(e){
   return e*e // [1, 4, 9, 16, 25]
}))
console.log(arr) //[1, 2, 3, 4, 5]
```
**注：在空数组上调用,every返回true,some 返回false**

### every 
所有函数的每个回调函数都返回true时才会返回true,当遇到false时终止执行，返回false

```javascript
var arr = [1,2,3,4,5]
arr.every(function(val){
    return val>0?true:false
})//true
```
###some 
只要有一个回调函数返回true时终止执行并返回true,否则返回false 

```javascript
var arr = [1,2,3,4,5]
arr.some(function(val){
   return val>0?true:false
})//true
```
### filter(function(element))
返回一个子集，回调函数用于逻辑判断是否返回，返回true则把当前元素加入到返回数组中，false则不加
数组只包含返回true的值，索引缺失的不包括，原数组保持不变

```javascript
var arr = [1,2,3,4,5,6]
console.log(arr.filter(function(val){
    return val > 3
})) // [4, 5, 6]
console.log(arr) // [1,2,3,4,5,6]
```
### reduce(function(v1,v2),value)
遍历数组，调用回调函数，将数组元素组合成一个值，从索引最小值开始，方法有两个参数

1、回调函数：把两个值合为一个，返回结果
2、value : 一个初始值，可选

```javascript
var arr = [1,2,3,4,5,6]
arr.reduce(function(v1,v2){
    return v1 + v2
}) //21
```