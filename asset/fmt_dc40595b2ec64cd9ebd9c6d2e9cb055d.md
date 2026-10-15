
**未实现的函数。** OpenGIS 规范还定义了以下 MULTIPOLYGON 属性函数，但 MySQL 未实现它们：`CENTROID()`、`POINTONSURFACE()`。

以下函数接受处于内部格式的空间 `GEOMETRYCOLLECTION` 值 `gc`，并返回该值的属性。

- `GEOMETRYN(gc, n)`

返回 `gc` 中的第 n 个几何体。返回值的类型取决于第 n 个几何体是什么。几何体的编号从 1 开始。

- `NUMGEOMETRIES(gc)`

返回 `gc` 中的几何体数量。

### C.2.9.3 空间关系函数

MySQL 实现了以下函数，用于测试内部空间格式中两个几何体 `geom1` 和 `geom2` 之间的空间关系。这些函数基于每个几何体值的最小边界矩形（MBR）。

- `MBRCONTAINS(geom1,geom2)`

如果 `geom1` 的最小边界矩形包含 `geom2` 的最小边界矩形，则返回 1；否则返回 0。

- `MBRDISJOINT(geom1,geom2)`

如果 `geom1` 和 `geom2` 的最小边界矩形不相交，则返回 1；否则返回 0。如果两个几何体不相交，则它们互不相交。

- `MBREQUAL(geom1,geom2)`

如果 `geom1` 和 `geom2` 的最小边界矩形相等，则返回 1；否则返回 0。

- `MBRINTERSECTS(geom1,geom2)`

如果 `geom1` 和 `geom2` 的最小边界矩形相交，则返回 1；否则返回 0。

- `MBROVERLAPS(geom1,geom2)`

如果 `geom1` 和 `geom2` 的最小边界矩形重叠，则返回 1；否则返回 0。

- `MBRTOUCHES(geom1,geom2)`

如果 `geom1` 和 `geom2` 的最小边界矩形相触，则返回 1；否则返回 0。

- `MBRWITHIN(geom1,geom2)`

如果 `geom1` 的最小边界矩形位于 `geom2` 的最小边界矩形之内，则返回 1；否则返回 0。

OpenGIS 规范定义了用于测试空间关系的以下函数。MySQL 目前以与相应的基于 MBR 的函数相同的方式实现它们。

- `CONTAINS(geom1,geom2)`
- `DISJOINT(geom1,geom2)`
- `EQUALS(geom1,geom2)`
- `INTERSECTS(geom1,geom2)`
- `OVERLAPS(geom1,geom2)`
- `TOUCHES(geom1,geom2)`
- `WITHIN(geom1,geom2)`

**未实现的函数。** OpenGIS 规范还定义了这些空间关系函数，但它们尚未实现：`CROSSES()`、`DISTANCE()` 和 `RELATED()`。

### C.2.10 XML 函数

本节中的函数允许处理表示 XML 片段的字符串，使用 XPath 表达式从片段中提取文本，或返回将匹配的元素替换为另一个字符串后的片段。

传递给这些函数的 XML 字符串参数必须包含正确平衡和嵌套的标签。

这些函数使用 XPath 1.0。有关 XPath 的一般信息，请参见 http://www.w3.org/TR/xpath 中的规范。对 XPath 的支持存在一些限制。请参阅 MySQL 参考手册了解当前的限制。

#### EXTRACTVALUE (xml_str, xpath_expr)

应用 XPath 表达式对 XML 字符串求值，并返回表达式匹配的元素的第一个文本节点的内容。如果表达式匹配多个元素，结果是每个匹配元素的第一个文本节点，中间用空格连接。

```sql
EXTRACTVALUE('<a><b>B</b><c>CC</c></a>', '/b')      -> 'B'
EXTRACTVALUE('<a><b>B1</b><b>B2</b><b>B3</b>...</a>', '/b')
    -> 'B1 B2 B3'
```

如果没有匹配项，结果为空字符串（与匹配没有文本内容的元素的结果相同）。

`EXTRACTVALUE()` 在 MySQL 5.1.5 中引入。

#### UPDATEXML (xml_str, xpath_expr, xml_new)

应用 XPath 表达式对 XML 字符串求值，将匹配的元素替换为 `xml_new`，并返回结果。如果表达式没有匹配项或匹配多个元素，则返回未修改的 XML 字符串。

`UPDATEXML()` 在 MySQL 5.1.5 中引入。

### C.2.11 其他函数

本节中的函数不属于前面各节中的任何类别。

#### BENCHMARK (n, expr)

重复求值表达式 `expr` `n` 次。`BENCHMARK()` 是一种特殊的函数，旨在用于 `mysql` 客户端程序。它的返回值总是 0，因此没有用处。感兴趣的值是 `mysql` 在查询结果后显示的经过时间：

```
mysql> SELECT BENCHMARK(1000000, PASSWORD('secret'));
+-----------------------------------------+
| BENCHMARK(1000000, PASSWORD('secret')) |
+-----------------------------------------+
|                                       0 |
+-----------------------------------------+
1 row in set (2.35 sec)
```

时间只是服务器求值表达式速度的近似指标，因为它表示的是客户端的挂钟时间，而不是服务器上的 CPU 时间。时间可能受到诸如服务器负载、查询到达时服务器是否处于可运行状态或被换出等因素的影响。您可能希望多次执行以查看典型值。

#### BIT_COUNT(n)

返回参数中设置的位数，该参数被视为 `BIGINT` 值（64 位整数）。

| 表达式 | 结果 |
| :--- | :--- |
| `BIT_COUNT(0)` | → 0 |
| `BIT_COUNT(1)` | → 1 |
| `BIT_COUNT(2)` | → 1 |
| `BIT_COUNT(7)` | → 3 |
| `BIT_COUNT(-1)` | → 64 |
| `BIT_COUNT(NULL)` | → NULL |

#### BIT_LENGTH(str)

返回字符串 `str` 的位数长度，如果参数为 NULL 则返回 NULL。

| 表达式 | 结果 |
| :--- | :--- |
| `BIT_LENGTH('abc')` | → 24 |
| `BIT_LENGTH('a long string')` | → 104 |
| `BIT_LENGTH(CONVERT('abc' USING ucs2))` | → 48 |

#### CONNECTION_ID()

返回服务器与当前客户端连接关联的连接标识符。每个客户端都有一个在已连接客户端集合中唯一的标识符。

| 表达式 | 结果 |
| :--- | :--- |
| `CONNECTION_ID()` | → 10146 |

#### CURRENT_USER()

当您连接到 MySQL 服务器时，您的连接将与 `mysql.user` 表中的某个特定账户行进行身份验证。`CURRENT_USER()` 函数返回该行中 User 和 Host 列的值，格式为 `'user_name@host_name'` 的 utf8 字符串。括号是可选的。

| 表达式 | 结果 |
| :--- | :--- |
| `CURRENT_USER()` | → 'sampadm@localhost' |
| `SUBSTRING_INDEX(CURRENT_USER(), '@', 1)` | → 'sampadm' |

您可以使用 `CURRENT_USER()` 来确定服务器认为您是谁。如果服务器将您身份验证为其他账户，这可能与您连接时指定的用户不同。特别是，如果服务器将您身份验证为匿名用户，返回值的用户名部分为空，而 `USER()` 返回值的用户名部分包含您在连接时指定的用户名。

#### DATABASE()

返回包含默认数据库名称的 utf8 字符串，如果没有默认数据库则返回 NULL。

```
DATABASE()                      → 'sampdb'
```

#### FOUND_ROWS()

返回在前面的 SELECT 语句中没有 LIMIT 子句时本应返回的行数。例如，此语句最多将返回 10 行：

```
mysql> SELECT * FROM mytbl LIMIT 10;
```

要确定在没有 LIMIT 子句的情况下该语句将返回多少行，请执行以下操作：
