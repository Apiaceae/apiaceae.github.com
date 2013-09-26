---
layout: post
title: Ubuntu为drupal7配置Apache Solr详细步骤
date: 2012-07-18 15:21
categories: Linux
tags: ubuntu
---

###下面为详细安装步骤，一步步来就能配出如图所示的搜索效果:

**1). 安装Java SDK**

,,,
yum install java-1.6*
,,,

**2).下载最新版本的Solr，当前最新版本是1.4.1 , 经过测试，在国内用bjtu.edu.cn地址下载速度比较快，下载下来后，放到非web目录的文件夹下面，我放在了/home/ruby 目录下面，并重命名为solr**

'''
cd /home/ruby
'''
wget <a title="http://mirror.bjtu.edu.cn/apache/lucene/solr/1.4.1/apache-solr-1.4.1.tgz" href="http://mirror.bjtu.edu.cn/apache/lucene/solr/1.4.1/apache-solr-1.4.1.tgz" target="_blank">http://mirror.bjtu.edu.cn/apache/lucene/solr/1.4.1/apache-solr-1.4.1.tgz</a> <br /><br />tar xvfz apache-solr-1.4.1.tgz<br /><br />mv apache-solr-1.4.1 solr</code></div>
<p>3).下载Drupal的Apache Solr(<a title="http://drupal.org/project/ApacheSolr" href="http://drupal.org/project/ApacheSolr" target="_blank">http://drupal.org/project/ApacheSolr</a>)模块, 如果你有drush,用drush会方便的</p>
<p>多,如果没有drush,就按常规方便，下载解压缩，放到sites/all/modules目录。并下载php的solr库（</p>
<p>http://code.google.com/p/solr-php-client/），放到sites/all/modules/apachesolr根目录,最终结构</p>
<p>为:/sites/all/modules/apachesolr/SolrPhpClient。</p>
<div class="codeblock"><code>cd /var/www/html/yourdrupal_root<br />drush dl apachesolr<br />cd sites/all/modules/apachesolr<br />wget <a title="http://solr-php-client.googlecode.com/files/SolrPhpClient.r22.2009-11-09.zip" href="http://solr-php-client.googlecode.com/files/SolrPhpClient.r22.2009-11-09.zip" target="_blank">http://solr-php-client.googlecode.com/files/SolrPhpClient.r22.2009-11-09...</a> <br />unzip SolrPhpClient.r22.2009-11-09.zip </code></div>
<p>4).根据apachesolr模块里面的说明，复制apachesolr模块里面的schema.xml，solrconfig.xml</p>
<p>到/home/ruby/solr/example/solr目录.</p>
<div class="codeblock"><code>cp /var/www/html/yourdrupal_root/sites/all/modules/apachesolr/schema.xml /home/ruby/solr/example/solr/conf<br />cp /var/www/html/yourdrupal_root/sites/all/modules/apachesolr/solrconfig.xml /home/ruby/solr/example/solr/conf</code></div>
<p>5).测试一下Apache Solr是否工作了？</p>
<div class="codeblock"><code>cd /home/ruby/solr/example<br />java -jar start.jar</code></div>
<p><br />在浏览器中输入http://192.168.1.110:8983/solr/admin/ （192.168.1.110换成你自已的地址）,如果你顺利看到</p>
<p>如下界面，说明你就成功了！</p>
<p><img src="http://drupalsh.cn/userfiles/solr.png" alt="" /></p>
<p>6).按照常规模式启用drupal的Apache Solr模块,OK,到后台配制一下(admin/settings/apachesolr)，测试是否成</p>
<p>功,如果不出意外，你就会看到本文开头的图片效果.</p>
<p>续&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;<br /> 你肯定不想每次都在命令行窗口打开solr服务，好，让我们把solr变成系统服务</p>
<p>7).创建系统启动服务功能</p>
<div class="codeblock"><code>nano -w /etc/init.d/solr</code></div>
<p>复制以下代码:</p>
<div class="codeblock"><code>SOLR_DIR="/home/ruby/solr/example"&nbsp; # 换成你的安装路径<br />JAVA_OPTIONS="-Xmx1024m -DSTOP.PORT=8079 -DSTOP.KEY=stopkey -jar start.jar"<br />LOG_FILE="/var/log/solr.log"<br />JAVA="/usr/bin/java"<br /> <br />case $1 in<br />&nbsp;&nbsp;&nbsp; start)<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; echo "Starting Solr"<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cd $SOLR_DIR<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $JAVA $JAVA_OPTIONS 2&gt; $LOG_FILE &amp;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ;;<br />&nbsp;&nbsp;&nbsp; stop)<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; echo "Stopping Solr"<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cd $SOLR_DIR<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $JAVA $JAVA_OPTIONS --stop<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ;;<br />&nbsp;&nbsp;&nbsp; restart)<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $0 stop<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; sleep 1<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $0 start<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ;;<br />&nbsp;&nbsp;&nbsp; *)<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; echo "Usage: $0 {start|stop|restart}" &gt;&amp;2<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit 1<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ;;<br />esac</code></div>
<p>保存退出,授权</p>
<div class="codeblock"><code>chmod 755 /etc/init.d/solr</code></div>
<p>现在，你可以用以下linux常用命令去启动apache solr了</p>
<div class="codeblock"><code>service solr start<br />service solr stop<br />service solr restart</code></div>
<p>如果需要，还可以加上开机自动开启apache solr</p>
<div class="codeblock"><code>sudo chkconfig --add solr</code></div>
