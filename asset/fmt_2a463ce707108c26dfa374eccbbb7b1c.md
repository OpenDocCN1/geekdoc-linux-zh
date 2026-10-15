
此命令调用 DBI 系统连接名为 `tv` 的 MySQL 数据库，使用用户名和密码。

`connect()` 的返回值是一个 DBI 对象（称为数据库句柄），你用它发送 SQL 语句。对象的附加方法用于发送辅助接口、创建多行查询以及从数据库接收和提取信息。

连接是持久的——在关闭它或脚本终止之前，你可以在脚本中使用该句柄。因此，建议在脚本中使用全局变量；或者如果你正在为数据库构建辅助接口，最好将数据库句柄整合到你的对象中。

要关闭连接，你在数据库句柄上使用 `disconnect()` 方法：

```
$dbh->disconnect();
```

## SQL 指南

在继续之前，让我们看看 SQL 语言的基础知识，以便你了解如何编写请求或更新信息的简单查询。

### SELECT、INSERT、UPDATE 和 DELETE 语句的语法

基本上，可以在 SQL 数据库上执行四种主要的 SQL 语句：`SELECT`、`INSERT`、`UPDATE` 和 `DELETE`。你还会使用第五种语句，

`CREATE` 用于在课程数据库中创建新对象（表和索引），在大多数情况下，你只会使用一次 `CREATE`。

### SELECT

当你想要从数据库中提取信息时，可以使用 `SELECT` 语句。`SELECT` 语句从数据库中检索一组行和列，并返回一个数据集。

`SELECT` 语句的基本格式如下：

```sql
SELECT field [, field, ...]
FROM table
WHERE condition
ORDER BY field [ASC|DESC] [, field [ASC|DESC]]
```

`field` 是你想要从表中选择的字段名称的名称（或多个字段名称）。由于 `SELECT` 语句允许你指定想要从表中提取的单个字段，因此你可以避免许多通常与从数据库提取数据相关的问题。你不需要手动忽略不想访问的字段，只需只选择你需要的字段即可。你也可以使用星号 `*` 作为字段名来选择表中的所有字段。

`WHERE` 条件允许你指定提取行时的条件。例如，要从缩写字数据库中提取一个特定的缩写，你可能会使用：

```
SELECT Acronym FROM Acronyms WHERE Acronym = 'AAMOF'
```

`ORDER BY` 子句指定了用于排序信息的字段。你可以选择 `ASC`（升序）或 `DESC`（降序）排序。

### INSERT

`INSERT` 语句向表中添加一行信息。`INSERT` 语句具有以下语法：

```sql
INSERT INTO table
[(column, column ] ... ])
VALUES (value [, value ... ])
```

`table` 是将插入数据的表的名称，`column` 和 `value` 是你想要插入表中的字段名和对应值。字段名和值应该（显而易见）相匹配，以确保信息正确插入。

另一种，如果你正在向所有字段插入数据，可以省略字段名列表。

例如，要向缩写字数据库中添加一条新记录，你可能会使用以下 SQL 语句：

```
INSERT INTO Acronyms (Acronym, Expansion)
VALUES ('PDQ', 'Pretty Darn Quick')
```

由于你在两个列中创建创建条目，你可以简化语句：

```
INSERT INTO Acronyms VALUES ('PDQ', 'Pretty Darn Quick')
```

### UPDATE

`UPDATE` 语句更新表中一或多行的信息。`UPDATE` 语句的语法为：

```sql
UPDATE table
SET column=value
[, column=value ...]
[WHERE condition]
```

`table` 是数据库中的表名。`column` 和 `value` 是你想要赋值给这些列的列名和值。如果包含了 `WHERE` 关键字，则语句仅更新符合条件的列。该条件使用与 `SELECT` 语句相同的运算符和语法。注意，如果条件匹配多行，所有行都将用给定信息进行更新。

例如，你可以如下所示修改缩写字数据库中的 `IIRC` 条目：

```
UPDATE Acronyms Expansion='If I Recall Correctly'
WHERE Acronym='IIRC'
```

注意，此语句更新了表中的所有 `IIRC` 条目。你可以提供更具体的语句来确保更新了正确的行：

```
UPDATE Acronyms SET Expansion='If I Recall Correctly'
WHERE Acronym='IIRC' AND Expansion='If I Remember Correctly'
```

### DELETE

`DELETE` 语句与 `SELECT` 语句基本相同，不同之处它不是从表中返回匹配的行列表，而是从数据库中删除这些行：

```
DELETE [FROM] table [WHERE condition]
```

`table` 是你想要从中删除行的表名，`condition` 是用于查找要删除行的表达式。在某些数据库驱动中，`FROM` 关键字是可选的；请检查文档获取更多信息。

例如，你可以如下从缩写字表中删除所有 `IIRC` 条目：

```
DELETE FROM Aconyms WHERE Acronym = 'IIRC'
```

你也可以通过省略搜索条件来删除表中的所有行：

```
DELETE FROM Aconyms
```

### CREATE

如果你正在开发数据库系统，偶尔你需要在 Perl 中务实地构建你的表。创建数据库的一个主要优点是，你可以将应用程序传输到另一台机器，并让脚本创建运行所需的表。并不是所有的数据库都支持创建数据库表。许多数据库对 `CREATE` 语句的操作有约束或限制。

`CREATE` 语句的基本格式如下：

```sql
CREATE TABLE table
(field type[(size)]
, field type[(size)]...)
```

`table` 是要创建的表名。`field` 是要在表中创建的字段名，`type` 和 `size` 定义了字段的类型和宽度。

有效类型取决于你使用的底层数据库，但某些通用类型在大多数系统中都有效。表 17.1 列出了大多数驱动程序应该翻译为本地格式的基础类型。

#### 表 17.1 基础 SQL 字段类型

| DATA TYPE | SIZE SPECIFICATION | DESCRIPTION |
|---|---|---|
| Char (char or varchar) | (x) | 简单的字符字段。宽度由 x 的值决定。 |
| Integer (int) | N/A | 整数字段，可以是正数或负数。 |

#### 表 17.1 续：基础 SQL 字段类型

| DATA TYPE | SIZE SPECIFICATION | DESCRIPTION |
| --- | --- | --- |
| Decimal (real) | (x) | 小进制数字字段。 |
| Date (date) | N/A | 日期字段。 |
| Logical | N/A | 真/假值字段。 |
| binary | x | 二进制数据字段。 |
| text | x | 长字符串字段。 |
| blob | x | 大二进制对象字段。 |

### 执行扩展查询

`SELECT` 语句从数据库中检索信息。你需要使用 DBI 提供的方法从数据库中传输信息。

你首先定义要在数据库上运行的查询，并准备一个选择句柄。这是一个用于访问语句返回的行的新对象。然后你可以对语句调用 `execute()`，将查询发送到数据库。例如：

```
$my($sth) = $dbh->prepare("select * from tv \n  where title like \n  $dbh->quote($title)");
```

```
$sth->execute();
```

要访问查询返回的信息，你可以在 while 循环中调用 fetch 函数来提取查询的每行信息。例如：

```
while($my $row = $sth->fetch_hashref())
```

`fetch_hashref` 方法可能是实用的，因为它以哈希的形式的形式行。每个键都是返回列的名称，对应的值是字段的值。例如，你可以如下提取日期和时间：

```
$date = $row->{date};\n$time = $row->{time};
```

其他方法包括按 `SELECT` 语句中指定的顺序返回字段数组的 `fetch_array()`，以及基于相同的方式返回数组引用的。

读取完所有行后，必须在选择对象上调用 `finish()` 以完成序列并释放查询系统。

### 错误消息

所有函数都可以根据操作的成功与否返回真假值。你可以通过访问数据库句柄上的 `errstr()` 方法来提取操作返回的错误消息。例如：
