---
layout: post
title : Python学习笔记(2)--纯文本标记转换成简易html
description : Python实例(1)，即时标记，照着《Python基础教程》上的说明自己操作一遍。
category : 技术
tags : Python study-note
keywords : 
---

#Python实例(1)--即时标记

　　前两天了解些基础的Python基础语法之后，必须要真正实践一下，才能感受到Python带来的便捷和强大。

　　于是乎，今天抽空将《Python基础教程(第二版)》翻了翻，针对模块、类、继承、生成器等进一步了解了下，书的最后有一些实例，跟着实例说明一步步来实践一下。

## 要求

　　对于一段纯文本，如果想要将其转换成html代码，需要添加很多的html标签，手工添加会非常困难麻烦。

　　我们希望能够用Python很好的自动完成这个步骤。

### 1. 分块

　　纯文本中会以空行按文本分成一个个段落，那么我们首先需要将文本分成段落，然后对于每个段落去匹配相应的规则。

　　这里应用到生成器，关键字yield。

　　首先分解成一行一行的，然后分成块，按空行分成一个个block。

    # -*- coding:utf-8 -*-
    
    'rules.py'
    
    # 按行读入的生成器
    def lines (file) :
    	for line in file : yield line
    	yield '\n'
    
    # 通过空行将文本分块
    def blocks (file) :
    	block = []
    	for line in lines (file) :
    		# 如果不是空行，那么加入到块中
    		if line.strip () :
    			block.append (line)
    		elif block :
    			# 如果是空行，则生成一个块，然后继续
    			yield ''.join (block).strip ()
    			block = []

### 2.  定义规则

　　我们将文本分块之后，希望通过一些特征来判断使用什么样的标签，所以定义一些rule。

　　整个实践只是为了更好地了解Python，相应的规则肯定也很随意，只是个测试而已。

    # -*- coding:utf-8 -*-
    
    'util.py'
    
    class Rule :
    	"""
    	定义一些规则，对于不同的块，根据不同的规则去定义这个块的所属
    	下面只是应用了一些简单的规则，具体的可以自己去定义
    	"""
    	def action (self , block , handler) :
    		handler.start (self.type)
    		handler.feed (block)
    		handler.end (self.type)
    		return True
    
    class HeadingRule (Rule) :
    	"""
    	标题单独占一行，最多70个字符，而且不以冒号结尾
    	"""
    	type = 'heading'
    	def condition (self , block) :
    		return not '\n' in block and len (block) <= 70 and not block[-1] == ':'
    
    class TitleRule (HeadingRule) :
    	"""
    	题目是文档的第一个块，而且是个标题
    	"""
    	type = 'title'
    	first = True
    
    	def condtion (self , block) :
    		if not self.first :
    			return False
    		self.first = False
    		return HeadingRule.condition (self , block)
    
    class ListItemRule (Rule) :
    	"""
    	列表项是以连字符开始的段落
    	"""
    	type = 'listitem'
    	def condition  (self , block) :
    		return block[0] == '-'
    	def action (self , block , handler) :
    		handler.start (self.type)
    		handler.feed (block[1:].strip ())
    		handler.end (self.type)
    		return True
    
    class ListRule (ListItemRule) :
    	"""
    	列表就是包括一些连续的列表项
    	"""
    	type = 'list'
    	inside = False
    	def condition (self , block) :
    		return True
    	def action (self , block , handler) :
    		if not self.inside and ListItemRule.condition (self , block) :
    			handler.start (self.type)
    			self.inside = True
    		elif self.inside and not ListItemRule.condition (self , block) :
    			handler.end (self.type)
    			self.inside = False
    		return False
    
    class ParagraphRule (Rule) :
    	"""
    	除了以上特殊规则，则视为段落
    	"""
    	type = 'paragraph'
    	def condition (self , block) :
    		return True


### 3. 定义一些操作，对于不同的规则、不同的过滤器执行不同的操作

　　如果我们根据定义的Rule，识别出不同的块之后，希望对于不同的块进行不同的操作，而且还有一些针对URL,mail的过滤器。

    # -*- coding:utf-8 -*-
    
    'handlers.py'
    
    class Handlers :
    	"""
    	对于不同的对象，调用不同的方法。
    	对于不同的块，分成三个部分，start , feed , end
    	start和end就很显然，输出不同的html标签，而feed部分就是将文档部分输出
    	而sub()是应用于正则表达式的匹配
    	"""
    	def callback (self , prefix , name , *args) :
    		method = getattr (self , prefix + name , None)
    		if callable (method) :
    			return method (*args)
    	def start (self , name) :
    		self.callback ('start_' , name)
    	def end (self , name) :
    		self.callback ('end_' , name)
    	def sub (self , name) :
    		def substitution (match) :
    			result = self.callback ('sub_' , name , match)
    			if result is None :
    				match.group (0)
    			return result
    		return substitution
    		
    class HTMLRenderer (Handlers) :
    	"""
    	对于HTML标签的特定方法
    	"""
    	def start_document (self) :
    		print '<html><head><title>World Wide Spam</title></head><body>'
    	def end_document (self) :
    		print '</body></html>'
    	def start_paragraph (self) :
    		print '<p>'
    	def end_paragraph (self) :
    		print '</p>'
    	def start_heading (self) :
    		print '<h2>'
    	def end_heading (self) :
    		print '</h2>'
    	def start_list (self) :
    		print '<ul>'
    	def end_list (self) :
    		print '</ul>'
    	def start_listitem (self) :
    		print '<li>'
    	def end_listitem (self) :
    		print '</li>'
    	def start_title (self) :
    		print '<h1>'
    	def end_title (self) :
    		print '</h1>'
    	def sub_emphasis (self,match) :
    		return '<em>%s</em>' % match.group(1)
    	def sub_url (self,match) :
    		return '<a href="%s">%s</a>' % (match.group(1),match.group(1))
    	def sub_mail (self,match) :
    		return '<a href="mailto:%s">%s</a>' % (match.group(1),match.group(1))
    	def feed(self,data):
    		print data

### 4. 文本解析过程，即主过程

　　接下来就是串联整个过程
	
1.  首先我们添加一些指定的规则和过滤器。
2.  然后利用生成器将文本分块
3.  之后对每个块先使用过滤器
4.  然后匹配相应规则

　　源码：

    # -*- coding:utf-8 -*-
    
    'markup.py'
    
    import re , sys
    from util import *
    from rules import *
    from handlers import *
    class Parser :
    	"""
    	语法分析器读取文本之后，按块去对应规则处理
    	"""
    	def __init__ (self , handler) :
    		self.handler = handler
    		self.rules = []
    		self.filters = []
    	def addRule (self , rule) :
    		self.rules.append (rule)
    	def addFilter (self , pattern , name) :
    		def filter (block , handler) :
    			return re.sub (pattern , handler.sub (name) , block)
    		self.filters.append (filter)
    	def parse (self , file) :
    		self.handler.start ('document')
    		for block in blocks (file) :
    			# 先对每个块进行过滤
    			for filter in self.filters :
    				block = filter (block , self.handler)
    			# 匹配规则
    			for rule in self.rules :
    				if rule.condition (block) :
    					last = rule.action (block , self.handler)
    					if last :
    						break
    		self.handler.end ('document')
    
    class BasicTextParser (Parser) :
    	"""
    	对于不同的需求，去添加不同的规则和过滤器
    	"""
    	def __init__ (self , handler) :
    		Parser.__init__ (self , handler)
    		self.addRule (ListRule ())
    		self.addRule (ListItemRule ())
    		self.addRule (TitleRule ())
    		self.addRule (HeadingRule ())
    		self.addRule (ParagraphRule ())
    		
    		#三个过滤器，强调、链接、电子邮件
    		self.addFilter (r'\*(.+?)\*' , 'emphasis')
    		self.addFilter (r'(http://[\.a-zA-Z/]+)' , 'url')
    		self.addFilter (r'([\.a-zA-Z]+@[\.a-zA-Z]+[a-zA-Z])' , 'mail')
    
    handler = HTMLRenderer ()
    parser = BasicTextParser (handler)
    parser.parse (sys.stdin)
    
　　执行方法，在命令行运行以下命令：

	python markup.py <text_input.txt >text_input.html

　　其实两个参数分别表示输入和输出，`<`表示输入，`>`表示输出。

### 5. 结果

　　教材上的用例：

    Welcome to World Wide Spam. Inc.
    
     
    
     
    
    These are the corporate web pages of *World Wide Spam*, Inc. We hope you find your stay enjoyable, and that you will sample many of our products.
    
     
    
    A short history of the company
    
     
    
    World Wide Spam was started in the summer of 2000. The business concept was to ride the dot-com wave and to make money both through bulk email and by selling canned meat online.
    
     
    
    After receiving several complaints from customers who weren't satisfied by their bulk email, World Wide Spam altered their profile, and focused 100% on canned goods. Today, they rank as the world's 13,892 online supplier of SPAM.
    
     
    
    Destinations
    
     
    
    From this page you may visit several of our interesting web pages:
    
     
    
     - What is SPAM?(http://wwspam.fu/whatisspam)
    
     
    
     - How do they make it?(http://wwspam.fu/howtomakeit)
    
     
    
     - Why should I eat it?(http://wwspam.fu/whyeatit)
    
     
    
    How to get in touch with us
    
     
    
    You can get in touch with us in *many* ways: By phone (555-1234), by email (wwspam@wwspam.fu) or by visiting our customer feedback page (http://wwspam.fu/feedback)　

　　相应的html效果：


![Result](\images\PythonNote2_1.png)

## 扩展

　　其实这种即时标记的方法可以应用在很多上面，比如说markdown和html的转换等等。

　　不过要用在实际中，可能需要一些更智能的解析处理。