
`CREATE TABLE table_name (column_name column_type(parameters) options, ...);`

你应该了解关于 `CREATE` 语句的以下内容：

- SQL 命令不区分大小写——例如，`CREATE TABLE`、`create table` 和 `Create Table` 都是有效的。
- 空格符通常会被忽略——这意味着你应该使用它来让你的 SQL 命令更加清晰。

以下示例展示了如何为 `cd_collection` 数据库创建表：

```
CREATE TABLE cd_collection (
  id INT NOT NULL,
  title VARCHAR(50) NOT NULL,
  artist VARCHAR(50) NOT NULL,
  year VARCHAR(50) NOT NULL,
  rating VARCHAR(50) NULL
);
```

注意，语句以分号 (`;`) 结束。这是 SQL 能够知道你已完成语句中的所有条目的。在某些情况下，你可以省略分号，我们会在这些情况出现时指出。

| TIP | SQL 有许多不能在表名或字段名使用的保留关键字。例如，如果你在跟踪 CD，你可能想度假时带上它们，你将无法使用 `select` 作为字段名，因为它是保留关键字。相反，你应该选择另一个名称（如 `selected?`）或在字段名前加上前缀 `f`，例如 `fselect`。 |

# 向表中插入数据

创建表后，你可以向它们放入数据。你可以使用 `INSERT` 语句手动插入数据，其语法如下：

```
INSERT INTO table_name VALUES('value1', 'value2', 'value3', ...);
```

该语句将 `value1`、`value2` 等插入到表 `table_name` 中。插入的值构成了表中的一行（或一条记录）。另有说明，否则值是按照数据库表中列列出的顺序进行插入的。如果由于某种原因，你想以不同的顺序插入值（或者只想插入少数值且不是连续顺序的），你可以使用以下语法指定你想让数据进入哪些列：

```
INSERT INTO table_name (column1,column4) VALUES ('value1', 'value2');
```

你还可以使用单个 `INSERT` 语句填充多行，语法如下所示：

```
INSERT INTO table_name VALUES ('value1', 'value2'), ('value3', 'value4');
```

在该语句中，`value1` 和 `value2` 被插入第一行，`value3` 和 `value4` 被插入到第二行。

以下示例展示了如何向 `cd_collection` 表插入 `Nevermind` 条目：

```
INSERT INTO cd_collection VALUES (9, 'Nevermind', 'Nirvana', '1991', NULL);
```

如果你不想包含评分，MySQL 要求最后一列（rating）为 `NULL` 值。相比之下，PostgreSQL 只需要省略最后一列即可。如果你中间的列为空，你需要在 `INSERT` 语句中显式声明 `NULL`。

通常，`INSERT` 语句被编码在前端程序中，因此向数据库添加数据的用户不需要担心涉及的 SQL 语句。

# 从数据库检索数据

当然，在数据库中存储数据的主要目的是为了以后对数据进行查询、排序和生成报告。基本的数据检索通过 `SELECT` 语句完成，其语法如下：

```
SELECT column1, column2, column3 FROM table_name WHERE search_criteria;
```

语句的前两个部分——`SELECT` 部分和 `FROM` 部分是必须的。语句的 `WHERE` 部分是可选的。如果省略，将返回表 `table_name` 中的所有行。

`column1,column2,column3` 语法表示你想查看的列名。如果你想查看所有列，也可以使用通配符 `*` 来显示匹配搜索条件的所有列。例如，以下语句显示了 `cd_collection` 表中的所有列：

```
SELECT * FROM cd_collection;
```

如果你只想查看表中所有 CD 的标题，你可以使用如下的语句：

```
SELECT title FROM cd_collection;
```

# 数据库基础简述

为了选择 CD 的标题和年份，你使用以下操作：

```
SELECT title, year FROM cd_collection;
```

如果你想做得更花哨一点，可以使用 SQL 打印 CD 标题，后面紧跟括号内的年份，这是惯常做法。然而，MySQL 和 PostgreSQL 提供了字符串连接函数来处理此类问题。在两个系统中。

在 MySQL 中，你可以使用 `CONCAT()` 函数将标题和年份列合并为一个带括号的输出列。以下语句即为示例：

```
SELECT CONCAT(title,' (',year,')') AS TitleYear FROM cd_collection
```

该语句在一个标记为 `TitleYear` 的列下同时列出标题和年份。注意，`CONCAT()` 函数中字段之外还有两个字符串；这些添加了空格和括号。

在 PostgreSQL 中，字符串连接函数简单地使用双竖线 (`||`)。以下命令是上述 MySQL 命令的 PostgreSQL 等效写法：

```
SELECT (title||' ('||year||')') AS TitleYear FROM cd_collection
```

为了选择 CD 的标题和年份，你使用以下操作：

```
SELECT title, year FROM cd_collection;
```
