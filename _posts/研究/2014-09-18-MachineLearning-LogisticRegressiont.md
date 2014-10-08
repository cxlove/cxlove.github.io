---
layout: post
title : MachineLearing学习笔记(4)--Logistic回归
description : MachineLearing学习笔记(4)--Logistic回归
category : 研究
tags : MachineLearning study-note Python
keywords : 
---

# Logistic 回归

　　这是真正意义上的最优化算法了，之前的K-means,KNN都不涉及这些。

　　首先要了解回归，通常认识是建立一个模型(线性，多项式等)去拟合数据，更好得用这个模型去表征数据。

　　而Logistic回归最基础的是用于二值型输出分类器，即将一个class定义成0，另外一个class定义成1。Logistic回归的作为就是对于输入的特征X，输出预测的类Y(0/1)。

## Sigmod函数
　　因为现在要做的是二值型的预测，所以回归模型的返回值应该是0,1，有点像是阶跃函数，分段函数，或者阶梯函数等等。但是边界便不好处理，或者说不好表示。

　　但是存在另外一个函数有着相似的性质，便是sigmod函数，公式如下 ：

<a href="http://www.codecogs.com/eqnedit.php?latex=f(x)&space;=&space;\frac{1}{1&plus;e^{-z}}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?f(x)&space;=&space;\frac{1}{1&plus;e^{-z}}" title="f(x) = \frac{1}{1+e^{-z}}" /></a>

　　可以知道sigmod函数在z=0的时候，值为0.5，然后是关于(0 , 0.5)中心对称的，而且值在(0 , 1)之间，z越接近负无穷，值越接近0，反之越接近1。

　　通过这样的处理，便可以得到一个(0 , 1)之间的数值，为了更好的分类，我们可以定义小于等于0.5的被分为y = 0类，其余的分为y = 1类。

## 线性模型

### 模型的定义
　　假设当前样本有两个特征<a href="http://www.codecogs.com/eqnedit.php?latex=(x_1&space;,&space;x_2)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?(x_1&space;,&space;x_2)" title="(x_1 , x_2)" /></a> ,所属类别y = 0 | y = 1。

　　我们定义线性模型<a href="http://www.codecogs.com/eqnedit.php?latex=f(x)&space;=&space;w_0&space;&plus;&space;w_1&space;*&space;x_1&space;&plus;&space;w_2&space;*&space;x_2" target="_blank"><img src="http://latex.codecogs.com/gif.latex?f(x)&space;=&space;w_0&space;&plus;&space;w_1&space;*&space;x_1&space;&plus;&space;w_2&space;*&space;x_2" title="f(x) = w_0 + w_1 * x_1 + w_2 * x_2" /></a>。我们令<a href="http://www.codecogs.com/eqnedit.php?latex=x_0&space;=&space;1" target="_blank"><img src="http://latex.codecogs.com/gif.latex?x_0&space;=&space;1" title="x_0 = 1" /></a>，那么便可以对每组特征构造向量<a href="http://www.codecogs.com/eqnedit.php?latex=x&space;=&space;\{x_0&space;,&space;x_1&space;,&space;x_2\}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?x&space;=&space;\{x_0&space;,&space;x_1&space;,&space;x_2\}" title="x = \{x_0 , x_1 , x_2\}" /></a>，系数向量<a href="http://www.codecogs.com/eqnedit.php?latex=w&space;=&space;\{w_0&space;,&space;w_1&space;,&space;w_2\}^T" target="_blank"><img src="http://latex.codecogs.com/gif.latex?w&space;=&space;\{w_0&space;,&space;w_1&space;,&space;w_2\}^T" title="w = \{w_0 , w_1 , w_2\}^T" /></a>。那么可以得到<a href="http://www.codecogs.com/eqnedit.php?latex=f(x)&space;=&space;w^T&space;*&space;x" target="_blank"><img src="http://latex.codecogs.com/gif.latex?f(x)&space;=&space;w^T&space;*&space;x" title="f(x) = w^T * x" /></a>。

### Cost Function
　　我们知道，在不论是回归还是分类中，我们都会定义一个cost function，以得到模型预测与实际样本之间的“差距”，我们希望得到的模型的cost function尽可能小(当然了，我们这里暂时不考虑overfitting的情况)。

　　那么两类0/1，我们直接定义距离的平方和作为cost function。

　　然后定义<a href="http://www.codecogs.com/eqnedit.php?latex=J(w)&space;=&space;\frac{1}{2}\sum\limits_{i=1}^{N}(f(x_i)&space;-&space;y_i)&space;^&space;2" target="_blank"><img src="http://latex.codecogs.com/gif.latex?J(w)&space;=&space;\frac{1}{2}\sum\limits_{i=1}^{N}(f(x_i)&space;-&space;y_i)&space;^&space;2" title="J(w) = \frac{1}{2}\sum\limits_{i=1}^{N}(f(x_i) - y_i) ^ 2" /></a>。其中<a href="http://www.codecogs.com/eqnedit.php?latex=x_i" target="_blank"><img src="http://latex.codecogs.com/gif.latex?x_i" title="x_i" /></a>表示第i组学习样本的特征数据,<a href="http://www.codecogs.com/eqnedit.php?latex=y_i" target="_blank"><img src="http://latex.codecogs.com/gif.latex?y_i" title="y_i" /></a>表示第i组学习样本的类别。

 　接下来的最优化过程，就是通过得到w使得J(w)尽可能的小。

## 梯度下降法

### 基础算法
　　梯度下降法，基本上是个最简单的最优化算法，十分易懂。基于的思想就是，找到某函数的最值，最好的方法就是沿着该函数的梯度方向探寻。

　　不断进行以下过程的迭代
　　<a href="http://www.codecogs.com/eqnedit.php?latex=for&space;~~each&space;~~&space;w_i&space;~~&space;in&space;~~&space;w&space;:&space;~~&space;w_i&space;:=&space;w_i&space;-&space;\alpha&space;*&space;\frac{d&space;J(w)}{d&space;w_i}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?for&space;~~each&space;~~&space;w_i&space;~~&space;in&space;~~&space;w&space;:&space;~~&space;w_i&space;:=&space;w_i&space;-&space;\alpha&space;*&space;\frac{d&space;J(w)}{d&space;w_i}" title="for ~~each ~~ w_i ~~ in ~~ w : ~~ w_i := w_i - \alpha * \frac{d J(w)}{d w_i}" /></a>

　　其中$\alpha$指的是迭代步长，如果过大，则会达不到梯度下降的效果，可能直接越过最值。如果过小，则会迭代过慢。

### 随机梯度下降
　　梯度下降有个问题就是可能收敛得很慢，需要迭代次数非常多。如果数据集非常大的话，计算复杂度可能过于大。所以考虑进行优化加速。

　　例如方案1：每次迭代，并不会对所有数据进行更新回归系数，而是选取选取一组或者若干组样本。或者方案2：每一组样本都用来更新一次回归系统。我们称这样的做法为随机梯度下降法。

### 改进的随机梯度下降法
　　实验发现随机梯度下降效果并不好，由于数据并不一定完全线性可分，导致了一些很大的波动。所以考虑进行改进。

　　改进1：每次更新步长，随机迭代次数的增加，步长减少，但是在最优化过程中，一般步长不要严格下降，而且不要达到0。

　　改进2：在选取样本更新系数的时候，采用随机的方法，并不是按顺序处理。

##实验结果
　　我们对于一组数据进行Logistic回归预测。每组样本包含两个特征，以及一个0/1分类。我们分别用不同的随机梯度下降方法，以及不同的参数进行实验。

　　测试1，普通的梯度下降，步长0.01，迭代500次。实验结果如下：

![result1](/images/ML4_1.png)
![result2](/images/ML4_2.png)

　　测试2，普通梯度下降，步长0.001，迭代500次。实验结果如下：

![result3](/images/ML4_3.png)
![result4](/images/ML4_4.png)

　　测试3，随机梯度下降，步长0.01，迭代500次。实验结果如下：

![result5](/images/ML4_5.png)
![result6](/images/ML4_6.png)

　　测试４，改进后的随机梯度下降，迭代500次。实验结果如下：

![result7](/images/ML4_7.png)
![result8](/images/ML4_8.png)

# 从疝飞病症预测病马的死亡率

##处理数据中的缺失值
　　数据集可以从[http://archive.ics.uci.edu/ml/datasets/Horse+Colic](http://archive.ics.uci.edu/ml/datasets/Horse+Colic)下载。

　　但是现实生活中，很多数据都有缺失，比如说有些样本中的某些数据采集困难，或者因为设备问题，等等。但是如果有个特征无效便丢弃数据的话，成本过高。

　　有以下办法进行弥补：
1.  使用其它样本的均值来填补
2.  使用特殊值，如果 -1或者0
3.  丢弃样本
4.  使用相似样本的均值，或者其它ML算法来预测。

　　在这个数据集中，有30%的数据丢失，我们采用0来填补，因为0的话，对于梯度下降的时候，不会影响到系数。

##结果
　　我们采用普通的梯度下降，迭代500次，步长为0.01的方法进行二值分类，然后通过给定的测试集进行预测，正确率大约为63%。因为数据丢失在30%，所以这样的正确率还可以接受。

![result](/images/ML4_9.png)

#代码君
[代码君请前往Github取](https://github.com/cxlove/MachineLearning/tree/master/logisticRegression)




