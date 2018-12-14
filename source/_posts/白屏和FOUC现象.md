---
title: 白屏和FOUC现象
date: 2018-10-01 18:01:20
tags:
---

通过以下语句将CSS文件的加载时间拉长，来演示白屏和FOUC现象

```css
<link rel = "stylesheet" href = "b.css?t=10">
<link rel = "stylesheet" href = "a.css?t=3">
```



##一、白屏效果

Chrome浏览器的加载机制会出现白屏的现象

(1)  当我们访问服务器时，css在加载过程中，页面是这样的：
![p2.jpg](https://upload-images.jianshu.io/upload_images/14339384-816e95cceee328f4.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(2)  当有一个css文件加载完成时，页面依然白屏：
![p3.jpg](https://upload-images.jianshu.io/upload_images/14339384-dfce2b6069e4ee24.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(3)  当所有css文件加载完成时，浏览布局渲染，页面显示出来应有的效果：
![p4.jpg](https://upload-images.jianshu.io/upload_images/14339384-16f43d75920527b3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



##二、FOUC效果

Firefox浏览器的加载机制会出现FOUC的现象

(1)  当我们访问服务器时，在任何一个css文件未加载完成时，页面已经有显示文本显示了：
![p5.png](https://upload-images.jianshu.io/upload_images/14339384-802f547fe7896b1d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

(2)  当有一个css文件加载完成时，浏览器就会通过已经加载完成的css文件渲染页面，没有加载完成的继续加载：
![p6.png](https://upload-images.jianshu.io/upload_images/14339384-4ca7c061954e6490.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(3)  当全部css文件加载完成后，页面的最终呈现最终的效果，在每一个css文件加载完成后，页面的样式会发生变化：
![p7.png](https://upload-images.jianshu.io/upload_images/14339384-f45228727bc00c4b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)