---
layout: post
title : Jekyll 学习笔记
category : 技术
tags : Jekyll  study-note
keywords :
description : jekyll是一个简单的免费的Blog生成工具,可以免费部署在GitHub上。本文简单记录下自己配置环境，以及入门的过程。

---


#Windows 下配置Jekyll
　　首先，很惭愧地作为一个Win狗，即使很乐意在Liunx下玩玩，但是始终还是愿意把一份工作在Win下也做一遍。

　　OS:Windows 7

　　Jekyll是用Ruby语言编写的，所以首先要配置好Ruby环境。

##步骤
1.  安装Ruby：在windows下，使用rubyinstaller。
2.  安装Ruby DevKit。
3.  安装Jekyll。

##操作
1.  下载rubyinstaller,[点击下载](http://rubyinstaller.org/downloads/)。我下的是`2.00-p481`。
2.  安装rubyinstaller,安装选项里所有都勾上。
3.  下载DevKit,[点击下载](https://github.com/downloads/oneclick/rubyinstaller/DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe)。
4.  把下载的DevKit解压，在该目标下运行以下命令。

		ruby dk.rb init

    然后可以发现生成了一个config.xml的配置文件，文件里面是Ruby的安装目录。

	然后运行以下命令
    	
		ruby dk.rb install
5.  安装jekyll，运行以下命令：

		gem install jekyll

6.  这样就完成了，你可以写一个简单页面，或者fork一个，然后在进	入到相应目录，运行以下命令：
  
		jekyll serve


	然后通过浏览器访问`localhost:4000`就可以了。

　　PS：很多人说直接在CMD里安装jekyll会有很多问题，但是似乎我没遇到过。不过也可以通过DevKit来安装。