---
layout: post
title:  "如何构架出我的博客"
date:   2016-03-22 14:57:41 +0800
duoshuo_comment: true
categories: jekyll
tags: 博客
---
去年暑假的时候折腾好了博客，实现还是Githubs+jekyll,之前用的掌心的一个模板，一直觉得不怎么好看，所以最近改版了下。

写好之后一直也没更新，主要觉得是自己的水平不够，不知道更新些什么。现在也大三了，之前一直瞎折腾各种web方面的东西。博主自己由于也是个学习者，所以折腾自己一个小博客，偶尔记录一下自己的学习过程中碰到有意思的事情。
就像我之前折腾Ubuntu，装好之后配置环境，各种都是每次网上去找，每次碰到各种问题，解决之后时间一长，然后忘了＝＝＃

然后下次接着重新折腾...囧＝＝＃

简单说一下我的博客搭建：
jekyll是基于ruby写的一个小东西，所以首先电脑上配置好ruby,rails环境，然后安装好jekyll。

{% highlight ruby %}
$jekyll new myblog
$New jekyll site installed in /home/longfellow/Projects/ruby/myblog.

$jekyll server
{% endhighlight %}

终端下面敲完这两句代码，然后就可以在本地预览你的博客了。页面比较简单，各种配置具体在jekyll网页上面学习文档。

也可以随便在我的右上角fork一下，然后随便改改就行了，我这个就是在[咀嚼之味][jerryzou]的基础上改了下前端页面

由于原来博主的组织文章等方法具体没怎么看，所以用了下他的模板。

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
[jerryzou]:http://jerryzou.com
