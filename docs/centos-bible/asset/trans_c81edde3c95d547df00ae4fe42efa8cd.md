

| 名字 | 姓氏 | 街道地址 | 城市 | 州 | 邮政编码 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Mantly | 1515 Broadway | New York | NY | 10028 |

以下命令显示 name 表中所有 lastname 列设置为 Jones 的记录。使用 lastname 之外，你还可以搜索表中使用的任何列名的值：

```sql
mysql> SELECT * FROM name WHERE lastname= "Jones";
```

| 名字 | 姓氏 | 街道地址 | 城市 | 州 | 邮政编码 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |

使用 OR 运算符，你可以选择匹配多个不同值的记录。在下面的命令中，firstname 为 Chris 或 Howard 的记录会被匹配并显示。

```sql
mysql> SELECT * FROM name WHERE firstname= "Chris" OR firstname= "Howard";
```

| 名字 | 姓氏 | 街道地址 | 城市 | 州 | 邮政编码 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| Howard | Mantly | 1515 Broadway | New York | NY | 10028 |

要根据记录中两列的值来匹配并显示记录，你可以使用 AND 运算符。在下面的命令中，任何 firstname 为 Chris 且 lastname 为 Smith 的记录都会被匹配。

```sql
mysql> SELECT * FROM name WHERE firstname= "Chris" AND lastname= "Smith";
```

| 名字 | 姓氏 | 街道地址 | 城市 | 州 | 邮政编码 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |

## 显示选定的列

你不需要显示所有列的数据。与其使用前面示例中显示的天文符号 (*) 来匹配所有列，你可以输入一个逗号分隔的列名列表。以下命令显示 name 表中所有记录的 firstname、lastname 和 zipcode 信息：

```sql
mysql> SELECT firstname,lastname,zipcode FROM name;
```

| 名字 | 姓氏 | 邮政编码 |
| :--- | :--- | :--- |

同样，你可以按任何顺序对列进行排序。键入以下命令以显示相同的三列，并将 `zipcode` 列显示在最前：

```sql
mysql> SELECT zipcode, firstname, lastname FROM name;

+---------+-----------+----------+
| zipcode | firstname | lastname |
+---------+-----------+----------+
| 98999 | Chris | Smith |
| 54889 | John | Jones |
| 10028 | Howard | Mantly |
+---------+-----------+----------+
```

你还可以将列选择与记录选择混合使用，如下例所示：

```sql
mysql> SELECT firstname, lastname, city FROM name WHERE firstname= “Chris”;

+-----------+----------+-----------+
| firstname | lastname | city |
+-----------+----------+-----------+
| Chris | Smith | Gig Harbor |
+-----------+----------+-----------+
```

# 第四部分 网络

![](img/2f265415ceec72538dd3c78ffca75c10_903_0.png)

## 排序数据

你可以根据任何列中的值对记录进行排序。例如，使用 ORDER BY 运算符，你可以基于 `lastname` 列显示记录。

```sql
mysql> SELECT * FROM name ORDER BY lastname;

+-----------+----------+--------------+----------+--------+---------+
| firstname | lastname | streetaddr | city | state | zipcode |
+-----------+----------+--------------+----------+--------+---------+
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Mantly | 1515 Broadway | New York | NY | 10028 |
| Chris | Smith | 167 Small Road | Gig Harbor | WA | 98999 |
+-----------+----------+--------------+----------+--------+---------+
```

要根据城市名称对记录进行排序，你可以使用以下命令：

```sql
mysql> SELECT * FROM name ORDER BY city;

+-----------+----------+--------------+----------+--------+---------+
| firstname | lastname | streetaddr | city | state | zipcode |
+-----------+----------+--------------+----------+--------+---------+
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
+-----------+----------+--------------+----------+--------+---------+
```

你还可以添加 ASC 或 DESC 以指示排序顺序，因为 MySQL 否则不会保证数据显示的顺序。现在你已输入并显示了数据库记录，你可能会发现需要更改其中一些记录。下一节描述了如何在 mysql 会话期间更新数据库记录。

# 修改表和记录

当你开始使用 MySQL 数据库时，你会发现需要对数据库表的结构和内容进行修改。本节描述如何更改 MySQL 表的结构以及如何更改 MySQL 记录的内容。如果你尚未连接到 mysql 会话，请键入以下命令（假设 MySQL 用户名为 root）：

```bash
$ mysql -u root -p
Enter password: ******
mysql>
```

要使用下列各节中显示的示例，请通过键入以下内容将数据库（本例中为 allusers）识别为当前数据库：

```sql
mysql> USE allusers;
Database changed
```

## 更改 MySQL 表的结构

在你创建数据库表之后，你难免会想要对其进行一些更改。本节描述了如何在 mysql 会话中使用 ALTER 命令完成以下任务：添加列、删除列、重命名列以及更改列的数据类型。

要在表末尾添加一个显示当前日期的列，请键入以下内容：

```sql
mysql> ALTER TABLE name ADD curdate TIMESTAMP;
```

上一行指示 MySQL 更改当前数据库中名为 name 的表（ALTER TABLE name），添加一个名为 curdate 的列（ADD curdate），并将该列的值分配为显示最后编辑日期（TIMESTAMP 数据类型）。如果你后来决定想要删除该列，可以键入以下内容将其移除：

```sql
mysql> ALTER TABLE name DROP COLUMN curdate;
```

如果你想更改现有列的名称，可以使用 `ALTER` 的 `CHANGE` 选项进行操作。这里有一个示例：

```sql
mysql> ALTER TABLE name CHANGE city town varchar(20);
```

在上面的示例中，选择了 name 表（`ALTER TABLE name`）以将 city 列的名称更改为 town（`CHANGE city town`）。即使你不更改该列的数据类型，也必须输入该列的数据类型（`varchar(20)`）。事实上，如果你只是想更改列的数据类型，你可以使用与上述示例相同的语法，只需将列名重复两次（在本例中为 `zipcode`）。这里有一个示例：

```sql
mysql> ALTER TABLE name CHANGE zipcode zipcode INTEGER;
```

上面的示例将 `zipcode` 列的数据类型从其先前类型（`varchar`）更改为 `INTEGER` 类型。

> **注意**
> 如果你最初创建表时（`CREATE TABLE` 命令）指定了列，它将更改该列的默认值。通过运行 `ALTER TABLE` 语句，你可以重新指定列的默认值，如果你希望恢复为该值的话。

# 更新和删除 MySQL 记录

你可以基于任何你选择的值选择记录，并更新这些记录中的任何值。当你处于 `mysql` 会话中时，你可以使用 `UPDATE` 来更改选定表中的值。这里有一个示例。

```sql
mysql> UPDATE name SET streetaddr="933 3rd Avenue" WHERE firstname="Chris";
Query OK, 1 row affected (0.00 sec)
Rows matched: 1 Changed: 1 Warnings: 0
```

这个示例试图更新 name 表（`UPDATE name`）。在这个示例中，每个 `firstname` 列设置为 `Chris` 的记录都将把该记录的 `streetaddr` 列的值更改为 933 3rd Avenue。请注意，查询找到了一个匹配的行。该匹配的行也被更改了，没有错误警告。你可以使用任何值的组合来匹配记录（使用 `WHERE`）并更改你希望的列值（使用 `SET`）。在进行更改后，最好显示结果以确保更改是你预期的那样。

要删除整行（即一条记录），你可以使用 `DELETE` 命令。例如，如果你想删除 `firstname` 列值为 `Chris` 的任何行，你可以键入以下内容：

```sql
mysql> DELETE FROM name WHERE firstname="Chris";
Query OK, 1 row affected (0.00 sec)
```

下次你显示该表时，应该没有名字为 Chris 的记录了。

