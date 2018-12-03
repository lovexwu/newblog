---
title: ajax
date: 2018-11-19 17:25:20
tags:
---

#### 什么是ajax. (异步的Javascript and XML)

Ajax 是一种技术方案，但并不是一种新技术。它依赖的是现有的CSS/HTML/Javascript,而其中最核心的依赖是浏览器提供的XMLHttpRequest对象，是这个对象使得浏览器可以发出HTTP请求与接收HTTP响应。实现在页面不刷新的情况下和服务端进行数据交互。

一句话总结：我们使用`XMLHttpRequest`对象来发送一个`Ajax`请求

##### 来一个简易版实例（写一个ajax）


```javascript
var xhr = new XMLHttpRequest()//建立对象
xhr.open('GET','/hello.json',true)
//创建一个GET请求，采用异步,true表示异步，异步代表需要绑定一个事件
// "/hello.json"表示域名+/hello.json,如果http-server打开静态服务器，127.0.0.1:8080/hello.json
xhr.send()//发送请求
xhr.addEventListener('load',function(){
   var data = xhr.responseText
       console.log(data)    
})
```

如果是同步请求的话，代码是这样子的

```javascript
var xhr = new XMLHttpRequest()
xhr.open('GET','/hello.json',false) //设置参数，false表示同步
xhr.send()
var data = xhr.responseText
console.log(data)
```

##### 这里提到了同步和异步，那我们稍稍说解下

**同步：** 我发了一个请求，然后属于等待中，就卡死啦,这个时候只有后端给我响应之后，我才可以继续操作,代码才能继续往下执行

就相当于我在算一个很复杂的数据，花了5分钟一样，在5分钟内一直属于算的状态，所以后面的js 是不执行的,是卡死状态

**异步：** 我发了一个请求，我就不管了，然后我会去监听我的某一个状态,当状态发生改变时，也就是说达到我的一个需求时或是满足我的条件时,那我再去做一个事情

像这些就是异步：

**1､点击事件**

绑定一个事件后，我就不管了,就不去执行它,什么时侯去执行呢

当达到某一个条件（用户去点击，或是用户去点击去触发那个事件时）

那我才去执行它

**2､setTimeout**

绑定一个函数后，它不执行,什么时侯去执行呢

当这个时间点到了之后，浏览器内部会发出一个事件（时间到了的这个事件），去执行它

**3､ajax **

也是一样的，我的请求发出去之后，就先不去管了，什么时候去执行呢

当我这里面内部状态发生改变的时侯，我监听到了，我觉得该去处理了，我就去处理它

##### 进一步完善

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

##### 最后完善：

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

##### 换种写法

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

a、GET形式的数据请求 (**数据拼装成url形式**)

准确地说是传递参数(username、password)  把数据拼装成url形式,放到?后面】

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

b、POST形式数据请求 (**直接发送数据**)

准确地说是不会把数据拼装成url形式,而是把数据拼好了放到send里面。当然数据拼接的过程可以写一个函数

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

##### 封装一个ajax

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

##### 可参考  https://segmentfault.com/a/1190000004322487