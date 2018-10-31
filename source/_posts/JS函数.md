---
title: JS函数
date: 2018-10-31 13:57:45
tags:
---

### 解密类型转换

#### if的判断

```javascript
if(xxx){
}
```

js是如何处理的？做几道测试题看一看

###### 题目 如下代码输出什么？

```javascript
if （"hello"){	//true
	console.log("hello")
} //"hell0"

if(""){//false
	console.log('empty')
} //不输出

if(" "){//true
	console.log('blank')
}//'blank

if([0]){//true
    console.log('array')
}//'array'

if('0.00'){//true
    console.log('0.00')
}//0.00
```

#### 解密

对括号里的表达式，会被强制转换为布尔类型

#### 原理

| 类型      |             结果              |
| :-------- | :---------------------------: |
| Undefined |             false             |
| Null      |             false             |
| Boolean   |           直接判断            |
| Number    | +0,-0,或NaN为false,其他为true |
| String    | 空字符串为false,其他都为true  |
| Object    |             true              |

#### ==的判断

对于==的判断，js是怎么处理的？做几道题看看

```javascript
"" == 0 //true ""转数字是0
" " == 0 //true " "转数字也是0 
"" == true //false
"" == false//true
" " == true//false

!" " == true  //false " "转布尔是true 取反就是false
!" " == false //true " "转布尔是true 取反就是false
"hello" == true //false "hello"转数字是NaN 
"hello" == false //false
"0" == true //false
"00" == true //false
"0.00" == false //true

undefined == null //true
{} == true // false {}转数字为[object object],ture转数字是1
[] == true // false
var obj = {
    a: 0,
    valueOf:function(){return 1}
}
obj == "[object object]" //false 因为obj返回的是1
obj == 1 //true
obj == true //true

```

<u>**只有空白字符串（“ ”）转布尔值是true,其他都是false**</u>

#### 解密

| x      |             y              |结果|
| :-------- | :---------------------------: |:-------- |
| null |             undefined             |ture|
| Number      |             String             |x == toNumber(y)|
| Boolean   |           (any)            |toNumber(x) == y|
| Object    | String or Number|toPrimitive(x) == y|
| otherwise    | otherwise  |false|

#### toNumber

| type      |             result              |
| :-------- | :---------------------------: |
| Undefined |             NaN             |
| Null      |             0             |
| Boolean   |           true ->1,false ->0            |
| String    | "abc" -> NaN, "123" -> 123  |

#### toPrimitive

对于Object 类型，先尝试调用.valueOf方法获取结果。如果没有定义，再尝试调用.toString方法获取结果

#### arguments

在函数内部，你可以使用arguments对象获取到该函数的所有传入参数

```javascript
function pop(name,age,sex){
    console.log(name)
    console.log(age)
    console.log(sex)
    console.log(arguments)
}
pop('xiaowu',19,'boy')
// xiaowu
//19
//boy
//Arguments(3) ["xiaowu", 19, "boy", callee: ƒ, Symbol(Symbol.iterator): ƒ] 
```

命名冲突

当在同一个作用域内定义了名字相同的变量和方法的话，无论其顺序如何，变量的赋值会覆盖方法的赋值

```javascript
var fn = 3
function fn(){}
console.log(fn) //3

相当于
var fn
function fn(){} //覆盖上面的
fn = 3 // 重新赋值
console.log(fn)
```

当函数执行有命令冲突时，可以认为在还是内部一开始有隐藏的声明变量这个操作

```javascript
function fn(fn){
    console.log(fn)
    var fn = 3;
    console.log(fn);
}
fn(10)

相当于
function fn(){
    var fn = arguments[0]
    console.log(fn)
    var fn = 3;
    console.log(fn)
}
fn(10) //10 3
```

#### 递归

简单来说自已调用自已

```javascript
function fact(n){
    if(n === 1){
        return n = 1
    }
    return n*fact(n-1)
}
console.log(fact(3)) //6
```

