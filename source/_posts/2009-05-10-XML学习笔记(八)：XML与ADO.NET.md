---
layout: post
title: XML学习笔记(八)：XML与ADO.NET
date: 2009-05-10 18:36:28
comments: true
sharing: true
categories: linux
tags: 
---

<h2>DataSet architecture</h2>  <p><a href="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/XMLXMLADO.NET/05F28B28/20090510_175702.jpg"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="2009-05-10_175702" border="0" alt="2009-05-10_175702" src="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/XMLXMLADO.NET/438279A2/20090510_175702_thumb.jpg" width="379" height="484" /></a> </p>  <h2>DataAdapter architecture</h2>  <p><a href="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/XMLXMLADO.NET/17657CB1/20090510_175821.jpg"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="2009-05-10_175821" border="0" alt="2009-05-10_175821" src="http://blog.cnpc.ac.cn/Blogs/image.axd?picture=WindowsLiveWriter/XMLXMLADO.NET/1BDE8E29/20090510_175821_thumb.jpg" width="475" height="484" /></a> </p>  <h2>ADO.NET模式的两种数据连接模式</h2>  <h3>? Connected data access</h3>  <h4>执行步骤如下</h4>  <p>1. Establish a connection with the database.   <br />2. Fetch a set of records in a cursor.    <br />3. Work with the fetched data (perform read, modify, and delete operations or even calculations).    <br />4. Update the database, if there are any changes.    <br />5. Close the database connection.</p>  <h4>适合使用的情景</h4>  <p>? You are developing applications that are online all the time. For example, in a ticket reservation   <br />application it is necessary that you work with the latest data from the database.    <br />In such cases, connected data access becomes necessary.    <br />? You want to avoid the overhead of using offline data. When you use queries directly    <br />against a database, naturally they bypass any of the intermediate layers that are involved    <br />in disconnected data-access techniques. For example, suppose that you wish to display a    <br />simple employee listing to the end user. This task does not involve any processing as such.    <br />Using connected data access in such cases will of course give the best performance.    <br />? You need a cursor model for some reason.</p>  <h4>示例代码</h4>  <div class="csharpcode">   <pre class="alt"><span class="lnum">   1:  </span><span class="kwrd">protected</span> <span class="kwrd">void</span> Button1_Click(<span class="kwrd">object</span> sender, EventArgs e)</pre>

  <pre><span class="lnum">   2:  </span>    {</pre>

  <pre class="alt"><span class="lnum">   3:  </span>        SqlConnection cnn = <span class="kwrd">new</span> SqlConnection(<span class="str">@&quot;data source=.;initial catalog=northwind;integrated security=true&quot;</span>);</pre>

  <pre><span class="lnum">   4:  </span>        SqlCommand cmd = <span class="kwrd">new</span> SqlCommand();</pre>

  <pre class="alt"><span class="lnum">   5:  </span>        cmd.Connection = cnn;</pre>

  <pre><span class="lnum">   6:  </span>        cmd.CommandType = CommandType.Text;</pre>

  <pre class="alt"><span class="lnum">   7:  </span>        cmd.CommandText = TextBox1.Text + <span class="str">&quot; FOR XML AUTO&quot;</span>;</pre>

  <pre><span class="lnum">   8:  </span>        cnn.Open();</pre>

  <pre class="alt"><span class="lnum">   9:  </span>        <span class="rem">//Connected Data Access关键代码</span></pre>

  <pre><span class="lnum">  10:  </span>        XmlReader reader = cmd.ExecuteXmlReader();</pre>

  <pre class="alt"><span class="lnum">  11:  </span>        StreamWriter writer = File.CreateText(<span class="str">@&quot;\temp.xml&quot;</span>);</pre>

  <pre><span class="lnum">  12:  </span>        writer.Write(<span class="str">&quot;&lt;root&gt;&quot;</span>);</pre>

  <pre class="alt"><span class="lnum">  13:  </span>        <span class="kwrd">while</span> (reader.Read())</pre>

  <pre><span class="lnum">  14:  </span>        {</pre>

  <pre class="alt"><span class="lnum">  15:  </span>            writer.Write(reader.ReadOuterXml());</pre>

  <pre><span class="lnum">  16:  </span>        }</pre>

  <pre class="alt"><span class="lnum">  17:  </span>        writer.Write(<span class="str">&quot;&lt;/root&gt;&quot;</span>);</pre>

  <pre><span class="lnum">  18:  </span>        writer.Close();</pre>

  <pre class="alt"><span class="lnum">  19:  </span>        reader.Close();</pre>

  <pre><span class="lnum">  20:  </span>        cnn.Close();       </pre>

  <pre class="alt"><span class="lnum">  21:  </span>        Process.Start(<span class="str">@&quot;\temp.xml&quot;</span>);</pre>

  <pre><span class="lnum">  22:  </span>    }</pre>

  <div class="csharpcode">
    <pre class="alt"><span class="asp">&lt;%@ Page Language=&quot;C#&quot; AutoEventWireup=&quot;true&quot; CodeFile=&quot;Default6.aspx.cs&quot; Inherits=&quot;Default6&quot; %&gt;</span></pre>

    <pre>&#160;</pre>

    <pre class="alt"><span class="kwrd">&lt;!</span><span class="html">DOCTYPE</span> <span class="attr">html</span> <span class="attr">PUBLIC</span> <span class="kwrd">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot;</span> <span class="kwrd">&quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;</span><span class="kwrd">&gt;</span></pre>

    <pre><span class="kwrd">&lt;</span><span class="html">html</span> <span class="attr">xmlns</span><span class="kwrd">=&quot;http://www.w3.org/1999/xhtml&quot;</span><span class="kwrd">&gt;</span></pre>

    <pre class="alt"><span class="kwrd">&lt;</span><span class="html">head</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span></pre>

    <pre>    <span class="kwrd">&lt;</span><span class="html">title</span><span class="kwrd">&gt;&lt;/</span><span class="html">title</span><span class="kwrd">&gt;</span></pre>

    <pre class="alt"><span class="kwrd">&lt;/</span><span class="html">head</span><span class="kwrd">&gt;</span></pre>

    <pre><span class="kwrd">&lt;</span><span class="html">body</span><span class="kwrd">&gt;</span></pre>

    <pre class="alt">    <span class="kwrd">&lt;</span><span class="html">form</span> <span class="attr">id</span><span class="kwrd">=&quot;form1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span><span class="kwrd">&gt;</span></pre>

    <pre>    <span class="kwrd">&lt;</span><span class="html">div</span><span class="kwrd">&gt;</span></pre>

    <pre class="alt">        Execute Select Query:</pre>

    <pre>        <span class="kwrd">&lt;</span><span class="html">asp:TextBox</span> <span class="attr">ID</span><span class="kwrd">=&quot;TextBox1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">Height</span><span class="kwrd">=&quot;21px&quot;</span> <span class="attr">Width</span><span class="kwrd">=&quot;371px&quot;</span><span class="kwrd">&gt;&lt;/</span><span class="html">asp:TextBox</span><span class="kwrd">&gt;</span></pre>

    <pre class="alt">        <span class="kwrd">&lt;</span><span class="html">br</span> <span class="kwrd">/&gt;</span></pre>

    <pre>        <span class="kwrd">&lt;</span><span class="html">asp:Button</span> <span class="attr">ID</span><span class="kwrd">=&quot;Button1&quot;</span> <span class="attr">runat</span><span class="kwrd">=&quot;server&quot;</span> <span class="attr">Text</span><span class="kwrd">=&quot;Execute&quot;</span> <span class="attr">OnClick</span><span class="kwrd">=&quot;Button1_Click&quot;</span> <span class="kwrd">/&gt;</span></pre>

    <pre class="alt">        <span class="kwrd">&lt;</span><span class="html">br</span> <span class="kwrd">/&gt;</span></pre>

    <pre>        Result XML File:<span class="kwrd">&lt;/</span><span class="html">div</span><span class="kwrd">&gt;</span></pre>

    <pre class="alt">    <span class="kwrd">&lt;</span><span class="html">asp:TextBox</span> <span class="attr">ID</span><span cl