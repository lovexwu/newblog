---
title: Grid
date: 2019-02-08 22:27:57
tags:
---

## 一、场景

1､ 一个容器设置了 **display: grid**属性，就把容器元素定义了一个网格

2､ 设置列/行的大小：**grid-template-columns / grid-template-rows**

3､使用**grid-column**和 **grid-row**把它的子元素放入网格



## 二、重要术语

#### 1､Grid Container（父容器）

设置了 **display: grid** 的元素， 这是所有 grid item 的**直接父项**。 下面的.container 就是 grid container

```html
<div class="container">
  <div class="item item-1"></div>
  <div class="item item-2"></div>
  <div class="item item-3"></div>
</div>
```



#### 2､Grid Item（Grid 容器的孩子）

即**直接子元素**，下面的 .item 元素就是 grid item，但 **.sub-item不是**

```html
<div class="container">
  <div class="item"></div> 
  <div class="item">
    <p class="sub-item"></p>
  </div>
  <div class="item"></div>
</div>
```



#### 3､Grid Line（分界线）

这个分界线组成网格结构。 它们既可以是**垂直的（“column grid lines”）**，也可以是**水平的（“row grid lines”）**，并位于行或列的任一侧。 下面的黄线就是一个列网格线。

![image.png](https://upload-images.jianshu.io/upload_images/14339384-efd9b54927a4b259.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



#### 4､Grid Track（两个相邻网格线之间的空间）

可以把它们想象成网格的列或行。 下面是第二行和第三行网格线之间的网格轨道

![image.png](https://upload-images.jianshu.io/upload_images/14339384-727620e3957041c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



#### 5､Grid Cell（两个相邻的行和两个相邻的列网格线之间的空间）

它是网格的一个“单元”。 下面是行网格线1和2之间以及列网格线2和3的网格单元

![image.png](https://upload-images.jianshu.io/upload_images/14339384-c95a216ad75a3b67.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



#### 6､Grid Area（四个网格线包围的总空间）

网格区域可以由任意数量的网格单元组成。 下面是行网格线1和3以及列网格线1和3之间的网格区域

![image.png](https://upload-images.jianshu.io/upload_images/14339384-06841c75d365ba46.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



## 三、Grid Container 的部分属性

#### 1､ display

##### 1.1 作用

将元素定义为 grid contaienr，并为其内容建立新的网格格式化上下文(grid formatting context)



##### 1.2 用法

```css
.container {
  display: grid | inline-grid | subgrid;
}
```

a). grid ——— 生成一个块级(block-level)网格
b). inline-grid ——— 生成一个行级(inline-level)网格
c). subgrid ——— 如果你的 grid container 本身就是一个 grid item（即,嵌套网格），可以使用这个属性来表示你想从它的父节点获取它的行/列的大小，而不是指定它自己的大小

**注：column, float, clear, 以及 vertical-align 对一个 grid container 没有影响**



#### 2､ grid-template

##### 2.1 作用

在单个声明中定义 grid-template-rows、grid-template-columns、grid-template-areas 的简写



##### 2.2 实例

```css
.container {
  grid-template:
    [row1-start] "header header header" 25px [row1-end]
    [row2-start] "footer footer footer" 25px [row2-end]
    / auto 50px auto;
}
```

等价于

```css
.container {
  grid-template-rows: [row1-start] 25px [row1-end row2-start] 25px [row2-end];
  grid-template-columns: auto 50px auto;
  grid-template-areas: 
    "header header header" 
    "footer footer footer";
}
```



#### 3､grid-gap

##### 3.1 作用

grid-row-gap 和 grid-column-gap 的缩写



##### 3.2 用法

```css
.container {
  grid-gap: <grid-row-gap> <grid-column-gap>;
}
```



##### 3.3 实例

```css
.container {
  grid-template-columns: 100px 50px 100px;
  grid-template-rows: 80px auto 80px; 
  grid-gap: 10px 15px;
}
```



#### 4､justify-items

##### 4.1 作用

a). 沿着行轴对齐网格内的内容（与之对应的是 align-items, 即沿着列轴对齐）

b). 该值适用于容器内的所有的 grid items



##### 4.2 用法

```css
.container {
  justify-items: start | end | center | stretch;
}
```

a). start ——— 内容与网格区域的左端对齐

![image.png](https://upload-images.jianshu.io/upload_images/14339384-ed82572142db676d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



b). end ——— 内容与网格区域的右端对齐

![image.png](https://upload-images.jianshu.io/upload_images/14339384-8765e1169356dece.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



c). center ——— 内容位于网格区域的中间位置

![image.png](https://upload-images.jianshu.io/upload_images/14339384-7174643083a92570.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



d). stretch ——— 内容宽度占据整个网格区域空间(这是默认值)

![image.png](https://upload-images.jianshu.io/upload_images/14339384-98aeed32990c2a4d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



#### 5､align-items

##### 5.1 作用

a). 沿着列轴对齐grid item 里的内容（与之对应的是使用 justify-items 设置沿着行轴对齐）

b). 该值适用于容器内的所有 grid item



##### 5.2 用法

```css
.container {
  align-items: start | end | center | stretch;
}
```

a). start ——— 内容与网格区域的左端对齐

![image.png](https://upload-images.jianshu.io/upload_images/14339384-b16d1fa66a315d0f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



b). end ——— 内容与网格区域的底部对齐

![image.png](https://upload-images.jianshu.io/upload_images/14339384-cc8d01542c71e44c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



c). center ——— 内容位于网格区域的垂直中心位置

![image.png](https://upload-images.jianshu.io/upload_images/14339384-2a681576266a5680.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



d). stretch ——— 内容高度占据整个网格区域空间(这是默认值)

![image.png](https://upload-images.jianshu.io/upload_images/14339384-bfce968a5623f44d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





## 四、Grid Items 的部分属性

#### 1､grid-column-start / grid-column-end / grid-row-start /grid-row-end

##### 1.1 作用

a). 使用特定的网格线确定 grid item 在网格内的位置。

b). grid-column-start/grid-row-start 属性表示grid item的网格线的起始位置

c). grid-column-end/grid-row-end属性表示网格项的网格线的终止位置



##### 1.2 用法

```css
.item {
  grid-column-start: <number> | <name> | span <number> | span <name> | auto
  grid-column-end: <number> | <name> | span <number> | span <name> | auto
  grid-row-start: <number> | <name> | span <number> | span <name> | auto
  grid-row-end: <number> | <name> | span <number> | span <name> | auto
}
```

a). <line> ——— 可以是一个数字来指代相应编号的网格线，也可使用名称指代相应命名的网格线
b). span <number> ——— 网格项将跨越指定数量的网格轨道
c). span <name> ——— 网格项将跨越一些轨道，直到碰到指定命名的网格线
d). auto ——— 自动布局， 或者自动跨越， 或者跨越一个默认的轨道



##### 1.3 实例

实例一

```css
.item-a {
  grid-column-start: 2;
  grid-column-end: five;
  grid-row-start: row1-start
  grid-row-end: 3
}
```

![image.png](https://upload-images.jianshu.io/upload_images/14339384-78e4a28bc0773421.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



实例二

```css
.item-b {
  grid-column-start: 1;
  grid-column-end: span col4-start;
  grid-row-start: 2
  grid-row-end: span 2
}
```

![image.png](https://upload-images.jianshu.io/upload_images/14339384-b3731a1a1fe1576f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**特别注意：** 

1)､如果没有声明 grid-column-end / grid-row-end，**默认情况下，该网格项将跨越1个轨道**

2)､网格项可以相互重叠。 您可以**使用z-index来控制它们的堆叠顺序**



#### 2､grid-column / grid-row

##### 2.1 作用

grid-column-start + grid-column-end, 和 grid-row-start + grid-row-end 的简写形式



##### 2.2 用法

```css
.item {
  grid-column: <start-line> / <end-line> | <start-line> / span <value>;
  grid-row: <start-line> / <end-line> | <start-line> / span <value>;
}
```



##### 2.3 实例

```css
.item-c {
  grid-column: 3 / span 2;
  grid-row: third-line / 4;
}
```

![image.png](https://upload-images.jianshu.io/upload_images/14339384-026a9f40f77462f6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**特别注意：如果没有指定结束行值，则该网格项默认跨越1个轨道**



#### 3､grid-area

##### 3.1 作用

a). 给 grid item 进行命名以便于使用 grid-template-areas 属性创建模板时来进行引用。

b). 可以做为 grid-row-start + grid-column-start + grid-row-end + grid-column-end 的简写形式



##### 3.2 用法

```css
.item {
  grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>;
}
```

a). <name> - 你的命名
b). <row-start> / <column-start> / <row-end> / <column-end> - 可以是数字，也可以是网格线的名字



##### 3.3 实例 

```css
.item-d {
  grid-area: header
}/*给一个网格项命名*/
```

作为 grid-row-start + grid-column-start + grid-row-end + grid-column-end 的简写:

```css
.item-d {
  grid-area: 1 / col4-start / last-line / 6
}
```

![image.png](https://upload-images.jianshu.io/upload_images/14339384-2ff00b0b270e7a4e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



#### 参考 

http://chris.house/blog/a-complete-guide-css-grid-layout/