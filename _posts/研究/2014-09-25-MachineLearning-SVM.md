---
layout: post
title : MachineLearingѧϰ�ʼ�(5)--SVM
description : MachineLearingѧϰ�ʼ�(5)--SVM
category : �о�
tags : MachineLearing study-note Python
---

#SVM���Ƶ�����

## ���Կɷֵ�SVM��Ӳ������

�������һ�������ռ��ϵ�ѵ�����ݼ�<a href="http://www.codecogs.com/eqnedit.php?latex=$$T&space;=&space;\{(x_1&space;,&space;y_1)&space;,&space;(x_2&space;,&space;y_2)&space;\dots&space;,&space;(x_n&space;,&space;y_n)&space;\}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$T&space;=&space;\{(x_1&space;,&space;y_1)&space;,&space;(x_2&space;,&space;y_2)&space;\dots&space;,&space;(x_n&space;,&space;y_n)&space;\}$$" title="$$T = \{(x_1 , y_1) , (x_2 , y_2) \dots , (x_n , y_n) \}$$" /></a>

����<a href="http://www.codecogs.com/eqnedit.php?latex=$$x_i&space;\in&space;R^n&space;,&space;y_i&space;\in&space;\{&plus;1&space;,&space;-1\}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$x_i&space;\in&space;R^n&space;,&space;y_i&space;\in&space;\{&plus;1&space;,&space;-1\}$$" title="$$x_i \in R^n , y_i \in \{+1 , -1\}$$" /></a>��<a href="http://www.codecogs.com/eqnedit.php?latex=$$x_i$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$x_i$$" title="$$x_i$$" /></a>�ǵ�i��������...(line truncated)...

����һ����ֵ�������������ͨ��һ�����Ժ����ֳ������ռ䣬���������ռ��ֱַ����������ĵ���ȫ��Ӧ����������Կɷֵġ�<del>��ʵ��׼������ǣ����ŷʽ�ռ��ϣ�����ؿռ䡣</del>

### ���Կɷ�SVM

��������֮ǰ��֪ʶ��������Ҫ��Ƴ�һ�����Ժ������õ�һ�����볬ƽ�棬�Դﵽ��ֵ�����Ч����

<a href="http://www.codecogs.com/eqnedit.php?latex=$$w^T&space;*&space;x&space;&plus;&space;b&space;=&space;0$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$w^T&space;*&space;x&space;&plus;&space;b&space;=&space;0$$" title="$$w^T * x + b = 0$$" /></a>

�Լ��õ���Ӧ�ľ��ߺ���

<a href="http://www.codecogs.com/eqnedit.php?latex=$$f(x)&space;=&space;sign&space;(w^T&space;*&space;x&space;&plus;&space;b)$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$f(x)&space;=&space;sign&space;(w^T&space;*&space;x&space;&plus;&space;b)$$" title="$$f(x) = sign (w^T * x + b)$$" /></a>

����sign()���ǵõ���Ӧ�������ţ�logistic������0.5��Ϊ�ֽ�ֵ����SVM�У�������һ��ƽ����Ϊ�ֽ磬��ά�б���һ��������һ��ֱ�ߡ�ֱ�ߵ������������������ϱ��Ϊ���Կɷ�֧����������

### ��������뼸�μ��

��֮ǰ�ķ����У�����ֻ��׷���ڷ������ȷ�����⣬ϣ���õ���cost function���ߴ����ʾ����ܵ�С����Logistic�ع��У����Ǳ�Ȼ���Եõ�����⣬����Щ����ڷ�����ȷ�ʶ�����ͬ�ģ���֮ǰ���㷨���ǲ�������Щ�ġ�

����SVM�У��������ĸ������Ҫ��֤����ȷ�ط��������������ݣ���ϣ��ȷ�ԶȾ����ܵĸߡ���νȷ�Ŷȱ���ָһ���㵽����ƽ���Զ�����Ա�ʾ����Ԥ���ȷ�Ŷȡ��ܺ���⣬�����Է���ƽ��Ϊ�ֽ�㣬һ��Ϊ������һ��Ϊ������������ǿ��ܳ����ھ������ƽ��ܽ��ĵ㣬����Щ���ȷ�ŶȱȽ�С��

<strong>������� : </strong>

���ڷ���ƽ��<a href="http://www.codecogs.com/eqnedit.php?latex=$$w^T&space;*&space;x&space;&plus;&space;b&space;=&space;0$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$w^T&space;*&space;x&space;&plus;&space;b&space;=&space;0$$" title="$$w^T * x + b = 0$$" /></a>ȷ��������£�������Ϊ<a href="http://www.codecogs.com/eqnedit.php?latex=$$|w^T&space;*&space;x&space;&plus;&space;b|$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$|w^T&space;*&space;x&space;&plus;&space;b|$$" title="$$|w^T *...(line truncated)...

������ƽ��(w , b)�������������ĵĺ������Ϊ������������ĺ����������Сֵ������<a href="http://www.codecogs.com/eqnedit.php?latex=$$\gamma&space;=&space;\min\limits_{i=1,2,\dots&space;n}\hat{\gamma}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\gamma&space;=&space;\min\limits_{i=1,2,\dots&space;n}\hat{\gamma}$$" title="$$\gamma = \min\limits_{i=1,2,\dots n}\hat{\gamma}$$" /></a>

**���μ�� :**

���μ��������ֱ����㵽��/�ߵľ��룬��:<a href="http://www.codecogs.com/eqnedit.php?latex=$$\gamma_i&space;=&space;|\frac{w^T&space;*&space;x&space;&plus;&space;b}{||w||}|$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\gamma_i&space;=&space;|\frac{w^T&space;*&space;x&space;&plus;&space;b}{||w||}|$$" title="$$\gamma_i = |\frac{w^T * x + b}{||w||}|$$" /></a>��

ͬ���ľ���ֵ���ô������ҷ���||w|| = 1��ʱ����������ڼ��μ��������ƽ��������������ļ��μ���������£�<a href="http://www.codecogs.com/eqnedit.php?latex=$$\gamma&space;=&space;\frac{\hat{\gamma}}{||w||}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\gamma&space;=&space;\frac{\hat{\gamma}}{||w||}$$" title="$$\gamma = \frac{\hat{\gamma}}{||w||}$$" /></a>

### ������

����֮ǰ˵��֧������������Ϊ�˵õ�һ������ƽ�棬ʹ�ü����󻯡����Զ�������Լ�����Ż����⣺

![Equal](/images/ML5_3.png)

���Ƿ��ֽ�w��b����������||w||����Ӧ�������ӣ���<a href="http://www.codecogs.com/eqnedit.php?latex=$$\hat{\gamma}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\hat{\gamma}$$" title="$$\hat{\gamma}$$" /></a>Ҳͬ�����������󣬶Խ��û��Ӱ�죬������������<a href="http://www.codecogs.com/eqnedit.php?latex=$$\hat{\gamma}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$\hat{\gamma}$$" title="$$\hat{\gamma}$$" /></a>��Լ��Ӱ�죬�������1��������Է������<a href="http://www.codecogs.com/eqnedit.php?latex=$$\frac{1}{||w||}$$" target="...(line truncated)...

<a href="http://www.codecogs.com/eqnedit.php?latex=\min\limits_{w,b}&space;\frac{||w||^2}{2}$$&space;\\&space;\\&space;$$s.t&space;:&space;y_i&space;*&space;(w^T&space;*&space;x_i&space;&plus;&space;b)&space;\geq&space;1" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\min\limits_{w,b}&space;\frac{||w||^2}{2}$$&space;\\&space;\\&space;$$s.t&space;:&space;y_i&space;*&space;(w^T&space;*&space;x_i&space;&plus;&space;b)&space;\geq&space;1" title="\min\limits_{w,b} \frac{||w||^2}{2}$$ \\ \\ $$s.t ...(line truncated)...

����һ����Լ����͹�Ż����⣬�ں������ǻ����ʹ���������ճ��ӷ���������������Ż����⡣

### ���Կɷ�SVMѧϰ�㷨-�����󻯷�

1. ���첢���Լ�����Ż����⣬��õ����Ž�(w , b)��
2. �õ�����ƽ��<a href="http://www.codecogs.com/eqnedit.php?latex=$$w^T*x&space;&plus;&space;b&space;=&space;0$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$w^T*x&space;&plus;&space;b&space;=&space;0$$" title="$$w^T*x + b = 0$$" /></a>�Լ�������ߺ���<a href="http://www.codecogs.com/eqnedit.php?latex=$$f(x)&space;=&space;sign&space;(w^T&space;*&space;x&space;&plus;&space;b)$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$f(x)&space;=&space;sign&space;(w^T&space;*&space;x&space;&plu...(line truncated)...

### �������ն�ż��������Ż�

�����������ճ��ӣ������������պ�����

<a href="http://www.codecogs.com/eqnedit.php?latex=$$L(w&space;,&space;b&space;,&space;\alpha)&space;=&space;\frac{||w||^2}{2}&space;-&space;\sum\limits_{i=1}^N\alpha_iy_i(w^T&space;*&space;x_i&space;&plus;&space;b)&space;&plus;&space;\sum\limits_{i=1}^N\alpha_i��$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$L(w&space;,&space;b&space;,&space;\alpha)&space;=&space;\frac{||w||^2}{2}&space;-&space;\sum\limits_{i=1}^N\alpha_iy_i(w^T&space;*&space;x_i&space;&plus;&space;b)&space;&plus;&space...(line truncated)...

����<a href="http://www.codecogs.com/eqnedit.php?latex=(\alpha_1&space;,&space;\alpha_2&space;,&space;\dots&space;,&space;\alpha_N)&space;^&space;T" target="_blank"><img src="http://latex.codecogs.com/gif.latex?(\alpha_1&space;,&space;\alpha_2&space;,&space;\dots&space;,&space;\alpha_N)&space;^&space;T" title="(\alpha_1 , \alpha_2 , \dots , \alpha_N) ^ T" /></a>��Ϊ�������ճ���������

�����������ն�ż���⣬������Ҫ������<a href="http://www.codecogs.com/eqnedit.php?latex=\max\limits_\alpha\min\limits_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\max\limits_\alpha\min\limits_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" title="\max\limits_\alpha\min\limits_{w,b}L(\alpha , w , b)" /></a>����������Ҫ��������������С���⡣

(1).  ����<a href="http://www.codecogs.com/eqnedit.php?latex=\min\limits_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\min\limits_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" title="\min\limits_{w,b}L(\alpha , w , b)" /></a>����⣺

�����w,b��ƫ��Ϊ0��Ȼ��ֱ���⣺

<a href="http://www.codecogs.com/eqnedit.php?latex=\frac{\partial&space;L(\alpha&space;,&space;w&space;,&space;b))}{\partial&space;w}&space;=&space;w&space;-&space;\sum\limits_{i=1}^N\alpha_iy_ix_i&space;=&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\frac{\partial&space;L(\alpha&space;,&space;w&space;,&space;b))}{\partial&space;w}&space;=&space;w&space;-&space;\sum\limits_{i=1}^N\alpha_iy_ix_i&space;=&space;0" title="\frac{\partial L(\alpha , w , b))}{\partial w} = w - \sum\limits...(line truncated)...

<a href="http://www.codecogs.com/eqnedit.php?latex=\frac{\partial&space;L(\alpha&space;,&space;w&space;,&space;b))}{\partial&space;b}&space;=&space;-&space;\sum\limits_{i=1}^N\alpha_iy_i&space;=&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\frac{\partial&space;L(\alpha&space;,&space;w&space;,&space;b))}{\partial&space;b}&space;=&space;-&space;\sum\limits_{i=1}^N\alpha_iy_i&space;=&space;0" title="\frac{\partial L(\alpha , w , b))}{\partial b} = - \sum\limits_{i=1}^N\alpha_iy_i = 0"...(line truncated)...

Ȼ��

<a href="http://www.codecogs.com/eqnedit.php?latex=w&space;=&space;\sum\limits_{i=1}^N\alpha_iy_i" target="_blank"><img src="http://latex.codecogs.com/gif.latex?w&space;=&space;\sum\limits_{i=1}^N\alpha_iy_i" title="w = \sum\limits_{i=1}^N\alpha_iy_i" /></a>

<a href="http://www.codecogs.com/eqnedit.php?latex=\sum\limits_{i=1}^N\alpha_iy_i&space;=&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\sum\limits_{i=1}^N\alpha_iy_i&space;=&space;0" title="\sum\limits_{i=1}^N\alpha_iy_i = 0" /></a>

���뵽֮ǰ��ʽ���еõ���

![Result](/images/ML5_1.png)

���е�<a href="http://www.codecogs.com/eqnedit.php?latex=(x_i*y_i)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?(x_i*y_i)" title="(x_i*y_i)" /></a>�������������ڻ���

**ps:����Latex��֧�ֺܲ��Ѻá�����֮ǰʹ��maxjax���о�markdown�����֧��Ҳ������������ֻ�������߹�ʽ�༭��ת��html����(��ʵ����һ��ͼƬ)�����ֶ��й�ʽֻ����latexд�꣬��ͼ�ˡ�**

(2)��<a href="http://www.codecogs.com/eqnedit.php?latex=\max_\alpha\min_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\max_\alpha\min_{w,b}L(\alpha&space;,&space;w&space;,&space;b)" title="\max_\alpha\min_{w,b}L(\alpha , w , b)" /></a>

����
<a href="http://www.codecogs.com/eqnedit.php?latex=\max_\alpha\min_{w,b}L(\alpha&space;,&space;w&space;,&space;b)=\max_\alpha(-\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)&plus;\sum_{i=1}^N\alpha_i)=\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\max_\alpha\min_{w,b}L(\alpha&space;,&space;w&space;,&space;b)=\max_\alpha(-\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_j...(line truncated)...

�����������Ż�����ת���ɶ�ż���⣺

<a href="http://www.codecogs.com/eqnedit.php?latex=\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)&space;\\&space;st.&space;\sum_{i=1}^N\alpha_iy_i=0&space;\\&space;\alpha_i&space;\geq&space;0&space;,&space;i&space;=&space;1&space;,&space;2&space;,&space;\dots&space;,&space;N" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)&space;\\&space;st....(line truncated)...

���Եõ����Ž�<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" title="\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" /></a>�����ǵ�����Ŀ����w��b��

����KKT������
![Process](/images/ML5_2.png)

���Խ��w�����Ž⣺

<a href="http://www.codecogs.com/eqnedit.php?latex=w^*&space;=&space;\sum_{i=1}^N\alpha_i^*y_ix_i" target="_blank"><img src="http://latex.codecogs.com/gif.latex?w^*&space;=&space;\sum_{i=1}^N\alpha_i^*y_ix_i" title="w^* = \sum_{i=1}^N\alpha_i^*y_ix_i" /></a>

����������һ��<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha_j&space;>&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha_j&space;>&space;0" title="\alpha_j > 0" /></a>�������÷�֤����һ�¡�

���������ʽ�ӿ��Եõ���
<a href="http://www.codecogs.com/eqnedit.php?latex=y_j(w^**x_j&plus;b^*)-1=0&space;\rightarrow&space;b^*&space;=&space;y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?y_j(w^**x_j&plus;b^*)-1=0&space;\rightarrow&space;b^*&space;=&space;y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" title="y_j(w^**x_j+b^*)-1=0 \rightarrow b^* = y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" /></a>

����<a href="http://www.codecogs.com/eqnedit.php?latex=y_j&space;\in&space;\{1&space;,&space;-1\}&space;\rightarrow&space;y_j^2=&space;1" target="_blank"><img src="http://latex.codecogs.com/gif.latex?y_j&space;\in&space;\{1&space;,&space;-1\}&space;\rightarrow&space;y_j^2=&space;1" title="y_j \in \{1 , -1\} \rightarrow y_j^2= 1" /></a>

�������Ǳ�õ������Ž⡣

### ���Կɷ�֧��������ѧϰ�㷨
(1)  ���첢������Ż�����

<a href="http://www.codecogs.com/eqnedit.php?latex=\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)&space;\\&space;st.&space;\sum_{i=1}^N\alpha_iy_i=0&space;\\&space;\alpha_i&space;\geq&space;0&space;,&space;i&space;=&space;1&space;,&space;2&space;,&space;\dots&space;,&space;N" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\min_\alpha(\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_i\alpha_jy_iy_j(x_i*x_j)-\sum_{i=1}^N\alpha_i)&space;\\&space;st....(line truncated)...

������Ž�<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" title="\alpha^*=(\alpha_1^*,\alpha_2^*,\dots,\alpha_N^*)^T" /></a>��

(2) ���� <a href="http://www.codecogs.com/eqnedit.php?latex=w^*&space;=&space;\sum_{i=1}^N\alpha_i^*y_ix_i" target="_blank"><img src="http://latex.codecogs.com/gif.latex?w^*&space;=&space;\sum_{i=1}^N\alpha_i^*y_ix_i" title="w^* = \sum_{i=1}^N\alpha_i^*y_ix_i" /></a>

��ѡ��ĳ��jʹ��<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha_j&space;>&space;0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha_j&space;>&space;0" title="\alpha_j > 0" /></a>������ 

<a href="http://www.codecogs.com/eqnedit.php?latex=b^*&space;=&space;y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?b^*&space;=&space;y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" title="b^* = y_j-\sum_{i=1}^N\alpha_i^*y_i(x_i*x_j)" /></a>

(3)���ǵõ�����ƽ��<a href="http://www.codecogs.com/eqnedit.php?latex=w^**x&plus;b^*=0" target="_blank"><img src="http://latex.codecogs.com/gif.latex?w^**x&plus;b^*=0" title="w^**x+b^*=0" /></a>

�����Եõ���Ӧ�ľ��ߺ�����Over!
