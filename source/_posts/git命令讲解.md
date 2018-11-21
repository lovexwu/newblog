---
title: git命令讲解
date: 2018-10-02 18:28:37
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
```

![添加文件并提交1.jpg](https://upload-images.jianshu.io/upload_images/14339384-81b25ac7b0cd1e77.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



```javascript
#在当前目录下的新增和修改的文件添加到暂存区
git add .
git status
```

![添加文件并提交2.jpg](https://upload-images.jianshu.io/upload_images/14339384-1252dd98333c031a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



```javascript
#把暂存区的更新提交到本地库
git commit -am "add file"
git status
```

![添加文件并提交3.jpg](https://upload-images.jianshu.io/upload_images/14339384-8d7658adef991691.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



```javascript
#把当前本地库里的改动推送到远程库（origin) 的master分支
git push origin master //如果之前提交过，以后只需要git push即可
```

![添加文件并提交4.jpg](https://upload-images.jianshu.io/upload_images/14339384-ceb545cf25896176.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### 修改删除文件

```javascript
#把远程仓库的变动更新合并到本地仓库
git pull
//如果远程仓库有修改，切记一定要git pull，这样子远程的修改才可以更新到本地仓库,不然会报错！

#修改文件
vim a.md
git add .

// 这里需注意：
// 如果提交消息包含大量字符串，提交参数不用加m
// 此时会进入vim 界面，按下i 进入编辑状态，进行编辑
// 编辑完成后按下esc 进入命令状态，输入 :wq 保存退出 vim

git commit -a
git push origin master

rm -rf a.md
git add .
```



### 本地创建一个git项目推送到远程空仓库

```javascript
mkdir newProject
cd newProject

# 把一个文件夹初始化成一个本地 git仓库
# 注意 仓库和文件夹的区别在于仓库下有一个隐藏的.git文件夹，里面有一些信息
# 对于一个仓库，删除.git 文件夹，就变成一个普通的文件夹了

//如何把本地空文件夹变成仓库呢？我们用git init 初始化
git init //初始化，把本地的空文件夹变成仓库，才执行，
#注意别克隆一个项目，再用git init，因为克隆的项目里，本身是一个仓库，它已经有了.git,
#完全不需要你去操作，如果再去执行.git init的话，会把它的.git全给覆盖掉，把以前仓库的记录的信息全给抹掉 

touch index.html
echo "hello" > index.html

git add .
git commit -am "init"

# 查看本地库里记录的远程库地址
git remote -v

# 这里把远程库的地址添加个标签origin
git remote add origin git@github.com:jirengu/blog2.git

# 推送到远程库地址
git push origin master

# 慎用，这样会强制推送，会覆盖别人的代码
git push -f origin master

# 在添加一个远程库的标签
git remote add gitlab git@gitlab.com:abc/blog.git

# 推送到gitlab标签的地址上
git push gitlab master

# 删除gitlab 标签
git remote remove gitlab

# 修改origin标签对应的地址
git remote set-url origin git@github.com:jirengu/blog3.git

# 把gitlab标签改名为coding
git remote rename gitlab coding

```



### 分支操作(很重要的一部分)

```javascript
# 创建本地库dev 分支
git branch dev

# 切换到dev 分支
git checkout dev

touch b.md
git add .
git commit -am "add b.md"

# 推送到origin 地址的 dev 分支上
git push origin dev 

```



### 分支合并

```javascript
git checkout master

# 把dev 分支上的内容合并到当前分支（master）上
git merge dev
```



### 冲突

###### 当自已和别人改同一个文件的同一个地方，在执行<u>git pull</u> 时更新本地合并时会出现冲突

1､ 修改冲突文件

2､ 重新提交