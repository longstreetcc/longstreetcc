---
layout: post
title: 搭建github+jekyll博客的教程
description: 如何使用Github Page搭建简易博客
category: tech
---

<!-- ######2015-04-20-搭建github+jekyll博客的教程.md -->

前段时间在看技术博客，知道了github可以免费搭建博客，而近期github的接入速度也很快，就一时兴起，根据[一个大牛的搭建教程][1]和[一个详细教程][2]搭建了本博客。

## 建博客一步就可以完成

申请了github账号之后，fork下这个[jekyll-now][3]项目，然后进入settings，将Repository name修改为xxx.github.io，其中xxx为**你guthub的用户名**，请千万记住，不要改成其他的。哥就是在这里卡住了，卡了一天，导致别人10分钟的教程我花了一整天才弄好，最后没法，看了github的官方帮助手册[Using Jekyll with Pages][4]才恍然大悟。最后在网址打开xxx.github.io就可以看到你的博客了。

**逗比的注意事项**  
你完全可以只看[jekyll-now][3]这个项目下面的README就可以了。不过该jekyll-now已经新增了很多功能，而我只想要个简单的能在本地测试，能在github上面运行就行的版本就好，不要太多模板。而这个版本要在本地运行需要装太多环境，实在太麻烦了。所以我搭建了很简单的版本。

## 我的博客搭建过程

  1. 搭建本地环境 
    需要安装本地运行环境。
    
        gem sources --remove https://rubygems.org/
        gem sources -a https://ruby.taobao.org/
        gem sources -l  
        gem install jekyll

  2. 创建博客 

        mkdir -p ~/Blog && cd ~/Blog
        jekyll new .
        cd ~/Blog
        jekyll serve

    本地简易版博客已搭建好。通过浏览器访问 http://localhost:4000/

  3. 修改成个人配置
    
    根目录下面的_config.yml的配置设置好个人信息。

  4. 写博客
    
    通过本地简易版博客看到，文章都存储在_posts文件夹。拷贝2014-3-3-Hello-World.markdown文件，修改名字为你写博客的日期和博文名。文章使用markdown语法写的，该语法很简单，自学很容易。

  5. 部署博客到github
    
    整个博客在github来看就是个开源项目。所有文件都通过git操作文件来完成。本地写完博客然后git到你的github上，就可以在网页显示了。
    
      * 首先在git上创建项目，命名为xxx.github.io，xxx为你的github用户名</p> 
      * 部署项目
        
            git init
            git add .
            git commit -m "init"
            git remote add origin <你的git项目>
            git push -u origin master

 [1]: http://cenalulu.github.io/jekyll/how-to-build-a-blog-using-jekyll-markdown/
 [2]: http://www.smashingmagazine.com/2014/08/01/build-blog-jekyll-github-pages/
 [3]: https://github.com/barryclark/jekyll-now
 [4]: https://help.github.com/articles/using-jekyll-with-pages/