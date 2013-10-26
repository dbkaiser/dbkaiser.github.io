---
layout: post
title: "刷A2109以及更换默认sdcard"
description: ""
category: Android
tags: [a2109,解锁,sdcard,Android]
---
{% include JB/setup %}
# lenovo 乐pad A2109刷机以及更换默认sdcard

折腾了一天，终于把年初赢来的pad给刷了，也不知道怎么就来了这么大动力。竟然搞了一天。

其实现在刷机的教程已经很丰富了。

这里做一个索引而已。把一些学习到的信息记录一下。

## 前言

[Lenovo
A2109a](http://pad.zol.com.cn/316/3162648.html)是去年联想推出的一个物美价廉的android系列pad。推出是售价1999，不贵，性能也不错。4核1Gn内存，玩个gta3啥的一点不卡。本人不是硬件控，这里就不赘述了。只是联想的android系统虽没有深度定制，但是也不像小米那样轻松地给你提供root权限管理。需要自己刷系统、添加root权限等等。因此就带来了后面这些文章。

## 解锁与root

[这篇文章](http://lefen.lenovo.com/lfb/thread-94533-1-1.html)讲述了一键解锁和一键root的方法。一键的过程可以在bat文件中看到。貌似就是用adb的方式把能root的bootloader传到机器上然后用fastboot的方式进行启动。

root之后，adb就具有了root权限。但是若使机器上面的应用也都具有root权限，则还需要增加superuser的应用程序apk来管理。这个安装方法可以参考[这篇文章](http://pad.cnmo.com/19/196989.html),
不过我没有按照这上面继续，因为我想尝试下那些非官方的固件，那些极客们深度修改的固件。于是就有了下面的文章。

## recovery mode

recovery mode是回复出厂设置、清除缓存、备份应用以及从sdcard刷新固件的方式。貌似有两种渠道进入recovery
mode。[这篇文章](http://lepad.it168.com/thread-2527820-1-1.html)介绍了一种很简单的方式，就是pad默认进入recovery
mode的方式。而[这篇文章](http://lefen.lenovo.com/lfb/forum.php?mod=viewthread&amp;tid=106313&amp;fromuid=388446)介绍了使用工具进入recovery
mode的方式。这两者更大的区别在于前者只能升级官方发布几种固件，（我不确定是否和解锁和root有关），而后者可以升级后面提到的非官方的固件。

同时，recovery
mode也可以用于从sdcard中安装apk的功能，比如前面所讲到的superuser.apk和后面将会用到的gapps的apk都是经过打包后用external
sdcard在recovery mode下升级的。

## 固件

[这篇文章](http://lefen.lenovo.com/lfb/thread-106150-1-1.html)介绍了一个android
jelly bean
4.1.1的私有升级版本以及下载地址。这是一篇翻译文章，原文在lenovo海外论坛也可以搜到。这个版本中删除了若干官方版本中加入的应用，但是没有安装谷歌默认的服务，比如google
play。我很费解的就是为什么是在诸如lenovo 三星等机器上，如果默认没有安装google
play，从豌豆荚上安装service和play就启动不起来。这个版本中作者也提供了这些服务。用一个zip打包好，利用前面讲的recovery
mode安装。

## sdcard

我觉得很多android系统最烦人的就是sdcard位置不固定。如果从android程序中我们可以通过getExternalPath()函数得到他，但是很多安装的apk都是默认的/sdcard，这样往往就指向了pad内置的存储器，往往也就几个g。而外置存储卡可能会被mount到/sdcard2
或者/sdcard/external等地方，我们得修改每个应用软件的默认位置才能使他们的应用数据存储到外部存储卡，否则内部存储卡很快就满了。而很多应用甚至都不提供外存储卡位置配置。这样就非常不方便。有了root以后我们可以把外部存储设备mount到/sdcard/上。但是每次机器重启以后还是会丢失，我们总不能每次都连adb啊。有[一篇文章](http://forum.xda-developers.com/showthread.php?t=1716166)讲述了通过修改/etc/vold.fstab来修改默认mount配置，但是这种配置因机器而异，a2109只有一个外部存储卡，这种配置无效。于是，还是利用万能的论坛，[这篇文章](http://lenovobbs.cnmo.com/thread-12296057-1-1.html)提供了一个好的解决方案，虽然还是有点麻烦，也差强人意了。就是利用gscript这个软件，可以在ui界面上执行固定的脚本，甚至root的。这样就需要我们每次重启机器时，执行下这个脚本了。

至此，刷机，改sdcard，完成。
