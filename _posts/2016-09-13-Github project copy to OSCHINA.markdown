---
layout: post
title: "将Github项目同时托管到Git@OSC"
date: 2016-09-13 16:20:00
categories: ['oschina','github']
tags: ['oschina','github']
---
# 给本地仓库添加第二个远程地址
用户可能在本地已经有了一个Github仓库，如果想在GIT@OSC上也放一份代码，可以给仓库添加一个远程地址，使之能够推送到GIT@OSC。 
第一，你先得在GIT@OSC上创建一个空仓库，也就是创建项目的时候不要初始化。然后按照下面的命令就行了，比如我创建了一个blog的项目。
```
git remote -v 
#查看远程地址
git remote add osc https://git.oschina.net/jameswong/blog.git
#添加新的远程地址
git push -u osc --all#推送所有的本地分支git push osc --tags#推送所有的标签
```