
### 解释

- 1 函数显示为列的名称。
- 2 你可以使用 `AS` 关键字为函数显示结果集的列创建别名或另一个名称。

## B.4.1 数值函数

假设你想获取所有订单的总和，或一组项目的平均成本，或基于特定条件统计表中所有行。聚合函数将基于其他值集返回单个值。如果在 `SELECT` 语句的项列表中与其他多个表达式一起使用，该 `SELECT` 必须包含 `GROUP BY` 子句。如果聚合函数是 `SELECT` 语句获取的唯一值，则不需要 `GROUP BY` 子句。函数及其语法列于表 B.4 中。

**表 B.4 聚合函数**

| 函数 | 功能 |
| :--- | :--- |
| `AVG()` | 计算并返回列的平均值。 |
| `COUNT(*expression*)` | 统计由表达式定义的行的数量。 |
| `COUNT()` | 统计表中所有行的数量。 |
| `MIN()` | 返回列中的最小值。 |
| `MAX()` | 通过表达式返回列中的最大值。 |
| `SUM()` | 返回列中所有值的总和。 |

### EXAMPLE B.37

```
mysql> SELECT COUNT(*) FROM products;
+-----------------+
| COUNT(*)        |
+-----------------+
| 81              |
+-----------------
1 row in set (0.00 sec)
```

```
mysql> SELECT COUNT(*) AS 'Number of Rows' FROM products;
+---------------+
| Number of Rows |
+---------------+
| 81            |
+---------------+
1 row in set (0.00 sec)
```

### 解释

- 1 `COUNT()` 函数统计表中所有行的数量。

### 示例 B.38

```
mysql> SELECT  avg(UnitPrice)
   FROM order_details;
   +-------------------+
   | avg(UnitPrice)    |
   +-------------------+
   |  26.21851972      |
   +-------------------+
   1 row in set (0.01 sec)
```

```
mysql> SELECT FORMAT(avg(UnitPrice),2) as 'Average Price'
   FROM order_details;
   +-------------------+
   | Average Price      |
   +-------------------+
   | 26.22              |
   +-------------------+
   1 row in set (0.00 sec)
```

### 解释

- 1 `AVG()` 函数计算并返回列的平均值，在此称为 `UnitPrice`。
- 2 `FORMAT` 函数返回 `AVG()` 函数的结果，精度为两位小数。

**使用 GROUP BY。** `GROUP BY` 子句可以与 `SELECT` 一起使用，以收集跨越多条记录的所有数据，并按一个或多个列对结果进行分组。这对于 `SUM`、`COUNT`、`MIN` 或 `MAX` 等聚合函数非常有用。请参阅以下两个示例。

### 示例 B.39

```
mysql> select CategoryID, SUM(UnitsInStock) as 'Total Units in Stock'
    -> FROM products
    -> GROUP BY CategoryID;
```

| CategoryID | Total Units in Stock |
| :--- | :--- |
| NULL | 0 |
| 1 | 559 |
| 2 | 507 |
| 3 | 386 |
| 4 | 393 |
| 5 | 308 |
| 6 | 165 |
| 7 | 100 |
| 8 | 701 |

9 rows in set (0.00 sec)

### 示例 B.40

```
mysql> select C.CategoryName,
    -> SUM(P.UnitsInStock) AS Units
    -> FROM products AS P
    -> join categories AS C ON C.CategoryID=
    -> P.CategoryID Group By C.CategoryName;
```

| CategoryName | Units |
| :--- | :--- |
| Beverages | 559 |
| Condiments | 507 |
| Confections | 386 |
| Dairy Products | 393 |
| Grains/Cereals | 308 |
| Meat/Poultry | 165 |
| Produce | 100 |
| Seafood | 701 |

8 rows in set (0.00 sec)

## B.4.2 字符串函数

SQL 提供了许多基本的字符串函数，如表 B.5 所列。

| 函数 | 功能 |
| :--- | :--- |
| `CONCAT(string1, string2, . . . )` | 将列值或变量组合成一个字符串。 |
| `LOWER(string)` | 将字符串转换为全小写字母。 |
| `SUBSTRING(string, position)` | 提取字符串的一部分（参见示例 B.41）。 |
| `TRANSLATE` | 将字符串从一种字符集转换为另一种。 |
| `TRIM(' string ');` | 从字符字符串中删除前导字符、尾随字符或两者。 |
| `UPPER(string)` | 将字符串转换为全大写字母（参见示例 B.41）。 |

SQL99 定义了一个连接运算符 (`||`)，用于与 `CONCATENATE()` 函数一起使用。MySQL 使用表 B.5 中显示的 `concat()` 函数。

### EXAMPLE B.41

```
mysql> select upper(CompanyName) as 'Company' from shippers;
+---------------------+
| Company             |
+---------------------+
| SPEEDY EXPRESS      |
| UNITED PACKAGE      |
| FEDERAL SHIPPING    |
+---------------------+
3 rows in set (0.00 sec)
```

```
mysql> select lower(CompanyName) as 'Company' FROM shippers;
+---------------------+
| Company             |
+---------------------+
| speedy express      |
| united package      |
| federal shipping    |
+---------------------+
3 rows in set (0.00 sec)
```
