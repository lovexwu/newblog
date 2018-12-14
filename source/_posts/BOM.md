---
title: BOM
date: 2018-11-18 13:35:58
tags:
---

## 一、定义

浏览器对象模型，全称Browser Object Model



## 二、作用

(1)  描述这种对象与对象之间层次关系的模型

(2)  提供了独立于内容的、可以与浏览器窗口进行互动的对象结构

BOM由多个对象组成，其中代表浏览器窗口的Window对象是BOM的顶层对象，其他对象都是该对象的子对象。



## 三、window 对象

**A、  定义**

(1)  BOM 的核心是window对象，它表示浏览器的一个实例。

(2)   在浏览器中，即是javascript访问浏览器窗口的一个接口，又是ECMAScript规定的Global对象

在网页中定义的任意变量、函数、对象都是以window作为Global对象，比如

```javascript
var age = 24;
function printName(){
    console.log(age);
}
console.log(window.age);
window.printName();
```

**所有在全局作用域中声明的变量、函数、对象都会作为window的属性和方法**



**B、属性**

(1)  window.innerHeight，window.innerWidth

返回网页的CSS布局占据的浏览器窗口的高度和宽度，单位为像素 ，但是当用户放大网页的时候（比如将网页从100%的大小放大为200%），这两个属性会变小

![image.png](https://upload-images.jianshu.io/upload_images/14339384-77533106158e4837.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



注意，这两个属性值包括滚动条的高度和宽度**



(2)  scrollX、scrollY

- scrollX：滚动条横向偏移

- scrollY：滚动条纵向偏移

这两个值随着滚动位置变化而变化



(3)  scrollTo、scrollBy、scroll

通过方法scrollTo或者scroll方法改变滚动条位置到指定坐标

```javascript
window.scrollTo(0, 300); // 滚动条移动到300px处
```

两个参数分别是水平、垂直方向偏移



scrollBy可以相对当前位置移动滚动条，而不是移动到绝对位置

```javascript
scrollBy(0, 100); // 滚动条下移100px
```



(4)  navigator **(重点)**

Window对象的navigator属性，指向一个包含浏览器相关信息的对象。

navigator.userAgent属性返回浏览器的`User-Agent`字符串，用来标示浏览器的种类。下面是Chrome浏览器的User-Agent。

```javascript
navigator.userAgent // "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.118 Safari/537.36"
```



判断用户的浏览器类型

![image.png](https://upload-images.jianshu.io/upload_images/14339384-122ad196a6e60343.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(5)  screen

screen对象包含了显示设备的信息。

```javascript
// 显示设备的高度，单位为像素
screen.height
// 1920

// 显示设备的宽度，单位为像素
screen.width
// 1080
```

一般使用以上两个属性，了解设备的分辨率。上面代码显示，某设备的分辨率是1920x1080。除非调整显示器的分辨率，否则这两个值可以看作常量，不会发生变化。显示器的分辨率与浏览器设置无关，缩放网页并不会改变分辨率



(6)  window.getComputedStyle

getComputedStyle是一个可以获取当前元素所有最终使用的CSS属性值。返回的是一个CSS样式声明对象([object CSSStyleDeclaration])

一看这个函数的名字我们就知道问题解决了

```javascript
var style = window.getComputedStyle("元素", "伪类");
```

第二个参数没有伪类则不设置

```javascript
var div = document.getElementById('test');
console.log(getComputedStyle(div).width);
```



(7)  currentStyle

这个是低版本IE的实现方案，我们可以写个兼容的方式

```javascript
element.currentStyle ?
    element.currentStyle : window.getComputedStyle(element, null)
```