title: "Hexo简介"
date: 2015-03-31 08:57:47
tags: []
categories: 数字生活
---


话说最近我终于提起精神看了一眼许久没有打理的博客，除了篇数少得可怜之外，时间也还停留在2013年，实在有点惭愧，于是振作精神，决定还是要继续将博客坚持下去。我原来是基于Jekyll Bootstrap + GitHub Pages搭建的，感觉也还不错，但是Jekyll Bootstrap现在已经停止开发了，在它的开发页面上推荐使用ruhoh，搜索了一下，很多都吐槽说文章多了生成速度慢，于是也放弃了。最后看到了一个推荐得比较多的hexo，觉得还不错，是用NodeJS开发的，而自己对NodeJS也比较有兴趣，于是开始动手将博客从Jekyll迁移到Hexo，以下步骤均在Mac Os Mavericks和[Homebrew](http://brew.sh)环境下完成。

## 准备工作
如果原来使用过其它的工具来使用Git Pages进行博客写作的话需要进行一下备份的工作，避免出现数据丢失的现象：
<!-- more -->
### 备份
1. 将原来的博客git仓库备份
2. 将GitHub上原来的博客git仓库删除掉（当然也可以不删，和新创建的博客git仓库进行合并就可以了，但是会发生很多冲突，太麻烦，还不如直接删掉重建来得方便）
3. 在GitHub上新建git仓库USERNAME.github.com

### 安装配置基本运行环境
1. 安装Git
{% codeblock bash %}
brew install git
{% endcodeblock %}

2. 安装NodeJS
{% codeblock bash %}
brew install node
{% endcodeblock %}

3. 安装Hexo
{% codeblock bash %}
npm install -g hexo
{% endcodeblock %}

## 基本配置
### 创建博客
{% codeblock bash %}
;; 创建博客并进入该目录
hexo init myblog && cd myblog
{% endcodeblock %}

### 基本站点信息配置
打开根目录下的_config.yml文件，根据自己的情况更改相应的信息，主要是下面几项：
{% codeblock yml %}
title: 你的博客站点名称
subtitle: 子标题
description: 博客站点的描述
author: 作者名字
email: 联系email
language: zh-CN # 语言选项，我当然设置为中国了
{% endcodeblock %}

### 主题配置
在Hexo的项目主页上提供了许多主题，默认的是landscape主题，但是一看到上面大大的一幅图片我就觉得堵得慌，我还是比较喜欢自己原来Jekyll Bootstrap提供的那种清爽、简洁的主题风格，可惜找了一圈都没找到，暂时先用了一个iOS7的主题，回头深入研究一下，自己改造一个吧。
1. 安装主题
{% codeblock bash %}
git clone https://github.com/tracy-e/hexo-theme-iOS7.git themes/iOS7
{% endcodeblock %}

2. 配置主题
打开themes/iOS7下的_config.yml文件，进行如下修改：
- 菜单名称。将menu下的英文菜单名称修改为中文
- Widget。我将默认添加的weibo去掉了，因为我试了一下，觉得挂在默认的位置实在不怎么样，而暂时也不太想费太多时间去调整
- 更改weibo下的配置。
{% codeblock yml %}
Weibo:
name: 你的名字 # 一定要配置，否则每篇文章下默认添加的”Posted by xxx”就变成”Posted by null”了
uid: ## 微博的用户ID？不怎么明白，空着也没事
link: ## 你的微博链接地址
{% endcodeblock %}

### 自定义域名
在Jekyll中直接在根目录下创建一个CNAME文件即可，而在Hexo中必须将该文件放在source目录中


## 基本用法
### 创建项目
{% codeblock bash %}
hexo init
{% endcodeblock %}

### 创建页面
{% codeblock bash %}
hexo new post “post name”
hexo new draft “draft name”
{% endcodeblock %}

### 部署
这里和Jekyll不一样，我最开始想当然的直接将整个git仓库push到远端，结果当然是什么都没有，后来才发现是要在_config.yml中配置deploy选项，然后运行hexo deploy即可。

## 从Jekyll到Hexo的转换
### 文件名格式
在_config.yml中更改new_post_name选项

### 语法高亮
从{% raw %}{% highlight groovy %}{% endraw %}切换为{% raw %}{% codeblock lang:groovy %}{% endraw %}

## 参考资料
1. [Hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)
2. [Hexo官方文档](http://hexo.io/docs/index.html)
3. [Setting up a custom domain with GitHub Pages](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages)
4. [My custom domain isn’t working](https://help.github.com/articles/my-custom-domain-isn-t-working)
5. [Hello Hexo](http://snger.github.io/2013/12/31/hello-hexo/)
