---
layout: post
title: 如何更新Dell服务器的BIOS及Locale问题
date: 2012-10-22 15:30
categories: Linux
tags: 服务器
---
#Install libsmbios

,,,
$ apt-get update    (not always necessary)

$ apt-get install libsmbios-bin
,,,

# Get the System ID
$ getSystemId 
,,,
Libsmbios:    0.12.1

System ID: 0x01DD

Service Tag:  DT6WLB1

Express Service Code: 30063287773

Product Name: Dell DM061

BIOS Version: 2.3.2

Vendor:       Dell Inc.

Is Dell:      1
,,,

Download the latest BIOS ".HDR" file for this system. Go here: <a class="external free" href="http://linux.dell.com/repo/firmware/bios-hdrs/" rel="nofollow">http://linux.dell.com/repo/firmware/bios-hdrs/</a>. Scroll down the list to find a directory matching the System ID from the previous step. The directory will be named: system_bios_ven_0x1028_dev_<strong>SYSTEM_ID</strong>_version_<strong>BIOS_VERSION</strong>. Go into this directory and download the file, "bios.hdr".</li>
</ul>
<p><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"></span></span></p>
<ul>
<li>load the <strong>dell_rbu</strong> driver</li>
</ul>
<p><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"></span></span></p>
<pre># modprobe dell_rbu
</pre>
<p><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"></span></span></p>
<ul>
<li>update the bios</li>
</ul>
<p><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"></span></span></p>
<pre># dellBiosUpdate -u -f ./bios.hdr-2.3.2 
Supported RBU type for this system: (MONOLITHIC)
Using RBU v2 driver. Initializing Driver. 
Setting RBU type in v2 driver to: MONOLITHIC
Prep driver for data load.
Writing RBU data (4096bytes/dot): ............................
..............................................................
.......................
Notify driver data is finished.
Activate CMOS bit to notify BIOS that update is ready on next boot.
Update staged sucessfully. BIOS update will occur on next reboot.
</pre>
<p><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"></span></span></p>
<ul>
<li>reboot the system</li>
</ul>
<p><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"></span></span></p>
<pre># reboot
</pre>
<p><a href="http://linux.dell.com/wiki/index.php/Tech/libsmbios_dellBiosUpdate">http://linux.dell.com/wiki/index.php/Tech/libsmbios_dellBiosUpdate</a></p>
<p><span style="font-family: sans-serif; font-size: 13px; line-height: 19px;"></span>&nbsp;</p>
<h2 class="title content-title">典型错误：locale.Error：unsupported locale setting</h2>
<div id="content" class="content mod-cs-content text-content clearfix"><strong>&nbsp;locale.Error：unsupported locale setting<br /><br /><br /><br /></strong><strong>1、错误提出</strong><br />（1）locale指令运行出现的错误信息<br />locale：Cannot set LC_CTYPE to default locale： No such file or directory<br />locale：Cannot set LC_MESSAGES to default locale： No such file or directory<br />locale：Cannot set LC_ALL to default locale： No such file or directory<br />（2）setup指令运行出现的错误信息<br />locale.Error：unsupported locale setting，导致无法设置&ldquo;network configuration"<br />（3）yum指令运行出现的错误信息<br />Failed to set locale, defaulting to C<br /><img src="http://hiphotos.baidu.com/9812658/pic/item/03ca8c7109101d2c8601b07b.jpg" alt="" /><br /><img src="http://hiphotos.baidu.com/9812658/pic/item/61139699c5fff585c8eaf47b.jpg" alt="" /><br /><img src="http://hiphotos.baidu.com/9812658/pic/item/982718a3fbd4dcbb4610647b.jpg" alt="" /><br /><br /><br /><strong>2、分析原因</strong><br />locale是用来设置软件运行的语言环境，所以语言环境设置有问题<br /><br /><strong>3、解决故障<br /></strong>重新设置语言环境，最简单的解决办法，例如：<br />[root@Mylinux ~]#&nbsp; echo "export&nbsp; LC_ALL=en_US.UTF-8"&nbsp; &gt;&gt;&nbsp;&nbsp; /home/XXX/.bash_profile（特定用户）<br />或者<br />[root@Mylinux ~]#&nbsp; echo "export LC_ALL=en_US.UTF-8"&nbsp; &gt;&gt;&nbsp; /etc/profile（所有用户）<br />[root@Mylinux ~]#&nbsp; exit<br />然后重新登录，使用locale指令查看变量<br /><img src="http://hiphotos.baidu.com/9812658/pic/item/58f80bee1050cc1762d09ffa.jpg" alt="" /><br /><br />

*关于locale的设置，请查阅文章：《<span style="text-decoration: underline;"><strong><a href="http://hi.baidu.com/9812658/blog/item/d0021e33c0b32aa35fdf0e6c.html" target="_blank">Linux系统locale的设置</a></strong></span></div>
<p><a href="http://hi.baidu.com/linuxtrip/item/02b8c7774d7a70215d17893d">http://hi.baidu.com/linuxtrip/item/02b8c7774d7a70215d17893d</a></p>
<p>&nbsp;</p>
