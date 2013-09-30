---
layout: post
title: XML学习笔记(三)：写入XML文档的XmlTextWriter
date: 2009-05-09 16:31:45
comments: true
sharing: true
categories: linux
tags: 
---

<p>页面代码：</p>  <div class="csharpcode">   <pre class="alt"><span class="asp">&lt;%@ Page Language=&quot;C#&quot; AutoEventWireup=&quot;true&quot; CodeFile=&quot;WriteXML.aspx.cs&quot; Inherits=&quot;WriteXML&quot; %&gt;</span></pre>

  <pre>&#160;</pre>

  <pre class="alt"><span class="kwrd">&lt;!</span><span class="html">DOCTYPE</span> <span class="attr">html</span> <span class="attr">PUBLIC</span> <span class="kwrd">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot;</span> <span class="kwrd">&quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd">&lt;</span><span class="html">html</span> <span class="attr">xmlns</span><span class="kwrd">=&quot;http://www.w3.org/1999/xhtml&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt"><span class="kwrd">&lt;</span><span class="html">head</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre>    <span class="kwrd">&lt;</span><span class="html">title</span><span class="kwrd">&gt;&lt;/</span><span class="html">title</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt"><span class="kwrd">&lt;/</span><span class="html">head</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd">&lt;</span><span class="html">body</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">    <span class="kwrd">&lt;</span><span class="html">form</span> <span class="attr">id</span><span class="kwrd">=&quot;form1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre>    <span class="kwrd">&lt;</span><span class="html">div</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">        ConnecionString:</pre>

  <pre>        <span class="kwrd">&lt;</span><span class="html">asp:TextBox</span> <span class="attr">ID</span><span class="kwrd">=&quot;TextBox1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">Height</span><span class="kwrd">=&quot;70px&quot;</span> <span class="attr">Width</span><span class="kwrd">=&quot;531px&quot;</span><span class="kwrd">&gt;&lt;/</span><span class="html">asp:TextBox</span><span class="kwrd">&gt;&lt;</span><span class="html">br</span> <span class="kwrd">/&gt;</span></pre>

  <pre class="alt">        Table Name:</pre>

  <pre>        <span class="kwrd">&lt;</span><span class="html">asp:TextBox</span> <span class="attr">ID</span><span class="kwrd">=&quot;TextBox2&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">Height</span><span class="kwrd">=&quot;48px&quot;</span> <span class="attr">Width</span><span class="kwrd">=&quot;525px&quot;</span><span class="kwrd">&gt;&lt;/</span><span class="html">asp:TextBox</span><span class="kwrd">&gt;&lt;</span><span class="html">br</span> <span class="kwrd">/&gt;</span></pre>

  <pre class="alt">        Destination File Name:</pre>

  <pre>        <span class="kwrd">&lt;</span><span class="html">asp:TextBox</span> <span class="attr">ID</span><span class="kwrd">=&quot;TextBox3&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">Height</span><span class="kwrd">=&quot;56px&quot;</span> <span class="attr">Width</span><span class="kwrd">=&quot;519px&quot;</span><span class="kwrd">&gt;&lt;/</span><span class="html">asp:TextBox</span><span class="kwrd">&gt;&lt;</span><span class="html">br</span> <span class="kwrd">/&gt;</span></pre>

  <pre class="alt">    <span class="kwrd">&lt;/</span><span class="html">div</span><span class="kwrd">&gt;</span></pre>

  <pre>    <span class="kwrd">&lt;</span><span class="html">asp:RadioButton</span> <span class="attr">ID</span><span class="kwrd">=&quot;RadioButton1&quot;</span> <span class="attr">Text</span><span class="kwrd">=&quot;Columns as elements&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">GroupName</span><span class="kwrd">=&quot;ExportType&quot;</span> <span class="kwrd">/&gt;</span></pre>

  <pre class="alt">    <span class="kwrd">&lt;</span><span class="html">br</span> <span class="kwrd">/&gt;</span></pre>

  <pre>    <span class="kwrd">&lt;</span><span class="html">asp:RadioButton</span> <span class="attr">ID</span><span class="kwrd">=&quot;RadioButton2&quot;</span> <span class="attr">Text</span><span class="kwrd">=&quot;Columns as attributes&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">GroupName</span><span class="kwrd">=&quot;ExportType&quot;</span> <span class="kwrd">/&gt;</span></pre>

  <pre class="alt">    <span class="kwrd">&lt;</span><span class="html">br</span> <span class="kwrd">/&gt;</span></pre>

  <pre>    <span class="kwrd">&lt;</span><span class="html">asp:Button</span> <span class="attr">ID</span><span class="kwrd">=&quot;Button1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">Height</span><span class="kwrd">=&quot;31px&quot;</span> <span class="attr">Text</span><span class="kwrd">=&quot;Export Data&quot;</span> <span class="attr">Width</span><span class="kwrd">=&quot;134px&quot;</span></pre>

  <pre class="alt">        <span class="attr">OnClick</span><span class="kwrd">=&quot;Button1_Click&quot;</span> <span class="kwrd">/&gt;</span></pre>

  <pre>    <span class="kwrd">&lt;/</span><span class="html">form</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt"><span class="kwrd">&lt;/</span><span class="html">body</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd">&lt;/</span><span class="html">html</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd"></span></pre>
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

<p>执行代码：</p>

<div class="csharpcode">
  <pre class="alt"><span class="lnum">   1:  </span><span class="kwrd">using</span> System;</pre>

  <pre><span class="lnum">   2:  </span><span class="kwrd">using</span> System.Data.SqlClient;</pre>

  <pre class="alt"><span class="lnum">   3:  </span><span class="kwrd">using</span> System.Xml;</pre>

  <pre><span class="lnum">   4:  </span>&#160;</pre>

  <pre class="alt"><span class="lnum">   5:  </span><span class="kwrd">public</span> <span class="kwrd">partial</span> <span class="kwrd">class</span> WriteXML : System.Web.UI.Page</pre>

  <pre><span class="lnum">   6:  </span>{</pre>

  <pre class="alt"><span class="lnum">   7:  </span>    <span class="kwrd">protected</span> <span class="kwrd">void</span> Page_Load(<span class="kwrd">object</span> sender, EventArgs e)</pre>

  <pre><span class="lnum">   8:  </span>    {</pre>

  <pre class="alt"><span class="lnum">   9:  </span>&#160;</pre>

  <pre><span class="lnum">  10:  </span>    }</pre>

  <pre class="alt"><span class="lnum">  11:  </span>    <span class="kwrd">protected</span> <span class="kwrd">void</span> Button1_Click(<span class="kwrd">object</span> sender, EventArgs e)</pre>

  <pre><span class="lnum">  12:  </span>    {</pre>

  <pre class="alt"><span class="lnum">  13:  </span>       