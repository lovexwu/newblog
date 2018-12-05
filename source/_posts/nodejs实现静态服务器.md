---
title: nodejs实现静态服务器
date: 2018-11-25 22:30:00
tags:
---

看了一天的nodejs 实现静态服务器 ,还是晕乎乎，费话不说了，直接上代码，记笔记吧！

首先是页面index.js代码如下：

##### 实例1

```javascript
# require-----nodejs通过它来加载模块

var http = require('http') 
/*
http是nodejs的内置模块,它是一个对象，然后这个对象提供了一些方法，实现我们所需要的一些功能
整个服务器底层都是由nodejs的http模块实现的

函数createServer内部是一个异步的过程,内部会创建一个服务器，创建服务器时里面有一个回调function(req,res),把函数function(req,res)作为对应的参数，来处理我们的请求

换句话说，创建服务器后，当浏览器访问这个服务器时,那请求呢，底层会封装成一个对象，这个对象就是第一个参数，是req,可以随便起名

req 用户请求的信息都在这里，用户的(ip ,访问的域名,浏览器的一些信息)
res 需要返回给用户哪些东西的这个对象
*/

# res.write是把数据放到响应体Response里面
# 响应体 是 页面的查看源代码，
# 响应头 是 Response Header

//setHeader 设置响应头 

 var server = http.createServer(function(req, res){
     console.log('hello world')
     res.setHeader("Content-Type","text/paint; charset=utf-8")
     res.write('<h1> 你好</h1>') 
     res.end()
 })
 server.listen(9000) // listen方法 启动服务器 ,使这个服务器监听 9000端口


```

##### 实例2

```javascript

var server = http.createServer(function(request, response){
  setTimeout(function(){
    /*text/plain 告诉浏览器，你接收到的字符串，你把它当成字符去渲染.  
      text/html 告诉浏览器，你接收到的字符串，你把它当成html去渲染
      charset=utf-8 告诉浏览器，用 utf-8解码
      charset=bgk 告诉浏览器，用 bgk 解码
    */
    response.setHeader('Content-Type','text/html; charset=utf-8')
    //response.writeHead(404, 'Not Found')
    response.writeHead(200,'haha') // 相当于 状态码 status code
    response.write('<html><head><meta charset="gbk" /></head>')
    response.write('<body>')
    response.write('<h1>你好</h1>')
    response.write('</body>')
    response.write('</html>')
    
    response.end()
  },2000);
})

console.log('open http://localhost:8080')
server.listen(8080)
```



##### 接下来是终端

```javascript
➜  ~ cd node-server // 去到对应的目录
➜  node-server git:(master) ✗ cd step0
➜  step0 git:(master) ✗ node index.js //通过node 加上文件名, 启动服务器

如果页面有更改需关闭服务器重新启动，终端操作 ctrl + c 关闭，然后重新启动 node index.js即可!
```

然后浏览器地址输入如下地址 浏览即可！其中9000是对应的端口

```javascript
localhost: 9000
```



##### 实例3  实现一个静态服务器

1､把我们的代码放到static文件夹下,

2､把我们的网站放到远程的机器在上

3､然后通过执行**node server.js** 去运行服务器

![list.jpg](https://upload-images.jianshu.io/upload_images/9375265-a85157201549beb2.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```javascript
var http = require('http') //创建服务器的模块
var path = require('path') //处理文件路径的模块,自动识别url类型
var fs = require('fs') // 读写文件的 ，读到数据，也可以往文件里写东西
var url = require('url') // 自动解析url 得到一些信息 
/*相当于location, url 作为参数，然后进行解析，得到一个对象,然后我们可以使用里面的某些部分了
不用使用正则去提取啦*/

function staticRoot(staticPath,req,res){
    console.log(staticPath)
    
    console.log(req.url)
    var pathObj = url.parse(req.url,true)
    console.log(pathObj)
}

/*
if(pathObj.pathname === '/'){
    pathObj.pathname += 'index.html'
}
index.html 作为默认的
*/

var filePath = path.join(staticPath,pathObj.pathname)

/* 同步读文件
var fileContent = fs.readFileSync(filePath,'binary')
res.write(fileContent,'binary')
res.end()
*/

//异步读文件
fs.readFile(filePath,'binary',function(err,fileContent){
    if(err){
        console.log('404')
        res.writeHead(404,'not find')
        res.end('<h1> 404 Not Found')
    }else{
       console.log('ok')
       res.writeHead(200,'ok')
       res.write(fileContent,'binary')
       res.end()
    }
})

console.log(path.join(__dirname,'static'))
//__dirname：当前模块的文件夹名称，nodejs内置的变量，代表当前代码的server.js的文件夹路径。也就是step1的绝对路径,然后拼上static路径，最终static的绝对路径

var server = http.createServer(function(req,res){
    staticRoot(path.join(__dirname,'static'),req,res)
})

server.listen(8080)
console.log('visit http://localhost:8080')
```

__dirname 请参照 http://nodejs.cn/api/modules.html#modules_dirname

总结如下简图

![pic.jpg](https://upload-images.jianshu.io/upload_images/9375265-3999c2e18dac389d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



用户的浏览器随便输入一个URL，http://localhost:8080/a/b/c 

这时浏览器会把这个请求向这个域名http://localhost:8080对应的IP去发送

发完之后这个请求从左边浏览器到了右边的远程机器上

然后根据端口进行匹配,匹配上后，交给某个服务器

这个服务器就拿到了这个请求,一个请求可以当成一个对象,对象里有关于这个请求的信息

拿到之后，在服务器里进行处理,处理好之后，把结果再从服务器发回浏览器,就行了

发回去分为两部分，一个是响应头，一个是响应体

来一个简单版的静态服务器 server-simple.js

```javascript
var http = require('http')
var fs = require('fs')

var server = http.createServer(function(req,res){
    console.log(__dirname + '/static' + req.url)
    // 当一个请求到来时，通过当前的目录（__dirname）step1,加上'/static'，再加上'req.url',拼装成一个完整的路径
    try{
        var fileContent = fs.readFileSync(__dirname + '/static' + req.url)
        // 然后去读这个文件,读完之后，得到结果
        res.write(fileContent) // 得到结果之后，再把结果发出去 
    }catch(e){
        res.writeHead(404,'not found')
    }
    res.end()
})
server.listen(8080)
console.log('visit http://localhost:8080')
```

如需要nodejs 服务器 路由解析 上面代码改为：

// 其中路由是指域名后边的东西 如：localhost:8080/user/123 中的 '/user/123'

```javascript
var http = require('http')
var fs = require('fs')

http.createServer(function(req,res){
    switch(req.url){
        case 'getWeather':
        	res.end(JSON.stringify({a:1,b:2}))
        	break;
        case 'user/123':
        	res.end(fs.readFileSync(__dirname + '/static/user.tpl'))
        	break;
        default:
        	res.end(fs.readFileSync(__dirname + '/static' + req.url))
    }
}).listen(8080)
```

