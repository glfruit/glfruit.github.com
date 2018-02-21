title: "使用Zotero做科研（五）——与Scrivener的整合"
date: 2015-12-27 12:37:47
tags: [Zotero, Scrivener]
categories: IT生活
---
通常我的写作都是在Scrivener里面进行，它跨平台，对于写作素材的搜集和管理也十分方便，但是用在写论文时有个最大的问题，就是不能像在Word里面一样方便地添加文献引用。虽然也有折衷的办法，像[这篇文章](https://danielvreeman.com/using-scrivener-for-writing-scientific-papers/)里的方法，我的上一篇论文就是采取这种方式完成的，可是觉得繁琐，而且还要装个不想干的LireOffice。几天前心血来潮又开始新的折腾的时候，发现了[这篇文章](http://davepwsmith.github.io/academic-scrivener-howto/)，按照其中的步骤进行配置，又根据自己的环境进行了调整，总算是实现了在Scrivener里一键插入文献引用的功能，并且又根据里面的AppleScript脚本依样画葫芦，用PowerShell实现了一个Windows版的脚本，这样在Windows上也可以实现同样的效果了。
<!-- more -->
下面就是详细的折腾步骤：

首先下载安装Zotero的[Better BibTex插件](https://zotplus.github.io/better-bibtex/)；安装好之后在Zotero里使用该插件将文献库导出，导出时最好勾选上Keep Updated选项，这样当你更新文献库时对应的BitTex文件也会自动更新；

然后安装Pandoc，我用的[HomeBrew](http://brew.sh)管理安装，因此直接用它安装pandoc和它的一个插件pandoc-citeproc：
`````
brew install pandoc   
brew install pandoc-citeproc
`````
安装好pandoc后还要做的一件事情就是去[这里](https://www.zotero.org/styles/chinese-gb7714-2005-numeric)下载中文的样式，并且将它放在自己的用户目录的.csl目录下，pandoc默认是在这个位置搜索样式文件，当然你也可以根据自己的喜好配置pandoc去其它地方搜索。

这样之后就可以开始在Scrivener里面用pandoc支持的Markdown语法撰写文章了，但是这不是重点，我们的重点是要能在Scrivener里方便地一键引用文献，所以我们还需要下载一个[AppleScript文件](https://github.com/davepwsmith/zotpick-applescript)，将它放在你喜欢的地方，然后打开Scrivener，将文献管理器设置为该文件。当然你如果直接设置的话会发觉无法将该文件设置为文献管理器，需要将它打包成一个应用的形式才行，打包的方法在上面的链接里已经提供了，我就不多说了。完成这一步之后，当你在Scrivener里写作需要引用文献时只需要按下Cmd+Y键，一个供你搜索插入文献的对话框就出现了，真的是十分的方便。
完成写作之后当然就是发布了，这时我们只需要运行下面这条命令就可以生成Word文档了：
`````
pandoc -s -S --normalize --bibliography \ ~/.pandoc/YOUR_BIBLIOGRAPHY.bib \ --csl ~/.csl/YOUR_CITATION_STYLE.csl \ -f markdown -t docx \ -o MYPROJECT.docx MYPROJECT.txt
`````
其中YOUR_BIBLIOGRAPHY.bib是你导出的BibTex文件的名字，YOUR_CITATION_STYLE.csl是所选择的样式文件的名字。完成之后，一篇样式精美的论文也就生成了。

### Windows下的设置
基本步骤和在Mac上差不多，只是不能用前面提供的AppleScript文件作为文献管理器，而是需要把[Set-ActiveWindow.ps1](https://gist.github.com/glfruit/6e7218abb6a1449d4016)和[zotpick-pandoc-win.bat](https://gist.github.com/glfruit/3bd34f4e5d29c4c80bcc)这两个文件下载下来，放在同一个地方，然后在Scrivener里将zotpick-pandoc-win.bat文件设置为其文献管理器就可以了。

### 注意事项：

- Zotero必须保持打开状态
- 搜索框里无法直接搜索中文文献，要切换到经典视图才行，无论是Mac还是Windows都是一样

### 遗留问题：
中文啊，还是中文，在弹出的搜索框里输入中文没有任何反应，只有切换到经典视图才能进行中文搜索，算是美中不足吧。原来以为是脚本的问题，经测试发现是Better Latex插件的问题，怎么解决还不知道

### 参考资料：

1. [Scrivener for academic writing with Zotero](http://davepwsmith.github.io/academic-scrivener-howto/)
2. [Provide input to applications with PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2011/01/10/provide-input-to-applications-with-powershell.aspx)
