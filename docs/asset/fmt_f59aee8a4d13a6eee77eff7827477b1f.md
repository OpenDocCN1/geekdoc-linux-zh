
其中 `table` 是你的表名。请参阅 [MySQL 参考手册](http://dev.mysql.com/doc/refman/5.0/en/upgrade.html) 获取更多关于升级到 MySQL 5.0 的信息。

## 第 24 章：设置 MySQL 数据库服务器

在 `mysql` 会话期间，或通过将数据添加到纯文本文件中并加载到数据库来处理每条记录。

> 注意：在进行 `mysql` 会话期间，请记住您可以使用上方向键来检索和更改之前的命令。当你正在手动输入包含相似信息的数据库记录时，这特别有用用。

### 手动输入数据

为了在此会话中执行此操作，我假设你已经打开了一个 `mysql` 会话，并且已经按照上一节的描述创建了数据库。如果你尚未连接到 `mysql` 会话，请输入以下命令（假设 `mysql` 用户名为 `root`）：

```mysql
$ mysql -u root -p
Enter password: ********
mysql>
```

要向现有的 MySQL 数据库中添加数据，以下内容介绍了如何查看可用表以及如何手动将数据加载到这些表中。下一节将描述如何创建一个包含数据库数据的纯文本文件，以及如何将该文件加载到你的数据库中。

1. 要让你想使用的数据库成为当前数据库（在本例中为 `allusers`），请在 `mysql>` 提示符下输入以下命令：
```mysql
mysql> USE allusers;
Database changed
```

2. 要查看与当前数据库关联表，请在 `mysql>` 提示符下输入以下命令：
```mysql
mysql> SHOW tables;
+--------------------+
| Tables_in_allusers |
+--------------------+
| name               |
+--------------------+
1 row in set (0.00 sec)
```

你可以看到到为止为 `allusers` 数据库定义的唯一表名为 `name` 的表。

3. 要显示 `name` 表的格式，请在 `mysql>` 提示符下输入以下命令：
```mysql
mysql> DESCRIBE name;
+------------------------------------------------+
| Field      | Type        | Null | Key  | Default | Extra |
+------------------------------------------------+
| firstname | varchar(20) | NO   |        |         | |
| lastname  | varchar(20) | NO   |        |         | |
+------------------------------------------------+
```

### 从文件加载数据

在 `mysql` 会话中使用 `LOAD` 命令，你可以将包含数据库记录的文件加载到你的 MySQL 数据库中。关于创建要加载到 MySQL 的数据文件，你需要了解以下几点内容：

- 你可以使用任何 Linux 文本编辑器创建文件。
- 每条记录（由表中的所有列组成）必须独占一行。（换行符表示下一条记录的开始）
- 使用 Tab 字符（制表符）分隔每个列。
- 你可以通过在特定记录的该列中放置 `\N` 来将该记录的该列留空。
- 你在文件中留下的任何空行都会导致数据库表中出现空行。

在例例中，将以下文本被添加到纯文本文件中。该文本的格式可以加载到本章之前创建的 `name` 表。要尝试一下，请将以下文本输入到文件中。确保在每个值之间插入一个 Tab 字符。

Chris Smith 175 Harrison Street Gig Harbor WA 98999

John Jones 18 Talbot Road NW NJ 54889

Howard Manty 1515 Broadway New York NY 10028

当你输入数据时，将文本保存到任何 `mysql` 服务守护进程可访问的文件名（例如，`/tmp/name.txt`）。记住文件名，以便稍后使用。如果你尚未连接到 `mysql` 会话，请输入以下命令（假设 `mysql` 用户名为 `root`）：

```mysql
$ mysql -u root -p
Enter password: ********
mysql>
```

接下来，通过输入以下内容将数据库（本例中为 `allusers`）识别为当前数据库：

```mysql
mysql> USE allusers;
Database changed
```

要实际将文件加载到 `allusers` 数据库中的 `name` 表，请在 `mysql>` 提示符下输入以下命令加载文件（在此为 `/tmp/name.txt`）：

> 注意：输入文件的完整路径或将其放在 `mysql` 命令启动的目录中。在后的情况下，你可以输入文件名而不指定其完整路径。

```mysql
mysql> LOAD DATA INFILE "/tmp/name.txt" INTO TABLE name;
Query OK, 3 rows affected (0 sec)
Records: 3 Deleted: 0 Warnings: 0
```

输入以下内容使记录已添加：

| firstname | lastname | streetaddr | city | state | zipcode |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| John | Jones | 18 Talbot Road NW | NJ | 54889 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |

到此时，你已经有一个包含你可以操作数据的数据库。尽管 MySQL 不支持所有的 SQL，但它包含了足够满足用户的功能。如果你发现 MySQL 不满足你的需求，可以使用 PostgreSQL 对象关系数据库管理系统（它也随 Fedora 和 RHEL 提供）。有关 PostgreSQL 的更多信息，请参考 www.postgresql.org。Firebird (www.firebird.org) 是另一个你可能感兴趣的关系数据库。

## 理解 MySQL 表

设置表时你有很大的活性。为了让你的 MySQL 高效运行，你必须为列分配最合适的大小和类型以存储你需要的数据。

使用下表作为分配给列的不同数据类型的参考。MySQL 中可用的数据类型分为以下几类：数字、时间和字符字符串。在阅读这些表时，你需要了解以下几点内容：

- 列的最大显示大小为 255 个字符。M 数据类型选项设置了显示以及在大多数情况下存储的列字符。
- 对于浮点或固定点数据类型，小数点后最多可以有 30 位数字。数据类型的 D 选项指示小数点后允许的位数。
- `UNSIGNED` 选项（括号中显示）表示列中只允许正数。这允许列存储更大的正数。
- `ZEROFILL` 选项（括号中显示）表示列中的数据将用零填充。例如，在类型为 `INTEGER (7) ZEROFILL` 的列中，数字 25 将显示 0000025。（任何 `ZEROFILL` 列会自动变为 `UNSIGNED`。）
- 所有括号中显示的值都是可选的。
