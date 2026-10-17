
Threads:             2

Queries:            184

Slow queries:       0

Opens:               11

Flush threads:      1

Open tables:        0

Queries per second avg:0.004

Server version:     5.0.22 MySQL C

Type `'\help'` or `'\h'` for help. Type `'\q'` to quit. Commands end with `;` or `\g`

```
`status` 输出告诉你关于 MySQL 服务器的版本 (14.1) 以及发行版本 (5.0.22)。它告诉你当前数据库 (`mysql`) 和你的用户 (`root@localhost`)。你可以看到服务器已运行多久 (`Uptime`)。你可以看到有多少活动线程以及运行了多少命令 (`184`)。
```

# 第四部分：Fedora 和 RHEL 的网络与服务器设置

## 使用 mysql 创建数据库

在交互式 `mysql` 会话中，你可以创建和修改数据库。如果你尚未连接到会话，输入以下（假设 `mysql` 用户为 `root`）：

```
$ mysql -u root -p
password: ********
mysql>
```

创建 MySQL 数据库的通用步骤包括创建数据库名称、将新数据库设置为当前数据库、创建表以及向表中添加数据。当你连接到会话时，可以运行以下过程创建一个示例数据库。

1. 在 `mysql` 提示符处使用 `CREATE DATABASE` 命令创建数据库名称。例如，要创建一个名为 `allusers` 的数据库，输入：
`mysql> CREATE DATABASE allusers;`

此操作会在 `/var/lib/mysql` 目录下创建一个名为 `allusers` 的数据库。（虽然命令不需要使用大写，但这样有助于区分命令和数据库条目。）

> 注意：或者，你可以使用 `mysqladmin` 命令从命令行创建数据库。例如，使用 `mysqladmin` 创建名为 `allusers` 的数据库，你可以输入：
`mysqladmin -u root create allusers`

2. 要查看 MySQL 服务器上有哪些可用数据库，在 `mysql` 提示符处输入以下内容：
`mysql> SHOW DATABASES;`

| Database |
|------|
| information_schema |
| allusers |
| mysql |
| test |
| 4 rows in set (0.00 sec) |

这里显示的数据库名为 `information_schema`、`allusers`、`mysql` 和 `test`。`information_schema` 数据库包含了有关服务器上其他数据库信息的元数据（例如每个数据库使用的数据类型、列或表）。`allusers` 数据库是你上一步创建的数据库。`mysql` 数据库包含用户访问数据。`test` 数据库是自动创建的，用于测试 MySQL 数据库。

3. 要操作刚刚创建的数据库 (`allusers`)，你需要将 `allusers` 设置为当前数据库。为了这样做，在 `mysql>` 命令提示符处输入：
`mysql> USE allusers;`
`Database changed`

# 第 24 章：设置 MySQL 数据库服务器

## 创建数据库表

创建数据库表需要一些规划以及对表语法的理解。你可以输入以下命令和列信息来尝试创建表。有关创建表和使用不同数据类型的更多详细信息，请参阅本章稍后部分的“理解 MySQL 表”章节。

要创建一个名为 `names` 的表，请在 `mysql>` 提示符下使用 `CREATE TABLE` 命令：

```
mysql> CREATE TABLE names (
  -> firstname varchar(20) not null,
  -> lastname varchar(20) not null,
  -> streetaddr varchar(30) not null,
  -> city varchar(20) not null,
  -> state varchar(20) not null,
  -> zipcode varchar(10) not null
);
Query OK, 0 rows affected (0.00 sec)
```

你现在已经为 `users` 数据库创建名为 `names` 的表。它包含 `firstname`、`lastname`、`streetaddr`、`city`、`state` 和 `zipcode` 等列。每列记录的长度在 10 到 30 个字符之间。虽然 MySQL 支持多种数据库格式，但由于此处没有指定，因此使用了默认的 MyISAM 数据库类型。

在创建数据库和一个表后，你现在可以向表中添加数据了。

### 向 MySQL 数据库表添加数据

在创建数据库且数据库表结构准备完成后，你就可以开始操作数据库了。你可以通过在 `mysql` 会话期间手动输入每条记录，或将数据添加到纯文本文件中加载到数据库来向 MySQL 数据库添加数据。

> 注意：当你处于 `mysql` 会话时，请记住使用向上方向键来检索和更改之前的命令。这在你手动输入包含相似信息的数据库记录时特别有用。

#### 手动输入数据

为了执行本节中的操作，我假设你已经有一个交互式的 `mysql` 会话，并且按照上一节所述创建了数据库和表。如果你还没有连接到 `mysql` 会话，请输入以下命令（假设 mysql 用户名为 `root`）：

```
mysql -u root -p
password: ********
mysql>
```

要向现有 MySQL 数据库添加数据，以下步骤描述了如何查看可用表并将数据手动加载到这些表中。下一节将描述如何创建一个包含数据库数据的纯文本文件，以及如何将其加载到你的数据库中。

1. 要让你想要使用的数据库成为当前数据库（在本例中为 `allusers`），请在 `mysql>` 提示符下输入以下命令：

```
mysql> USE allusers;
Database changed
```

2. 查看与当前数据库关联的表，请在 `mysql>` 提示符下输入以下命令：

```
mysql> SHOW tables;
+--------------------+
| Tables_in_allusers |
+--------------------+
| names              |
+--------------------+
1 row in set (0.00 sec)
```

你可以看到，为止为 `allusers` 数据库定义的表只有一个名为 `names` 的表。

3. 显示 `names` 表的格式，请在 `mysql>` 提示符下输入以下命令：

```
mysql> DESCRIBE names;
+----------------+------+------+------+------+
| Field     | Type         | Key  | Default | Extra  |
+----------------+------+------+------+------+
| firstname | varchar(20) | NO   |         |        |
| lastname  | varchar(20) | NO   |         |        |
| streetaddr| varchar(30) | NO   |         |        |
| city      | varchar(20) | NO   |         |        |
| state     | varchar(20) | NO   |         |        |
| zipcode   | varchar(10) | NO   |         |        |
+----------------+------+------+------+------+
```

4. 要向新表添加数据，请在 `mysql>` 提示符下使用 `INSERT INTO` 命令。这里有一个向新表添加人的姓名和地址的示例：

```
mysql> INSERT INTO names
-> VALUES ('Jerry', 'Wingnut', '167 E Street', 'Roy', 'UT', '84103');
```

在此示例中，`INSERT INTO` 识别了 `names` 表。然后它指示该表中一条记录的值包括地址为 `167 E Street, Roy, UT` 的姓名 `Jerry Wingnut`。

5. 要检查数据是否已输入，请输入以下内容：
