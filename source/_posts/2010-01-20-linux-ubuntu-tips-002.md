---
layout: default
title: Linux Ubuntu8.04常用操作命令
date: 2010-01-20 15:30
comments: true
categories: [Linux]
---

*1. 如何完全的卸载MySQL*
```
sudo apt-get --purge remove mysql-server-5.1 mysql-common mysql-client libmysqlclient15-dev libmysql-ruby
```
卸载过程中会询问你是否要卸载所有相关的配置文件已经数据库，选择Yes。

*2. 安装完MySQL后如何设置root用户的密码*
```
mysqladmin -u root password new-password
```