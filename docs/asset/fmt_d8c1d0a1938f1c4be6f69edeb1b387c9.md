
你可以使用标准的 UNIX 工具（如 `grep`、`awk` 和 `perl`）从这个原始数据库中搜索并提取信息。虽然对于仅供一人使用的地址簿的小数据库可能有效，但此类平文件数据库具有局限性：

- 它们无法扩展。平文件数据库无法对数据进行随机访问。它们只能执行顺序访问。这意味着必须逐行扫描文件的每一行来查找特定信息。随着数据库规模的增长，访问时间会增加，性能会下降。

平文件数据库不适用于多用户环境。根据数据库的设置方式，它要么只允许一个用户同时访问，要么允许两个用户同时进行更改，而更改可能会重叠。这些局限性显然使得平文件数据库不适用于任何正式工作——更不用说是在企业环境中。关系型数据库（称为 `RDBMS`）非常擅长发现数据碎片之间的关系。`RDBMS` 将数据存储在表格中，使数据可以搜索和排序。

# 第 17 章 数据库服务的管理

## 关系型数据库的工作原理

为了设置和管理 `RDBMS`，你需要了解关系型数据库如何存储信息以及用户如何访问。本节并不提供详细的关系数据库理论课程，但对核心概念提供了一个良好的概述。

`RDBMS` 将数据存储在表中，你可以将其可视化为电子表格。表格中的每一列是一个字段；例如，某一列可能包含名称或地址。表格中的每一行是一单独记录。表格本身有一个名称，当你想要获取或存入数据时可以使用该名称。图 17.1 显示了一个简单关系型数据库的示例，它存储了姓名和地址信息。

| last_name | first_name | address | city | state | zip | phone |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Doe | John | 501 Streets | Anytown | NY | 55011 | 555-1212 |
| Doe | Jane | 501 Streets | Anytown | NY | 55011 | 555-1212 |
| Palmer | John | 205 Streets | Sweetown | NY | 55055 | 123-456-7890 |
| Johnson | Robert | 100 Streets | Easytown | CT | 12345 | 111-222-333 |

图 17.1 在此 `RDBMS` 数据可视化中，数据库存储了包含姓名和地址信息的行，分为七个字段（列）

在图 17.1 显示的示例中，数据库只包含一个表。大多数 `RDBMS` 设置比这复杂得多，单个数据库包含多个表。图 17.2 显示了一个名为 `sample_database` 包含两个表的数据库示例。

`phonebook`

| last_name | first_name | phone |
|---|---|---|
| Doe | John | 555-1212 |
| Doe | Jane | 555-1212 |
| Palmer | John | 123-456-7890 |
| Johnson | Richard | 111-222-3333 |

`sample_database`

`serengeti_mammal`

| common_name | order | family | genus | sub-species |
|---|---|---|---|---|
| African Lion | Carnivore | Felidae | Panthera | |
| African Elephant | Proboscide | Elephantidae | Loxodonta | africana |
| Meerkat | Carnivore | Vivididae | Suricata | surricatta |
| Hyena | Carnivore | Hyaenidae | Crocuta | |
| Reticulated Giraffe | Herbivore | Giraffidae | Giraffa | camelopardalis |
| Plains Zebra | Herbivore | Equidae | Equus | bonny |
| Cheetah | Carnivore | Felidae | Acinonyx | |
| Thompson's Gazelle | Artiodactyl | Bovidae | Gazella | thomson |
| Hippopotamus | Artiodactyl | Hippopotamidae | Hippopotamus | amphibius |

图 17.2 单个数据库可以包含两个表——在本例中为 `phonebook` 和 `serengeti_mammal`。

在 `sample_database` 示例中，`phonebook` 表包含四条记录（行），而 `serengeti_mammal` 表包含九条记录，分为六个数据字段。

如果你认为 `phonebook` 表与 `sample_database` 示例之间完全没有关系，那么你的想法完全正确。在关系型数据库中，用户可以在单个数据库中存储多个数据表——即使一个表中的数据与其他表中的数据无关。

例如，你经营着一家销售小部件和小构设备的小型公司，并且有一个计算机化的客户数据库。除了存储每个客户的姓名、地址和电话号码外，你可能还想查询任何客户的未结订单和发票信息。你可以在 `RDBMS` 中使用三个相关表来实现此类目的。图 17.3 展示了此类数据库的示例。

在图 17.3 示例中，我们为每个客户记录添加了客户 ID（`cid`）。该字段持有唯一信息，可用于链接每个客户的所有其他信息，以便跟踪订单和发票。每个客户都分配有一个唯一的 ID；两个客户在字段中的数据可能相同，但它们的字段值永远不会相同。`Orders` 和 `Overdue` 表中的 Customer ID 字段替换了 `Customers` 表中的姓（Last Name）、名（First Name）和收货地址（Shipping Address）信息。现在，当你想搜索任何客户的订单和发票数据时，你可以基于一个键而不是多个键进行搜索。你可以获得更准确、且更快、更方便地-

## 数据库基础回顾

`customers`

| cid | last_name | first_name | shipping_address |
|---|---|---|---|
| 1 | Doe | John | 505 Somestreet |
| 2 | Doe | Jane | 505 Somestreet |
| 3 | Palmer | John | 200 Anystreet |
| 4 | Johnson | Richard | 1000 Anystreet Street |

`orders`

| cid | order_num | stock_num | priority | shipped | date |
|---|---|---|---|---|---|
| 1 | 1002 | 100,252,342 | 3 | Y | 8/31/01 |
| 1 | 1221 | 200,352 | 1 | N | 10/2/01 |
| 3 | 1223 | 200,121 | 2 | Y | 10/2/01 |
| 2 | 1225 | 221,152 | 1 | N | 10/3/01 |

`overdue`

| cid | order_num | days_overdue | action |
|---|---|---|---|
| 1 | 1002 | 32 | sent letter |

**图 17.3** 你可以利用数据在相关表中存储的思路，来跟踪客户、订单和未结发票。

现在你已经了解了数据在 `RDBMS` 中如何存储，以及 `RDBMS` 结构如何让你处理这些数据，你准备好学习如何从数据库输入和输出数据了。这就是 `SQL` 发挥用场的地方

## 理解 SQL 基础

`SQL`（读作 "S-QL" 或 "se-quel"）是目前几乎所有可用 `RDBMS` 都的数据库查询语言。你可以使用 `SQL` 语句将数据导入数据库并从数据库检索数据。与任何语言中的语句一样，`SQL` 语句具有定义的结构，决定了它们的含义和功能。

在大多数情况下，`SQL` 被编写在用户无需直接操作的前端或中间件应用程序中。因此，大多数终端用户不知道 `SQL` 及其作用，也没有理由担心 `SQL` 语句的结构。

然而，作为一名 DBA，你应该理解 `SQL` 的基础，即使你没有亲自进行任何实际编程工作。幸运的是，`SQL` 与标准英语非常相似，学习基础非常简单。

> **提示**
>
> 以下章节并非打算……（注意：OCR 文本在此处似乎已损坏或中断）

## 创建表

如前所述，你可以创建表。例如，`serengeti_mammal` 有以下列：
