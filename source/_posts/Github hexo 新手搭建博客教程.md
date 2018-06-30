---
title: Github hexo 新手搭建博客教程 #文章標題
date: 2018-06-24 23:47:44 #文章生成時間
categories: "Technology" #文章分類目錄 可以省略
tags: #文章標籤 可以省略
     - Technology
---
免费方便，不用花一分钱就可以搭建一个自由的个人博客，不需要服务器不需要后台。 可以随意绑定自己的域名，多种多样的模板可供选择，也可以自己定制开发自己喜欢的模板。
那么，让咱们开始吧！
<h3>一、准备工作</h3>
 - 下载Git            [官网下载](https://git-scm.com/)
 - 下载Node.js    [官网下载](https://nodejs.org/en/)
 - 注册Github   [Gtihub.com](https://github.com/)
 - 域名注册（可选）       [阿里云](https://wanwang.aliyun.com/?spm=5176.8006371.388261.603.25b37e63Z4rrJ5) 
 - 文本编辑器  （Notopad++，Sublime，Atom ...）

----------


<h3>二、安装注册</h3>

**1.安装Git**
双击安装程序，默认安装就可以。
**2.安装Nodejs**
双击安装程序，默认安装就可以。
查看安装结果与版本
```
node -v #查看安装版本
npm -v #查看npm安装版本
```

 **3.建立博客目录**
  新建博客文件目录，比如D:\blog\hexo ，右键该目录，点击Git Bash Here，启动Git
  
 **4.安装Hexo** 

Hexo安装命令： npm install -g hexo 

```ruby
npm install -g hexo
```
 <h5>注册Github</h5>
 
 **5.建立仓库** 
 注册完成之后， 新建一个名为 你的用户名.github.io的仓库，比如说，如果你的github用户名是xxx，那么你就新建xxx.github.io的仓库（必须是你的用户名，其它名称无效），将来你的网站访问地址就是 http://xxx.github.io 
 <!--more-->
 


----------


<h3>三、配置</h3>
**1.Hexo介绍**
 
 Hexo是一个简单、快速、强大的基于 Github Pages 的博客发布工具，支持Markdown格式，有众多优秀插件和主题。

&emsp;官网： http://hexo.io
&emsp;Github: https://github.com/hexojs/hexo

由于github pages存放的都是静态文件，博客存放的不只是文章内容，还有文章列表、分类、标签、翻页等动态内容，假如每次写完一篇文章都要手动更新博文目录和相关链接信息，相信谁都会疯掉，所以hexo所做的就是将这些md文件都放在本地，每次写完文章后调用写好的命令来批量完成相关页面的生成，然后再将有改动的页面提交到github。

注意事项：

 - 很多命令既可以用Windows的cmd来完成，也可以使用git bash来完成，但是部分命令会有一些问题，为避免不必要的问题，建议全部使用git bash来执行；
 - hexo不同版本差别比较大，网上很多文章的配置信息都是基于2.x的，所以注意不要被误导；
 - hexo有2种_config.yml文件，一个是根目录下的全局的_config.yml，一个是各个theme下的； 

**2.npm镜像**
npm太慢， 淘宝npm镜像使用方法

淘宝 npm 地址： http://npm.taobao.org/

如何使用 
有很多方法来配置npm的registry地址，下面根据不同情境列出几种比较常用的方法。以淘宝npm镜像举例：

临时使用
```
npm --registry https://registry.npm.taobao.org install express
```
持久使用
```
npm config set registry https://registry.npm.taobao.org
```
配置后可通过下面方式来验证是否成功 
```
npm config get registry
```
或   npm info express

**3.Hexo初始化**

初始化hexo模板,初始化之后，生成一些文件。
初始化之前，新建一个空文件夹，因为非空不允许初始化，比如d:\blog\hexo  ，
进入该目录： cd /d/blog/hexo  输入命令
```
hexo init
```
本地查看效果，执行下面语句，
```
hexo generate   #生成
hexo server     #本地预览
hexo g -s       #合并使用，简写
```
执行完即可登录查看效果: http://localhost:4000/

**4.安装hexo部署到git page的deployer**
```
npm install hexo-deployer-git --save
```
至此，hexo本地安装完成，下面是一些hexo简单编辑方法。

**5.Hexo文章编辑**

文章编辑有两种方式，一种是通过命令来创建新文章
一种是创建MD格式的文件，编辑完成之后把.md 文件放到博客目录：...\source\_posts  ，网上推荐Markdown编辑器，但是收费，可以选择其他的编辑器
也有很多在线编辑器，比如CSDN创作中心等等
文章中插入图片令人比较不方便，一般是选择将图片上传到图片网站，比如图床，七牛等等，之后再把图片地址复制到编辑器中。

**7.修改主题**

比如安装主题hexo-theme-yilia
先下载这个主题，在博客目录下
**安装**
```
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
```
**配置**
修改hexo目录的_config.yml中的   theme: landscape   改为    theme: yilia
**更新**
```
cd themes/yilia
git pull
```

然后重新执行hexo g来重新生成。
hexo s 本地预览


----------
<h3>四、hexo发布到Github</h3>

**1._config.yml配置文件修改**

hexo 3.0 部署类型不再是github，_config.yml 中修改为下面这个格式:   (xxx为Github用户名)
```
deploy:
  type: git
  repository: git@xxx.github.com:xxx/xxx.github.io.git
  branch: master
```

**2.配置SSH key**

为什么要配置这个呢？因为你提交代码肯定要拥有你的github权限才可以，但是直接使用用户名和密码太不安全了，所以我们使用ssh key来解决本地和服务器的连接问题。邮件地址为注册Github的邮箱
```
 ssh-keygen -t rsa -C "邮件地址"
```
然后连续3次回车，最终会生成一个文件在用户目录下，打开用户目录，找到.ssh\id_rsa.pub文件，记事本打开并复制里面的内容，打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key：
![](https://i.loli.net/2018/06/26/5b31f502434b1.png)
将刚复制的内容粘贴到key那里，title随便填，保存。

**3.SSH用户配置：**
```
git config --global user.name "xxx"  //你的github用户名，非昵称
git config --global user.email "xxx@qq.com" //填写你的github注册邮箱
```
Github博客绑定自己的域名，在Setting 中填写自己的域名信息
![](https://i.loli.net/2018/06/26/5b320d469b1c3.png)

**4.域名解析设置**

以阿里云的为例：
![](https://i.loli.net/2018/06/26/5b31f6fdcf4f1.png)
IP地址，ping 你的GitHub博客地址就知道了，比如：ping  xxx.github.io 
![ping.png](https://i.loli.net/2018/06/26/5b31f91e95579.png)

**5.将博客部署到Github Page上**
```
hexo  g  -d
```
通过在浏览器中输入自己的域名来访问GitHub Pages博客。


----------
参考资料：
[浅析 Hexo 搭建博客的原理](https://juejin.im/post/598eeaff5188257d592e55bb)
[Hexo Docs](http://www.ituring.com.cn/article/199295)
[Hexo主题制作指南](http://www.360doc.com/content/16/0913/16/33651124_590545274.shtml#/)
[写一个自己的Hexo主题](https://segmentfault.com/a/1190000006057336)