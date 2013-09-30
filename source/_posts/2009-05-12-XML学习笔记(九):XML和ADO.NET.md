---
layout: post
title: XML学习笔记(九):XML和ADO.NET
date: 2009-05-12 16:34:20
comments: true
sharing: true
categories: linux
tags: 
---

<h2>将DataSet的内容存储为XML文件: </h2>  <h2><font color="#ff0000">WriteXml(), WriteXmlSchema(), GetXml(), GetXmlSchema()</font></h2>  <p>XmlWriteMode的几个主要的属性</p>  <p>IgnoreSchema: 将DataSet内容写入XML文件，不包括XSD架构信息</p>  <p>WriteSchema: 同时将DataSet内容和XSD架构信息写入    <br />DiffGram: 写入为DiffGram格式</p>  <p>Saving Only the Schema:仅仅写入XSD架构信息，不包括实际的数据</p>  <p>示例如下：</p>  <p><a href="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/XMLXMLADO.NET/369195AC/20090512_161852.jpg"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="2009-05-12_161852" border="0" alt="2009-05-12_161852" src="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/XMLXMLADO.NET/7EDEDB7B/20090512_161852_thumb.jpg" width="644" height="328" /></a> </p>  <div class="csharpcode">&#160;</div>  <h5>DataSetWriteXML.aspx</h5>  <div class="csharpcode">&#160;</div>  <div class="csharpcode">   <pre class="alt"><span class="asp">&lt;%@ Page Language=&quot;C#&quot; AutoEventWireup=&quot;true&quot; CodeFile=&quot;DataSetWriteXML.aspx.cs&quot;</pre>

  <pre>    Inherits=&quot;DataSetWriteXML&quot; %&gt;</span></pre>

  <pre class="alt">&#160;</pre>

  <pre><span class="kwrd">&lt;!</span><span class="html">DOCTYPE</span> <span class="attr">html</span> <span class="attr">PUBLIC</span> <span class="kwrd">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot;</span> <span class="kwrd">&quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt"><span class="kwrd">&lt;</span><span class="html">html</span> <span class="attr">xmlns</span><span class="kwrd">=&quot;http://www.w3.org/1999/xhtml&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd">&lt;</span><span class="html">head</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">    <span class="kwrd">&lt;</span><span class="html">title</span><span class="kwrd">&gt;&lt;/</span><span class="html">title</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd">&lt;/</span><span class="html">head</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt"><span class="kwrd">&lt;</span><span class="html">body</span><span class="kwrd">&gt;</span></pre>

  <pre>    <span class="kwrd">&lt;</span><span class="html">form</span> <span class="attr">id</span><span class="kwrd">=&quot;form1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">    <span class="kwrd">&lt;</span><span class="html">div</span><span class="kwrd">&gt;</span></pre>

  <pre>        <span class="kwrd">&lt;</span><span class="html">fieldset</span> <span class="attr">title</span><span class="kwrd">=&quot;DataSet to XML&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">            <span class="kwrd">&lt;</span><span class="html">asp:TextBox</span> <span class="attr">ID</span><span class="kwrd">=&quot;TextBox1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">Height</span><span class="kwrd">=&quot;20px&quot;</span> <span class="attr">Width</span><span class="kwrd">=&quot;284px&quot;</span><span class="kwrd">&gt;&lt;/</span><span class="html">asp:TextBox</span><span class="kwrd">&gt;</span></pre>

  <pre>            <span class="kwrd">&lt;</span><span class="html">br</span> <span class="kwrd">/&gt;</span></pre>

  <pre class="alt">            <span class="kwrd">&lt;</span><span class="html">asp:RadioButtonList</span> <span class="attr">ID</span><span class="kwrd">=&quot;RadioButtonList1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span></pre>

  <pre>                <span class="kwrd">&lt;</span><span class="html">asp:ListItem</span> <span class="attr">Value</span><span class="kwrd">=&quot;0&quot;</span><span class="kwrd">&gt;</span>No Schema<span class="kwrd">&lt;/</span><span class="html">asp:ListItem</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">                <span class="kwrd">&lt;</span><span class="html">asp:ListItem</span> <span class="attr">Value</span><span class="kwrd">=&quot;1&quot;</span><span class="kwrd">&gt;</span>With Schema<span class="kwrd">&lt;/</span><span class="html">asp:ListItem</span><span class="kwrd">&gt;</span></pre>

  <pre>                <span class="kwrd">&lt;</span><span class="html">asp:ListItem</span> <span class="attr">Value</span><span class="kwrd">=&quot;2&quot;</span><span class="kwrd">&gt;</span>DiffGram<span class="kwrd">&lt;/</span><span class="html">asp:ListItem</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">                <span class="kwrd">&lt;</span><span class="html">asp:ListItem</span> <span class="attr">Value</span><span class="kwrd">=&quot;3&quot;</span><span class="kwrd">&gt;</span>Only Schema<span class="kwrd">&lt;/</span><span class="html">asp:ListItem</span><span class="kwrd">&gt;</span></pre>

  <pre>            <span class="kwrd">&lt;/</span><span class="html">asp:RadioButtonList</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">            <span class="kwrd">&lt;</span><span class="html">br</span> <span class="kwrd">/&gt;</span></pre>

  <pre>            <span class="kwrd">&lt;</span><span class="html">asp:Button</span> <span class="attr">ID</span><span class="kwrd">=&quot;Button1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">Text</span><span class="kwrd">=&quot;Write to XML&quot;</span> <span class="attr">OnClick</span><span class="kwrd">=&quot;Button1_Click&quot;</span> <span class="kwrd">/&gt;</span></pre>

  <pre class="alt">            <span class="kwrd">&lt;</span><span class="html">asp:Button</span> <span class="attr">ID</span><span class="kwrd">=&quot;Button2&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">Text</span><span class="kwrd">=&quot;Load XML&quot;</span> <span class="attr">OnClick</span><span class="kwrd">=&quot;Button2_Click&quot;</span> <span class="kwrd">/&gt;</span></pre>

  <pre>        <span class="kwrd">&lt;/</span><span class="html">fieldset</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt">    <span class="kwrd">&lt;/</span><span class="html">div</span><span class="kwrd">&gt;</span></pre>

  <pre>    <span class="kwrd">&lt;/</span><span class="html">form</span><span class="kwrd">&gt;</span></pre>

  <pre class="alt"><span class="kwrd">&lt;/</span><span class="html">body</span><span class="kwrd">&gt;</span></pre>

  <pre><span class="kwrd">&lt;/</span><span class="html">html</span><span class="kwrd">&gt;</span></pre>
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

<h5>DataSetWriteXML.aspx.cs</h5>

<div class="csharpcode">
  <pre class="alt"><span class="lnum">   1:  </span><span class="kwrd">using</span> System;</pre>

  <pre><span class="lnum">   2:  </span><span class="kwrd">using</span> System.Collections.Generic;</pre>

  <pre class="alt