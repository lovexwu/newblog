---
title: jQuery之选择器
date: 2018-12-16 16:07:19
tags:
---

## 一、选择器

看图就会发现，jQuery选择器相当于复习CSS选择器哦，所以呀，开发者在众多js库中迅速青睐于jQuery。

![image.png](https://upload-images.jianshu.io/upload_images/14339384-2b841af1c0fb82be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14339384-322dad93b88a9d72.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![image.png](https://upload-images.jianshu.io/upload_images/14339384-af9e22827ca94926.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



## 二、常用方法

(1)  .eq(index)， .get([index])

- 获取到指定index的jQuery对象，可以用eq 方法

```javascript
$('div').eq(3); // 获取到第四个div
```

- 通过类数组下标的获取方式或者get方法获取指定index的DOM对象，也就是我们说的jQuery对象转DOM对象

  ```javascript
  $('div')[3];
  $('div').get(3);
  // 都是获取到第四个div
  ```

注：**get() 不写参数把所有对象转为DOM对象返回**

![image.png](https://upload-images.jianshu.io/upload_images/14339384-8666bcb3a1eea64d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(2)  .next([selector])，.prev([selector])

next 取得匹配的元素集合中**每一个元素紧邻**的后面**同辈元素**的元素集合。如果提供一个选择器，那么只有紧跟着的兄弟元素满足选择器时，才会返回此元素。

prev正好相反，获取元素**之前**的同辈元素

![image.png](https://upload-images.jianshu.io/upload_images/14339384-64983fc7e076b542.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(3)  .nextAll([selector])， .prevAll([selector])

nextAll获得每个匹配元素集合中每个元素**所有后面的同辈元素**，选择性筛选的选择器

prevAll与之相反，获取元素前面的同辈元素

![image.png](https://upload-images.jianshu.io/upload_images/14339384-6d39aa09435a2e50.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(4)  .siblings([selectors])

获得匹配元素集合中**每个元素的兄弟元**素,可以提供一个可选的选择器

![image.png](https://upload-images.jianshu.io/upload_images/14339384-6258c253b1991080.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(5)  .parent([selector])

取得匹配元素集合中，**每个元素的父元素**，可以提供一个可选的选择器

![image.png](https://upload-images.jianshu.io/upload_images/14339384-273b7d8b67359c96.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(6)  .parents([selector])

获得集合中**每个匹配元素的祖先元素**，可以提供一个可选的选择器作为参数

![image.png](https://upload-images.jianshu.io/upload_images/14339384-3bbe677759f45cd5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(7)  .children([selector])

获得匹配元素集合中**每个元素的子元素**，选择器选择性筛选

![image.png](https://upload-images.jianshu.io/upload_images/14339384-f22b025c28499844.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(8)  .find([selector])

查找符合选择器的后代元素

![image.png](https://upload-images.jianshu.io/upload_images/14339384-ae87bc1a22fc5d50.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(9)  .filter(selector) ，.filter(function(index))

筛选当前结果集中**符合条件的对象**，参数可以是一个**选择器**

![image.png](https://upload-images.jianshu.io/upload_images/14339384-06dcf3f04a6d23c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



参数也可以是一个**函数**

![image.png](https://upload-images.jianshu.io/upload_images/14339384-a0af0ed388d14b9b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(10)  .has(selector) ，.has(dom)

筛选匹配元素集合中的那些有**相匹配的选择器**或**DOM元素的后代元素**

![image.png](https://upload-images.jianshu.io/upload_images/14339384-170cfbece22bd765.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(10)  .is(selector) ， is(function(index)) ，is(dom/jqObj)

判断当前匹配的元素集合中的元素，是否为一个选择器，DOM元素，或者jQuery对象，如果这些元素**至少一个匹配给定的参数**，那么返回true

![image.png](https://upload-images.jianshu.io/upload_images/14339384-13eb3233c305f46b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



使用 jQuery 实现 多个Tab 切换效果

```javascript
var change = function(){
  var t=$('.slider').find('.item');
  t.click(function(){
    console.log(this);
    $(this).parents('.slider').find('.item').removeClass('active');
    $(this).addClass('active');
    $(this).parents('.slider').find('.box').removeClass('active');
    $(this).parents('.slider').find('.box').eq($(this).index()).addClass('active');
  });
}
change();
```



遇到的坑 ，页面多个tab切换时，一定要找到相应的容器，即其**父元素($(this).parents('.slider'))** ，再去找到其对应的元素，进行操作

![image.png](https://upload-images.jianshu.io/upload_images/14339384-1188414fc89ee450.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



如果直接元素进行操作，就会出现两个tab切换相互影响

![image.png](https://upload-images.jianshu.io/upload_images/14339384-801f3debcf588a0a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



更多可参考 http://jquery.com



