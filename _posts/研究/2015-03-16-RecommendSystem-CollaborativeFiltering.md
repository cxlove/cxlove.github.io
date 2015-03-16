---
layout: post
title : 推荐系统(1)--协同过滤
description : Recommend System(1)--Collaborative Filtering
category : 研究
tags : RecommendSystem study-note Python
keywords : 
---

# 推荐系统(Recommend System)

## 什么是RS

推荐系统顾名思义就是向用户推荐东西的系统。

推荐系统无所不在，如电子商务平台，广告推送，门户网站，新闻平台等等。

而推荐系统兴起的重要原因便是信息过载，互联网上的信息过多，导致用户很难在较短的时间内浏览所有的内容，每天都有新的音乐，新的电影，新的图书上架，每天都有数以万计，甚至更多的新闻。所谓的推荐系统所承担的角色便是个“专家”，分析每个人不同的兴趣，爱好，预测每个人可能感兴趣的内容，以此进行推荐。

## 应用

1.  电子商务，如淘宝推荐商品等。
2.  社交网络，如Facebook推荐好友等。
3.  电影、音乐、图书网站等，如果Youtube推荐视频等。
4.  搜索引擎，根据每个人不同兴趣爱好，对搜索结果不同的排序。
5.  个性化阅读推荐。
6.  等等

## 评价
1.  满意度，算是个很直观的评价，意味着客户直接对推荐评价，比如说Facebook根据个人社交网络推荐好友，如果选择添加，意味着客户和所推荐个确实可能存在某种联系，属于推荐成功等。
2.  准确度，不同环境有不同的定义，如评分预测中可能通过方根误差衡量，而在推荐中可能是召回率或者准确率。
3.  覆盖率，同时需要很高的覆盖率，推荐不能只集中在少量的热门产品。
4.  流行度，某些经典电影可能每个人都愿意去看，也存在一些推荐流行度非常高的产品。
5.  新颖性，冷门产品可能给用户带来更多的新颖性，如某些感兴趣艺人的不知名作品。
6.  惊喜度，和新颖性类似，又不完全相同，新颖性可能还是兴趣相关，而惊喜度往往是一个完全崭新的领域，同时这种推荐看上去可能会有风险。
7.  实时性，如新闻，不能推送很久以前，即使用户再多感兴趣。
8.  等等

# 基于领域的算法

## 评价指标

1.  召回率

	假设给用户u推荐的N个物品为Recommend(u)，而用户u在测试集上喜欢的用户集合为Test(u)，则召回率为：
	
	<a href="http://www.codecogs.com/eqnedit.php?latex=Recall&space;=&space;\frac{\sum\limits_u{|Recommend(u)\cap&space;Test(u))|}}{\sum\limits_u{Test(u)}}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Recall&space;=&space;\frac{\sum\limits_u{|Recommend(u)\cap&space;Test(u))|}}{\sum\limits_u{Test(u)}}" title="Recall = \frac{\sum_u{|Recommend(u)\cap Test(u))|}}{\sum_u{Test(u)}}" /></a>

2.  准确率

	<a href="http://www.codecogs.com/eqnedit.php?latex=Precision&space;=&space;\frac{\sum\limits_u{|Recommend(u)\cap&space;Test(u))|}}{\sum\limits_u{Recommend&space;(u)}}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Precision&space;=&space;\frac{\sum\limits_u{|Recommend(u)\cap&space;Test(u))|}}{\sum\limits_u{Recommend&space;(u)}}" title="Precision = \frac{\sum\limits_u{|Recommend(u)\cap Test(u))|}}{\sum\limits_u{Recommend (u)}}" /></a>

3.  覆盖率

      <a href="http://www.codecogs.com/eqnedit.php?latex=Coverage&space;=&space;\frac{|\cup_{u\in&space;U}&space;Recommend(u)|}{|Item|}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Coverage&space;=&space;\frac{|\cup_{u\in&space;U}&space;Recommend(u)|}{|Item|}" title="Coverage = \frac{|\cup_{u\in U} Recommend(u)|}{|Item|}" /></a>

4.  流行度

	popularity(u)表示物体u的流行度，即有多少用户喜欢/选择u。
	
	<a href="http://www.codecogs.com/eqnedit.php?latex=Popularity&space;=&space;\frac{|\sum\limits_{u\in&space;Choose}\log&space;{(1&space;&plus;&space;popularity(u))}|}{|Choose|}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Popularity&space;=&space;\frac{|\sum\limits_{u\in&space;Choose}\log&space;{(1&space;&plus;&space;popularity(u))}|}{|Choose|}" title="Popularity = \frac{|\sum\limits_{u\in Choose}\log {(1 + popularity(u))}|}{|Choose|}" /></a>

## 基于用户的协同过滤算法(UserCF)

### 基础思路

如果你需要一些专业技术书籍的时候，必然会优先选择同专业，同研究方向的人进行推荐。这是因为你们之间有相同的共同的研究领域和兴趣。

那么在推荐系统中一个常用的算法便是将用户按兴趣爱好进行聚类，对需要推荐的用户，总是找到和他兴趣爱好很相近的其它用户，而将其它用户所感兴趣的物品推荐给此用户。

而仅基于用户行为数据设计的推荐算法称之为协同过滤算法。

### 用户相似度

令N(u)表示用户u曾经喜欢/选择过的物体集合，我们认为是正向反馈，而用M(u)表示曾经喜欢/选择过物体u的用户集合。

而用户相似度计算包括了著名的Jaccard公式，计算u和v的相似度。

<a href="http://www.codecogs.com/eqnedit.php?latex=Similarity&space;(u&space;,&space;v)&space;=&space;\frac{|N(u)&space;\cap&space;N(v)|}{|N(u)&space;\cup&space;N(v)|}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Similarity&space;(u&space;,&space;v)&space;=&space;\frac{|N(u)&space;\cap&space;N(v)|}{|N(u)&space;\cup&space;N(v)|}" title="Similarity (u , v) = \frac{|N(u) \cap N(v)|}{|N(u) \cup N(v)|}" /></a>

也有余弦相似度计算公式 ：

<a href="http://www.codecogs.com/eqnedit.php?latex=Similarity&space;(u&space;,&space;v)&space;=&space;\frac{|N(u)&space;\cap&space;N(v)|}{\sqrt{|N(u)|&space;*&space;|N(v)|}}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Similarity&space;(u&space;,&space;v)&space;=&space;\frac{|N(u)&space;\cap&space;N(v)|}{\sqrt{|N(u)|&space;*&space;|N(v)|}}" title="Similarity (u , v) = \frac{|N(u) \cap N(v)|}{\sqrt{|N(u)| * |N(v)|}}" /></a>

而在实际过程中可以发现，有些物品，流行程度过高，而影响到计算。应该改变其中的权值，比如说两个人同时购买了《十万个为什么》和两个人同时购买了《Hadoop权威指南》所包含的意义是完全不一样的。前者流行程度很高，可能很多家庭都有购买，而后者相对整个市场是冷门物体，而同时购买后者的两个人更有可能有相同的兴趣爱好，所以可以用log函数平滑之后取倒数，对热门产品，权值低，而对于冷门产品，权值反而高。所以John S.Breese在1998提出以下公式 ：

<a href="http://www.codecogs.com/eqnedit.php?latex=Similarity&space;(u&space;,&space;v)&space;=&space;\frac&space;{\sum\limits_{i&space;\in&space;(N(u)&space;\cap&space;N(v))}\frac{1}{\log{(1&plus;|M(i)|)}}}{\sqrt{|N(u))|*|N(v))|}}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Similarity&space;(u&space;,&space;v)&space;=&space;\frac&space;{\sum\limits_{i&space;\in&space;(N(u)&space;\cap&space;N(v))}\frac{1}{\log{(1&plus;|M(i)|)}}}{\sqrt{|N(u))|*|N(v))|}}" title="Similarity (u , v) = \frac {\sum\limits_{i \in (N(u) \cap N(v))}\frac{1}{\log{(1+|M(i)|)}}}{\sqrt{|N(u))|*|N(v))|}}" /></a>

**PS : 很多时候，在实际实践的过程中，可能需要建立物体与用户的倒排索引，依具体情况，数据规律而定**。

### 主过程

对于所需要推荐的用户u，考虑与其相似度最高的k个用户，如果用S(u , k)表示和u相似的k个用户集合，sim(u,v)表示u和v的相似程度，那么用户u对物品i的兴趣程度为：

<a href="http://www.codecogs.com/eqnedit.php?latex=Score&space;(u&space;,&space;i)&space;=&space;\sum\limits_{v\in&space;(M(i)\cap&space;S(u,k))}(sim(u,v)&space;*&space;Score&space;(v&space;,&space;i))" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Score&space;(u&space;,&space;i)&space;=&space;\sum\limits_{v\in&space;(M(i)\cap&space;S(u,k))}(sim(u,v)&space;*&space;Score&space;(v&space;,&space;i))" title="Score (u , i) = \sum\limits_{v\in (M(i)\cap S(u,k))}(sim(u,v) * Score (v , i))" /></a>

其中Score(u,i)表示用户u对i的感兴趣程度，如果是是否会购买之类的，可能权值就是0/1，如果是评分系统，那就是分值。

### 实验结果

我们对MoviesLens的small数据集进行实验，对于不同的K，N，实验结果如下：

![result](/images/RS1_1.png)

### 代码

[代码君在这里](https://github.com/cxlove/RecommendSystem/tree/master/src/UserCF)

## 基于物品的协同过滤算法(ItemCF)

### 基础思路

如果你曾经购买过《具体数学》，那么可能对《组合数学》感兴趣，因为这两本书很相近，都和数学相关，也同时和计算机相关。

如果你曾经观看过《失恋三十三天》，《不二神探》，那么你可能会对《西游降魔记》感兴趣，因为他们的主演都是文章。

那么在推荐系统中一个常用的算法便是分析用户曾经感兴趣的物品，进而推荐和这些物品相似度很高的物品。

### 用户相似度

令M(u)表示用户u曾经喜欢/选择过的物体集合，我们认为是正向反馈，而用N(u)表示曾经喜欢/选择过物体u的用户集合。

而用户相似度计算包括了著名的Jaccard公式，计算u和v的相似度。

<a href="http://www.codecogs.com/eqnedit.php?latex=Similarity&space;(u&space;,&space;v)&space;=&space;\frac{|N(u)&space;\cap&space;N(v)|}{|N(u)&space;\cup&space;N(v)|}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Similarity&space;(u&space;,&space;v)&space;=&space;\frac{|N(u)&space;\cap&space;N(v)|}{|N(u)&space;\cup&space;N(v)|}" title="Similarity (u , v) = \frac{|N(u) \cap N(v)|}{|N(u) \cup N(v)|}" /></a>

也有余弦相似度计算公式 ：

<a href="http://www.codecogs.com/eqnedit.php?latex=Similarity&space;(u&space;,&space;v)&space;=&space;\frac{|N(u)&space;\cap&space;N(v)|}{\sqrt{|N(u)|&space;*&space;|N(v)|}}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Similarity&space;(u&space;,&space;v)&space;=&space;\frac{|N(u)&space;\cap&space;N(v)|}{\sqrt{|N(u)|&space;*&space;|N(v)|}}" title="Similarity (u , v) = \frac{|N(u) \cap N(v)|}{\sqrt{|N(u)| * |N(v)|}}" /></a>

而在实际过程中可以发现，每个物品都有很多消费者，那是否每个用户的权重一样。其实不然，比如说图书销售商，可能所有书都采购过，而可能参考价值很小。类似UserCF中，所以John S.Breese在1998提出以下公式 ：

<a href="http://www.codecogs.com/eqnedit.php?latex=Similarity&space;(u&space;,&space;v)&space;=&space;\frac&space;{\sum\limits_{i&space;\in&space;(N(u)&space;\cap&space;N(v))}\frac{1}{\log{(1&plus;|M(i)|)}}}{\sqrt{|N(u))|*|N(v))|}}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Similarity&space;(u&space;,&space;v)&space;=&space;\frac&space;{\sum\limits_{i&space;\in&space;(N(u)&space;\cap&space;N(v))}\frac{1}{\log{(1&plus;|M(i)|)}}}{\sqrt{|N(u))|*|N(v))|}}" title="Similarity (u , v) = \frac {\sum\limits_{i \in (N(u) \cap N(v))}\frac{1}{\log{(1+|M(i)|)}}}{\sqrt{|N(u))|*|N(v))|}}" /></a>

### 主过程

对于所需要推荐的用户u，考虑与其喜欢的物品集合相似度很高的物体集合，如果用S(u , k)表示和物品u相似的k个用户集合，sim(u,v)表示u和v的相似程度，那么用户user对物品v的兴趣程度为：

<a href="http://www.codecogs.com/eqnedit.php?latex=Score&space;(u&space;,&space;i)&space;=&space;\sum\limits_{v\in&space;(M(u)\cap&space;S(i,k))}(sim(i,v)&space;*&space;Score&space;(u&space;,&space;v))" target="_blank"><img src="http://latex.codecogs.com/gif.latex?Score&space;(u&space;,&space;i)&space;=&space;\sum\limits_{v\in&space;(M(u)\cap&space;S(i,k))}(sim(i,v)&space;*&space;Score&space;(u&space;,&space;v))" title="Score (u , i) = \sum\limits_{v\in (M(u)\cap S(i,k))}(sim(i,v) * Score (u , v))" /></a>

其中Score(u,i)表示用户u对i的感兴趣程度，如果是是否会购买之类的，可能权值就是0/1，如果是评分系统，那就是分值。

### 实验结果

我们对MoviesLens的small数据集进行实验，对于不同的K，N，实验结果如下：

![result](/images/RS1_2.png)

### 代码

[代码君在这里](https://github.com/cxlove/RecommendSystem/tree/master/src/ItemCF)


## UserCF与ItemCF的对比

从结果中可以发现，N越大，推荐的越多，召回率提高，准确率降低，平均流行度降低，覆盖率提高。K越大，召回率提高，准确率提高，流行度提高，覆盖率降低。当然了在一定范围之内 的变化。

可以看出N＝20，K＝5左右，各项性能综合情况较好。

同时也可以发现ItemCF相对UserCF有一点点优势。

在性能效率方面，UserCF适用于用户较少的情况，ItemCF适用于物品个数较少的情况，否则相似矩阵的代价可能较大。而在本文测试所用数据集上，ItemCF耗时远大于UserCF，正是因为物品数量是几倍于用户数。

在领域方面，UserCF更能体现社会整体性，按群体的热门物品推荐，ItemCF更能体现个性化，着重考虑个性，兴趣的传承。

在实时性上，一旦用户有新的行为，对于UserCF影响不大，用户之间的相似度不会有过大变化，而对于ItemCF而言，通过新的物体，可能就会有新的推荐选项。

在推荐理由上，UserCF无法很直观的表达，所推荐的物品受多个相似用户影响，而ItemCF可以较为直观表现，因为你曾经购买了A,B,C，而D又与A,B,C十分相近，所以推荐了D。































