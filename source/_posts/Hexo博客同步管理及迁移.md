---
title: Hexo博客同步管理及迁移 #文章標題
date: 2018-06-30 11:47:44 #文章生成時間
categories: "Technology" #文章分類目錄 可以省略
tags: #文章標籤 可以省略
     - Technology
---
一台电脑上已有一个在用的博客，又新用了一台电脑，实现原电脑和新电脑都可以提交更新博客，实现同步或者说博客的版本管理。本文参考了知乎中的高票答案,把过程重新梳理了一遍，并在一些关键的地方做了更详细的阐述，自认为更好理解一点。
用分支的思路，一个分支用来存放Hexo生成的网站原始的文件，另一个分支用来存放生成的静态网页。
![](https://i.loli.net/2018/06/30/5b36efe300dff.png)

步骤：
1.在原电脑上操作，给 username.github.io 博客仓库创建hexo分支，并设为默认分支。
2.如果未给你的 github 账号添加过当前电脑生成的 ssh key，需要创建 ssh key 并添加到 github 账号上。（如何创建和添加 github help 就有）
3.随便一个目录下，命令执行 git clone git@github.com:username/username.github.io.git 把仓库 clone 到本地。
4.显示所有隐藏文件和文件夹，进入刚才 clone 到本地的仓库，删掉除了 .git 文件夹以外的所有内容。
5.命令行 cd 到 clone 的仓库，git add -A ，git commit -m "--"，git push origin hexo，把刚才删除操作引起的本地仓库变化更新到远程，此时刷新下 github 端博客hexo分支，应该已经被清空了。
6.将上述 .git 文件夹复制到本机本地博客根目录下（即含有 themes、source 等文件夹的那个目录），现在可以把上述 clone 的本地仓库删掉了，因为它已经没有用了，本机博客目录已经变成可以和 hexo 分支相连的仓库了。
7.将博客目录下 themes 文件夹下每个主题文件夹里面的 .git .gitignore 删掉。
8.cd 到博客目录，git add -A ，git commit -m "--"，git push origin hexo，将博客目录下所有文件更新到 hexo 分支。如果上一步没有删掉 .git .gitignore，主题文件夹下内容将传不上去。至此原电脑上的操作结束。
9.cd 到博客目录，npm install、hexo g && hexo s，安装依赖，生成和启动博客服务。正常的话，浏览器打开 localhost:4000 可以看到博客了。至此新电脑操作完毕。

以后无论在哪台电脑上，更新以及提交博客，依次执行，git pull，git add -A ，git commit -m "--"，git push origin hexo，hexo clean && hexo g && hexo d 即可。