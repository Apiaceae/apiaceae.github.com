---
layout: post
title: 如何在Linux上安装Apache 2
date: 2009-09-24 08:48:52
comments: true
sharing: true
categories: linux
tags: 
---

<strong>Apache 2 Installation</strong>
<table border="0" align="right">
	<tbody>
		<tr>
			 
			<td> 
			<script type="text/javascript">
			<!--
			google_ad_client = "pub-6811628779299912";
			/* 300x250 Devtut Text Only */
			google_ad_slot = "3906716933";
			google_ad_width = 300;
			google_ad_height = 250;
			//-->
			</script>
			<script src="http://pagead2.googlesyndication.com/pagead/show_ads.js" type="text/javascript">
			</script>
			<script src="http://pagead2.googlesyndication.com/pagead/expansion_embed.js">
			</script>
			<script src="http://googleads.g.doubleclick.net/pagead/test_domain.js">
			</script>
			<script>
			google_protectAndRun("ads_core.google_render_ad", google_handleError, google_render_ad)</script><ins style="border: medium none ; margin: 0pt; padding: 0pt; display: inline-table; height: 250px; position: relative; visibility: visible; width: 300px"><ins style="border: medium none ; margin: 0pt; padding: 0pt; display: block; height: 250px; position: relative; visibility: visible; width: 300px"><iframe src="http://googleads.g.doubleclick.net/pagead/ads?client=ca-pub-6811628779299912&amp;output=html&amp;h=250&amp;slotname=3906716933&amp;w=300&amp;lmt=1253753088&amp;flash=10.0.22&amp;url=http%3A%2F%2Fwww.developertutorials.com%2Ftutorials%2Flinux%2Fhow-to-install-apache-2-on-linux-7-12-19%2Fpage2.html&amp;ref=http%3A%2F%2Fwww.google.com%2Furl%3Fsa%3Dt%26source%3Dweb%26ct%3Dres%26cd%3D2%26url%3Dhttp%253A%252F%252Fwww.developertutorials.com%252Ftutorials%252Flinux%252Fhow-to-install-apache-2-on-linux-7-12-19%252Fpage2.html%26ei%3D-8C6StX4NYmV8Aam04DKCw%26rct%3Dj%26q%3Dlinux%2Binstall%2Bapache2%26usg%3DAFQjCNHgNOogLoN0IRLaeG9S_OmAOJIYtA&amp;dt=1253753088464&amp;correlator=1253753088467&amp;frm=0&amp;ga_vid=1597959829.1253753089&amp;ga_sid=1253753089&amp;ga_hid=1380721164&amp;ga_fc=0&amp;u_tz=480&amp;u_his=1&amp;u_java=1&amp;u_h=800&amp;u_w=1280&amp;u_ah=733&amp;u_aw=1280&amp;u_cd=24&amp;u_nplug=9&amp;u_nmime=111&amp;biw=1167&amp;bih=571&amp;fu=0&amp;ifi=1&amp;dtd=94&amp;xpc=VDGzTRTtwn&amp;p=http%3A//www.developertutorials.com" width="300" height="250" frameborder="0" name="google_ads_frame" style="left: 0pt; position: absolute; top: 0pt"></iframe></ins></ins>
			<br />
			</td>
		</tr>
	</tbody>
</table>
<br />
<h3>prerequisites</h3>
<p>
Before you begin, it is highly recommended
(though not inevitable) to create a system user and user group under
which your Apache <a style="border-bottom: 0.075em solid #0066e3 ! important; font-weight: normal ! important; font-size: 100% ! important; text-decoration: underline ! important; padding-bottom: 1px ! important; color: #0066e3 ! important; background-color: transparent ! important; background-image: none; padding-top: 0pt; padding-right: 0pt; padding-left: 0pt" href="http://www.developertutorials.com/tutorials/linux/how-to-install-apache-2-on-linux-7-12-19/page2.html#" target="_blank" class="iAs">server</a> will be running.
</p>
# groupadd www <br />
# useradd -g www apache2   
<p>
What
is it good for? All actions performed by <a style="border-bottom: 1px dotted #0066e3 ! important; font-weight: normal ! important; font-size: 100% ! important; text-decoration: none ! important; padding-bottom: 0px ! important; color: #0066e3 ! important; background-color: transparent ! important; background-image: none; padding-top: 0pt; padding-right: 0pt; padding-left: 0pt" href="http://www.developertutorials.com/tutorials/linux/how-to-install-apache-2-on-linux-7-12-19/page2.html#" target="_blank" class="iAs">Apache<img style="border: 0pt none ; margin: 0pt; padding: 0pt; display: inline ! important; height: 10px; width: 10px; position: relative; top: 1px; left: 1px; float: none" src="http://images.intellitxt.com/ast/adTypes/2.gif" alt="" /></a> (for instance your PHP
scripts execution) will be restricted by this user&#39;s privileges. Thus
you can explicitly rule which directories your PHP scripts may read or
change. Also all files created by Apache (e.g. as a result of executing
your PHP scripts) will be owned by this user (apache2 in my case), and
affiliated with this user group (www in my case).
</p>
<h3>download source </h3>
<p>
Get the source from <a href="http://httpd.apache.org/download.cgi" target="_blank" class="external">http://httpd.apache.org/download.cgi</a>   ( <span class="dirPath">httpd-2.2.4.tar.gz</span>  ). These instructions are known to work with all 2.x.x Apache versions. 
</p>
<h3>unpack, configure, compile </h3>
<p>
Go to the directory with the downloaded file and enter:
</p>
# tar -xzf httpd-2.2.4.tar.gz <br />
# cd httpd-2.2.4 <br />
# ./configure --prefix=/usr/local/apache2 --enable-so --with-included-apr 
<p>
The configure options deserve a little bit more of detail here. The most important --prefix option specifies the location where Apache is to be installed. Another commonly used option --enable-so turns on the <acronym title="Dynamic Shared Object">DSO</acronym> support, i.e. available modules  compiled as shared objects can be loaded or unloaded at runtime. Very handy.
</p>
<p>
To compile some modules statically (they are always loaded, faster execution times), use --enable-<em>module</em> option. To compile a module as a shared object, use --enable-<em>module</em>=shared option.
</p>
<p>
For all available configuration options and their default values check the <a href="http://httpd.apache.org/docs-2.2/programs/configure.html#configurationoptions" target="_blank" title="Apache - Configuration options" class="external">Apache documentation</a> or type ./configure --help.
</p>
<h4>SSL support</h4>
<p>
To support secure connections, you need to specify --enable-ssl option when you run ./configure. In addition to that, you will also have to <a href="http://laffers.net/howtos/howto-install-apache#edit_httpd_conf_for_ssl" target="_blank">configure your httpd.conf</a> file later. 
</p>
<p>
<em>Note: Make sure that openssl is installed on your system before you run ./configure with --enable-ssl. If not, download the latest version from <a href="http://www.openssl.org/source/" target="_blank" class="external">http://www.openssl.org/source/</a> , unpack, configure, make, make install. You will also need to <a href="http://www.google.com/search?hl=en&amp;q=howto+generate+ssl+certificate&amp;btnG=Google+Search" target="_blank" class="external">generate server certificate</a>. Place <span class="dirPath">server.crt</span> and <span class="dirPath">server.key</span> into <span class="dirPath">/etc/ssl/apache2/ </span>directory and make them readable by Apache2. </em>
</p>
<h4>configuration example</h4>
<p>
 For example, to compile the <a href="http://httpd.apache.org/docs-2.0/mod/mod_rewrite.html" target="_blank" class="external">mod_rewrite</a> module statically and <a href="http://httpd.apache.org/docs-2.0/mod/mod_auth_digest.html" class="external">mod_auth_digest</a> as a <acronym title="Dynamic Shared Object">DSO</acronym>, and to enable secure connections, enter:
</p>
# ./configure --prefix=/usr/local/apache2 --enable-so --enable-rewrite --enable-auth-digest=shared --enable-ssl
<p>
<em>Tip: If you are upgrading from older Apache version, you may want to copy <span class="dirPath">config.nice</span>
from the directory to which the previous version was unpacked (if
available) to where you unpacked the new Apache tarball file. Run ./config.nice instead of</em><em> ./configure. This way all the previously used configure options will be applied to the new installation effortlessly.</em>
</p>
<p>
Once you configured everything as you like, compile and install the <a style="border-bottom: 0.075em solid #0066e3 ! important; font-weight: normal ! important; font-size: 100% ! important; text-decoration: underline ! important; padding-bottom: 1px ! important; color: #0066e3 ! important; background-color: transparent ! important; background-image: none; padding-top: 0pt; padding-right: 0pt; padding-l