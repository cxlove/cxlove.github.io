---
layout: post
title : Python学习笔记(4)--将OnlineJudge上的代码爬下来
description : Python学习笔记(4)--将OnlineJudge上的代码爬下来，如POJ,HDOJ
category : 技术
tags : Python study-note
keywords : 
---


#Python实例(4)--代码收集器

##说在前面

　　混了几年的ACM，在大大小小的OJ上也做了不少的题，尤其是国内比较著名的POJ,HDOJ。但是很遗憾，一直没有保留代码的习惯，所以借着学习python的时机，希望能够弥补这个小小的遗憾。

　　那么目的就很明确了，进入 POJ/HDOJ，将自己Accept的代码down到本地。

##步骤
1.  模拟登录网站
2.  访问相关页面
3.  将代码保存到本地

##知识点
1.  网络相关知识，urllib2库的使用
2.  基础爬虫知识
3.  文件处理
4.  正则表达式

##具体操作
###模拟登录
　　总体来说，登录的时候，页面会post相关数据。那么我们模拟登录的话，就是伪造这样一个post数据。

　　首先，我们先抓吧，看看POJ在登录的时候，都post了些什么数据。在chrome中，直接F12利用开发工具就能完成抓包。见下图

![PostData](/images/PythonNote4_1.png)

　　有两个步骤，1、伪造成浏览器，不然可能会被认为是恶意攻击，即构造 一个headers，2、提供相应的PostData,即From Data里面的信息。

###下载代码
　　成功登录之后，进入相应的status页面，观察html代码，像poj,hdoj，可以获得AC代码的ID，然后直接通过URL就能访问代码页面。这需要一定的RE处理。

　　打开代码页面之后，可以发现代码只是其中一部分，头部有一些信息，而从中可以得到语言、题号等信息，这也需要一定的正则处理。

　　还有一点是，status页面需要翻页，我发现在POJ/HDOJ上，URL中都有一个类似的属性，如top=XXX，那么表示从top这个ID开始，逆序排列相应的提交记录。

　　所以就可以根据这个信息进行翻页。

## 代码

[代码前往Github](https://github.com/cxlove/Python/tree/master/CodeCollect)




