---
layout: post
title: "el get方便管理emacs插件"
description: "el get方便管理emacs插件"
category: Emacs
tags: [Emacs, el-get]
---
{% include JB/setup %}

# el get 介绍 #

  el-get是Emacs现下最受欢迎的包安装管理工具。由于Emacs一直以来虽然具有强大的扩展能力，但是第三方插件始终没有个统一的安装方法。往往用户需要编写或者粘贴大量的elisp代码到.emacs文件或者init.el文件中。而且升级往往也是比较麻烦的事。el-get就是这样一个肩负起Emacs“一键安装”，“简单部署”大任的利器。el-get就如同著名的debian package管理工具apt-get一样，简单易用。让你的emacs配置需求大大降低。进而可以专注于享受emacs给你带来的快乐。

安装 
======

1. 联网，并且安装需要的外部工具： git\ cvs\ install-info 等等

2. 安装

## 懒加载安装 ##
懒加载的意思就是说平时你不想乱动你的emacs。需要el-get运行时可以直接在\*scratch\*的buffer里面运行：

#### 稳定版 ####

稳定版就是粘贴下面的代码到你的buffer里面


    ;; So the idea is that you copy/paste this code into your *scratch* buffer,
	;; hit C-j, and you have a working el-get.
	(url-retrieve
	"https://raw.github.com/dimitri/el-get/master/el-get-install.el"
	(lambda (s)
       (goto-char (point-max))
	      (eval-print-last-sexp)))

然后运行`eval-buffer`

一小会儿后emacs会有通知相应，这样就可以运行el-get了

#### 开发版 ####

开发版也差不多：

    ;; So the idea is that you copy/paste this code into your *scratch* buffer,
	;; hit C-j, and you have a working developper edition of el-get.
	(url-retrieve
	  "https://raw.github.com/dimitri/el-get/master/el-get-install.el"
	  (lambda (s)
	    (let (el-get-master-branch)
	      (goto-char (point-max))
	        (eval-print-last-sexp))))


运行之后实际上是将git上的工程clone到本地默认路径是：
`~/.emacs.d/el-get/el-get`。


## 自动安装 ##
自动安装可以在emacs启动运行时加载`el-get`，这样你可以随时运行了。
可以第一次运行上面的“懒安装”，将el-get下载下来之后尝尝鲜。后买就可以开始配置你的emacs启动文件了：


    (add-to-list 'load-path "~/.emacs.d/el-get/el-get")
	(unless (require 'el-get nil 'noerror)
	(with-current-buffer
    (url-retrieve-synchronously
		       "https://raw.github.com/dimitri/el-get/master/el-get-install.el")
	        (goto-char (point-max))
			(eval-print-last-sexp)))
	(add-to-list 'el-get-recipe-path "~/.emacs.d/el-get-user/recipes")
	(el-get 'sync)

这里面，首先是加载本地的el-get。如果加载失败，则从github上下载。
之后将`el-get-user`作为用户的recipes目录。用户可以自己定义“recipe”。即相当于apt-get 中的ppa。
最后`'sync`表示同步最新的版本。

只有在emacs初始文件中加入了el-get初始化，el-get才能够帮助你自动加载在el-get文件夹内下载的packages。

使用
===========

由于el-get是异步更新的。包的下载并不会影响用户的其他工作。这点非常爽。emacs2.4里面的package如果网络链接有问题，其他事情也就干不了了。

几个最常用的命令：
- `el-get-list-packages` 列举可安装的项及简介
- `el-get-install` 安装指定项
- `el-get-remove` 卸载
- `el-get-emacswiki-refresh` 从emacswiki上获得可安装的列表，这里货相当多。

`el-get-install`的功能是将远程包下载到本地。依然需要你在emacs启动文件中进行`require`等的配置。

## Package ##
el-get并不是唯一的包管理的工具，emacs官方推出的是elpa。这个管理工具对其内容限制非常严格。因此很多优秀的第三方插件不能在里面找到。但是很多很关键的软件更新还是建议用elpa来进行：
最主要的比如org。emacswiki中只能获得2.3版（2003年）的老版本。应该注意。

Package的控制也很简单，在命令行输入：
`package-list-packages`即可，之后标注`i`为准备安装，`d`为准备删除。`x`为执行。执行后，elpa将将安装下载到`~/.emacs.d/elpa/`对应文件夹下。

关于package的相关信息可以参考package的[emacswiki](http://wikemacs.org/index.php/Package.el)，以及[org官方文档](http://orgmode.org/org.html#Installation)

## 集成 ##
el-get可以将elpa emacs-wiki全部集成进来。运行`el-get-emacswiki-refresh`可以将emacswiki下的软件自动加入源。`el-get-elpa-build-local-recipes`可以将elpa的软件自动加入到源。

  
其他帮助
=============
- 安装后就可以在你emacs info中`C-h i`查看到el-get的帮助文档。
- 可以参考[官方安装指南](http://wikemacs.org/index.php/El-get)
- 可以参考官方的[README文件](https://github.com/dimitri/el-get/blob/master/README.md)
- 可以参考[我的配置文件](http://google.com)

