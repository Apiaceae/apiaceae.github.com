---
layout: post
title: 如何利用UBio的FindIT服务从文本和Word文档中提取拉丁学名
date: 2009-04-29 15:31:44
comments: true
sharing: true
categories: linux
tags: 
---

<p>
&nbsp;&nbsp; 下面两个图是我们经常在Word或文本文档中见到的物种名录最基本的格式
</p>
<p>
<a href="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_103612_2.png"><img style="border: 0px" src="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_103612_thumb.png" border="0" alt="2009-04-28_103612" width="616" height="484" /></a> <a href="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_103633_2.png"><img style="border: 0px" src="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_103633_thumb.png" border="0" alt="2009-04-28_103633" width="305" height="484" /></a> 
</p>
<p>
将上面这些文件中的名录数据Copy到一个单独的文本文件，然后上传到UBio的名录网络服务网站: <a href="http://www.ubio.org/tools/recognize.php" title="http://www.ubio.org/tools/recognize.php">http://www.ubio.org/tools/recognize.php</a>
</p>
<p>
<a href="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_105013_2.png"><img style="border: 0px" src="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_105013_thumb.png" border="0" alt="2009-04-28_105013" width="644" height="397" /></a> 
</p>
<p>
点击上图中的浏览按钮将文本文件上传，选中文件类型：File Type为Plain Text;然后下面有几个Parsing Algorithm的选项：TaxonFinder(忽略名录中的学名的作者字符串，仅仅通过名称来匹配和检查);Resolve Authors(包括拉丁学名中的作者来检查)。最后点击Submit按钮，返回的结果如下图：
</p>
<p>
<a href="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_104041_2.png"><img style="border: 0px" src="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_104041_thumb.png" border="0" alt="2009-04-28_104041" width="636" height="772" /></a> 
</p>
<p>
<a href="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_104107_2.png"><img style="border: 0px" src="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_104107_thumb.png" border="0" alt="2009-04-28_104107" width="655" height="610" /></a> 
</p>
<p>
<a href="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_104212_2.png"><img style="border: 0px" src="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_104212_thumb.png" border="0" alt="2009-04-28_104212" width="656" height="750" /></a> 
</p>
<p>
<a href="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_104234_2.png"><img style="border: 0px" src="/Blogs/image.axd?picture=WindowsLiveWriter/UBioFindITWord_9574/2009-04-28_104234_thumb.png" border="0" alt="2009-04-28_104234" width="657" height="828" /></a> 
</p>
<p>
如上图所示，系统服务通过给拉丁学名标记不同的颜色和积分值来说明这些拉丁学名检查的正确程度。
</p>
