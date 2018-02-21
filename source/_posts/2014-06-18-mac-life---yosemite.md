title: 'Mac生活（一）—— Yosemite的召唤'
categories:
- Mac生活
tags:
- Mac
date: 2014-06-18 16:51:12
---

本月的3号，苹果的WWDC 2014开始了，当时我还苦逼地在火车上摇啊摇，用时断时续的3G信号马马虎虎地了解了新发布的Yosemite的新特性之后心中一阵激动。等到好不容易终于摇到家里，顾不上休息，打开电脑就开始升级，一切顺利，除了在最后显示1 minute remaining那里实际停留了一个多小时之外，重启，顺利进入新系统。哇，界面给人的感觉还是很舒服的，哇，居然有毛玻璃效果了，哇......等等，怎么bartender弹出对话框说，对不起，它歇菜了，因为调用了私有的API，在Yosemite中挂掉了；启动CleanMyMac 2，这货吭都没吭，直接崩溃了；打开iBooks，点击搜索，崩溃了......虽然有这样那样的问题，但是Yosemite和iOS 8的整合还是让我舍不得放弃，还是继续坚持使用，倒也没什么其它大问题，直到第二天我到了办公室很愉快地打开电脑准备工作的时候悲剧了：系统启动到登录界面之后，苹果那可爱的彩球就一直飘啊飘，在google上翻了一阵也没见有什么有用的信息，只好又重新装回Mavericks，用的覆盖安装的方式，结果各种小问题，比Yosemite还不稳定，只好将盘格掉全新安装。然后几天后，在[v2ex](http://www.v2ex.com)上看到了解决登录界面卡住问题的[帖子](http://www.v2ex.com/t/116066)，真是欲哭无泪啊，怎么不早点贴出来呢......
<!-- more -->
今天一大早睁眼一看，iOS 8 Beta 2和Yosemite的DP2都出来了，iOS 8 Beta 2增加了来电归属地的功能，忍受不住诱惑，又将最新的iOS 8和Yosemite下载下来进行更新，貌似比上一个版本稳定多了，而且一些原来不兼容的软件也及时推出了更新的版本，但是当我很手贱地打开Trim Enabler并重启之后又悲剧了，这次连登录界面都没看到，直接卡在白色背景的启动界面上了，好在有了上一次的经验，也没太慌张，我猜测十有八九是因为打开了Trim Enabler的缘故，于是准备进入单用户模式将其禁止掉。先重启机器，按Command + S，准备进入单用户模式，但是在出现Still waiting for root device之后就没动静了。在网上翻来翻去，终于找到了[Heads up - OSX 10.10 Beta -no go](http://www.cindori.org/forums/topic/heads-up-osx-10-10-beta-no-go/)，按照里面的方法终于解决了问题，其实就是这么简单几步：

{% code %}
rm -rf /Volumes/<10.10 Partition>/System/Library/Extensions/IOAHCIFamily.kext
cp -r /System/Library/Extensions/IOAHCIFamily.kext /Volumes/<10.10 Partition>/System/Library/Extensions/IOAHCIFamily.kext
touch /Volumes/<10.10 Partition>/System/Library/Extensions
kextcache -u /Volumes/<10.10 Partition>
{% endcode %}
