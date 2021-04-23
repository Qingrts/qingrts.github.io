---
layout: post
title:  "MySQL基本操作"
date:   2021-04-14 08:45:50
categories: IT
tags: 数据库 MySQL
excerpt: MySQL基本操作
mathjax: true
---

* content
{:toc}


# MySQL基本操作

4. SHOW DATABASES:

	列出 MySQL 数据库管理系统的数据库列表。

5. USE 数据库名 :
	
	选择要操作的Mysql数据库，使用该命令后所有Mysql命令都只针对该数据库。

6. SHOW TABLES:

	示指定数据库的所有表，使用该命令前需要使用 use 命令来选择要操作的数据库。

7. SHOW COLUMNS FROM 数据表:

	显示数据表的属性，属性类型，主键信息 ，是否为 NULL，默认值等其他信息。

8. SHOW INDEX FROM 数据表:

	显示数据表的详细索引信息，包括PRIMARY KEY（主键）。

9. CREATE DATABASE 数据库名;
10. drop database <数据库名>;
11. DROP TABLE table_name 删除MySQL数据表的通用语法：
12. 以下为向MySQL数据表插入数据通用的 INSERT INTO SQL语法：
```sql
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
```

13. 以下为在MySQL数据库中查询数据通用的 SELECT 语法：
```sql
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][ OFFSET M]
```
+ 查询语句中你可以使用一个或者多个表，表之间使用逗号(,)分割，并使用WHERE语句来设定查询条件。
+ SELECT 命令可以读取一条或者多条记录。
+ 你可以使用星号（*）来代替其他字段，SELECT语句会返回表的所有字段数据
+ 你可以使用 WHERE 语句来包含任何条件。
+ 你可以使用 LIMIT 属性来设定返回的记录数。
+ 你可以通过OFFSET指定SELECT语句开始查询的数据偏移量。默认情况下偏移量为0。


14.  以下是 SQL SELECT 语句使用 WHERE 子句从数据表中读取数据的通用语法：
```sql
SELECT field1, field2,...fieldN FROM table_name1, table_name2...
[WHERE condition1 [AND [OR]] condition2.....
```
+ 查询语句中你可以使用一个或者多个表，表之间使用逗号, 分割，并使用WHERE语句来设定查询条件。
+ 你可以在 WHERE 子句中指定任何条件。
+ 你可以使用 AND 或者 OR 指定一个或多个条件。
+ WHERE 子句也可以运用于 SQL 的 DELETE 或者 UPDATE 命令。
+ WHERE 子句类似于程序语言中的 if 条件，根据 MySQL 表中的字段值来读取指定的数据。


15.  以下是 UPDATE 命令修改 MySQL 数据表数据的通用 SQL 语法：
```sql
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]
```
+ 你可以同时更新一个或多个字段。
+ 你可以在 WHERE 子句中指定任何条件。
+ 你可以在一个单独表中同时更新数据。

当你需要更新数据表中指定行的数据时 WHERE 子句是非常有用的。

16. 以下是 SQL DELETE 语句从 MySQL 数据表中删除数据的通用语法：
```sql
DELETE FROM table_name [WHERE Clause]
```
+ 如果没有指定 WHERE 子句，MySQL 表中的所有记录将被删除。
+ 你可以在 WHERE 子句中指定任何条件
+ 您可以在单个表中一次性删除记录。

当你想删除数据表中指定的记录时 WHERE 子句是非常有用的。

17. 以下是 SQL SELECT 语句使用 LIKE 子句从数据表中读取数据的通用语法：
```sql
SELECT field1, field2,...fieldN 
FROM table_name
WHERE field1 LIKE condition1 [AND [OR]] filed2 = 'somevalue'
```

+ 你可以在 WHERE 子句中指定任何条件。
+ 你可以在 WHERE 子句中使用LIKE子句。
+ 你可以使用LIKE子句代替等号 =。
+ LIKE 通常与 % 一同使用，类似于一个元字符的搜索。
+ 你可以使用 AND 或者 OR 指定一个或多个条件。
+ 你可以在 DELETE 或 UPDATE 命令中使用 WHERE...LIKE 子句来指定条件。


18. 以下是 SQL SELECT 语句使用 ORDER BY 子句将查询数据排序后再返回数据：
```sql
SELECT field1, field2,...fieldN FROM table_name1, table_name2...
ORDER BY field1 [ASC [DESC][默认 ASC]], [field2...] [ASC [DESC][默认 ASC]]
```

+ 你可以使用任何字段来作为排序的条件，从而返回排序后的查询结果。
+ 你可以设定多个字段来排序。
+ 你可以使用 ASC 或 DESC 关键字来设置查询结果是按升序或降序排列。 默认情况下，它是按升序排列。
+ 你可以添加 WHERE...LIKE 子句来设置条件。

19. insert
  
|指令|已存在|不存在|举|
|---|---|---|---|
|insert|	报错| 	插入| 	insert into names(name, age) values(“小明”, 23);| 
|insert ignore| 	忽略| 	插入| 	insert ignore into names(name, age) values(“小明”, 24);| 
|replace|	替换| 	插入| 	replace into names(name, age) values(“小明”, 25);| 
