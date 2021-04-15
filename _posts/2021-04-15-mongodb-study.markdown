---
layout: post
title:  "MongodDB的学习"
date:   2021-04-14 08:45:50
categories: IT
tags: 数据库 NoSQL MongoDB
excerpt: 记录学习MongoDB
mathjax: true
---

* content
{:toc}

# NoSQL 简介
NoSQL(NoSQL = Not Only SQL )，意即"不仅仅是SQL"。

在现代的计算系统上每天网络上都会产生庞大的数据量。

这些数据有很大一部分是由关系数据库管理系统（RDBMS）来处理。 1970年 E.F.Codd's提出的关系模型的论文 "A relational model of data for large shared data banks"，这使得数据建模和应用程序编程更加简单。

通过应用实践证明，关系模型是非常适合于客户服务器编程，远远超出预期的利益，今天它是结构化数据存储在网络和商务应用的主导技术。

NoSQL 是一项全新的数据库革命性运动，早期就有人提出，发展至2009年趋势越发高涨。NoSQL的拥护者们提倡运用非关系型的数据存储，相对于铺天盖地的关系型数据库运用，这一概念无疑是一种全新的思维的注入。

## 关系型数据库遵循ACID规则
事务在英文中是transaction，和现实世界中的交易很类似，它有如下四个特性：

1. **A (Atomicity) 原子性**

原子性很容易理解，也就是说事务里的所有操作要么全部做完，要么都不做，事务成功的条件是事务里的所有操作都成功，只要有一个操作失败，整个事务就失败，需要回滚。

比如银行转账，从A账户转100元至B账户，分为两个步骤：1）从A账户取100元；2）存入100元至B账户。这两步要么一起完成，要么一起不完成，如果只完成第一步，第二步失败，钱会莫名其妙少了100元。

2. **C (Consistency) 一致性**

一致性也比较容易理解，也就是说数据库要一直处于一致的状态，事务的运行不会改变数据库原本的一致性约束。

例如现有完整性约束a+b=10，如果一个事务改变了a，那么必须得改变b，使得事务结束后依然满足a+b=10，否则事务失败。

3. **I (Isolation) 独立性**

所谓的独立性是指并发的事务之间不会互相影响，如果一个事务要访问的数据正在被另外一个事务修改，只要另外一个事务未提交，它所访问的数据就不受未提交事务的影响。

比如现在有个交易是从A账户转100元至B账户，在这个交易还未完成的情况下，如果此时B查询自己的账户，是看不到新增加的100元的。

4. **D (Durability) 持久性**

持久性是指一旦事务提交后，它所做的修改将会永久的保存在数据库上，即使出现宕机也不会丢失。

## 分布式系统
分布式系统（distributed system）由多台计算机和通信的软件组件通过计算机网络连接（本地网络或广域网）组成。

分布式系统是建立在网络之上的软件系统。正是因为软件的特性，所以分布式系统具有高度的内聚性和透明性。

因此，网络和分布式系统之间的区别更多的在于高层软件（特别是操作系统），而不是硬件。

分布式系统可以应用在不同的平台上如：Pc、工作站、局域网和广域网上等。

## 分布式计算的优点
**可靠性（容错） ：**

分布式计算系统中的一个重要的优点是可靠性。一台服务器的系统崩溃并不影响到其余的服务器。

**可扩展性：**

在分布式计算系统可以根据需要增加更多的机器。

**资源共享：**

共享数据是必不可少的应用，如银行，预订系统。

**灵活性：**

由于该系统是非常灵活的，它很容易安装，实施和调试新的服务。

**更快的速度：**

分布式计算系统可以有多台计算机的计算能力，使得它比其他系统有更快的处理速度。

**开放系统：**

由于它是开放的系统，本地或者远程都可以访问到该服务。

**更高的性能：**

相较于集中式计算机网络集群可以提供更高的性能（及更好的性价比）。

## 分布式计算的缺点
**故障排除：**

故障排除和诊断问题。

**软件：**

更少的软件支持是分布式计算系统的主要缺点。

**网络：**

网络基础设施的问题，包括：传输问题，高负载，信息丢失等。

**安全性：**

开放系统的特性让分布式计算系统存在着数据的安全性和共享的风险等问题。

## 什么是NoSQL?
NoSQL，指的是非关系型的数据库。NoSQL有时也称作Not Only SQL的缩写，是对不同于传统的关系型数据库的数据库管理系统的统称。

NoSQL用于超大规模数据的存储。（例如谷歌或Facebook每天为他们的用户收集万亿比特的数据）。这些类型的数据存储不需要固定的模式，无需多余操作就可以横向扩展。

## 为什么使用NoSQL ?
今天我们可以通过第三方平台（如：Google,Facebook等）可以很容易的访问和抓取数据。用户的个人信息，社交网络，地理位置，用户生成的数据和用户操作日志已经成倍的增加。我们如果要对这些用户数据进行挖掘，那SQL数据库已经不适合这些应用了, NoSQL 数据库的发展却能很好的处理这些大的数据。


## RDBMS vs NoSQL
### RDBMS
- 高度组织化结构化数据
- 结构化查询语言（SQL） (SQL)
- 数据和关系都存储在单独的表中。
- 数据操纵语言，数据定义语言
- 严格的一致性
- 基础事务

### NoSQL
- 代表着不仅仅是SQL
- 没有声明性查询语言
- 没有预定义的模式
-键 - 值对存储，列存储，文档存储，图形数据库
- 最终一致性，而非ACID属性
- 非结构化和不可预知的数据
- CAP定理
- 高性能，高可用性和可伸缩性

## NoSQL 简史
NoSQL一词最早出现于1998年，是Carlo Strozzi开发的一个轻量、开源、不提供SQL功能的关系数据库。

2009年，Last.fm的Johan Oskarsson发起了一次关于分布式开源数据库的讨论[2]，来自Rackspace的Eric Evans再次提出了NoSQL的概念，这时的NoSQL主要指非关系型、分布式、不提供ACID的数据库设计模式。

2009年在亚特兰大举行的"no:sql(east)"讨论会是一个里程碑，其口号是"select fun, profit from real_world where relational=false;"。因此，对NoSQL最普遍的解释是"非关联型的"，强调Key-Value Stores和文档数据库的优点，而不是单纯的反对RDBMS。

## CAP定理（CAP theorem）
在计算机科学中, CAP定理（CAP theorem）, 又被称作 布鲁尔定理（Brewer's theorem）, 它指出对于一个分布式计算系统来说，不可能同时满足以下三点:

+ **一致性(Consistency)** (所有节点在同一时间具有相同的数据)
+ **可用性(Availability)** (保证每个请求不管成功或者失败都有响应)
+ **分隔容忍(Partition tolerance)** (系统中任意信息的丢失或失败不会影响系统的继续运作)

CAP理论的核心是：一个分布式系统不可能同时很好的满足一致性，可用性和分区容错性这三个需求，最多只能同时较好的满足两个。

因此，根据 CAP 原理将 NoSQL 数据库分成了满足 CA 原则、满足 CP 原则和满足 AP 原则三 大类：

+ CA - 单点集群，满足一致性，可用性的系统，通常在可扩展性上不太强大。
+ CP - 满足一致性，分区容忍性的系统，通常性能不是特别高。
+ AP - 满足可用性，分区容忍性的系统，通常可能对一致性要求低一些。

## NoSQL的优点/缺点
###优点:

- 高可扩展性
- 分布式计算
- 低成本
- 架构的灵活性，半结构化数据
- 没有复杂的关系

### 缺点:

- 没有标准化
- 有限的查询功能（到目前为止）
- 最终一致是不直观的程序

## BASE
BASE：Basically Available, Soft-state, Eventually Consistent。 由 Eric Brewer 定义。

CAP理论的核心是：一个分布式系统不可能同时很好的满足一致性，可用性和分区容错性这三个需求，最多只能同时较好的满足两个。

BASE是NoSQL数据库通常对可用性及一致性的弱要求原则:

+ Basically Availble --基本可用
+ Soft-state --软状态/柔性事务。 "Soft state" 可以理解为"无连接"的, 而 "Hard state" 是"面向连接"的
+ Eventual Consistency -- 最终一致性， 也是 ACID 的最终目的。


# MongoDB 简介
## 什么是MongoDB ?
MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。

在高负载的情况下，添加更多的节点，可以保证服务器性能。

MongoDB 旨在为WEB应用提供可扩展的高性能数据存储解决方案。

MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。

## 主要特点
+ MongoDB 是一个面向文档存储的数据库，操作起来比较简单和容易。
+ 你可以在MongoDB记录中设置任何属性的索引 (如：FirstName="Sameer",Address="8 Gandhi Road")来实现更快的排序。
+ 你可以通过本地或者网络创建数据镜像，这使得MongoDB有更强的扩展性。
+ 如果负载的增加（需要更多的存储空间和更强的处理能力） ，它可以分布在计算机网络中的其他节点上这就是所谓的分片。
+ Mongo支持丰富的查询表达式。查询指令使用JSON形式的标记，可轻易查询文档中内嵌的对象及数组。
+ MongoDb 使用update()命令可以实现替换完成的文档（数据）或者一些指定的数据字段 。
+ Mongodb中的Map/reduce主要是用来对数据进行批量处理和聚合操作。
+ Map和Reduce。Map函数调用emit(key,value)遍历集合中所有的记录，将key与value传给Reduce函数进行处理。
+ Map函数和Reduce函数是使用Javascript编写的，并可以通过db.runCommand或mapreduce命令来执行MapReduce操作。
+ GridFS是MongoDB中的一个内置功能，可以用于存放大量小文件。
+ MongoDB允许在服务端执行脚本，可以用Javascript编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可。
+ MongoDB支持各种编程语言:RUBY，PYTHON，JAVA，C++，PHP，C#等多种语言。
+ MongoDB安装简单。

## 历史
+ 2007年10月，MongoDB由10gen团队所发展。2009年2月首度推出。
+ 2012年05月23日，MongoDB2.1 开发分支发布了! 该版本采用全新架构，包含诸多增强。
+ 2012年06月06日，MongoDB 2.0.6 发布，分布式文档数据库。
+ 2013年04月23日，MongoDB 2.4.3 发布，此版本包括了一些性能优化，功能增强以及bug修复。
+ 2013年08月20日，MongoDB 2.4.6 发布。
+ 2013年11月01日，MongoDB 2.4.8 发布。
+ ……

## MongoDB 下载
你可以在mongodb官网下载该安装包，地址为：[https://www.mongodb.com/download-center#community](https://www.mongodb.com/download-center#community)。MonggoDB支持以下平台:

+ OS X 32-bit
+ OS X 64-bit
+ Linux 32-bit
+ Linux 64-bit
+ Windows 32-bit
+ Windows 64-bit
+ Solaris i86pc
+ Solaris 64

## 语言支持
MongoDB有官方的驱动如下：

+ C
+ C++
+ C# / .NET
+ Erlang
+ Haskell
+ Java
+ JavaScript
+ Lisp
+ node.JS
+ Perl
+ PHP
+ Python
+ Ruby
+ Scala

## MongoDB 工具
有几种可用于MongoDB的管理工具。

### 监控
MongoDB提供了网络和系统监控工具Munin，它作为一个插件应用于MongoDB中。

Gangila是MongoDB高性能的系统监视的工具，它作为一个插件应用于MongoDB中。

基于图形界面的开源工具 Cacti, 用于查看CPU负载, 网络带宽利用率,它也提供了一个应用于监控 MongoDB 的插件。

### GUI
+ Fang of Mongo – 网页式,由Django和jQuery所构成。
+ Futon4Mongo – 一个CouchDB Futon web的mongodb山寨版。
+ Mongo3 – Ruby写成。
+ MongoHub – 适用于OSX的应用程序。
+ Opricot – 一个基于浏览器的MongoDB控制台, 由PHP撰写而成。
+ Database Master — Windows的mongodb管理工具
+ RockMongo — 最好的PHP语言的MongoDB管理工具，轻量级, 支持多国语言

## MongoDB 应用案例
下面列举一些公司MongoDB的实际应用：

+ Craiglist上使用MongoDB的存档数十亿条记录。
+ FourSquare，基于位置的社交网站，在Amazon EC2的服务器上使用MongoDB分享数据。
+ Shutterfly，以互联网为基础的社会和个人出版服务，使用MongoDB的各种持久性数据存储的要求。
+ bit.ly, 一个基于Web的网址缩短服务，使用MongoDB的存储自己的数据。
+ spike.com，一个MTV网络的联营公司， spike.com使用MongoDB的。
+ Intuit公司，一个为小企业和个人的软件和服务提供商，为小型企业使用MongoDB的跟踪用户的数据。
+ sourceforge.net，资源网站查找，创建和发布开源软件免费，使用MongoDB的后端存储。
+ etsy.com ，一个购买和出售手工制作物品网站，使用MongoDB。
+ 纽约时报，领先的在线新闻门户网站之一，使用MongoDB。
+ CERN，著名的粒子物理研究所，欧洲核子研究中心大型强子对撞机的数据使用MongoDB。

# MongoDB 概念解析
不管我们学习什么数据库都应该学习其中的基础概念，在mongodb中基本的概念是文档、集合、数据库，下面我们挨个介绍。

|SQL术语/概念 |	MongoDB术语/概念	|解释/说明|
| ---- | ---- | ---- |
|database|	database|	数据库|
|table	|collection|	数据库表/集合|
|row	|document	|数据记录行/文档|
|column	|field|	数据字段/域|
|index	|index|	索引|
|table |joins	 |	表连接,MongoDB不支持|
|primary key	|primary key|	主键,MongoDB自动将_id字段设置为主键|

通过下图实例，我们也可以更直观的了解Mongo中的一些概念：

![Mongo](./images/Figure-1-Mapping-Table-to-Collection-1.png)

## 数据库
一个mongodb中可以建立多个数据库。

MongoDB的默认数据库为"db"，该数据库存储在data目录中。

MongoDB的单个实例可以容纳多个独立的数据库，每一个都有自己的集合和权限，不同的数据库也放置在不同的文件中。

**"show dbs"** 命令可以显示所有数据的列表。

```
$ ./mongo
MongoDB shell version: 3.0.6
connecting to: test
> show dbs
local  0.078GB
test   0.078GB
> 
```

执行 "**db**" 命令可以显示当前数据库对象或集合。

```
$ ./mongo
MongoDB shell version: 3.0.6
connecting to: test
> db
test
> 
```

运行"use"命令，可以连接到一个指定的数据库。
```
> use local
switched to db local
> db
local
> 
```

以上实例命令中，"local" 是你要链接的数据库。

数据库也通过名字来标识。数据库名可以是满足以下条件的任意UTF-8字符串。

+ 不能是空字符串（"")。
+ 不得含有' '（空格)、.、$、/、\和\0 (空字符)。
+ 应全部小写。
+ 最多64字节。

有一些数据库名是保留的，可以直接访问这些有特殊作用的数据库。

+ admin： 从权限的角度来看，这是"root"数据库。要是将一个用户添加到这个数据库，这个用户自动继承所有数据库的权限。一些特定的服务器端命令也只能从这个数据库运行，比如列出所有的数据库或者关闭服务器。
+ local: 这个数据永远不会被复制，可以用来存储限于本地单台服务器的任意集合
+ config: 当Mongo用于分片设置时，config数据库在内部使用，用于保存分片的相关信息。

## 文档(Document)
文档是一组键值(key-value)对(即 BSON)。MongoDB 的文档不需要设置相同的字段，并且相同的字段不需要相同的数据类型，这与关系型数据库有很大的区别，也是 MongoDB 非常突出的特点。

一个简单的文档例子如下：
```
{"site":"www.runoob.com", "name":"菜鸟教程"}
```
下表列出了 RDBMS 与 MongoDB 对应的术语：

|RDBMS|	MongoDB|
| ---- | ---- |s
|数据库	|数据库|
|表格	|集合|
|行	|文档|
|列|	字段|
|表联合|	嵌入文档|
|主键 |	主键(MongoDB 提供了 key 为 \_id ) |

| 数据库服务和客户端 | &nbsp; |
| ---- | ---- |
|Mysqld/Oracle	|mongod|
|mysql/sqlplus	|mongo|

需要注意的是：

1. 文档中的键/值对是有序的。
2. 文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌入的文档)。
3. MongoDB区分类型和大小写。
4. MongoDB的文档不能有重复的键。
5. 文档的键是字符串。除了少数例外情况，键可以使用任意UTF-8字符。

文档键命名规范：

1. 键不能含有\0 (空字符)。这个字符用来表示键的结尾。
2. .和$有特别的意义，只有在特定环境下才能使用。
3. 以下划线"\_"开头的键是保留的(不是严格要求的)。

## 集合
集合就是 MongoDB 文档组，类似于 RDBMS （关系数据库管理系统：Relational Database Management System)中的表格。

集合存在于数据库中，集合没有固定的结构，这意味着你在对集合可以插入不同格式和类型的数据，但通常情况下我们插入集合的数据都会有一定的关联性。

比如，我们可以将以下不同数据结构的文档插入到集合中：
```
{"site":"www.baidu.com"}
{"site":"www.google.com","name":"Google"}
{"site":"www.runoob.com","name":"菜鸟教程","num":5}
```
当第一个文档插入时，集合就会被创建。

## 合法的集合名
+ 集合名不能是空字符串""。
+ 集合名不能含有\0字符（空字符)，这个字符表示集合名的结尾。
+ 集合名不能以"system."开头，这是为系统集合保留的前缀。
+ 用户创建的集合名字不能含有保留字符。有些驱动程序的确支持在集合名里面包含，这是因为某些系统生成的集合中包含该字符。除非你要访问这种系统创建的集合，否则千万不要在名字里出现$。　

如下实例：
```
db.col.findOne()
```

## capped collections
Capped collections 就是固定大小的collection。

它有很高的性能以及队列过期的特性(过期按照插入的顺序). 有点和 "RRD" 概念类似。

Capped collections 是高性能自动的维护对象的插入顺序。它非常适合类似记录日志的功能和标准的 collection 不同，你必须要显式的创建一个capped collection，指定一个 collection 的大小，单位是字节。collection 的数据存储空间值提前分配的。

Capped collections 可以按照文档的插入顺序保存到集合中，而且这些文档在磁盘上存放位置也是按照插入顺序来保存的，所以当我们更新Capped collections 中文档的时候，更新后的文档不可以超过之前文档的大小，这样话就可以确保所有文档在磁盘上的位置一直保持不变。

由于 Capped collection 是按照文档的插入顺序而不是使用索引确定插入位置，这样的话可以提高增添数据的效率。MongoDB 的操作日志文件 oplog.rs 就是利用 Capped Collection 来实现的。

要注意的是指定的存储大小包含了数据库的头信息。
```
db.createCollection("mycoll", {capped:true, size:100000})
```
+ 在 capped collection 中，你能添加新的对象。
+ 能进行更新，然而，对象不会增加存储空间。如果增加，更新就会失败 。
+ 使用 Capped Collection 不能删除一个文档，可以使用 drop() 方法删除 collection 所有的行。
+ 删除之后，你必须显式的重新创建这个 collection。
+ 在32bit机器中，capped collection 最大存储为 1e9( 1X109)个字节。

## 元数据
数据库的信息是存储在集合中。它们使用了系统的命名空间：
```
dbname.system.*
```
在MongoDB数据库中名字空间 <dbname\>.system.* 是包含多种系统信息的特殊集合(Collection)，如下:

|集合命名|空间	描述|
| ---- | ---- |
|dbname.system.namespaces|	列出所有名字空间。|
|dbname.system.indexes	|列出所有索引。|
|dbname.system.profile	|包含数据库概要(profile)信息。|
|dbname.system.users	|列出所有可访问数据库的用户。|
|dbname.local.sources	|包含复制对端（slave）的服务器信息和状态。|

对于修改系统集合中的对象有如下限制。

在{{system.indexes}}插入数据，可以创建索引。但除此之外该表信息是不可变的(特殊的drop index命令将自动更新相关信息)。

{{system.users}}是可修改的。 {{system.profile}}是可删除的。

##　MongoDB 数据类型
下表为MongoDB中常用的几种数据类型。

|数据类型|	描述|
| ---- | ---- |
|String |	字符串。存储数据常用的数据类型。在 MongoDB 中，UTF-8 编码的字符串才是合法的。|
|Integer	|整型数值。用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位。|
|Boolean	|布尔值。用于存储布尔值（真/假）。|
|Double	|双精度浮点值。用于存储浮点值。|
|Min/Max keys|	将一个值与 BSON（二进制的 JSON）元素的最低值和最高值相对比。|
|Array	|用于将数组或列表或多个值存储为一个键。|
|Timestamp	|时间戳。记录文档修改或添加的具体时间。|
|Object	|用于内嵌文档。|
|Null	|用于创建空值。|
|Symbol	|符号。该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言。|
|Date	|日期时间。用 UNIX 时间格式来存储当前日期或时间。你可以指定自己的日期时间：创建 Date 对象，传入年月日信息。|
|Object ID|	对象 ID。用于创建文档的 ID。|
|Binary Data|	二进制数据。用于存储二进制数据。|
|Code	|代码类型。用于在文档中存储 JavaScript 代码。|
|Regular expression	|正则表达式类型。用于存储正则表达式。|

下面说明下几种重要的数据类型。

### ObjectId
ObjectId 类似唯一主键，可以很快的去生成和排序，包含 12 bytes，含义是：

+ 前 4 个字节表示创建 unix 时间戳,格林尼治时间 UTC 时间，比北京时间晚了 8 个小时
+ 接下来的 3 个字节是机器标识码
+ 紧接的两个字节由进程 id 组成 PID
+ 最后三个字节是随机数

### 字符串
BSON 字符串都是 UTF-8 编码。

### 时间戳
BSON 有一个特殊的时间戳类型用于 MongoDB 内部使用，与普通的 日期 类型不相关。 时间戳值是一个 64 位的值。其中：

+ 前32位是一个 time_t 值（与Unix新纪元相差的秒数）
+ 后32位是在某秒中操作的一个递增的序数

在单个 mongod 实例中，时间戳值通常是唯一的。

在复制集中， oplog 有一个 ts 字段。这个字段中的值使用BSON时间戳表示了操作时间。

BSON 时间戳类型主要用于 MongoDB 内部使用。在大多数情况下的应用开发中，你可以使用 BSON 日期类型。

### 日期
表示当前距离 Unix新纪元（1970年1月1日）的毫秒数。日期类型是有符号的, 负数表示 1970 年之前的日期。


# MongoDB
非关系型数据库

## 基本使用
### 服务的开启与关闭
```
// ctrl + x 之后按下a 打开以管理员身份运行的cmd窗口
// 开启 mongodb 服务
net start mongodb
// 关闭 gongodb 服务
net stop mongodb
```

### 操作
1. 查看所有数据库
```
show databases;
// 可以简写为 show dbs;
```

2. 使用数据库
```
use 数据库名;
// 如果 use 了一个不存在的库,如果后边添加了数据,那么它会被隐式创建
```

3. 查看当前数据库
```
db;
```

4. 删除数据库
```
db.dropDatabase();
// 它会删除你之前use的库,如果没有的话,默认为test
```

5. 查看当前数据库的所有集合
```
show collections;
```

6. 创建集合
```
db.createCollection("test2");
```

7. 插入数据
```
// test2为集合,如果没有的话,隐式创建
db.test2.insert({name: zs, age: 18});
// json数据中对象的键是需要用双引号包裹的,但是mongodb为我们封装了,可以不添加
```
```
db.test2.insert([
		{name: "zs", age: 18},
		{name: "ls", age: 20},
		{name: "ww", age: 21}
	])
// 插入多条数据
```
```
// 支持少部分js语法,但是执行结果只显示最后一条的结果
for(var i = 1; i <= 10; i++){
	db.c1.insert({name: "a" + 1, age: i});
}
```

8. 查看所有数据
```
db.test2.find(); 
```

9. 条件查询
```
db.c1.find({age: {$gt: 5}});
// 描述:查看所有列,并且age>=5的数据
```

	```
	db.c1.find({}, {age: 1});
	// 描述: 参数为1时, 查看age列中的所有数据,_id也默认显示
	// 		参数为2时, 除了age列其它的都显示
	```