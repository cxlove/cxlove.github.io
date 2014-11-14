---
layout: post
title : MachineLearing学习笔记(9)--PCA主成成分分析
description : MachineLearing学习笔记(9)--PCA主成成分分析
category : 研究
tags : MachineLearning study-note Python
keywords : 
---

##PCA(principal components analysis)
真实数据集中可能会遇到许多特征非常多的数据集，甚至于特征数量>样本数据个数。

但是如果人为的去分析，会发现其中可能有很多的的冗余特征，或者有些强相关的特征。

所以我们希望能够降低特征的维数，减少数据里面的噪声和冗余，减少过拟合的可能性。

PCA就是一种十分常用的方法，整个过程是将n维的特征映射到k维上。

###步骤
1.  先将数据归一化，首先使均值为0，求得均值后，将数据集减去均值。然后方差归一化，求得方差，将数据集除以方差
2.  求得协方差矩阵，表示特征两两之前的相关性
3.  求得协方差矩阵的特征值和特征向量
4.  将特征向量排序，选取前k大的特征值，保留相对应的特征向量，组成特征向量矩阵
5.  将数据集投影到选取的特征向量上，即数据集是(m * n) ,特征向量矩阵是(n * k)，得到(m * k)的数据，即m组数据，每组数据k维特征。


###最大方差理论
方差越大，说明数据具有更好的区分度。

我们认为信号应该是方差大，噪声是方差小，所以在我们选取投影矩阵的时候，我们希望得到的方差最大，这就是最大方差理论。

###最小平方误差理论
投影的话相当于去拟合，那么我们可以通过最小平方误差来衡量好坏。这就是最小平方误差理论。

### 证明
[最大方差理论](http://www.cnblogs.com/jerrylead/archive/2011/04/18/2020209.html)

[最小平方误差理论](http://www.cnblogs.com/jerrylead/archive/2011/04/18/2020216.html)

### 结果
![result](/images/ML9_1.png)

###代码君
[代码君前往cxlove's github寻找](https://github.com/cxlove/MachineLearning/tree/master/PCA)


