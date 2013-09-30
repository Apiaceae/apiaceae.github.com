---
layout: post
title: 使用Macports在Mac机器上配置Ruby on Rails开发环境
date: 2009-09-23 04:50:18
comments: true
sharing: true
categories: linux
tags: 
---

<p>
<strong>MacPorts</strong>
</p>
<p>
You might already have your Rails environment set up using <a href="http://www.macports.org/">MacPorts</a>.
If that&rsquo;s the case, why not just use that? Even if you are like me with
a fresh installed Leopard, MacPorts still has its advantages. For
example, you can use MacPorts to upgrade ruby in the future.
</p>
<p>
I used MacPorts to set up my Rails environment based on these other great articles:
</p>
<ul>
	<li><a href="http://teabass.com/super-simple-ruby-on-rails-install-with-macports-for-leopard/">Teabass</a></li>
	<li><a href="http://www.robbyonrails.com/articles/2007/06/19/installing-ruby-on-rails-and-postgresql-on-os-x-second-edition">Robby on Rails</a></li>
	<li><a href="http://michael.biven.org/2006/12/22/starting-mongrel-or-memcached-with-launchd/">Michael Biven</a></li>
	<li><a href="http://gorn.ch/archive/2007/01/22/start-memcached-with-launchd.html"> Tobias Ebn&amp;Atilde;?&amp;Acirc;&para;ther</a></li>
</ul>
<p>
1. Install the latest Xcode version for Leopard.  <a href="http://developer.apple.com/tools/download/">Download</a> from the Apple website.
</p>
<p>
2. Install the latest MacPorts version for Leopard.  <a href="http://www.macports.org/">Download</a> from the MacPorts website.
</p>
<p>
Run this to update MacPorts:
</p>
<div class="wp_syntax">
<div class="code">
<pre class="bash" style="font-family: monospace">
<span style="color: #c20cb9; font-weight: bold">sudo</span> port selfupdate
</pre>
</div>
</div>
<p>
3. Install Ruby, RubyGems, and Rails.
</p>
<div class="wp_syntax">
<div class="code">
<pre class="bash" style="font-family: monospace">
<span style="color: #c20cb9; font-weight: bold">sudo</span> port <span style="color: #c20cb9; font-weight: bold">install</span> ruby
<span style="color: #c20cb9; font-weight: bold">sudo</span> port <span style="color: #c20cb9; font-weight: bold">install</span> rb-rubygems
<span style="color: #c20cb9; font-weight: bold">sudo</span> gem update <span style="color: #660033">--system</span>
<span style="color: #c20cb9; font-weight: bold">sudo</span> gem <span style="color: #c20cb9; font-weight: bold">install</span> rails <span style="color: #660033">-y</span>
</pre>
</div>
</div>
<p>
4. Install MySQL (directly from Andrew Nesbitt, shown here for completeness).
</p>
<div class="wp_syntax">
<div class="code">
<pre class="bash" style="font-family: monospace">
<span style="color: #c20cb9; font-weight: bold">sudo</span> port <span style="color: #c20cb9; font-weight: bold">install</span> mysql5 +server
<span style="color: #c20cb9; font-weight: bold">sudo</span> launchctl load <span style="color: #660033">-w</span> <span style="color: #000000; font-weight: bold">/</span>Library<span style="color: #000000; font-weight: bold">/</span>LaunchDaemons<span style="color: #000000; font-weight: bold">/</span>org.macports.mysql5.plist
<span style="color: #c20cb9; font-weight: bold">sudo</span> <span style="color: #660033">-u</span> mysql mysql_install_db5
<span style="color: #7a0874; font-weight: bold">cd</span> <span style="color: #000000; font-weight: bold">/</span>opt<span style="color: #000000; font-weight: bold">/</span><span style="color: #7a0874; font-weight: bold">local</span> ; <span style="color: #c20cb9; font-weight: bold">sudo</span> <span style="color: #000000; font-weight: bold">/</span>opt<span style="color: #000000; font-weight: bold">/</span>local<span style="color: #000000; font-weight: bold">/</span>lib<span style="color: #000000; font-weight: bold">/</span>mysql5<span style="color: #000000; font-weight: bold">/</span>bin<span style="color: #000000; font-weight: bold">/</span>mysqld_safe <span style="color: #000000; font-weight: bold">&amp;</span>
<span style="color: #c20cb9; font-weight: bold">sudo</span> <span style="color: #c20cb9; font-weight: bold">ln</span> <span style="color: #660033">-s</span> <span style="color: #000000; font-weight: bold">/</span>opt<span style="color: #000000; font-weight: bold">/</span>local<span style="color: #000000; font-weight: bold">/</span>var<span style="color: #000000; font-weight: bold">/</span>run<span style="color: #000000; font-weight: bold">/</span>mysql5<span style="color: #000000; font-weight: bold">/</span>mysqld.sock <span style="color: #000000; font-weight: bold">/</span>tmp<span style="color: #000000; font-weight: bold">/</span>mysql.sock
</pre>
</div>
</div>
<p>
5. Install mongrel and mongrel_cluster.
</p>
<div class="wp_syntax">
<div class="code">
<pre class="bash" style="font-family: monospace">
<span style="color: #c20cb9; font-weight: bold">sudo</span> gem <span style="color: #c20cb9; font-weight: bold">install</span> mongrel
<span style="color: #c20cb9; font-weight: bold">sudo</span> gem <span style="color: #c20cb9; font-weight: bold">install</span> mongrel_cluster
</pre>
</div>
</div>
<p>
6. Install memcached.
</p>
<div class="wp_syntax">
<div class="code">
<pre class="bash" style="font-family: monospace">
<span style="color: #c20cb9; font-weight: bold">sudo</span> port <span style="color: #c20cb9; font-weight: bold">install</span> memcached
<span style="color: #c20cb9; font-weight: bold">sudo</span> gem <span style="color: #c20cb9; font-weight: bold">install</span> memcache-client
</pre>
</div>
</div>
<p>
Create a file called /Library/LaunchDaemons/com.danga.memcached.plist, and insert the following:
</p>
<div class="wp_syntax">
<div class="code">
<pre class="xml" style="font-family: monospace">
<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;?xml</span> <span style="color: #000066">version</span>=<span style="color: #ff0000">&quot;1.0&quot;</span> <span style="color: #000066">encoding</span>=<span style="color: #ff0000">&quot;UTF-8&quot;</span><span style="color: #000000; font-weight: bold">?&gt;</span></span>
<span style="color: #00bbdd">&lt;!DOCTYPE plist PUBLIC &quot;-//Apple//DTD PLIST 1.0//EN&quot; &quot;http://www.apple.com/DTDs/PropertyList-1.0.dtd&quot;&gt;</span>
<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;plist</span> <span style="color: #000066">version</span>=<span style="color: #ff0000">&quot;1.0&quot;</span><span style="color: #000000; font-weight: bold">&gt;</span></span>
<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;dict<span style="color: #000000; font-weight: bold">&gt;</span></span></span>
<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;key<span style="color: #000000; font-weight: bold">&gt;</span></span></span>Label<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;/key<span style="color: #000000; font-weight: bold">&gt;</span></span></span>
<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;string<span style="color: #000000; font-weight: bold">&gt;</span></span></span>com.danga.memcached<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;/string<span style="color: #000000; font-weight: bold">&gt;</span></span></span>
<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;key<span style="color: #000000; font-weight: bold">&gt;</span></span></span>OnDemand<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;/key<span style="color: #000000; font-weight: bold">&gt;</span></span></span>
<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;false</span><span style="color: #000000; font-weight: bold">/&gt;</span></span>
<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;key<span style="color: #000000; font-weight: bold">&gt;</span></span></span>ProgramArguments<span style="color: #009900"><span style="color: #000000; font-weight: bold">&lt;/key<span style="color: #000000; font-weight: bold">&gt;</span></span></span>
<span style="color: #009900"><span s