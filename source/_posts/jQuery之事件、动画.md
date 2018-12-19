---
title: jQuery之事件、动画
date: 2018-12-18 11:17:35
tags:
---

# 一、事件

在1.7之前的版本中jQuery处理事件有多个方法， (google 搜索: jquery live bind degelate)作用各不相同，后来统一的使用 **on / off**  方法

(1)  .on( events [,selector ][,data ], handler(eventObject) )

##### A、参数

- events：**事件类型**和可选的**命名空间**，比如"click", "keydown.myPlugin"

  注：如有**多个**事件类型，用**空格**分隔

- selector：一个选择器字符串，用于**过滤**出**被选中的元素中**能触发事件的**后代元素**。

  注：选择器是 **null 或者忽略了该选择器**，那么被选中的元素**总是能触发事件**

- data：当一个**事件被触发**时，要传递给事件处理函数的**event.data**

- handler(eventObject)：**事件被触发时，执行的函数**。

  注：若该函数只是执行**return false**，那么该参数位置可以直接**简写成 false**

##### B、实例

html部分

```html
<div class="box">
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
  </ul>
</div>
<input id="ipt" type="text"> <button id="btn">添加</button>
<div id="wrap">
</div>
```



Js 部分

- **场景一、点击li，wrap里展示li里内容**

```javascript
$('.box li').on('click', function(){
  var str = $(this).text()//所点击的元素的内容 即li元素里面的1,2,3,4
  $('#wrap').text(str)
})
// .on事件 其实类似于原生js 的addEventListener
```



也可以简写为事件后边直接回调

```javascript
$('.box>ul>li').click(function(){
  var str = $(this).text()
  $('#wrap').text(str)
})
```



如果需要**解绑对应的事件**，此时需要给事件加一个**命名空间**

```javascript
$('.box li').on('click.hello', function(){
    console.log(3)
  var str = $(this).text()
  $('#wrap').text(str)
})
//命名空间没什么特别的作用，只不过在解绑事件时便于区分绑定的事件
$('.box li').off('click.hello')
```



执行结果

![image.png](https://upload-images.jianshu.io/upload_images/14339384-88684406823d4687.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 上图我们可以发现，click.hello 解绑事件了，但是没有影响到click.world事件

**注：解绑事件只会解绑对应的事件，其他事件不受影响**



- 场景二、点击button ,把 input 的值变成 li 添加到ul

```javascript
  $('#btn').on('click', function(){
    var value = $('#ipt').val()
    $('.box>ul').append('<li>'+value+'</li>')
  })
```

![image.png](https://upload-images.jianshu.io/upload_images/14339384-40136199a7c14b9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



绑定事件只对页面已有元素的绑定，**新增的元素没有绑定事件，可以用事件代理**解决这个问题

```javascript
$('#btn').on('click', function(){
  var value = $('#ipt').val()
  $('.box>ul').append('<li>'+value+'</li>')
})//这里的 this 是你所点击的元素

$('.box ul').on('click', 'li', function(){
  var str = $(this).text()//这里的this也是代表所点击的元素li
  $('#wrap').text(str)
})
```

![image.png](https://upload-images.jianshu.io/upload_images/14339384-839dd3b257fedfbe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



- **场景三  绑定事件时，给回调函数传递数据**

```javascript
$('.box').on('click', {name: 'hunger'}, function(e){
    console.log(e.data)
})
```



![image.png](https://upload-images.jianshu.io/upload_images/14339384-25bbdc8b142ef135.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



(2)  .one( events [, selector ][, data ], handler(eventObject) )

同 on，绑定事件，但**只执行一次**



(3)  .off( events [, selector ][, handler ] )

移除(解绑)一个事件处理函数

```javascript
$('.box li').off('click')
```



(4)  .trigger( eventType [, extraParameters ] )

根据绑定到匹配元素的给定的事件类型执行所有的处理程序和行为

```javascript
$('.box li').on('click', function() {
  console.log($(this).text())
});
$('.box li').trigger('click')
```

其实就是**不需要手动操作**，代码自已去触发事件



(5)  其他常见事件

![image.png](https://upload-images.jianshu.io/upload_images/14339384-f70eee006f203447.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



# 二、动画

### A、常用动画

(1)  .hide([duration ][,easing ] [,complete ])

用于隐藏元素，没有参数的时候等同于直接设置 display 属性为 none

```javascript
$('.box').hide()
```

等同于

```javascript
$('.box').css('display','none')
```



(2)  .show( [duration ][, easing ] [, complete ] )

用于显示元素，用法和 hide 类似



(3)  .fadeIn( [duration ][, easing ] [, complete ] )

通过淡入的方式显示匹配元素，参数含义和上面相同

```javascript
$('#book').fadeIn('slow', function() {
// Animation complete
});
```



(4)  .fadeOut( [duration ][, easing ] [, complete ] )

通过淡出的方式隐藏匹配元素

```javascript
$('#book').fadeOut('slow', function() {
// Animation complete.
});
```



(5)  .slideDown( [duration ][, easing ] [, complete ] )

用滑动动画显示一个匹配元素，方法将给匹配元素的高度的动画，这会导致页面的下面部分滑下去，弥补了显示的方式

```javascript
$('#book').slideDown('slow', function() {
    // Animation complete.
});
```



(6)  .slideUp( [duration ][, easing ] [, complete ] )

用滑动动画隐藏一个匹配元素，方法将给匹配元素的高度的动画，这会导致页面的下面部分滑上去，当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局。 display 样式属性将被设置为none，以确保该元素不再影响页面布局。

```javascript
$('#book').slideUp('slow', function() {
    // Animation complete.
});
```



(7)  .slideToggle( [duration ][, easing ] [, complete ] )

用滑动动画**显示或隐藏**一个匹配元素，方法将给匹配元素的高度的动画，这会导致页面中，在这个元素下面的内容往下或往上滑。display属性值保存在jQuery的数据缓存中，所以display可以方便以后可以恢复到其初始值。

如果一个元素的display属性值为inline，然后是隐藏和显示，这个元素将再次显示inline。当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局。

```javascript
$('#clickme').click(function() {
 $('#book').slideToggle('slow', function() {
 // Animation complete.
 });
});
```

 

demo 地址参考   http://js.jirengu.com/sogiy/embed?html,console,output



### B、自定义动画

简单的动画不能满足需求时，jquery提供了自定义动画行为的方法

.animate( properties [, duration ][, easing ] [, complete ] )

可参考官网API https://api.jquery.com/animate/

**注：properties是一个CSS属性和值的对象,动画将根据这组对象移动**

```javascript
$('#clickme').click(function() {
  $('#book').animate({
    opacity: 0.25,
    left: '+=50',
    height: 'toggle'
  }, 5000, function() {
    // Animation complete.
  });
});
```

demo 地址参考  http://js.jirengu.com/viqiv/1/edit?html,css,output



### C、动画队列

##### (1)  写法方式

- **方式一：将动画连续的写就会形成一个动画队列，按顺序从上至下依次执行**

```javascript
$('#btn4').click(function(){
      $('.box').animate({
        left: '100px'
      }, 1000)  // 执行第一帧动画
      $('.box').animate({
        left: '100px',
        top: '100px'
      }, 1000) // 执行第二帧动画
      $('.box').animate({
        left: '0',
        top: '100px'
      }, 1000) // 执行第三帧动画
      $('.box').animate({
        left: '0',
        top: '0'
      }, 1000) // 执行第四帧动画
    })
```



- **方式二：将后续动画写入第一个动画的回调函数里**

```javascript
$box.hide(1000, function(){
   $box.show(1000, function(){
     $box.fadeOut('slow',function(){
       $box.fadeIn('slow',function(){
         $box.slideUp(function(){
           $box.slideDown(function(){
             console.log('动画执行完毕')
           })
         })
       })
     })
   })
})
//等价于
$box.hide(1000)
    .show(1000)
    .fadeOut()
    .fadeIn()
    .slideUp()
    .slideDown(function(){
      console.log('真的完毕了')
    })
```



**特别注意：**队列运行在元素上**异步地**调用动作序列的。例如下面代码，执行顺序是 **马上显示字符showla**，再执行**show动画**

```javascript
$('#btn-box1').on('click',function(){
    $('.box').show(400) // 第二次执行
    console.log('showla') // 第一次执行
})
```

可以把**显示showla 代码**放到show动画回调函数里

```javascript
$('#btn-box1').on('click',function(){
    $('.box').show(400,function(){ // 第一次执行
        console.log('showla') // 第二次执行
    })  
})
```



(2)  清除和停止

- .clearQueue

清除动画队列中未执行的动画



-  .finish

**停止当前动画**，并清除动画队列中所有未完成的动画,最终**展示动画队列最后一帧的最终状态**



-  .stop( [clearQueue ][, jumpToEnd ] )

stop()：停止当前正在运行的动画 ，立刻去执行后面的动画

.stop(true, false) ：停止当前动画，并清除未执行的动画队列

.stop(true, true)：停止当前动画，并清除未执行的动画队列，并且当前动画展示最终状态

clearQueue(default: false)

jumpToEnd(default: false)



demo 地址参考 http://js.jirengu.com/viqiv/1/edit?html,css,output