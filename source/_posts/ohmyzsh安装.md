---
title: ohmyzsh
date: 2018-12-24 12:09:44
tags:
---

### 一、终端输入命令，安装 oh-my-zsh

```java
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

执行过程中会要求输入用户密码（过程中密码并不会显示，输入完成后直接敲回车就可以）
安装成功之后，终端显示如下：

![image.png](https://upload-images.jianshu.io/upload_images/14339384-20500f47d3a7e5cc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



终端的上面就已经显示，已经从默认的 bash 切换到了 zsh 。
如果不想用了可以随时直接切换回原本的 bash ，输入命令：

```javascript
chsh -s /bin/bash
```

同理，切换回zsh，只要把 bash 改成 zsh 执行命令即可



### 二、安装前/后

安装前：

![image.png](https://upload-images.jianshu.io/upload_images/14339384-27932858a7085ad2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

安装后：

![image.png](https://upload-images.jianshu.io/upload_images/14339384-bf302f4f731dade2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





参考 https://www.jianshu.com/p/300827734b69