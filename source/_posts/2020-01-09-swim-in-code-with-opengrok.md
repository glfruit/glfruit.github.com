---
title: 代码畅游必备工具-在Debian上安装配置OpenGrok 
date: 2020-01-09 20:54:29
categories: 技术研究
---
最近打算好好研究一下微软给出的微服务架构示例项目[eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers)，需要一个方便的源代码浏览工具，自然而言地想到了用[OpenGrok](https://oracle.github.io/opengrok/)来进行。原来安装配置过，但是没有做记录，这么久了也忘记怎么做了，又从头折腾了一遍，为了备忘，将安装配置的过程记录下来。

##  基本环境
- Debian 10.1.0(buster)
- JDK 11
- Tomcat 9
- [universal-ctags](https://github.com/universal-ctags)

<!-- more -->

##  安装步骤
1. 安装JDK 11 


```bash
sudo apt install openjdk-11-jdk
```
2. 安装Tomcat 9

```bash
sudo apt install tomcat9
```
3. 安装universal-ctags

```bash
sudo apt install universal-ctags
```
4. 在OpenGrok的[下载页面](https://github.com/oracle/opengrok/releases)下载最新版本（目前是1.3.6）

```bash
wget https://github.com/oracle/opengrok/releases/download/1.3.6/opengrok-1.3.6.tar.gz
```
5. 将下载的文件解压至*/opt/opengrok*目录
6. 将*source.war*部署志Tomcat

```bash
sudo cp /opt/opengrok/lib/source.war /var/lib/tomcat9/webapps
```
7. 源码目录和索引目录默认存放在/var/opengrok下，新建下列文件夹

```bash
mkdir -p /var/opengrok/data
mkdir -p /var/opengrok/src
mkdir -p /var/opengrok/etc
```
8. 将想阅读的源代码放在*src*目录下，例如eShopOnContainers

```bash
cd /var/opengrok/src
git clone https://github.com/dotnet-architecture/eShopOnContainers.git
```
9. 配置默认日志配置

```bash
sudo cp /opt/opengrok/doc/logging.properties /var/opengrok/logging.properties
```
10. 生成源代码的索引

```bash
java -Djava.util.logging.config.file=/var/opengrok/logging.properties \
  -jar /opt/opengrok/lib/opengrok.jar \
  -c /usr/bin/ctags-universal \
  -s /var/opengrok/src -d /var/opengrok/data -H -P -S -G \
  -W /var/opengrok/etc/configuration.xml -U http://localhost:8080
```
11. 访问**http://localhost:8080/source**，即可看到源代码
![](https://raw.githubusercontent.com/glfruit/pic_bed/master/20200109205025.png)

## 参考资料
1. [OpenGrok安装和配置](http://panqiincs.me/2018/12/31/how-to-setup-opengrok/)
2. [SEVERE: Couldn't notify the webapp on https://.... HTTP 401 Unauthorized #2635](https://github.com/oracle/opengrok/issues/2635)
3. [Installing opengrok in linux · GitHub](https://gist.github.com/vineelkovvuri/a6ca0def344e04b8293d)

