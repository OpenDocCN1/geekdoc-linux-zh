
`CREATE table_name (column_name column_type(parameters) options, ...);`

你应该了解关于 `CREATE` 语句的以下内容：

- SQL 命令不区分大小写——例如，`CREATE TABLE`、`create table` 和 `Create Table` 都是有效的。
- 空格通常会被忽略——这意味着你应该使用空格来让你的 SQL 命令更清晰。

以下示例展示了如何为 `cd_collection` 数据库创建表：

```
CREATE TABLE cd_collection

(

id INT NOT NULL,

title VARCHAR(50) NOT NULL,

artist VARCHAR(50) NOT NULL,

year VARCHAR(50) NOT NULL,

rating VARCHAR(50) NOT NULL

);
```

注意该语句以分号结束。这是 SQL 借此知道你已经完成了语句中所有条目的方式。在某些情况下，分号可以省略，我们会在这些情况出现时指出。

> 提示：SQL 有许多保留关键字，不能用作表名或字段名。例如，如果你在跟踪想要去度假时携带的 CD，你将无法使用 `select` 作为字段名，因为它是一个保留关键字。相反，你应该选择一个不同的名称（如 `selected?`）或直接在字段名前加上前缀 `f`，例如 `fselect`。

## 向表中插入数据

创建表后，你就可以将数据放入其中。你可以使用 `INSERT` 语句手动插入数据，其语法如下：

```
INSERT table_name VALUES('value1', 'value2', 'value3', ...);
```

该语句将 `value1`、`value2` 等插入到 `table_name` 表中。插入的值构成了数据库中的一行（或一条记录）。除非另有说明，否则值是按照数据库表中列出的列顺序插入的。如果由于某种原因，你想以不同的顺序插入值（或者如果你只想插入几个值且它们不是连续顺序），你可以通过以下语法指定数据要存入列：

```
INSERT table_name (column1,column4) VALUES('value1', 'value2');
```

你还可以用一个 `INSERT` 语句填充多行，其后续可能如下：

```
INSERT table_name VALUES('value1', 'value2'),('value3', 'value4');
```

在该语句中，`value1` 和 `value2` 被插入到第一行，`value3` 和 `value4` 被插入到第二行。

以下示例展示了你如何向 `cd_collection` 插入 `Nevermind` 条目：

```
INSERT cd_collection VALUES(9, 'Nevermind', 'Nirvana', '1991', NULL);
```

如果你不想包含评分，MySQL 要求最后一列（`rating`）必须为 `NULL` 值。相反，PostgreSQL 允许你省略最后一列。然而，如果你中间的列是空，你需要在 `INSERT` 语句中显式声明 `NULL`。

通常，`INSERT` 语句被编码在前端程序中，这样向数据库添加数据的用户就不必担心涉及的 SQL 语句。

## 从数据库检索数据

当然，在数据库中存储数据的主要目的是之后可以对这些数据进行查询、排序并生成报告。基础的数据检索通过 `SELECT` 语句完成，其语法如下：

```
SELECT column1, column2,column3 FROM table_name WHERE search_criteria;
```

语句的前两个部分——`SELECT` 和 `FROM` 部分是必须的。语句的 `WHERE` 部分是可选的。如果省略，将返回 `table_name` 表中的所有行。

`column1`、`column2`、`column3` 表示你想查看的列名。如果你想查看所有列，也可以使用通配符 `*` 来显示匹配搜索条件的所有列。例如，以下语句显示 `cd_collection` 表中的所有列：

```
SELECT * FROM cd_collection;
```

如果你只想查看表中所有 CD 的标题，你将使用如下的语句：

```
SELECT title FROM cd_collection;
```

要选择 CD 的标题和年份，你将使用以下语句：

```
SELECT title, year FROM cd_collection;
```
