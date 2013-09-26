---
layout: post
title: "ubuntu解压命令全览"
date: 2012-07-17 13:25
categories: Linux
tags: [ubuntu, tar]
---

**.tar**

解包：tar xvf FileName.tar

打包：tar cvf FileName.tar DirName

(注：tar是打包，不是压缩！）


**.gz**

解压1：gunzip FileName.gz
解压2：gzip -d FileName.gz<br /> 压缩：gzip FileName<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.tar.gz 和 .tgz</span></span></strong><br /> 解压：tar zxvf FileName.tar.gz<br /> 压缩：tar zcvf FileName.tar.gz DirName<br /> ---------------------------------------------<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.bz2</span></span></strong><br /> 解压1：bzip2 -d FileName.bz2<br /> 解压2：bunzip2 FileName.bz2<br /> 压缩： bzip2 -z FileName<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.tar.bz2</span></span></strong><br /> 解压：tar jxvf FileName.tar.bz2<br /> 压缩：tar jcvf FileName.tar.bz2 DirName<br /> ---------------------------------------------<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.bz</span></span></strong><br /> 解压1：bzip2 -d FileName.bz<br /> 解压2：bunzip2 FileName.bz<br /> 压缩：<span style="color: #ffa500;">未知</span><br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.tar.bz</span></span></strong><br /> 解压：tar jxvf FileName.tar.bz<br /> 压缩：<span style="color: #ffa500;">未知</span><br /> ---------------------------------------------<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.Z</span></span></strong><br /> 解压：uncompress FileName.Z<br /> 压缩：compress FileName<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.tar.Z</span></span></strong><br /> 解压：tar Zxvf FileName.tar.Z<br /> 压缩：tar Zcvf FileName.tar.Z DirName<br /> ---------------------------------------------<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.zip</span></span></strong><br /> 解压：unzip FileName.zip<br /> 压缩：zip FileName.zip DirName<br /> ---------------------------------------------<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.rar</span></span></strong><br /> 解压：rar x FileName.rar<br /> 压缩：rar a FileName.rar DirName<br /> <span style="color: #008000;"><br /> rar请到：<a style="color: #003793;" href="http://www.rarsoft.com/download.htm" target="_blank"><span style="color: #003793;">http://www.rarsoft.com/download.htm</span></a> 下载！<br /> 解压后请将rar_static拷贝到/usr/bin目录（其他由$PATH环境变量指定的目录也可以）：<br /> [root@www2 tmp]# cp rar_static /usr/bin/rar</span><br /> ---------------------------------------------<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.lha</span></span></strong><br /> 解压：lha -e FileName.lha<br /> 压缩：lha -a FileName.lha FileName<br /> <span style="color: #008000;"><br /> lha请到：<a style="color: #003793;" href="http://www.infor.kanazawa-it.ac.jp/%7Eishii/lhaunix/" target="_blank"><span style="color: #003793;">http://www.infor.kanazawa-it.ac.jp/~ishii/lhaunix/</span></a>下载！<br /> &gt;解压后请将lha拷贝到/usr/bin目录（其他由$PATH环境变量指定的目录也可以）：<br /> [root@www2 tmp]# cp lha /usr/bin/</span><br /> ---------------------------------------------<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.rpm</span></span></strong><br /> 解包：rpm2cpio FileName.rpm | cpio -div<br /> ---------------------------------------------<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.deb</span></span></strong><br /> 解包：ar p FileName.deb data.tar.gz | tar zxf -<br /> ---------------------------------------------<br /> <strong><span style="font-size: x-small;"><span style="color: #0000ff;">.tar .tgz .tar.gz .tar.Z .tar.bz .tar.bz2 .zip .cpio .rpm .deb .slp .arj .rar .ace .lha .lzh .lzx .lzs .arc .sda .sfx .lnx .zoo .cab .kar .cpt .pit .sit .sea</span></span></strong><br /> 解压：sEx x FileName.*<br /> 压缩：sEx a FileName.* FileName</p>
<p>文章转自：http://blog.csdn.net/zad522/article/details/2770446</p>
