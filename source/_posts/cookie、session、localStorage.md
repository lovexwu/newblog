---
title: cookie、session、localStorage
date: 2018-11-18 16:35:39
tags:
---

#### 一、cookie ：

1、存储在浏览器上的一小段数据，用来记录某些当页面关闭或刷新后仍然需要记录的信息。在控制台用 document.cookie 查看你当前正在浏览的网站的cookie

2、可以使用js 在浏览器直接设置（用于记录不敏感信息，如用户名),也可 以在服务端使用HTTP协议规定的set-cookie来让浏览器种下cookie,这是最常见的做法。（打开一个网站，清除全部cookie, 然后刷新页面，在network的Response headers 试试找一找set-cookie吧）

3、每次网络请求Request headers中都会带上cookie. 所以如果cookie 太多太大对传输效率会有影响。

4、一般浏览器存储cookie 最大容量为4k,所以大量数据不要存到cookie。

5、设置cookie时的参数：

a、path: 表示cookie影响到的路径，匹配该路径才发送这个cookie。expires和maxAge: 告诉浏览器cookie时候过期，maxAge是cookie多久后过期的相对时间。不设置这两个选项时会产生session cookie，session cookie 是transient的，当用户关闭浏览器时，就被清除。一般用来保存session 的 session 的 session_id。

b、secure：当secure值为true时，cookie在HTTP中是无效，在HTTPS中才有效

c、httpOnly：浏览器不允许脚本操作document.cookie去更改cookie。一般情况下都应该设置这个为true。这样可以避免被xss 攻击拿到 cookie。

#### 二、session

当一个用户打开淘宝登录后，刷新浏览器仍然展示登录状态。服务器如何分辨这次发起请求的用户是刚才登录过的用户呢？这时就使用了session保存状态。用户在输入用户名密码提交给服务端，服务端验证通过后会创建一个session用于记录用户的相关信息。这个session可保存在服务器内存中，也可保存在数据库中。

- 创建session后，会把关联的session_id通过setCookie添加一http响应头部中。
- 浏览器在加载页面时发现响应头部有set-cookie字段，就把这个cookie种到浏览器指定域名中。
- 当下次刷新页面时，发送的请求会带上这条cookie,服务端在接收到后根据这个session_id来识别用户。

cookie是存储在浏览器里的一小段数据，而session是一种让服务器能识别某个用户的机制，session在实现的过程中需要使用cookie。二者不是同一维度的东西。



#### 三、localStorage

1､ localStorage HTML5本地存储web storage 特性之一，用于将大量数据（最大5M）保存在浏览器中，保存后数据永远不会失效过期，除非用js 手动清除。

2､ 不参与网络传输

3､一般用于性能优化，可以保存图片、js、css、html模板、大量数据



### 总结：

sessionStorage、localStorage是HTML5提供的Web Storage API提供的，可以避免数据在浏览器和服务器之间不必要的来回传递。  sessionStorage、 localStorage 、 cookie 都是在浏览器端存储的数据。  

三者之间的区别： 

#####  cookie: 

1､每个域名的存储量有限（一般是4k）      

2､所有域名的存储量有限  

3､会跟随请求被发送到服务器上  

4､有个数限制，不同浏览器下，一个域名下cookie的个数有限，并且限制数量可能不一样  

##### sessionStorage:  

1､当浏览器窗口关闭的时候， sessionStorage 就会被销毁  

2､存储容量大(一般比localStorage的存储容量大)  

##### localStorage:  

1､在客户端永久保存  

2､单个域名的存储容量大(一般为5M)  

3､总体数量无限制





