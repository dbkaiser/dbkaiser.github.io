---
layout: post
title: "mysql collation问题"
description: ""
category: 
tags: [MySql Collation]
---
{% include JB/setup %}

Mysql Collation问题
====

问题描述
---
Mysql 中有时会发生这种问题：Beyoncé在插入数据库时出现Duplicate key，原因是因为在那unique的列上没有设定collation，而且表中已经有了Beyonce这样的项目。

虽然这里应该将两个merge在一起，但是在数据库设计时还是应该注意这一点，在必要时设定collation。

上网搜索了一下：

mysql collation的命名规则：
---
它们以其相关的字符集名开始，通常包括一个语言名，并且以`_ci`（大小写不敏感）、`_cs`（大小写敏感）或`_bin`（二元）结束。

比如latin1字符集有以下几种校正规则：

- 校对规则 含义

`latin1_german1_ci` 德国DIN-1
`latin1_swedish_ci` 瑞典/芬兰
`latin1_danish_ci` 丹麦/挪威
`latin1_german2_ci` 德国 DIN-2
`latin1_bin` 符合latin1编码的二进制
`latin1_general_ci` 多种语言(西欧)
`latin1_general_cs` 多种语言(西欧ISO),大小写敏感
`latin1_spanish_ci` 现代西班牙

MySQL按照下面的方式选择表字符集和 校对规则：
如果指定了CHARACTER SET X和COLLATE Y，那么采用CHARACTER SET X和COLLATE Y。
如果指定了CHARACTER SET X而没有指定COLLATE Y，那么采用CHARACTER SET X和CHARACTER SET X的默认校对规则。
否则，采用服务器字符集和服务器校对规则。

建议collation都尽量采用字符集相应的bin类型的校对规则，这样不容易出错。

因此，根据你的标的内容需要建立相应的collation：
    alter table artist modify artist_name varchar(255) character set utf8 collate utf8_bin not null;

