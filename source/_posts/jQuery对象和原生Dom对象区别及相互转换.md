# 一、区别

- **jQuery 对象：**通过jQuery包装DOM对象后产生的对象

假设获取header元素内的文本内容,其中**text()是jQuery里的方法**
```javascript
$('.header').text()
```

等同于**DOM对象实现**

```javascript
document.querySelector('.header').innerText
```

- **DOM对象：**w3c标准用于操作文档的API



#二、DOM对象转jQuery对象

把DOM对象包装起来【$(DOM对象)】，就可以获得一个jQuery对象了

```javascript
var header = document.querySelector('.header')  //Dom 对象
$header = $(header) //jQuery对象
```



#三、jQuery对象转DOM对象

jQuery对象是类数组对象，通过数组下标方式获取jQuery中的DOM对象
```javascript
$p[0]   //选中了第一个dom对象
```



#总结

可以任意的相互转换jQuery对象和DOM对象。
**但，jQuery对象是jQuery独有的，只能使用jQuery里的方法，不能使用DOM的方法，反之一样** 
像类似下面的写法是不可以的，这样子会报错

```javascript
$('.header').innerText
document.querySelector('.header').text()
```

