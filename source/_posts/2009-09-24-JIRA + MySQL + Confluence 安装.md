---
layout: post
title: JIRA + MySQL + Confluence 安装
date: 2009-09-24 03:12:48
comments: true
sharing: true
categories: linux
tags: 
---

<h2 class="post-title">JIRA + MySQL + Confluence 安装</h2>
<table border="0" cellspacing="0" width="100%" class="fixedTable blogpost">
	<tbody>
		<tr>
			<td class="ellipse"><span class="bvTitle"><strong><font size="3">JIRA + MySQL + Confluence 安装</font></strong></span></td>
		</tr>
		<tr>
			<td class="bvh8">&nbsp;</td>
		</tr>
		<tr>
			<td id="msgcns!804037BC681CF72D!112">
			<p>
			JIRA + MySQL + Confluence 安装
			</p>
			<p>
			&nbsp;
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp; 官方有详细文档：<a href="http://www.atlassian.com/software/jira/docs/latest/"><font color="#004377">http://www.atlassian.com/software/jira/docs/latest/</font></a>
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;<strong><font size="4"> 1.1 </font></strong><a href="http://www.atlassian.com/software/jira/docs/latest/requirements.html"><strong><font size="4" color="#004377">安装前确认软硬件配置需求</font></strong></a>
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (1) 软件需求：
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;需JAVA支持，已内嵌 HSQL 数据库引擎，如用于正式应用，建议使用 <a href="http://www.mysql.com/"><u><font color="#800080">MySQL</font></u></a> or <a href="http://www.postgresql.org/"><u><font color="#0000ff">PostgreSQL</font></u></a>。
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(2) 硬件建议:&nbsp;
			</p>
			<ul>
				<li>&nbsp;评估安装&nbsp;需要 1.5GHz 主频＋ 256MB 内存即可; </li>
				<li>&nbsp;10－20个项目/100－200用户/1000－5000问题数，需要2.8GHz主频 + 256-512MB内存 </li>
				<li>&nbsp;更多更大项目/10万问题数,&nbsp; 1G内存足够了 </li>
			</ul>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;作为参考 <a href="http://jira.atlassian.com/"><u><font color="#0000ff">jira.atlassian.com</font></u></a> 有14,000问题和10,000用户，最高负载没分钟30个页面需求，目前使用双2.8GHZ Xeon CPU + 450MB内存
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
			</p>
			<p>
			<font size="4">&nbsp;&nbsp;&nbsp;&nbsp; 1.2 </font><a href="http://www.atlassian.com/software/jira/docs/latest/java.html"><font size="4" color="#004377">安装JAVA JDK，设置JAVA_HOME，及添加JDK可执行目录bin到path路径</font></a>
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; JIRA 运行需要JDK 1.3 或更高版本，可从 <a href="http://java.sun.com/j2se/1.5.0/jdk/download.jsp"><u><font color="#0000ff">Sun&#39;s website</font></u></a>&nbsp;下载windows&nbsp;offline 版本安装:
			</p>
			<p>
			<strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Linux </strong>用户要 要安装<strong>xorg-x11-deprecated-libs包</strong> (Fedora) 获类似支持包以避免如下错误:
			</p>
			<pre>
									    java.lang.UnsatisfiedLinkError: /opt/j2sdk1.4.2_11/jre/lib/i386/libawt.so: libXp.so.6: cannot open<br />
			<br />
						<br />
			<br />
									    shared object file: No such file or directory<br />
			<br />
						<br />
			<br />
									            <br />
			<br />
									<br />
						
			<table border="0" cellspacing="0" cellpadding="0" width="100%">
				<tbody>
					<tr>
						<td width="9" height="10">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </td>
						<td>
						<h3>&nbsp;设置JAVA_HOME系统环境变量</h3>
						</td>
						<td>&nbsp;</td>
					</tr>
					<tr>
						<td>&nbsp;</td>
						<td bgcolor="#a5b6c6">&nbsp;</td>
						<td>&nbsp;</td>
					</tr>
				</tbody>
			</table>
			<br />
						<br />
			<br />
									<br />
			<br />
						<br />
			<br />
									            <br />
			<br />
									<br />
						
			</pre>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp; 在控制面板，右键点击&ldquo;我的电脑&rdquo;图标，选择属性
			</p>
			<ol>
				<li>点击&ldquo;<strong>高级</strong>&rdquo; 页 </li>
				<li>点击&ldquo;<strong>环境变量</strong>&rdquo;按钮 </li>
				<li>点击 &ldquo;<strong>新建</strong>&rdquo; 系统环境变量 </li>
				<li>设置 <strong>JAVA_HOME</strong> 指向 Java安装目录,不是 Bin目录. </li>
				<li>cmd 或 Dos 下执行&nbsp;％Java_Home％\bin\javac, 确认变量设置无误 </li>
			</ol>
			<p>
			&nbsp;&nbsp;&nbsp;<font size="4">1.3 </font><a href="http://http//www.atlassian.com/software/jira/docs/latest/install.html"><font size="4" color="#004377">安装JIRA，直接解压即可</font></a>
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <a href="http://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-enterprise-3.6.2-standalone.zip"><font color="#004377">http://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-enterprise-3.6.2-standalone.zip</font></a>
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp; <font size="4">1.4 </font><a href="http://www.atlassian.com/software/jira/docs/latest/standalone-dbconfig.html"><font color="#004377"><font size="4">安装MySQL数据库</font>，创建JIRADB，同时下载 JDBC for MySQL 驱动jar文件到Jira/common/lib/目录</font></a>, 注意数据库设置使用UTF-8支持中文&nbsp; http://<a href="http://www.mysql.com/"><font color="#004377">www.mysql.com</font></a>
			</p>
			<p>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 按照要求编辑conf/server.xml和atlassian-jira/WEB-INF/classes/entityengine.xml，注意数据库名和前面创建要一致:
			</p>
			<ol>
				<li>安装MySQL:http://dev.mysql.com/downloads/ </li>
				<li>创建JIRA连接用户(如 <strong>jirauser</strong>). </li>
				<li>创建JIRA数据库 (如 <strong>jiradb</strong>). </li>
				<li>确认数据库JIRA连接用户有权限连接数据库、创建和使用数据表 </li>
				<li>
				<p>
				把MySQL JDBC driver jar 文件拷到 <span>common/lib/</span> 目录. <a href="http://ekylin.spaces.msn.com/mmm2006-06-19_17.24/#specific_databases"><u><font color="#0000ff">[download driver]</font></u></a> 
				</p>
				</li>
				<li>
				<p>
				编辑 <strong>conf/server.xml</strong> 文件,&nbsp; 设置用户名、密码、驱动类名、数据源 url参数：
				</p>
				<pre>
												&lt;Server port=&quot;8005&quot; shutdown=&quot;SHUTDOWN&quot;&gt;
				&lt;Service name=&quot;Catalina&quot;&gt;
				&lt;Connector port=&quot;8080&quot;
				maxHttpHeaderSize=&quot;8192&quot; maxThreads=&quot;150&quot; minSpareThreads=&quot;25&quot; maxSpareThreads=&quot;75&quot;
				enableLookups=&quot;false&quot; redirectPort=&quot;8443&quot; acceptCount=&quot;100&quot; connectionTimeout=&quot;20000&quot; disableUploadTimeout=&quot;true&quot; /&gt;
				&lt;Engine name=&quot;Catalina&quot; defaultHost=&quot;localhost&quot;&gt;
				&lt;Host name=&quot;localhost&quot; appBase=&quot;webapps&quot; unpackWARs=&quot;true&quot; autoDeploy=&quot;true&quot;&gt;
				&lt;Context path=&quot;&quot; docBase=&quot;${catalina.home}/atlassian-jira&quot; reloadable=&quot;true&quot;&gt;
				&lt;Resource name=&quot;jdbc/JiraDS&quot; auth=&quot;Container&quot; type=&quot;javax.sql.DataSource&quot;
				username=&quot;<strong>[enter db username]</strong>&quot;
				password=&quot;<strong>[enter db password]</strong>&quot;
				driverClassName=&quot;<strong>com.mysql.jdbc.Driver</strong>&quot;
				url=&quot;<strong>jdbc:mysql://localhost/jiradb?autoReconnect=true&amp;amp;useUnicode=true&amp;amp;characterEncoding=UTF8</strong>&quot;
				<strong>[ delete the minEvictableIdleTimeMillis and timeBetweenEvictionRunsMillis params here ]</strong>
				/&gt;
				&lt;Resource name=&quot;UserTransaction&quot; auth=&quot;Container&quot; type=&quot;javax.transaction.UserTransaction&quot;
				factory=&quot;org.objectweb.jotm.UserTransactionFactory&quot; jotm.timeout=&quot;60&quot;/&gt;
				&lt;Manager className=&quot;org.apache.catalina.session.PersistentManager&quot; saveOnRestart=&quot;false&quot;/&gt;
				&lt;/Context&gt;
				&lt;/Host&gt;
				&lt;/Engine&gt;
				&lt;/Service&gt;
				&lt;/Server&gt;
				</pre>
				</li>
				<li>在n <span>conf/server.xml文件里删除</span> <strong>minEvictableIdleTimeMillis</strong> 和 <strong>ti