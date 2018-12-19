---
title: jQuery之ajax
date: 2018-12-19 11:48:42
tags:
---

## 一、jQuery.Ajax()

#### A、设置方式

(1)  $.ajax( url[,settings])

(2)  $ajax([settings])

```javascript
$.ajax({
    url: 'xxx.php', //请求的接口
    type: 'GET', // 类型
    data: {// json格式的传递参数
        name: 'Byron',
        age: 24,
        sex: 'Male'
    },
    dataType: 'json' //会自动解析json格式
}).done(function(result){
//.done 请求成功
    console.log(result);

}).fail(function(jqXHR, textStatus){
//.fail 请求失败
    consloe.log(textStatus);

});
```

这样子，发送了一个get 请求



#### B、常用参数

(1) async：默认设置下，所有请求均为**异步请求**（也就是说这是**默认设置为 true** ）。如果需要发送同步请求，请将此选项设置为 false

(1) beforeSend：请求发送前的回调函数，用来**修改请求发送前jqXHR对象**，此功能用来设置**自定义 HTTP 头**信息，等等。该jqXHR和设置对象作为参数传递

(2) cache：如果设置为 **false** ，浏览器将**不缓存此页面**。注意: 设置cache为 false将在 HEAD和GET请求中正常工作。它的工作原理是在GET请求参数中附加"_={timestamp}"

(3) context：这个对象用于设置Ajax **相关回调函数的上下文**。 默认情况下，这个上下文是一个ajax请求使用的参数设置对象

(4) data：**发送到服务器的数据**。将自动转换为请求字符串格式。**GET 请求**中将附加**在 URL 后面**，**POST请求作为表单数据**

(5) headers：一个额外的 {键:值} 对映射到请求一起发送。此设置会**在beforeSend 函数调用之前**被设置 ;因此，请求头中的设置值，会被beforeSend 函数内的设置覆盖

(6) method：**HTTP 请求方法** (比如："POST", "GET ", "PUT"，1.9之前使用“type”)



使用jQuery处理ajax请求，其实挺简单，比如

```javascript
$.ajax({
  method: "POST",
  url: "some.php",
  data: { name: "John", location: "Boston" }
}).done(function( msg ) {
  alert( "Data Saved: " + msg );
});
```



## 二、jQuery.get() | jQuery.post()

#### A、设置方式

(1) $.get（url [，data][，success] [，dataType]）

(2)$.get（[settings]）

在默认是GET，dataType是 Json， 且没有data情况下，发送一个简单请求，得到数据

```javascript
 $.get('http://api.jirengu.com/fm/getChannels.php')
   .done(function(channelInfo){
    console.log(channelInfo)
  });
```

![image.png](https://upload-images.jianshu.io/upload_images/14339384-702f94d07f443c0a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



#### B、实例

(1) 请求test.php页面，但忽略返回结果。

```javascript
`$.get( "test.php" );`
```



(2) 请求test.php页面并发送一些其他数据（同时仍然忽略返回结果）。

```javascript
`$.get( "test.php", { name: "John", time: "2pm" } );`
```



(3) 将数据数组传递给服务器（同时仍然忽略返回结果）。

```javascript
`$.get( "test.php", { "choices[]": ["Jon", "Susan"] } );`
```



(4) 请求test.php（HTML或XML，具体取决于返回的内容）的结果。

```javascript
`$.get( "test.php", function( data ) {  alert( "Data Loaded: " + data );});`
```



(5) 通过额外的数据有效负载（HTML或XML，取决于返回的内容）来请求test.cgi的结果。

```javascript
`$.get( "test.cgi", { name: "John", time: "2pm" } )  .done(function( data ) {    alert( "Data Loaded: " + data );  });`
```



(6) 获取以json格式返回的test.php页面内容（<？php echo json_encode（array（“name”=>“John”，“time”=>“2pm”））;？>），并添加它到页面。

```javascript
`$.get( "test.php", function( data ) {  $( "body" )    .append( "Name: " + data.name ) // John    .append( "Time: " + data.time ); //  2pm}, "json" );`
```



#### C、处理 get 和 post 请求的方法

```javascript
$.ajax({
  url: url,
  data: data,
  success: success,
  dataType: dataType
});

$.ajax({
  type: "POST",
  url: url,
  data: data,
  success: success,
  dataType: dataType
});

//dataType：从服务器返回的预期的数据类型。默认：智能猜测（xml, json, script, 或 html）
```



## 三、jQuery.getJSON( url [, data ][, success(data, textStatus, jqXHR) ] )

使用一个HTTP GET请求从**服务器加载JSON编码**的数据，这是一个Ajax函数的缩写，这相当于:

```javascript
$.ajax({
  dataType: "json",
  url: url,
  data: data,
  success: success
});
```

可参考 http://api.jquery.com

