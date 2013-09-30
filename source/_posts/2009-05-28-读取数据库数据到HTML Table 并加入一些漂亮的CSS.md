---
layout: post
title: 读取数据库数据到HTML Table 并加入一些漂亮的CSS
date: 2009-05-28 13:39:35
comments: true
sharing: true
categories: linux
tags: 
---

<h2>效果图</h2>  <p><a href="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/edb0d7de12e0/352A5F48/20090528_00079.jpg"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="2009-05-28_00079" border="0" alt="2009-05-28_00079" src="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/edb0d7de12e0/78262DB5/20090528_00079_thumb.jpg" width="644" height="214" /></a> </p>  <h2>Default.aspx</h2>  <pre class="csharpcode"><span class="asp">&lt;%@ Page Language=&quot;C#&quot; AutoEventWireup=&quot;true&quot; CodeFile=&quot;Default.aspx.cs&quot; Inherits=&quot;_Default&quot; %&gt;</span>

<span class="kwrd">&lt;!</span><span class="html">DOCTYPE</span> <span class="attr">html</span> <span class="attr">PUBLIC</span> <span class="kwrd">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot;</span> <span class="kwrd">&quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;</span><span class="kwrd">&gt;</span>
<span class="kwrd">&lt;</span><span class="html">html</span> <span class="attr">xmlns</span><span class="kwrd">=&quot;http://www.w3.org/1999/xhtml&quot;</span><span class="kwrd">&gt;</span>
<span class="kwrd">&lt;</span><span class="html">head</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;</span><span class="html">title</span><span class="kwrd">&gt;&lt;/</span><span class="html">title</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;</span><span class="html">style</span><span class="kwrd">&gt;</span></pre>

<pre class="csharpcode"><span class="kwrd">//见附件</span></pre>

<pre class="csharpcode"><span class="kwrd"></span><span class="kwrd">&lt;/</span><span class="html">style</span><span class="kwrd">&gt;</span>
<span class="kwrd">&lt;/</span><span class="html">head</span><span class="kwrd">&gt;</span>
<span class="kwrd">&lt;</span><span class="html">body</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;</span><span class="html">form</span> <span class="attr">id</span><span class="kwrd">=&quot;form1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;</span><span class="html">div</span><span class="kwrd">&gt;</span>
        <span class="kwrd">&lt;</span><span class="html">div</span> <span class="attr">id</span><span class="kwrd">=&quot;display&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span>
            中国高等植物名录<span class="kwrd">&lt;/</span><span class="html">div</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;/</span><span class="html">div</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;/</span><span class="html">form</span><span class="kwrd">&gt;</span>
<span class="kwrd">&lt;/</span><span class="html">body</span><span class="kwrd">&gt;</span>
<span class="kwrd">&lt;/</span><span class="html">html</span><span class="kwrd">&gt;</span></pre>

<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:fb3a1972-4489-4e52-abe7-25a00bb07fdf:92d50799-44df-4802-9477-a72fd58361d7" class="wlWriterEditableSmartContent"><p> <a href="http://blog.cnpc.ac.cn/Blogs/file.axd?file=WindowsLiveWriter/edb0d7de12e0/12F253C2/table_design.css" target="_blank">CSS File</a></p></div>
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

<h2>Default.aspx.cs</h2>

<p>&#160;</p>

<div class="csharpcode">
  <pre class="alt"><span class="kwrd">using</span> System;</pre>

  <pre><span class="kwrd">using</span> System.Data;</pre>

  <pre class="alt"><span class="kwrd">using</span> System.Data.SqlClient;</pre>

  <pre><span class="kwrd">using</span> System.Web.Configuration;</pre>

  <pre class="alt">&#160;</pre>

  <pre><span class="kwrd">public</span> <span class="kwrd">partial</span> <span class="kwrd">class</span> _Default : System.Web.UI.Page</pre>

  <pre class="alt">{</pre>

  <pre>    <span class="kwrd">protected</span> <span class="kwrd">void</span> Page_Load(<span class="kwrd">object</span> sender, EventArgs e)</pre>

  <pre class="alt">    {</pre>

  <pre>        <span class="rem">// Connection set up</span></pre>

  <pre class="alt">        String strConnection = WebConfigurationManager.ConnectionStrings[<span class="str">&quot;CNPCEditConnectionString&quot;</span>].ConnectionString;</pre>

  <pre>&#160;</pre>

  <pre class="alt">        SqlConnection objConnection = <span class="kwrd">new</span> SqlConnection(strConnection);</pre>

  <pre>        String strSQL = <span class="str">&quot;SELECT FamilyName, FamilyNameCh,FamilyID from Family&quot;</span>;</pre>

  <pre class="alt">        <span class="rem">// DataAdapter setup</span></pre>

  <pre>        SqlDataAdapter objAdapter = <span class="kwrd">new</span> SqlDataAdapter(strSQL, objConnection);</pre>

  <pre class="alt">        <span class="rem">// DataSet &amp; Adapter &amp; Table</span></pre>

  <pre>        DataSet objDataSet = <span class="kwrd">new</span> DataSet();</pre>

  <pre class="alt">        objAdapter.Fill(objDataSet, <span class="str">&quot;Family&quot;</span>);</pre>

  <pre>        String strResultsHolder;</pre>

  <pre class="alt">        strResultsHolder = <span class="str">&quot;&lt;table&gt;&quot;</span>;</pre>

  <pre>        strResultsHolder += <span class="str">&quot;&lt;tr&gt;&quot;</span>;</pre>

  <pre class="alt">        <span class="rem">//Change the column header name</span></pre>

  <pre>        objDataSet.Tables[<span class="str">&quot;Family&quot;</span>].Columns[0].ColumnName = <span class="str">&quot;科学名&quot;</span>;</pre>

  <pre class="alt">        objDataSet.Tables[<span class="str">&quot;Family&quot;</span>].Columns[1].ColumnName = <span class="str">&quot;科中文名&quot;</span>;</pre>

  <pre>        objDataSet.Tables[<span class="str">&quot;Family&quot;</span>].Columns[2].ColumnName = <span class="str">&quot;科编号&quot;</span>;</pre>

  <pre class="alt">        <span class="kwrd">foreach</span> (DataColumn c <span class="kwrd">in</span> objDataSet.Tables[<span class="str">&quot;Family&quot;</span>].Columns)</pre>

  <pre>        {</pre>

  <pre class="alt">            strResultsHolder += <span class="str">&quot;&lt;td&gt;&quot;</span> + c.ColumnName + <span class="str">&quot;&lt;/td&gt;&quot;</span>;</pre>

  <pre>        }</pre>

  <pre class="alt">        strResultsHolder += <span class="str">&quot;&lt;/tr&gt;&quot;</span>;</pre>

  <pre>        <span class="kwrd">foreach</span> (DataRow r <span class="kwrd">in</span> objDataSet.Tables[<span class="str">&quot;Family&quot;</span>].Rows)</pre>

  <pre class="alt">        {</pre>

  <pre>            strResultsHolder += <span class="str">&quot;&lt;tr&gt;&lt;td width=5%&gt;&quot;</span> + r[<span class="str">&quot;科学名&quot;</span>] + <span class="str">&quot;&lt;td width=5%&gt;&quot;</span> + r[<span class="str">&quot;科中文名&quot;</span>] + <span class="str">&quot;&lt;td width=5%&gt;&quot;</span> + r[<span class="str">&quot;科编号&quot;</span>] + <span class="str">&quot;&lt;/td&gt;&lt;