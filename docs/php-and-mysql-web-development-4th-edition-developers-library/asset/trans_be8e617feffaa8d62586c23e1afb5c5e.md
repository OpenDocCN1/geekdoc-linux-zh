
## 2.6 创建、删除、索引和修改表

如果你使用连接池或持久连接，当你的应用程序终止时，你与 MySQL 服务器的连接并不一定会关闭。这些机制可能会保持连接打开，以供其他客户端使用，这意味着你不能假设 TEMPORARY 表会在应用程序终止时自动消失。

### 2.6.2.4 从其他表或查询结果创建表

有时创建表的副本会有用。例如，你可能有一个数据文件想要使用 LOAD DATA 加载到表中，但对于指定数据格式的选项并不完全确定。如果第一次没有正确设置选项，原始表中可能会出现格式错误的行。使用原始表的空副本，可以让你对指定列和行定界符的 LOAD DATA 选项进行实验，直到你满意输入行被正确解释为止。然后，你可以使用原始表名重新运行 LOAD DATA 语句，将文件加载到原始表中。

有时，将查询结果保存到表中而不是看着它从屏幕顶部滚过也是有价值的。通过保存结果，你可以稍后引用它而无需重新运行原始查询，也许是为了对其进行进一步的分析。MySQL 提供了两个语句，用于从其他表或查询结果创建新表。这些语句各有优缺点：

- CREATE TABLE ... LIKE 将新表创建为原始表的空副本。它精确地复制原始表的结构，因此每个列都保留其所有属性，索引结构也会被复制。但是，新表是空的，如果你想要填充它，需要第二条语句（如 INSERT INTO ... SELECT）。此外，CREATE TABLE ... LIKE 不能创建原始表列子集的新表，也不能使用除原始表以外的其他表的列。

- CREATE TABLE ... SELECT 从任意 SELECT 语句的结果创建新表。默认情况下，此语句不会复制所有列属性，例如 AUTO_INCREMENT。此外，通过选择数据到表中来创建表也不会自动从原始表复制任何索引，因为结果集本身并没有索引。另一方面，CREATE TABLE ... SELECT 可以在一个语句中同时创建和填充新表。它还可以使用原始表的子集创建新表，并包括来自其他表的列或作为表达式结果创建的列。

要使用 CREATE TABLE ... LIKE 创建现有表的空副本，请编写如下语句：

```sql
CREATE TABLE new_tbl_name LIKE tbl_name;
```

要创建表的空副本然后从原始表填充它，请使用 CREATE TABLE ... LIKE 后跟 INSERT INTO ... SELECT：

```sql
CREATE TABLE new_tbl_name LIKE tbl_name;
INSERT INTO new_tbl_name SELECT * FROM tbl_name;
```

要将表创建为自身的临时副本，请包含 TEMPORARY 关键字：

```sql
CREATE TEMPORARY TABLE new_tbl_name LIKE tbl_name;
INSERT INTO new_tbl_name SELECT * FROM tbl_name;
```

当你想要尝试一些修改表内容的语句，但不希望更改原始表时，使用与原始表同名的 TEMPORARY 表会有用。要使用使用原始表名的预写脚本，你不需要编辑它们以引用不同的表；只需在脚本开头添加 CREATE TEMPORARY TABLE 和 INSERT 语句即可。脚本将创建一个临时副本并在副本上操作，该副本会在脚本结束时由服务器删除。（但是，请记住第 2.6.2.3 节“临时表”中提到的自动重连注意事项。）

如果要向新表插入原始表中的一些行，请添加一个 WHERE 子句来标识要选择的行。以下语句创建一个名为 student_f 的新表，其中仅包含 student 表中女性学生的行：

```sql
CREATE TABLE student_f LIKE student;
INSERT INTO student_f SELECT * FROM student WHERE sex = 'f';
```

如果你不关心从原始表返回确切的列定义，CREATE TABLE ... SELECT 有时比 CREATE TABLE ... LIKE 更容易使用，因为它可以在一个语句中创建和填充新表：

```sql
CREATE TABLE student_f SELECT * FROM student WHERE sex = 'f';
```

CREATE TABLE ... SELECT 还可以创建不包含现有表中完全相同列集的新表。你可以使用它使新表迅速出现，以保存任意 SELECT 查询的结果。这使得创建完全填充了你感兴趣的数据的表变得异常简单，并准备好用于进一步的语句。但是，如果你不仔细，新表可能包含奇怪的列名。当你通过选择数据到表中创建表时，列名取自你选择的列。如果列是作为表达式的结果计算出来的，列的名称就是该表达式的文本，这将创建一个具有不寻常列名的表：

```sql
mysql> CREATE TABLE mytbl SELECT PI() * 2;
mysql> SELECT * FROM mytbl;
+----------------+
| PI() * 2       |
+----------------+
| 6.283185       |
+----------------+
```

这是不幸的，因为列名只能作为带引号的标识符直接引用：

```sql
mysql> SELECT `PI() * 2` FROM tdbl;
+-----------+
| PI() * 2 |
+-----------+
| 6.283185 |
+-----------+
```

为了避免这个问题并提供一个更容易处理的列名，请使用别名：

```sql
mysql> DROP TABLE mytbl;
mysql> CREATE TABLE mytbl SELECT PI() * 2 AS mycol;
mysql> SELECT mycol FROM mytbl;
+-------+
| mycol |
+-------+
| 6.283185 |
+-------+
```

如果你从具有相同名称列的不同表中选择数据，也会出现相关的问题。假设表 t1 和 t2 都有一个列 c，你想创建一个包含两个表中所有行组合的表。以下语句会失败，因为它试图创建一个有两个名为 c 的列的表：

```sql
mysql> CREATE TABLE t3 SELECT * FROM t1 INNER JOIN t2;
ERROR 1060 (42S21): Duplicate column named 'c'
```

为了解决这个问题，请提供必要的别名，以在新表中为每个列提供唯一的名称：

```sql
mysql> CREATE TABLE t3 SELECT t1.c, t2.c AS c2
    -> FROM t1 INNER JOIN t2;
```

如前所述，CREATE TABLE ... SELECT 的一个缺点是，原始数据的所有特性并未都结合到新表的结构中。例如，通过选择数据到表中创建表不会从原始表复制索引，并且可能会丢失列属性。保留的属性包括列是 NULL 还是 NOT NULL，字符集和排序规则，默认值，以及列注释。

在某些情况下，通过在语句的 SELECT 部分调用 CAST() 函数，你可以强制在新表中使用特定的属性。以下 CREATE TABLE ... SELECT 语句强制由 SELECT 产生的列被视为 INT UNSIGNED、TIME 和 DECIMAL(10,5)，你可以通过 DESCRIBE 验证：

```sql
mysql> CREATE TABLE mytbl SELECT
    -> CAST(1 AS UNSIGNED) AS i,
    -> CAST(CURTIME() AS TIME) AS t,
    -> CAST(PI() AS DECIMAL(10,5)) AS d;
```

```sql
mysql> DESCRIBE mytbl;
+-------+----------------+-----+------+---------+
| Field | Type           | Null| Key  | Default | Extra
+-------+----------------+-----+------+---------+
| i     | int(1) unsigned| NO  |      | 0       |       |
| t     | time           | YES |      | NULL    |       |
| d     | decimal(10,5)  | NO  |      | 0.00000 |       |
+-------+----------------+-----+------+---------+
```

允许的强制转换类型有 BINARY（二进制字符串）、CHAR、DATE、DATETIME、TIME、SIGNED、SIGNED INTEGER、UNSIGNED、UNSIGNED INTEGER 和 DECIMAL。

你也可以在 CREATE TABLE 部分提供明确的列定义，用于 SELECT 部分检索的列。两部分的列按名称匹配，因此在 SELECT 部分提供必要的别名，以使它们正确匹配：

```sql
mysql> CREATE TABLE mytbl ( i INT UNSIGNED, t TIME, d DECIMAL(10,5))
    -> SELECT
    -> 1 AS i,
    -> CAST(CURTIME() AS TIME) AS t,
    -> CAST(PI() AS DECIMAL(10,5)) AS d;
mysql> DESCRIBE mytbl;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null| Key | Default | Extra
+-------+--------------+------+-----+---------+-------+
| i     | int(10) unsigned| YES|     | NULL    |       |
| t     | time         | YES |     | NULL    |       |
| d     | decimal(10,5)  | YES |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
```

提供明确定义的技术使你可以创建具有指定精度和小数的数值列，具有与结果集中最长值不同宽度的字符列等。另外请注意，在此示例中，某些列的 Null 和 Default 属性与上一个示例中的不同。如有必要，你可以在 CREATE TABLE 部分为这些属性提供明确的定义。

### 2.6.2.5 使用 MERGE 表

MERGE 存储引擎允许你将一组 MyISAM 表视为一个单一的逻辑单元，从而同时对它们执行查询。如前文第 2.6.1 节“存储引擎特性”中所述，MERGE 可以应用于一组结构完全相同的 MyISAM 表。每个表中的列必须以相同的名称和类型，按相同的顺序定义，索引必须按相同的方式和顺序定义。

