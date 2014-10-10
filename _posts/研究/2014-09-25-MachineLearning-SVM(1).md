---
layout: post
title : MachineLearing学习笔记(5)--SVM(1)
description : MachineLearing学习笔记(5)--SVM(1)
category : 研究
tags : MachineLearning study-note Python
keywords : 
---

#SVM的推导过程

## 线性可分的SVM与硬间隔最大化

假设给定一个特征空间上的训练数据集<a href="http://www.codecogs.com/eqnedit.php?latex=$$T&space;=&space;\{(x_1&space;,&space;y_1)&space;,&space;(x_2&space;,&space;y_2)&space;\dots&space;,&space;(x_n&space;,&space;y_n)&space;\}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$T&space;=&space;\{(x_1&space;,&space;y_1)&space;,&space;(x_2&space;,&space;y_2)&space;\dots&space;,&space;(x_n&space;,&space;y_n)&space;\}$$" title="$$T = \{(x_1 , y_1) , (x_2 , y_2) \dots , (x_n , y_n) \}$$" /></a>

其中<a href="http://www.codecogs.com/eqnedit.php?latex=$$x_i&space;\in&space;R^n&space;,&space;y_i&space;\in&space;\{&plus;1&space;,&space;-1\}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$x_i&space;\in&space;R^n&space;,&space;y_i&space;\in&space;\{&plus;1&space;,&space;-1\}$$" title="$$x_i \in R^n , y_i \in \{+1 , -1\}$$" /></a>。<a href="http://www.codecogs.com/eqnedit.php?latex=$$x_i$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$x_i$$" title="$$x_i$$" /></a>是第i个特征向量，而<a href="http://www.codecogs.com/eqnedit.php?latex=$$y_i$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$y_i$$" title="$$y_i$$" /></a>是所属类别，我们定义+1为正例，反之为-1。其实可以发现在logistic回归，我们是定义了{0 , 1}作为二值分类的标准，其实这些是等价的，定义成{+1 , -1}只是为了方便后面的统计。

考虑一个二值分类器，如果能通过一个纯性函数分成两个空间，而这两个空间又分别与两个类别的点完全对应，则称是线性可分的。<del>其实标准定义上牵扯到欧式空间和希尔伯特空间。</del>

### 线性可分SVM

根据我们之前的知识，我们需要设计出一个线性函数，得到一个分离超平面，以达到二值分类的效果。

<a href="http://www.codecogs.com/eqnedit.php?latex=$$w^T&space;*&space;x&space;&plus;&space;b&space;=&space;0$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$w^T&space;*&space;x&space;&plus;&space;b&space;=&space;0$$" title="$$w^T * x + b = 0$$" /></a>

以及得到相应的决策函数

<a href="http://www.codecogs.com/eqnedit.php?latex=$$f(x)&space;=&space;sign&space;(w^T&space;*&space;x&space;&plus;&space;b)$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$f(x)&space;=&space;sign&space;(w^T&space;*&space;x&space;&plus;&space;b)$$" title="$$f(x) = sign (w^T * x + b)$$" /></a>

其中sign()便是得到相应的正负号，logistic我们用0.5作为分界值。在SVM中，我们用一个平面作为分界，二维中便是一个向量，一条直线。直线的两侧便是两个类别。以上便称为线性可分支持向量机，

### 函数间隔与几何间隔

在之前的分类中，我们只是追求于分离的正确率问题，希望得到的cost function或者错误率尽可能的小。像Logistic回归中，我们必然可以得到多个解，而这些解对于分类正确率都是相同的，在之前的算法中是不在意这些的。

而在SVM中，引入间隔的概念，不仅要保证能正确地分离两个类别的数据，还希望确性度尽可能的高。所谓确信度便是指一个点到分离平面的远近可以表示分类预测的确信度。很好理解，我们以分离平面为分界点，一侧为正例，一侧为反例，误差总是可能出现在距离分离平面很近的点，而这些点的确信度比较小。

<strong>函数间隔 : </strong>

对于分离平面<a href="http://www.codecogs.com/eqnedit.php?latex=$$w^T&space;*&space;x&space;&plus;&space;b&space;=&space;0$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$w^T&space;*&space;x&space;&plus;&space;b&space;=&space;0$$" title="$$w^T * x + b = 0$$" /></a>确定的情况下，我们认为<a href="http://www.codecogs.com/eqnedit.php?latex=$$|w^T&space;*&space;x&space;&plus;&space;b|$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$|w^T&space;*&space;x&space;&plus;&space;b|$$" title="$$|w^T * x + b|$$" /></a>便是到分离平面的距离，由于绝对值不方便后面的运算，所以刚好利用正例为+1，反例为-1的特征，函数间隔定义为：<a href="http://www.codecogs.com/eqnedit.php?latex=$$\hat{\gamma}&space;=&space;y_i&space;*&space;(w^T&space;*&space;x&space;&plus;&space;b)$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\hat{\gamma}&space;=&space;y_i&space;*&space;(w^T&space;*&space;x&space;&plus;&space;b)$$" title="$$\hat{\gamma} = y_i * (w^T * x + b)$$" /></a>

而分离平面(w , b)对于所有样本的的函数间隔为对所有样例点的函数间隔的最小值，即：<a href="http://www.codecogs.com/eqnedit.php?latex=$$\gamma&space;=&space;\min\limits_{i=1,2,\dots&space;n}\hat{\gamma}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\gamma&space;=&space;\min\limits_{i=1,2,\dots&space;n}\hat{\gamma}$$" title="$$\gamma = \min\limits_{i=1,2,\dots n}\hat{\gamma}$$" /></a>

**几何间隔 :**

几何间隔，便是直接算点到面/线的距离，即:<a href="http://www.codecogs.com/eqnedit.php?latex=$$\gamma_i&space;=&space;|\frac{w^T&space;*&space;x&space;&plus;&space;b}{||w||}|$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\gamma_i&space;=&space;|\frac{w^T&space;*&space;x&space;&plus;&space;b}{||w||}|$$" title="$$\gamma_i = |\frac{w^T * x + b}{||w||}|$$" /></a>。

同样的绝对值不好处理，而且发现||w|| = 1的时候函数间隔等于几何间隔，分离平面对于所有样本的几何间隔定义如下：<a href="http://www.codecogs.com/eqnedit.php?latex=$$\gamma&space;=&space;\frac{\hat{\gamma}}{||w||}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\gamma&space;=&space;\frac{\hat{\gamma}}{||w||}$$" title="$$\gamma = \frac{\hat{\gamma}}{||w||}$$" /></a>

### 间隔最大化

我们之前说到支持向量机就是为了得到一个分离平面，使得间隔最大化。所以定义以下约束最优化问题：

![Equal](/images/ML5_3.png)

我们发现将w和b按比例扩大，||w||按相应比例增加，而<a href="http://www.codecogs.com/eqnedit.php?latex=$$\hat{\gamma}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\hat{\gamma}$$" title="$$\hat{\gamma}$$" /></a>也同样按比例扩大，对结果没有影响，所以我们消除<a href="http://www.codecogs.com/eqnedit.php?latex=$$\hat{\gamma}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\hat{\gamma}$$" title="$$\hat{\gamma}$$" /></a>的约束影响，令其等于1。另外可以发现最大化<a href="http://www.codecogs.com/eqnedit.php?latex=$$\frac{1}{||w||}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\frac{1}{||w||}$$" title="$$\frac{1}{||w||}$$" /></a>和最小化<a href="http://www.codecogs.com/eqnedit.php?latex=$$\frac{||w||^2}{2}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\frac{||w||^2}{2}$$" title="$$\frac{||w||^2}{2}$$" /></a>是等价的，所以约束最优化问题写成以下形式：

<a href="http://www.codecogs.com/eqnedit.php?latex=\min\limits_{w,b}&space;\frac{||w||^2}{2}$$&space;\\&space;\\&space;$$s.t&space;:&space;y_i&space;*&space;(w^T&space;*&space;x_i&space;&plus;&space;b)&space;\geq&space;1" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\min\limits_{w,b}&space;\frac{||w||^2}{2}$$&space;\\&space;\\&space;$$s.t&space;:&space;y_i&space;*&space;(w^T&space;*&space;x_i&space;&plus;&space;b)&space;\geq&space;1" title="\min\limits_{w,b} \frac{||w||^2}{2}$$ \\ \\ $$s.t : y_i * (w^T * x_i + b) \geq 1" /></a>

这是一个带约束的凸优化问题，在后面我们会介绍使用拉格朗日乘子法来解决这样的最优化问题。

### 线性可分SVM学习算法-间隔最大化法

1. 构造并求解约束最优化问题，求得到最优解(w , b)。
2. 得到分离平面<a href="http://www.codecogs.com/eqnedit.php?latex=$$w^T*x&space;&plus;&space;b&space;=&space;0$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$w^T*x&space;&plus;&space;b&space;=&space;0$$" title="$$w^T*x + b = 0$$" /></a>以及分类决策函数<a href="http://www.codecogs.com/eqnedit.php?latex=$$f(x)&space;=&space;sign&space;(w^T&space;*&space;x&space;&plus;&space;b)$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$f(x)&space;=&space;sign&space;(w^T&space;*&space;x&space;&plus;&space;b)$$" title="$$f(x) = sign (w^T * x + b)$$" /></a>。

### 拉格朗日对偶法求解最优化

引入拉格朗日乘子，定义拉格朗日函数：

<a href="http://www.codecogs.com/eqnedit.php?latex=$$L(w&space;,&space;b&space;,&space;\alpha)&space;=&space;\frac{||w||^2}{2}&space;-&space;\sum\limits_{i=1}^N\alpha_iy_i(w^T&space;*&space;x_i&space;&plus;&space;b)&space;&plus;&space;\sum\limits_{i=1}^N\alpha_i｝$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$L(w&space;,&space;b&space;,&space;\alpha)&space;=&space;\frac{||w||^2}{2}&space;-&space;\sum\limits_{i=1}^N\alpha_iy_i(w^T&space;*&space;x_i&space;&plus;&space;b)&space;&plus;&space;\sum\limits_{i=1}^N\alpha_i｝$$" title="$$L(w , b , \alpha) = \frac{||w||^2}{2} - \sum\limits_{i=1}^N\alpha_iy_i(w^T * x_i + b) + \sum\limits_{i=1}^N\alpha_i｝$$" /></a>

其中<a href="http://www.codecogs.com/eqnedit.php?latex=(\alpha_1&space;,&space;\alpha_2&space;,&space;\dots&space;,&space;\alpha_N)&space;^&space;T" target="_blank"><img src="http://latex.codecogs.com/gif.latex?(\alpha_1&space;,&space;\alpha_2&space;,&space;\dots&space;,&space;\alpha_N)&space;^&space;T" title="(\alpha_1 , \alpha_2 , \dots , \alpha_N) ^ T" /></a>称为拉格朗日乘子向量。

根据拉格朗日对偶问题，我们需要求解的是<a href="http://www.codecogs.com/eqnedit.php?latex=\max\limits_\alpha\min\limits_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\max\limits_\alpha\min\limits_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" title="\max\limits_\alpha\min\limits_{w,b}L(\alpha , w , b)" /></a>，所以我们要解决的是这个极大极小问题。

(1).  对于<a href="http://www.codecogs.com/eqnedit.php?latex=\min\limits_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\min\limits_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" title="\min\limits_{w,b}L(\alpha , w , b)" /></a>的求解：

令其对w,b的偏导为0，然后分别求解：

<a href="http://www.codecogs.com/eqnedit.php?latex=\frac{\partial&space;L(\alpha&space;,&space;w&space;,&space;b))}{\partial&space;w}&space;=&space;w&space;-&space;\sum\limits_{i=1}^N\alpha_iy_ix_i&space;=&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\frac{\partial&space;L(\alpha&space;,&space;w&space;,&space;b))}{\partial&space;w}&space;=&space;w&space;-&space;\sum\limits_{i=1}^N\alpha_iy_ix_i&space;=&space;0" title="\frac{\partial L(\alpha , w , b))}{\partial w} = w - \sum\limits_{i=1}^N\alpha_iy_ix_i = 0" /></a>

<a href="http://www.codecogs.com/eqnedit.php?latex=\frac{\partial&space;L(\alpha&space;,&space;w&space;,&space;b))}{\partial&space;b}&space;=&space;-&space;\sum\limits_{i=1}^N\alpha_iy_i&space;=&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\frac{\partial&space;L(\alpha&space;,&space;w&space;,&space;b))}{\partial&space;b}&space;=&space;-&space;\sum\limits_{i=1}^N\alpha_iy_i&space;=&space;0" title="\frac{\partial L(\alpha , w , b))}{\partial b} = - \sum\limits_{i=1}^N\alpha_iy_i = 0" /></a>

然后将

<a href="http://www.codecogs.com/eqnedit.php?latex=w&space;=&space;\sum\limits_{i=1}^N\alpha_iy_i" target="_blank"><img src="http://latex.codecogs.com/gif.latex?w&space;=&space;\sum\limits_{i=1}^N\alpha_iy_i" title="w = \sum\limits_{i=1}^N\alpha_iy_i" /></a>

<a href="http://www.codecogs.com/eqnedit.php?latex=\sum\limits_{i=1}^N\alpha_iy_i&space;=&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\sum\limits_{i=1}^N\alpha_iy_i&space;=&space;0" title="\sum\limits_{i=1}^N\alpha_iy_i = 0" /></a>

代入到之前的式子中得到：

![Result](/images/ML5_1.png)

其中的<a href="http://www.codecogs.com/eqnedit.php?latex=(x_i*y_i)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?(x_i*y_i)" title="(x_i*y_i)" /></a>是两个向量的内积。

**ps:对于Latex的支持很不友好。。。之前使用maxjax，感觉markdown对其的支持也不流畅，现在只能用在线公式编辑器转成html代码(其实就是一个图片)，这种多行公式只能用latex写完，截图了。**

(2)求<a href="http://www.codecogs.com/eqnedit.php?latex=\max_\alpha\min_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\max_\alpha\min_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" title="\max_\alpha\min_{w,b}L(\alpha , w , b)" /></a>

即：
<a href="http://www.codecogs.com/eqnedit.php?latex=\max_\alpha\min_{w,b}L(\alpha&space;,&space;w&space;,&space;b)=\max_\alpha(-\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)&plus;\sum_{i=1}^N\alpha_i)=\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\max_\alpha\min_{w,b}L(\alpha&space;,&space;w&space;,&space;b)=\max_\alpha(-\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)&plus;\sum_{i=1}^N\alpha_i)=\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)" title="\max_\alpha\min_{w,b}L(\alpha , w , b)=\max_\alpha(-\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)+\sum_{i=1}^N\alpha_i)=\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)" /></a>

所以整个最优化问题转换成对偶问题：

<a href="http://www.codecogs.com/eqnedit.php?latex=\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)&space;\\&space;st.&space;\sum_{i=1}^N\alpha_iy_i=0&space;\\&space;\alpha_i&space;\geq&space;0&space;,&space;i&space;=&space;1&space;,&space;2&space;,&space;\dots&space;,&space;N" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)&space;\\&space;st.&space;\sum_{i=1}^N\alpha_iy_i=0&space;\\&space;\alpha_i&space;\geq&space;0&space;,&space;i&space;=&space;1&space;,&space;2&space;,&space;\dots&space;,&space;N" title="\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i) \\ st. \sum_{i=1}^N\alpha_iy_i=0 \\ \alpha_i \geq 0 , i = 1 , 2 , \dots , N" /></a>

可以得到最优解<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" title="\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" /></a>，我们的最终目标是w和b。

根据KKT条件：
![Process](/images/ML5_2.png)

可以解出w的最优解：

<a href="http://www.codecogs.com/eqnedit.php?latex=w^*&space;=&space;\sum_{i=1}^N\alpha_i^*y_ix_i" target="_blank"><img src="http://latex.codecogs.com/gif.latex?w^*&space;=&space;\sum_{i=1}^N\alpha_i^*y_ix_i" title="w^* = \sum_{i=1}^N\alpha_i^*y_ix_i" /></a>

其中至少有一个<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha_j&space;>&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha_j&space;>&space;0" title="\alpha_j > 0" /></a>，可以用反证法推一下。

根据上面的式子可以得到：
<a href="http://www.codecogs.com/eqnedit.php?latex=y_j(w^**x_j&plus;b^*)-1=0&space;\rightarrow&space;b^*&space;=&space;y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?y_j(w^**x_j&plus;b^*)-1=0&space;\rightarrow&space;b^*&space;=&space;y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" title="y_j(w^**x_j+b^*)-1=0 \rightarrow b^* = y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" /></a>

其中<a href="http://www.codecogs.com/eqnedit.php?latex=y_j&space;\in&space;\{1&space;,&space;-1\}&space;\rightarrow&space;y_j^2=&space;1" target="_blank"><img src="http://latex.codecogs.com/gif.latex?y_j&space;\in&space;\{1&space;,&space;-1\}&space;\rightarrow&space;y_j^2=&space;1" title="y_j \in \{1 , -1\} \rightarrow y_j^2= 1" /></a>

至此我们便得到了最优解。

### 线性可分支持向量机学习算法
(1)  构造并求解最优化问题

<a href="http://www.codecogs.com/eqnedit.php?latex=\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)&space;\\&space;st.&space;\sum_{i=1}^N\alpha_iy_i=0&space;\\&space;\alpha_i&space;\geq&space;0&space;,&space;i&space;=&space;1&space;,&space;2&space;,&space;\dots&space;,&space;N" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)&space;\\&space;st.&space;\sum_{i=1}^N\alpha_iy_i=0&space;\\&space;\alpha_i&space;\geq&space;0&space;,&space;i&space;=&space;1&space;,&space;2&space;,&space;\dots&space;,&space;N" title="\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i) \\ st. \sum_{i=1}^N\alpha_iy_i=0 \\ \alpha_i \geq 0 , i = 1 , 2 , \dots , N" /></a>

求得最优解<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" title="\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" /></a>。

(2) 计算 <a href="http://www.codecogs.com/eqnedit.php?latex=w^*&space;=&space;\sum_{i=1}^N\alpha_i^*y_ix_i" target="_blank"><img src="http://latex.codecogs.com/gif.latex?w^*&space;=&space;\sum_{i=1}^N\alpha_i^*y_ix_i" title="w^* = \sum_{i=1}^N\alpha_i^*y_ix_i" /></a>

并选择某个j使得<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha_j&space;>&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha_j&space;>&space;0" title="\alpha_j > 0" /></a>，计算 

<a href="http://www.codecogs.com/eqnedit.php?latex=b^*&space;=&space;y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?b^*&space;=&space;y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" title="b^* = y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" /></a>

(3)我们得到分离平面<a href="http://www.codecogs.com/eqnedit.php?latex=w^**x&plus;b^*=0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?w^**x&plus;b^*=0" title="w^**x+b^*=0" /></a>

并可以得到相应的决策函数，Over!









