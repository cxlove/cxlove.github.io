---
layout: post
title : MachineLearing学习笔记(8)--回归
description : MachineLearing学习笔记(8)--回归
category : 研究
tags : MachineLearning study-note Python
keywords : 
---

## 线性回归
定义方程y = w * x

x是特征向量，我们添加x0 = 1

然后利用最小二乘法直接解，w = (x^T * x)^-1 * x^T * y

## 局部加权线性回归
对于每个测试点，加入到训练集中，对于训练集中的每个点，设定一个权值，一般就认为离测试点近的权值大，这样作出的预测比较合理。

通常采用高斯核  weight = |x - x'| / (-2 * k ^ 2)

weight就是一个矩阵，定义训练集中点的权值。

w = (x^T * weight * x)^-1 * x^T * weight * y

## 岭回归
我们添加惩罚项
w = (x^T * x + lambda * I)^-1 * x^T * y

lambda是个系数，I是个单位矩阵。能够减少不重要的参数特征。

## 前向逐步回归
其实很接近随机化变步长，以及模拟退火等思想。

就是迭代很多次，每次枚举一个系数，然后小幅改变一下，然后通过误差函数判断，选择误差最小的方向继续迭代。



## 代码
[代码君前往cxlove's github寻找](https://github.com/cxlove/MachineLearning/tree/master/Regression)