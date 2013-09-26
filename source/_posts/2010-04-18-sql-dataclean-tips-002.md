--- 
layout: post 
title: "拆分字符串为单条记录"
date: 2010-04-18 12:30
categories: data sciences
tags: sql
---

[![2010-04-18\_201757](/images/WindowsLiveWriter/cefc5b49342d/4AD8034B/20100418_201757_thumb.png "2010-04-18_201757")](http://blog.cnpc.ac.cn/Blogs/images/WindowsLiveWriter/cefc5b49342d/19B3A749/20100418_201757.png)

原来的数据如上图上图，需要得到的结果如下图

[![2010-04-18\_202054](/images/WindowsLiveWriter/cefc5b49342d/3679EFD3/20100418_202054_thumb.png "2010-04-18_202054")](http://blog.cnpc.ac.cn/Blogs/images/WindowsLiveWriter/cefc5b49342d/552E490D/20100418_202054.png)

**sql语句如下：**

``` sql
SELECT  vo.name_id , COMNAME = SUBSTRING(vo.COMNAME, number, CHARINDEX(',', vo.COMNAME + ',', number) - b.number) FROM    dbo.verna_org AS vo
JOIN master..spt_values b ON b.type = 'p'
AND CHARINDEX(',', ',' + vo.COMNAME, number) = number
```
