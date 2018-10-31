---
title: Git-使用方法
date: 2018-10-05 17:13:09
tags:
---

首先我们打开mac终端输入
![1.png](https://upload-images.jianshu.io/upload_images/14260087-7ae4d51cbdd5ba28.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果终端告诉你
![2.png](https://upload-images.jianshu.io/upload_images/14260087-16999227ad4fc005.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

那么说明你已经有git了，不需下载安装

#本地仓库创建
![3.png](https://upload-images.jianshu.io/upload_images/14339384-fb2d559ba2b3d088.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


再输入命令
![4.png](https://upload-images.jianshu.io/upload_images/14260087-02bb43d7f21a3ccd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样子 ，本地仓库就建好了

#创建远程仓库
首页登陆Github，并选择创建
![5.png](https://upload-images.jianshu.io/upload_images/14260087-e90d9b087fce4015.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

填写仓库名称，这里注意仓库名称不要写中文，中文显示不出来
![6.jpg](https://upload-images.jianshu.io/upload_images/14339384-2f8260b4006c805a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样远程仓库也创建好了

#将本地仓库与远程仓库进行关联 
在终端中输入
![7.png](https://upload-images.jianshu.io/upload_images/14260087-c93fc4f2200df010.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
git remote add origin后的网址是你的远程仓库的地址，如下图
![8.jpg](https://upload-images.jianshu.io/upload_images/14339384-6e1a5c5e8128f6b8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


OK现在已经关联成功了

#克隆地址
终端输入
![9.png](https://upload-images.jianshu.io/upload_images/14260087-725d2a374013e595.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样子git 可以正常使用了

#常用命令行如下
git status     查看本地git仓库的状态
git add -A    添加所有修改的内容
git commit -m "提交详情内容记录"      提交更新到本地仓库
git push -u origin master    将本地仓库更新的内容提交到远程仓库
git diff   查看修改的内容
git log   查看历史版本，显示从最近到最远的提交日志


