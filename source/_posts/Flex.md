---
title: Flex
date: 2019-02-05 20:25:04
tags:
---

## 一、场景

一个容器设置了 **display: flex**；属性就定义了一个**flex容器**，它的直接子元素会接受这个flex环境



## 二、属性

#### 1､flex-direction


设置或检索伸缩盒对象的子元素在父容器中的位置

.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
row 默认值，水平从左到右
row-reverse 水平从右到左
column 垂直从上到下
column-reverse 垂直从下到上



#### 2､flex-wrap

设置或检索弹性盒模型对象的子元素超出父容器时是否换行

默认所有的flex item会尝试放在一行中，可以通过设置flex-wrap设置新行的方向

.container{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
nowrap 默认值，不换行
wrap 换行
wrap-reverse 换行，并且颠倒行顺序



#### 3､flex-flow

flex-direction 和 flex-wrap 的缩写，默认值row nowrap

flex-flow: <‘flex-direction’> || <‘flex-wrap’>
设置或检索弹性盒子元素在主轴（横轴）方向上的对齐方式，当弹性盒里一行上的所有子元素都不能伸缩或已经达到其最大值时，这一属性可协助对多余的空间进行分配。当元素溢出某行时，这一属性同样会在对齐上进行控制

.container {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
flex-start 默认值、弹性盒子元素将向行起始位置对齐

flex-end 弹性盒子元素将向行结束位置对齐

center弹性盒子元素将向行中间位置对齐。该行的子元素将相互对齐并在行中居中对齐

space-between 弹性盒子元素会平均地分布在行里

space-around 弹性盒子元素会平均地分布在行里，两端保留子元素与子元素之间间距大小的一半



#### 4､align-items

设置或检索弹性盒子元素在侧轴（纵轴）方向上的对齐方式

.container {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
flex-start 弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。

flex-end 弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。

center 弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。

baseline 如弹性盒子元素的行内轴与侧轴为同一条，则该值与flex-start等效。其它情况下，该值将参与基线对齐。

stretch 如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。



#### 5､align-content

设置或检索弹性盒堆叠伸缩行的对齐方式

.container {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
flex-start 各行向弹性盒容器的起始位置堆叠。弹性盒容器中第一行的侧轴起始边界紧靠住该弹性盒容器的侧轴起始边界，之后的每一行都紧靠住前面一行。

flex-end 各行向弹性盒容器的结束位置堆叠。弹性盒容器中最后一行的侧轴起结束界紧靠住该弹性盒容器的侧轴结束边界，之后的每一行都紧靠住前面一行。

center 各行向弹性盒容器的中间位置堆叠。各行两两紧靠住同时在弹性盒容器中居中对齐，保持弹性盒容器的侧轴起始内容边界和第一行之间的距离与该容器的侧轴结束内容边界与第最后一行之间的距离相等。

space-between 各行在弹性盒容器中平均分布。第一行的侧轴起始边界紧靠住弹性盒容器的侧轴起始内容边界，最后一行的侧轴结束边界紧靠住弹性盒容器的侧轴结束内容边界，剩余的行则按一定方式在弹性盒窗口中排列，以保持两两之间的空间相等。

space-around 各行在弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半。各行会按一定方式在弹性盒容器中排列，以保持两两之间的空间相等，同时第一行前面及最后一行后面的空间是其他空间的一半。

stretch 各行将会伸展以占用剩余的空间。剩余空间被所有行平分，以扩大它们的侧轴尺寸。

然后是用在子元素上的属性



#### 6､order

在默认情况下flex order会按照书写顺训呈现，可以通过order属性改变，数值小的在前面，还可以是负数

.item {
  order: <integer>;
}



#### 8､flex-shrink

设置或检索弹性盒的收缩比率,根据弹性盒子元素所设置的收缩因子作为比率来收缩空间

.item {
  flex-shrink: <number>; /* default 1 */
}







#### 10､flex

flex-grow, flex-shrink,flex-basis 的缩写

.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}



#### 11､align-self

设置或检索弹性盒子元素在侧轴（纵轴）方向上的对齐方式，可以覆盖父容器align-items的设置

.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}



## 三、实例

#### 1､flex-basis 

用于设置子项的占用空间。如果设置了值，则子项占用的空间为设置的值；如果没设置或者为 auto，那子项的空间为width/height 的值

![image.png](https://upload-images.jianshu.io/upload_images/14339384-69b33e699be54f66.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

解析：

(1)、对于子项1，flex-basis 如果设置默认是auto，子项占用的宽度使用width 的宽度，width没设置也为 auto，所以子项占用空间由内容决定

(2)、对于子项2，flex-basis 为auto，子项占用宽度使用width 的宽度，width 为70px，所以子项子项占用空间是70px

(3)、对于子项3，flex-basis 为100px，覆盖width 的宽度，所以子项占用空间是100px

demo地址 http://js.jirengu.com/weqoc/5/edit?html,output

#### 2､flex-grow

用来“瓜分”父项的“剩余空间”

![image.png](https://upload-images.jianshu.io/upload_images/14339384-dab53ba492f1746a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

解析：

(1)、容器的宽度为400px, 子项1的占用的基础空间(flex-basis)为50px，子项2占用的基础空间是70px，子项3占用基础空间是100px，剩余空间为 400-50-70-100 = 180px

(2)、其中子项1的flex-grow: 0(未设置默认为0)， 子项2flex-grow: 2，子项3flex-grow: 1，剩余空间分成3份，子项2占2份(120px)，子项3占1份(60px)。

(3)、所以 子项1真实的占用空间为: 50+0 = 50px， 子项2真实的占用空间为: 70+120 = 190px， 子项3真实的占用空间为: 100+60 = 160px

demo地址：http://js.jirengu.com/sivoy/1/edit?html,css,js,output

#### 3､flex-shrink

用来“吸收”超出的空间

![image.png](https://upload-images.jianshu.io/upload_images/14339384-0a39a2d1f2659645.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

解析：

(1)、容器的宽度为400px, 子项1的占用的基准空间(flex-basis)为250px，子项2占用的基准空间是150px，子项3占用基准空间是100px，总基准空间为 250+150+100=500px。

(2)、容器放不下，多出来的空间需要被每个子项根据自己设置的flex-shrink 进行吸收。 子项1的flex-shrink: 1(未设置默认为1)， 子项2 flex-shrink: 2，子项3 flex-shrink: 2

子项1需要吸收的的空间为 `(250*1)/(250*1+150*2+100*2) * 100 = 33.33px`，子项1真实的空间为 250-33.33 = 216.67px。同理子项2吸收的空间为`(150*2)/(250*1+150*2+100*2) * 100=40px`，子项2真实空间为 `150-40 = 110px`。子项3吸收的空间为`(100*2)/(250*1+150*2+100*2) * 100 = 26.67px`，真实的空间为`100-26.67=73.33px`

demo地址：http://jsbin.com/pozebetibu/edit?html,output



#### 参考

[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
[demo代码](http://js.jirengu.com/jur/2)

