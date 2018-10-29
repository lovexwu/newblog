---
title: JS对象
date: 2018-10-29 18:07:30
tags:
---

## JS对象 & JSON & JS数组操作之习题

第 1 题

JSON格式的数据需要遵循什么规则？

答案：

1、复合类型的值只能是数组或对象，不能是函数、正则表达式对象、日期对象
2、简单类型的值只有四种：字符串、数值（必须是十进制表示）、布尔型和null（不能是NaN,Infinity,-Infinity和undefined）
3、字符串必须是使用双引号表示，不能使用单引号
4、对象的键名必须放在双引号里面
5、数组或对象最后一个成员的后面，不能加逗号



第 2 题

遍历 company 对象，输出里面每一项的值

```javascript
var company = {
    name: '饥人谷',
    age: 3,
    sex: '男'
}


```

答案：

```javascript
for (var key in company){
console.log(company[key])
}
```



第 3 题

使用 JSON 对象实现一个简单的深拷贝函数(deepCopy)。

```javascript
var obj = {
    name: 'xwu',
    age: '18'
}

var obj2 = JSON.parse(Json.stringify(obj))
obj.age = 4
console.log(obj) //4
obj2.age = 3

```

第 4 题 

分别举例说明数组方法`push`、`pop`、`shift`、`unshift`、`join`、`splice`、`sort`、`reverse`、`concat`的作用？

```javascript
var arr = [1,2,3]
arr.push('ok')   //给数组最后添加一个元素
//[1, 2, 3, "ok"] 

arr.pop() //把数组最后一位踢出来
//[1, 2, 3]

arr.shift() //把数组第一位踢出来
//[2, 3]

arr.unshift('haha') //在数组第一位添加一个元素
//["haha", 2, 3]

arr.join('-') //连接
//"2-3"

arr.splice(1,1,'hello','one','two') //从数组的第一位开始，替换掉一位
//[2, "hello", "one", "two"]

arr.sort()  //排序
//[2, "hello", "one", "two"]

arr.reverse() //逆序即倒序
//["two", "one", "hello", 2]

arr.concat('super') //拼接
//["two", "one", "hello", 2, "super"]
```

第 5 题

写一个函数，操作数组，返回一个新数组，新数组中只包含正数。

```
function filterPositive(arr){
补全
}
var arr = [3, -1,  2,  '饥人谷', true]
filterPositive(arr)
console.log(filterPositive(arr)) //[3,  2]

```

答案：

```javascript
方法1
function filterPositive(arr){
	for(var i = 0; i< arr.length; i++){
         var newArr = [];
         if(typeof(arr[i]) === 'number' && arr[i] > 0){
            newArr.push(arr[i]) 
         }
	}
	return newArr
}
var arr = [3, -1,  2,  '饥人谷', true]
filterPositive(arr)
console.log(filterPositive(arr)) //[3,  2]


方法2
function filterPositive(arr){
  return arr.filter(function(val){
     return typeof val === 'number' && val > 0 
  })
}
var arr = [3, -1,  2,  '饥人谷', true]
filterPositive(arr)
console.log(filterPositive(arr)) //[3,  2]
```



第 6 题

用 splice函数分别实现 `push`、`pop`、`shift`、`unshift`方法, 如：

```
function push(arr, value){
    arr.splice(arr.length, 0, value)
    return arr.length
}
var arr = [3, 4, 5]
arr.push(10) // arr 变成[3,4,5,10]，返回4

```

答案：

```javascript
1、pop 把数组的最后一位踢出去

function pop(){
    arr.splice(arr.length-1,1)
}
var arr = [3, 4, 5]
arr.pop() // [3,4]

2、shift 把数组的第一位踢出去
function shift(){
    arr.splice(0,1)
}
var arr = [3, 4, 5]
arr.shift() // [4,5]

3､ unshift 在数组的第一位添加元素
    arr.splice(0,1)
}
var arr = [3, 4, 5]
arr.unshift(10)
```

第 7 题

对以下代码 users中的对象，分别以 name 字段、age 字段、company 字段进行排序

```
var users = [
  { name: "John", age: 20, company: "Baidu" },
  { name: "Pete", age: 18, company: "Alibaba" },
  { name: "Ann", age: 19, company: "Tecent" }
]
```

答案：

```
1、 name字段排序
users.sort(function(v1,v2){
    return v1.name > v2.name
})

2､ age 字段排序
users.sort(function(v1,v2){
    return v1.age - v2.age
})

3、company 字段排序
users.sort(function(v1,v2){
    return v1.company > v2.company
})
```



第 8 题

分别举例说明ES5数组方法 indexOf、forEach、map、every、some、filter、reduce的用法？

答案：

```
indexOf 
查找数组内指定元素的位置，查找到第一个返回其索引，没有返回-1
var arr = [1,2,3,4,5]
console.log(arr.indexOf(3)) 2
console.log(arr.indexOf(9)) -1

forEach(element,index,array)
 遍历数组，参数为一个回调函数，回调函数有三个参数：
 1、当前元素
 2、当前元素索引
 3、整个数组

var arr = [1,2,3,4,5]
arr.forEach(function(e,index){
    arr[index] = e + 1      
})
console.log(arr) [2, 3, 4, 5, 6]

map 与forEach类似，遍历数组，回调函数返回值组成一个新数组返回，新数组索引结构和原数组一致，原数组不变
var arr = [1,2,3,4,5]
console.log(arr.map(function(e){
   return e*e  [1, 4, 9, 16, 25]
}))
console.log(arr) [1, 2, 3, 4, 5]

注：在空数组上调用,every返回true,some 返回false

every 所有函数的每个回调函数都返回true时才会返回true,当遇到false时终止执行，返回false
var arr = [1,2,3,4,5]
arr.every(function(val){
    return val>0?true:false
})true

some 只要有一个回调函数返回true时终止执行并返回true,否则返回false 
var arr = [1,2,3,4,5]
arr.some(function(val){
    return val>0?true:false
})true

filter
filter(function(element))
返回一个子集，回调函数用于逻辑判断是否返回，返回true则把当前元素加入到返回数组中，false则不加
新数组只包含返回true的值，索引缺失的不包括，原数组保持不变
var arr = [1,2,3,4,5,6]
console.log(arr.filter(function(val){
    return val > 3
}))  [4, 5, 6]
console.log(arr)  [1,2,3,4,5,6]

reduce 
reduce(function(v1,v2),value)
遍历数组，调用回调函数，将数组元素组合成一个值，从索引最小值开始，方法有两个参数
1、回调函数：把两个值合为一个，返回结果
2、value : 一个初始值，可选
```


第9题

以下代码输出什么？

```javascript
1、
var name = 'sex'
var company = {
    name: '饥人谷',
    age: 3,
    sex: '男'
}
console.log(company.name) //饥人谷 

分析：company.name中的name是指的company对象中的属性name，因为它的值是饥人谷，所以最后结果是饥人谷

2､
var name = 'sex'
var company = {
    name: '饥人谷',
    age: 3,
    sex: '男'
}
console.log(company[name]) //男

分析：此处的company[name]中的name是指变量name，它的值是sex,然后再读取company对象中的sex的值，sex的值是男，所以最后输出男
```



第10题

写补全sortString函数，实现字符串倒序

```
function  sortString(str){
    //补全
}
var str = 'jirenguhungervalley'
var str2 = sortString(str)
console.log(str2) // 'yellavregnuhugnerij'
```

答案：

```javascript
function  sortString(str){
    return str.split('').reverse().join('')
}
```

