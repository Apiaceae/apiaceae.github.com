---
layout: post
title: ObjectDataSource控件的分页、排序和筛选
date: 2009-03-13 11:53:21
comments: true
sharing: true
categories: linux
tags: 
---

<p>
ObjectDataSource控件提供了两种方法对绑定到控件(比如GridView)的数据进行分页和排序： 
</p>
<ol>
	<li>通过用户界面进行分页，优点是容易设置，缺点是当数据量大时执行效率较低； </li>
</ol>
<p>
实现方法： 
</p>
<ol>
	<li>对GridView控件使用正确的数据源，比如：DataSet, Collection, DataTable或者DataView，但不能使用DataReader </li>
	<li>在页面设置GridView控件分分页属性为True。<span style="font-size: 9pt; font-family: Consolas"><span style="color: red">AllowPaging</span><span style="color: blue">=&quot;True&quot;</span></span> </li>
</ol>
<p>
&nbsp;
</p>
<ol>
	<li>通过设置ObjectDataSource的分页，优点是数据量大时执行效率较高，特别是如果配合Caching能极大的提高以数据驱动为主的网络应用程序的效率。 </li>
</ol>
<p>
ObjectDataSource数据源的分页可以在类Class, 存储过程, LINQ to SQL查询中实现，下面以LINQ to SQL,Northwind数据库的Product表为例子来说明用法： 
</p>
<p>
实例网站的文档结构如下图： 
</p>
<p>
<img src="/Blogs/image.axd?picture=2009%2f3%2f04.png" alt="" width="276" height="264" /> 
</p>
<p>
1、新建网页，添加LINQ to SQL Class，命名为Products，在Server Exploer中拖拽Northwind数据库的Product表到设计界面。 
</p>
<p>
&nbsp;
</p>
<p>
<img style="width: 574px; height: 445px" src="/Blogs/image.axd?picture=2009%2f3%2f05.png" alt="" width="574" height="445" /> 
</p>
<p>
&nbsp;
</p>
<p>
<img style="width: 589px; height: 386px" src="/Blogs/image.axd?picture=2009%2f3%2f06.png" alt="" width="589" height="386" /> 
</p>
<p>
2、添加一个新类Class命名为roductsLINQPaging&nbsp;&nbsp; 
</p>
<p>
&nbsp;
</p>
<p>
<img style="width: 594px; height: 433px" src="/Blogs/image.axd?picture=2009%2f3%2f07.png" alt="" width="594" height="433" /> 
</p>
<p>
3、类中实现的方法如下：
</p>
<p>
<span style="color: #008080">&nbsp;1</span><img src="http://www.cnblogs.com/Images/OutliningIndicators/None.gif" alt="" width="11" height="16" align="top" /><span style="color: #0000ff">using</span><span style="color: #000000">&nbsp;System;<br />
</span><span style="color: #008080">&nbsp;2</span><span style="color: #000000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/None.gif" alt="" width="11" height="16" align="top" /></span><span style="color: #0000ff">using</span><span style="color: #000000">&nbsp;System.Collections.Generic;<br />
</span><span style="color: #008080">&nbsp;3</span><span style="color: #000000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/None.gif" alt="" width="11" height="16" align="top" /></span><span style="color: #0000ff">using</span><span style="color: #000000">&nbsp;System.Linq;<br />
</span><span style="color: #008080">&nbsp;4</span><span style="color: #000000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/None.gif" alt="" width="11" height="16" align="top" /></span><span style="color: #0000ff">using</span><span style="color: #000000">&nbsp;System.Data.Linq;<br />
</span><span style="color: #008080">&nbsp;5</span><span style="color: #000000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/None.gif" alt="" width="11" height="16" align="top" /></span><span style="color: #0000ff">using</span><span style="color: #000000">&nbsp;System.Web;<br />
</span><span style="color: #008080">&nbsp;6</span><span style="color: #000000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/None.gif" alt="" width="11" height="16" align="top" /><br />
</span><span style="color: #008080">&nbsp;7</span><span style="color: #000000"><img id="Codehighlighter1_110_186_Open_Image" src="http://www.cnblogs.com/Images/OutliningIndicators/ExpandedBlockStart.gif" alt="" width="11" height="16" align="top" /><img id="Codehighlighter1_110_186_Closed_Image" style="display: none" src="http://www.cnblogs.com/Images/OutliningIndicators/ContractedBlock.gif" alt="" width="11" height="16" align="top" /></span><span style="display: none; background-color: #ffffff; border: #808080 1px solid">/**/</span><span><span style="color: #808080">///</span><span style="color: #008000">&nbsp;</span><span style="color: #808080">&lt;summary&gt;</span><span style="color: #008000"><br />
</span><span style="color: #008080">&nbsp;8</span><span style="color: #008000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif" alt="" width="11" height="16" align="top" /></span><span style="color: #808080">///</span><span style="color: #008000">&nbsp;Summary&nbsp;description&nbsp;for&nbsp;ProductsLINQPaging<br />
</span><span style="color: #008080">&nbsp;9</span><span style="color: #008000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/ExpandedBlockEnd.gif" alt="" width="11" height="16" align="top" /></span><span style="color: #808080">///</span><span style="color: #008000">&nbsp;</span><span style="color: #808080">&lt;/summary&gt;</span></span><br />
<span style="color: #008080">10</span><img src="http://www.cnblogs.com/Images/OutliningIndicators/None.gif" alt="" width="11" height="16" align="top" /><span style="color: #0000ff">public</span><span style="color: #000000">&nbsp;</span><span style="color: #0000ff">class</span><span style="color: #000000">&nbsp;ProductsLINQPaging<br />
</span><span style="color: #008080">11</span><span style="color: #000000"><img id="Codehighlighter1_218_962_Open_Image" src="http://www.cnblogs.com/Images/OutliningIndicators/ExpandedBlockStart.gif" alt="" width="11" height="16" align="top" /><img id="Codehighlighter1_218_962_Closed_Image" style="display: none" src="http://www.cnblogs.com/Images/OutliningIndicators/ContractedBlock.gif" alt="" width="11" height="16" align="top" /></span><span style="display: none; background-color: #ffffff; border: #808080 1px solid"><img src="http://www.cnblogs.com/Images/dot.gif" alt="" width="15" height="20" /></span><span><span style="color: #000000">{<br />
</span><span style="color: #008080">12</span><span style="color: #000000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif" alt="" width="11" height="16" align="top" />&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color: #0000ff">public</span><span style="color: #000000">&nbsp;ProductsLINQPaging()<br />
</span><span style="color: #008080">13</span><span style="color: #000000"><img id="Codehighlighter1_250_302_Open_Image" src="http://www.cnblogs.com/Images/OutliningIndicators/ExpandedSubBlockStart.gif" alt="" width="11" height="16" align="top" /><img id="Codehighlighter1_250_302_Closed_Image" style="display: none" src="http://www.cnblogs.com/Images/OutliningIndicators/ContractedSubBlock.gif" alt="" width="11" height="16" align="top" />&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="display: none; background-color: #ffffff; border: #808080 1px solid"><img src="http://www.cnblogs.com/Images/dot.gif" alt="" width="15" height="20" /></span><span><span style="color: #000000">{<br />
</span><span style="color: #008080">14</span><span style="color: #000000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif" alt="" width="11" height="16" align="top" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color: #008000">//</span><span style="color: #008000"><br />
</span><span style="color: #008080">15</span><span style="color: #008000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif" alt="" width="11" height="16" align="top" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color: #008000">//</span><span style="color: #008000">&nbsp;TODO:&nbsp;Add&nbsp;constructor&nbsp;logic&nbsp;here<br />
</span><span style="color: #008080">16</span><span style="color: #008000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif" alt="" width="11" height="16" align="top" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color: #008000">//<br />
</span><span style="color: #008080">17</span><span style="color: #008000"><img src="http://www.cnblogs.com/Images/OutliningIndicators/ExpandedSubBlockEnd.gif" alt="" width="11" height="16" align="top" /></span><span sty