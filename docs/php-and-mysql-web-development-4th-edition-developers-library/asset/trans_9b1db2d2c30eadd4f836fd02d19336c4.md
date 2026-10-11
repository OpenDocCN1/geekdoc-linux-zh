
**FULLTEXT**（全文）索引 _index_name_ ON _tbl_name_ [_index_columns_]; **SPATIAL**（空间）索引 _index_name_ ON _tbl_name_ [_index_columns_];

*tbl_name*、*index_name* 和 *index_columns* 的含义与 **ALTER TABLE** 中的相同。与 **ALTER TABLE** 不同，在 **CREATE INDEX** 中，索引名称不是可选的，并且你无法在单个语句中创建多个索引。

当发出 **CREATE TABLE** 语句为新表创建索引时，语法与用于 **ALTER TABLE** 的语法类似，但你除了指定列定义外，还需指定索引创建子句：

```sql
CREATE TABLE _tbl_name_ (
    ... 列定义 ...
    INDEX _index_name_ [_index_columns_],
    UNIQUE _index_name_ [_index_columns_],
    PRIMARY KEY [_index_columns_],
    FULLTEXT _index_name_ [_index_columns_],
    SPATIAL _index_name_ [_index_columns_],
    ...
);
```

与 **ALTER TABLE** 一样，*index_name* 是可选的。如果你省略它，MySQL 会选择一个索引名称。

作为一个特殊情况，你可以通过在列定义的末尾添加 **PRIMARY KEY** 或 **UNIQUE** 子句来创建单列的 **PRIMARY KEY**（主键）或 **UNIQUE**（唯一）索引。例如，以下两个 **CREATE TABLE** 语句是等价的：

```sql
CREATE TABLE _mytbl_ (
    i INT NOT NULL PRIMARY KEY,
    j CHAR(10) NOT NULL UNIQUE
);

CREATE TABLE _mytbl_ (
    i INT NOT NULL,
    j CHAR(10) NOT NULL,
    PRIMARY KEY (i),
    UNIQUE (j)
);
```

**MEMORY** 表的默认索引类型是 **HASH**（哈希）。哈希索引对于精确值查找非常快，这是使用 **MEMORY** 表的典型方式。然而，如果你打算将 **MEMORY** 表用于可以匹配值范围（例如，_id_ < 100）的比较，则哈希索引效果不佳。在这种情况下，最好创建 **BTREE**（B 树）索引。你可以通过在索引定义中添加 **USING BTREE** 子句来实现：

```sql
CREATE TABLE _nametbl_
```

要为字符串列的前缀创建索引，索引定义中指定列名的语法是 col_name(n)，而不仅仅是 col_name。前缀值 n 表示索引应包含二进制字符串类型的前 n 个字节，或非二进制字符串类型的前 n 个字符。例如，以下语句创建一个包含 CHAR 列和 BINARY 列的表。它对 CHAR 列的前 10 个字符和 BINARY 列的前 15 个字节创建索引：

```sql
CREATE TABLE addresslist
(
    name     CHAR(30)  NOT NULL,
    address  BINARY(60)  NOT NULL,
    INDEX (name(10)),
    INDEX (address(15))
);
```

当你对字符串列的前缀创建索引时，前缀长度与列长度一样，是以与列数据类型相同的单位指定的——即二进制字符串为字节，非二进制字符串为字符。但是，索引条目的最大大小在内部是以字节衡量的。对于单字节字符集，这两种衡量方式是相同的，但对于多字节字符集则不同。对于具有多字节字符集的非二进制字符串，MySQL 会在允许的字节长度最大值内存储尽可能多的完整字符到索引值中。

在某些情况下，对列前缀而非整列创建索引不仅是有利的，而且是必要的：

-   对 BLOB 或 TEXT 列创建索引时，前缀是必需的。
-   索引行的长度等于构成索引的各个列的索引部分长度之和。如果此长度超过索引行中允许的最大字节数，你可以通过对列前缀创建索引来使索引“变窄”。假设一个使用 latin1 单字节字符集的 MyISAM 表包含四个名为 c1 到 c4 的 CHAR(255) 列。每个完整列值的索引值占用 255 字节，因此对所有四个列创建的索引需要 1,020 字节。然而，MyISAM 索引行的最大长度为 1,000 字节，因此你无法创建包含所有四个列完整内容的复合索引。但是，你可以通过对其中一个或所有列的较短部分创建索引来创建该索引。例如，你可以对每个列的前 250 个字符创建索引。

**FULLTEXT** 索引中的列是完整索引的，没有前缀。如果你为 **FULLTEXT** 索引中的列指定了前缀长度，MySQL 会忽略它。

具有空间数据类型（如 POINT 或 GEOMETRY）的列可以如下索引：

-   **SPATIAL** 索引仅可用于 MyISAM 表，且仅可用于 NOT NULL 的列。这些列是完整索引的。
-   其他索引类型（INDEX、UNIQUE、PRIMARY KEY）可用于任何支持空间数据类型且不是 ARCHIVE 的存储引擎。除非是 **PRIMARY KEY** 的一部分，否则列可以为 NULL。对于索引中的每个空间列（POINT 列除外），必须指定以字节为单位的 가前缀长度。

### 2.6.4.3 删除索引

要删除索引，请使用 **DROP INDEX** 或 **ALTER TABLE** 语句。要使用 **DROP INDEX**，你必须命名要删除的索引：

```sql
DROP INDEX index_name ON tbl_name;
```

要使用 **DROP INDEX** 删除 **PRIMARY KEY**（主键），请将名称 PRIMARY 作为带引号的标识符指定：

```sql
DROP INDEX `PRIMARY` ON tbl_name;
```

该语句没有歧义，因为一个表只能有一个 **PRIMARY KEY**，其名称始终为 PRIMARY。

与 **CREATE INDEX** 语句一样，**DROP INDEX** 在内部作为 **ALTER TABLE** 语句处理。上述 **DROP INDEX** 语句对应于以下 **ALTER TABLE** 语句：

```sql
ALTER TABLE tbl_name DROP INDEX index_name;
ALTER TABLE tbl_name DROP PRIMARY KEY;
```

如果你不知道表索引的名称，请使用 **SHOW CREATE TABLE** 或 **SHOW INDEX** 来查找。

当你从表中删除列时，索引可能会隐式受到影响。如果你删除作为索引一部分的列，MySQL 也会从索引中删除该列。如果你删除构成索引的所有列，MySQL 将删除整个索引。

### 2.6.5 修改表结构

**ALTER TABLE** 是一个多功能语句，有很多用途。我们在此前本章中已经看到了一些功能（用于更改存储引擎以及创建和删除索引）。你还可以使用 **ALTER TABLE** 重命名表、添加或删除列、更改列数据类型等。本节介绍其中的一些功能。附录 E 描述了 **ALTER TABLE** 的完整语法。

当你发现表的结构不再反映你希望对其执行的操作时，**ALTER TABLE** 非常有用。你可能想使用该表来记录额外信息。也许表包含的信息已变得多余。可能现有列太小，或者你发现定义的列比你需要的更大，你希望使它们变小以节省空间并提高查询性能。以下是 **ALTER TABLE** 有价值的几种情况：

-   你正在运行一个研究项目。你使用 **AUTO_INCREMENT** 列为研究记录分配案例编号。你没有预计你的资金会持续足够长的时间以生成超过 50,000 条记录，因此你将数据类型设为 **SMALLINT UNSIGNED**，它最多可容纳 65,535 个唯一值。然而，项目资金得到更新，看起来你 might 生成另外 50,000 条记录。你需要将类型变大以容纳更多的案例编号。
-   大小变化也可以是反过来的。也许你创建了一个 **CHAR(255)** 列，但现在意识到表中没有值超过 100 个字符。你可以缩短列以节省空间。
-   你想要将表转换为使用不同的存储引擎，以利用该引擎提供的功能。例如，MyISAM 表不是事务安全的，但你有一个需要事务功能的应用程序。你可以将受影响的表转换为使用 InnoDB 或 Falcon，因为这些存储引擎是支持事务的。

**ALTER TABLE** 的语法如下所示：

```sql
ALTER TABLE tbl_name action [, action] ... ;
```

每个 action 指定要对表进行的修改。一些数据库系统允许在 **ALTER TABLE** 语句中仅使用单个操作，但 MySQL 允许通过逗号分隔的多个操作。

> 如果你需要在使用 **ALTER TABLE** 之前提醒某表当前的定义，请发出 **SHOW CREATE TABLE** 语句。该语句在 **ALTER TABLE** 之后也很有用，可用于验证更改是否如预期那样影响了表定义。

以下示例讨论了 **ALTER TABLE** 的一些功能。

**更改列的数据类型。** 要更改数据类型，可以使用 **CHANGE** 或 **MODIFY** 子句。假设 mytbl 表中的列是 **SMALLINT UNSIGNED**，你想将其更改为 **MEDIUMINT UNSIGNED**。使用以下任一命令即可：

```sql
ALTER TABLE mytbl MODIFY i MEDIUMINT UNSIGNED;
ALTER TABLE mytbl CHANGE i i MEDIUMINT UNSIGNED;
```

为什么在使用 **CHANGE** 的命令中列名被命名了两次？因为 **CHANGE** 能做而 **MODIFY** 不能做的一件事是在更改类型的同时重命名列。如果你想在更改类型的同时将 i 重命名为 k，你可以这样做：

```sql
ALTER TABLE mytbl CHANGE i k MEDIUMINT UNSIGNED;
```

