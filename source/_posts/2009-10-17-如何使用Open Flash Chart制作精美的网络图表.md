---
layout: post
title: 如何使用Open Flash Chart制作精美的网络图表
date: 2009-10-17 17:33:19
comments: true
sharing: true
categories: linux
tags: 
---

<p><a href="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=20091017_165945.png"><img title="2009-10-17_165945" style="border-top-width: 0px; display: inline; border-left-width: 0px; border-bottom-width: 0px; border-right-width: 0px" height="257" alt="2009-10-17_165945" src="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=20091017_165945_thumb.png" width="399" border="0" /></a> </p>  <p>Open Flash Chart .NET </p>  <p>Open Flash Chart .NET (OFC.NET)是基于Open Flash Chart项目，网址在<a href="http://teethgrinder.co.uk/open-flash-chart">http://teethgrinder.co.uk/open-flash-chart</a> (或者 <a href="http://sourceforge.net/projects/openflashchart/">SourceForge</a>). 也可以通过SVN获得源码：<a href="http://svn.k2colocation.com/svn/OpenFlashChart">http://svn.k2colocation.com/svn/OpenFlashChart</a>. </p>  <p>安装步骤<strong>:</strong> </p>  <p>1、首先在应用程序(.net项目)根目录下建立<em><strong>aspnet_client</strong></em>文件夹。 </p>  <p>2、<em>在aspnet_client</em>文件夹下在建一个文件夹<em><strong>OpenFlashCh</strong>art</em>. </p>  <p>3、在<em>OpenFlashChart</em>文件夹下再建一个文件夹<strong>js</strong>，同时添加文件<font color="#ff0000">o<em>pen-flash-chart.swf</em></font> </p>  <p>4、js文件夹要添加文件<em><font color="#ff0000">swfobject.js</font></em> </p>  <p><em>5、</em>添加对<font color="#ff0000">OpenFlashChart.dll</font>的引用 </p>  <p>6、添加Defaul.aspx和Data.aspx两个页面 </p>  <p>项目的文件夹结构如下图： </p>  <p><a href="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=20091017_171249.png"><img title="2009-10-17_171249" style="border-top-width: 0px; display: inline; border-left-width: 0px; border-bottom-width: 0px; border-right-width: 0px" height="772" alt="2009-10-17_171249" src="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=20091017_171249_thumb.png" width="271" border="0" /></a> </p>  <p>在页面中调用OFC.NET需要首先注册程序集，在Default.aspx页面顶部添加如下语句 </p>  <pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@</span><span style="color: #a31515">Register </span><span style="color: red">TagPrefix</span><span style="color: blue">=&quot;ofc&quot; </span><span style="color: red">Namespace</span><span style="color: blue">=&quot;OpenFlashChart&quot; </span><span style="color: red">Assembly</span><span style="color: blue">=&quot;OpenFlashChart&quot; </span><span style="background: #ffee62">%&gt;</span> </pre>
<a href="http://11011.net/software/vspaste"></a>

<p>然后在页面中添加控件，代码如下： </p>

<pre class="code">    <span style="color: blue">&lt;</span><span style="color: #a31515">ofc</span><span style="color: blue">:</span><span style="color: #a31515">Chart </span><span style="color: red">ID</span><span style="color: blue">=&quot;Chart&quot; </span><span style="color: red">Height</span><span style="color: blue">=&quot;500&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;800&quot; </span><span style="color: red">Url</span><span style="color: blue">=&quot;data.aspx&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt; </span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p><strong>Data.aspx.cs</strong>文件的代码如下： </p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Web;
<span style="color: blue">using </span>System.Web.UI;
<span style="color: blue">using </span>System.Web.UI.WebControls;
<span style="color: blue">using </span>OpenFlashChart;
<span style="color: blue">using </span>System.Collections;

<span style="color: blue">namespace </span>OpenFlashChartDemo
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">data </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: #2b91af">Graph </span>graph = <span style="color: blue">new </span><span style="color: #2b91af">Graph</span>();
            graph.LegendX = <span style="color: blue">new </span><span style="color: #2b91af">LegendX</span>(<span style="color: #a31515">&quot;大类群统计&quot;</span>, 12, <span style="color: #a31515">&quot;#FF0000&quot;</span>);
            graph.LabelsX.Add(<span style="color: #a31515">&quot;苔藓&quot;</span>);
            graph.LabelsX.Add(<span style="color: #a31515">&quot;蕨类&quot;</span>);
            graph.LabelsX.Add(<span style="color: #a31515">&quot;裸子植物&quot;</span>);
            graph.LabelsX.Add(<span style="color: #a31515">&quot;被子植物&quot;</span>);
            graph.StepsY = 5;
            graph.MaxY = 50;
            OpenFlashChart.Charts.<span style="color: #2b91af">ChartData </span>temp;
            <span style="color: green">//Bar(alpha (transparency), color (Hex), Label, Line Size)        
            </span>temp = <span style="color: blue">new </span>OpenFlashChart.Charts.<span style="color: #2b91af">Bar</span>(75, <span style="color: #a31515">&quot;#FF0000&quot;</span>, <span style="color: #a31515">&quot;Sales&quot;</span>, 2);
            temp.Data.Add(20);
            temp.Data.Add(30);
            temp.Data.Add(40);
            temp.Data.Add(10);
            graph.Data.Add(temp);
            Response.Clear();
            Response.Write(graph.ToString());
            Response.End();           

        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<pre class="code">可以在这里下载整个程序和示例文件包<a href="/Blogs/file.axd?file=2009%2f10%2fOpenFlash.rar">OpenFlash.rar (369.61 kb)</a></pre>