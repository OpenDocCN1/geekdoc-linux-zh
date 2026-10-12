
## 16.5.4. 查看选定的记录

在 `select` 语句中使用 `where` 子句，你可以指定你想查看的记录。

```sql
mysql> SELECT * FROM country WHERE countrycode='ES';

+-------------+-------------+-------------+---------------+
| countrycode | countryname | population | countrycapital|
+-------------+-------------+-------------+---------------+
| ES          | Spain       | 48000000    | Madrid        |
+-------------+-------------+-------------+---------------+
1 row in set (0.00 sec)
```

`where` 子句的另一个示例。

```sql
mysql> select * from country where country='Spain';

+-------------+-------------+-------------+---------------+
| countrycode | countryname | population | countrycapital|
+-------------+-------------+-------------+---------------+
| ES          | Spain       | 48000000    | Madrid        |
+-------------+-------------+-------------+---------------+
1 row in set (0.00 sec)
```

### 16.5.5. where 子句中的主键

表的主键是唯一标识表中每条记录（每一行）的字段。当在 `where` 子句中使用另一个字段时，可能会返回多行。

```sql
mysql> insert into country ('EG','Egypt','82000000','Cairo');
```

#### SQL MySQL 简介

```sql
mysql> select * from country where population='82000000';
```

| countrycode | countryname | population | countrycapital |
|---|---|---|---|
| DE | Germany | 82000000 | Berlin |
| EG | Egypt | 82000000 | Cairo |

2 rows in set (0.00 sec)

### 16.5.6. 记录排序

我们知道 `select` 允许我们查看表中的所有记录。考虑此表：

```sql
mysql> select countryname,population from country;

| countryname | population |
|---|---|
| Belgium | 110000000 |
| China | 140000000 |
| Germany | 82000000 |
| Egypt | 82000000 |
| Spain | 48000000 |
| France | 64000000 |
| India | 130000000 |
| Japan | 128000000 |
| Mexico | 113000000 |
| United States | 313000000 |

10 rows in set (0.00 sec)
```

使用 `order by` 子句，我们可以更改记录呈现的顺序。

```sql
mysql> select countryname,population from country order by countryname;

| countryname | population |
|---|---|
| Belgium | 110000000 |
| China | 140000000 |
| Egypt | 82000000 |
| France | 64000000 |
| Germany | 82000000 |
| India | 130000000 |
| Japan | 128000000 |
| Mexico | 113000000 |
| Spain | 48000000 |
| United States | 313000000 |

10 rows in set (0.00 sec)
```

### 16.5.7. 记录分组

考虑这个人员表。截图显示了如何使用 `avg` 函数计算平均值。

```sql
mysql> select * from people;

| Name | Field | birthyear | countrycode |
|---|---|---|---|
| Barack Obama | politics | 1961 | US |
| Deng Xiaoping | politics | 1904 | CN |
| Guy Hofstadt | politics | 1953 | BE |
| Justine Henin | tennis | 1982 | BE |
| Kim Clijters | tennis | 1983 | BE |
| Li Na | tennis | 1982 | CN |
| Liu Yang | astronaut | 1978 | CN |
| Serena Williams | tennis | 1981 | US |
| Venus Williams | tennis | 1980 | US |

9 rows in set (0.0 sec)

mysql> select Field, AVG(birthyear) from people;

+--------------------------+
| Field | AVG(birthyear)   |
+--------------------------+
| politics | 1967.111111111111 |
+--------------------------+
1 row in set (0.0 sec)
```

使用 `group by` 子句，我们可以获得每个字段的平均值。

```sql
mysql> select Field, AVG(birthyear) from people group by Field;

+-----------+----------------+
| Field     | AVG(birthyear) |
+-----------+----------------+
| astronaut | 1978           |
| politics  | 1939.3333333333333 |
| tennis    | 1981.6         |
+-----------+----------------+
3 rows in set (0.0 sec)
```

### 16.5.8. 删除记录

你可以使用 `delete` 永久地从表中删除一条记录。

```sql
