---
title: Git命令使用
date: 2018-10-06 17:59:22
tags:
---

大家在使用git提交代码的过程中，难免会因为各种原因执行一些错误的commit / push，想要修复这些错误，reset和revert就能很好的帮到我们。

首先我们到区分几个概念，工作区，暂存区，版本库。

**工作区**
所谓工作区，即我们电脑中所看到的目录。

**版本库**
在工作区有一个隐藏目录.git，这是Git的版本库。

**暂存区**
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD

#小小实例了解下

![1.jpg](https://upload-images.jianshu.io/upload_images/14339384-b42621a6dd3db2d3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**开始做几次提交**
![2.jpg](https://upload-images.jianshu.io/upload_images/14339384-8d7e52440fcb334f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**看下提交log**
![3.jpg](https://upload-images.jianshu.io/upload_images/14339384-e4d7a68891094b51.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**当前提交的readme**
![4.jpg](https://upload-images.jianshu.io/upload_images/14339384-25e76b753234941f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**一种方式，soft模式**
![6.jpg](https://upload-images.jianshu.io/upload_images/14339384-6419fb2ce901c22a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
采用这种模式，git不回清除你的stage区，因此，git status时就显示了stage区相对于second commit的变化。此时工作区是clean 的，而stage区则有变化

**另一种方式，hard模式**
![7.jpg](https://upload-images.jianshu.io/upload_images/14339384-4ad49e7c87bc5a24.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
采用这种模式，git回用first commit 的内容覆盖stage区和工作区，因此所有的内容都回到了first commit的状态。
#区别（重点）

**reset**
是起到了撤销commit的作用，但实质上它是将HEAD的指向移动了位置
![12.png](https://upload-images.jianshu.io/upload_images/14339384-efe2bb12e2043bb6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**revert**
是一次新的commit，HEAD会继续向前执行
![13.png](https://upload-images.jianshu.io/upload_images/14339384-d66f6700cbe7a215.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)