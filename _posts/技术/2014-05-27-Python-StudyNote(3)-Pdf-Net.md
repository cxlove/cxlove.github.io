---
layout: post
title : Python学习笔记(3)--绘制PDF图表以及网络编程
description : Python实例(2)，画幅好画。主要是从网络上获取文档之后，进行PDF上的绘制图表。
category : 技术
tags : [Python,study-note]
keywords : 
---

#Python实例(2)--画幅好画

## 要求

　　从网上down一个文件下来，将里面的数据绘制成图表存于PDF文件。

　　数据源：[太阳黑子运动](http://www.swpc.noaa.gov/ftpdir/weekly/Predict.txt)

　　观察数据之前，前面几行都是不需要的数据，从数字表格开始。每一行8个实数。

## 实现

　　首先会有两个子问题：

1.  从网上down获取数据的方法，牵扯网络编程，用的是urllib模块。
2.  Python对于PDF的操作，用的是reportlab模块。

## urllib 模块

　　这是Python提供的一个网络编程模块，可以帮助我们访问网络上的数据，如同本地操作一样。

　	<del>**由于cxlove不是很懂网络知识，所以只能口胡了。**</del>

　　像我了解一些基本方法的用法就好了：

1. `urlopen`可以理解为打开一个网络上的文件，<del>其实似乎是创建了一个远程的类文件对象</del>。可以帮助我们读取、操作远程数据。
2. `urlretrieve`可以理解为从网络上down一个文件保存在本地。

　　那么在我们这个实例中，只需要获取文件，然后读取信息就OK了。

## reportlab 模块
　　
　　这是Python平台上很常用的PDF报表类库，可以很方便在PDF文件中生成一些报表。

　　不是标准类库，所以首先是下载安装：
1.  [ReportLab](https://www.reportlab.com/software/downloads/)
2.  [Python Imaging Library](http://www.pythonware.com/products/pil/)

　　其中PIL是Pyhton对于图片操作的模块。

## 代码

    # -*- coding:utf-8 -*-
    
    import urllib
    from reportlab.graphics.shapes import *
    from reportlab.graphics.charts.lineplots import *
    from reportlab.graphics.charts.textlabels import *
    from reportlab.graphics import *
    
    URL = 'http://www.swpc.noaa.gov/ftpdir/weekly/Predict.txt'
    data = []
    for line in urllib.urlopen (URL).readlines ():
    	if not line.isspace () and line[0] != '#' and line[0] != ':' :
    		data.append ([float (n) for n in line.split ()])
    
    times = [row[0] + row[1] / 12.0 for row in data]
    pred = [row[2] for row in data]
    high = [row[3] for row in data]
    low = [row[4] for row in data]
    
    drawing = Drawing (400 , 200)
    
    lp = LinePlot ()
    lp.x = 50
    lp.y = 50
    lp.height = 125
    lp.width = 300
    lp.data = [zip (times , pred) , zip (times , high) , zip (times , low)]
    lp.lines[0].strokeColor = colors.blue
    lp.lines[1].strokeColor = colors.red
    lp.lines[2].strokeColor = colors.green
    
    drawing.add (lp)
    drawing.add (String (250 , 150 , 'Sunspots' , frontSize = 14 , fillColor = colors.red))
    
    renderPDF.drawToFile (drawing , 'Report.pdf' , 'Sunspots')
    
　　照着敲一下熟悉一下好了，有机会可以尝试一下其它的数据源，然后就会有不同的需求

### 结果

　　生成的PDF效果见下图：

![Result](\images\PythonNote3_1.png)
