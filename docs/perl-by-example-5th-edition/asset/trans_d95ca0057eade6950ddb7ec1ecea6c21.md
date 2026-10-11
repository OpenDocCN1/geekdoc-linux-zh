
## 说明

`INSERT INTO` 语句用于向 `Shippers` 表中插入一个新的行，首先列出字段名，然后在 `VALUES` 关键字后列出对应的值。`ShipperID` 的值未被包含在内，因为在创建表时，`ShipperID` 被设置为 `PRIMARY KEY`（主键），每次添加新的托运商记录时，数据库会自动对其进行自增。（让数据库自动递增 `PRIMARY KEY` 可以确保该值始终唯一。）要了解该表最初是如何设置的，请参阅此处 `DESCRIBE` 命令的输出：

```sql
mysql> DESCRIBE shippers;

+---------------+----------+-----+----+
| Field          | Type     |     |    |
+---------------+----------+-----+----+
| ShipperID      | int(11)  |     | PRI |
| CompanyName    | varchar(40)|   | NULL |
| Phone          | varchar(24)| YES| NULL |
+---------------+----------+-----+----+
```

### B.2.3 `UPDATE` 命令

`UPDATE` 语句用于修改表中的数据。在 `UPDATE` 命令之后，列出要更改数据的表名，然后是使用 `SET` 语句来指示要更改的字段，接着是要分配给该字段的新值。`WHERE` 子句进一步限定了要修改的数据，从而限制了更新的范围。

在示例 B.23 中，关键在于使用 `WHERE` 语句来限制更新的范围。

**格式**

```sql
UPDATE table_name
SET column_name = new_value
WHERE column_name = some_value
```

**示例：**

```sql
UPDATE orders SET ShipCountry='Luxembourg' WHERE CustomerId='white';
```

**示例 B.23**

```sql
1
mysql> select * from shippers;
+-----------+---------------------+---------------+
| ShipperID | CompanyName         | Phone         |
+-----------+---------------------+---------------+
|         1 | Speedy Express      | (503) 555-9831|
|         2 | United Package      | (503) 555-3199|
|         3 | Federal Shipping    | (503) 555-9931|
+-----------+---------------------+---------------+
3 rows in set (0.00 sec)

2
mysql> UPDATE shippers SET PHONE='(777) 444-1234'
    -> WHERE companyname = 'Federal Shipping';
Query OK, 1 row affected (0.08 sec)
Rows matched: 1  Changed: 1  Warnings: 0

3
mysql> select * from shippers;
+-----------+---------------------+---------------+
| ShipperID | CompanyName         | Phone         |
+-----------+---------------------+---------------+
|         1 | Speedy Express      | (503) 555-9831|
|         2 | United Package      | (503) 555-3199|
|         3 | Federal Shipping    | (777) 444-1234|
+-----------+---------------------+---------------+
3 rows in set (0.00 sec)
```

**说明**

1.  `SELECT` 命令显示了 `Shippers` 表中的所有字段。
2.  `UPDATE` 命令允许你修改现有记录。此处正在更改 Federal Shipping 的电话号码。
3.  此 `SELECT` 命令显示，Federal Shipping 的电话号码已被上一个 `UPDATE` 命令更改。

### B.2.4 `DELETE` 语句

`DELETE` 语句用于删除表中的行，并返回被删除的行数。`DELETE` 使用 `FROM` 子句来指定包含要删除数据的表名，并使用 `WHERE` 子句来指定识别要移除哪些数据的条件。

请小心！如果没有 `WHERE` 子句，所有行都将被删除。[1]

如果指定了 `ORDER BY` 子句，则按指定的顺序删除行。`LIMIT` 子句限制了可删除的行数。

1.  你可以配置 MySQL，使得如果你在没有 `WHERE` 子句的情况下使用 `DELETE`，则行不会被删除。

**格式**

```sql
DELETE FROM table_name
WHERE column_name = some_value
```

**DELETE** 语句与 **UPDATE** 语句非常相似。要删除上一条记录，你可以输入此查询：

```sql
DELETE FROM Shippers WHERE CompanyName='Canada Post';
```

## B.3 SQL 数据定义语言

SQL 的数据定义语言（DDL）部分允许创建或销毁数据库对象。你还可以定义索引（键），指定表之间的链接，以及在数据库表之间施加约束。通常，创建和删除数据库的决策由数据库管理员处理，而是否具有创建和删除表的权限则取决于被授予的访问权限。

SQL 中最重要的数据定义语句包括：

-   **CREATE TABLE** — 创建新的数据库表。
-   **ALTER TABLE** — 修改（更改）数据库表。
-   **DROP TABLE** — 删除数据库表。
-   **CREATE INDEX** — 创建索引（搜索键）。
-   **DROP INDEX** — 删除索引。

### B.3.1 创建数据库

创建数据库非常简单。你只需发出一个命令，唯一的参数是数据库名称。

**格式**

```sql
CREATE DATABASE database_name
```

在之前的示例中，我们使用了 *northwind* 数据库。现在我们将为一家艺术画廊创建一个数据库。

**示例 B.24**

```sql
1 mysql> CREATE DATABASE gallerydb;
   Query OK, 1 row affected (0.03 sec)

2 mysql> show databases;
+-----------------+
| Database        |
+-----------------+
| gallerydb       |
| mysql           |
| northwind       |
| phpmyadmin      |
| test            |
+-----------------+
5 rows in set (0.00 sec)
```

**说明**

就这样。数据库现在已经创建好了。请注意，尽管我们创建了数据库，但我们此时仍不在该数据库中。下一个示例中的 USE 命令将使新数据库成为当前默认数据库。

**示例 B.25**

```sql
1 mysql> USE gallerydb;
   Database changed
```

**说明**

我们现在处于 gallerydb 数据库中，所有的 SQL 命令都将在此数据库上执行。

### B.3.2 SQL 数据类型

创建数据库后，你需要添加构成该数据库的表。在创建表之前，你必须决定其中将存储什么类型的数据；例如，你会存储姓名、日期、零件号、社保号、价格等行吗？数据类型指定列可以容纳的数据类型。基本类型包括字符串、数字以及日期和时间类型。有关完整记录的列表，请参见 http://dev.mysql.com/doc/refman/5.0/en/data-types.html。

表 B.3 包含 SQL 中最常见的数据类型。

**表 B.3 最常见的 SQL 数据类型**

| 数据类型 | 描述 |
| :--- | :--- |
| **数字** | |
| INTEGER | 存储 4 字节的整数。 |
| INT UNSIGNED | 存储 4 字节的非负整数。 |
| SMALLINT | 存储 2 字节的整数。 |
| TINYINT | 存储 1 字节的整数。 |
| FLOAT(m, d) | 4 字节的浮点数。对于值 999.00009，FLOAT(7, 4) 的结果为 999.0001。m 指定数字的最大位数。d 指定小数点右侧的最大位数。 |
| DOUBLE(m, d) | 8 字节的双精度浮点数。 |
| DECIMAL(m, d) | 实数或 8 字节的小数。m 指定数字的最大位数。d 指定小数点右侧的最大位数。 |
| NUMERIC(m, d) | DECIMAL 和 NUMERIC 数据类型用于存储具有精确精度的精确数值数据，例如货币数据。存储带小数的数字。 |
| **字符串** | |
| CHAR(SIZE) | 存储固定长度的字符串（可包含字母、数字和特殊字符），长度从 0 到 255 个字符。括号中指定固定大小。 |
| VARCHAR(SIZE) | 可变长度字符串（可包含字母、数字和特殊字符），在 MySQL 5.0.3 及更高版本中长度为 0 到 65,535。括号中指定最大大小。 |
| TINYTEXT | 最大长度为 255 个字符的字符串。 |
| TEXT | 最大长度为 65,535 个字符的可变长度文本字符串，用于存储大型文本文件、文档、文本区域等。 |
| BLOB | 二进制大对象。最大长度为 65,535 个字符的二进制字符串，用于存储二进制文件、图像、声音等。 |
| **日期和时间** | |
| DATE | (yyyy-mm-dd) 年、月、日；例如，2006-10-30（注意：MySQL 也允许你存储 0000-00-00 作为“虚拟日期”。） |
| DATETIME | (yyyy-mm-dd hh:mm:ss) 日期和时间；例如，2006-10-30 22:59:59 |
| TIMESTAMP | (yyyy-mm-dd hh:mm:ss) 日期和时间；例如，1970-01-01（行上次事务的日期和时间） |
| TIME | (hh:mm:ss) 时间；例如，10:30:58 |
| YEAR | (yyyy \| yy) 四位或两位数的年份；例如，1978 或 78 |

