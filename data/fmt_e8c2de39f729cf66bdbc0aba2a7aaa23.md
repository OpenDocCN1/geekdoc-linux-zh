
```
mysql> SELECT * FROM vpres WHERE suffix <> '';
ERROR 1054 (42S22): Unknown column 'suffix' in 'where clause'
```

视图的列名默认是其 `SELECT` 语句输出列列表中命名的列名。若要显式提供列名，请在视图定义中视图名称后添加括号内的名称列表：

```
mysql> CREATE VIEW vpres2 (ln, fn) AS
    -> SELECT last_name, first_name FROM president;
```

现在引用该视图时，必须使用给定的列名，而不是 `SELECT` 中的名称：

```
mysql> SELECT last_name, first_name FROM vpres2;
ERROR 1054 (42S22) at line 1: Unknown column 'last_name' in 'field list'
mysql> SELECT ln, fn FROM vpres2;
```

| ln        | fn     |
|-----------|--------|
| Washington| George |
| Adams     | John   |
| Jefferson | Thomas |
| Madison   | James  |
| Monroe    | James  |
| ...       |        |

## 2.11 使用视图

视图可用于自动执行计算。在第 1.4.9.6 节“处理日期”中，我们制定了一个确定总统去世时年龄的语句。相同的计算可以纳入视图定义中：

```
mysql> CREATE VIEW pres_age AS
mysql>    SELECT last_name, first_name, birth, death,
mysql>           TIMESTAMPDIFF(YEAR, birth, death) AS age
mysql>    FROM president;
```

此视图包含一个定义为计算的 `age` 列，从视图中选择该列会检索计算结果：

```
mysql> SELECT * FROM pres_age;
```

| last_name | first_name | birth    | death    | age |
|-----------|------------|----------|----------|-----|
| Washington| George     | 1732-02-22 | 1799-12-14 | 67  |
| Adams     | John       | 1735-10-30 | 1826-07-04 | 90  |
| Jefferson | Thomas     | 1743-04-13 | 1826-07-04 | 83  |
| Madison   | James      | 1751-03-16 | 1836-06-28 | 85  |
| Monroe    | James      | 1758-04-28 | 1831-07-04 | 73  |
| ...       |            |          |          |     |

通过在视图定义中包含年龄计算，不再有必要写出公式来查看年龄值。视图隐藏了细节。

视图可以引用多个表，这使得运行涉及连接的查询更容易。以下视图查找分数，并将其与学生和赛事事件信息连接：

```
mysql> CREATE VIEW vstudent AS
mysql>    SELECT student.student_id, name, date, score, category
mysql>    FROM grade_event INNER JOIN score INNER JOIN student
mysql>    ON grade_event.event_id = score.event_id
mysql>       AND score.student_id = student.student_id;
```

当您从视图中选择数据时，`MySQL` 执行连接并返回来自多个表的信息：

```
mysql> SELECT * FROM vstudent;
```

| student_id | name   | date       | score | category |
|------------|--------|------------|-------|----------|
| 1          | Megan  | 2008-09-03 | 20    | Q        |
| 3          | Kyle   | 2008-09-03 | 20    | Q        |
| 4          | Katie  | 2008-09-03 | 18    | Q        |
| 5          | Abby   | 2008-09-03 | 13    | Q        |
| 6          | Nathan | 2008-09-03 | 18    | Q        |
| 7          | Liesl  | 2008-09-03 | 14    | Q        |
| 8          | Tan    | 2008-09-03 | 14    | Q        |
| ...        |        |            |       |          |

视图使按姓名检索特定学生的分数变得轻而易举：

```
mysql> SELECT * FROM vstudent WHERE name = 'Emily';
```

```
+------------+-------+------------+-------+----------+
| student_id | name  | date       | score | category |
+------------+-------+------------+-------+----------+
|         31 | Emily | 2008-09-03 |    11 | Q        |
|         31 | Emily | 2008-09-06 |    19 | Q        |
|         31 | Emily | 2008-09-09 |    81 | T        |
|         31 | Emily | 2008-09-16 |    19 | Q        |
|         31 | Emily | 2008-09-23 |     9 | Q        |
|         31 | Emily | 2008-10-01 |    76 | T        |
+------------+-------+------------+-------+----------+
```

某些视图是可更新的，这意味着您可以通过对视图的操作来插入、更新和删除底层表中的行。以下是一个简单的示例：

```
mysql> CREATE TABLE t (i INT);
mysql> INSERT INTO t (i) VALUES(1), (2), (3);
mysql> CREATE VIEW v AS SELECT i FROM t;
mysql> SELECT i FROM v;
```

```
+---+
| i |
+---+
| 1 |
| 2 |
| 3 |
+---+
```

```
mysql> INSERT INTO v (i) VALUES(4);
mysql> DELETE FROM v WHERE i < 3;
mysql> SELECT i FROM v;
```

```
+---+
| i |
+---+
| 3 |
| 4 |
+---+
```

```
mysql> UPDATE v SET i = i + 1;
mysql> SELECT i FROM v;
```

```
+---+
| i |
+---+
| 4 |
| 5 |
+---+
```

## 2.12 多表删除和更新

有时，根据行是否匹配另一张表中的行来删除这些行会很有用。同样地，使用另一张表中行的内容来更新一张表中的行也常常很有用。本节介绍如何执行多表 `DELETE`（删除）和 `UPDATE`（更新）操作。这类语句大量借鉴了连接（`join`）使用的概念，因此请务必熟悉前面第 2.8 节“使用连接执行多表检索”中讨论的内容。

要执行单表 `DELETE` 或 `UPDATE`，你只需引用一张表的列，因此无需使用表名来限定列名。例如，要删除表 `t` 中所有 `id` 值大于 100 的行，你可以编写如下的语句：

```sql
DELETE FROM t WHERE id > 100;
```

但如果你想要删除的行不是基于行本身的固有属性，而是基于它们与另一张表中行的关系怎么办？假设你想从表 `t` 中删除那些 `id` 值出现在另一张表 `t2` 中的行？
