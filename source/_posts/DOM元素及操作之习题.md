---
layout: dom
title: DOM元素及操作之习题
date: 2019-01-02 16:50:00
tags:
---

1､要求：当鼠标放置在`li`元素上，会在`img-preview`里展示当前`li`元素的`data-img`对应的图片。

```
<ul class="ct">
    <li data-img="1.png">鼠标放置查看图片1</li>
    <li data-img="2.png">鼠标放置查看图片2</li>
    <li data-img="3.png">鼠标放置查看图片3</li>
</ul>
<div class="img-preview"></div>
<script>
//你的代码
</script>
```

预览地址：
<http://js.jirengu.com/tefom/5/edit?html,output>

2､要求：

- 当点击按钮`开头添加时`在`<li>这里是</li>`元素前添加一个新元素，内容为用户输入的非空字符串；当点击`结尾添加`时在最后一个 li 元素后添加用户输入的非空字符串.

- 当点击每一个元素 li时，控制台展示该元素的文本内容。

  ```html
  <ul class="ct">
    <li>这里是</li>
    <li>饥人谷</li>
    <li>任务班</li>
  </ul>
  <input class="ipt-add-content" placeholder="添加内容"/>
  <button id="btn-add-start">开头添加</button>
  <button id="btn-add-end">结尾添加</button>
  <script>
  //你的代码
  </script>
  ```

预览地址：<http://js.jirengu.com/qonup/1/edit?html,output>



3､要求当点击每一个元素`li`时控制台展示该元素的文本内容。不考虑兼容。

```html
<ul class="ct">
    <li>这里是</li>
    <li>饥人谷</li>
    <li>前端14班</li>
</ul>
<script>
//todo ...
</script>
```

预览地址：http://js.jirengu.com/wabub/1/edit?html,console,output>



4､解释DOM2事件传播机制。

1、DOM2的事件传播包含三个阶段:
捕捉阶段（capturing），事件从顶级文档树节点一级一级向下遍历，直到到达该事件的目标节点。
到达事件的目标节点，执行目标节点的时间处理程序。
事件起泡（bubbling），事件从目标节点一级一级向上上溯，直到顶级文档树节点。

2、相应的，2级DOM通过下面的两个函数给节点对象添加和删除事件处理函数。
addEventListener(eventType, handler, propagate);
removeEventListener(eventType, handler, propagate);

三个参数意思分别如下:
eventType: 即事件类型（不加on）。比如："click"。
handler: 事件处理函数。传入参数即为事件对象event。
propagate: 是否只执行捕获和目标节点两个阶段。true的话，只执行1，2两个阶段；false的话，只指向2，3两个阶段。

3、IE的事件传播只包含上边的2和3两个阶段
相应的，IE通过下面两个函数给节点对象添加和删除事件处理函数。
attachEvent(eventType, handler);
detachEvent(eventType, handler);
参数意思同2级DOM对应的函数参数



5､`onlick`与`addEventListener`的区别

1、onclick 只能绑定一个事件，绑定多个会产生覆盖；不能设置参数，使用默认的事件冒泡阶段。

2、addEventListener中有第3个参数，attachEvent没有。第3个参数传递的是false或true。这个参数可选，默认是false。
false--表示事件处理将在冒泡阶段执行。
true--表示事件处理将在捕获阶段执行。

3、理论上，Event Listeners (addEventListener、attachEvent（IE使用 ）)可以无限增加事件监听给某个一元素。实际应用的约束就是客户端内存的限制，这一点因每个浏览器而异。

参考链接：<https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener>



6､实现[此效果](http://js.jirengu.com/nupom)。

预览地址：
<http://js.jirengu.com/cidag/13/edit>



7､如何获取 DOM 计算后的样式？

使用getComputedStyle获取元素计算后的样式，不要通过 node.style.属性 获取

```javascript
var node = document.querySelector('p')
var color = window.getComputedStyle(node).color
console.log(color)
```



8､写一个函数，批量操作 css。

```javascript
function css(node, styleObj){
//todo ..
}
css(document.body, {
  'color': 'red',
  'background-color': '#ccc'
})
```

预览地址：
<http://js.jirengu.com/nixac/2/edit?html,js>



9､列出DOM 元素选取的 API。

getElementById() //获取id
getElementsByClassName() //获取class类名
getElementsByTagName() //获取标签名
getElementsByName() //获取有name属性的html元素
querySelector() //选择器
querySelectorAll() //选择所有选择器



10､如何创建元素？如何添加元素？

创建元素：
createElement() //元素节点
createTextNode() //文本节点
createDocumentFragment()

添加元素:
appendChild() //添加元素
insertBefore() //某个元素之前插入元素
replaceChild() //要插入的元素和要替换的元素