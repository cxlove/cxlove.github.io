---
layout: post
title : Python学习笔记(1)--文件操作
keywords :
description : 初学Python，记录一些Python针对文件、目录操作的函数。以及一些简单的实例。
category : 技术
tags : Python study-note
---


## 目录操作

　　首先，Python中可以很方便地进入目录，操作文件。那么这些对文件、文件夹操作的函数都涉及到了os模块和shutil模块。

	import os
	import shutil

###　目录操作函数

1.  得到当前工作目录：`os.getcwd ()`
2.  返回指定目录下的所有文件和目录名：`os.listdir ()`
3.  删除一个文件：`os.remove ()`
4.  删除一个文件夹:`os.removedirs () # 我没成功过`
5.  检验给出的路径是否是一个文件：`os.path.isfile ()`
6.  检验给出的路径是否是一个文件夹:`os.path.isdir ()`
7.  判断路径是否是绝对路径：`os.path.isabs ()`
8.  判断路径是否存在：`os.path.exists ()`
9.  返回一个路径的目录名和文件名（按最后一个'/'分开,返回的是一个字符串list，两个元素）:`os.path.split ()`
10.  分离文件的扩展名：`os.path.splitext ()`
11.  获取路径名:`os.path.dirname ()`
12.  获取文件名：`os.path.basename ()`
13.  运行shell命令：`os.system ()`
14.  重命名：`os.rename (old , new)`
15.  创建多级目录：`os.makedirs ()`
16.  创建单个目录：`os.mkdir ()`
17.  获取文件大小：`os.path.getsize ()`
18.  复制文件，从文件到文件：`shutil.copyfile (old , new)`
19.  复制目录，newdir必须不存在：`shutil.copytree (old , new)`
20.  移动文件：`shutil.move (old , new)`
21.  删除空目录:`os.rmdir ()`
22.  删除目录，连同文件一起删:`shutil.rmtree ()`
23.  换路径：`os.chdir ()`


### 文件操作函数

1.  创建空文件:`os.mknod (name)`
2.  读取长度size byte的：`fp.read ([size])`
3.  读取一行：`fp.readline ()`
4.  将每一行按一个list读入：`fp.readlines () #其实就是个循环的readline ()`
5.  将串写到文件：`fp.write (str)`
6.  多行写入（注意：是不会在行末添加换行的）:`fp.writelines (list)`
7.  缓冲区写入硬盘：`fp.flush ()`


## 实例操作

### 1. 将某个目录下的所有文件名，去除后缀后保存在文件里

　　这个问题很简单，首先不是在当前目录下，先转换一下目录后，读取所有的文件在list中，然后把后缀去掉，找到文件名里的.即可,Python里的切片非常方便。`with open () as XX :`是Python中针对IO读写提供的异常进制，比try expected finally方便点。

    # by cxlove
    import os
    
    os.chdir (r'E:\Code')   #当前在源文件目录下，更改目录
    file = os.listdir (os.getcwd ())  #得到当前目录下所有文件名
    
    for name in file :
    	file[file.index (name)] = name[0:name.index ('.')] #去掉后缀
    
    with open(r'filename.txt', 'w') as out:  #文件读写
    	for name in file :
    		out.write (name + '\n')

### 2. 将目录下所有的.h重新标号，1.h,2.h……


    # by cxlove
    # -*- coding:utf-8 -*-
    
    import os , time
    
    start_time = time.time ()
    os.chdir (r'E:\Python\temp')  
    file = os.listdir (os.getcwd ())  
    id = 1
    for name in file :
    	if os.path.isfile (name):
    		if len (name) >= 3 and name[-2:] == '.h' :
    			os.rename (name , str (id) + '.h')
    			id = id + 1
    print u'总共处理%d 个.h文件 ，总共耗时%.2f S' % (id , time.time () - start_time)
    

　　运行结果如下：

![Result](/images/PythonNote1_1.png)


