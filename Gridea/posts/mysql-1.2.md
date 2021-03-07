---
title: 'MySQL数据库-1.2'
date: 2021-03-07 19:38:59
tags: [MySQL,数据库]
published: true
hideInList: false
feature: 
isTop: false
---
数据库技术构成
===

数据库技术的出现是为了更加有效的管理和存取大量的数据资源。简单的来讲，数据库技术主要包括数据库系统，SQL语言，数据库访问技术。

## 数据库系统

数据库系统有3个主要的组成部分。

### 数据库

_数据库（Database System）：用于存储数据的地方。_

### 数据库管理系统

_数据库管理系统（Database Management System，DBMS）：用户管理数据库的软件。_

### 数据库应用程序

_数据库应用程序（Database Application）：为了提高数据库系统的处理能力所使用的管理数据库的软件补充。_


## SQL语言

SQL，(Structured Query Language)即结构化查询语言，数据库管理系统专门通过SQL语言来管理数据库中的数据，与数据库通信。

### SQL的优点:

- SQL不是某个特定数据库供应商专有的语言。几乎所有重要的DBMS都支持SQL，所以，学习此语言使你几乎能与所有数据库打交道。
- SQL简单易学。它的语句全都是由描述性很强的英语单词组成，而且这些单词的数目不多。
- SQL尽管看上去很简单，但它实际上是一种强有力的语言，灵活使用其语言元素，可以进行非常复杂和高级的数据库操作。

> **DBMS专用的SQL**：SQL不是一种专利语言，而且存在一个标准委员会，他们试图定义可供所有DBMS使用的SQL语法，但事实上任意两个DBMS实现的SQL都不完全相同。本书讲授的SQL是专门针对MySQL的，虽然书中所讲授的多数语法也适用于其他DBMS，但不要认为这些SQL语法是完全可移植的。

### SQL为数据库管理系统提供的功能

SQL语言是一种数据库查询和程序设计语言，其主要用于存取数据、查询数据、更新数据和管理数据库系统。具体的，SQL分为4个部分，这里只是大概整理一下，详细的后面我会在SQL相关中仔细整理。

- 数据定义语言（Data Definition Language，DDL）：DROP、CREATE、ALTER等语句；数据库定义语言。主要用于定义数据库、表、视图、索引和触发器等。CREATE语句主要用于创建数据库、创建表、创建视图。ALTER语句主要用于修改表的定义，修改视图的定义。DROP语句主要用于删除数据库、删除表和删除视图等。

- 数据操作语言（Data Manipulation Language，DML）：INSERT、UPDATE、DELETE语句；数据库操作语言。主要用于插入数据，更新数据，删除数据。INSERT语句用于插入数据，UPDATE语句用于更新数据，DELETE语句用于删除数据。

- 数据查询语言（Data Query Language，DQL）：SELECT语句。主要用于查询数据。

- 数据控制语言（Data Control Language，DCL）：数据库控制语言。主要用于控制用户的访问权限。其中GRANT语句用于给用户增加权限，REVOKE语句用于收回用户的权限。

数据库管理系统通过这些SQL语句可以操作数据库中的数据，在应用程序中，也可以通过SQL语句来操作数据。来几个 SQL 语句的例子，这条语句声明创建一个叫 user 的表：

```sql
CREATE TABLE `user` (
  `id`     int(100) unsigned NOT NULL AUTO_INCREMENT,
  `name`   varchar(32) NOT NULL DEFAULT '' COMMENT '姓名',
  `sex`    tinyint(32) NOT NULL DEFAULT 0  COMMENT '性别：0,保密；1,男；2,女',
  `mobile` varchar(20) NOT NULL DEFAULT '' COMMENT '手机',
  PRIMARY KEY (`id`)
);
```

这张表包含 4 个字段，分别为 id、name、sex、mobile，其中 id 定义为表的主键，并且只能为正数的自增长字段。并且字段 sex 有默认值 0，每个 COMMENT 后面均为字段注释。

表定义好了，我们可以向这张表插入数据，下面这条语句是在 user 表中插入一条数据记录：

```sql
INSERT INTO `user` SET name="张三",sex=1,mobile=13811772277;
INSERT INTO `user` VALUES (18,'王小二',0,12322224);
```

上面两条语句执行完之后，user 表中就会相对应增加一行新记录，第一条该记录中 id 是自增长的，部分字段有初始默认值，所以只需插入部分值也是可以插入成功的。第二条是必须按顺序填写对应的值，表中的id 字段比较特殊，所以插入 id 值的时候必须比表中最后一条数据的 id 值大，否则会报错。

插入数据之后我们再使用 SELECT 查询语句获取刚才插入的数据，如下：

```sql 
mysql> SELECT * FROM `user`;

-- +----+-----------+-----+-------------+
-- | id | name      | sex | mobile      |
-- +----+-----------+-----+-------------+
-- |  1 | 张三      |   1 | 13811772277 |
-- | 19 | 王小二    |   0 | 12322224    |
-- +----+-----------+-----+-------------+
```

上面几条 SQL 语句的例子，大家看了之后会有一个印象，知道 SQL 语句语法是什么样子，后面有大量的 SQL 语句知识帮助你学习 SQL 语法，玩好 MySQL。


## 数据库访问技术

这个`数据库访问技术` 小弟认为这个是一个学术性的研究词汇，我在维基百科各种百科对这个词汇要么没有，要么就一句话解释，不知道谁想出的这个词汇，在下甚是佩服，初步了解到这个是个什么技术呢？

不同的程序设计语言会有各自不同的数据库访问方法，这个访问方法称之为一种技术，程序语言通过这些技术，执行 SQL 语句，进行数据库的管理。下面搜集了一些主要的数据库访问技术

### ODBC

Open Database Connectivity(ODBC，开放数据库互连)，提供了一种标准的API（应用程序编程接口）方法来访问数据库管理系统（DBMS）。这些API利用SQL来完成其大部分任务。ODBC本身也提供了对SQL语言的支持，用户可以直接将SQL语句送给ODBC。ODBC的设计者们努力使它具有最大的独立性和开放性：与具体的编程语言无关，与具体的数据库系统无关，与具体的操作系统无关。

### ADO

微软公司的 ActiveX Data Objects（ADO）是一个用于访问数据源的COM组件，作为高层的编程界面层。ADO是在OLE DB之上，包含了很多层次化的COM对象与集合（Collections，也是一类对象，在其里面包含了其他层级对象）。允许开发人员编写访问数据的代码而不用关心数据源是如何实现与访问驱动的，而只用关心到数据库的连接。访问数据库的时候，关于SQL的知识不是必要的，但是特定数据库支持的SQL命令仍可以通过ADO中的命令对象（Command）来执行。

### MDAC

Microsoft Data Access Components（MDAC）是微软专门为数据访问功能而发展的应用程序开发接口，做为微软的统一化数据访问（Universal Data Access; UDA）解决方案的核心组成，最初的版本在1996年8月发表。目前其组成组件有ODBC，OLE DB以及ADO，其中ADO是在Visual Basic上唯一的数据访问管道，而OLE DB则是基于COM之上，供C/C++访问与提供数据的接口，ODBC则是统一化的数据访问API。

### JDBC

Java Database Connectivity（JDBC，Java数据库连接）是Java语言中用来规范客户端程序如何来访问数据库的应用程序接口，提供了诸如查询和更新数据库中数据的方法。JDBC也是Sun Microsystems的商标。JDBC是面向关系型数据库的。