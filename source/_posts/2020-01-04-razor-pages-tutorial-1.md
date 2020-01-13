---
title: ASP.NET Core Razor Pages入门（一）
date: 2020-01-04 22:56:55
tags: 教程,DotNet
---
# ASP.NET Core Razor Pages入门（一）
[原文地址](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-3.1&tabs=visual-studio)

**注：**本文及后续的系列文章是我对[Tutorial: Get started with Razor Pages in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-3.1&tabs=visual-studio)的中文翻译和补充。之所以内容上会有所补充，是由于.NET Core版本升级的关系，原文代码中饮用的一些类和方法的命名空间已经发生了变化，按照原文所给的源代码是无法顺利运行的，因此我进行了修正补充，以使得示例代码能够顺利运行。

在本教程中，你将：
- 创建一个Razor Pages的Web应用
- 运行该应用
- 查看项目文件

教程结束后，你将拥有一个可以用于后续教程中的可以工作的Razor Pages web应用。
![](https://raw.githubusercontent.com/glfruit/pic_bed/master/20191228085608.png)
<!-- more -->
## 先决条件
### Visual Studio 
- [Visual Studio 2019 16.4或之后的版本](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019),加载有ASP.NET和Web开发workload
- [.NET Core 3.1 SDK或之后的版本](https://dotnet.microsoft.com/download/dotnet-core/3.1)

### Visual Studio Code
- [Visual Studio Code](https://code.visualstudio.com/download)
- [C# for Visual Studio Code(最新版本)](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
- [.NET Core 3.1 SDK或之后的版本](https://dotnet.microsoft.com/download/dotnet-core/3.1)

## 创建Razor Pages web应用
### Visual Studio Code
- 打开内部终端
- 运行下列命令：
```
dotnet new webapp -o RazorPagesMovie
code -r RazorPagesMovie
```

- ```dotnet new```命令在RazorPagesMovie文件夹中创建一个新的Razor Pages项目
- ```code```命令在Visual Studio Code中打开RazorPagesMovie文件夹
- 在状态栏的OmniShapr图标变为绿色之后，会弹出一个对话框，显示"Required assets to build and debug are missing from 'RazorPagesMovie'. Add them?"。选择Yes。一个包含*launch.json*和*tasks.json*文件的*.vscode*目录会添加到项目的根目录下

## 运行应用
- 运行下列命令，信任HTTPS开发证书：
```
dotnet dev-certs https --trust
```

上面的命令在Linux上无法使用。参考所使用的Linux版本的文档以了解如何信任证书。
- 如果你同意信任开发证书，那么就选择Yes
![](https://raw.githubusercontent.com/glfruit/pic_bed/master/20191228091140.png)

参见[Trust the ASP.NET Core HTTPS开发证书](https://docs.microsoft.com/en-us/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos)以了解更多信息。
- 按**Ctrl-F5**，以非调试模式运行应用
Visual Studio Code会启动[Kestrel](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-3.1)，运行浏览器，导航到*http://localhost:5001*。

## 检查项目文件
下面对主要项目文件夹和文件进行概览，你在后面的教程中将会用到。
### Pages文件夹
包含了Razor页面和支持文件。每个Razor页面都由两个文件组成：
- 一个.cshtml文件，包含HTML标记以及使用Razor语法的C#代码
- 一个.cshtml.cs文件，包含处理页面事件的C#代码

支持文件的名字以下划线开头。例如，*_Layout.cshtml*文件配置对所有页面都通用的UI元素。这个文件设置页面顶部的导航菜单以及页面底部的版权声明，参见[Layout in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/layout?view=aspnetcore-3.1)。

### wwwroot文件夹
包含静态文件，例如HTML文件，JavaScript文件和CSS文件。参见[Static files in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/static-files?view=aspnetcore-3.1)以了解更多信息。

### appSettings.json
包含配置数据，例如连接字符串。参见[Configuration in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-3.1)以了解更多信息。

### Program.cs
包含程序的入口点。参见[.NET Generic Host](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-3.1)以了解更多信息。

### Startup.cs
包含配置应用行为的代码。参见[App startup in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/startup?view=aspnetcore-3.1)以了解更多信息。

## 下一步
进入到本系列的下一个教程：
[添加模型](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/model?view=aspnetcore-3.1)