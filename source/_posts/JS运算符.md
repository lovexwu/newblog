---
title: JS运算符
date: 2018-10-04 23:23:25
tags:
---

##### 加号运算符

有些操作符对不同数据类型有不同的含义，比如 +

- 在两个操作数都是数字的时候，会做加法运算
- 两个参数都是字符串或在有一个参数是字符串的情况下会把另外一个参数转换为字符串做字符串拼接
- 在参数有对象的情况下会调用其valueOf 或 toString
- 在只有一个字符串参数的时候会尝试将其转换为数字
- 在只有一个数字参数的时候返回其正数值

```javascript
console.log(2+4) //6
console.log("2"+"4") //"24"
console.log(2+"4") //"24"
console.log(+"4") //4

var obj = {
    toString:function(){
        return 10
    },
    valueOf:function(){
        return "100"
    }
}
console.log(+obj) // 100
//这里是因为obj的valueOf级别高于toString，所以是返回字符串100,然后+号会强制转为数字
```

##### 逻辑运算符

能够转换为false的表达式有：

- `null`；
- `NaN`；
- `0`；
- 空字符串（`""`）；
- `undefined`。

<u>

其他运算符参考</u>

 https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators