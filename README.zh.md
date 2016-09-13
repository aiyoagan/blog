# James blog 模板

### [我的博客在这里 &rarr;](http://blog.juzi89.com)

由于jekyll升级到3.0.x,对原来的pygments代码高亮不再支持，现只支持一种-rouge，所以你需要在 `_config.yml`文件中修改`highlighter: rouge`.另外还需要在`Gemfile`文件中加上
``
group :jekyll_plugins do
 gem "jekyll-paginate", "~> 1.1.0"
 end
    ``.

同时,你需要更新你的本地jekyll环境.

使用`jekyll server`的同学需要这样：

1. `gem update jekyll` # 更新jekyll
2. `gem install jekyll-paginate` #更新依赖的包

使用`bundle exec jekyll server`的同学在更新jekyll后，需要输入`bundle update`来更新依赖的包.

参考文档：[Installing a plugin](http://jekyllrb.com/docs/plugins/))
