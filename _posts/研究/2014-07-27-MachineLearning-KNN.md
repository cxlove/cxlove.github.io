---
layout: post
title : MachineLearing学习笔记(2)--K近邻算法
description : MachineLearing学习笔记(2)--K近邻算法
category : 研究
keywords :
tags : MachineLearning study-note Python
---

# K近邻算法

### 简述
KNN不同于Kmeans的一个很重要的地方就是,KNN是监督学习，而Kmeans是无监督学习。

Kmeans只是聚类，而没有学习。

KNN是需要训练数据集的，而Kmeans更多的是自动学习，没有参考。

KNN意为K近邻算法，很好理解。就是在训练数据集中找到数据特征最相近的K个样本，而这K个样本中某个分类的次数最大，就把测试样本归为这个类。

### 优点
1. 想法简单
2. 不需要训练
3. 精度高

### 缺点
1.  计算量高，对于每个测试样本，都要和所有的训练数据进行比对，时间、空间复杂度都高。

### 要点
1.  k值的确定，类似kmeans存在的一个问题
2.  距离或者相似度的衡量
3.  类别的判定，直接根据最近的K个样例投票决定，或者进行加权判定。

# 手写识别系统

### 数据
1.  traningDigits:给出若干手写数据集
2.  testDigits:给出若干测试数据，已知标签，可以检测正确率。

数据特征：每个手写用32 * 32的像素矩阵表示(0/1矩阵)

### 距离定义
1024个像素点，有多少个不同像素点，即距离。。。

### 结果
![result](/images/ML2_1.png)

### 代码
[代码及数据集请前往github](https://github.com/cxlove/MachineLearning/tree/master/KNN)