---
title: DOM
date: 2018-11-10 18:39:26
tags:
---

## 一、DOM 基本概念

### A、定义

全称为“文档对象模型”（Document Object Model），是 JavaScript 操作网页的接口



### B、作用

(1)  将网页转为一个 JavaScript 对象，从而可以用脚本进行各种操作（比如增删内容）。

(2)  浏览器会根据 DOM 模型，将结构化文档（比如 HTML 和 XML）解析成一系列的节点，再由这些节点组成一个树状结构（DOM Tree）。

**所有的节点和最终的树状结构，都有规范的对外接口**。



### C、节点（node）

**(1)  定义**

DOM 的最小组成单位



**(2)  类型**

文档的树形结构（DOM 树），就是由各种不同类型的节点组成

- Document：整个文档树的顶层节点
- DocumentType：doctype标签（比如<!DOCTYPE html>）
- Element：网页的各种HTML标签（比如<body>、<a>等）
- Attribute：网页元素的属性（比如class="right"）
- Text：标签之间或标签包含的文本
- Comment：注释
- DocumentFragment：文档的片段

**浏览器提供一个原生的节点对象Node，上面这七种节点都继承了Node，因此具有一些共同的属性和方法**。



### D、节点树

一个文档的所有节点，按照所在的层级，可以抽象成一种树状结构。这种树状结构就是 DOM 树。

浏览器原生提document节点，代表整个文档。

```javascript
document  // 整个文档树
```

文档的第一层只有一个节点，就是 **HTML 网页的第一个标签<html>**，它构成了树结构的根节点（root node），其他 HTML 标签节点都是它的下级节点

![image.png](https://upload-images.jianshu.io/upload_images/14339384-9e83ded0b29e238c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### E、使用场景

 HTML 元素进行添加、移动、改变或移除的方法和属性，都是通过DOM来获得的

准确地说，要改变页面的某个东西，JavaScript就需要获得对HTML文档中所有元素进行访问的入口。



## 二、document 对象

### A、定义

每个载入浏览器的HTML文档都会成为document对象。document对象包含了文档的基本信息，我们可以通过JavaScript对HTML页面中的所有元素进行访问、修改



### B、常用属性

(1) document.location

也可直接使用 location

```javascript
document.location === location //true
document.location === window.location  //true
```



location属性返回一个只读对象，提供了当前文档的URL信息

```javascript
// 假定当前网址为http://user:passwd@www.example.com:4097/path/a.html?x=111#part1

document.location.href //"http://user:passwd@www.example.com:4097/path/a.html?x=111#part1"
document.location.protocol // "http:"
document.location.host // "www.example.com:4097"
document.location.hostname // "www.example.com"
document.location.port // "4097"
document.location.pathname // "/path/a.html"
document.location.search // "?x=111"
document.location.hash // "#part1"
document.location.user // "user"
document.location.password // "passed"

// 跳转到另一个网址
document.location.assign('http://www.google.com')
// 优先从服务器重新加载
document.location.reload(true)
// 优先从本地缓存重新加载（默认值）
document.location.reload(false)
// 跳转到另一个网址，但当前文档不保留在history对象中，
// 即无法用后退按钮，回到当前文档
document.location.assign('http://www.google.com')
// 将location对象转为字符串，等价于document.location.href
document.location.toString()
```



虽然location属性返回的对象是只读的，但是可以将URL赋值给这个属性，网页就会自动跳转到指定网址。

```javascript
document.location = 'http://www.example.com';
// 等价于
document.location.href = 'http://www.example.com';
```



(2)  document.open()、document.close()

document.open方法用于新建一个文档，供write方法写入内容。它实际上等于清除当前文档，重新写入内容

document.close方法用于关闭open方法所新建的文档。一旦关闭，write方法就无法写入内容了。



(3)  document.write()

用于向当前文档写入内容。只要当前文档还没有用close方法关闭，它所写入的内容就会追加在已有内容的后面。

```javascript
document.open();
document.write("hello");
document.write("world");
document.close();
```

特别注意

- 如果页面已经渲染完成再调用write方法，它会先调用open方法，擦除当前文档所有内容，然后再写入。

- 如果在页面渲染过程中调用write方法，并不会调用open方法。

- 调用close方法之后，无法再用write方法写入内容，但这时当前页面的其他DOM节点还是会继续加载。

除了某些特殊情况，应该尽量避免使用document.write这个方法



## 三、Element

### A、定义

Element对象表示HTML元素



### B、类型

- 元素节点

- 文本节点

- 注释节点的子节点



### C、属性

- nodeName：元素标签名，还有个类似的tagName

- nodeType：元素类型

- className：类名

- id：元素id

- children：子元素列表（HTMLCollection）

- childNodes：子元素列表（NodeList）

- firstChild：第一个子元素

- lastChild：最后一个子元素

- nextSibling：下一个兄弟元素

- previousSibling：上一个兄弟元素

- parentNode、parentElement：父元素



### D、查询元素

(1)  getElementById()

返回匹配指定ID属性的元素节点。如果没有发现匹配的节点，则返回null。这也是获取一个元素最快的方法

```javascript
var elem = document.getElementById("test");
```



(2)  getElementsByClassName()

返回一个类似数组的对象（HTMLCollection类型的对象），包括了所有class名字符合指定条件的元素（搜索范围包括本身），元素的变化实时反映在返回结果中。这个方法不仅可以在document对象上调用，也可以在任何元素节点上调用。

```javascript
var elements = document.getElementsByClassName('tab');
```



getElementsByClassName方法的参数，可以是多个空格分隔的class名字，返回同时具有这些节点的元素。

```javascript
document.getElementsByClassName('red test');
```



(3)  getElementsByTagName()

返回所有指定标签的元素（搜索范围包括本身）。返回值是一个HTMLCollection对象，也就是说，搜索结果是一个动态集合，任何元素的变化都会实时反映在返回的集合中。这个方法不仅可以在document对象上调用，也可以在任何元素节点上调用。

```javascript
var paras = document.getElementsByTagName("p");
//返回当前文档的所有p元素节点
```

注意，getElementsByTagName方法会将参数转为小写后，再进行搜索。



(4)  getElementsByName()

选择拥有name属性的HTML元素，比如form、img、frame、embed和object，返回一个NodeList格式的对象，不会实时反映元素的变化。

```javascript
// 假定有一个表单是<form name="x"></form>
var forms = document.getElementsByName("x");
forms[0].tagName // "FORM"
```

注意，在IE浏览器使用这个方法，会将没有name属性、但有同名id属性的元素也返回，所以name和id属性最好设为不一样的值。



(5)  querySelector()

返回匹配指定的CSS选择器的元素节点。如果有多个节点满足匹配条件，则返回第一个匹配的节点。如果没有发现匹配的节点，则返回null。

```javascript
var el1 = document.querySelector(".myclass");
var el2 = document.querySelector('#myParent > [ng-click]');
```

**querySelector方法无法选中CSS伪元素**



(6)  querySelectorAll()

返回匹配指定的CSS选择器的所有节点，返回的是NodeList类型的对象。NodeList对象不是动态集合，所以元素节点的变化无法实时反映在返回结果中。

```javascript
elementList = document.querySelectorAll(selectors);
```



querySelectorAll方法的参数，可以是逗号分隔的多个CSS选择器，返回所有匹配其中一个选择器的元素。

```javascript
var matches = document.querySelectorAll("div.note, div.alert");
//返回class属性是note或alert的div元素
```



## 四、创建元素

(1)  createElement()

用来生成HTML元素节点

```javascript
var newDiv = document.createElement("div");
```

createElement方法的参数为元素的标签名，即元素节点的tagName属性。如果传入大写的标签名，会被转为小写。如果参数带有尖括号（即<和>）或者是null，会报错。



(2)  createTextNode()

用来生成文本节点，参数为所要生成的文本节点的内容

```javascript
var newDiv = document.createElement("div");
var newContent = document.createTextNode("Hello");
//新建一个div节点和一个文本节点
```



(3)  createDocumentFragment()

生成一个DocumentFragment对象

```javascript
var docFragment = document.createDocumentFragment();
```

DocumentFragment对象是一个存在于内存的DOM片段，但是不属于当前文档，常常用来生成较复杂的DOM结构，然后插入当前文档。这样做的好处在于，因为DocumentFragment不属于当前文档，对它的任何改动，都不会引发网页的重新渲染，比直接修改当前文档的DOM有更好的性能表现。



### 五、修改元素

(1)  appendChild()

在元素末尾添加元素

```javascript
var newDiv = document.createElement("div");
var newContent = document.createTextNode("Hello");
newDiv.appendChild(newContent);
```



(2)  insertBefore()

在某个元素之前插入元素

```javascript
var newDiv = document.createElement("div");
var newContent = document.createTextNode("Hello");
newDiv.insertBefore(newContent, newDiv.firstChild);
```



(3)replaceChild()

接受两个参数：要插入的元素和要替换的元素

```javascript
newDiv.replaceChild(newElement, oldElement);
```



### 六、删除元素

删除元素使用removeChild()方法即可

```javascript
parentNode.removeChild(childNode);
```



### 七、clone元素

用于克隆元素，方法有一个布尔值参数，传入true的时候会深复制，也就是会复制元素及其子元素（IE还会复制其事件），false的时候只复制元素本身

```javascript
node.cloneNode(true);
```



## 八、属性操作

(1)  getAttribute()

用于获取元素的attribute值

```javascript
node.getAttribute('id');
```



(2)  createAttribute()

生成一个新的属性对象节点，并返回它。

```javascript
attribute = document.createAttribute(name);
```

createAttribute方法的参数name，是属性的名称。



(3)  setAttribute()

用于设置元素属性

```javascript
var node = document.getElementById("div1");
node.setAttribute("my_attrib", "newVal");
```

等同于

```javascript
var node = document.getElementById("div1");
var a = document.createAttribute("my_attrib");
a.value = "newVal";
node.setAttributeNode(a);
```



(4)  removeAttribute()

用于删除元素属性

```javascript
node.removeAttribute('id');
```



(5)  element.attributes

当然上面的方法做的事情也可以通过类操作数组属性element.attributes来实现



(6)  innerText

是一个可写属性，返回元素内包含的文本内容，在多层次的时候会按照元素由浅到深的顺序拼接其内容

```javascript
<div>
    <p>
        123
        <span>456</span>
    </p>
</div>j
```

外层div的innerText返回内容是 `"123456"`



(7)  innerHTML

和innerText类似，但是不是返回元素的文本内容，而是返回元素的HTML结构，在写入的时候也会自动构建DOM

```javascript
<div>
    <p>
        123
        <span>456</span>
    </p>
</div>
```

外层div的innerHTML返回内容是 `"<p>123<span>456</span></p>"`



## 九、常见使用方式

### A、css样式修改

(1)   style 属性

可修改元素的 **style 属性**，修改结果直接反映到页面元素

```javascript
document.querySelector('p').style.color = 'red'
document.querySelector('.box').style.backgroundColor = '#ccc'
```



(2)  getComputedStyle

使用getComputedStyle获取元素计算后的样式，**不要通过 node.style属性** 获取

![image.png](https://upload-images.jianshu.io/upload_images/14339384-e422710273f305d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### B、 class 的新增、删除、切换、判断操作

```javascript
var nodeBox = document.querySelector('.box')
console.log( nodeBox.classList )
nodeBox.classList.add('active')   //新增 class
nodeBox.classList.remove('active')  //删除 class
nodeBox.classList.toggle('active')   //新增/删除切换
node.classList.contains('active')   // 判断是否拥有 class
```



## 十、页面宽高

(1)  element.clientHeight

![image.png](https://upload-images.jianshu.io/upload_images/14339384-a2b8e1d615f2fa98.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(2)  element.offsetHeight

![image.png](https://upload-images.jianshu.io/upload_images/14339384-7e3bb7bd8ccb892d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



控制台上输入以下代码，查看执行结果

![image.png](https://upload-images.jianshu.io/upload_images/14339384-e3bde3a457ebc96a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(3)  element.scrollHeight 

元素滚动内容的总长度。如果元素没出现滚动条， scrollHeight等于 clientHeight

```javascript
document.body.scrollHeight
```



(4)  element.scrollTop 滚动的高度

```javascript
document.body.scrollTop
```



(5)  window.innerHeight 窗口的高度

```javascript
window.innerHeigh
```