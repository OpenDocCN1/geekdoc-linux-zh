

# 表 24-9：（续）

| 命令 | 描述 |
|---|---|
| \o | 将所有查询输出发送到指定文件 |
| \qecho | 在查询输出流中显示指定字符串 |
| \d | 显示指定表、索引、序列或视图的信息 |
| \dt | 显示数据库中的表 |
| \di | 显示数据库中的索引 |
| \ds | 显示数据库中的序列 |
| \dv | 显示数据库中的视图 |
| \da | 显示数据库中的聚合函数 |
| \db | 显示数据库中的表空间 |
| \dc | 显示数据库中的字符集转换 |
| \dC | 显示数据库中的转换 |
| \dD | 显示数据库中的域 |
| \df | 显示数据库中的函数 |
| \dF | 显示数据库中的文本搜索配置 |
| \dg | 显示数据库中的组 |
| \dn | 显示数据库中的模式 |
| \do | 显示数据库中的操作符 |
| \d1 | 显示数据库中的大对象 |
| \dp | 显示数据库中的访问权限 |
| \dT | 显示数据库中的数据类型 |
| \du | 显示所有用户 |
| \l | 显示所有数据库 |
| \z | 显示指定表、视图或序列的访问权限 |
| \a | 在对齐和不对齐输出之间切换 |
| \C | 设置表标题 |
| \f | 显示或设置不对齐输出的字段分隔符 |
| \H | 切换 HTML 输出模式（默认关闭） |
| \pset | 设置表输出选项 |
| \t | 在输出中仅显示数据行 |

# 表 24-9：（续）

| 命令 | 描述 |
|---|---|
| \T | 设置 HTML 表格标签属性 |
| \x | 切换扩展输出（默认关闭） |
| \copy | 执行 SQL COPY 命令 |
| \lo_ | 用于导出、导入、列出和取消链接 PostgreSQL 大对象数据类型的命令 |

您可以从命令提示符输入任何 psql 命令，如图 24-2 所示。该图演示了使用 \l 命令列出当前数据库中可用的数据库，然后使用 CREATE DATABASE 语句创建一个新数据库。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_628_0.png)

# 图 24-2：使用 psql 命令进行 PostgreSQL 服务器。

# 使用数据库

现在您已经安装了 MySQL 和/或 PostgreSQL，您将希望开始使用它们来满足您的数据管理需求。本节介绍在 MySQL 和 PostgreSQL 环境中创建数据库、用户和表以管理您的数据的基础知识。

# 创建数据库

数据库是您数据管理的核心。MySQL 和 PostgreSQL 都基于数据库控制数据。您可以在两个服务器上使用 SQL CREATE DATABASE 语句创建新数据库：

```
$ mysql -u root -p
Enter password:
```

```
mysql> create database test;
Query OK, 1 row affected (0.01 sec)

mysql> use test;
Database changed
mysql>
```

新数据库在服务器上创建。在 MySQL 和 PostgreSQL 中，您一次只能连接到一个数据库。您可以在命令行上指定默认数据库，也可以在提示符下使用 connect 命令指定：

```
$ sudo -u postgres psql test
test=# test;
You are now connected to database "test."
test=#
```

```
$mysql test -u root -p
Enter password:
mysql>connect test;
Connection id: 32
Current database: test
mysql>
```

MySQL 服务器还允许您使用 SQL USE 语句切换到另一个数据库。

> PostgreSQL 服务器还支持一种称为模式的功能。每个数据库都有一个默认模式，称为 public，您可以在其中存储表。然而，您也可以创建额外的模式来控制数据库级别内的数据布局和访问。

# 管理用户

创建数据库后，您可能希望创建一个或多个可以访问数据库的用户帐户。不幸的是，创建用户帐户是 MySQL 和 PostgreSQL 不同的地方之一。本节演示如何在两个服务器环境中创建用户帐户。

# 在 MySQL 中创建用户帐户

在 MySQL 中，您可以使用两种方法之一创建用户帐户。MySQL 在 mysql 数据库中包含的特殊 user 表中维护用户帐户。您可以通过执行 SELECT 语句查询该表来查看现有用户帐户：

```
mysql> select user,host from user;
+---------------+
| user | host |
```

