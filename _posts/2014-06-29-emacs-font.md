---
layout: post
title: "Mac下Emacs 字体设置"
description: "在不同操作系统下设定emacs字体的统一方法"
category: Emacs
tags: [Emacs Font faces 字体]
---
{% include JB/setup %}
在mac下面安装了X-windows的emacs（brew也可以安装emacs，不过只能在终端显示）。桌面版的emacs的好处是有更丰富的字体和界面，而且有更丰富的功能，比如speedbar。

但是令我惊奇的是mac下面的字体很Q，是这个样子的：

![init](/images/initfont.png)

查了一下这个字体是mac系统里面自带的“娃娃体”。而英文字体默认的是Dejavu。一向严谨著称的程序员我当然不想写技术文章时用娃娃体，太不严肃点了。

于是从网上找到了这一段设置字体的代码：


    (set-language-environment 'UTF-8)
	(set-locale-environment "UTF-8")
	(set-default-font "Dejavu Mono 16")
	(if (and (fboundp 'daemonp) (daemonp))
		  (add-hook 'after-make-frame-functions
					(lambda (frame)
					  (with-selected-frame frame
						(set-fontset-font "fontset-default"
										  'unicode "黑体 16"))))
    (set-fontset-font "fontset-default" 'unicode "黑体 16"))


这里面设定英文字体还是Dejavu, 中文字体是黑体。

得到效果如下：

![with chinese_font](/images/chinese_effect.png)

不过很快又发现在我另一个ubuntu的机器上就会报找不到Dejavu字体的问题。怎么办呢？elisp里面提供了操作系统识别的api。于是更新代码如下：

    (if (eq system-type 'darwin) 
	  (progn 
	    (set-language-environment 'UTF-8)
    	(set-locale-environment "UTF-8")
		(set-default-font "Dejavu Mono 16")
		(if (and (fboundp 'daemonp) (daemonp))
		   (add-hook 'after-make-frame-functions
					(lambda (frame)
					  (with-selected-frame frame
						(set-fontset-font "fontset-default"
										  'unicode "黑体 16"))))
           (set-fontset-font "fontset-default" 'unicode "黑体 16")))
    )


注意这里面progn表示可以执行多个语句，并返回最后一个值，这在if语句里很有用。
