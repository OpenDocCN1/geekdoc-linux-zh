
| Rictor Supemarkt | Switzerland  |

+-----------------+-----------+

4 rows in set (0.00 sec)

```
## 解释

`SELECT` 返回来自以 Sw 开头的国家/地区的所有客户。

## 示例 8.16

```
mysql> SELECT City, Country FROM Suppliers WHERE City LIKE ' %o ';
```

+----------+-----------+
| City     | Country   |
+----------+-----------+
| Tokyo    | Japan     |
| Oviedo   | Spain     |
| Sao Paulo | Brazil    |
| Salerno  | Italy     |
+----------+-----------+
4 rows in set (0.00 sec)

## 解释

`SELECT` 返回所有城市和国家，其中 `%` 匹配任何以字母 o 结尾的城市。

## 示例 8.17

```
mysql> SELECT CompanyName FROM customers WHERE CompanyName LIKE '%Super';
```

+---------------+
| CompanyName   |
+---------------+
| LiLa-Supermercado |
| Rictor Supemarkt  |
+---------------+
2 rows in set (0.00 sec)

## 解释

`SELECT` 返回所有公司名称，其中 `%` 匹配包含模式 Super 的任何公司名称。

### `_` 通配符

下一个示例展示了下划线（`_`）通配符字符的工作方式。请记住，`_` 仅匹配一个字符。

## 示例 8.18

```
mysql> SELECT extension, firstname FROM employees
     -> WHERE extension LIKE '4_-';
```

+------------+------------+
| extension  | firstname  |
+------------+------------+
| 428        | Michael    |
| 465        | Robert     |
| 452        | Anne       |
+------------+------------+
3 rows in set (0.00 sec)

## 解释

此 `SELECT` 返回所有其中分机号为三位数且首位数字为 4 的分机号和名字。`_` 符号用于匹配单个字符。

### BETWEEN 语句

`BETWEEN` 关键字允许您根据表示值范围的标准选择字段。`BETWEEN` 子句的语法如下。

## 格式

```
SELECT column FROM table
WHERE column BETWEEN 'value1' AND 'value2'
```

示例：

```
select age from person where age BETWEEN 10 AND 20;
```

## 示例 8.19

```
mysql> SELECT ProductName, Productid
     -> FROM Products WHERE ProductId BETWEEN 30 AND 33;
```

+--------------------------+-----------+
| ProductName              | ProductId |
+--------------------------+-----------+
| Nord-Ost Matjeshering    | 30        |
| Gorgonzola Telino        | 31        |
| Mascarpone Fabioli       | 32        |
| Geitost                  | 33        |
+--------------------------+-----------+
4 rows in set (0.06 sec)

## 解释

如果 `ProductId` 值在 30 到 33 的范围内，`SELECT` 将返回产品名称和产品 ID。

### 使用 ORDER BY 对结果排序

您可以通过使用 `ORDER BY` 子句以特定顺序显示查询结果。行可以按升序（`ASC`，默认值）或降序（`DESC`）排序，其中被排序的值可以是字符串或数字。

## 格式

```
SELECT column FROM table
[WHERE condition]
ORDER BY column [ASC, DESC]
```

示例：

```
SELECT Company, OrderNumber FROM Orders
ORDER BY Company
```

## 示例 8.20

```
mysql> SELECT CompanyName, ContactName FROM suppliers
    -> ORDER BY CompanyName LIMIT 10;
```

| CompanyName                        | ContactName                 |
|------------------------------------|-----------------------------|
| Aux joyeux ecclésiastiques         | GuyLène Nodier              |
| Bigfoot Breweries                  | Cheryl Saylor               |
| Cooperativa de Quesos 'Las Cabras' | Antonio del Valle Saavedra |
| Escargots Nouveaux                 | Marie Delamare              |
| Exotic Liquids                     | Charlotte Cooper            |
| Fürst. d'Urshelles                 | Chantal Goulet              |
| Formaggi Fortini s.r.l.            | Elío Rossi                  |
| G'day, Mate                         | WENDY Mackenzie             |
| Gai pâturage                       | Éliane Noz                  |
| Grandma Kelly's Homestead          | Regina Murphy               |

10 rows in set (0.06 sec)

## 解释

`CompanyName` 按升序排序，限制为 10 条记录。

## 示例 8.21

```
mysql> SELECT CompanyName, ContactName FROM suppliers
mysql> ORDER BY CompanyName DESC LIMIT 10;
```

+-------------------------+------------------+
| CompanyName             | ContactName      |
+-------------------------+------------------+
| Zaane Snoepfabriek      | Dirk Luchte      |
| Tokyo Traders           | Yoshie Nagase    |
| Svensk Sjöföda AB       | Michael Björn    |
| Specialty Biscuits, Ltd.| Peter Wilson     |
| Refrescos Americanas LTD.| Carlos Diaz     |
| Plutzer Lebensmittelgro-märkte AG| Martin Bein |
| PB Knakebröd AB         | Lars Peterson    |
| Pavlova, Ltd.           | Ian Devling      |
| Pasta Buttini s.r.l.    | Giovanni Giudici |
