---
layout: post
title: "github下面建立blog"
description: "github下面建立blog"
category: Blog
tags: [github, blog]
---
{% include JB/setup %}

## 前言

新浪blog非常好。可以通过xrpc方式进行发布blog。用我用chrome的插件scribefire就可以很方便的用markdown来写blog。但是用emacs的org2blog插件确不能很好的兼容。org2blog可以支持wordpress。但是国内几个网站的blog
xrpc就不那么支持了。我又尝试了用几大网站的云app建wordpress。[百度云](http://developer.baidu.com/bae/)需要大量特有的api修改。不能和原生wordpress结合。而官网发布的wordpress不仅版本较老，而且貌似不是很稳定，我的blog在几天之后访问出现了问题。[新浪云](http://sae.sina.com.cn/)不免费，还得花钱。不符合我的屌丝习惯。。。[gae](http://appengine.google.com/)对wordpress支持很好，可以无缝安装部署。但是mysql的存储是收费的。相当与要写blog就要收费。也没戏。剩下那些国外的那些blog就是墙的问题了。突然看到别人的blog写了后缀是github。才发现github现在已经支持了个人网站的发布。好欣喜啊。终于可以方便的用emacs写blog了。

这里的文字都源于[官方文档](https://help.github.com/articles/creating-pages-with-the-automatic-generator)。

## 起步

- 建立你自己的页面repo：

以用户为例，你的新repo的名字必须是：`username.github.io`，这里面username必须是你的用户名。

- 点击repo的setting:

![setting](https://github-images.s3.amazonaws.com/help/repo-actions-settings.png)

- 点击Automatic Page Generator:

![apg](https://github-images.s3.amazonaws.com/help/pages-automatic-page-generator.png)

  这样你就可以编辑你在github上第一个页面的内容了。

- 编辑你的页面并配置你的主题(Theme):

  ![edit](https://github-images.s3.amazonaws.com/blog/2012/page-generator-picker.png)

- 发布(Publish)：

  ![publish](https://github-images.s3.amazonaws.com/blog/2012/page-generator-publish.png)

点击publish

好了。
这样你页面可以在10分钟之后通过http://username.github.io来访问，username是你的用户名。这是一个最基本的静态页面网站。你可以通过github的repo来修改，编辑内容。下面我们会学习怎么用[Jekyll](http://jekyllbootstrap.com/)
来建立自己的blog。

[这篇文章](http://erjjones.github.io/blog/How-I-built-my-blog-in-one-day/)提供了更多丰富的选择。
