---
title: ajax
date: 2018-11-19 17:25:20
tags:
---

#### 什么是ajax. (异步的Javascript and XML)

Ajax 是一种技术方案，但并不是一种新技术。它依赖的是现有的CSS/HTML/Javascript,而其中最核心的依赖是浏览器提供的XMLHttpRequest对象，是这个对象使得浏览器可以发出HTTP请求与接收HTTP响应。实现在页面不刷新的情况下和服务端进行数据交互。

###### 来一个实例（写一个ajax）


```javascript
var xhr = new XMLHttpRequest()//建立对象
xhr.open('GET','/hello.json',true)//设置参数,true表示异步，异步代表需要绑定一个事件
// "/hello.json"表示域名+/hello.json,如果http-server打开静态服务器，127.0.0.1:8080/hello.json
xhr.send()//发送请求
xhr.addEventListener('load',function(){
   var data = xhr.responseText
       console.log(data)    
})
```

###### 进一步完善

```javascript
var xhr = new XMLHttpRequest()
xhr.open('GET','/hello.json',true)
xhr.send()

//readystate的change事件
xhr.onreadystatechange = function(){
    if(xhr.readystate === 4 && xhr.status === 200){
       console.log(xhr.responsText)
    }
}
// xhr.readystate 它的交互流程是否完毕，有没结束
// xhr.status 服务器的状态 表示数据是否ok,是否正常

xhr.addEventListener('readystatechange',function(){
    console.log('readystate:',xhr.readyState)
})

//load是 readyState变为4时，会自动触发load,所以我们不用管readyState ，直接写onload, 表示 readyState是4啦
xhr.addEventListener('load',function(){
    console.log(xhr.status)
    if(xhr.status >= 200 && xhr.status < 300 || xhr.status === 304){
       var data = xhr.responseText
       console.log(data)
    }else{
        console.log('error')
    }
})
```

最后完善：

```javascript
var xhr = new XMLHttpRequest()
xhr.open('GET', '/hello.json', true)
xhr.onreadystatechange = function(){
    if(xhr.readyState === 4) {
        if((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
            //成功了
            console.log(xhr.responseText)
        } else {
            console.log('服务器异常')
        }
    }
}
xhr.onerror = function(){
    console.log('服务器异常')
}
xhr.send()
```



换种写法

```javascript
var xhr = new XMLHttpRequest()
xhr.open('GET', 'hello.json', true)
xhr.onload = function(){
    if((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
        //成功了
        console.log(xhr.responseText)
    } else {
        console.log('服务器异常')
    }
}
xhr.onerror = function(){
    console.log('服务器异常')
}
xhr.send()
```



- **GET形式的数据请求**

  会传递参数(username、password)  把数据拼装成url形式,放到？后面

```javascript
var xhr = new XMLHttpRequest()
xhr.open('GET','/login?username=xwu&password=123',true)
xhr.send()

//readystate的change事件
xhr.onreadystatechange = function(){
    if(xhr.readystate === 4 && xhr.status === 200){
       console.log(xhr.responsText)
    }
}
// xhr.readystate 它的交互流程是否完毕，有没结束
// xhr.status 服务器的状态 表示数据是否ok,是否正常

xhr.addEventListener('readystatechange',function(){
    console.log('readystate:',xhr.readyState)
})

//load是 readyState变为4时，会自动触发load,所以我们不用管readyState ，直接写onload, 表示 readyState是4啦
xhr.addEventListener('load',function(){
    console.log(xhr.status)
    if(xhr.status >= 200 && xhr.status < 300 || xhr.status === 304){
       var data = xhr.responseText
       console.log(data)
    }else{
        console.log('error')
    }
})
```



- **POST形式数据请求**

  不会把数据拼装成url形式,直接发的数据,然后数据拼好了放到send里面。【*数据拼接的过程可以写一个函数*】

```javascript
	var xhr = new XMLHttpRequest()
	xhr.open('POST','/login',true)
	//xml.send('username=xwupassword=123')
	xhr.send(makeUrl({
		username: 'xwu',
		age: 2
	}))
	
	xhr.addEventListener('load',function(){
		console.log(xhr.status)
		if((xhr.status >= 200 && xhr.status < 300) || xhr.status === 304){
		var data = xhr.responseText
			console.log(data)
		}else{
			console.log('error')			
		}
	}
	xhr.onerror = function(){
		console.log('error')
	}
	
	makeUrl({
		username: 'xwu',
		age: 2
	})

	function makeUrl(obj){
		var arr = []
		for(var key in obj){
			arr.push(key + '=' + obj[key])
		}
		return arr.join('&')
	}
```



封装一个ajax

```javascript
function ajax(opts){
    var url = opts.url
    var type = opts.type || 'GET'
    var dataType = opts.dataType || 'json'
    var onsuccess = opts.onsuccess || function(){}
    var onerror = opts.onerror || function(){}
    var data = opts.data || {}

    var dataStr = []
    for(var key in data){
        dataStr.push(key + '=' + data[key])
    }
    dataStr = dataStr.join('&')

    if(type === 'GET'){
        url += '?' + dataStr
    }

    var xhr = new XMLHttpRequest()
    xhr.open(type, url, true)
    xhr.onload = function(){
        if((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
            //成功了
            if(dataType === 'json'){
                onsuccess( JSON.parse(xhr.responseText))
            }else{
                onsuccess( xhr.responseText)
            }
        } else {
            onerror()
        }
    }
    xhr.onerror = onerror
    if(type === 'POST'){
        xhr.send(dataStr)
    }else{
        xhr.send()
    }
}

ajax({
    url: 'http://api.jirengu.com/weather.php',
    data: {
        city: '北京'
    },
    onsuccess: function(ret){
        console.log(ret)
    },
    onerror: function(){
        console.log('服务器异常')
    }
})
```



可参考 https://segmentfault.com/a/1190000004322487

