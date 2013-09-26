---
layout: post
title: "读取数据库数据到HTMLTable 并加入一些漂亮的CSS"
date: 2013-09-26 22:51
comments: true
sharing: true
categories: web
tags: [html, css] 
---


![效果图](/images/WindowsLiveWriter/edb0d7de12e0/352A5F48/20090528_00079.jpg)

{% codeblock lang:html ---default.aspx %}

<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">
    <title></title>
    <style>
        /* roScripts Table Design by Mihalcea Romeo www.roscripts.com */
        
        table
        {
            border-collapse: collapse;
            background: #EFF4FB url(http://www.roscripts.com/images/teaser.gif) repeat-x;
            border-left: 1px solid #686868;
            border-right: 1px solid #686868;
            font: 0.8em/145% 'Trebuchet MS' ,helvetica,arial,verdana;
            color: #333;
        }
        td, th
        {
            padding: 5px;
        }
        caption
        {
            padding: 0 0 .5em 0;
            text-align: left;
            font-size: 1.4em;
            font-weight: bold;
            text-transform: uppercase;
            color: #333;
            background: transparent;
        }
        /* =links */
        
        table a
        {
            color: #950000;
            text-decoration: none;
        }
        table a:link
        {
        }
        table a:visited
        {
            font-weight: normal;
            color: #666;
            text-decoration: line-through;
        }
        table a:hover
        {
            border-bottom: 1px dashed #bbb;
        }
        /* =head =foot*/
        
        thead th, tfoot th, tfoot td
        {
            background: #333 url(http://www.roscripts.com/images/llsh.gif) repeat-x;
            color: #fff;
        }
        tfoot td
        {
            text-align: right;
        }
        /* =body */
        
        tbody th, tbody td
        {
            border-bottom: dotted 1px #333;
        }
        tbody th
        {
            white-space: nowrap;
        }
        tbody th a
        {
            color: #333;
        }
        .odd
        {
        }
        tbody tr:hover
        {
            background: #fafafa;
        }
    </style>
    
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <div id="display" runat="server">
            中国高等植物名录</div>
    </div>
    </form>
</body>
</html>
{% endcodeblock %}