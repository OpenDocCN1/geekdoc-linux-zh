
## 确保数据库安全
为了确保数据库安全，你需要关注访问控制（确保只有授权的人员可以访问数据库）和权限（确保能够访问数据库的人不会执行不该做的事）。在本章中，你将学习如何管理安全外壳（SSH）以及访问数据库的本地图形用户界面（GUI）客户端。规划和监督组织数据库的定期备份以及从这些备份中恢复是确保数据库安全的另一项关键功能。

## 确保数据完整性
存储在服务器硬盘存储上的所有信息中，数据库中的信息变化最为关键。确保数据完整性涉及对多用户访问的规划，并确保当多个用户同时更改数据时，更改不会丢失或重复。

## 数据库基础简要回顾

使用本章讨论的 Linux 数据库服务基于客户端/服务器模型。数据库客户端通常用于输入数据和从服务器查询结果。你可以使用命令行或图形客户端访问运行中的服务器。数据库通常有两种形式：平文件和关系型。平级数据库可以像简单的文本文件，用空格、制表符或其他字符来分隔信息的各个部分。平级数据库可以是 `/etc/passwd` 这样的简单文件。另一个平级数据库的例子可能像这样：

Doe-John-505-Anytown-NY-12

你可以使用标准工具如 `grep`、`awk` 和 `perl` 来搜索并提取信息。平文件数据库在扩展性方面表现不佳——它们无法进行随机访问，只能进行顺序访问。这意味着随着数据量的增长，访问时间会增加，性能会下降。平文件对于多用户环境是不适用的——关系型系统（RDBMS）擅长发现各个数据片段之间的关系。

### NoSQL

对于我们所说的这一点有一个例外。现在使用的新数据库类别包括 Google BigTable、Cassandra、CouchDB、Redis 和 Memcached，这些被称为 NoSQL 数据库。这些数据库不使用关系模型，而是使用键值、文档、图或宽列模型。这些数据库通常用于需要高扩展性和灵活数据模式的应用。

## 关系型数据库的工作原理

RDBMS 将数据存储在表格中，类似于电子表格，可以搜索和排序。表格中的每一行都是一条记录，每一列都是一个字段。例如，下面的表显示了一个电话数据库：

| last_name | first_name | city | state | zip | phone |
|---|---|---|---|---|---|
| Doe | John | Somerset | NY | 5011 | 555-1212 |
| Doe | Jane | Somerset | NY | 5011 | 555-1212 |
| Palmer | John | Anytown | Somerset | 5055 | 555-4567 |
| Johnson | Richard | Eastcity | CT | 12345 | 555-4321 |

> 图 28.1 在此 RDBMS 的可视化中，电话表包含四条记录（行），每个记录有六个字段（列）。

许多数据库使用键将表连接起来。例如，下面的表显示了 `cd_collection` 数据库：

| id | title | artist | year | rating |
|---|---|---|---|---|
| 1 | Mindbomb | The The | 1989 | 4 |
| 2 | For All You've Done | Hillsong | 2004 |  |
| 3 | Trouser Jazz | Mr Scruff | 2002 | 5 |
| 4 | Natural Elements | Acoustic Alchemy | 1988 | 3 |
| 5 | Combat Rock | The Clash | 1982 | 4 |
| 6 | Life for Rent | Dido | 2003 | 5 |
| 7 | Adiemus 4 | Karl Jenkins | 2000 | 4 |
| 8 | The Two Towers | Howard Shore | 2002 | 5 |

> 图 28.2 单个数据库可以包含两个表——在这种情况下，是 phonebook 和 `cd_collection`。

在 `sample_database` 示例中，电话表包含四条记录（行），每个记录有六个字段（列）的数据。`cd_collection` 表包含八条记录，分为五个字段的数据。

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
| 1 | 1002 | 100,252 |  | Y | 8/3/01 |
|  | 121 | 200,352 |  | N | 10/2/01 |
| 3 | 123 | 200,121 |  | Y | 10/2/01 |
| 2 | 122 | 222,151 |  | N | 10/3/01 |

overdue

| cid | order_num | days_overdue | action |
|---|---|---|---|
| 1 | 1002 | 32 | sent letter |

图 28.3 你可以使用三个相关表来跟踪客户、订单和未结发票。

在图 28.3 中，我们在每条客户记录中都添加了 `cid` 字段。该字段持有客户 ID 数字，它是用于链接每个客户所有信息以跟踪订单和发票的唯一数据项。每个客户都分配了一个唯一的 ID，其作用是：两个客户的姓名字段数据可能相同，但他们在 `orders` 和 `overdue` 表中的 ID 字段值取代了 `customers` 表中的 `last_name`、`first_name` 和 `shipping_address` 字段信息。现在，当你想要查询任何客户的订单和发票数据时，你可以根据一个键进行搜索，而不是多个键。你可以在更快、更方便的数据搜索中获得更准确的结果。

现在你已经了解了数据如何在 RDBMS 中存储，以及 RDBMS 结构如何让你处理这些数据，你准备好学习如何从数据库进行输入和输出了。这就是 SQL 大显用场。

# 理解 SQL 基础

SQL（读作“S-Q-L”或“sequel”，取决于说话者）是一种几乎所有可用 RDBMS 都能理解的数据库查询语言。你使用 SQL 语句将数据存入数据库并从数据库检索数据。与任何语言中的语句一样，SQL 语句具有定义的结构，决定了它们的含义和功能。

作为 DBA，你应该理解 SQL 的基础知识，即使你亲自不进行任何实际编程。幸运的是，SQL 与标准英语相似，学习基础非常简单。

# 创建表

如前所述，RDBMS 将数据存储在类似于电子表格的表中。当然，在数据库中创建任何数据之前，你需要创建必要的表和列来存储数据。你可以使用 `CREATE` 语句来实现。

例如，图 28.2 中的 `cd_collection` 表有五列（或字段）：`id`、`title`、`artist`、`year` 和 `rating`。

SQL 为数据提供了几种列类型，定义了将存储什么类型的数据：

- `TINYINT`
- `SMALLINT`
- `INT`
- `BIGINT`
- `DECIMAL`
- `NUMERIC`
- `FLOAT`
- `REAL`
- `DATE`
- `DATETIME`
- `TIMESTAMP`
- `CHAR`
- `VARCHAR`
- `TEXT`
- `BLOB`
- `ENUM`
- `JSON`
- `BIT`
- `BOOLEAN`

SQL 提供了多种数据列类型，定义了数据的类型。例如，`cd_collection` 表有五列，或字段：`id`、`title`、`artist`、`year` 和 `rating`。

SQL 提供了几种数据列类型，定义了将存储什么类型的数据。例如，`cd_collection` 表有五列，或字段：`id`、`title`、`artist`、`year` 和 `rating`。
