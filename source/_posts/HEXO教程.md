---
title: HEXO教程
date: 2018-11-03 16:18:30
tags:
---

#### 注意：如果你使用的是 Windows 系统，Hexo 很容易安装不成功

如果不成功，二选一：

1. 你就放弃 Hexo，使用简书、知乎、segmentfault、掘金等工具写博客。
2. 你就放弃 Windows，改用 Linux，[教程](https://xiedaimala.com/tasks/11ad5683-7e18-4883-879d-8425e6a6ceb7)

#### 使用 Hexo + GitHub 可以轻松搞出一个好看的博客

##### 以下是步骤

1. 进入一个安全的目录，比如 `cd ~/Desktop` 或者 `cd ~/Documents`，别在根目录 / 瞎搞。以后所有的教程第一步都是「进入一个安全的目录，别在根目录瞎搞」，只有 ~ 里面的目录是你能碰的！

2. 在 GitHub 上新建一个空 repo，repo 名称是「你的用户名.github.io」（注意个用户名是你的GitHub用户名，不是你的电脑用户名）

3. `npm install -g hexo-cli`，安装 Hexo

4. `hexo init myBlog`

5. `cd myBlog`

6. `npm i`

7. `hexo new 开博大吉`  你会看到一个md文件的路径

   ![img.jpg](https://upload-images.jianshu.io/upload_images/9375265-f4bc8c7d1bb875b7.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   Windows 的路径中的 \ 需要变成 / 才行哦

8. `start xxxxxxxxxxxxxxxxxxx.md`，编辑这个 md 文件，内容自己想（Ubuntu 系统用 `xdg-open xxxxxxxxxxxxxxxxxxx.md` 命令）

9. `start _config.yml`，编辑网站配置

   - 把第 6 行的 title 改成你想要的名字

   - 把第 9 行的 author 改成你的大名

   - 把最后一行的 type 改成 `type: git`

   - 在最后一行后面新增一行，左边与 type 平齐，加上一行 `repo: 仓库地址` （请将仓库地址改为「你的用户名.github.io」对应的仓库地址，仓库地址以 [git@github.com](mailto:git@github.com): 开头你知道吧？不知道？不知道的话现在你知道了）

   - 第 4 步的 repo: 后面有个空格，不要眼瞎。

10. `npm install hexo-deployer-git --save`，安装 git 部署插件

11. `hexo deploy`

12. 进入「你的用户名.github.io」对应的 repo，打开 GitHub Pages 功能，如果已经打开了，你应该会看到一个预览链接

13. 用浏览器访问「预览链接/index.html」就应该看到了你的博客！（GitHub Pages 存在延迟，如果没看到，过三分钟再刷新看看）

##### 第二篇博客

1. `hexo new 第二篇博客`
2. 复制显示的路径，使用 `start 路径` 来编辑它
3. `hexo generate`
4. `hexo deploy`

##### 换主题

1. <https://github.com/hexojs/hexo/wiki/Themes> 上面有主题合集
2. 随便找一个主题，进入主题的 GitHub 首页，比如我找的是 <https://github.com/iissnan/hexo-theme-next>
3. 复制它的 SSH 地址或 HTTPS 地址，假设地址为 [git@github.com](mailto:git@github.com):iissnan/hexo-theme-next.git
4. `cd themes`
5. `git clone git@github.com:iissnan/hexo-theme-next.git`
6. `cd ..`
7. 将 _config.yml 的第 75 行改为 `theme: hexo-theme-next`，保存
8. `hexo generate`
9. `hexo deploy`
10. 等一分钟，然后刷新你的博客页面，你会看到一个新的外观。如果不喜欢这个主题，就回到第 1 步，重选一个主题。

##### 上传源代码

注意「你的用户名.github.io」上保存的只是你的博客，并没有保存「生成博客的程序代码」，你需要再创建一个名为 blog-generator 的空仓库，用来保存 myBlog 里面的「生成博客的程序代码」。

1. 在 GitHub 创建 blog-generator 空仓库

   ![res.jpg](https://upload-images.jianshu.io/upload_images/9375265-41320af865b4e459.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  2.按照截图中的命令执行即可，记住，别用 HTTPS 地址。

这样一来，你的博客发布在了「你的用户名.github.io」而你的「生成博客的程序代码」发布在了 blog-generator。所有数据万无一失，你就不会因为误删 myBlog 目录而痛哭了。

以后每次 hexo deploy 完之后，博客就会更新；然后你还要要 add / commit /push 一下「生成博客的程序代码」，以防万一。

这个 blog-generator 就是用来生成博客的程序，而「你的用户名.github.io」仓库就是你的博客页面。