---
layout : post
title : MachineLearing学习笔记(6)--AdaBoost自适应提升法
description : MachineLearing学习笔记(6)--AdaBoost自适应提升法
category : 研究
tags : MachineLearning study-note Python
keywords : 
---

##AdaBoost 自适应提升法
Boosting大法好，在一个很简单的分类器，或者方法中，通过不断迭代等方案，能够把一个弱可学习提升为一个强可学习。

可能在一些高端技术出现之前，如DL，AdaBoost是一项非常重要的技能，在之前技术的基础上，尽可能的提升效果。

## AdaBoost过程
1.  初始化训练数据权值,<a href="http://www.codecogs.com/eqnedit.php?latex=D_1&space;=&space;\{&space;w_{11}&space;,&space;w_{12}&space;,&space;\dots&space;,&space;w_{1N}\}&space;,&space;w_{1i}&space;=&space;\frac{1}{N}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?D_1&space;=&space;\{&space;w_{11}&space;,&space;w_{12}&space;,&space;\dots&space;,&space;w_{1N}\}&space;,&space;w_{1i}&space;=&space;\frac{1}{N}" title="D_1 = \{ w_{11} , w_{12} , \dots , w_{1N}\} , w_{1i} = \frac{1}{N}" /></a>
2.  对于每一次迭代

   (1)  训练弱分类器

   (2)  计算分类误差率 e

   (3)  计算系数<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha_m&space;=&space;\frac{1}{2}\log{\frac{1-e_m}{e_m}}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha_m&space;=&space;\frac{1}{2}\log{\frac{1-e_m}{e_m}}" title="\alpha_m = \frac{1}{2}\log{\frac{1-e_m}{e_m}}" /></a>

   (4)  更新权值分布

3.  通过所有弱分类器线性组合 ，得到强分类器。

## 实验

利用之前logistic回归中用到的实验数据，只需要50次迭代，错误率达到23%左右，优于logistic回归。

弱分类器中，我用的是决策树，而且就一层决策。

## 代码
[代码君请前往github](https://github.com/cxlove/MachineLearning/tree/master/AdaBoost)

