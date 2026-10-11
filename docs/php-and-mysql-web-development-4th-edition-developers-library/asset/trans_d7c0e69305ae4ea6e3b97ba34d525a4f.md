
| DATE_SUB('1970-1-1', INTERVAL 10 YEAR) |
|----------------------------------------|
| 1960-01-01                             |

本节前面展示的一个查询使用了字面量日期作为选择范围的端点，从而选出在20世纪70年代去世的总统。该查询可以重写为使用一个起始日期的字面量，以及根据起始日期和间隔计算出的结束日期：

```sql
mysql> SELECT last_name, first_name, death
    -> FROM president
    -> WHERE death >= '1970-1-1'
    -> AND death < DATE_ADD('1970-1-1', INTERVAL 10 YEAR);
| last_name | first_name | death      |
|-----------|------------|------------|
| Truman    | Harry S    | 1972-12-26 |
| Johnson   | Lyndon B.  | 1973-01-22 |
```

会员续费查询可以使用 `DATE_ADD()` 来编写：

```sql
SELECT last_name, first_name, expiration FROM member
WHERE expiration < DATE_ADD(CURDATE(), INTERVAL 60 DAY);
```

如果 expiration 列建有索引，由于第 5 章中讨论的原因，这比原始查询更高效。

在本章开头，你看到了以下用于确定牙医的哪些病人已经有一段时间没有来做检查的查询：

```sql
SELECT last_name, first_name, last_visit FROM patient
WHERE last_visit < DATE_SUB(CURDATE(), INTERVAL 6 MONTH);
```

当时你可能没有完全理解那个查询的含义。现在它是否更有意义了？

## 1.4.9.7 模式匹配

MySQL 支持模式匹配操作，使你能够在不提供精确比较值的情况下选择行。要执行模式匹配，你需要使用特殊运算符（`LIKE` 和 `NOT LIKE`），并指定一个包含通配符的字符串。字符 “_” 匹配任何单个字符，而 “%” 匹配任何字符序列（包括空序列）。

此模式匹配以 ‘w’ 或 ‘W’ 字符开头的姓氏：

```sql
mysql> SELECT last_name, first_name FROM president
    -> WHERE last_name LIKE 'W%';
| last_name | first_name |
|-----------|------------|
| Washington| George     |
| Wilson    | Woodrow    |
| Wilson    | Woodrow    |
```

下面的查询演示了一个常见错误。模式匹配是错误的，因为它没有使用 `LIKE`，而是使用算术比较运算符配合一个模式：

```sql
mysql> SELECT last_name, first_name FROM president
    -> WHERE last_name = 'w%' ;
Empty set (0.00 sec)
```

这种比较要成功，列中必须恰好包含字符串 'w%' 或 'w$'。

此模式匹配姓氏中任何位置（不仅是开头）包含 'w' 或 'W' 的：

```sql
mysql> SELECT last_name, first_name FROM president
    -> WHERE last_name LIKE 'w%w%' ;
| last_name  | first_name |
|------------|------------|
| Washington | George     |
| Wilson     | Woodrow    |
| Eisenhover | Dwight D.  |
```

此模式匹配恰好包含四个字符的姓氏：

```sql
mysql> SELECT last_name, first_name FROM president
    -> WHERE last_name LIKE '____' ;
| last_name | first_name  |
|-----------|-------------|
| Polk      | James K.    |
| Taft      | William H.  |
| Ford      | Gerald R.   |
| Bush      | George H.W. |
| Bush      | George W.   |
```

MySQL 还提供了另一种基于正则表达式和 `REGEXP` 运算符的模式匹配形式。`LIKE` 和 `REGEXP` 在第 3.5.1.1 节“运算符类型”以及附录 C 中有进一步讨论。

## 1.4.9.8 定义和使用用户定义变量

MySQL 允许你定义自己的变量。这些变量可以使用查询结果进行设置，这为保存值以供后续查询使用提供了方便的方式。假设你想要找出哪些总统出生在安德鲁·杰克逊之前。为了确定这一点，你可以将他的出生日期检索到一个变量中，然后选择其他出生日期早于该变量值的总统：

```sql
mysql> SELECT @birth := birth FROM president
    -> WHERE last_name = 'Jackson' AND first_name = 'Andrew';

+----------+
| @birth   |
+----------+
| 1767-03-15 |
+----------+

mysql> SELECT last_name, first_name, birth FROM president
    -> WHERE birth < @birth ORDER BY birth;

+-----------+-------------+------------+
| last_name | first_name  | birth      |
+-----------+-------------+------------+
| Washington| George      | 1732-02-22 |
| Adams     | John        | 1735-10-30 |
| Jefferson | Thomas      | 1743-04-13 |
| Madison   | James       | 1751-03-16 |
| Monroe    | James       | 1758-04-28 |
+-----------+-------------+------------+
```

用户变量使用 `@var_name` 语法命名，并在 `SELECT` 语句中使用 `@var_name := value` 形式的表达式赋值。因此，第一个查询查找安德鲁·杰克逊的出生日期并将其赋值给 `@birth` 变量。（`SELECT` 的结果仍然会显示；将查询结果赋值给变量不会抑制查询输出。）第二个查询引用该变量，并使用其值查找出生值较小的其他总统行。

上述问题实际上可以通过使用连接或子查询的单条查询来解决，但我们还没有讲到编写这些内容的阶段。此外，有时候使用变量只是更简单。

变量也可以使用 `SET` 语句进行赋值。在这种情况下，`=` 或 `:=` 均可用作赋值运算符：

```sql
mysql> SET @today = CURDATE();
mysql> SET @one_week_ago := DATE_SUB(@today, INTERVAL 7 DAY);
mysql> SELECT @today, @one_week_ago;

+----------+---------------+
| @today   | @one_week_ago |
+----------+---------------+
| 2008-03-21 | 2008-03-14   |
+----------+---------------+
```

## 1.4.9.9 生成摘要

MySQL 可以为你做的最有用的事情之一，是将大量原始数据浓缩并总结。当你学会使用 MySQL 生成摘要时，它会成为一个强大的盟友，因为手动执行这一活动特别繁琐、耗时且易出错。

一种简单的摘要形式是确定一组值中存在哪些唯一值。使用 `DISTINCT` 关键字从结果中删除重复行。例如，可以通过以下方式找到总统出生的不同州：

```sql
mysql> SELECT DISTINCT state FROM president ORDER BY state;
+----------+
| state    |
+----------+
| AR       |
| CA       |
| CT       |
| GA       |
| IA       |
| IL       |
| KY       |
| MA       |
| MO       |
| NC       |
| NE       |
| NH       |
| NJ       |
| NY       |
| OH       |
| PA       |
| SC       |
| TX       |
| VA       |
| VT       |
+----------+
```

另一种摘要形式涉及使用 `COUNT()` 函数进行计数。如果你使用 `COUNT(*)`，它会告诉你查询选中的行数。如果查询没有 `WHERE` 子句，它选择所有行，因此 `COUNT(*)` 告诉你表中的行数。以下查询显示了历史联盟 `member` 表包含多少会员记录：

```sql
mysql> SELECT COUNT(*) FROM member;
+----------+
| COUNT(*) |
+----------+
|      102 |
+----------+
```

如果查询有 `WHERE` 子句，`COUNT(*)` 告诉你该子句匹配了多少行。此查询显示了迄今为止你给班级出了多少测验：

```sql
mysql> SELECT COUNT(*) FROM grade_event WHERE category = 'Q';
+----------+
| COUNT(*) |
+----------+
|        4 |
+----------+
```

`COUNT(*)` 统计每个选中的行。相比之下，`COUNT(col_name)` 只统计非 NULL 值。以下查询演示了这些差异：

```sql
mysql> SELECT COUNT(*), COUNT(email), COUNT(expiration) FROM member;
+----------+---------------+-------------------+
| COUNT(*) | COUNT(email) | COUNT(expiration) |
+----------+---------------+-------------------+
|      102 |            80 |                96 |
+----------+---------------+-------------------+
```

这表明，虽然会员表有 102 行，但只有 80 行在 email 列中有值。它还表明有六名会员拥有终身会员资格。（expiration 列中的 NULL 值表示终身会员资格，由于 102 行中有 96 行不是 NULL，剩下六行。）

`COUNT()` 结合 `DISTINCT` 统计结果中不同的非 NULL 值的数量。例如，要统计总统出生的不同州的数量，请这样做：

```sql
mysql> SELECT COUNT(DISTINCT state) FROM president;
+---------------------+
| COUNT(DISTINCT state) |
+---------------------+
|                    20 |
+---------------------+
```

你可以生成列中值的总体计数，或按类别细分计数。例如，通过运行此查询，你可能知道班级中学生的总体数量：

```sql
mysql> SELECT COUNT(*) FROM student;
+----------+
| COUNT(*) |
+----------+
|       33 |
+----------+
```

但是有多少男生和多少女生？一种方法是分别询问每种性别的计数：

```sql
mysql> SELECT COUNT(*) FROM student WHERE sex='f';
+----------+
| COUNT(*) |
+----------+
|       15 |
+----------+
mysql> SELECT COUNT(*) FROM student WHERE sex='m';
+----------+
| COUNT(*) |
+----------+
|       18 |
+----------+
```

