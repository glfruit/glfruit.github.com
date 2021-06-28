---
layout: post
title: IntelliJ Idea中开发Grails应用的几个问题
date: 2013-11-20 10:56
description: "描述了使用IntelliJ IDEA进行Grails的开发时遇到的几个问题及其解决方法"
categories: 技术研究
tags: [Grails, IntelliJ]
---

原来系统里安装的是IntelliJ IDEA 12和[Grails](http://grails.org) 2.2.4，开发、调试运行没有任何问题，最近[Grails](http://grails.org) 2.3.2发布了，IntelliJ IDEA 13的Beta版本也出来了，于是将两者都升级到了相应的最新版本，经过几天的使用后发现了两个问题：

1. 在IDEA里以调试模式启动Grails应用后所设置的断点不起作用，程序运行到设置了断点的地方不会中断，而是继续执行
2. 在IDEA里点击停止按钮停掉后重新启动Grails应用，会报Address already in use的错误，用ps -ef | grep java查看，发现原来启动的Tomcat其实并没有被终止，而是仍然在运行

我开始怀疑是由于安装了两个版本的IDEA，导致它们的配置冲突引起上述问题，于是将两个版本全部卸载掉，重新安装了IntelliJ IDEA 12，发现问题依旧，于是上网搜索了一下，找到了答案，原来上述两个问题都是由于[Grails](http://grails.org)的2.3版本引入了fork模式导致的，简单的说，当用2.3版本的Grails新建一个项目之后，在BuildConfig.groovy中有如下配置：

{% codeblock lang:groovy %}
grails.project.fork = [
    // configure settings for compilation JVM, note that if you alter the Groovy version forked compilation is required
    //  compile: [maxMemory: 256, minMemory: 64, debug: false, maxPerm: 256, daemon:true],

    // configure settings for the test-app JVM, uses the daemon by default
    test: [maxMemory: 768, minMemory: 64, debug: false, maxPerm: 256, daemon:true],
    // configure settings for the run-app JVM
    run: [maxMemory: 768, minMemory: 64, debug: false, maxPerm: 256, forkReserve:false],
    // configure settings for the run-war JVM
    war: [maxMemory: 768, minMemory: 64, debug: false, maxPerm: 256, forkReserve:false],
    // configure settings for the Console UI JVM
    console: [maxMemory: 768, minMemory: 64, debug: false, maxPerm: 256]
]
{% endcodeblock %}

为了解决我碰到的两个问题，需要将这一行

{% codeblock lang:groovy %}
run: [maxMemory: 768, minMemory: 64, debug: false, maxPerm: 256, forkReserve:false],
{% endcodeblock %}
注释掉。根据我的理解，也就是运行Grails应用时仍然在当前的JVM中运行，而不是fork出一个JVM来运行，这样第二个问题得到解决，要解决第一个问题，还要在为运行Grails应用的命令行加入-debug选项，如下图所示：
![命令行配置]({{site.url}}/images/intellij-debug.jpg)
经过这些调整后上述两个问题都得到了解决。

参考资料

1. [IntelliJ Idea 13 EAP and Grails 2.3.0](http://vasya10.wordpress.com/2013/09/29/intellij-idea-13-eap-and-grails-2-3-0/)
2. [Grails 2.3 breakpoints](http://devnet.jetbrains.com/message/5498220;jsessionid=637BBFE806169DA22453426D2C92E6E7#5498220)
