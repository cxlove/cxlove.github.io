---
layout: post
title : 推荐系统(2)-- 隐语义模型
description : Recommend System(2)--Latent Factor Model
category : 研究
tags : RecommendSystem study-note Python
keywords : 
---

#隐语义模型

## 前情概要

隐语义模型，顾名思义就是挖掘用户行为信息中的隐含信息，，隐含语义。

在之前提到过通过相似性进行推荐，给用户推荐相似用户所喜欢的物品，给用户推荐和喜欢的物品相似的其它物品。

而在实际应用中，还有一点非常容易被想到，那就是分类别，分领域推荐。对不同的类别，喜欢的程度不一样，而每件物品在每个类中的权重也不一样。

在实际中，一般的商品都会添加有标签，通常可能是物品上架就自带有标签类别，或者是由编辑添加类别，或者是由用户分类。但是这样会有储多问题存在，比如部分物品不便于具体分类，如《具体数学》，可以认为是数学类，而大多是计算机科学技术人员阅读。比如不好控制分类的粗细，如《shell脚本学习指南》，可以属于计算机科学技术，也可以属于程序设计语言，也可以属于Linux平台开发，也可以属于软件工程。比如不好控制在不同类别中的权值，如《具体数学》可以是数学类，也可以是计算机类，但是相对而言，可能在计算机类的比重应当大于在数学类的比重。

对于以上问题，隐语义模型应运而生，通过对用户行为的数据自动分析，自动聚类，同时衡量每个用户对于隐含类别的权重，每个物品对于每个隐含类别的权重。

## 模型描述


### 模型

假设有F个隐类别。

而P(user , k)表示用户u的兴趣和第k个隐类别的关系，即在第k个类别中的权重。

Q(item , k)表示物品i和第k个隐类别的关系。

则用户user对物品item的兴趣度为：

<a href="http://www.codecogs.com/eqnedit.php?latex=Prefer&space;(user&space;,&space;item)&space;=&space;\sum_{k=1}^F{P(user&space;,&space;k)&space;*&space;Q(item&space;,&space;k)}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Prefer&space;(user&space;,&space;item)&space;=&space;\sum_{k=1}^F{P(user&space;,&space;k)&space;*&space;Q(item&space;,&space;k)}" title="Prefer (user , item) = \sum_{k=1}^F{P(user , k) * Q(item , k)}" /></a>


那么需要对于P,Q的参数进行训练。

则定义损失函数为：

<a href="http://www.codecogs.com/eqnedit.php?latex=L&space;=&space;\sum_{(user&space;,&space;item)&space;\in&space;data}&space;(score&space;(user&space;,&space;item)&space;-&space;Prefer&space;(user&space;,&space;item))&space;^&space;2&space;&plus;&space;\lambda&space;||P(user)||^2&space;&plus;&space;\lambda&space;||Q(item)^2||" target="_blank"><img src="http://latex.codecogs.com/gif.latex?L&space;=&space;\sum_{(user&space;,&space;item)&space;\in&space;data}&space;(score&space;(user&space;,&space;item)&space;-&space;Prefer&space;(user&space;,&space;item))&space;^&space;2&space;&plus;&space;\lambda&space;||P(user)||^2&space;&plus;&space;\lambda&space;||Q(item)^2||" title="L = \sum_{(user , item) \in data} (score (user , item) - Prefer (user , item)) ^ 2 + \lambda ||P(user)||^2 + \lambda ||Q(item)^2||" /></a>


其实后面的部分是防止过拟合的正则化项，然后通过随机梯度下降进行优化训练就可以了。

并没有什么好说的。。。


### 样本构造 

因为movielens里面并没有负样本，然后需要构造一些。用户只对部分物品有过行为，第一种方案就是用户所有没有行为的物品为负样本，或者是采样一些。另外的方案就是，在没有过行为的物品中，按流行度采样。流行度很高，但是用户没有行为，那就可能是真的不喜欢。











































