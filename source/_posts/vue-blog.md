---
title: vue-blog
date: 2019-03-05 16:15:03
tags:
---

## Vue.js之多人共享博客



**预览地址：**https://lovexwu.github.io/vue-blogclient/#/



### 项目功能

一、前、后端分离的**多个页面**的**单页**应用

二、页面包括 首页、博客详情、创建、编辑、用户、我的、登录、注册 8个页面

 **A、首页：** 展示所有人设置到首页的博客列表
 **B、博客详情：**展示博客详情
 **C、登录、注册：** 用户登录注册
 **D、用户页面：** 展示某个用户的所有博客列表
 **E、我的：** 展示个人主页
 **F、编辑、删除、创建博客**

注：

**1､详情页面**的博客内容是用 **markdown 写 , html 方式 做一个展现**

2､ **创建页面 + 编辑页面 **可以设置是否显示到首页（atIndex），如不设置，那首页就不会显示其内容



### Get 到的点

一、**上传dist 文件内容 GitHub 四步曲**   (考虑上传整个项目文件太大，可以上传编译后的dist文件内容即可)

1､ GitHub 新建远程库

2､ 终端 cd 到 项目文件夹 并 执行 npm run build 进行编译
![image.png](https://upload-images.jianshu.io/upload_images/14339384-1c7b52aca910751d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



3､编译完后，dist 文件夹下 会有新的东西啦

![image.png](https://upload-images.jianshu.io/upload_images/14339384-9c1e49e63379181e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4、终端切换到dist下，推送到 GitHub 上就行啦



#### 工程化上面四步曲

1､加上这一连串代码在package.json里

![image.png](https://upload-images.jianshu.io/upload_images/14339384-27b4a5b06088e1f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



分析： git push -f origin master  其中/f 是因为上传的不是源码，会覆盖也是应该的, 切记上传源码是不用 /f 

![image-20190306122914148](/Users/laoda/Library/Application Support/typora-user-images/image-20190306122914148.png)



2､终端就可以直接操作 npm run upload

![image.png](https://upload-images.jianshu.io/upload_images/14339384-0d2ee3934dcd056a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/14339384-f991ecf697e35a3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

也就是说，下次修改没问题，执行 npm run upload 就会依次执行那些命令操作啦



### 遇到的坑

1､ Github pages预览，GitHub不支持http协议，将接口 **http 改为 https** 即可

2、assetsPublicPath **‘/'改为‘./'** 即可![image.png](https://upload-images.jianshu.io/upload_images/14339384-2247ad058106ad3b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



Vue项目上传github在线预览 参考
https://zhuanlan.zhihu.com/p/48631279
https://www.jb51.net/article/142307.htm
https://zhuanlan.zhihu.com/p/35764920



### 技术栈

vue-cli、vue2､axios、vue-router、vuex、es6､npm、elementUI