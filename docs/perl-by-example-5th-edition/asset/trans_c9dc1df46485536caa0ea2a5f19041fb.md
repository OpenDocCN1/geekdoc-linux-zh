
## B.1.4 USE 命令

USE 命令会将指定的数据库设置为主数据库。从该时刻起，所有 SQL 命令都将在主数据库上执行。这是少数几个不需要分号来结束的命令之一。

**格式**

```sql
USE database_name;
```

**示例 B.2**

```
1    mysql> USE northwind;
       Database changed
```

**解释**

USE 命令将数据库切换为 northwind。命令行客户端会报告数据库已更改。

## B.1.5 SQL 数据库表

数据库通常包含一个或多个表。每个表都有一个名称来标识，例如 Customers（客户）或 Orders（订单）。SHOW TABLES IN 命令显示数据库内的所有表，如图 B.5 所示。SELECT * FROM 命令列出指定表中所有的字段和行。表包含称为记录的行和称为字段的列。图 B.6 中的表包含三条记录（每个运输商各一条）和三个列（ShipperID、CompanyName 和 Phone）。

**图 B.5** 显示 northwind 数据库中的所有表。

```
mysql> show tables in northwind;

+-------------------------------+
| Tables_in_northwind           |
+-------------------------------+
| categories                    |
| custmercustormerdemo          |
| customerdemographics          |
| customers                     |
| employees                     |
| employeeterritories           |
| order_details                 |
| orders                        |
| products                      |
| region                        |
| shippers                      |
| suppliers                     |
| territories                   |
| usstates                      |
+-------------------------------+
14 rows in set (0.03 sec)
```

**图 B.6** 显示特定表的内容。

```
mysql> select * from shippers;

+------------+-----------------+---------------+
| ShipperID  | CompanyName     | Phone         |
+------------+-----------------+---------------+
| 1          | Speedy Express  | (503) 555-9831|
| 2          | United Package  | (503) 555-3199|
| 3          | Federal Shipping| (503) 555-9931|
+------------+-----------------+---------------+
3 rows in set (0.00 sec)
```

**SHOW 和 DESCRIBE 命令。** 要查看可以分配到表的数据类型，请使用 MySQL 特有的 DESCRIBE 命令和标准 SQL 命令 SHOW FIELDS IN 命令。显示输出是每个字段的名称以及与每个字段对应的值的数据类型，如图 B.7 所示。数据类型可以是可变长度的字符串、日期、数字等。例如，类型 varchar(40) 表示一个最多包含 40 个字符的字段。同时显示的还有用于唯一标识记录的主键。

**格式**

```sql
SHOW FIELDS IN table_name;
```

或者

```sql
DESCRIBE table_name;
```

**图 B.7** SQL SHOW FIELDS IN 命令。

```
mysql> show fields in customers;

Field                 Type       Null Key Default Extra
CustomerID            varchar(5)  PRI
CompanyName           varchar(40) MUL
ContactName           varchar(30) YES     NULL
ContactTitle          varchar(30) YES     NULL
Address               varchar(60)         NULL
City                  varchar(15) YES MUL  NULL
Region                varchar(15) YES MUL  NULL
PostalCode            varchar(10) YES MUL  NULL
Country               varchar(15) YES      NULL
Phone                 varchar(24) YES      NULL
Fax                   varchar(24) YES      NULL

11 rows in set (0.05 sec)
```

更简短的 DESCRIBE 版本如图 B.8 所示。

**图 B.8** MySQL DESCRIBE 命令。

```
mysql> describe shippers;

Field            Type         Null Key Default Extra
ShipperID        int(11)      PRI NULL auto_increment
CompanyName      varchar(40)
Phone            varchar(24) YES NULL

3 rows in set (0.00 sec)
```

## B.2 SQL 数据操作语言 (DML)

SQL 是一种非过程化语言，提供用于提取数据的语法，包括用于更新、插入和删除记录的语法。

这些查询和更新命令共同构成了 SQL 的数据操作语言 (DML) 部分。我们将在本节中介绍以下 SQL 命令：

- SELECT—从数据库表中提取数据。
- UPDATE—更新数据库表中的数据。
- DELETE—删除数据库表中的数据。
- INSERT INTO—向数据库表中插入新数据。

### B.2.1 SELECT 命令

最常用的 SQL 命令之一是 SELECT，执行查询时它是必不可少的。SELECT 命令用于根据某些条件从表中检索数据。

它指定了要检索的逗号分隔的字段列表，FROM 子句指定要访问的表。结果存储在一个称为结果集的结果表中。* 符号可用于表示所有字段。

**格式**

```sql
SELECT column_name(s) FROM table_name
```

**示例：**

```sql
SELECT LastName, FirstName, Address FROM Students;
```

**示例 B.3**

![](img/8556abcb353c0991f12099420ec28735_761_0.png)

**解释**

SELECT 命令将从 Shippers 表中检索 CompanyName 字段中的所有项目。结果集表将作为对查询的响应而显示。

**选择指定列。** 若要选择 Shippers 表中名为 CompanyName 和 Phone 的列，SELECT 后跟一个逗号分隔的字段列表，这些字段是从 Shippers 表中选取的。生成的表称为结果集，如图 B.4 所示。

**示例 B.4**

![](img/8556abcb353c0991f12099420ec28735_761_1.png)

**选择所有列。** 若要选择 Shippers 表中的所有列，请使用 * 符号代替列名，如图 B.5 所示。* 是用于表示所有字段（列）的通配符。

**示例 B.5**

```
mysql> SELECT * FROM Shippers;
+-----------+----------------+-----------------+
| ShipperID | CompanyName     | Phone           |
+-----------+----------------+-----------------+
|         1 | Speedy Express  | (503) 555-9831  |
|         2 | United Package  | (503) 555-3199  |
|         3 | Federal Shipping| (503) 555-9931  |
+-----------+----------------+-----------------+
3 rows in set (0.06 sec)
```

**SELECT DISTINCT 语句。** DISTINCT 关键字用于仅从表中返回不同的（唯一的）值。如果指定字段有多个值，DISTINCT 结果集将只显示其中一个。

在下一个示例中，首先选中名为 ShipName 的列中的所有 ALL 值，并显示超过 800 条记录，但请注意，使用 DISTINCT 关键字后，检索到的记录少于 90 条。

**格式**

```sql
SELECT DISTINCT column_name(s) FROM table_name
```

**示例 B.6**

```
SELECT ShipName from Orders
(Partial Output)
| North/South
| Blauer See Delikatesesen
| Ricardo Adocidacos
| Franchi S.p.a.
| Great Lakes Food Market
| Reggiani Caseifici
| Hungry Owl All-Night Grocers
| Save-a-lot Markets
| LILA-Supermercado
| White Clover Markets
| Drachenblut Delikatesesen
| Queen Cozinha
| Tortuga Restaurante
| Lehmanns Marktstand
| LILA-Supermercado
| Ernst Handel
| Pericles Comidas clásicas
| Simons Bistro
| Richter Supermarkt
| Bon app'
| Rattlesnake Canyon Grocery
830 rows in set (0.00 sec)

SELECT DISTINCT ShipName FROM Orders;

| Océano Atlántico Ltda.
| Franchi S.p.A.
| Gourmet Lanchonetes
| Consolidated Holdings
| Rancho grande
| Lazy K Kountry Store
| Laughing Bacchus Wine Cellars
| Blauer See Delikateessen
| North/South
| Cactus Comidas para llevar
| Great Lakes Food Market
| Maison Dewey
| Trail's Head Gourmet Provisioners
| Let's Stop N Shop
```

使用 DISTINCT 关键字后，检索到的记录少于 90 条。

**使用 LIMIT 限制结果集中的行数。** 如果您不希望显示巨大的数据库，可以使用 LIMIT 来限制要打印的行数；例如，northwind 数据库中的表包含数千条记录。在上面的示例中，最好显示几行以证明查询成功。由于您只获取了部分列表，您可能想知道表中的总数。这可以通过使用 SQL_CALC_FOUND_ROWS 选项和 FOUND_ROWS() 函数来完成。SQL 将计算记录总数，而 FOUND_ROWS() 函数允许您显示该计算的结果。

