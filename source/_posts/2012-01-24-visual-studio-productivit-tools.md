--- 
layout: post 
title: Visual Studio 2010快捷工具配置 
date: 2012-01-24 14:20
categories: ASP.NET
tags: visualstudio
---


#### Visual Studio 2010+Code Rush + PowerCommand + Power Tools三種套件同時存在的微調修改

[系列文章](http://demo.tc/SeriesArticleList/Visual%20Studio%20%E7%B2%BE%E9%81%B8%E6%93%B4%E5%85%85%E5%A5%97%E4%BB%B6)

-  [將本文推到Facebook](http://www.facebook.com/sharer.php?t=[Visual%20Studio%202010]%20Code%20Rush%20+%20PowerCommand%20+%20Power%20Tools%20%E4%B8%89%E7%A8%AE%E5%A5%97%E4%BB%B6%E5%90%8C%E6%99%82%E5%AD%98%E5%9C%A8%E7%9A%84%E5%BE%AE%E8%AA%BF%E4%BF%AE%E6%94%B9-demo%E5%B0%8F%E9%8B%AA&u=http://demo.tc/Post/630)
-   [將本文推到Twitter](http://twitter.com/?status=http://demo.tc/Post/630%20[Visual%20Studio%202010]%20Code%20Rush%20+%20PowerCommand%20+%20Power%20Tools%20%E4%B8%89%E7%A8%AE%E5%A5%97%E4%BB%B6%E5%90%8C%E6%99%82%E5%AD%98%E5%9C%A8%E7%9A%84%E5%BE%AE%E8%AA%BF%E4%BF%AE%E6%94%B9+-+demo%E5%B0%8F%E9%8B%AA)
-   [將本文推到Plurk](http://plurk.com/?status=http://demo.tc/Post/630+([Visual%20Studio%202010]%20Code%20Rush%20+%20PowerCommand%20+%20Power%20Tools%20%E4%B8%89%E7%A8%AE%E5%A5%97%E4%BB%B6%E5%90%8C%E6%99%82%E5%AD%98%E5%9C%A8%E7%9A%84%E5%BE%AE%E8%AA%BF%E4%BF%AE%E6%94%B9+-+demo%E5%B0%8F%E9%8B%AA)&qualifier=shares)
-   [下載本文PDF](http://pdfmyurl.com/?url=http://demo.tc/Post/630)

demo 的 Visual Studio 一直以來都會安裝 Code Rush 和 PowerCommand
，一直也都合作愉快，但最近看了ScottGu's 的 Power Tool
介紹文，看到了一個相當棒的功能 Solution Navigator 讓我決定也要安裝 Power
Tools ，就因為這樣我的 Visual Studio 擁有了Code Rush + PowerCommand +
Power Tools
三套套件，部份功能重複性還滿高的，所以就稍微作了一下調整，記錄下來以免以後忘記。

-   最後更新：2011/7/6 上午 09:12:10

![demo廢言](http://demo.tc/images/msn/demosay.gif "demo廢言")先說明因為
demo 主要功能是 Code Rush \> PowerCommand \> Power
Tools，因此有重複的功能會優先關掉 Power Tool 的，不過考量到 Code Rush
免費版到底有什麼功能我不知道，因此衝突的部份都會寫出來，有需要的朋友再自行調配使用。

![](http://lh3.ggpht.com/_PgurvCEASJs/TFz8N-4jlFI/AAAAAAAAGjA/Ocr7cVFvqxo/s800/CPPTools01.gif)Code
Rush
（[官網](http://visualstudiogallery.msdn.microsoft.com/zh-TW/F9CDA5D8-10AF-4CC6-9D17-207222A3FD13)）預設所有功能都是他，不調整

* * * * *

![](http://lh5.ggpht.com/_PgurvCEASJs/TFz8NyaBirI/AAAAAAAAGjE/nyQLSYxbzps/s800/CPPTools02.gif)PowerCommand
（[官網](http://visualstudiogallery.msdn.microsoft.com/en-us/e5f41ad9-4edc-4912-bca3-91147db95b99)）調整如下：

![](http://lh5.ggpht.com/_PgurvCEASJs/TFz8OK_ov6I/AAAAAAAAGjM/swibUMiJ_3w/s800/CPPTools04.gif)

1.  用到機率太小所以關閉。
2.  內建就有了所以關閉。
3.  和 Power Tools 重複，所以關閉。

![](http://lh5.ggpht.com/_PgurvCEASJs/TFz8N2d1vOI/AAAAAAAAGjI/tE9LSJdYbIU/s800/CPPTools03.gif)Power
Tools
（[官網](http://visualstudiogallery.msdn.microsoft.com/en-us/d0d33361-18e2-46c0-8ff2-4adea1e34fef)）調整如下：

![](http://lh4.ggpht.com/_PgurvCEASJs/TFz8OLAP1QI/AAAAAAAAGjQ/D629sgQK1Zg/s800/CPPTools05.gif)

1.  因不一定團隊成員都有安裝，所以意義不大，因此關閉。
2.  與 Code Rush 衝突，因此關閉。
3.  與 Code Rush 衝突，因此關閉。
4.  因不一定團隊成員都有安裝，所以意義不大，因此關閉。
5.  與 Code Rush 衝突，因此關閉。
6.  單純因為自己用不到所以關閉.....
7.  單純因為自己用不到所以關閉.....
8.  單純因為自己用不到所以關閉.....
9.  CTRL﹢X 更好用所以關閉。

* * * * *

基於以上的調整後，一些重複的功能就不會出現了，但這三個套件功能繁雜，demo
不可能一一介紹（除非我開三篇文）所以就請各位參考一下官方和其他網友的說明吧。

![分隔線](http://demo.tc/images/msn/linkPage.gif "分隔線")

-   Code Rush
    -   [Visual Studio
        模組下載介紹頁面](http://visualstudiogallery.msdn.microsoft.com/zh-TW/F9CDA5D8-10AF-4CC6-9D17-207222A3FD13)
    -   [強力推薦寫程式一定要用的外掛工具 - CodeRush
        Xpress](http://www.dotblogs.com.tw/sam319/archive/2009/12/31/12747.aspx)
    -   [開啟 CodeRush Xpress 10.1
        的選單功能列](http://www.minitw.com/archives/633)

-   PowerCommand
    -   [Visual Studio
        模組下載介紹頁面](http://visualstudiogallery.msdn.microsoft.com/en-us/e5f41ad9-4edc-4912-bca3-91147db95b99)
    -   [Visual Studio 2010 Extension Manager (and the new VS 2010
        PowerCommands
        Extension)](http://weblogs.asp.net/scottgu/archive/2010/05/03/visual-studio-2010-extension-manager-and-the-new-vs-2010-powercommands-extension.aspx)

-   Poert Tools
    -   [Visual Studio
        模組下載介紹頁面](http://visualstudiogallery.msdn.microsoft.com/en-us/d0d33361-18e2-46c0-8ff2-4adea1e34fef)
    -   [[Visual Studio]Visual Studio 2010 Pro Power
        Tools](http://www.dotblogs.com.tw/larrynung/archive/2010/06/14/15862.aspx)
    -   [Some nice code editor features provided by the VS 2010 Power
        Tool
        Extensions](http://weblogs.asp.net/scottgu/archive/2010/08/04/some-nice-code-editor-features-provided-by-the-vs-2010-power-tool-extensions.aspx)
    -   [VS 2010 Productivity Power Tools Update (with some cool new
        features)](http://weblogs.asp.net/scottgu/archive/2010/07/19/vs-2010-productivity-power-tools-update-with-some-cool-new-features.aspx)

[Visual Studio
擴充套件](http://demo.tc/Tag/Visual%20Studio%20%E6%93%B4%E5%85%85%E5%A5%97%E4%BB%B6)

原文地址：[http://demo.tc/Post/630](http://demo.tc/Post/630)
