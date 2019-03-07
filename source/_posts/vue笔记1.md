---
$title: vue笔记1之数据绑定，指令，事件
date: 2019-03-06 23:16:04
tags:
---



### 一、Vuejs 模式 

MVVM 模式：**视图层和数据层的双向绑定**，不用关心DOM 操作的事，更多精力放在数据和业务逻辑上去



### 二、Vuejs 环境搭建

1､ 通过script 标签，引入vuejs

2、vue 脚手架工具 vue-cli 搭建【**基于nodejs npm 搭建的**】



### 三、Vue实例和数据绑定

通过构造函数 Vue 就可以创建一个 Vue 的根实例，并启动 Vue 应用—入口

```javascript
var app ＝new Vue({
   //element,用于指定页面中已存在的DOM元素，挂载到DOM中，也可以是css,是必不可少的选项
	el:'#app', 
	
	data:{ //可以声明应用内需要双向绑定的数据,也可以指向一个已经有的变量
    	msg:'开始学习vue'
	}
})
```

挂载成功后，访问属性

1､访问vue实例的属性

```javascript
app.$el  // 访问vue实例的属性，都是以 $ 开头
```

2､访问data中的属性

```javascript
app.msg //直接app.属性名
```



### 四、生命周期钩子

1､created （**还未挂载**）：实例创建完成后调用，此阶段完成了数据的观测等，但尚未挂载， $el 还不可用。需要初始化处理一些数据时会比较有用，

2､mounted el （**刚刚挂载**）：挂载到实例上后调用，一般我们的**第一个业务逻辑会在这里开始**，也就是初始化要执行的业务逻辑代码，相当于 $(document).ready()

3､beforeDestroy 实例销毁之前调用。主要解绑一些使用 addEventListener 监听的事件等



看个实例

![image.png](https://upload-images.jianshu.io/upload_images/14339384-b1c0b965b33534db.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### 五、文本插值和表达式

1､ 语法

使用双大括号  **“{{}}“**  ，会自动将我们双向绑定的数据实时显示



2､ 用法

在 {{ }} 中，除了**简单的绑定属性值**外，也可以是 **JavaScript 表达式进行简单的运算** 、 **三元运算**等

**特别注意：Vue .js 只支持单个表达式，不支持语句和流控制**



3､实例

```javascript
{{ 6+6 *3}} // 支持 简单的运算 
{{ 6<3 ? msg :a}}  // 支持 三元运算符 

{{if(6>3){}} // 不支持 书写表达式
{{var a = 6}} // 不支持 多行表达式 var a=6 相当于 var a;a = 6;
{{ var book = ’ Vue . js 实战 ’}} // 不支持 语句
{{ if (ok) return msg }} // 不支持 流控制
```



### 六、过滤器

1､ 作用

格式化文本【字母全大写、货币千位使用逗号分隔符】



2､用法

在 {{}} 插值的尾部添加一小管道符 “ | ” 对数据进行过滤

```javascript
{{date | formatDate}} // | 后面接的是 过滤器的名字

{{date | filter1 | filter2 }} // 过滤器的串联

{{date | formatDate('arg1', 'arg2')}} //过滤器的参数
```



3､规则

自定义的， 通过**给 Vue 实例添加选项 filters** 来设置


**注：{{date | formatDate(66,99)}} 中的第1个和第2个参数，分别对应script 标签内 过滤器 formatDate 的第2个 a 和 第3个参数 b **，而 script 标签内的过滤器 formatDate 第一个参数是 date 

![image.png](https://upload-images.jianshu.io/upload_images/14339384-cadea4afa929d0ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### 七、指令 

1､ 定义

带有前缀 v- ，能帮我们快速完成 DOM 操作，循环渲染，显示和隐藏

2､ 部分指令

A、v-text ：解析文本 等同于 {{ }} 文本插值

```java
<span v-text="apple"></span> === {{apple}} //true
```



B、v-html ：解析html

C、v-bind ：动态更新html 元素上的 属性，如id,class等

D、v-on ： 绑定事件监听器

v-on 用法：

1､在普通元素上，可以**监听原生的 DOM 事件**（ click、dblclick、 keyup, mousemove 等）

2､**表达式可以是一个方法名**，这些方法都写在 **Vue 实例的 methods 属性内**，并且是函数的形式，

3､函数内的 **this 指向的是当前 Vue 实例本身**，因此可以直接使用 **this.xxx** 的形式来访问或修改数据

**注：vue中用 到的所有方法都定义在methods中**



### 八、语法糖

在不影响功能的情况下，用简洁的方法实现同样的效果，从而更方便程序开发















