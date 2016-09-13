---
layout: post
title: "jekyll 官网文档部分翻译"
date: 2016-09-12 15:07:00
categories: ['jekyll','markdown']
tags: ['jekyll','markdown']
---
# 什么是jekyll??
简单说：它是静态网页生成器。
具体点：包含一些用markdown语法写的文件的文件夹；通过markdown和Liquid转换器
生成一个网站。
同时jekyll也是github静态页面引擎。意味着你可以用jekyll生成你的页面，免费托管在github服务器。


# 快速开始
gem install jekyll{安装jekyll。gem执行文件可能需要其他依赖，比如ruby}
jekyll new myblog{生成博客目录}
![](http://img.blog.csdn.net/20141026202452197?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbWFveHVueGluZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

tip::生成博客目录到本地:jekyll new .
启动服务器：
jekyl serve
然后浏览器访问：localhost:4000即可（预览）

基本用法：
通过gem安装包管理器安装好jekyll以后，就能够在windows的命令行中执行jekyll
jekyll build{到项目根目录，执行编译后，当前目录自动生成_site文件夹}


tip::
编译到指定地方
jekyll build --destination <destination>
编译指定文件夹
jekyll build --source <source> --destination <destination>
编译后好自动监听文件变化 自动编译
jekyll build --watch


提示：
编译到的目标文件夹会被清空

预览：
jekyll serve
访问：
localhost:4000


tip::
2.4版本以后会自动检测文件的改变
禁止该行为：
jekyll serve --no-watch

除了--no-watch等配置项，还有其他很多配置
一般是放在根目录下面的_config.xml文件下面，前面的放在命令行也是一种方式


调用jekyll命令的时候会自动用_config.xml里面的配置。
比如：_config.xml里的
source:_source
destination:_deploy
相当于：
jekyll build --source _source --destination _deploy

# 目录结构


jekyll本质上就是文本转换引擎。。


有很多的文件，用标记语言写好，放在不同的文件夹里面，
通过这种形式表现，你想你的网页长什么样，有哪些数据。
![](http://img.blog.csdn.net/20141027071828638?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbWFveHVueGluZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)



_config.yml :存储配置数据。把配置写在这个文件里面，可以让你不用在命令行中写。
_drafts:草稿，格式是:没有日期.md
_includes:包含一些模板，可以重复利用。你可以用通过{% include nav.html %}包含_includes/nav.html文件{这种方式是liquid语法}
_layouts:里面的文件通过{{ content }}包含_posts里面的文章。
_posts:存放你要发表的文章。格式YEAR-MONTH-DAY-title.MARKUP。
文件名确定了发表的日期和标记语言。博客的日期格式通过_config.yml的permalink字段设置或者通过YAML FRONT Matter设置
_data:保存数据的。jekyll会自动加载这里的所有
.jml或者.yaml结尾的文件。
比如你有一个members.yml。那么你可以通过site.data.members
访问该文件里的数据。
_site：
jekyll生成的网站会放在该文件夹下。
最好把它放到.gitignore文件里面，这样git就不会管理它了。
index.html:
该文件里面有一个YAML FRONT Matter。大概就长下面这样：
---
layout: index
title: FEX
page_id: index
---
jekyll会转换它。包括所有的根目录下面的，或者不是以上提到的，目录。
里的.html,.markdown,.md,和.textile文件。

除了上面提到的其他文件或者文件夹，会被自动拷贝
到_site文件夹里面。包括
css和图片文件夹，favicon.icon文件。

# 配置


有两种方式配置，一个是命令行，一个是通过_config.yml文件
source://定义jekyll读取文件的位置 比如本地就直接用.
destination://定义网站生成的位置，比如_site
safe://是否禁用自定义插件 不理解暂时不管他
encoding://通过名字定义文件的编码 只ruby1.9以后才有效
2.0.0以后默认的编码是utf-8，而之前的默认编码是ascii-8bit

Front Matter defaults
用这个东东可以具体地配置你的页面或者发表的文章。


经常你会重复配置一些东西，比如作者，
为了避免这种情况的解决方案是
在_config.xml中配置defaults字段


## 默认配置


jekyll默认是用如下的配置：看官网http://jekyllrb.com/docs/configuration/

Front Matter
通过这个可以设置一些变量（甚至可以自定义变量），比如title
---
layout: post
title: Blogging Like a Hacker
---
设置好变量以后，
你就可以在当前页面或者你的页面依赖的_layouts或者_includes
里的文件通过Liquid 标记，比如{page.title}访问了。


tip:::
不允许存在BOM字符
这个头不写也是可以的：
比如CSS and RSS feeds!可能不需要


已定义的全局变量：
layout:指定用_layouts下面的文件。


自定义的变量：
在Front Matter定义的变量（不是已定义的全局变量）都会在会话期间绑定数据给Liquid模板引擎。
比如你在定义了title，那你就可以再_layouts里面的模板使用它{{ page.title }}


# 写文章


jekyll有一个最好的特性就是：你写文章并发表他们只是意味着你只要管理一些文本文件即可。
而不需要配置和维护数据库以及良好的CMS系统。


## 发文章的文件夹：
_posts
里面都是些md或者testile文件。只要有yaml front matter，它们就会被转换为html格式的静态页面。


## 创建文件：
创建一个文件YEAR-MONTH-DAY-title.md
YEAR是4位数，month和day是两位数
例子：
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.textile


tip::
通过post_url访问其他的文章，不用担心链接（ the site permalink）的样式改变而访问不到。


## 内容的样式：
所有的文章都必须要有yaml front matter头。


tip::将<meta charset="utf-8">包含在head标签里面。


## 包含图片和资源
在根目录下创建文件夹比如assets和downloads
然后markdown语法访问通过这种形式：
![截屏]({{ site.url }}/assets/screenshot.jpg)
说明：
截屏链接的文字，（）里面的东西不会显示，是链接到的地址。
site.url可以访问你配置的（_config.yml）的网站url。
链接到pdf阅读器让用户下载：
you can [get the PDF]({{ site.url }}/assets/mydoc.pdf) directly.


## 显示一系列的文章：


<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>


## 显示文章的第一个段


<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>


## 高亮代码片段


通过Pygments or Rouge，jekyll具有内建的语法高亮能力


{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}


## 高亮代码同时显示行号：
{% highlight ruby linenos %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}



# _drafts文件夹工作方式


_drafts里面的文章是你暂时不想发表的


通过jekyll serve --drafts预览
jekyll build --drafts编译


# 创建页面


## 主页


即使是主页也可以用_layouts和_includes里面的东西


其他的增加的额外页面


一般方式：
|-- _config.yml
|-- _includes/
|-- _layouts/
|-- _posts/
|-- _site/
|-- about.html    # => http://example.com/about.html
|-- index.html    # => http://example.com/
└── contact.html  # => http://example.com/contact.html


干净的url方式（不带有文件后缀）
├── _config.yml
├── _includes/
├── _layouts/
├── _posts/
├── _site/
├── about/
|   └── index.html  # => http://example.com/about/
├── contact/
|   └── index.html  # => http://example.com/contact/
└── index.html      # => http://example.com/

## 变量


jekyll要遍历所有的文件，只要带有yaml front matter的文件
都可以通过Liquid 模板系统访问一些变量。




## 全局变量


site：包含了网站信息和_config.yml里面的信息
page:在yaml front matter的自定义的变量通过page访问
content:_layouts里面，不定义在_post和其他页面中。包含了post和其他页面里面的文章内容。
paginator:paginate在_config_yml里面配置以后，这个变量就可以用了。


## site变量


site.time:当前运行jekyll的时间
site.pages:所有的页面
site.posts:以时间逆序排序的所有的文章
site.data：包含从目录_data里面加载的数据列表


## page变量


page.content:页面内容
page.title:文章标题
page.urL:页面地址：比如/2008/12/14/my-post.html
page.date:页面的日期。可以在front matter重写：2008-12-14 10:30:00 +0900或者YYYY-MM-DD HH:MM:SS
page.id:页面id。比如/2008/12/14/my-post 在RSS feeds里面有用。


tip::
front matter里面可以自己定义变量：比如custom_css: true
然后你可以通过page.custom_css访问


## Paginator变量


paginator.per_page：每一页的文章数
paginator.posts：那一页可用的文章
paginator.page：当前页的值


tip::
Paginator只在index.html(或者/blog/index.html)中有效 

Data文件夹


# 通过Liquid模板系统可以自定义数据


jekyll支持从位于_data的yaml,json,csv文件中加载数据，（csv必须包含一个header row）


通过site.data访问里面的数据


例子：
比如定义一个文件_data/members.yml
- name: Tom Preston-Werner
  github: mojombo


- name: Parker Moore
  github: parkr


- name: Liu Fengyun
  github: liufengyun


然后可以通过site.data.members访问该文件（文件名决定了字段名）
<ul>
{% for member in site.data.members %}
  <li>
    <a href="https://github.com/{{ member.github }}">
      {{ member.name }}
    </a>
  </li>
{% endfor %}
</ul>


定义组织（包含子文件）


_data/orgs/jekyll.yml中：


username: jekyll
name: Jekyll
members:
  - name: Tom Preston-Werner
    github: mojombo


  - name: Parker Moore
    github: parkr


_data/orgs/doeorg.yml中：
username: doeorg
name: Doe Org
members:
  - name: John Doe
    github: jdoe


使用：
<ul>
{% for org_hash in site.data.orgs %}
{% assign org = org_hash[1] %}
  <li>
    <a href="https://github.com/{{ org.username }}">
      {{ org.name }}
    </a>
    ({{ org.members | size }} members)
  </li>
{% endfor %}
</ul>