
为了有效地设置和管理 RDBMS，你需要了解一点关系型数据库是如何存储存储的，以及用户如何访问和处理这些数据。本节不提供关系型数据库理论和管理的详细课程，但它对核心概念和过程提供了良好的概述。`DBMS` 将数据存储在表中，你可以将其想象成电子表格。表中的每列都是一个字段；例如，一列可能包含一个名称或地址。表中的每行都是一条单独的记录。表有一个名称，当你从中提取数据或向其输入数据时可以使用你可以引用该表。图 17.1 显示了一个简单的关系型数据库示例，存储了姓名和地址信息。

| last_name | first_name | address | city | state | phone |
|---|---|---|---|---|---|
| Doe | John | 501 Somerset | Anytown | NY | 555-555-1212 |
| Doe | Jane | 501 Somerset | Anytown | NY | 555-555-1212 |
| Palmer | John | 205 Street | Somerset | NY | 123-456-7890 |
| Johnson | Robert | 100 East | Anytown | CT | 111-222-3333 |

FIGURE 17.1 在此可视化中，RDBMS 存储了数据，数据库存储了四条记录

在此可视化中，RDBMS 存储数据，数据库存储了四条记录。在图 17.1 所示的示例中，RDBMS 存储数据，数据库存储了四条记录，分为七列。

图 17.2 显示的是一个包含两个记录的数据库。

| last_name | first_name | address | city | state | phone |
|---|---|---|---|---|---|
| Doe | John | 501 Somerset | Anytown | NY | 555-555-1212 |
| Doe | Jane | 501 Somerset | Anytown | NY | 555-555-1212 |
| Palmer | John | 205 Street | Somerset | NY | 123-456-7890 |
| Johnson | Robert | 100 East | Anytown | CT | 111-222-3333 |

| last_name | first_name | phone |
|---|---|---|
| Doe | John | 555-555-1212 |
| Doe | Jane | 555-555-1212 |
| Palmer | John | 123-456-7890 |
| Johnson | Robert | 111-222-3333 |

| common_name | order | family | species |
|---|---|---|---|
| Lion | Carnivora | Felidae | leo |
| Elephant | Proboscidea | Elephantidae | africana |
| Meerkat | Carnivora | Herpestidae | suricata |
| Hyena | Carnivora | Hyaenidae | cuta |
| Giraffe | Artiodacta | Giraffidae | reticulata |
| Zebra | Perissodyla | Equidae | burchell |
| Cheetah | Carnivora | Felidae | jubatus |
| Gazelle | Artiodacta | Bovidae | thomson |
| Hippopotamus | Artiodacta | Hippopotamidae | amphibius |

| order_num | stock_num | priority | shipped | date |
|---|---|---|---|---|
| 1002 | 252,342 | 3 | Y | 8/31/01 |
| 1221 | 200,352 | 1 | N | 10/2/01 |
| 1223 | 200,121 | 2 | Y | 10/2/01 |
| 1225 | 221,152 | 1 | N | 10/3/01 |

| order_num | days_overdue | action |
|---|---|---|
| 1002 | 32 | sent letter |

| last_name | first_name | shipping_address |
|---|---|---|
| Doe | John | 505 Street |
| Doe | Jane | 505 Street |
| Palmer | John | 200 Street |
| Johnson | Richard | 1000 Street |

在图 17.1 所示的示例中，数据库只包含一个表。大多数 RDBMS 比这复杂得多，包含多个表。

图 17.2 显示的是一个包含两个记录的数据库。

在图 17.3 所示的示例中，我们为每个客户记录添加了客户 ID 字段。该字段持有一个客户 ID 数字，它是用于链接所有其他信息的唯一信息，以便跟踪订单和发票。假设你经营一家销售小部件的公司，并且拥有客户数据库。除了存储客户的姓名、地址和电话，你还可以使用 RDBMS 中的三个表来跟踪订单和发票信息，这就是完全正确的。

为了有效地设置和管理 RDBMS，你需要了解一点关系型数据库是如何存储信息的，以及用户如何访问和处理这些数据。本节不提供关系型数据库理论和管理的详细课程，但它对核心概念和过程提供了良好的概述。`DBMS` 将数据存储在表中，你可以将其想象成电子表格。表中的每列都是一个字段；例如，一列可能包含一个名称或地址。表中的每行都是一条单独的记录。表有一个名称，当你从中提取数据或向其输入数据时可以使用该名称引用该表。

`SQL`（发音为 "S-Q-L" 或 "se-quel"）是一种几乎所有可用 RDBMS 都理解的数据库查询语言。你使用 SQL 语句将数据放入数据库并从中检索。正如任何语言中的语句一样，SQL 语句具有定义的结构，决定了它们的含义和功能。

在大多数情况下，SQL 被编写到前端或中间件应用程序中，用户并不直接操作它们。因此，大多数终端用户不知道 SQL 及其作用，也没有理由关注 SQL 语句的结构。

# 第 17 章在 Red Hat Linux 中管理数据库服务

然而，作为一名 DBA，即使你不会亲自进行任何实际编程工作，也应该理解 SQL 的基础知识。幸运的是，SQL 与标准英语非常相似，学习基础非常简单。

> 提示
>
> 下面的章节并不打算作为 SQL 教程。它们的目的仅仅是向你介绍该语言的基础知识。如果你需要完整的 SQL 编程教程，请查阅关于该主题的几本书中的一本，包括 MySQL (New Riders Publishing)、Sams Teach Yourself MySQL in 21 Days (Sams Publishing) 以及 PostgreSQL (Sams Publishing)。

## 创建表

如前所述，RDBMS（关系型数据库管理系统）将数据存储在类似于电子表格的表中。当然，在向数据库中存储任何数据之前，你需要创建所需的表和列来存储数据。你通过使用 `CREATE` 语句来实现这一点。

例如，图 17.2 中的 `serengeti_mammal` 表有六列字段分别是：`common_name`（通用名称）、`order`（目）、`family`（科）、`genus`（属）、`species`（种）和 `sub_species`（亚种）。

SQL 提供了几种列类型来定义列中将存储什么类型的数据。可用类型包括 `INT`、`FLOAT`、`CHAR` 和 `VARCHAR`。`CHAR` 和 `VARCHAR` 的区别在于前者持有固定长度字符串，而后者持有变长度字符串。

还有一些特殊的列类型，例如 `DATE`，它只接受日期格式的数据；以及 `ENUM`（枚举），用于指定只允许某些值。（例如，如果你想在数据库中记录动物的性别，可以使用一个接受 M 和 F 值的 `ENUM` 列。你将在本章稍后学习更多关于 `ENUM` 的知识。）

查看 `serengeti_mammal` 表，你可以发现所有列都包含字符数据。此外，这些字符字符串是变长度的。根据这些信息，你可以判断出所有列的最佳类型是 `VARCHAR`。你还应该注意到 `serengeti_mammal` 表的另一点：除了最后一列（`sub_species`）外，表中的所有列都需要一个值。表中的并不是所有动物都有亚种分类，因此最后一列可以留空。这两个事实在你设置表时将非常重要。

你现在准备好创建表了。如之前所述，你使用的 `CREATE` 语句使用以下语法：
