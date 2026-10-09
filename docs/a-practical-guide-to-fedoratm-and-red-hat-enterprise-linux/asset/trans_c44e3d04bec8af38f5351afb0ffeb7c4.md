

LIKE

你还可以在 **WHERE** 子句中使用 **LIKE** 运算符。**LIKE** 会使 **SELECT** 返回列中包含指定字符串的行。在 **LIKE** 后面跟随的字符串中，百分号（%）匹配零个或多个字符组成的任意字符串，而下划线（_）匹配任意单个字符。以下查询返回 **name** 列中包含字母 m 的行。

```
MariaDB [maxdb]> SELECT     name,
                    store
            FROM       people
            WHERE      name LIKE '%m%';
+------+------+ 
| name | store | 
+------+------+ 
| max  |    4 | 
| sam  |    6 | 
+------+------+ 
2 rows in set (0.00 sec)
```

## 备份数据库

`mysqldump` 实用程序可以备份和恢复数据库。备份数据库会生成一个包含创建表并加载数据的 **SQL** 语句的文件。你可以使用此文件从零开始恢复数据库。下一个示例展示了 Max 如何备份 **maxdb** 数据库到一个名为 **maxdb.bkup.sql** 的文件中。

```
$ mysqldump -u max -p maxdb > maxdb.bkup.sql
Enter password:
```

请注意：以下恢复过程将覆盖现有数据库。在恢复数据库之前，你必须按照第 1121 页的说明创建数据库。在创建 **maxdb** 数据库后，Max 运行 MariaDB，输入来自 `mysqldump` 创建的文件。输入以下命令后，**maxdb** 数据库将恢复到 Max 备份时的状态。

```
$ mysql -u max -p maxdb < maxdb.bkup.sql
Enter password:
```

## 修改数据

- **DELETE FROM**

**DELETE FROM** 语句从表中删除一行或多行。下一个示例删除 **people** 表中 **name** 列值为 **bailey** 或 **percy** 的行。

```
MariaDB [maxdb]> DELETE FROM     people
            WHERE      name='bailey'
                       OR name='percy';
Query OK, 2 rows affected (0.00 sec)
```

- **UPDATE**

**UPDATE** 语句修改表中的数据。以下示例将 **name** 列包含 **sam** 或 **topsy** 的行中的 **hourly** 列设置为 **TRUE**（1）。MariaDB 的消息显示查询匹配了两行（**sam** 和 **topsy**），但只修改了一行。它修改了包含 **topsy** 的行中的 **hourly**；在包含 **sam** 的行中，**hourly** 已经设置为 **TRUE**。

```
MariaDB [maxdb]> UPDATE       people
            ->      SET    hourly = TRUE
            ->      WHERE name = 'sam' OR
            ->             name = 'topsy';
Query OK, 1 row affected (0.00 sec)
Rows matched: 2  Changed: 1  Warnings: 0
```

CURDATE() 函数返回今天的日期。下一个示例将 **name** 列包含 max 的行中的 hired 列设置为今天的日期。

```
MariaDB [maxdb]> UPDATE       people
            ->      SET    hired = CURDATE()
            ->      WHERE name = 'max';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

下一个查询显示了上述 DELETE FROM 和 UPDATE 语句的结果。

```
MariaDB [maxdb]> select * from people;
+-------+------------+-------+--------+
| name  | hired      | store | hourly |
+-------+------------+-------+--------+
| topsy | 2012-11-01 |     4 |      1 |
| max   | 2012-02-12 |     4 |      0 |
| zach  | 2009-03-24 |     6 |      0 |
| sam   | 2008-01-28 |     6 |      1 |
+-------+------------+-------+--------+
4 rows in set (0.00 sec)
```

## 创建第二个表

接下来，setup.stores SQL 命令文件会在 maxdb 数据库中创建、填充并显示 stores 表。

```
$ mysql -vv < setup.stores

CREATE TABLE       stores (
                    name VARCHAR(20),
                    number INTEGER,
                    city VARCHAR(20)
)
------------------

Query OK, 0 rows affected


------------------
INSERT INTO        stores
     VALUES       ( 'headquarters' , 4 , 'new york' ) ,
                   ( 'midwest' , 5 , 'chicago' ) ,
                   ( 'west coast' , 6 , 'san francisco' )
------------------

Query OK, 3 rows affected
Records: 3  Duplicates: 0  Warnings: 0

------------------
SELECT * FROM stores
name number city
headquarters 4 new york
midwest 5 chicago
west coast 6 san francisco
3 rows in set
```

*stores* 表有 3 个列，分别命名为 **name**、**number** 和 **city**。 **name** 和 **city** 列的数据类型为 VARCHAR。VARCHAR 列存储变长字符串，不需要 CHAR 列所需的填充。在此示例中，**name** 和 **city** 列每列最多可存储 20 个字符。

VARCHAR 的大小是长度前缀加上要存储的字符串中的字符数之和。对于声明存储少于 255 个字符的列，其长度前缀为 1 字节；较大的列具有 2 字节的长度前缀。相比之下，CHAR 列始终占据其声明的字符数。

VARCHAR 声明中括号内的数字指定该列中任何行可存储的最大字符数。在示例中，**city** 列声明为 VARCHAR(20)，因此该列中的行不能超过 20 个字符。**city** 列中包含 **new york** 的行占用 9 字节的存储空间（8 + 1）。如果该列声明为 CHAR(20)，无论其存储的字符串长度如何，每行都将占用 20 字节。

## 连接

连接操作根据数据库中两个或多个相关表之间的关系，将这些表中的行进行组合。以 **maxdb** 数据库为例：**people** 表有包含员工姓名、入职日期、员工工作的商店以及员工是否为计时工（相对于计薪工）等信息的列；**stores** 表有包含商店名称、编号及其所在城市的列。在这种情况下，仅查询 **people** 或 **stores** 表无法确定员工工作的城市；必须连接这两个表才能获取此信息。

你使用 SELECT 语句来连接表，该语句指定每个表中的一个列以及这些列之间的关系。满足示例的查询指定了 **people** 表中的 **store** 列和 **stores** 表中的 **number** 列；这些列之间的关系是相等，因为这两列都存储商店编号。当你在这些列中赋予相同的值时，你可以显示 **people** 表中每个 **name** 对应的 **stores** 信息（或者 **stores** 表中每个 [store] **number** 对应的 **people** 信息）。

以下查询从 **people** 和 **stores** 表中选择行，并在 **people** 表中 **store** 的值等于 **stores** 表中 **number** 的值时（**store = number**）连接这些行。此查询使用隐式连接；它不使用 **JOIN** 关键字。此后的示例使用 JOIN。使用此关键字不会改变查询结果，但在某些类型的查询中你必须使用 JOIN。

```
MariaDB [maxdb]> SELECT *
->              FROM people, stores
->              WHERE store = number;
```

| name | hired | store | hourly | name | number | city |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| headquarter | 2012-11-01 | 4 | 1 | new york | 4 | |
| max | 2012-02-12 | 4 | 0 | headquarter | 4 | new york |
| zach | 2009-03-24 | 6 | 0 | west coast | 6 | san francisco |
| sam | 2008-01-28 | 6 | 1 | west coast | 6 | san francisco |

4 rows in set (0.00 sec)

## 内连接

前面的查询演示了 *内连接*。如果愿意，你可以在此类查询中使用关键字 INNER JOIN 替代 JOIN。在返回的每行中，people.store 的值等于 stores.number 的值。然而，stores 表中有一行 number 列的值为 5，但 people 表中没有 store 列值为 5 的行。因此，这些查询不会返回 people.store 和 stores.number 等于 5 的行。

## 表名

在处理关系型数据库时，你可以将特定表中的列表示为 table_name.column_name（例如，示例数据库中的 stores.name）。当处理单个表时，列名足以唯一标识你要处理的数据。当处理多个表时，你可能需要指定表名和列名来唯一标识某些数据。具体而言，如果在被连接的两个表中有两列具有相同的名称，你必须同时指定表和列以消除列的歧义。以下查询演示了这个问题。

```
MariaDB [maxdb]> SELECT *
->              FROM people, stores
->              WHERE store = number and
->                    name = 'max';
ERROR 1052 (23000): Column 'name' in where clause is ambiguous
```

在上面的查询中，列名存在歧义：people 和 stores 表中都存在名为 name 的列。MariaDB 无法确定在 WHERE 子句中应使用哪个表。下一个查询解决了这个问题。它使用 people.name 在 WHERE 子句中指定 MariaDB 应使用 people 表中的 name 列。

```
MariaDB [maxdb]> SELECT *
->              FROM people, stores
->              WHERE store = number and
->                    people.name = 'max';
```

| name | hired | store | hourly | name | number | city |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| max | 2012-05-01 | 4 | 0 | headquarter | 4 | new york |

1 row in set (0.01 sec)

