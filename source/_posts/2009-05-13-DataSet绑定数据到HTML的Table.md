---
layout: post
title: DataSet绑定数据到HTML的Table
date: 2009-05-13 22:04:46
comments: true
sharing: true
categories: linux
tags: 
---

<h3><font color="#800000">执行效果图</font></h3>  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:8747F07C-CDE8-481f-B0DF-C6CFD074BF67:a7d1dd3f-7071-4d0c-9c4c-d60a4d432985" class="wlWriterEditableSmartContent"><a href="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/DataSetHTMLTable/56D3D07E/20090513_2201308x6.jpg" title="虎克的博客" rel="thumbnail"><img border="0" src="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/DataSetHTMLTable/4039344A/20090513_220130.png" width="420" height="393" /></a></div>  <h3><font color="#800000">Default2.aspx页面代码</font></h3>  <p>&#160;</p>  <div class="csharpcode">   <pre class="alt"><span class="asp">&lt;%@ Page Language=&quot;C#&quot; AutoEventWireup=&quot;true&quot; CodeFile=&quot;Default2.aspx.cs&quot; Inherits=&quot;Default2&quot; %&gt;</span></pre>

  <pre>&#160;</pre>

  <pre class="alt"><span class="kwrd">&lt;!</span><span class="html">DOCTYPE</span> <span class="attr">html</span> <span class="attr">PUBLIC</span> <span class="kwrd">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot;</span> <span class="kwrd">&quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre>&#160;</pre>

  <pre class="alt"><span class="kwrd">&lt;</span><span class="html">html</span> <span class="attr">xmlns</span><span class="kwrd">=&quot;http://www.w3.org/1999/xhtml&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd">&lt;</span><span class="html">head</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">    <span class="kwrd">&lt;</span><span class="html">title</span><span class="kwrd">&gt;&lt;/</span><span class="html">title</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd">&lt;/</span><span class="html">head</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt"><span class="kwrd">&lt;</span><span class="html">body</span><span class="kwrd">&gt;</span></pre>

  <pre>    <span class="kwrd">&lt;</span><span class="html">form</span> <span class="attr">id</span><span class="kwrd">=&quot;form1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">    <span class="kwrd">&lt;</span><span class="html">div</span> <span class="attr">id</span><span class="kwrd">=&quot;display&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span>Table Will Go Here<span class="kwrd">&lt;/</span><span class="html">div</span><span class="kwrd">&gt;</span></pre>

  <pre>&#160;</pre>

  <pre class="alt">    <span class="kwrd">&lt;/</span><span class="html">form</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd">&lt;/</span><span class="html">body</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt"><span class="kwrd">&lt;/</span><span class="html">html</span><span class="kwrd">&gt;</span></pre>
</div>
<style type="text/css">

.csharpcode, .csharpcode pre
{
	font-size: small;
	color: black;
	font-family: consolas, "Courier New", courier, monospace;
	background-color: #ffffff;
	/*white-space: pre;*/
}
.csharpcode pre { margin: 0em; }
.csharpcode .rem { color: #008000; }
.csharpcode .kwrd { color: #0000ff; }
.csharpcode .str { color: #006080; }
.csharpcode .op { color: #0000c0; }
.csharpcode .preproc { color: #cc6633; }
.csharpcode .asp { background-color: #ffff00; }
.csharpcode .html { color: #800000; }
.csharpcode .attr { color: #ff0000; }
.csharpcode .alt 
{
	background-color: #f4f4f4;
	width: 100%;
	margin: 0em;
}
.csharpcode .lnum { color: #606060; }</style>

<p></p>

<h3><font color="#800000">Default.aspx.cs后台代码</font></h3>

<p>&#160;</p>

<div class="csharpcode">
  <pre class="alt"><span class="lnum">   1:  </span><span class="kwrd">using</span> System;</pre>

  <pre><span class="lnum">   2:  </span><span class="kwrd">using</span> System.Data;</pre>

  <pre class="alt"><span class="lnum">   3:  </span><span class="kwrd">using</span> System.Data.SqlClient;</pre>

  <pre><span class="lnum">   4:  </span><span class="kwrd">using</span> System.Web.Configuration;</pre>

  <pre class="alt"><span class="lnum">   5:  </span>&#160;</pre>

  <pre><span class="lnum">   6:  </span><span class="kwrd">public</span> <span class="kwrd">partial</span> <span class="kwrd">class</span> Default2 : System.Web.UI.Page</pre>

  <pre class="alt"><span class="lnum">   7:  </span>{</pre>

  <pre><span class="lnum">   8:  </span>    <span class="kwrd">protected</span> <span class="kwrd">void</span> Page_Load(<span class="kwrd">object</span> sender, EventArgs e)</pre>

  <pre class="alt"><span class="lnum">   9:  </span>    {</pre>

  <pre><span class="lnum">  10:  </span>        <span class="rem">// Connection set up</span></pre>

  <pre class="alt"><span class="lnum">  11:  </span>        String strConnection = WebConfigurationManager.ConnectionStrings[<span class="str">&quot;NorthWind&quot;</span>].ConnectionString;</pre>

  <pre><span class="lnum">  12:  </span>&#160;</pre>

  <pre class="alt"><span class="lnum">  13:  </span>        SqlConnection objConnection = <span class="kwrd">new</span> SqlConnection(strConnection);</pre>

  <pre><span class="lnum">  14:  </span>        String strSQL = <span class="str">&quot;SELECT ProductName, UnitsInStock FROM Products&quot;</span>;</pre>

  <pre class="alt"><span class="lnum">  15:  </span>        <span class="rem">// DataAdapter setup</span></pre>

  <pre><span class="lnum">  16:  </span>        SqlDataAdapter objAdapter = <span class="kwrd">new</span> SqlDataAdapter(strSQL, objConnection);</pre>

  <pre class="alt"><span class="lnum">  17:  </span>        <span class="rem">// DataSet &amp; Adapter &amp; Table</span></pre>

  <pre><span class="lnum">  18:  </span>        DataSet objDataSet = <span class="kwrd">new</span> DataSet();</pre>

  <pre class="alt"><span class="lnum">  19:  </span>        objAdapter.Fill(objDataSet, <span class="str">&quot;dtProducts&quot;</span>);</pre>

  <pre><span class="lnum">  20:  </span>        String strResultsHolder;</pre>

  <pre class="alt"><span class="lnum">  21:  </span>        strResultsHolder = <span class="str">&quot;&lt;table width=80% border=1&gt;&quot;</span>;</pre>

  <pre><span class="lnum">  22:  </span>        strResultsHolder += <span class="str">&quot;&lt;tr&gt;&quot;</span>;</pre>

  <pre class="alt"><span class="lnum">  23:  </span>        <span class="kwrd">foreach</span> (DataColumn c <span class="kwrd">in</span> objDataSet.Tables[<span class="str">&quot;dtProducts&quot;</span>].Columns)</pre>

  <pre><span class="lnum">  24:  </span>        {</pre>

  <pre class="alt"><span class="lnum">  25:  </span>            strResultsHolder += <span class="str">&quot;&lt;td&gt;&quot;</span> + c.ColumnName + <span class="str">&quot;&lt;/td&gt;&quot;</span>;</pre>

  <pre><span class="lnum">  26:  </span>        }</pre>

  <pre class="alt"><span class="lnum">  27:  </span>        strResultsHolder += <span class="str">&quot;&lt;/tr&gt;&quot;</span>;</pre>

  <pre><span class="lnum">  28:  </span>        <span class="kwrd">int</span> <span class="kwrd">value</span>, blankValue;</pre>

  <pre class="alt"><span class="lnum">  29:  </span>        <span class="kwrd">foreach</span> (DataRow r <span class="kwrd">in</span> objDataSet.Tables[<span class="str">&quot;dtProducts&quot;</span>].Rows)</pre>

  <pre><span class="lnum">  30:  </span>        {</pre>

  <pre class="alt"><span class="lnum">  31:  </span>            <span class="kwrd">value</span> = 100 * Convert.ToInt32(r[<span class="str">&quot;UnitsInStock&quot;</span>]) / 125;</pre>

  <pre><span class="lnum"