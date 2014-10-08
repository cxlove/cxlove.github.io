---
layout: post
title : MachineLearing学习笔记(3)--决策树
description : MachineLearing学习笔记(3)--决策树算法
category : 研究
keywords :
tags : MachineLearning study-note Python
---


>本文更多的关注的是ML算法的实践，理论上的研究可能偏少。 -- cxlove

# 决策树

### 简述
　　决策树，很好理解。就是建立一棵树，节点是个判断条件，根据不同的结果，一步步往下。最终叶子便是一个类别。

　　因此决策树是一种非常容易理解的分类器。可以理解成很多的条件判断，if语句。比如说如果这个人穿的是裙子，我们认为是女生，否则XXXXX。<del>真的是这个样子吗，也有可能是岛娘呢</del>

　　所以树的节点是个对象，分叉路径代表可能的属性值。

　　从数据产生决策树的机器学习技术叫做决策树学习, 通俗说就是决策树。

### 熵与信息增益
　　对于一种方案，必须有个量化的数据去衡量。

　　信息论中引入熵(Entropy)作为衡量标准，刻画了任意样例集的纯度。<a href="http://www.codecogs.com/eqnedit.php?latex=Entropy&space;=&space;-&space;\sum_{i&space;=&space;1}^{n}p(x_i)\log_{2}p(x_i)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Entropy&space;=&space;-&space;\sum_{i&space;=&space;1}^{n}p(x_i)\log_{2}p(x_i)" title="Entropy = - \sum_{i = 1}^{n}p(x_i)\log_{2}p(x_i)" /></a>，其中我们将样例分为n类，每类所占的比例为<a href="http://www.codecogs.com/eqnedit.php?latex=p(x_i)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?p(x_i)" title="p(x_i)" /></a>。

　　而进一步通过纯度差来表示信息增益(Information Gain)。<a href="http://www.codecogs.com/eqnedit.php?latex=\Delta&space;=&space;Entropy&space;(parent)&space;-&space;\sum_{j&space;=&space;1}^{k}{\frac{N(v_j)}{N}*Entropy(v_j)}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\Delta&space;=&space;Entropy&space;(parent)&space;-&space;\sum_{j&space;=&space;1}^{k}{\frac{N(v_j)}{N}*Entropy(v_j)}" title="\Delta = Entropy (parent) - \sum_{j = 1}^{k}{\frac{N(v_j)}{N}*Entropy(v_j)}" /></a>。

　　有了衡量标准之后，我们便是每次寻找信息增益最大的方案。

### ID3算法
　　接下来是如何构造决策树，这里使用的是ID3算法。

1.  遍历所有的分割方案，计算他们的信息增益
2.  选择最佳的方案，将数据集切割成多个子集。对于每个子集都递归构造
3.  递归结束的条件是，i)所有的数据都是同一个集合，2)没有其它有用的特征去分割，那么就进行投票选出所属集合。

### 特点
优点：

1.  复杂度不高，十分容易理解
2.  可以处理不相关特征数据

缺点：
1.  可能会产生过度匹配


# 实现

### 递归构造树
分为以下模块，详见代码中的decisionTree.py

1.  计算香农商(calcShannonEnt)
2.  将数据集根据某个条件抽取出子集(splitDataSet)
3.  枚举划分方式，选择最好的方式(chooseBestFeatureSplit)
4.  投票选出所属的类(majorityClass)
5.  开始递归建树，用dict嵌套保存树(buildTree)

### 用Matplotlib将决策树画出来
主要介绍的是一个方法annotate()，可以在两点之间画一个箭头。

然后text()方法，可以在某个位置添加文字注解。

注意画图的时候，不是固定坐标，而是通过树的深度和宽度动态计算出每个节点的坐标，这样比较和谐。

### 针对测试数据进行分类，测试效果
分类就比较简单了，从树根开始遍历，对于每个节点的判断，然后走向某个分支，直到到达某个叶子节点。

<strong>另类黑科技：pickle模板，可以把任意形式的data转化成一个序列，保存在txt中，这样建树之后就能存起来，每次检测的时候只需要读取文件，而不需要重新建树。</strong>

# 结果
进行了预测隐形眼镜类型的实验，相应的决策树如下：

![result](/images/ML3_1.png)

#代码君
[完整代码以及数据集前往Github](https://github.com/cxlove/MachineLearning/tree/master/decisionTree)

  