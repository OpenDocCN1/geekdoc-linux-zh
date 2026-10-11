

## 2.8 使用连接执行多表检索

与 INNER JOIN 类似，LEFT JOIN 可以使用 ON 子句或 USING() 子句来指定匹配条件。与 INNER JOIN 一样，无论连接的两个表中的列名是否相同，都可以使用 ON，但 USING() 要求列名必须相同。

LEFT JOIN 有几个同义词和变体。LEFT OUTER JOIN 是 LEFT JOIN 的同义词。MySQL 还支持一种 ODBC 风格的 LEFT OUTER JOIN 表示法，该方法使用花括号和 `OJ`（“外部连接”）：

```text
mysql> SELECT t1.* FROM { OJ t1 LEFT OUTER JOIN t2 ON t1.ii = t2.ij }
       -> WHERE t2.i2 IS NULL;
----------
| ii | c1 |
----------
| 1  | a  |
----------
```

NATURAL LEFT JOIN 类似于 LEFT JOIN；它执行 LEFT JOIN，匹配左右表中所有具有相同名称的列。（因此，不需要给出 ON 或 USING 子句。）

如前所述，LEFT JOIN 对于回答“哪些值是缺失的？”这类问题非常有用。让我们将这个原则应用到 sampdb 数据库中的表中，并考虑一个比之前使用 t1 和 t2 所示示例更复杂的例子。

对于第 1 章中首次提到的成绩管理项目，我们有一个列出学生的 student 表，一个列出已发生成绩事件的 grade_event 表，以及一个列出每个学生每个成绩事件分数的 score 表。然而，如果某个学生在某次测验或考试当天生病，score 表中将不包含该学生在该事件中的任何分数。在这种情况下应该补考，但我们如何找到这些缺失的行呢？

问题是确定哪些学生在给定的成绩事件中没有分数，并且要对每个成绩事件都这样做。换一种说法，我们要找出哪些学生和成绩事件的组合不存在于 score 表中。“哪些值不存在”这种措辞是一个提示，表明我们需要使用 LEFT JOIN。不过，这里的连接不像之前的示例那样简单：我们不仅仅是在寻找单个列中不存在的值；我们在寻找两列的组合。我们要找的组合是所有学生/事件组合。这些是通过将 student 表连接到 grade_event 表生成的：

```text
FROM student INNER JOIN grade_event
```

然后，我们取该连接的结果，并与 score 表执行 LEFT JOIN，以查找学生 ID/事件 ID 对的匹配项：

```text
FROM student INNER JOIN grade_event
LEFT JOIN score ON student.student_id = score.student_id
AND grade_event.event_id = score.event_id
```

请注意，`ON` 子句允许根据连接早期提到的不同表中的匹配项来连接 `score` 表中的行。这是解决此问题的关键。`LEFT JOIN` 强制为 `student` 和 `grade_event` 表交叉连接生成的每一行生成一行，即使不存在对应的 `score` 表行。这些缺失分数行的结果集行可以通过 `score` 表中的所有列都为 `NULL` 这一事实来识别。我们可以通过在 `WHERE` 子句中添加条件来识别这些行。`score` 表中的任何列都可以，但由于我们在寻找缺失的分数，从概念上最清晰的是测试 `score` 列：

```text
WHERE score.score IS NULL
```

我们还可以使用 `ORDER BY` 子句对结果进行排序。最合理的两种排序方式分别是按每个学生的事件和按每个事件的学生。我将选择第一种：

```text
ORDER BY student.student_id, grade_event.event_id
```

现在，我们只需要命名要在输出中看到的列，就完成了。以下是最终语句：

```sql
SELECT
    student.name,  student.student_id,
    grade_event.date, grade_event.event_id,  grade_event.category
FROM
    student INNER JOIN grade_event
    LEFT JOIN score ON student.student_id = score.student_id
                AND grade_event.event_id = score.event_id
WHERE
    score.score IS NULL
ORDER BY
    student.student_id, grade_event.event_id;
```

运行该查询产生以下结果：

| name | student_id | date | event_id | category |
|---|---|---|---|---|
| Megan | 1 | 2008-09-16 | 4 | Q |
| Joseph | 2 | 2008-09-03 | 1 | Q |
| Katie | 4 | 2008-09-23 | 5 | Q |
| Devi | 13 | 2008-09-03 | 1 | Q |
| Devi | 13 | 2008-10-01 | 6 | T |
| Will | 17 | 2008-09-16 | 4 | Q |
| Avery | 20 | 2008-09-06 | 2 | Q |
| Gregory | 23 | 2008-10-01 | 6 | T |
| Sarah | 24 | 2008-09-23 | 5 | Q |
| Carter | 27 | 2008-09-16 | 4 | Q |
| Carter | 27 | 2008-09-23 | 5 | Q |
| Gabrielle | 29 | 2008-09-16 | 4 | Q |
| Grace | 30 | 2008-09-23 | 5 | Q |

这里有一个细微的要点。输出显示了学生 ID 和事件 ID。student_id 列出现在 student 和 score 两个表中，因此乍一看，你可能会认为输出列列表可以命名 student.student_id 或 score.student_id 中的任意一个。事实并非如此，因为能够找到我们感兴趣的行的整个基础是，`score` 表的所有列都由 LEFT JOIN 作为 NULL 返回。选择 score.student_id 将在输出中仅生成一列 NULL 值。决定显示哪个 event_id 列也适用同样的原则。它出现在 grade_event 和 score 两个表中，但查询选择 grade_event.event_id，因为 score.event_id 的值将始终为 NULL。

## 2.9 使用子查询执行多表检索

子查询支持是一项功能，允许在一个括号内编写一个 SELECT 语句并将其嵌套在另一个语句内部。以下是一个示例，它查找对应于测试（'T'）的成绩事件行的 ID，并使用它们来选择这些测试的分数：

```sql
SELECT * FROM score
WHERE event_id IN (SELECT event_id FROM grade_event WHERE category = 'T');
```

子查询可以返回不同类型的信息：

- 标量子查询返回单个值。
- 列子查询返回一列中的一个或多个值。
- 行子查询返回一行中的一个或多个值。
- 表子查询返回一个包含一行或多行、一列或多列的表。

子查询的结果可以通过不同的方式进行测试：

- 标量子查询的结果可以使用相对比较运算符（如 = 或 <）进行评估。
- IN 和 NOT IN 测试某个值是否存在于子查询返回的值集合中。
- ALL、ANY 和 SOME 将某个值与子查询返回的值集合进行比较。
- EXISTS 和 NOT EXISTS 测试子查询结果是否为空。

标量子查询的限制最为严格，因为它只产生一个值。但作为结果，标量子查询可以在最广泛的各种上下文中使用。基本上，你可以在任何可以使用标量操作数的地方使用它们，例如表达式的项、函数参数或输出列列表中。返回更多信息的列、行和表子查询不能在需要单个值的上下文中使用。

子查询可以是相关的，也可以是不相关的。这取决于子查询是否引用外部查询中的值并依赖于这些值。

你可以在 SELECT 以外的语句中使用子查询。然而，对于修改表的语句（INSERT、REPLACE、DELETE、UPDATE、LOAD DATA），目前有一个限制，即子查询不能引用正在被修改的表。

在某些情况下，子查询可以重写为连接。如果你正在编写需要在旧版本 MySQL 服务器上运行的查询，或者你想看看 MySQL 优化器在处理连接时是否比处理子查询更好，你可能会发现子查询重写技术很有用。

以下章节讨论了用于测试子查询结果的操作类型，如何编写相关子查询，以及如何将子查询重写为连接。

### 2.9.1 使用相对比较运算符的子查询

=、<>、>、>=、< 和 <= 运算符执行相对值比较。当与标量子查询一起使用时，它们查找外部查询中所有与子查询返回的值具有特定关系的行。例如，要确定在 '2008-09-23' 举行的测验的分数，请使用标量子查询确定测验事件 ID，然后在外部 SELECT 中将该 ID 与分数行进行匹配：

```sql
SELECT * FROM score
WHERE event_id =
(SELECT event_id FROM grade_event
 WHERE date = '2008-09-23' AND category = 'Q');
```

在这种语句形式中，子查询之前有一个值和相对比较运算符，子查询必须产生单个值。也就是说，它必须是标量子查询；如果它产生多个值，语句将失败。在某些情况下，通过限制子查询结果来使用 LIMIT 1 可能适合满足单值要求。

使用相对比较运算符的标量子查询对于解决那些你本想使用聚合函数但 WHERE 子句中不能使用的問題很有用。例如，要确定 president 表中的哪位总统出生最早，你可能会尝试这种语句：

```sql
SELECT * FROM president WHERE birth = MIN(birth);
```

这不起作用，因为你不能在 WHERE 子句中使用聚合函数。WHERE 子句确定选择哪些行，但 MIN() 的值只有在行已经被选择之后才知道。然而，你可以使用子查询来生成最小出生日期，如下所示：

```sql
SELECT * FROM president
WHERE birth = (SELECT MIN(birth) FROM president);
```

