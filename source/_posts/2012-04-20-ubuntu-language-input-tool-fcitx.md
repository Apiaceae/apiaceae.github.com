--- 
layout: default 
title: "ubuntu中文输入法Fcitx安装"
date: 2012-04-20
categories: linux
tags: 输入法  
---

在ubuntu10.10系统安装成功后,系统默认的中文输入法是ibus,但是这个输入法给我们这些在windows下使用sougou用惯了的
人是很不习惯的.特别是打词组的时侯,不能联想,词库不是很多.后来有了解到还有一款中文输入法Fcitx,所以换成这个之后,发现比较适合我使用,虽然
存在很多不足.

首先来认识下Fcitx,它是Free Chinese Input Toy for X的简称,中文名叫小企鹅输入法,包括拼音和双拼输入法.目前最新版本为4.0.1,相比之前的版本,新增很多功能包括新的皮肤、词库和详细设置界面。\

[![](http://www.mylouge.com/wp-content/uploads/2011/02/Fcitx%E4%B8%AD%E6%96%87%E8%BE%93%E5%85%A5%E6%B3%95-300x186.gif "Fcitx中文输入法")](http://www.mylouge.com/wp-content/uploads/2011/02/Fcitx%E4%B8%AD%E6%96%87%E8%BE%93%E5%85%A5%E6%B3%95.gif)\

之前这款输入法是个人所做(不过已经停止开发)，目前官方主页已经转移到google code上: [http://code.google.com/p/fcitx/\
](http://code.google.com/p/fcitx/)上面有最新的版本下载和皮肤，词库。

**安装方法如下：**

' sudo add-apt-repository ppa:wengxt/fcitx-nightly   \\\\增加ppa源\
 sudo apt-get update   \\\\更新软件库\
 sudo apt-get install fcitx fcitx-config-gtk fcitx-sunpinyin
 \\\\安装fcitx和fcitx-sunpinyin输入法\
 sudo apt-get install fcitx-table-all   \\\\安装码表\'
 
 到目前为止输入法已经安装完成了.
 
 接下来输入:im-switch -s fcitx -z default 把fcitx设置为默认输入法

或者通过:系统—系统管理—语言支持,打开语言和文本设置项,在语言分页中的键盘输入方式系统中选择fcitx.\
 另外,可以右击输入法进行配置,包括皮肤,快捷键等.


除非注明，[空中楼阁](http://www.mylouge.com/)的文章均为原创，支持转载，但请以链接形式标明本文地址

本文地址：[http://www.mylouge.com/2011/02/1146.html](http://www.mylouge.com/2011/02/1146.html)
