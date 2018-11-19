---
title: onclick与addEventListener区别
date: 2018-11-14 15:04:18
tags:
---

addEventListener和onclick有什么不一样？于是Google查了下，稍微整理了下：

-  onclick 只能绑定一个事件，绑定多个会产生覆盖；不能设置参数，使用默认的事件冒泡阶段。

- addEventListener中有第3个参数，attachEvent没有。第3个参数传递的是false或true。这个参数可选，默认是false。
   false--表示事件处理将在冒泡阶段执行。
   true--表示事件处理将在捕获阶段执行。

- 理论上，Event Listeners (addEventListener、attachEvent（IE使用 ）)可以无限增加事件监听给某个一元素。实际应用的约束就是客户端内存的限制，这一点因每个浏览器而异。

**onclick** 属性返回当前元素的 `click` 事件处理器代码

语法

```javascript
element.onclick = functionRef;
```

*functionRef* 是一个函数：通常是在别处声明的函数名或者是一个函数表达式（*function expression*）

**来个实例：**

```javascript
<ul id = "list">
 <li id = "add_event">white</li>
 <li id = "on_click">black</li>
</ul>

<script>
var on_click = document.getElementById('on_click');
on_click.onclick = function(){
    alert('我是click1');
}
on_click.onclick = function(){
    alert('我是click2');
} 
</script>
```

**运行结果：**

可想而知，只会弹出一个弹出框(我是 click2)，虽然绑定了两次

一个click处理器在同一时间只能指向唯一的对象。因此就算对于一个对象绑定了多次，但是仍然只会出现最后的一次绑定

**addEventListener绑定click事件**

```javascript
currentTarget.addEventListener(type,listener,option)
```

**来个实例：**

```javascript
<ul id = "list">
 <li id = "add_event">white</li>
 <li id = "on_click">black</li>
</ul>

<script>
var addEvent = document.getElementById('add_event');
addEvent.onclick = function(){
    alert('我是addEvent1');
}
addEvent.onclick = function(){
    alert('我是addEvent2');
} 
</script>
```

**运行结果：**

两次绑定的事件，都能够成功运行，也就是前后弹出'我是addEvent1' '我是addEvent2'

**由此可见，对于一个可以绑定的事件对象，想多次绑定事件都能运行，选用addEventListener**

通过addEventListener添加的事件必须通过相对应的为removeListener注销事件。但是如果像上面的用匿名函数的方式注册的事件，不能使用removeListener注销，因为没用对应事件的引用。

所以注册事件如果需要取消，最好使用一个引用，即:

```
var eventName = function () {
    //something
}
```

也正是这种方式，对于一个对象多次绑定同样的eventName，那么不会重复执行，只会执行一次。对于上面的匿名函数，就算内容一样，也会依次执行，**因为并不能算是相同事件处理器**。

里面的this引用，不是window对象，而是触发事件的元素的引用。

对于IE9之前，相对应的是attachEvent和detachEvent



**最后总结：**

1. onclick事件在同一时间只能指向唯一对象

2. addEventListener给一个事件注册多个listener

3. addEventListener对任何DOM都是有效的，而onclick仅限于HTML

4. addEventListener可以控制listener的触发阶段，（捕获/冒泡）。对于多个相同的事件处理器，不会重复触发，不需要手动使用removeEventListener清除

5. IE9使用attachEvent和detachEvent



可参考: https://developer.mozilla.org/zh-CN/docs/Web/API/GlobalEventHandlers/onclick

​             https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener

