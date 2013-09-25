---
layout: post
title: "ObjectDataSource控件的分页、排序和筛选"
description: "ObjectDataSource控件"
categories: ASP.NET
tags: [ASP.NET]
---
ObjectDataSource控件提供了两种方法对绑定到控件(比如GridView)的数据进行分页和排序：

通过用户界面进行分页，优点是容易设置，缺点是当数据量大时执行效率较低；
实现方法：

对GridView控件使用正确的数据源，比如：DataSet, Collection, DataTable或者DataView，但不能使用DataReader
在页面设置GridView控件分分页属性为True。AllowPaging="True"
 

通过设置ObjectDataSource的分页，优点是数据量大时执行效率较高，特别是如果配合Caching能极大的提高以数据驱动为主的网络应用程序的效率。
ObjectDataSource数据源的分页可以在类Class, 存储过程, LINQ to SQL查询中实现，下面以LINQ to SQL,Northwind数据库的Product表为例子来说明用法：

实例网站的文档结构如下图：

######1、新建网页，添加LINQ to SQL Class，命名为Products，在Server Exploer中拖拽Northwind数据库的Product表到设计界面。
！[图1](/images/2009/3/04.png)

######2、添加一个新类Class命名为roductsLINQPaging

！[图2](/images/2009/3/05.png)
！[图3](/images/2009/3/06.png)
！[图3](/images/2009/3/06.png)

######3、类中实现的方法如下：

'''
using System;
using System.Collections.Generic;
using System.Linq;
using System.Data.Linq;
using System.Web;

/// <summary>
/// Summary description for ProductsLINQPaging
/// </summary>
public class ProductsLINQPaging
	{
	  public ProductsLINQPaging()
	    {
	        //
	        // TODO: Add constructor logic here
	        //
'''	        
