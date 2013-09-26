---
layout: post
title: "解决git pull时出现的几个问题"
date: 2012-11-28 13:20
comments: true
sharing: true
footer: true
categories: Git
tags: git
---

第1个问题: 解决Git代码仓库不同步git pull时出现:[root@linuxso.com&nbsp;/data/</span><span class="keyword">work</span><span>/www/rest/lib/Business/Inventory]#&nbsp;git&nbsp;pull &nbsp;</span></span></pre>
</li>
<li><span>Enter&nbsp;passphrase&nbsp;</span><span class="keyword">for</span><span>&nbsp;</span><span class="keyword">key</span><span>&nbsp;</span><span class="string">'/root/.ssh/<a href="http://www.linuxso.com/command/id.html" target="_blank"><span style="text-decoration: underline;">id</span></a>_rsa'</span><span>: &nbsp;</span></li>
<li class="alt"><span>Updating&nbsp;70e8b93..a0f1a6c &nbsp;</span></li>
<li><span style="background-color: #ff9900;">error:&nbsp;Your&nbsp;<span class="keyword">local</span>&nbsp;changes&nbsp;<span class="keyword">to</span>&nbsp;the&nbsp;following&nbsp;<a href="http://www.linuxso.com/command/file.html" target="_blank"><span style="text-decoration: underline;">file</span></a>s&nbsp;would&nbsp;be&nbsp;overwritten&nbsp;<span class="keyword">by</span>&nbsp;merge: &nbsp;</span></li>
<li class="alt"><span style="background-color: #ff9900;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rest/lib/Business/Inventory/Pro<a href="http://www.linuxso.com/command/du.html" target="_blank"><span style="text-decoration: underline;">du</span></a>ctStatus.php &nbsp;</span></li>
<li><span>Please,&nbsp;</span><span class="keyword">commit</span><span>&nbsp;your&nbsp;changes&nbsp;</span><span class="op">or</span><span>&nbsp;stash&nbsp;them&nbsp;before&nbsp;you&nbsp;can&nbsp;merge. &nbsp;</span></li>
<li class="alt"><span>Aborting&nbsp;</span></li>
</ol>
<p>解决方法: 执行git checkout -f，然后再执行git pull重新checkout</p>
<pre>&nbsp;</pre>
<ol class="dp-sql">
<li class="alt">
<pre><span><span>[root@linuxso.com&nbsp;/data/</span><span class="keyword">work</span><span>/www/rest/lib/Business/Inventory]#&nbsp;git&nbsp;checkout&nbsp;-f &nbsp;</span></span></pre>
</li>
<li><span>Your&nbsp;bra<a href="http://www.linuxso.com/command/nc.html" target="_blank"><span style="text-decoration: underline;">nc</span></a>h&nbsp;</span><span class="keyword">is</span><span>&nbsp;behind&nbsp;</span><span class="string">'origin/master'</span><span>&nbsp;</span><span class="keyword">by</span><span>&nbsp;2&nbsp;commits,&nbsp;</span><span class="op">and</span><span>&nbsp;can&nbsp;be&nbsp;fast-forwarded.&nbsp;</span></li>
</ol>
<p>再执行git pull时就可以了:</p>
<pre>&nbsp;</pre>
<ol class="dp-sql">
<li class="alt">
<pre><span><span>[root@linuxso.com&nbsp;/data/</span><span class="keyword">work</span><span>/www/rest/lib/Business/Inventory]#&nbsp;git&nbsp;pull &nbsp;</span></span></pre>
</li>
<li><span>Enter&nbsp;passphrase&nbsp;</span><span class="keyword">for</span><span>&nbsp;</span><span class="keyword">key</span><span>&nbsp;</span><span class="string">'/root/.ssh/id_rsa'</span><span>: &nbsp;</span></li>
<li class="alt"><span>Updating&nbsp;70e8b93..a0f1a6c &nbsp;</span></li>
<li><span>Fast-</span><span class="keyword">forward</span><span>&nbsp;</span></li>
<li class="alt"><span>&nbsp;rest/lib/Business/Inventory/ProductStatus.php&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;+ &nbsp;</span></li>
<li><span>&nbsp;1&nbsp;files&nbsp;changed,&nbsp;1&nbsp;insertions(+),&nbsp;0&nbsp;deletions(-) &nbsp;</span></li>
<li class="alt"><span>&nbsp;mode&nbsp;change&nbsp;100644&nbsp;=&gt;&nbsp;100755&nbsp;rest/lib/Business/Inventory/ProductStatus.php&nbsp;</span></li>
</ol>
<p>&nbsp;</p>
<p>第2个问题: git pull的默认地址问题.</p>
<p>1.git处于master这个branch下时，默认的remote就是origin； 2.当在master这个brach下使用指定remote和merge的git pull时，使用默认的remote和merge。 &nbsp; 但是对于自己建的项目，并用push到远程服务器上，并没有这块内容，需要自己配置。 如果直接运行git pull，会得到如此结果：</p>
<p>#当执行git pull之后的提示:</p>
<pre>&nbsp;</pre>
<ol class="dp-sql">
<li class="alt">
<pre><span><span>$&nbsp;git&nbsp;pull &nbsp;</span></span></pre>
</li>
<li><span class="keyword">Password</span><span>: &nbsp;</span></li>
<li class="alt"><span>You&nbsp;asked&nbsp;me&nbsp;</span><span class="keyword">to</span><span>&nbsp;pull&nbsp;without&nbsp;telling&nbsp;me&nbsp;<a href="http://www.linuxso.com/command/which.html" target="_blank"><span style="text-decoration: underline;">which</span></a>&nbsp;branch&nbsp;you &nbsp;</span></li>
<li><span>want&nbsp;</span><span class="keyword">to</span><span>&nbsp;merge&nbsp;</span><span class="keyword">with</span><span>,&nbsp;</span><span class="op">and</span><span>&nbsp;</span><span class="string">'branch.master.merge'</span><span>&nbsp;</span><span class="op">in</span><span>&nbsp;</span></li>
<li class="alt"><span>your&nbsp;configuration&nbsp;file&nbsp;does&nbsp;</span><span class="op">not</span><span>&nbsp;tell&nbsp;me,&nbsp;either.&nbsp;Please &nbsp;</span></li>
<li><span>specify&nbsp;which&nbsp;branch&nbsp;you&nbsp;want&nbsp;</span><span class="keyword">to</span><span>&nbsp;use&nbsp;</span><span class="keyword">on</span><span>&nbsp;the&nbsp;command&nbsp;line&nbsp;</span><span class="op">and</span><span>&nbsp;</span></li>
<li class="alt"><span><a href="http://www.linuxso.com/command/tr.html" target="_blank"><span style="text-decoration: underline;">tr</span></a>y&nbsp;again&nbsp;(e.g.&nbsp;</span><span class="string">'git&nbsp;pull&nbsp;&lt;repository&gt;&nbsp;&lt;refspec&gt;'</span><span>). &nbsp;</span></li>
<li><span>See&nbsp;git-pull(1)&nbsp;</span><span class="keyword">for</span><span>&nbsp;detai<a href="http://www.linuxso.com/command/ls.html" target="_blank"><span style="text-decoration: underline;">ls</span></a>. &nbsp;</span></li>
<li class="alt"><span>&nbsp; &nbsp;</span></li>
<li><span>If&nbsp;you&nbsp;often&nbsp;merge&nbsp;</span><span class="keyword">with</span><span>&nbsp;the&nbsp;same&nbsp;branch,&nbsp;you&nbsp;may&nbsp;want&nbsp;</span><span class="keyword">to</span><span>&nbsp;</span></li>
<li class="alt"><span>use&nbsp;something&nbsp;</span><span class="op">like</span><span>&nbsp;the&nbsp;following&nbsp;</span><span class="op">in</span><span>&nbsp;your&nbsp;configuration&nbsp;file: &nbsp;</span></li>
<li><span>&nbsp; &nbsp;</span></li>
<li class="alt"><span>[branch&nbsp;</span><span class="string">"master"</span><span>] &nbsp;</span></li>
<li><span>&nbsp;remote&nbsp;=&nbsp;&lt;nickname&gt; &nbsp;</span></li>
<li class="alt"><span>&nbsp;merge&nbsp;=&nbsp;&lt;remote-ref&gt; &nbsp;</span></li>
<li><span>&nbsp; &nbsp;</span></li>
<li class="alt"><span>[remote&nbsp;</span><span class="string">"&lt;nickname&gt;"</span><span>] &nbsp;</span></li>
<li><span>&nbsp;url&nbsp;=&nbsp;&lt;url&gt; &nbsp;</span></li>
<li class="alt"><span>&nbsp;</span><span class="keyword">fetch</span><span>&nbsp;=&nbsp;&lt;refspec&gt; &nbsp;</span></li>
<li><span>&nbsp; &nbsp;</span></li>
<li class="alt"><span>See&nbsp;git-config(1)&nbsp;</span><span class="keyword">for</span><span>&nbsp;details.&nbsp;</span></li>
</ol>
<p>#解决方法, 通过git config进行如下配置.</p>
<pre>&nbsp;</pre>
<ol class="dp-sql">
<li class="alt">
<pre><span><span>git&nbsp;remote&nbsp;</span><span class="keyword">a<a href="http://www.linuxso.com/command/dd.html" target="_blank"><span style="text-decoration: underline;">dd</span></a></span><span>&nbsp;-f&nbsp;origin&nbsp;git@192.168.21.44:rest.git &nbsp;</span></span></pre>
</li>
<li><span>git&nbsp;config&nbsp;branch.master.remote&nbsp;origin &nbsp;</span></li>
<li class="alt"><span>git&nbsp;config&nbsp;branch.master.merge&nbsp;refs/heads/master&nbsp;</span></li>
</ol>
<p>&nbsp;</p>
<!-- google_ad_section_end -->
<p><a href="http://www.linuxso.com/linuxrumen/13158.html">http://www.linuxso.com/linuxrumen/13158.html</a></p>
<p><br />&nbsp;</p>
