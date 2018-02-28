---
title: 使用Hexo创建博客站点
tags:
  - Hexo
categories: IT生活
date: 2018-02-22 07:10:28
---


[Hexo](https://hexo.io)是一个老牌的博客写作与管理工具，我从[Jekyll](https://github.com/mojombo/jekyll)迁移到[Hexo](https://hexo.io)也有五六年的时间了，虽然博客没写几篇（写作也是个体力活啊），但是断断续续也在维护，只是开始用[Hexo](https://hexo.io)时还是2.x的版本，后来升级到3.x版本，使用过程中始终有些小问题，而且因为我有多台电脑，如何在多台电脑之间维护管理博客也是一个问题，一直没有认真去解决，这次趁着春节放假，离上班还有几天时间，就把整个博客仓库清理了一遍，把遗留的问题也都解决了，把整个过程记录下来，以做备忘。
<!-- more -->

## 基本安装和配置
### hexo的安装和配置
[Hexo](https://hexo.io)自身的安装其实很简单，一行命令就完成了：
`````
npm install -g hexo-cli
`````
但是在运行这行命令之前还必须安装[Hexo](https://hexo.io)所依赖的两个工具：
[Node.js](https://nodejs.org)
[Git](https://git-scm.com)
这些工具以及[Hexo](https://hexo.io)的基本安装在H[官方文档](https://hexo.io/zh-tw/docs/)里已经说得很详细了，这里也就不再赘述了。

### 创建博客站点
#### 创建Git仓库
其实这一步不是必须的，但是出于备份（谁也不想自己辛辛苦苦写的东西一夜之间就没了）和同步（需要在多台电脑写作和同步博客内容及配置的话，这种情况现在并不少见）的考虑，我们最好还是使用版本控制工具将所写的内容和[Hexo](https://hexo.io)的配置管理起来。由于一般使用[Hexo](https://hexo.io)的话都会将博客部署到[GitHub Pages](https://pages.github.com/)，所以我们这里选择使用[GitHub](https://github.com)来托管我们的博客内容。
首先要在[GitHub](https://github.com)上创建一个xxx.github.io的仓库（这里xxx为你的GitHub用户名，如果没有GitHub账户的话就自己注册一个）；
然后在本地检出这个仓库：
`````
git clone https://github.com/xxx/xxx.github.io
cd xxx.github.io
`````
现在这还是一个空仓库，通过运行
`````
git branch
`````
可以看到现在只有一个master分支，我们不对这个分支进行任何修改，而是新创建一个分支，例如叫做hexo：
`````
git checkout -b hexo
`````
这样就创建并切换到了新的hexo分支，我们的站点配置管理和博客写作都将在这个分支上进行。博客目录下会有一个隐藏的叫做.git的文件夹，我们先将其移动到其它地方。

#### 初始化
进入博客目录，并使用Hexo进行初始化：
`````
cd xxx.github.io
hexo init
hexo install
`````

#### 基本配置
打开_config.yml文件，根据自己的情况修改以下几项：
`````
title: A Blog # 博客站点的名称
subtitle: Blog Subtitle # 博客站点的副标题
description:
author: Somebody # 作者名称
language: zh-CN # 站点语言
timezone: Asia/Shanghai # 时区
`````
运行
`````
hexo server
`````
使用浏览器访问 http://localhost:4000 应该就能看到博客的首页了。

### 主题的安装和配置
选择一个自己喜欢的主题，我选择的主题是[next](https://theme-next.org/)，下面以这个主题为例来描述如何安装和配置主题。
首先将前面移走的.git目录移回博客目录下，这样博客目录里面的内容才会被Git管理起来；
然后访问选定主题的GitHub页面，将其fork到自己的账户下；
第三步将主题的git仓库fork到自己的账户下：
`````
git submodule add https://github.com/theme-next/hexo-theme-next.git
`````
打开博客目录下的_config.yml文件，修改下面一行：
`````
theme: my-next
`````

【注】: 关于如何Fork以及同步Fork，请参考[Fork A Repo](https://help.github.com/articles/fork-a-repo/)

### 部署到GitPages
用 [Hexo](https://hexo.io)创建的博客可以有多种部署方式，最常见的就是部署到GitPages，免费又好用。要部署到GitPages，我们需要完成以下几个步骤：
1. 在source目录下创建一个名为CNAME的文件，在里面加入自己注册好的域名，例如example.domain，然后通过 [DNSPod](https://www.dnsprod.cn)之类的DNS解析服务商将域名解析道对应的GitPages地址。
2. 安装git部署器，以便部署到github
```
npm install hexo-deployer-git --save
```
3. 将博客部署到GitPages:
```
hexo deploy
```

### 电脑之间的同步
如果新电脑上还没有检出博客，则先执行检出操作并切换到hexo分支并进行更新：
```
git checkout https://www.github.com/xxx/xxx.github.io
git fetch
git checkout hexo
git submodule update --init
npm install --save
npm install hexo-deployer-git --save
```

如果已经检出了博客，则直接运行更新命令即可：
```
git submodule update
git pull
```


## 参考资料
1. [Github pages + hexo博客搭建教程](https://segmentfault.com/a/1190000011535121)
2. [How to setup a hexo-based blog: Part 2](http://fenglu.me/2016/08/12/How-to-setup-a-hexo-based-blog-Part-2/)
3. [打造个性超赞博客Hexo+NexT+GithubPages的超深度优化](https://reuixiy.github.io/technology/computer/computer-aided-art/2017/06/09/hexo-next-optimization.html)
4. [Using a custom domain with GitHub Pages](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)