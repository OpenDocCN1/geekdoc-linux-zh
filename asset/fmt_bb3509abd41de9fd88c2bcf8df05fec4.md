
`-t tables` 选项仅导出表的数据，而不包含创建表的结构信息。

`-d` 选项仅导出表结构，而不包含实际数据。

默认情况下，`mysqldump` 将数据发送到标准输出，因此你可能需要将其重定向到文件。

该工具对于数据迁移或快速备份非常方便，得益于 `MySQL` 的客户端/服务器实现，它可以用于非常出色的远程备份实现：

```
$ mysqldump -u rick -p rick > rick.dump
```

生成的文件（在我们系统中，`rick` 数据库中只有一个表）看起来如下：

```sql
-- MySQL dump 8.22
-- Host: localhost Database: rick
-- Table structure for table 'children'

CREATE TABLE children (
  childno int(11) DEFAULT '0' NOT NULL auto_increment,
  fname varchar(30),
  age int(11),
  PRIMARY KEY (childno)
);

-- Dumping data for table 'children'
INSERT INTO children VALUES (1,'Jenny',17);
INSERT INTO children VALUES (2,'Andrew',13);
INSERT INTO children VALUES (3,'Gavin',4);
INSERT INTO children VALUES (4,'Duncan',2);
INSERT INTO children VALUES (5,'Emma',0);
INSERT INTO children VALUES (6,'Alex',11);
INSERT INTO children VALUES (7,'Adrian',5);
```

### mysqldump

`mysqldump` 命令是 `mysql` 同样实用的“兄弟”。使用 `mysql`，你可以从输入文件中读取大量数据。所需的特定命令参数是文件名和数据库。通常情况下，你将读取一个由 `mysqldump` 创建的文件，但也可以手动创建一个可以被 `mysql` 读取的文件。

正如我们之前提到的，也可以通过简单运行带有文件输入重定向的 `mysql` 来从文本文件执行 `SQL` 命令。

### mysqlshow

该工具可以提供有关你的 `MySQL` 安装及其组件数据库的快速信息。

- 不带任何参数时

## 创建用户并赋予权限

作为 `MySQL` 管理员，你最常见的任务之一将用户维护。在你对对用户使用“扳手”之前（尽管在最好的日子这也是个诱人的想法），我们指的是在 `MySQL` 中添加和删除用户并管理它们的权限。从 `MySQL` 3.22 开始，用户通过 `MySQL` 监控器内的 `grant` 和 `revoke` 命令进行管理——这项任务比以前版本需要直接编辑权限表要简单得多。

### grant

`MySQL` `grant` 命令密切遵循 `SQL92`，但并不完全相同。其通用格式为：

```sql
grant <privilege> on <object> to <user> [identified by user-password] [with grant];
```

有几个可以授予的权限值，如下表所示：

| 权限 | 描述 |
| :--- | :--- |
| `alter` | 修改表。 |
| `create` | 创建数据库。 |
| `drop` | 删除数据库。 |
| `insert` | 添加数据。 |
| `select` | 查询数据。 |
| `update` | 修改数据。 |

假设你想为用户 `foo` 分配密码 `bar`；你可以这样操作：

```
mysql> UPDATE user SET password = password('bar') WHERE user = 'foo';
```

再次显示 `user` 表中的相关列：

```
mysql> SELECT host, user, password FROM user;
+-----------------------------------------------------------+
| host      | user    | password                                |
+-----------------------------------------------------------+
| localhost | root    | 65457e236glalwbq                         |
| localhost | foo     | 7c9e0a4122752fa                          |
+-----------------------------------------------------------+
2 rows in (0.00 sec)
mysql>
```

现在，用户 `foo` 已经有了密码。

在 `MySQL` 4.1 中，密码方案已经更新。然而，你仍然可以使用旧算法设置密码，以保持与 `OLD_PASSWORD('password to set')` 函数向后兼容。这种实现仍然有些粗糙，但随着更新版本的发布，它将变得更加可靠。

## 创建数据库

让我们从名为 `rick` 的数据库开始。你可能记得我们已经创建了一个同名的用户。

```
mysql> GRANT ALL *.* TO rick@localhost IDENTIFIED BY 'secretpassword';
```

通过登录用户 `rick` 并创建数据库来测试该权限设置：

```
mysql> quit
Bye
$ mysql -u rick -p
Enter password:
...
mysql> CREATE DATABASE rick;
```

现在我们告诉 `MySQL` 我们想使用这个新数据库：

```
mysql> use rick
```

现在我们可以向此数据库中填充我们需要的表和信息。在将来的登录中，我们可以在命令行中指定数据库，从而跳过对 `use` 命令的需求：

```
$ mysql -u rick -p rick
```

然后我们将自动切换到使用 `rick` 数据库。

# 第8章

## 数据类型

现在我们有了一个运行中的 `MySQL` 服务器、一个为用户提供的安全登录以及一个准备好使用的数据库。接下来是什么？嗯，现在我们需要创建一些带有列的表来存储我们的数据。在此之前，我们需要了解 `MySQL` 支持的数据类型。

`MySQL` 数据类型非常标准，因此我们在这里简要介绍一下主要类型。一如既往，`MySQL` 网站上的 `MySQL` 手册对此有更详细的讨论。

### 布尔 (Boolean)

布尔列可以使用关键字 `BOOL` 定义。如你所预期的，它可以持有 `TRUE` 和 `FALSE` 值。它还可能持有特殊的数据库“未知”值 `NULL`。

### 字符 (Character)

有多种字符类型，如下表所示。前三个是标准类型，后三个是 `MySQL` 特有的。我们建议在可行的情况下坚持使用标准类型。

| 定义 | 意义 |
| :--- | :--- |
| `CHAR` | 单字符。 |
| `CHAR (N)` | 恰好为 `N` 个字符的字符字符串，必要时将用空格字符填充。限制为 255 个字符。 |
| `VARCHAR (N)` | 长度为 `N` 的字符数组。限制为 255 个字符。 |
| `TINYTEXT` | 类似于 `VARCHAR (N)` |
| `MEDIUMTEXT` | 最多 65,535 个字符的文本字符串。 |
| `LONGTEXT` | 最多 $2^{31}-1$ 个字符的文本字符串。 |

### 数字 (Number)

数字类型分为整数类型和浮点数类型，如下表所示：

| 定义 | 类型 | 意义 |
| :--- | :--- | :--- |
| `TININT` | 整数 | 8 位数据类型。 |
| `SMALLINT` | 整数 | 16 位数据类型。 |
| `MEDIUMINT` | 整数 | 24 位数据类型。 |
| `INT` | 整数 | 32 位数据类型。这是一个标准类型，也是很好的通用选择。 |
| `BIGINT` | 整数 | 64 位带符号数据类型。 |
| `FLOAT (P)` | 浮点 | 至少有 `P` 位精度的浮点数。 |

### MySQL 类型

| 定义 | 类型 | 意义 |
| :--- | :--- | :--- |
| `DOUBLE (D, N)` | 浮点 | 带有符号的双倍精度浮点数，有 `D` 位数字和 `N` 位小数。 |
| `NUMERIC (P, S)` | 浮点 | 总共 `P` 位数字的实数，`S` 为小数点后的位数。与 `DOUBLE` 不同，这是一个精确数字，因此更适合存储货币，但处理效率较低。 |
| `DECIMAL (P, S)` | 浮点 | `NUMERIC` 的同义词。 |

通常，我们建议你坚持使用 `INT`、`DOUBLE` 和 `NUMERIC` 类型，因为这些最接近标准 `SQL` 类型。其他类型是非标准的，如果你将来需要迁移数据，它们在其他数据库系统中可能不可用。

### 时间类型 (Temporal)

有四种时间数据类型，如下表所示：

| 定义 | 意义 |
| :--- | :--- |
| `DATE` | 存储 1000 年 1 月 1 日到 9999 年 12 月 31 日之间的日期。 |
| `TIME` | 存储 -838:59:59 到 838:59:59 之间的时间。 |
| `TIMESTAMP` | 存储 1970 年 1 月 1 日到 2037 年之间的时间戳。 |
| `DATETIME` | 存储 1000 年 1 月 1 日到 9999 年 12 月 31 日最后一秒之间的日期。 |

# 创建表

现在我们有一个运行中的 `MySQL` 服务器、一个为用户提供的安全登录以及一个准备好使用的数据库。接下来是什么？嗯，现在我们需要创建一些带有列的表来存储我们的数据。在此之前，我们需要了解 `MySQL` 支持的数据类型。

（注：OCR 文本从 360 页起存在大量的重复/乱码，我已经清理了冗余内容并遵循了文档的逻辑流。）

# 第 8 章

## 图形化工具

在命令行操作表格和数据固然不错，但现在许多人更倾向于使用图形化工具。

`MySQL` 一直以来有一个名为 `MySQLGUI` 的图形化工具。该工具仍然可以从 `MySQL` 网站获取，但现在的开发重心已转向另一个工具——`MySQL` 控制中心（`MySQL Control Center`），简称 `MySQLCC`。`MySQL Control Center` 是一个非常实用的方位工具，值得安装。

我们强烈建议你查看一下 `MySQLCC`；它是一个针对 `MySQL` 的强大、稳定且易于使用的图形化界面，提供了适用于 `Linux` 和 `Windows` 的预编译版本（如果你需要，甚至可以获取源代码）。它允许你既通过 GUI 界面管理 `MySQL` 服务器并执行 `SQL` 语句。

如果你的 `Linux` 发行版中没有提供 `MySQLCC`，你可以从 `MySQL` 网站下载一个副本并按照简单的安装说明进行操作。或者，你也可以从运行在 `Windows` 桌面上的 `MySQLCC` 直接管理运行在你的 `Linux` 服务器上的 `MySQL` 副本。它的外观和运行方式几乎完全相同。

第一次运行 `MySQLCC` 时，你将看到一个空白的控制中心窗口，其中控制台管理器也是空的，如图 8-2 所示。将鼠标悬停在工具栏上的第一个图标上，会显示这是创建新连接的图标。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_363_0.png)

图 8-2

当你点击此按钮时，会在额外的弹出窗口中要求你输入一些基本信息（见图 8-3）。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_364_0.png)

图 8-3

如果你想从 `Windows` PC 远程管理服务器，那么配置过程几乎相同，仅需要在“主机名”（Host Name）字段中输入主机名或 `IP` 地址，如图 8-4 所示。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_364_1.png)

图 8-4

你需要提供的所有信息包括识别连接的名称（你可以选择任何名称）、主机名、用户名和密码。所有其他值都由系统默认填充。然后点击“测试”（Test）按钮，它将告诉你哪个连接是正常的。

然后点击“添加”（Add）将此连接添加到列表中。名称 `gw1`（或你选择的任何名称——`gw1` 恰好是它运行的机器的名称）应该显示在 `MySQL` 服务器列表中，通过点击它，你应该能够展开更多信息，如图 8-5 所示。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_365_0.png)

图 8-5

如果你探索数据库部分，你可以看到表格，通过右键点击表格，可以编辑表格定义或表中的数据，如图 8-6 所示。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_366_0.png)

图 8-6

你还可以编辑用户及其权限、执行 `SQL`、查看与数据库的连接，以及进行许多其他操作。

## 从 C 访问 MySQL 数据

现在我们已经掌握了 `MySQL` 的基础知识，让我们探索如何从自己的应用程序访问它，而不是使用 `mysql` 或基础的 `mysql` 客户端。

`MySQL` 可以通过许多不同的语言访问。我们知道有：

- C
- C++
- Java
- Perl
- Python
- REXX
- Tcl
- PHP

ODBC 驱动也可用于从 `Access` 等 `Windows` 原生应用程序访问 `MySQL`；甚至还有适用于 `Linux` 的 ODBC 驱动，尽管使用它的人寥寥无几。

在本章中，我们将限于 C 接口，因为它是本书的重点，而且相同的库方便了许多其他语言的连接。

### 连接程序

从 C 连接到 `MySQL` 数据库涉及的两个步骤：

- 初始化连接句柄
- 物理上建立连接

首先，我们将使用 `mysql_init` 来初始化我们的连接句柄：

```c
*mysql_init (MYSQL *);
```

通常你向该程序传递 `NULL`，返回一个指向新分配连接句柄的指针。如果你传递一个现有结构，它将被重新初始化。如果出错，则返回 `NULL`。到目前，我们只是简单地分配并初始化了一个结构。我们仍然需要为 `mysql_real_connect` 提供连接参数：
