---
layout: post
title: "使用 MySQL"
data: 2021-08-12 14:32:49 +0800
categories: mysql
---

# [MySQL](https://dev.mysql.com/doc/refman/8.0/en/entering-queries.html) 常用命令

## 1. 连接和断开服务器
***

### 1.1 连接服务器

```
shell> mysql -h host -u user -p
Enter password: ********
```

如果你在运行mysql 的同一台主机上，可以省略 `host`

```
shell> mysql -u user -p
```

### 1.2 断开连接

```
mysql> QUIT 或者 \q
Bye
```

### 1.3 查询 版本号 和 当前日期（关键字可以以任何字母大小写输入，以下查询是等效的）

```
mysql> select version(),current_date;
+-----------+--------------+
| version() | current_date |
+-----------+--------------+
| 8.0.26    | 2021-08-09   |
+-----------+--------------+
1 row in set (0.01 sec)

```

```
mysql> SELECT VERSION(), CURRENT_DATE;
mysql> select version(), current_date;
mysql> SeLeCt vErSiOn(), current_DATE;
```



### 1.4 将 [**mysql**](https://dev.mysql.com/doc/refman/8.0/en/mysql.html)用作一个简单的计算器

```
mysql> SELECT SIN(PI()/4), (4+1)*5;
+------------------+---------+
| SIN(PI()/4)      | (4+1)*5 |
+------------------+---------+
| 0.70710678118655 |      25 |
+------------------+---------+
1 row in set (0.02 sec)
```

### 1.5 可以在一行中输入多个语句。只需用分号结束每一项，例如：

```
mysql> select version(); select now();
+-----------+
| version() |
+-----------+
| 8.0.26    |
+-----------+
1 row in set (0.00 sec)

+---------------------+
| now()               |
+---------------------+
| 2021-08-09 18:33:26 |
+---------------------+
1 row in set (0.00 sec)
```

### 1.6  多行语句查询；例如:

```
mysql> select
    -> user()
    -> ,
    -> current_date();
+----------------+----------------+
| user()         | current_date() |
+----------------+----------------+
| root@localhost | 2021-08-09     |
+----------------+----------------+
1 row in set (0.01 sec)
```

### 1.7  如果你决定不想执行正在输入的查询，输入`\c` 取消它 

```
mysql> select
    -> user()
    -> \c
```

## 2.创建和使用数据库

### 2.1 使用[`SHOW`](https://dev.mysql.com/doc/refman/8.0/en/show.html) 语句找出服务器上当前存在哪些数据库：

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sakila             |
| sys                |
| world              |
+--------------------+
```

### 2.2  访问数据库 `use`

```
mysql> use world
Database changed
```

### 2.3  创建数据库menagerie

```
mysql> CREATE DATABASE menagerie;

mysql> create database menagerie;
Query OK, 1 row affected (0.03 sec)
```

### 2.4 使用`menagerie`数据库

```
mysql> USE menagerie
Database changed
```

或者

```
shell> mysql -h host -u user -p menagerie
Enter password: ********
```

## 3 创建表

### 3.1 创建数据库是简单的部分，但此时它是空的，[`SHOW TABLES`](https://dev.mysql.com/doc/refman/8.0/en/show-tables.html)：

```
mysql> show tables;
Empty set (0.00 sec)
```

创建表一个宠物表 `pet`

```
mysql> CREATE TABLE pet (name VARCHAR(20), owner VARCHAR(20),
       species VARCHAR(20), sex CHAR(1), birth DATE, death DATE);
```

show tables;

```
mysql> show tables;
+---------------------+
| Tables_in_menagerie |
+---------------------+
| pet                 |
+---------------------+
1 row in set (0.00 sec)
```

[`DESCRIBE`](https://dev.mysql.com/doc/refman/8.0/en/describe.html) pet; 显示`pet`表的内容

```
mysql> DESCRIBE pet;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| name    | varchar(20) | YES  |     | NULL    |       |
| owner   | varchar(20) | YES  |     | NULL    |       |
| species | varchar(20) | YES  |     | NULL    |       |
| sex     | char(1)     | YES  |     | NULL    |       |
| birth   | date        | YES  |     | NULL    |       |
| death   | date        | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
6 rows in set (0.02 sec)
```

使用INSERT向`pet`表中添加新数据

```SHI
mysql> INSERT INTO pet
       VALUES ('Puffball','Diane','hamster','f','1999-03-30',NULL);
```

## 4 从表中检索信息

### 4.1 使用 [`SELECT`](https://dev.mysql.com/doc/refman/8.0/en/select.html) 从表 中检索所有内容

```
mysql> select * from pet;
+------+-------+---------+------+------------+-------+
| name | owner | species | sex  | birth      | death |
+------+-------+---------+------+------------+-------+
| 小明 | kk    | 猫科    | F    | 2021-08-09 | NULL  |
+------+-------+---------+------+------------+-------+
1 row in set (0.01 sec)
```

### 4.2 使用[`UPDATE`](https://dev.mysql.com/doc/refman/8.0/en/update.html)语句修复错误记录

```
mysql> UPDATE pet SET birth = '2021-08-11' WHERE name = '小明';
Query OK, 0 rows affected (0.00 sec)
Rows matched: 1  Changed: 0  Warnings: 0
```

```
mysql> SELECT * from pet;
+------+-------+---------+------+------------+-------+
| name | owner | species | sex  | birth      | death |
+------+-------+---------+------+------------+-------+
| 小明 | kk    | 猫科    | F    | 2021-08-11 | NULL  |
+------+-------+---------+------+------------+-------+
1 row in set (0.00 sec)
```

### 4.3 清空表中数据 `DELETE`

```
mysql> DELETE FROM pet;
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * from pet;
Empty set (0.00 sec)

mysql> DESCRIBE pet;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| name    | varchar(20) | YES  |     | NULL    |       |
| owner   | varchar(20) | YES  |     | NULL    |       |
| species | varchar(20) | YES  |     | NULL    |       |
| sex     | char(1)     | YES  |     | NULL    |       |
| birth   | date        | YES  |     | NULL    |       |
| death   | date        | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
6 rows in set (0.00 sec)
```

### 4.4 [选中特定行](https://dev.mysql.com/doc/refman/8.0/en/selecting-rows.html) 待续...
