

你可以通过几种方式执行此语句。你可以手动输入它，或者使用 sampDB 发行版中 create_president.sql 文件包含的预编写语句。

如果你想手动输入该语句，请调用 mysql，并将 sampDB 设为默认数据库：

```
% mysql sampDB
```

然后输入上面显示的 CREATE TABLE 语句，包括末尾的分号，以便 mysql 能知道语句在哪里结束。缩进无关紧要，你也不必在相同位置换行。例如，如果你想的话，可以将该语句作为一行长行输入。

若要使用预编写的描述来创建 president 表，请使用 sampDB 发行版中的 create_president.sql 文件。该文件位于解压缩发行版时创建的 sampDB 目录中。更改位置至该目录，然后运行以下命令：

```
% mysql sampDB < create_prescent.sql
```

无论你以何种方式调用 mysql，如果命令名称后需要任何连接参数（主机名、用户名或密码），请将其指定在命令行上。

现在让我们更仔细地看看 CREATE TABLE 语句。该语句中的每个列规范由列名、数据类型（列将保存的值类型）以及可能的某些列属性组成。

president 表中使用的两种数据类型是 VARCHAR 和 DATE。VARCHAR(n) 表示该列包含变长字符值，最大长度为每个 n 个字符。也就是说，它们包含大小可能不同的字符串，但长度有上限。你根据预期值的长度来选择 n 的值。state 定义为 VARCHAR(2)；用两个字符的缩写输入州名只需要这么多。其他字符串值列需要更宽以容纳更长的值。

我们使用的另一种数据类型是 DATE。不出所料，该类型表示列保存日期值。然而，可能会让你惊讶的是日期的表示格式。MySQL 期望日期以 'CCYY-MM-DD' 格式编写，其中 CC、YY、MM 和 DD 分别代表世纪、世纪内的年份、月份和月份中的日期。这是 SQL 日期表示标准（也称为 "ISO 8601 格式"）。例如，要在 MySQL 中指定 "2005 年 7 月 18 日" 的日期，你使用 '2005-07-18'，而不是 '07-18-2005' 或 '18-07-2005'。

我们在 president 表的列中使用的唯一属性是 NULL（值可以缺失）和 NOT NULL（值必须填充）。大多数列是 NOT NULL，因为我们总是要求它们有值。可以具有 NULL 值的两个列是 suffix（大多数名字没有后缀）和 death（对于在世总统，没有死亡日期）。

对于 `member` 表，`CREATE TABLE` 语句如下所示：

```
CREATE TABLE member
(
  member_id   INT UNSIGNED NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (member_id),
  last_name   VARCHAR(20) NOT NULL,
  first_name  VARCHAR(20) NOT NULL,
  suffix      VARCHAR(5) NULL,
  expiration  DATE NULL,
  email       VARCHAR(100) NULL,
  street      VARCHAR(50) NULL,
  city        VARCHAR(50) NULL,
  state       VARCHAR(2) NULL,
  zip         VARCHAR(10) NULL,
  phone       VARCHAR(20) NULL,
  interests   VARCHAR(255) NULL
);
```

同样，你可以手动将该语句输入 *mysql*，或者使用预编写的文件。`sampdb` 发行版中包含 `member` 表的 `CREATE TABLE` 语句的文件是 `create_member.sql`。要使用它，执行此命令：

```
% mysql sampdb < create_member.sql
```

就数据类型而言，`member` 表的大多数列除了两列之外并不特别有趣，因为它们被创建为变长字符串。例外是 `member_id` 和 `expiration`，它们分别用于保存序列号和日期。

`member_id` 会员号列的主要考虑因素是，每个值都应该是唯一的，以避免成员之间的混淆。在这里，`AUTO_INCREMENT` 列很有用，因为这样我们可以让 MySQL 在添加新成员时自动为我们生成唯一的数字。尽管它只包含数字，但 `member_id` 的定义有几个部分：

- `INT` 表示该列保存整数（没有小数部分的数值）。
- `UNSIGNED` 不允许负值。
- `NOT NULL` 要求必须填充列值。这防止创建没有 ID 号的成员。
- `AUTO_INCREMENT` 是 MySQL 中的特殊属性。它表示该列保存序列号。`AUTO_INCREMENT` 机制的工作方式如下：如果你创建新的 `member` 表行时为 `member_id` 列不提供值，MySQL 会自动生成下一个序列号并将其分配给该列。如果你显式将值 `NULL` 分配给该列，也会发生这种特殊行为。`AUTO_INCREMENT` 功能使得为每个新成员分配唯一 ID 变得容易，因为 MySQL 为我们生成值。

`PRIMARY KEY` 子句表示 `member_id` 列被索引以允许快速查找。它还建立了该列中每个值必须唯一的约束。后者特性对于成员 ID 值是理想的，因为它防止我们错误地两次使用相同的 ID。此外，MySQL 要求每个 `AUTO_INCREMENT` 列必须具有某种索引，因此如果没有索引，表定义将是非法的。（任何 PRIMARY KEY 列还必须是 NOT NULL，因此如果我们从 `member_id` 定义中省略 NOT NULL，MySQL 会自动添加它。）

如果你不明白关于 `AUTO_INCREMENT` 和 PRIMARY KEY 的那些事情，只要把它们看作给我们一种魔术方法来生成带索引的 ID 号。只要每个成员的值都是唯一的，具体是什么并不特别重要。（当你准备好学习更多有关如何使用 `AUTO_INCREMENT` 列时，第 3 章 “数据类型” 将详细涵盖它们。）

*expiration* 列是一个 DATE。它允许空值，因此它的默认值也是 `NULL`。`NULL` 意味着没有输入日期。原因是，如前所述，我们使用 *expiration* 可以为 NULL 的约定来指示哪些成员拥有终身会员资格。

既然你已经告诉 MySQL 创建几个表，请检查它是否如你所愿那样做了。在 *mysql* 中，发出以下语句以查看 *president* 表的结构：

```
mysql> DESCRIBE president;
```

| 字段       | 类型         | 可空 | 键 | 默认值 | 额外 |
|------------|--------------|------|----|--------|------|
| last_name  | varchar(15)  | 否   |    |        |      |
| first_name | varchar(15)  | 否   |    |        |      |
| suffix     | varchar(5)   | 是   |    | NULL   |      |
| city       | varchar(20)  | 否   |    |        |      |
| state      | varchar(2)   | 否   |    |        |      |
| birth      | date         | 否   |    |        |      |
| death      | date         | 是   |    | NULL   |      |

如果你发出 `DESCRIBE` member 语句，*mysql* 将向你显示 member 表的类似信息。

当你忘记表中某列的名称，或需要了解其数据类型或宽度等时，`DESCRIBE` 很有用。它也有助于了解 MySQL 在表行中存储列的顺序。当你发出期望列值按默认列顺序列出的 `INSERT` 或 `LOAD DATA` 语句时，这种顺序很重要。

`DESCRIBE` 产生的信息可以通过不同方式获取。它可以缩写为 `DESC`，或者写成 `EXPLAIN` 或 `SHOW` 语句。以下语句是同义的：

```
DESCRIBE president;
DESC president;
EXPLAIN president;
SHOW COLUMNS FROM president;
SHOW FIELDS FROM president;
```

