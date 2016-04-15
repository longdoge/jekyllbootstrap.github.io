---
layout: post
title: "python爬虫入门（一）"
date: 　　2016-03-28 10:30:41 +0800
duoshuo_comment: true
categories: python 
---

<p>最近由于信息检索一门选修课，对爬虫这个东西产生了兴趣，遂自己找了相关的文档资料，学习一下有关搜索引擎这方面。关于python爬虫方面的介绍无需多言，感兴趣的可以多goolge了解一下。</p>

<h3>Urllib库的基本使用：</h3>

<p>首先来看一下python来爬一个最基本的网页（多了解点web方面的知识会更好）：</p>

{% highlight python %}
import urllib2

response = urllib2.urlopen("http://www.baidu.com")
print response.read()
{% endhighlight %}

<p>然后你就会发现有两个错，如下</p>

{% highlight python %}
  File "pythonSpider.py", line 4
    print response.read()
                 ^
SyntaxError: invalid syntax
{% endhighlight %}

{% highlight python %}
Traceback (most recent call last):
  File "pythonSpider.py", line 2, in <module>
    import urllib2
ImportError: No module named 'urllib2'
{% endhighlight %}

<p>这是由于python2.7和python3.0及以上版本的问题，在python3.0中<code>print</code>已经作为一个函数了，而且在python3.3之后，urllib2这个库已经用urllib.request代替。所以应该这么写：
{% highlight python %}
import urllib.request

response = urllib.request.urlopen("http://www.baidu.com")
print (response.read())
{% endhighlight %}</p>

<mark>注意提示—我的环境：Ubuntu+python3.5.0</mark>

<p>爬出来之后是一堆无排版格式的html，所以在这里就不贴了。</p>

<h3>Urllib库的扩展使用：</h3>