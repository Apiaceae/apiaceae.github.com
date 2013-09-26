--- 
layout: post 
title: "MacOS Fink命令"
date: 2012-03-11 13:29
categories: Linux
tags: Fink
comments: true
sharing: true
---

苹果上自带的Unix其实是很少的，像gcc，make，gnuplot，unrar啊这种杀人越货必备武器都默认没有的。gcc这帮工具好说，安装xcode就行了，其他东西以前用Mac的时候都是用MacPort来搞，但是这次的新Mac在安装Unix工具的时候，上网搜了一下，发现Fink这个更好的工具。

Fink工程的目的和MacPort一样，通过修改 Unix 软件来port到Mac OS X
上，然后提供某种下载安装机制供大家使用。在Fink里面你可以像Ubuntu中那样用apt这套工具直接安装二进制包，也可以直接使用Fink来通过源代码编译安装。一般直接用Fink比较好，因为里面的东西比较新。

Fink 的所有文件几乎都安装在 /sw（或你选择安装的地方）。因此，如果你想删除 Fink，输入下面的命令：

``
$ sudo rm -rf /sw
``

**升级fink自身**

``` 
$ fink selfupdate

$ fink selfupdate-rsync

$ fink index -f

$ fink selfupdate
```

**安装**

``
$ fink install xxx
``

**卸载**

``
$ fink remove xxx
``

**如果想把依赖包也一起卸载，加-r。如果想配置文件一并卸载，用**

``
$ fink purge
``

类似与ubuntu里面的remove –purge

**更新所有已安装包**

``
$ fink update-all
``

**查看可安装包**

``
$ fink list xxx 或者 fink apropos xxx
``

**也支持正泽表达式**

``
$ fink list “xxx\*”
``

**查看相关包的描述**

``
$ fink info
``

**如果不小心删除了某个包的文件，想重新安装整个包**

``
$ fink reinstall
``

**显示某个包的依赖关系**

``
$ fink show-deps xxx
 ``

原文地址：http://www.kunli.info/2009/12/11/mac-install-pink/
