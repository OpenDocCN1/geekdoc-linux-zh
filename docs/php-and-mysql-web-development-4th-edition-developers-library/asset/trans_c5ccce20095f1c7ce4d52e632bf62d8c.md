
## 注意

尽管 GROUP BY 列包含限定符，但对于此查询而言并非严格必要。GROUP BY 引用的是输出列，而名为 student_id 的输出列只有一个，因此 MySQL 知道你指的是哪一个。

如果我们只想了解哪些学生有缺勤记录，查询产生的输出是没有问题的。但如果我们将此列表交给学校办公室，他们可能会说：“其他学生呢？我们希望为每个学生都提供一个值，即使是那些在缺勤表中没有记录的学生。要编写此查询，请使用 FROM 子句中命名的表之间的 LEFT JOIN（而不是用逗号分隔它们），并使用 ON 子句来说明如何匹配两个表中的行。该查询如下所示：

```sql
mysql> SELECT student.student_id, student.name, COUNT(absence.date) AS absences
  -> FROM student LEFT JOIN absence
  -> ON student.student_id = absence.student_id
  -> GROUP BY student.student_id;
```

| student_id | name | absences |
| :---: | :---: | :---: |
| 1 | Megan | 0 |
| 2 | Joseph | 0 |
| 3 | Kyle | 1 |
| 4 | Katie | 0 |
| 5 | Abby | 1 |
| 6 | Nathan | 0 |
| 7 | Liesl | 0 |
| ... | | |

此前，在第 1.4.9.9 节“生成摘要”中，我们运行了一个查询，该查询对 score 表中的数据进行了数值表征。该查询的输出列出了事件 ID，但没有包括事件日期或类别，因为我们当时不知道如何将 score 表与 grade_event 表连接起来，以便将 ID 映射到日期和类别。现在我们知道如何做到了。以下查询与之前运行的查询类似，但它显示的是日期和类别，而不仅仅是数值型的事件 ID：

```sql
mysql> SELECT grade_event.date, grade_event.category,
  -> MIN(score.score) AS minimum,
  -> MAX(score.score) AS maximum,
  -> MAX(score.score)-MIN(score.score)+1 AS span,
  -> SUM(score.score) AS total,
  -> AVG(score.score) AS average,
  -> COUNT(score.score) AS count
  -> FROM score INNER JOIN grade_event
  -> ON score.event_id = grade_event.event_id
  -> GROUP BY grade_event.date;
```

| date       | category | minimum | maximum | span | total | average | count |
|------------|---------|--------|--------|------|-------|---------|-------|
| 2008-09-03 | Q       | 9      | 20     | 12   | 439   | 15.1379 | 29    |
| 2008-09-06 | Q       | 8      | 19     | 12   | 425   | 14.1667 | 30    |
| 2008-09-09 | T       | 60     | 97     | 38   | 2425  | 78.2258 | 31    |
| 2008-09-16 | Q       | 7      | 20     | 14   | 379   | 14.0370 | 27    |
| 2008-09-23 | Q       | 8      | 20     | 13   | 383   | 14.1852 | 27    |
| 2008-10-01 | T       | 62     | 100    | 39   | 2325  | 80.1724 | 29    |

你可以使用诸如 COUNT( ) 和 AVG( ) 之类的函数来生成跨多个列的摘要，即使这些列来自不同的表也是如此。以下查询确定每种事件日期和学生性别组合下的分数数量和平均分：

```sql
mysql> SELECT grade_event.date, student.sex,
  -> COUNT(score.score) AS count, AVG(score.score) AS average
  -> FROM grade_event INNER JOIN score INNER JOIN student
  -> ON grade_event.event_id = score.event_id
  -> AND score.student_id = student.student_id
  -> GROUP BY grade_event.date, student.sex;
```

| date       | sex | count | average |
|------------|----|-------|---------|
| 2008-09-03 | F  | 14    | 14.6429 |
| 2008-09-03 | M  | 15    | 15.6000 |
| 2008-09-06 | F  | 14    | 14.7143 |
| 2008-09-06 | M  | 16    | 13.6875 |
| 2008-09-09 | F  | 15    | 77.4000 |
| 2008-09-09 | M  | 16    | 79.0000 |
| 2008-09-16 | F  | 13    | 15.3077 |
| 2008-09-16 | M  | 12    | 12.9571 |
| 2008-09-23 | F  | 12    | 14.0833 |
| 2008-09-23 | M  | 15    | 14.2667 |
| 2008-10-01 | F  | 14    | 77.7857 |
| 2008-10-01 | M  | 15    | 82.4000 |

## 1.4 MySQL 教程

我们可以使用类似的查询来执行成绩管理项目任务之一：计算学期末每位学生的总得分。该查询如下所示：

```sql
mysql> SELECT student.student_id, student.name,
  -> SUM(score.score) AS total, COUNT(score.score) AS
  -> FROM grade_event INNER JOIN score INNER JOIN student
  -> ON grade_event.event_id = score.event_id
  -> AND score.student_id = student.student_id
  -> GROUP BY score.student_id
  -> ORDER BY total;
```

并不强制要求连接操作必须在不同的表之间执行。起初这似乎有些奇怪，但你也可以将表与其自身进行连接。例如，你可以通过将每位总统的出生地与每位其他总统的出生地进行比对，来确定是否有总统出生在同一个城市：

```sql
mysql> SELECT pl.last_name, pl.first_name, pl.state
  -> FROM president AS pl INNER JOIN president AS p2
  -> ON pl.city = p2.city AND pl.state = p2.state
  -> WHERE (pl.last_name <> p2.last_name OR pl.first_name <> p2.first_name)
  -> ORDER BY state, city, last_name;
```

| last_name | first_name | city | state |
| :--- | :--- | :--- | :--- |
| Adams | John Quincy | Braintree | MA |
| Adams | John | Braintree | MA |

这个查询有两个棘手的地方：

- 需要引用同一表的两个实例，因此我们创建了表别名 (pl, p2) 并使用它们来消除对该表列引用的歧义。与列别名一样，在命名表别名时，AS 关键字是可选的。
- 每位总统的行都会与其自身匹配，但我们不希望在输出中看到这种情况。WHERE 子句通过确保被比较的行属于不同的总统，从而禁止行与其自身匹配。

类似的查询可以找到出生在同一天（同月同日）的总统。但是，不能直接比较出生日期，因为那样会漏掉出生年份不同的总统。相反，请使用 MONTH( ) 和 DAYOFMONTH( ) 来比较出生日期的月份和日期：

```sql
mysql> SELECT pl.last_name, pl.first_name, pl.birth
  -> FROM president AS pl INNER JOIN president AS p2
  -> WHERE MONTH(pl.birth) = MONTH(p2.birth)
  -> AND DAYOFMONTH(pl.birth) = DAYOFMONTH(p2.birth)
  -> AND (pl.last_name <> p2.last_name OR pl.first_name <> p2.first_name)
  -> ORDER BY pl.last_name;
```

| last_name | first_name | birth      |
| :--- | :--- | :--- |
| Harding | Warren G. | 1865-11-02 |
| Polk | James K. | 1795-11-02 |

使用 DAYOFYEAR() 而不是 MONTH() 和 DAYOFMONTH() 的组合会使查询更简单，但在比较闰年日期与非闰年日期时会产生错误结果。

另一种多表检索方式使用“子查询”，即嵌套在另一个 SELECT 中的一个 SELECT。有几种类型的子查询，将在第 2.9 节“使用子查询执行多表检索”中进一步讨论。目前，举几个例子就足够了。假设你想找出那些出勤率完美的学生。这相当于确定哪些学生未出现在缺勤表中，可以这样做：

```sql
mysql> SELECT * FROM student
  -> WHERE student_id NOT IN (SELECT student_id FROM absence);
```

| name | sex | student_id |
| :--- | :--- | :--- |
| Megan | F | 1 |
| Joseph | M | 2 |
| Katie | F | 4 |
| Nathan | M | 6 |
| Liesl | F | 7 |

嵌套的 SELECT 确定存在于缺勤表中的 student_id 值的集合，而外层的 SELECT 检索与这些 ID 不匹配的学生行。

子查询还为第 1.4.9.8 节“设置和使用用户定义变量”中提出的问题提供单语句解决方案，该问题询问哪些总统出生在安德鲁·杰克逊之前。原始解决方案使用了两个语句和一个用户变量，但可以使用子查询如下所示完成：

```sql
mysql> SELECT last_name, first_name, birth FROM president
  -> WHERE birth < (SELECT birth FROM president
  -> WHERE last_name = 'Jackson' AND first_name = 'Andrew');
```

| last_name | first_name | birth      |
| :--- | :--- | :--- |
| Washington | George | 1732-02-22 |
| Adams | John | 1735-10-30 |
| Jefferson | Thomas | 1743-04-13 |
| Madison | James | 1751-03-16 |
| Monroe | James | 1758-04-28 |

