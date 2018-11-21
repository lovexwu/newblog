---
title: git命令讲解
date: 2018-11-21 18:28:37
tags:
---

### 起步

初次使用需要设置姓名和邮箱

```javascript
git config --global user.name "你的姓名"
git config --global user.email 邮箱地址（如123@163.com）
```

### clone项目

用于把一个GitHub上的项目clone（下载）到本地，变为本地仓库

```javascript
git clone git@github.com:jirengu/blog.git
cd blog
```

### 添加文件并提交

```javascript
#创建文件
touch a.md

#在文件里写入一个字符串
echo "hello" > a.md
git status 

#在当前目录下的新增和修改的文件添加到暂存区
git add .
git status

#把暂存区的更新提交到本地库
git commit -am "add file"
git status
```

![添加文件并提交.jpg](https://upload-images.jianshu.io/upload_images/14339384-c4671d1fd1420b30.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

