---
layout: post
title: "Ubuntu 13.04 下的一些软件配置：MPlayer,Anyconnect,VMWare, Oracle Java"
description: "Ubuntu下的一些软件配置：MPlayer,Anyconnect,VMWare"
category: Linux
tags: [Ubuntu 13.04, VMWare, Anyconnect, MPlayer, Software, Java]
---

# 前言 #

Ubuntu 13.04下有些软件和之前的版本配置有所不同，其实是更好用了，但是网上的老版本教程会不管用。这里记录一下：

# VMWare tool在Ubuntu 13下安装失败的问题 #

vmware player 非常好用，在任何操作系统下都可以简单完成虚拟系统的安装。不过，在Ubuntu13下安装完xp系统后在安装vmware tool时确没有那么顺利。不是自动升级完成的。这里就可以参考[这篇文章](https://communities.vmware.com/thread/447865?start%3D0&tstart%3D0)。 需要手动下载vmware tool进行安装。

# Cisco Anyconnect 在Ubuntu 1304下面的使用 #

很多公司登录vpn都是用的Cisco Anyconnect。非常好用，且各个平台都很齐全。但是在Ubuntu1304下面安装之后确发现无法正常连接。总出出现“cannot connect to gateway”的错误。于是谷歌一下。发现了[这篇文章](https://supportforums.cisco.com/thread/2226093)。 Ubuntu下面一个开源工具： openconnect就可以适配的完成这个工作。无需另行安装。

只需运行：

    sudo apt-get install network-manager-openconnect-gnome
	
之后直接在屏幕右上角上面的vpn connection中选择你要链接的公司vpn网址就ok了。很方便的！

# Ubuntu 下面MPlayer的中文字体 #

这个真是折腾了好久，可能是因为网上的同学们使用的版本不一致，按照各种各样的说法都不能展示中文字幕。最后发现是这样的：（我这里说明的是命令行的，MPlayer, gmplayer可以参考，但没有实践）

我这里使用的是Ubuntu1304版本

MPlayer 版本： 

如很多教程所说： 需要在~/.mplayer/config中设定参数只要两项： 

     subcp=cp936
     subfont="AR PL UKai CN"

这里很多教程都是说指向ttf或ttc的绝对路径。但是我这样试都是失败的。只有横线留下。这里我用的是font的名称。可以通过`gnome-font-viewer`来查看。

这里最主要的问题就是这个subfont。一直没找对路，一旦subfont对了以后，后面都还是很智能的。subcp是选择语言种类，这里你填utf-8\gbk\cp936都可以，如果是cp936的话，他甚至可以自动识别字母的编码是gbk还是utf-8，不需要用iconv手工转换。教程太多了也麻烦。

# Ubuntu 下安装oracle官方Java #

其实可能没必要。因为Java从7开始和openjdk的架构都很相似了。官方支持的openjdk完全可以完成我们需要的Java任务。本来我是要安装web Java。因此搜寻了一下。
可以参考[这篇文章](http://www.webupd8.org/2012/01/install-oracle-java-jdk-7-in-ubuntu-via.html)。 很简单，通过ppa的方式添加repo，然后用apt-get安装。


{% include JB/setup %}
