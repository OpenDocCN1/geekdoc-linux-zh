
SQL 提供了几种列类型用于数据，定义了将存储什么类型的数据。例如，`cd_collection` 表有五列，或字段：`id`、`title`、`artist`、`year` 和 `rating`。

- `CHAR`：固定长度字符串。
- `VARCHAR`：变长字符串。
- `TEXT`：长文本。
- `BLOB`：二进制大对象。
- `ENUM`：枚举类型。
- `JSON`：JSON 格式数据。
- `BIT`：位字段。
- `BOOLEAN`：布尔值（TRUE/FALSE）。

如果你认为 `sample_database` 示例中的 `phonebook` 表和 `cd_collection` 表之间没有逻辑关系，那么你是对的。在关系型数据库中，用户可以在单个数据库中存储多个数据表，即使一个表中的数据与其他表中的数据没有关联。

例如，假设你经营着一家销售小部件的小型公司，并拥有一个计算机化的客户数据库。除了存储每个客户的姓名、地址和电话号码外，你还希望查询任何客户的未结订单和发票信息。你可以使用 RDBMS 中的相关表来存储和组织这些客户数据。图 28.3 显示了此类数据库的示例。

customers

| cid | last_name | first_name | shipping_address |
|---|---|---|---|
| 1 | Doe | John | 505 Somerset |
| 2 | Doe | Jane | 505 Somerset |
| 3 | Palmer | John | 200 Anystreet |
| 4 | Johnson | Richard | 1000 Another Street |

orders

| cid | order_num | stock_num | priority | shipped | date |
|---|---|---|---|---|---|
| 1 | 1002 | 100,252 | | Y | 8/3/01 |
| | 121 | 200,352 | | N | 10/2/01 |
| 3 | 123 | 200,121 | | Y | 10/2/01 |
| 2 | 122 | 222,151 | | N | 10/3/01 |

overdue

| cid | order_num | days_overdue | action |
|---|---|---|---|
| 1 | 1002 | 32 | sent letter |

图 28.3 你可以使用三个相关表来跟踪客户、订单和未结发票。

在图 28.3 中，我们在每条客户记录中都添加了 `cid` 字段。该字段持有客户 ID 数字，它是用于链接每个客户所有信息以跟踪订单和发票的唯一数据项。每个客户都分配了一个唯一的 ID，其作用是：两个客户的姓名字段数据可能相同，但他们在 `orders` 和 `overdue` 表中的 ID 字段取代了 `customers` 表中的 `last_name`、`first_name` 和 `shipping_address` 字段信息。现在，当你想要查询任何客户的订单和发票数据时，你可以根据一个键进行搜索，而不是多个键。你可以在更快、更方便的数据搜索中获得更准确的结果。

现在你已经了解了数据如何在 RDBMS 中存储，以及 RDBMS 结构如何让你处理这些数据，你准备好学习如何从数据库进行输入和输出了。这就是 SQL 大显用场。

# 理解 SQL 基础

SQL（读作“S-Q-L”或“sequel”，取决于说话者）是一种几乎所有可用 RDBMS 都能理解的数据库查询语言。你使用 SQL 语句将数据存入数据库并从数据库检索数据。与任何语言中的语句一样，SQL 语句具有定义的结构，决定了它们的含义和功能。

作为 DBA，你应该理解 SQL 的基础知识，即使你亲自不进行任何实际编程。幸运的是，SQL 与标准英语相似，学习基础非常简单。

# 创建表

如前所述，RDBMS 将数据存储在类似于电子表格的表中。当然，在数据库中创建任何数据之前，你需要创建必要的表和列来存储数据。你可以使用 `CREATE` 语句来实现。

例如，图 28.2 中的 `cd_collection` 表有五列，或字段：`id`、`title`、`artist`、`year` 和 `rating`。

SQL 提供了几种列类型用于数据，定义了将存储什么类型的数据：

- `TINYINT`：极小整数。
- `SMALLINT`：小型整数。
- `INT`：整数。
- `BIGINT`：大整数。
- `DECIMAL(p,s)`：精确数值。
- `NUMERIC(p,s)`：与 DECIMAL 相同。
- `FLOAT`：单精度浮点数。
- `REAL`：单精度浮点数。
- `DATE`：日期（YYYY-MM-DD）。
- `DATETIME`：日期和时间（YYYY-MM-DD HH:MM:SS）。
- `TIMESTAMP`：时间戳，通常包含时区支持的日期和时间。
- `CHAR(n)`：固定长度字符串。
- `VARCHAR(n)`：变长字符串。
- `TEXT`：长文本。
- `BLOB`：二进制大对象。
- `ENUM`：枚举类型。
- `JSON`：JSON 格式数据。
- `BIT`：位字段。
- `BOOLEAN`：布尔值（TRUE/FALSE）。

# 数据库基础简述

该语句将标题和年份列在一个标记为 `TitleYear` 的列下。请注意，在 `CONCAT()` 函数中，字段之外有两个字符串；这些字符串添加了空格和括号。

在 PostgreSQL 中，字符串连接函数简单地用双竖线 (`||`)。下面的命令是前面 MySQL 命令的 PostgreSQL 等效命令：
