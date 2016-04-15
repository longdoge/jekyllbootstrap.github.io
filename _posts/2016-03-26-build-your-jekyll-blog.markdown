---
layout: post
title: "Jekyll＋Github搭建你自己的博客"
date: 2016-03-26 17:30:41 +0800
duoshuo_comment: true
categories: jekyll 
---
<p>如果你懂点git(当然不懂也没关系，读完这篇文章希望对你有点帮助)，又比较喜欢折腾，又比较喜欢文字，你也可以不是程序员，用jekyll搭建一个轻量级的博客,写点自己的文章，不失为一种很有意思的事。jekyll＋github+markdown完全能达到你的要求。</p>

<p>开题建议：你可能需要一个Ubuntu或者mac。这个主要原因是方便，不是说必须。jekyll是基于ruby的一个框架，如果你想在windows下面折腾ruby我劝你还是放弃，因为你可能会遇到些能让你发狂的问题。而且还网上鲜有解决办法。</p>

<p>假设你已经装好了Ubuntu,并且安装了ruby,gem,rails(如果没搞定的话建议移步<a href="https://ruby-china.org/">Ruby China</a>)</p>

<p>接下来你首先要做的是：安装jekyll.(假设你跟我一样实在Ubuntu下面折腾)</p>

{% highlight ruby %}
$sudo gem install jekyll
{% endhighlight %}

<p>这过程中你可能遇到的问题<br/>１：错误信息提示：找不到一个JavaScript环境，只要在终端中输入如下命令即可：    
{% highlight ruby %}
$sudo apt-get install nodejs
{% endhighlight %}
</p>

<h3>接下来可以开始了</h3>

{% highlight ruby %}
longfellow@longfellow:~/Projects/ruby$jekyll new myblog.github.io
longfellow@longfellow:~/Projects/ruby$cd myblog.github.io
longfellow@longfellow:~/Projects/ruby/myblog.github.io$jekyll server
{% endhighlight %}

<p>本地就可以跑了，然后就可以推送到Github上面去了（假设你已经有了帐号并且有个名字是my.github.io的repository）：</p>

{% highlight ruby %}
longfellow@longfellow:~/Projects/ruby$cd myblog.github.io
longfellow@longfellow:~/Projects/ruby/myblog.github.io$git init .
longfellow@longfellow:~/Projects/ruby/myblog.github.io$git add .
longfellow@longfellow:~/Projects/ruby/myblog.github.io$git commit -m "update"
longfellow@longfellow:~/Projects/ruby/myblog.github.io$git remote add origin https://github.com/myblog/myblog.github.io.git
longfellow@longfellow:~/Projects/ruby/myblog.github.io$git push -u origin master
Username for 'https://github.com': 
Password for 'https://longdoge@github.com':
{% endhighlight %}

<p>第一次推送可能需要等10min左右，然后打开myblog.github.io就可以了。接下来你可能觉得：哎，不行这页面太low了，而且域名看着也不舒服。所以接下来才是折腾的部分－－设计你自己喜欢的模板。这时候你就需要懂点jekyll里面有哪些变量了：全局变量，全站变量，页面变量，如何创建出几个页面，如何添加标签，如何添加订阅这些功能。看博客不如看文档，所以假设你是个程序员的话移步<a href="http://jekyll.bootcss.com/">Jekyll</a>。当然不喜欢折腾的话请google一下jekyll theme</p>

<p><mark>看别人的博客好比给你打开一扇新世界的大门，让你看到有意思的事情，然后自己去折腾。</mark>而不是企图在别人短短的一篇博客中学到很多东西。这是我一直阅读别人文章的一个原则。</p>

<p>然后买个域名，这时候你就不得不去了解一些关于域名解析的事情了。然后加一个评论。新技能Get√.</p>

<p>你花了好几天，可能十几天搞定这些，你就会觉得，这也没什么难度嘛，_post下面写好markdown文件，然后<code>jekyll build</code>，推送到Gituhub上面，没什么可以折腾的嘛。别急！还有能折腾的地方：要是能在终端直接敲行命令建好markdown多爽，自己直接随后写好文字，就可以了喵～不用麻烦每次都写头信息了。</p>

<p>当然，这时候懂点ruby的话最好了。在终端下面敲：
{% highlight ruby %}
longfellow@longfellow:~/Projects/ruby/myblog.github.io$rake post title="titlename"
rake aborted!
No Rakefile found (looking for: rakefile, Rakefile, rakefile.rb, Rakefile.rb)

(See full trace by running task with --trace)
{% endhighlight %}</p>

<p>参考<code>jekyll-bootstrap</code>可以写一个Rakefile,用来执行这条命令。</p>

<h3>我的Rakefile:</h3>

{% highlight ruby %}
require "rubygems"
require 'rake'
require 'yaml'
require 'time'

SOURCE = "."
CONFIG = {
  'themes' => File.join(SOURCE, "_includes", "themes"),
  'layouts' => File.join(SOURCE, "_layouts"),
  'posts' => File.join(SOURCE, "_posts"),
  'post_ext' => "markdown",
}

# Usage: rake post title="titlename" 
desc "Begin a new post in #{CONFIG['posts']}"
task :post do
  abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])
  title = ENV["title"] || "new-post"
  tags = ENV["tags"] || "[]"
  category = ENV["category"] || ""
  category = "\"#{category.gsub(/-/,' ')}\"" if !category.empty?
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  begin
    date = (ENV['date'] ? Time.parse(ENV['date']) : Time.now).strftime('%Y-%m-%d')
  rescue => e
    puts "Error - date format must be YYYY-MM-DD, please check you typed it correctly!"
    exit -1
  end
  filename = File.join(CONFIG['posts'], "#{date}-#{slug}.#{CONFIG['post_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end
  
  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts 'date: ""'
    post.puts "duoshuo_comment: true"
    post.puts "category: #{category}"
    #post.puts "tags: #{tags}"
    post.puts "---"
  end
end # task :post

# Usage: rake page name="about.html"
desc "Create a new page."
task :page do
  name = ENV["name"] || "new-page.md"
  filename = File.join(SOURCE, "#{name}")
  filename = File.join(filename, "index.html") if File.extname(filename) == ""
  title = File.basename(filename, File.extname(filename)).gsub(/[\W\_]/, " ").gsub(/\b\w/){$&.upcase}
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end
  
  mkdir_p File.dirname(filename)
  puts "Creating new page: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: page"
    post.puts "title: \"#{title}\""
    post.puts 'description: ""'
    post.puts "---"
  end
end # task :page

desc "Launch preview environment"
task :preview do
  system "jekyll serve -w"
end # task :preview

#Load custom rake scripts
Dir['_rake/*.rake'].each { |r| load r }
{% endhighlight %}

--------

<p><code>rake post title="titlename"</code>用来在_post下面生成带有头信息的<mark>markdown</mark>文件<br/></p>

<p><code>rake page name="about.html"</code>生成其他类似于about这样的页面</p>