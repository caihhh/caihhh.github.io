---
layout: post
title:  Mysql error：1045 Access denied for user user@host
category: Database
tags: Mysql Database
description: 
---

## 问题
```
[sankuai@yf-mos-integration-test01 cube]$ mysql -h 10.5.249.29  -u root -p<password>
ERROR 1045 (28000): Access denied for user 'root'@'yf-mos-integration-test01.yf.sankuai.com' (using password: YES)
```
## 原因
Mysql中未对相关host进行授权

## 方法
###### 1.利用localhost进入mysql

```
mysql -h localhost -u root -p<password>
or
mysql -u root -p<password>
```
###### 2.查看mysql的用户和主机信息

```
root@(none)12:21:57>SELECT user, host FROM mysql.user;
+--------------+-------------+
| user         | host        |
+--------------+-------------+
| billing      | %           |
| cds          | %           |
| ebs          | %           |
| egw          | %           |
| keystone     | 127.0.0.1   |
| ebs          | localhost   |
| mos_security | localhost   |
| root         | localhost   |
| zabbix       | localhost   |
+--------------+-------------+
```
###### 3.查看授权信息

```
root@(none)12:26:34>show grants for root@'localhost';
+----------------------------------------------------------------------------------------------------------------------------------------+
| Grants for root@localhost                                                                                                              |
+----------------------------------------------------------------------------------------------------------------------------------------+
| GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' IDENTIFIED BY PASSWORD '*15C580D021946B272F501E006E4908D263B397FB' WITH GRANT OPTION |
| GRANT PROXY ON ''@'' TO 'root'@'localhost' WITH GRANT OPTION                                                                           |
+----------------------------------------------------------------------------------------------------------------------------------------+
```
###### 4.添加授权信息，然后退出mysql重新登录即可用之前的host连接或者登录mysql

```
root@(none)12:26:47>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY PASSWORD '*15C580D021946B272F501E006E4908D263B397FB' WITH GRANT OPTION;
Query OK, 0 rows affected (0.00 sec)

root@(none)12:27:40>flush privileges;
Query OK, 0 rows affected (0.00 sec)
```





