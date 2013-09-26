--- 
layout: post 
title: ubuntu12.04配置静态IP及设置DNS 
date: 2012-07-17
categories: Linux
tags: [ubuntu, ip, dns]
---

静态IP配置方法：
================

编辑/etc/network/interfaces，删掉内容，并输入以下几行（假设你的网卡是eth0）



,,,`sudo gedit /etc/network/interfaces

auto eth0

iface eth0 inet static   //指定为static

address 192.168.1.103   //IP地址

gateway 192.168.1.1   //网关

netmask 255.255.255.0   //子网掩码

network 192.168.1.0   //这个是网络？

broadcast 192.168.1.255   //广播`

然后重启网络设备

sudo /etc/init.d/networking restart

 

设置DNS：

Ubuntu设置DNS，只要将DNS地址写入/ect/resolv.conf文件即可，但在12.04
desktop版中，重启系统之后，静态IP设置生效，但无法链接外网，/etc/resole.conf文件的DNS地址也覆盖掉了。

解决办法，在/etc/resol[vc](http://biancheng.dnbcw.info/vc/)onf/resolv.conf.d/目录下创建tail文件，写入

nameserver 202.96.134.133

nameserver 202.96.128.68

然后重启，DNS生效。

 

参考链接：http://ask[ubuntu](http://biancheng.dnbcw.info/ubuntu/).com/questions/130452/how-do-i-add-a-dns-server-via-resolv-conf

 

Ubuntu12.04的一些源列表
=======================

 

 

\

 

安装好ubuntu
12.04之后，可以联网之后，马上要做的最重要的事情之一就是配置更新源列表，这样以后安装更新或者软件才可以获得较好的下载速度。\
 首先，备份一下原来的源地址列表文件\
 sudo cp /etc/apt/sources.list /etc/apt/sources.list.old\
 然后进行修改\
 sudo gedit /etc/apt/sources.list\
 可以在里面添加资源地址，我是直接覆盖掉原来的。\
 添加好后保存，再输入 sudo apt-get update
就可以更新了，等着慢慢下载东西吧。我虽然选了一个网易的和一个中科大的源，无奈那天网速不给力，还是花了差不多两个小时。\

下面是网上找到的一些较好的源，有大型网站的，也有教育网的，可以根据自己的情况添加两三个即可。\
 \#网易的源（速度很快）\
 deb http://mirrors.163.com/ubuntu/ precise main universe restricted
multiverse\
 deb-src http://mirrors.163.com/ubuntu/ precise main universe restricted
multiverse\
 deb http://mirrors.163.com/ubuntu/ precise-security universe main
multiverse restricted\
 deb-src http://mirrors.163.com/ubuntu/ precise-security universe main
multiverse restricted\
 deb http://mirrors.163.com/ubuntu/ precise-updates universe main
multiverse restricted\
 deb http://mirrors.163.com/ubuntu/ precise-proposed universe main
multiverse restricted\
 deb-src http://mirrors.163.com/ubuntu/ precise-proposed universe main
multiverse restricted\
 deb http://mirrors.163.com/ubuntu/ precise-backports universe main
multiverse restricted\
 deb-src http://mirrors.163.com/ubuntu/ precise-backports universe main
multiverse restricted\
 deb-src http://mirrors.163.com/ubuntu/ precise-updates universe main
multiverse restricted\
 \#搜狐的源\
 deb http://mirrors.sohu.com/ubuntu/ precise main restricted\
 deb-src http://mirrors.sohu.com/ubuntu/ precise main restricted\
 deb http://mirrors.sohu.com/ubuntu/ precise-updates main restricted\
 deb-src http://mirrors.sohu.com/ubuntu/ precise-updates main
restricted\
 deb http://mirrors.sohu.com/ubuntu/ precise universe\
 deb-src http://mirrors.sohu.com/ubuntu/ precise universe\
 deb http://mirrors.sohu.com/ubuntu/ precise-updates universe\
 deb-src http://mirrors.sohu.com/ubuntu/ precise-updates universe\
 deb http://mirrors.sohu.com/ubuntu/ precise multiverse\
 deb-src http://mirrors.sohu.com/ubuntu/ precise multiverse\
 deb http://mirrors.sohu.com/ubuntu/ precise-updates multiverse\
 deb-src http://mirrors.sohu.com/ubuntu/ precise-updates multiverse\
 deb http://mirrors.sohu.com/ubuntu/ precise-backports main restricted
universe multiverse\
 deb-src http://mirrors.sohu.com/ubuntu/ precise-backports main
restricted universe multiverse\
 deb http://mirrors.sohu.com/ubuntu/ precise-security main restricted\
 deb-src http://mirrors.sohu.com/ubuntu/ precise-security main
restricted\
 deb http://mirrors.sohu.com/ubuntu/ precise-security universe\
 deb-src http://mirrors.sohu.com/ubuntu/ precise-security universe\
 deb http://mirrors.sohu.com/ubuntu/ precise-security multiverse\
 deb-src http://mirrors.sohu.com/ubuntu/ precise-security multiverse\
 deb http://extras.ubuntu.com/ubuntu precise main\
 deb-src http://extras.ubuntu.com/ubuntu precise main\
 \#台湾源\
 deb http://tw.archive.ubuntu.com/ubuntu/ precise main universe
restricted multiverse\
 deb-src http://tw.archive.ubuntu.com/ubuntu/ precise main universe
restricted multiverse\
 deb http://tw.archive.ubuntu.com/ubuntu/ precise-security universe main
multiverse restricted\
 deb-src http://tw.archive.ubuntu.com/ubuntu/ precise-security universe
main multiverse restricted\
 deb http://tw.archive.ubuntu.com/ubuntu/ precise-updates universe main
multiverse restricted\
 deb-src http://tw.archive.ubuntu.com/ubuntu/ precise-updates universe
main multiverse restricted

\#骨头源，骨头源是bones7456架设的一个Ubuntu源 ，提供ubuntu,deepin\
 deb http://ubuntu.srt.cn/ubuntu/ precise main universe restricted
multiverse\
 deb-src http://ubuntu.srt.cn/ubuntu/ precise main universe restricted
multiverse\
 deb http://ubuntu.srt.cn/ubuntu/ precise-security universe main
multiverse restricted\
 deb-src http://ubuntu.srt.cn/ubuntu/ precise-security universe main
multiverse restricted\
 deb http://ubuntu.srt.cn/ubuntu/ precise-updates universe main
multiverse restricted\
 deb http://ubuntu.srt.cn/ubuntu/ precise-proposed universe main
multiverse restricted\
 deb-src http://ubuntu.srt.cn/ubuntu/ precise-proposed universe main
multiverse restricted\
 deb http://ubuntu.srt.cn/ubuntu/ precise-backports universe main
multiverse restricted\
 deb-src http://ubuntu.srt.cn/ubuntu/ precise-backports universe main
multiverse restricted\
 deb-src http://ubuntu.srt.cn/ubuntu/ precise-updates universe main
multiverse restricted

\#mirror.lupaworld.com的源，速度很快\
 deb http://mirror.lupaworld.com/ubuntu/archive/ precise main restricted
universe multiverse\
 deb http://mirror.lupaworld.com/ubuntu/archive/ precise-security main
restricted universe multiverse\
 deb http://mirror.lupaworld.com/ubuntu/archive/ precise-updates main
restricted universe multiverse\
 deb http://mirror.lupaworld.com/ubuntu/archive/ precise-backports main
restricted universe multiverse\
 deb http://mirror.lupaworld.com/ubuntu/ubuntu-cn/ precise main
restricted universe multiverse

\#ubuntu.cn99.com源（推荐）:\
 deb http://ubuntu.cn99.com/ubuntu/ precise main restricted universe
multiverse\
 deb http://ubuntu.cn99.com/ubuntu/ precise-updates main restricted
universe multiverse\
 deb http://ubuntu.cn99.com/ubuntu/ precise-security main restricted
universe multiverse\
 deb http://ubuntu.cn99.com/ubuntu/ precise-backports main restricted
universe multiverse\
 deb http://ubuntu.cn99.com/ubuntu-cn/ precise main restricted universe
multiverse

\#教育网源\
 \#电子科技大学\
 deb http://ubuntu.uestc.edu.cn/ubuntu/ precise main restricted universe
multiverse\
 deb http://ubuntu.uestc.edu.cn/ubuntu/ precise-backports main
restricted universe multiverse\
 deb http://ubuntu.uestc.edu.cn/ubuntu/ precise-proposed main restricted
universe multiverse\
 deb http://ubuntu.uestc.edu.cn/ubuntu/ precise-security main restricted
universe multiverse\
 deb http://ubuntu.uestc.edu.cn/ubuntu/ precise-updates main restricted
universe multiverse\
 deb-src http://ubuntu.uestc.edu.cn/ubuntu/ precise main restricted
universe multiverse\
 deb-src http://ubuntu.uestc.edu.cn/ubuntu/ precise-backports main
restricted universe multiverse\
 deb-src http://ubuntu.uestc.edu.cn/ubuntu/ precise-proposed main
restricted universe multiverse\
 deb-src http://ubuntu.uestc.edu.cn/ubuntu/ precise-security main
restricted universe multiverse\
 deb-src http://ubuntu.uestc.edu.cn/ubuntu/ precise-updates main
restricted universe multiverse

\#中国科技大学\
 deb http://debian.ustc.edu.cn/ubuntu/ precise main restricted universe
multiverse\
 deb http://debian.ustc.edu.cn/ubuntu/ precise-backports restricted
universe multiverse\
 deb http://debian.ustc.edu.cn/ubuntu/ precise-proposed main restricted
universe multiverse\
 deb http://debian.ustc.edu.cn/ubuntu/ precise-security main restricted
universe multiverse\
 deb http://debian.ustc.edu.cn/ubuntu/ precise-updates main restricted
universe multiverse\
 deb-src http://debian.ustc.edu.cn/ubuntu/ precise main restricted
universe multiverse\
 deb-src http://debian.ustc.edu.cn/ubuntu/ precise-backports main
restricted universe multiverse\
 deb-src http://debian.ustc.edu.cn/ubuntu/ precise-proposed main
restricted universe multiverse\
 deb-src http://debian.ustc.edu.cn/ubuntu/ precise-security main
restricted universe multiverse\
 deb-src http://debian.ustc.edu.cn/ubuntu/ precise-updates main
restricted universe multiverse

\#北京理工大学\
 deb http://mirror.bjtu.edu.cn/ubuntu/ precise main multiverse
restricted universe\
 deb http://mirror.bjtu.edu.cn/ubuntu/ precise-backports main multiverse
restricted universe\
 deb http://mirror.bjtu.edu.cn/ubuntu/ precise-proposed main multiverse
restricted universe\
 deb http://mirror.bjtu.edu.cn/ubuntu/ precise-security main multiverse
restricted universe\
 deb http://mirror.bjtu.edu.cn/ubuntu/ precise-updates main multiverse
restricted universe\
 deb-src http://mirror.bjtu.edu.cn/ubuntu/ precise main multiverse
restricted universe\
 deb-src http://mirror.bjtu.edu.cn/ubuntu/ precise-backports main
multiverse restricted universe\
 deb-src http://mirror.bjtu.edu.cn/ubuntu/ precise-proposed main
multiverse restricted universe\
 deb-src http://mirror.bjtu.edu.cn/ubuntu/ precise-security main
multiverse restricted universe\
 deb-src http://mirror.bjtu.edu.cn/ubuntu/ precise-updates main
multiverse restricted universe

\#兰州大学\
 deb ftp://mirror.lzu.edu.cn/ubuntu/ precise main multiverse restricted
universe\
 deb ftp://mirror.lzu.edu.cn/ubuntu/ precise-backports main multiverse
restricted universe\
 deb ftp://mirror.lzu.edu.cn/ubuntu/ precise-proposed main multiverse
restricted universe\
 deb ftp://mirror.lzu.edu.cn/ubuntu/ precise-security main multiverse
restricted universe\
 deb ftp://mirror.lzu.edu.cn/ubuntu/ precise-updates main multiverse
restricted universe\
 deb ftp://mirror.lzu.edu.cn/ubuntu-cn/ precise main multiverse
restricted universe

\#上海交通大学\
 deb http://ftp.sjtu.edu.cn/ubuntu/ precise main multiverse restricted
universe\
 deb http://ftp.sjtu.edu.cn/ubuntu/ precise-backports main multiverse
restricted universe\
 deb http://ftp.sjtu.edu.cn/ubuntu/ precise-proposed main multiverse
restricted universe\
 deb http://ftp.sjtu.edu.cn/ubuntu/ precise-security main multiverse
restricted universe\
 deb http://ftp.sjtu.edu.cn/ubuntu/ precise-updates main multiverse
restricted universe\
 deb http://ftp.sjtu.edu.cn/ubuntu-cn/ precise main multiverse
restricted universe\
 deb-src http://ftp.sjtu.edu.cn/ubuntu/ precise main multiverse
restricted universe\
 deb-src http://ftp.sjtu.edu.cn/ubuntu/ precise-backports main
multiverse restricted universe\
 deb-src http://ftp.sjtu.edu.cn/ubuntu/ precise-proposed main multiverse
restricted universe\
 deb-src http://ftp.sjtu.edu.cn/ubuntu/ precise-security main multiverse
restricted universe\
 deb-src http://ftp.sjtu.edu.cn/ubuntu/ precise-updates main multiverse
restricted universe

\

本文链接地址: [http://www.maybe520.net/blog/a/424.html](http://www.maybe520.net/blog/a/424.html "ubuntu12.04 更新源地址列表")
