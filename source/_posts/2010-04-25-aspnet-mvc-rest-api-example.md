--- 
layout: default 
title: "ASP.NET MVC REST API 应用实例"
date: 2010-04-25 16:20
categories: ASP.NET
tags: api
---

**需要解决的问题**

****

**1：创建更为简洁的/Product/Details/1 URL**

**** 

+--------------------------------------+--------------------------------------+
| **Valid route definitions**          | ****                                 |
|                                      |                                      |
|                                      | **Examples of matching URL**         |
+--------------------------------------+--------------------------------------+
| {controller}/{action}/{id}           | /Products/Details/1                  |
+--------------------------------------+--------------------------------------+
| {controller}/{action}/{id}           | /Products/1                          |
+--------------------------------------+--------------------------------------+
| {controller}/{action}/{id}.{Format}  | /Products/Show/1.xml                 |
+--------------------------------------+--------------------------------------+

 

“/Products/Details/1”是我们在MVC开发中默认浏览对象Details方法的路由，需要实现的是更为简洁的url表示，如“/Products/1”，返回和“/Products/Details/1“同样的结果。这个处理比较简单，仅仅需要在Global.asax文件中添加一条新的路由规则，不过一定记得是添加在默认路由的前面。

[![2010-04-25\_233011](/images/WindowsLiveWriter/ASP.NETMVCRESTAPI/56873DDE/20100425_233011_thumb.png "2010-04-25_233011")](http://blog.cnpc.ac.cn/Blogs/images/WindowsLiveWriter/ASP.NETMVCRESTAPI/77781FD4/20100425_233011.png)

 

**2：创建一个/Product/Show/1.xml的API**

要实现xml访问的API,需要先建立一个抽象类来处理返回结果的路由和xml结果的序列化，这里用到了MVC
Contrib的类库，可以去[MVC Contrib Code
Plex](http://mvccontrib.codeplex.com/documentation)下载添加引用。见下图代码的return
new XMLResult

代码如下：

[![2010-04-25\_233740](/images/WindowsLiveWriter/ASP.NETMVCRESTAPI/3E1C4BE3/20100425_233740_thumb.png "2010-04-25_233740")](http://blog.cnpc.ac.cn/Blogs/images/WindowsLiveWriter/ASP.NETMVCRESTAPI/383F1799/20100425_233740.png)

最后需要在相应的Action中添加对应的返回类型，这里是Show，见下图

[![2010-04-25\_234102](/images/WindowsLiveWriter/ASP.NETMVCRESTAPI/57A8FA72/20100425_234102_thumb.png "2010-04-25_234102")](http://blog.cnpc.ac.cn/Blogs/images/WindowsLiveWriter/ASP.NETMVCRESTAPI/5C1F7B39/20100425_234102.png)

实际效果如下：

[![2010-04-25\_234456](/images/WindowsLiveWriter/ASP.NETMVCRESTAPI/3ED1D582/20100425_234456_thumb.png "2010-04-25_234456")](http://blog.cnpc.ac.cn/Blogs/images/WindowsLiveWriter/ASP.NETMVCRESTAPI/2DCB16EE/20100425_234456.png)
