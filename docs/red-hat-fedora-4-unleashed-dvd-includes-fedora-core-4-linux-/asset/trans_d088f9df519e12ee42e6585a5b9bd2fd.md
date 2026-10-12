

# 客户

| cid | 姓氏 | 名字 | 收货地址 |
|---|---|---|---|
| 1 | Doe | John | 505 Somestreet |
| 2 | Doe | Jane | 505 Somestreet |
| 3 | Palmer | John | 200 Anystreet |
| 4 | Johnson | Richard | 1000 Another Street |

# 订单

| cid | 订单号 | 库存号 | 优先级 | 已发货 | 日期 |
|---|---|---|---|---|---|
| 1 | 1002 | 100,252,342 | 3 | Y | 8/31/01 |
| 1 | 1221 | 200,352 | 1 | N | 10/2/01 |
| 3 | 1223 | 200,121 | 2 | Y | 10/2/01 |
| 2 | 1225 | 221,152 | 1 | N | 10/3/01 |

# 逾期

| cid | 订单号 | 逾期天数 | 措施 |
|---|---|---|---|
| 1 | 1002 | 32 | 已发送信函 |

![](img/774d40fd20903495c5cd00e2efad3f33_594_0.png)

现在，您已经了解了数据在关系型数据库管理系统（RDBMS）中的存储方式，以及 RDBMS 的结构如何支持您对数据进行处理，这就为您学习如何从数据库中读写数据做好了准备。这正是 SQL 发挥作用的地方。

## 了解 SQL 基础

SQL（读音可以是“S-Q-L”，也可以是“se-quel”）是一种数据库查询语言，几乎市面上所有的 RDBMS 都能理解它。您使用 SQL 语句将数据存入数据库，并从数据库中检索数据。与任何语言中的语句一样，SQL 语句具有定义明确的结构，以确定其含义和功能。

在大多数应用场景中，SQL 被编写在前端或中间件应用程序中，最终用户通常不会直接操作它们。因此，大多数最终用户对 SQL 及其作用并不知情，也没有太多理由去关心 SQL 语句的结构。

然而，作为一名数据库管理员（DBA），即使您不亲自进行实际的编程工作，也应该了解 SQL 的基础知识。幸运的是，SQL 与普通英语相似，因此学习其基础很简单。

> **提示**
> 接下来的几节内容并不旨在成为 SQL 的教程。它们仅仅是为了向您介绍该语言的基础知识。如果您需要一份完整的 SQL 编程教程，请查阅关于此主题的几本现有书籍，包括 *MySQL*、*Sams Teach Yourself MySQL in 21 Days* 和 *PostgreSQL*（均由 Sams Publishing 出版）。

## 创建表

如前所述，RDBMS 将数据存储在与电子表格相似的表中。当然，在您向数据库中存储任何数据之前，您需要创建必要的表和列来存储数据。您通过使用 CREATE 语句来完成此操作。

例如，图 20.2 中的 cd_collection 表有五个列（或字段）：id、title、artist、year 和 rating。

SQL 提供了多种用于定义列中将存储何种数据的列类型。一些可用的类型包括 INT、FLOAT、CHAR 和 VARCHAR。CHAR 和 VARCHAR 都存储文本字符串，区别在于 CHAR 存储固定长度的字符串，而 VARCHAR 存储可变长度的字符串。

还有一些特殊的列类型，例如 DATE，只接受日期格式的数据，以及 ENUM（枚举），可用于指定只允许某些值。例如，如果您想要记录 CD 的流派，可以使用一个只接受 POP、ROCK、EASY_LISTENING 等值的 ENUM 列。您将在本章后续部分进一步了解 ENUM。

观察 cd_collection 表，您可以看到其中三列存储数值数据，另外两列存储字符串数据。此外，这些字符串是可变长度的。根据这些信息，您可以判断出最适合文本列的类型是 VARCHAR，而其他列的最佳类型是 INT。您还应该注意到 cd_collection 表中的另一件事：其中一张 CD 缺少评分，也许是因为我们尚未收听过它。因此，这个值是可选的；它最初为空，以后可以填入。

现在您可以创建表了。如前所述，您通过使用 CREATE 语句来完成此操作，其语法如下：

```
CREATE TABLE table_name (column_name column_type(parameters) options, ...);
```

您应该了解关于 CREATE 语句的以下事项：

- **SQL 命令不区分大小写**——例如，CREATE TABLE、create table 和 create Table 都是有效的。您应该养成使用全大写命令的习惯，因为稍后当您开始用 C、Perl 等语言为数据库编写前端时，使用全大写将使您更容易识别出 SQL 代码。（C、Perl 等语言中的关键字几乎总是小写的。）
- **空白字符通常被忽略**——这意味着您应该使用它们来使您的 SQL 命令更清晰。

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

请注意，该语句以分号结束。这是 SQL 知道您已完成该语句中所有条目的方式。在某些情况下，可以省略分号，当出现这种情况时，我们会指出。

> **提示**
> SQL 拥有大量保留关键字，不能用作表名或字段名。例如，如果您记录想要在度假时携带的 CD，您将无法使用字段名 select，因为 select 是保留关键字。相反，您应该选择其他名称（selected2?）或者在字段名前加一个 f，例如 fselect。

## 向表中插入数据

创建表后，您可以向其中放入数据。您可以使用 INSERT 语句手动插入数据，其语法如下：

```
INSERT INTO table_name VALUES('value1', 'value2', 'value3', ...);
```

该语句将 *value1*、*value2* 等插入到表 *table_name* 中。插入的值构成数据库中的一行，即一条*记录*。除非另有说明，否则值将按照数据库表中列出的顺序插入。如果出于某种原因，您希望以不同的顺序插入值（或者您只希望插入少数几个值且它们不是按顺序的），您可以通过使用以下语法来指定您希望数据进入哪些列：

```
INSERT INTO table_name (column1, column4) VALUES('value1', 'value2');
```

您还可以使用单个 INSERT 语句填充多行，使用类似以下的语法：

```
INSERT INTO table_name VALUES('value1', 'value2'), ('value3', 'value4');
```

在该语句中，*value1* 和 *value2* 被插入到第一行，而 *value3* 和 *value4* 被插入到第二行。

以下示例展示了如何向 *cd_collection* 表中插入 Nevermind 条目：

```
INSERT INTO cd_collection VALUES(9, 'Nevermind', 'Nirvana', '1991', 'NULL');
```

如果您不想包含评分，MySQL 要求最后一列（rating）使用 `NULL` 值。另一方面，PostgreSQL 允许您直接省略最后一列。当然，如果中间的列是空的，您需要在 `INSERT` 语句中明确说明 `NULL`。

通常，`INSERT` 语句会被编码到前端程序中，这样向数据库添加数据的用户就不必担心所涉及的 SQL 语句。

## 从数据库中检索数据

当然，将数据存储在数据库中的主要原因就是以便后续查找、排序并生成关于该数据的报告。基本的数据检索是使用 `SELECT` 语句完成的，其语法如下：

```
SELECT column1, column2, column3 FROM table_name WHERE search_criteria;
```

该语句的前两部分——`SELECT` 和 `FROM` 部分——是必需的。语句中的 `WHERE` 部分是可选的。如果省略它，将返回表 *table_name* 中的所有行。

`column1`、`column2`、`column3` 指示您想要查看的列的名称。如果您想查看所有列，也可以使用通配符 `*` 来显示所有符合搜索条件的列。例如，以下语句显示 `cd_collection` 表中的所有列：

```
SELECT * FROM cd_collection;
```

如果您只想查看表中所有 CD 的标题，您可以使用如下的语句：

```
SELECT title FROM cd_collection;
```

要选择 CD 的标题和年份，您可以使用以下语句：

```
SELECT title, year FROM cd_collection;
```

如果您想要更花哨一点，可以使用 SQL 打印 CD 标题，后面跟着括号内的年份，这符合惯例。MySQL 和 PostgreSQL 都提供字符串连接函数来处理此类问题。然而，这两个系统的语法不同。

在 MySQL 中，您可以使用 `CONCAT()` 函数将标题和年份列结合为一个输出列，并加上括号。以下是一个示例语句：

```
SELECT CONCAT(title, " (", year, ")") AS TitleYear FROM cd_collection;
```

该语句在具有标签 `TitleYear` 的一个列下同时列出标题和年份。请注意，`CONCAT()` 函数中除了字段外还有两个字符串——这些添加了空格和括号。

