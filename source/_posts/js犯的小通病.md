---
title: js犯的小通病
date: 2018-12-20 16:39:09
tags:
---

### 一､ console.log 和 return

 1､情况一、a的值是 undefined

```javascript
function fn(a,b){
   console.log(a+b); 
    //console.log 相当于画画，把a+b画出来，然后在控制台下可以看见出来，但是它并没有放在变量a里面
    return undefined;
}
var a = fn()
/*
fn()看成一个整体，看成一个值，也就是函数的值，是 return 出来的值
a的值并不是console.log(a+b)的值，是 return 出来的值，也就是 undefined
*/
```

2､情况二、a的值是 undefined

```javascript
function fn(a,b){
   return console.log(a+b)   
}
var a = fn(1,3) 

/*
控制台是看到值了，但是a 还是undefined, 为什么呢
因为a 是 函数fn，return 出来的值，也就是console.log执行的结果，但是console.log也是函数，那console.log(a+b)的值是多少呢，它的返回值是undefined,它本身的值是没有的
*/
```

3､情况三、正确这么写才对

```javascript
function fn(a,b){
   console.log(a+b); 
   return a+b;
}
var a = fn(1,3)
```



### 二、切换效果需注意事项

html文件

```html
<style>
.tab-header{display: flex;}
.tab-header div{padding:5px 15px 0;background:#ccc;margin-right:5px;}	
.tab-header div.active{color:red;}

.tab-panels div{display: none;background:pink;}
.tab-panels div.active{display: block;}
</style>

<div class="tab-container">
	<div class="tab-header">
		<div class= "active">1</div>
		<div>2</div>
		<div>3</div>
	</div>
	<div class="tab-panels">
		<div class="active">box1</div>
		<div>box2</div>
		<div>box3</div>
	</div>
</div>
```


js文件

```javascript
// 选择好之后 去绑定事件 因为它是列数组对象,不能用 .on('click',function(){})事件，可以用forEach
var tabs = document.querySelectorAll('.tab-header div');
var panels = document.querySelectorAll('.tab-panel div');
tabs.forEach(function(node){
    node.onclick = function(){
        var index = 0;
        tabs.forEach(function(tab,idx){
           console.log(tab);        
           tab.classList.remove('active');   
           if(node === tab){
            index = idx;
        	}
        });
        this.classList.add('active');  
        
        panels.forEach(function(panel){
            panel.classList.remove('active');
            panels[index].classList.add('active');
        })    
    };
});
```

实现了一个切换效果

![image.png](https://upload-images.jianshu.io/upload_images/14339384-82e5ade1267e519c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

假设页面有多个切换，上面这写法不行了，所以呢，我们要优化代码

第一次优化：

```javascript
var Tab = {
    init:function(){
        this.tabs = document.querySelectorAll('.tab-header div');
        this.panels = document.querySelectorAll('.tab-panel div');
    },
    bind:function(){
        var self = this;
        self.tabs.forEach(function(node){
            node.onclick = function(){
                var index = 0;
                self.tabs.forEach(function(tab,idx){
                   console.log(tab);        
                   tab.classList.remove('active');   
                   if(node === tab){
                    index = idx;
                    }
                });
                this.classList.add('active');  

                self.panels.forEach(function(panel){
                    panel.classList.remove('active');
                    self.panels[index].classList.add('active');
                })    
            }
        })
    }
}
Tab.init()
```

执行结果发现 ：

1､只能**实现一个切换**，要**多个切换的实现**，代码部分还得继续优化呀

2､但是代码部分简洁了，页面只有一个全局变量Tab



好吧，**继续更改优化吧**

```javascript
function Tab(container){
    this.container = container;
    this.init();
    this.bind();
}

Tab.prototype.init = function(){
    this.tabs = this.container.querySelectorAll('.tab-header div');
    this.panels = this.container.querySelectorAll('.tab-panel div');
    this.bind();
}

Tab.prototype.bind = function(){
 	var self = this;
    self.tabs.forEach(function(node){
        node.onclick = function(){
            var index = 0;
            self.tabs.forEach(function(tab,idx){
                console.log(tab);        
                tab.classList.remove('active');   
                if(node === tab){
                        index = idx;
                }
            });
            this.classList.add('active');  

            self.panels.forEach(function(panel){
                panel.classList.remove('active');
                self.panels[index].classList.add('active');
            })    
        }
    })  
}

//var tab1 = new Tab(document.querySelectorAll('.tab-container')[0])
//var tab2 = new Tab(document.querySelectorAll('.tab-container')[1])

document.querySelectorAll('.tab-container').forEach(function(container){
    new Tab(container)
})
```

Demo 地址：http://js.jirengu.com/qutaz/6/edit

老师地址：http://js.jirengu.com/setod/1/edit?html,output



### 三、写js 的三步曲

1､ 初始化 init

2､绑定事件 bind

3､渲染数据 render

```javascript
var App={
    init: function(){},
    bind: function(){},
    render: function(){}
}
App.init() // 切记别忘记了这一句，不然代码没法执行，老掉的坑就是没加这一句，请求的数据，拿不到
```

