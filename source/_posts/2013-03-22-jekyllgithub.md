---
layout: post
title: "基于GitHub Pages搭建个人博客（一）"
date: 2013-03-22
description: ""
categories: IT生活
tags: [jekyll, jekyllbootstrap, github]
---

我其实不是一个博客系统的重度用户，写博客的频率并不高，在先先后后注册的若干个博客里面都躺着我开个了头然后就没有了结尾的帖子。但是，我也确实越来越觉得坚持写博客是一件好事，
是一个忠实记录自己的心路历程的过程，也是让自己飘忽的思想能够有一个落脚点的地方，于是又兴起了开一个新博客的念头，原打算花点钱买个wordpress空间折腾一下，念及自己去年
的失败经历，花了钱却总共没写到十篇博客，今年也不敢保证，所以虽然钱不多却也不想浪费了，还是决定找个免费空间来用，但是这个免费空间一定要稳定、可靠。转了一圈也没发现满意
的，正准备放弃时，看到了基于[GitHub](http://www.github.com)和[Jekyll](https://github.com/mojombo/jekyll)搭建博客的文章，正好满足自己的需求，经过一番折腾，算是将基本框架
搭建起来了，下面就是我的折腾日记，也算作开篇吧。

整个折腾过程大致可以分为以下几个部分：

* 搭建基本环境
* 绑定域名
* 使用reStructuredText

本篇博客主要讲的就是基本环境的搭建，不过需要说明的是，因为我使用的是Mac OS的系统，所以全部的步骤都是按Mac OS的情况来进行的。

1. 基本运行环境

   由于GitHub Pages事实上是用Jekyll来生成的静态页面，所以我们在写博客时要遵守其规则，而为了测试是否确实符合，我们需要在自己的机器上按照Jekyll，而Jekyll实际上使用[Ruby](http://www.ruby-lang.org/zh_cn/)
   写的一个工具，因此还需要[Ruby](http://www.ruby-lang.org/zh_cn/)运行环境;又由于事实上整个博客就是一个[Git](http://git-scm.com)仓库，所以还需要安装[Git](http://git-scm.com)。
   如果安装了[Homebrew](https://github.com/mxcl/homebrew)的话就很好办了：

       $ brew install ruby

       $ sudo gem install jekyll

       $ brew install git

2. 注册[GitHub](http://www.github.com)账号
   
   前往[GitHub](http://www.github.com)，用自己喜欢的用户名注册一个账号，要注意的是，如果打算绑定到自己的域名上，那么注册的用户名要和打算绑定的域名一致才行。这步很简单，
   只要看得懂基本的英文就没问题了。

3. 安装Jekyll-Bootstrap

       $ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com

       $ cd USERNAME.github.com

       $ git remote set-url origin git@github.com:USERNAME/USERNAME.github.com.git

       $ git push origin master

    这里的USERNAME就是你在[GitHub](http://www.github.com)上所注册的用户名。这一步其实不是必需的，你完全可以按照[这里](http://net.tutsplus.com/tutorials/other/building
    -static-sites-with-jekyll)的说明从零开始，但是使用Jekyll-Bootstrap的话可以让你的博客有一个不错的初始模板，再在这个基础上根据自己的需要进行修改就方便多了。完成之后，
    最多等个10分钟左右，访问USERNAME.github.com，应该就可以看到搭建好的博客首页了。


参考文档

* [Building Static Sites with Jekyll](http://net.tutsplus.com/tutorials/other/building-static-sites-with-jekyll/)
* [使用Github Pages建独立博客](http://beiyuu.com/github-pages/)
* [Jekyll-Bootstrap](http://jekyllbootstrap.com/)
