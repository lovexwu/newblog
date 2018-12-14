---
title: JSON格式
date: 2018-10-13 11:18:45
tags:
---

## 一、定义

全称 JavaScript Object Notation，是一种用于数据交换的**文本格式**，2001年由 Douglas Crockford 提出，目的是取代繁琐笨重的 XML 格式。



## 二、使用规则

(1)  复合类型的值只能是**数组或对象**，不能是**函数、正则表达式对象、日期对象**。

(2)  简单类型的值只有**四种**：**字符串、数值**（必须以十进制表示）、**布尔值和null**（不能使用NaN, Infinity, -Infinity和undefined）。

(3)  字符串必须使用**双引号**表示，**不能使用单引号**。

(4)  对象的**键名**必须放在**双引号**里面。

(5)  数组或对象最后一个成员的后面，**不能加逗号**。



比如说：合格的JSON 格式

```javascript
["one", "two", "three"]

{ "one": 1, "two": 2, "three": 3 }

{"names": ["张三", "李四"] }

[ { "name": "张三"}, {"name": "李四"} ]
```



如果这样子，是不合格的啦

```javascript
{ name: "张三", 'age': 32 }  // 属性名必须使用双引号

[32, 64, 128, 0xFFF] // 不能使用十六进制值

{ "name": "张三", "age": undefined } // 不能使用undefined

{ "name": "张三",
  "birthday": new Date('Fri, 26 Aug 2011 07:13:10 GMT'),
  "getName": function() {
      return this.name;
  }
} // 不能使用函数和日期对象

```



## 三、处理JSON格式数据方法

### A、JSON.stringify()

将一个值(**对象或数组**)转为JSON字符串。该字符串符合 JSON 格式，并且可以被JSON.parse方法还原

#### 语法

> ```json
> JSON.stringify(value[, replacer [, space]])
> ```

**参数**

(1)  **value**:  将要序列化成 一个JSON 字符串的值

(2)  **replacer** （可选）

- 如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理

  ```javascript
  function replacer(key, value) {
    if (typeof value === "string") {
      return undefined;
    }
    return value;
  }
  
  var foo = {foundation: "Mozilla", model: "box", week: 45, transport: "car", month: 7};
  var jsonString = JSON.stringify(foo, replacer);
  //JSON序列化结果为 {"week":45,"month":7}
  ```

- 如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中

  ```javascript
  JSON.stringify(foo, ['week', 'month']);  
  // '{"week":45,"month":7}', 只保留“week”和“month”属性值
  ```

- 如果该参数为null或者未提供，则对象所有的属性都会被序列化


(3)  **space** （可选）

指定缩进用的空白字符串，用于美化输出（pretty-print）

- 如果参数是个数字，它代表有多少的空格；上限为10。该值若小于1，则意味着没有空格

  ![image.png](https://upload-images.jianshu.io/upload_images/14339384-06eea597aa5d848c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 如果该参数为字符串(字符串的前十个字母)，该字符串将被作为空格

  ![image.png](https://upload-images.jianshu.io/upload_images/14339384-b5f31214d1b4532a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 如果该参数没有提供（或者为null）将没有空格

  ![image.png](https://upload-images.jianshu.io/upload_images/14339384-2e463848ad60ef9e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**返回值**:  一个表示给定值的JSON字符串。



转换 JSON 字符串

```javascript
JSON.stringify('abc') // ""abc""
JSON.stringify(1) // "1"
JSON.stringify(false) // "false"
JSON.stringify([]) // "[]"
JSON.stringify({}) // "{}"

JSON.stringify([1, "false", false])
// '[1,"false",false]'

JSON.stringify({ name: "张三" })
// '{"name":"张三"}'
```



**特别注意啦**   对于原始类型的字符串，转换结果会带双引号

```javascript
JSON.stringify('foo') === "foo" // false
JSON.stringify('foo') === "\"foo\"" // true
```

**分析：**字符串'foo'，被转成了""foo""。这是因为将来还原的时候，双引号可以让 JavaScript 引擎知道 。foo是一个字符串，而不是一个变量名



如果**原始对象**中，有一个成员的值**undefined、函数**或 **XML 对象**，这个成员会被过滤

```javascript
var obj = {
  a: undefined,
  b: function () {}
};

JSON.stringify(obj) // "{}"
```

**分析：**对象obj的a属性是undefined，而b属性是一个函数，结果都被JSON.stringify过滤。



如果**数组**的成员是**undefined、函数**或 **XML 对象**，则这些值被转成null。

```javascript
var arr = [undefined, function () {}];
JSON.stringify(arr) // "[null,null]"
```

**分析：**数组arr的成员是undefined和函数，它们都被转成了null。



**正则对象会被转成空对象**

```javascript
JSON.stringify(/foo/) // "{}"
```

JSON.stringify方法会忽略对象的不可遍历属性



### B、JSON.parse()

用于将JSON字符串转化成对象

```javascript
JSON.parse('{}') // {}
JSON.parse('true') // true
JSON.parse('"foo"') // "foo"
JSON.parse('[1, 5, "false"]') // [1, 5, "false"]
JSON.parse('null') // null

var o = JSON.parse('{"name": "张三"}');
o.name // 张三
```



如果传入的字符串不是有效的JSON格式 ，JSON.parse方法将报错。

```javascript
JSON.parse("'String'") // illegal single quotes
// SyntaxError: Unexpected token ILLEGAL
```

**分析：**双引号字符串中是一个单引号字符串，因为单引号字符串不符合JSON格式，所以报错。



## 四、JavaScript 对象和 JSON 的关系

(1)  JavaScript 对象的字面量写法只是长的像 JSON 格式数据，二者属于不同的范畴

(2)  JavaScript 对象中很多类型(函数、正则、Date) ，JSON 格式的规范并不支持

(3)  JavaScript 对象的字面量写法更宽松。



## 五、深拷贝例子

```javascript
var obj = {
    name: 'hunger',
    age: 3,
    friends: ['aa', 'bb', 'cc']
}

var obj2 = JSON.parse(JSON.stringify(obj))
obj.age = 4
console.log(obj2.age)
```





参考 

 https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify

http://javascript.ruanyifeng.com/stdlib/json.html

https://blog.jirengu.com/?p=378