
或许是因为我们还没有聆听它。因此，这个值是可选的；它初始为空，可以稍后填写。

你现在准备好创建表了。如前所述，你可以通过使用 CREATE 语句来完成，其语法如下：

```
CREATE TABLE table_name (column_name column_type(parameters) options, ...);
```

你应该了解 CREATE 语句的以下几点：

- **SQL 命令不区分大小写**——例如，CREATE TABLE、create table 和 Create Table 都是有效的。
- **空白通常会被忽略**——这意味着你应该使用它来使你的 SQL 命令更清晰。

以下示例展示了如何为 cd_collection 数据库创建表：

```
CREATE TABLE cd_collection
(
  id INT NOT NULL,
  title VARCHAR(50) NOT NULL,
  artist VARCHAR(50) NOT NULL,
  year VARCHAR(50) NOT NULL,
  rating VARCHAR(50) NULL
);
```

请注意，该语句以分号结尾。这就是 SQL 知道你已完成该语句中所有条目的方式。在某些情况下，可以省略分号，我们会在出现这些情况时指出。

## TIP

SQL 有许多保留关键字，不能用作表名或字段名。例如，如果你想跟踪你想在度假时带走的 CD，你将无法使用字段名 select，因为那是一个保留关键字。相反，你应该选择不同的名称（selected？）或只在字段名前加上 f，例如 fselect。

## Inserting Data into Tables

创建表后，你可以向其中插入数据。你可以使用 INSERT 语句手动插入数据，其语法如下：

```
INSERT INTO table_name VALUES('value1', 'value2', 'value3', ...);
```

该语句将 value1、value2 等插入到表 table_name 中。插入的值构成数据库中的一行，或记录。除非另有说明，否则值将按照数据库表中列出的列的顺序插入。如果出于某种原因，你想按不同的顺序插入（或如果你想插入

要选择 CD 的标题和年份，你可以使用以下语句：

```
SELECT title, year FROM cd_collection;
```

如果你想要更精致一点，你可以使用 SQL 将 CD 标题后跟年份用括号括起来，就像惯例一样。MySQL 和 PostgreSQL 都提供了字符串连接函数来处理此类问题。但是，两种系统的语法不同。

在 MySQL 中，你可以使用 CONCAT() 函数将 title 和 year 列合并为一个输出列，并加上括号。以下语句是一个示例：

```
SELECT CONCAT(title, ' (', year, ')') AS TitleYear FROM cd_collection;
```

该语句将标题和年份列在标记为 TitleYear 的一个列下。请注意，CONCAT() 函数中除了字段外还有两个字符串——这些用于添加空白和括号。

在 PostgreSQL 中，字符串连接函数只是双竖线（||）。以下命令是前面 MySQL 命令的 PostgreSQL 等价物：

```
SELECT (genus||' ('||species||')') AS TitleYear FROM cd_collection;
```

请注意，括号是可选的，但它们使语句更易于阅读。同样，中间和末尾的字符串（注意引号之间的空格）用于在标题和年份之间插入空格和括号。

当然，更多时候，你并不想要数据库中每一行的列表。相反，你只想找到符合某些特征的行。为此，你将 WHERE 语句添加到 SELECT 语句中。例如，假设你想找到 cd_collection 表中评分为 5 的所有 CD。你将使用如下语句：

```
SELECT * FROM cd_collection WHERE rating = 5;
```

使用图 21.2 中的表，你可以看到此查询将返回 Trouser Jazz、Life for Rent 和 The Two Towers 的行。这是一个简单的查询，SQL 能够处理比这更复杂的查询。复杂查询可以使用逻辑 AND 和逻辑 OR 语句编写。例如，假设你想细化查询，只列出那些未在 2003 年发行的 CD。你将使用如下查询：

```
SELECT * FROM cd_collection WHERE rating = 5 AND year != 2003;
```

在 SQL 中，!= 表示“不等于”。因此再次查看图 21.2 中的表，你可以看到此查询返回 Trouser Jazz 和 The Two Towers 的行，但不会返回 Life for Rent 的行，因为它是在 2003 年发行的。

