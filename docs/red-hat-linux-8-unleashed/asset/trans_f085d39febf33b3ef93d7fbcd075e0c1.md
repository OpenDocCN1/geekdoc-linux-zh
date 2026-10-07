

# 第 17 章在 Red Hat Linux 中管理数据库服务

然而，作为一名 DBA，即使你不会亲自进行任何实际编程工作，也应该理解 SQL 的基础知识。幸运的是，SQL 与标准英语非常相似，学习基础非常简单。

> 提示
> 下面的章节并不打算作为 SQL 教程。它们的目的仅仅是向你介绍该语言的基础知识。如果你需要完整的 SQL 编程教程，请查阅关于该主题的几本书中的一本，包括 MySQL (New Riders Publishing)、Sams Teach Yourself MySQL in 21 Days (Sams Publishing) 以及 PostgreSQL (Sams Publishing)。

# 创建表

如前所述，RDBMS（关系型数据库管理系统）将数据存储在类似于电子表格的表中。当然，在向数据库中存储任何数据之前，你需要创建所需的表和列来存储数据。你通过使用 `CREATE` 语句来实现这一点。

例如，图 17.2 中的 `serengeti_mammal` 表有六列字段分别是：`common_name`（通用名称）、`order`（目）、`family`（科）、`genus`（属）、`species`（种）和 `sub_species`（亚种）。

SQL 提供了几种列类型来定义列中将存储什么类型的数据。可用类型包括 `INT`、`FLOAT`、`CHAR` 和 `VARCHAR`。`CHAR` 和 `VARCHAR` 的区别在于前者持有固定长度字符串，而后者持有变长度字符串。

还有一些特殊的列类型，例如 `DATE`，它只接受日期格式的数据；以及 `ENUM`（枚举），用于指定只允许某些值。（例如，如果你想在数据库中记录动物的性别，可以使用一个接受 M 和 F 值的 `ENUM` 列。你将在本章稍后学习更多关于 `ENUM` 的知识。）

查看 `serengeti_mammal` 表，你可以发现所有列都包含字符数据。此外，这些字符字符串是变长度的。根据这些信息，你可以判断出所有列的最佳类型是 `VARCHAR`。你还应该注意到 `serengeti_mammal` 表的另一点：除了最后一列（`sub_species`）外，表中的所有列都需要一个值。表中的并不是所有动物都有亚种分类，因此最后一列可以留空。这两个事实在你设置表时将非常重要。

你现在准备好创建表了。如之前所述，你使用的 `CREATE` 语句使用以下语法：

```
CREATE TABLE table_name (column_name column_type(parameters) options, ...);
```

关于 `CREATE` 语句，你应该了解以下内容：

- SQL 命令不区分大小写。例如，`CREATE TABLE`、`create table` 和 `Create Table` 都是有效的。养成以后全大写命令的习惯是个好主，当你开始用 C、Perl 等语言为数据库编写前端时，使用全大写会更容易识别出 SQL 代码。（C、Perl 等语言中的关键字几乎全都是小写的）。

- 空格通常会被忽略。稍后当你为 `serengeti_mammal` 数据库创建表时，你会看到这个例子。

下面的示例显示了如何为 `serengeti_mammal` 数据库创建表：

```
CREATE TABLE serengeti_mammal
commonname VARCHAR(25) NOT NULL,
torder VARCHAR(20) NOT NULL,
family VARCHAR(20) NOT NULL,
genus VARCHAR(20) NOT NULL,
species VARCHAR(20) NOT NULL,
subspecies VARCHAR(20) NULL
);
```

注意该语句以分号结束。这是 SQL 知道你已完成语句中所有输入的方式。（在某些情况下，可以省略分号。本章会在出现这些情况时指出它们。）

> 注意，对于包含“目”信息的列，你使用了 `order` 而不不仅仅是 `order`。因为 `order` 是 PostgreSQL 中的保留关键字，不能用列名，你只需要在前面加一个 `t`（或任何其他字母）使其成为有效的列名。（在 MySQL 中，`order` 不是保留关键字，可以作为列名使用。）

# 向表中插入数据

创建表后，你就可以将数据放入表中。使用以下语法：

```
INSERT INTO table_name VALUES('value1', 'value2', 'value3', ...);
```

该语句将 `value1`、`value2` 等值插入到表 `table_name` 中。插入的值构成了数据库中的一行（或一条记录）。除非另有说明，否则值的插入顺序与数据库表中列列出的顺序相同。如果由于某种原因，你想以不同的顺序插入值（或者如果你只想插入几个值且它们不是连续的），你可以使用以下语法指定数据要进入哪些列：

```
INSERT table_name (column1,column4) VALUES('value1', 'value2');
```

你还可以使用单个 `INSERT` 语句填充多行，使用如下所示语法：

```
INSERT INTO table_name VALUES('value1', 'value2'),('value3', 'value4');
```

在该语句中，`value1` 和 `value2` 被插入到第一行，`value3` 和 `value4` 被插入到第二行。

下面的示例显示了你如何向 `serengeti_mammal` 数据库插入非洲狮的条目：

```
INSERT INTO serengeti_mammal VALUES('African Lion', 'Carnivora', 'Felidae', 'Panthera', 'leo', NULL);
```

如果你不想包含亚种，MySQL 要求最后一列（`sub_species`）必须为 `NULL` 值。另一方面，PostgreSQL 允许你直接省略最后一列。当然，如果你中间的某些列是空的，那么你需要在 `INSERT` 语句中显式声明 `NULL`。

通常情况下，`INSERT` 语句被编码到前端程序中，这样向数据库添加数据的用户就不必担心涉及的 SQL 语句。

# 从数据库中检索数据

当然，在数据库中存储数据的主要目的是为了以后能够对这些数据进行查询、排序和生成报告。基础检索通过 `SELECT` 语句完成，其语法如下：

```
SELECT column(s) FROM table_name WHERE search_criteria;
```

语句的前两个部分——`SELECT` 部分和 `FROM` 部分是必须的。语句的 `WHERE` 部分是可选的。如果省略，将返回表 `table_name` 中的所有行。

`column(s)` 表示你想查看的列名。如果你想查看多个列，可以用逗号将它们列出来。如果你想查看所有列，也可以使用通配符 `*` 来显示匹配搜索条件的所有列。例如，以下语句将显示匹配搜索条件的所有列：

```
SELECT * FROM serengeti_mammal;
```

# 基础知识简要回顾

如果你想查看 `serengeti_mammal` 数据库中的通用名称，可以使用如下语句：

```
SELECT common_name FROM serengeti_mammal;
```

如果你想查看动物的目和种，可以使用以下语句：

```
SELECT genus,species FROM serengeti_mammal;
```

然而，这不会产生你期望的格式。在陈述物学名称时，目和种总是列在一起。MySQL 和 PostgreSQL 都提供了字符串连接函数来处理此类问题。在 MySQL 中，你可以使用 `CONCAT` 函数将 `genus` 和 `species` 合并为一个列。示例如下：

```
SELECT CONCAT(genus, ' ', species) AS Scientific_Name FROM serengeti_mammal;
```

该语句在一个名为 `Scientific_Name` 的列下列出目和种。`genus` 和 `species` 之间的空引号插入了一个空格。如果没有它，它们将连在一起，这不是你想要的。

在 PostgreSQL 中，字符串连接简单地使用双竖线 `||`。以下命令是上述 MySQL 命令的等效写法：

```
SELECT (genus'||species) AS Scientific_Name FROM serengeti_mammal;
```

注意括号是可选的，但它们让语句更易读。再次，中间的单引号（引号之间的空格）用于在目和种名称之间插入一个空格。如果没有它们，这两个值将连成单词，那不是你想要的。

当然，通常情况下，你并不想要数据库中每一行的列表。而是只想找到符合特定的行。为了这一点，我们在 `SELECT` 语句中添加 `WHERE` 语句。例如，假设你想找到 `serengeti_mammal` 表中所有肉食目的动物。你可以使用如下语句：

```
SELECT * FROM serengeti_mammal WHERE order='Carnivore';
```

