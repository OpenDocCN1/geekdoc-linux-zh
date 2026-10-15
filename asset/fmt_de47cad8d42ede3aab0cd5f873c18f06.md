
对于每个应用程序，你都需要权衡 ZODB 还是外部数据库是正确的选择。如果你发现应用程序中需要使用外部数据库系统，你的第一个任务将是学习如何将其连接到 Zope。

## 12.2 RDBMS

关系型数据库是存储和检索大量表格化数据的行业标准。这些系统由服务器程序组成，这些数据库后端（或引擎）响应来自客户端程序（包括 Zope）的命令。这些命令使用 SQL 语言给出，这是一种被接受的标准数据库查询语言。

关系型数据库管理系统（RDBMS）本质上有两种类型：商业和开源。以下是每种类型最重要的示例：

### 商业 RDBMS

| | | |
| :--- | :--- | :--- |
| Oracle | `http://www.oracle.com` | 一种广泛使用的、健壮的商业数据库。 |
| Sybase | `http://www.sybase.com` | 一个成功的商业数据库平台。 |

### 开源 RDBMS

| | | |
| :--- | :--- | :--- |
| MySQL | `http://www.mysql.com` | 一种快速且日益复杂的开源数据库引擎。由于其查询性能，常用于 Web 应用。 |
| PostgreSQL | `http://www.postgresql.org` | 可能是最复杂的开源数据库系统。针对复杂的多用户应用程序定制。比 MySQL 更适合写密集型应用程序。 |
| Interbase | `http://www.interbase.com` | 来自 Borland 的一个健壮的开源数据库。像 MySQL 和 PostgreSQL 一样被广泛使用，人气正在增长。 |
| ODBC | `http://www.odbc.com` | 本身不是数据库，但是一种允许你连接到任何数据库的标准接口（如 SQL Server 甚至 Access）。 |

本章将尝试让你成为 SQL 专家。事实上，如果你是 Web 程序员，我们将关注如何将数据库连接到 Zope，以 MySQL 为例。

## 12.3 MySQL 数据库

在尝试在 Zope 中使用 MySQL 之前，确保你的计算机上运行了 MySQL 服务器（版本 3.22 或更高。（请参考 MySQL 随附的文档安装并运行服务器）。一旦运行，你就可以登录服务器并创建数据库。

### 12.3.1 启动监控器

MySQL 监控器是一个命令行程序，允许你访问和管理数据库。（Windows 用户使用 DOS 提示符），使用以下命令运行：

```
mysql -h host -u -p
Enter password: ********
```

如果 MySQL 服务器运行在不同的计算机上，你需要输入 `host` 参数。对于 `user` 参数，输入你在 MySQL 服务器上的用户名。登录后，会出现以下文本：

```
Welcome to the MySQL monitor.
Your connection id is 459 to server version: 3.22

Type 'help' for help.

mysql>
```

现在出现了 mysql 提示符（`mysql>`），你可以输入 SQL 语句。输入命令

```
mysql> help
```

将调用可用选项列表。退出 MySQL 服务器，输入命令

```
mysql> quit
```

### 12.3.2 使用 Monitor 创建数据库

首先，你创建一个名为 `mydb` 的数据库，并在其中存储用户数据，步骤如下：

1. 如上所述运行 MySQL Monitor。
2. 使用以下命令创建一个名为 `mydb` 的新数据库：

```
mysql> CREATE DATABASE mydb;
```

3. 通过输入选择该数据库（每次启动新的 MySQL 会话时都需要这样做）：

```
mysql> USE mydb;
```

在响应中，你应该看到

```
Database changed
```

你现在已经创建并选择了数据库。在向其中添加数据之前，你需要在数据库中创建适当的表来存放数据。通过指定表名和有关表字段的信息（包括字段名、数据类型和其他数据规则）来定义表。每个字段定义表的一个列。表中的数据作为记录存储；每条记录是表的一行，为每个字段指定了特定值。

在提示符处输入 `SHOW Databases;` 来显示所有可用数据库。

### 12.3.3 使用 MySQL Monitor 创建数据表

你可以使用 MySQL Monitor 或使用 Zope 在数据库中创建数据表。由于你尚未将 Zope 与 MySQL 连接，请使用 MySQL Monitor 来创建表。（第 12.3.5 节“从 Zope 建立 MySQL 连接”讨论了如何在没有 MySQL Monitor 的情况下从 Zope 在 MySQL 数据库中创建表。）

用户数据将存储在名为 `user` 的表中，该表应包含字段：

| | |
| :--- | :--- |
| `userid` | `zipcode` |
| `firstname` | `city` |
| `lastname` | `telephone` |
| `address` | |

要创建 `user` 表，输入以下 SQL 语句：

```sql
CREATE TABLE user (
  userid INT(12) NOT NULL,
  firstname CHAR(20) NOT NULL,
  lastname CHAR(20) NOT NULL,
  address CHAR(20) NOT NULL,
  zipcode INT(5) NOT NULL,
  telephone CHAR(15) NOT NULL,
  PRIMARY KEY(userid)
);
```

上面的 SQL 代码使用 `CREATE TABLE` SQL 语句创建了 `user` 表。第 2-8 行指定了表中的字段。每行的第一列是字段名，第二列是数据类型，最后一列描述了对表的任何约束。最后一行指定字段 `userid` 是记录的主键——即记录的唯一标识符。任何两个用户记录不能具有相同的主键值。

现在输入命令

```bash
mysql show tables;
```

以查看 `user` 表是否已正确创建。如果是，你应该看到以下内容：

| Tables in myDB |
| :--- |
| user |

1 row in set (0.00 sec)

### 表 12-1: 数据库适配器所需文件

| 文件 | 描述 |
| :--- | :--- |
| `ZMySQLDA-2.0.6.tar.gz`（或更高版本）。（从 `http://www.zope.org/Members/oduston/Products/ZMySQLDA` 下载） | 数据库适配器。 |
| `MySQL-python-0.3.5.tar.gz`（或更高版本）。（从 `http://www.zope.org/Members/oduston/Products/MySQLdb` 下载） | MySQL 数据库模块，包含比数据库适配器提供的更新的驱动程序。 |

### 12.3.4 安装数据库适配器 ZMySQLDA

在 Zope 能与 `myDB` 数据库通信之前，你必须使用数据库适配器连接到 MySQL 服务器，适配器是 `myDB` 和 Zope 之间的接口。我们将安装数据库适配器 `ZMySQLDA`。

在开始安装之前，下载表 12-1 中列出的文件，包括 `ZMySQLDA` 适配器本身以及最新的 MySQL 驱动程序。

在 Linux 下安装 `ZMySQLDA`，请执行以下操作：

1. 在 Zope 安装的根目录下解压 `ZMySQLDA` 压缩包。例如，如果你将 Zope 安装在 `Zope-2.3` 目录，请将压缩包提取到该目录。解压压缩包会创建一个名为 `Zope-Directory/lib/python/Products/ZMySQLDA` 的文件夹。
2. 在 `Zope-Directory/lib/python/Products` 目录下解压 MySQL 驱动程序。操作时请遵循随产品附带的安装说明。
3. 重启 Zope 以使更改生效。

### 12.3.5 在 Zope 中建立 Z MySQL 连接

> 在文件夹中创建数据库连接对象，以便你可能创建的任何 Z SQL 方法都能获取它。根文件夹通常是一个很好的选择。

#### 12.3.5.1 数据库连接字符串

在 `Database Connection`（数据库连接）字段中，使用以下语法输入你的数据库信息：

```sql
<DatabaseName>[@Host> <Username> <Password>
```
