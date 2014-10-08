---
layout: post
title : GitHub上搭建blog的一些注意事项
category : 技术
tags : Disqus  LaTeX
keywords : 
description : 自己在GitHub上搭建blog的过程中，得到的一些需要注意的地方。
---



## 如何让Markdown语法支持LaTeX

　　作为工科屌丝，编辑公式似乎是必不可少的技能，而Markdown本身是不支持LaTeX的，总是插入图片似乎不是一件炫酷的事情。

　　Mathjax的存在似乎可以很好的解决这个问题，Mathjax提供了很优秀的方案能够帮助解决在主流浏览器上显示数学公式的问题。而在Jekyll写博文的时候，只需要在开头加上下面这段javascript代码就行：

		<script type="text/javascript"
			src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
		</script>

　　那么Jekyll里面，只需要在_posts下相应的模板加上即可，比如我是用_posts下的post.html作为发布博文的模板。

　　以下用作LaTeX测试。
　　

　　LaTeX代码如下:

		$$ N(x;u;\Sigma) = \frac{1}{\sqrt{2\pi \| \Sigma \|}} \exp[-\frac{1}{2}(x-u)^T\Sigma^{-1} (x-u)]$$

　　那么实际效果如下：<a href="http://www.codecogs.com/eqnedit.php?latex=$$&space;N(x;u;\Sigma)&space;=&space;\frac{1}{\sqrt{2\pi&space;\|&space;\Sigma&space;\|}}&space;\exp[-\frac{1}{2}(x-u)^T\Sigma^{-1}&space;(x-u)]$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$&space;N(x;u;\Sigma)&space;=&space;\frac{1}{\sqrt{2\pi&space;\|&space;\Sigma&space;\|}}&space;\exp[-\frac{1}{2}(x-u)^T\Sigma^{-1}&space;(x-u)]$$" title="$$ N(x;u;\Sigma) = \frac{1}{\sqrt{2\pi \| \Sigma \|}} \exp[-\frac{1}{2}(x-u)^T\Sigma^{-1} (x-u)]$$" /></a>

## 如何在博客上添加评论功能

　　Jekyll本身没有评论功能，所以我们需要引用第三方平方，比如说Disqus，使用十分简单。

1.  首先在Disqus上注册帐号。
2.  然后选择`Add Disqus to Your Site`。添加博客信息。
3.  同样是在相应的Jekyll发布博文的模板中，添加上Disqus官网上提供的代码。
4.  如果Verify的时候失败，可以进入`Setting->General`里面的信息是否正确，尤其是博客的URL。

　　还是十分容易操作的，欢迎大家评论。  