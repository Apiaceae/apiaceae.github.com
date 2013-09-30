---
layout: post
title: Ubuntu服务器配置Ruby On Rails开发环境
date: 2009-09-23 23:58:00
comments: true
sharing: true
categories: linux
tags: 
---

<p>
首先安装Ubuntu服务器版本 Server，我使用的是9.04版本<br />
UPDATED FOR UBUNTU 9.04 HARDY HERON<br />
* Ubuntu packages information [http://packages.ubuntu.com/]<br />
Originally based on Ref: [http://www.rubystarman.org/wiki/UbuntuEdgyEft]<br />
<br />
Install Ubuntu<br />
* Download iso for Ubuntu, use it to install barebone server (without LAMP)<br />
* uncomment universe, security and multiverse sources in /etc/apt/sourses.list, comment out cdrom source<br />
<br />
Upgrade installed server<br />
sudo apt-get update<br />
sudo apt-get dist-upgrade<br />
Install Ruby and other things<br />
sudo apt-get install ssh ruby ruby1.8 ri1.8 rdoc1.8 irb1.8 irb rdoc \<br />
libreadline-ruby1.8 libopenssl-ruby1.8 libmysql-ruby libfcgi-ruby1.8 \<br />
libsqlite3-ruby build-essential ruby1.8-dev libpcre3-dev libssl-dev \<br />
libdb4.3-dev libneon26-dev python-dev python-setuptools python-docutils \<br />
python-clearsilver python-pysqlite2 enscript nmap libncurses5-dev \<br />
libsqlite3-dev sqlite3 sqlite3-doc libbz2-dev expat libexpat1-dev, git-core<br />
download !RubyGems<br />
create ~/software dir, go to !RubyGems website [http://docs.rubygems.org/] to find download url.<br />
In my case it was !http://rubyforge.org/frs/download.php/35283/rubygems-1.1.1.tgz<br />
<br />
cd \~/software<br />
wget (URL to download)<br />
tar xf (downloaded filename)<br />
cd (unarchived directory)<br />
sudo ruby setup.rb<br />
sudo gem install rails mongrel \--include-dependencies<br />
Select which gem to install for your platform (i486-linux) \[Select 2 for Ruby\]<br />
&amp;nbsp;1. mongrel 1.0.1 (mswin32)<br />
&amp;nbsp;2. mongrel 1.0.1 (ruby)<br />
&amp;nbsp;3. mongrel 1.0 (mswin32)<br />
&amp;nbsp;4. mongrel 1.0 (ruby)<br />
&amp;nbsp;5. Skip this gem<br />
&amp;nbsp;6. Cancel installation<br />
&gt; 2<br />
Select which gem to install for your platform (i486-linux) \[Select 1 for Ruby\]<br />
&amp;nbsp;1. fastthread 1.0 (ruby)<br />
&amp;nbsp;2. fastthread 1.0 (mswin32)<br />
&amp;nbsp;3. fastthread 0.6.4.1 (mswin32)<br />
&amp;nbsp;4. fastthread 0.6.4.1 (ruby)<br />
&amp;nbsp;5. Skip this gem<br />
&amp;nbsp;6. Cancel installation<br />
&gt; 1<br />
Install MySQL<br />
sudo apt-get install mysql-server<br />
* after creating a user for yourself you can add its data into .my.cnf file. After you&#39;ve done it you can get to mysql just by typing mysql in command line<br />
cd<br />
touch .my.sql<br />
echo &quot;\[client\]<br />
user = DBUSERNAME<br />
password = DBPASSWORD<br />
host = DBSERVER<br />
\[mysql\]<br />
database = DBNAME&quot; &gt; .my.cnf<br />
chmod 400 .my.cnf<br />
Sun Java<br />
sudo apt-get install sun-java6-jdk sun-java6-plugin<br />
\#then<br />
sudo update-java-alternatives<br />
Jruby<br />
* Get latest src for jruby from [http://dist.codehaus.org/jruby/]<br />
in my case it was !http://dist.codehaus.org/jruby/jruby-src-1.1.2.tar.gz<br />
<br />
cd \~/software<br />
tar zxvf (downloaded filename)<br />
cd (unarchived directory)<br />
ant clean jar<br />
cd /usr/local<br />
sudo mv \~/software/(unarchived directory) .<br />
sudo ln \-s (unarchived_directory) jruby<br />
echo &quot;export PATH=$PATH:/usr/local/jruby/bin&quot; &gt;&gt; \~/.bashrc<br />
. \~/.bashrc<br />
jruby \-S gem install jruby-openssl rails rake mongrel hpricot haml activerecord-jdbcmysql-adapter activerecord-jdbcderby-adapter glassfish<br />
\# if rails install gives out of memory error try<br />
jruby \-J-XX:-UseGCOverheadLimit \-S gem install rails<br />
Install Apache 2.2<br />
* Apache 2.2 is now distributed with feisty 7.04 so compiling by source is not needed for plain vanilla install<br />
* Get Apache 2.2 code: go to [http://httpd.apache.org/download.cgi] and find the right link to download<br />
In my case it was !http://download.filehat.com/apache/httpd/httpd-2.2.8.tar.gz<br />
<br />
cd \~/software<br />
wget (URL to download)<br />
tar xf (downloaded filename)<br />
cd (unarchived directory)<br />
./configure \--with-external-pcre=/usr \--with-included-apr \--with-berkeley-db=/usr \<br />
&amp;nbsp;--enable-deflate \--enable-rewrite \--enable-auth-digest&amp;nbsp; \--enable-dav=shared \<br />
&amp;nbsp;--enable-proxy=shared \--enable-proxy-balancer=shared \--enable-proxy-http=shared \<br />
&amp;nbsp;--enable-ssl=shared \--enable-headers=shared<br />
make<br />
sudo make install<br />
Note: for webdav filesystem add the following:<br />
\--enable-dav-fs=shared&amp;nbsp; \--enable-setenvif=shared \--enable-alias=shared \--enable-authn-file=shared<br />
Install mod_fcgid<br />
go to mod_fcgid website [http://fastcgi.coremail.cn/] find download url<br />
in my case it was !http://prdownloads.sourceforge.net/mod-fcgid/mod_fcgid.2.1.tar.gz?download<br />
<br />
cd \~/software<br />
wget (URL to download)<br />
tar xf (downloaded filename)<br />
cd (unarchived directory)<br />
make<br />
sudo make install<br />
Install Subversion<br />
libneon 0.26 in Ubuntu 8.04 comes without one library. So we will complile neon as well<br />
Currently subversion needs !http://www.webdav.org/neon/neon-0.25.5.tar.gz<br />
<br />
cd \~/software<br />
wget (URL to download<br />
tar xf (downloaded filename)<br />
cd (unarchived directory<br />
./configure \--with-ssl \--enable-shared<br />
make<br />
sudo make install<br />
go to Subversion website [http://subversion.tigris.org/] find download url<br />
in my case it is !http://subversion.tigris.org/downloads/subversion-1.4.6.tar.gz<br />
cd \~/software<br />
wget (URL to download)<br />
tar xf (downloaded filename)<br />
cd (unarchived directory)<br />
./configure \--with-apr=/usr/local/apache2 \--with-apr-util=/usr/local/apache2 \--with-neon=/usr/local<br />
make<br />
sudo make install<br />
Install svn-python<br />
Subversion comes with a Python binding that Trac will use.<br />
<br />
cd \~/software/(subversion directory)<br />
make swig-py<br />
sudo make install-swig-py<br />
Python came with Ubuntu so it&#39;s in /usr but subversion installed the library in /usr/local. We&#39;ll have to link them up.<br />
sudo nano /usr/lib/python2.5/site-packages/svn.pth<br />
\#The file should contain a single line, the path to svn-python:<br />
/usr/local/lib/svn-python<br />
install Trac<br />
As of this writing, version 0.10.3.1 is the current stable release.<br />
Or you can use 0.11beta version instead<br />
Trac download [http://trac.edgewall.org/wiki/TracDownload]<br />
in my case it was [http://ftp.edgewall.com/pub/trac/trac-0.10.4.tar.gz]<br />
<br />
cd \~/software<br />
wget (URL to download)<br />
tar xf (downloaded filename)<br />
cd (unarchived directory)<br />
sudo python setup.py install<br />
Install mod_python<br />
To best run Trac under Apache 2.2 you&#39;ll want mod_python.<br />
mod_python download [http://httpd.apache.org/modules/python-download.cgi]<br />
in my case it was [http://mirror.olnevhost.net/pub/apache/httpd/modpython/mod_python-3.3.1.tgz]<br />
<br />
cd \~/software<br />
wget (URL to download)<br />
tar xf (downloaded filename)<br />
cd (unarchived directory)<br />
./configure \--with-apxs=/usr/local/apache2/bin/apxs<br />
make<br />
sudo make install<br />
Install !SilverCity<br />
&nbsp;*Not needed for Trac 011*<br />
!SilverCity provides additional syntax highlighting for Trac. It has Ruby and CSS support which enscript lacks.<br />
!SilverCity website [http://sourceforge.net/projects/silvercity/]<br />
in my case it was [http://downloads.sourceforge.net/silvercity/SilverCity-0.9.7.tar.gz]<br />
<br />
cd \~/software<br />
wget (URL to download)<br />
tar xf (downloaded filename)<br />
cd (unarchived directory)<br />
sudo python setup.py install<br />
!WebAdmin for Trac<br />
&nbsp;*Not needed for Trac 0.11*<br />
The next major version of Trac will come with !WebAdmin. We can get it now as a plugin. When downloading plugins from