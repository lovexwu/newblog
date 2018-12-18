---
title: jQuery之DOM操作、属性、函数
date: 2018-12-17 13:26:37
tags:
---

# 一、DOM操作

### A、创建元素

只需要把DOM字符串传入 $ 方法即可返回一个jQuery对象

```javascript
var obj = $('<div class="test"><p><span>Done</span></p></div>');
```

![image.png](https://upload-images.jianshu.io/upload_images/9375265-d352524426d7770c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### B、添加元素

(1)  .append(content[,content]) / .append(function(index,html))

- 可以一次添加多个内容，内容可以是DOM对象、HTML string、 jQuery对象
- 如果参数是function，function可以返回DOM对象、HTML string、 jQuery对象，参数是集合中的元素位置与原来的html值

![image.png](https://upload-images.jianshu.io/upload_images/9375265-e479978f4956892f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(2)  .prepend(content[,content]) / .prepend(function(index,html))

向**对象头部**追加内容，用法和append类似，内容**添加到最开始**

![image.png](https://upload-images.jianshu.io/upload_images/9375265-ba189a1015d84a37.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(3) .before([content][,content]) / .before(function)

在对象前面(**不是头部，而是外面，和对象并列同级**)插入内容，参数和append类似

![image.png](https://upload-images.jianshu.io/upload_images/9375265-ae94968ffc102f32.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(4) .after([content][,content]) / .after(function（index）)

和before相反，在对象后面(**不是尾部，而是外面，和对象并列同级**)插入内容，参数和append类似

![image.png](https://upload-images.jianshu.io/upload_images/9375265-fc4f9f67af1cb0da.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### C、删除元素

(1)  .remove([selector])

删除被选元素（及其子元素）,也可以添加一个**可选的选择器参数**来过滤匹配的元素

![image.png](https://upload-images.jianshu.io/upload_images/9375265-c3181833189d95b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





(2)  empty()

清空被选择元素内所有子元素

![image.png](https://upload-images.jianshu.io/upload_images/9375265-1630eb6bd974fc49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### D、包裹元素

(1)  .html([string])
这是一个**读写两用**的方法，用于**获取/修改**元素的**innerHTML**

- 当没有传递参数的时候，返回元素的innerHTML
- 当传递了一个string参数的时候，修改元素的innerHTML为参数

![image.png](https://upload-images.jianshu.io/upload_images/9375265-ecdbc9b6ebabc2b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



其中，特别注意：读写两用的方法很多，原理都类似

- 如果**结果是多个进行赋**值操作的时候会给**每个结果都赋值**

- 如果**结果多个，获取值**的时候，返回结果集中的**第一个对象**的相应值

![image.png](https://upload-images.jianshu.io/upload_images/9375265-b65f74e09094a294.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(2) .text()
和html方法类似，操作的是**DOM的innerText**值

![image.png](https://upload-images.jianshu.io/upload_images/9375265-ce4dff1fd7d144ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



# 二、属性及css操作

### A、属性

(1)  .val([value])

这是一个读写双用的方法，用来处理input的value，当方法没有参数的时候返回input的value值，当传递了一个参数的时候，方法修改input的value值为参数值

![image.png](https://upload-images.jianshu.io/upload_images/14339384-7610f39f79333fd2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(2)  .attr() / .attr(attributeName)

获取元素特定属性的值

![image.png](https://upload-images.jianshu.io/upload_images/14339384-714717eb82771581.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/14339384-bf7c43c4adc6d000.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(3)  .removeAttr()

为匹配的元素集合中的每个元素中移除一个属性（attribute）

.removeAttr() 方法使用原生的 JavaScript removeAttribute() 函数,但是它的优点是可以直接在一个 jQuery 对象上调用该方法，并且它解决了跨浏览器的属性名不同的问题。

![image.png](https://upload-images.jianshu.io/upload_images/14339384-99d2aaa5af1686b7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(4)  .prop()/.removeProp()
这两个方法是用来操作元素的property的，property和attibute是非常相似的概念

可参考  https://blog.jirengu.com/?p=222



### B、css操作

(1)  .css()

和 attr 非常相似的方法，用来处理元素的css

.css(propertyName) / .css(propertyNames)

获取元素style特定property的值

![image.png](https://upload-images.jianshu.io/upload_images/14339384-b5fa52f785444582.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(2)  .addClass(className) / .removeClass(className)

.addClass(className) / .addClass(function(index,currentClass))

为元素添加class，不是覆盖原class，是追加，也不会检查重复

![image.png](https://upload-images.jianshu.io/upload_images/14339384-051026893a23afdf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(3)  removeClass([className]) / ,removeClass(function(index,class))

移除元素单个/多个/所有class

![image.png](https://upload-images.jianshu.io/upload_images/14339384-e3c61ec617f0fac9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(4)  .hasClass(className)

检查元素是否包含某个class，返回true/false

![image.png](https://upload-images.jianshu.io/upload_images/14339384-5bd990d600152a85.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(5)  .toggleClass(className)

toggle是切换的意思，方法用于切换

![image.png](https://upload-images.jianshu.io/upload_images/14339384-86ccdbf19df1deb9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





# 三、常用方法

(1)  .each( function(index, Element) )

遍历一个jQuery对象，为每个匹配元素执行一个函数

```javascript
$('li').each(function( index ) {
  console.log( index + ":" + $(this).text() );
});
```



![image.png](https://upload-images.jianshu.io/upload_images/14339384-a709afc2c5fe34ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(2)  jQuery.extend([deep,] target [, object1 ][, objectN ] )

- 当我们提供**两个或多个对象**给 $.extend()，对象的**所有属性都添加到目标对象**（target参数）。

- 如果**只有一个参数**提供给 $.extend()，这意味着目标参数被省略。在这种情况下，jQuery**对象本身被默认为目标对象**。这样，我们可以在jQuery的命名空间下添加新的功能。这对于插件开发者希望向 jQuery 中添加新函数时是很有用的

**目标对象（第一个参数）**将被修改，并且将通过$.extend()返回。然而，如果我们想**保留原对象**，我们可以通过传递一个**空对象**作为目标对象：

```javascript
var object = $.extend({}, object1, object2);
```

**在默认情况下，通过 $.extend() 合并操作不是递归的**

如果第一个对象的属性本身是一个对象或数组，那么它将完全用第二个对象相同的key重写一个属性。这些值不会被合并。如果将  true 作为该函数的第一个参数，那么会在对象上进行递归的合并。

```javascript
var object1 = {
  apple: 0,
  banana: { weight: 52, price: 100 },
  cherry: 97
};
var object2 = {
  banana: { price: 200 },
  durian: 100
};

// Merge object2 into object1
$.extend( object1, object2 );
```



执行结果

![image.png](https://upload-images.jianshu.io/upload_images/14339384-a764c94dbbf3113b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(3)  clone( [withDataAndEvents ] )

深度复制**所有匹配的元素集合**，包括所有**匹配元素**、**匹配元素的下级元素**、**文字节点**

- 类似剪切的效果

```javascript
<div class="container">
  <div class="hello">Hello</div>
  <div class="goodbye">
    Goodbye
  </div>
</div>
$('.hello').appendTO('.goodbye')
```



执行结果
![image.png](https://upload-images.jianshu.io/upload_images/14339384-d0f08cea21361e58.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



- 如果需要的是复制而不是剪切，可以像下面这样写代码：

```javascript
$('.hello').clone().appendTo('.goodbye');
```



执行结果

![image.png](https://upload-images.jianshu.io/upload_images/14339384-d85e2f594fd7dc1f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(4)  .index() / .index(selector)/ .index(element)

从给定集合中查找特定元素index，即获取的它所在的邻居的下标

- 没参数返回第一个元素index

- 如果参数是DOM对象或者jQuery对象，则返回参数在集合中的index

  ![image.png](https://upload-images.jianshu.io/upload_images/14339384-5cfb35aabe288a27.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 如果参数是选择器，返回第一个匹配元素index，没有找到返回-1

![image.png](https://upload-images.jianshu.io/upload_images/14339384-7b3badbf1fb450e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(5)  .ready( handler )

当DOM准备就绪时，指定一个函数来执行。

虽然JavaScript提供了load事件，当页面呈现时用来执行这个事件，直到所有的东西，如图像已被完全接收前，此事件不会被触发。

在大多数情况下，只要DOM结构已完全加载时，脚本就可以运行。传递处理函数给.ready()方法，能保证DOM准备好后就执行这个函数，因此，这里是进行所有其它事件绑定及运行其它 jQuery 代码的最佳地方。

如果执行的代码需要在元素被加载之后才能使用时，（例如，取得图片的大小需要在图片被加载完后才能知道），就需要将这样的代码放到 load 事件中。

下面两种语法全部是等价的：

- $(document).ready(handler)
- $(handler)

我们经常这么使用

```javascript
$(function(){
    console.log('ready');
});
```