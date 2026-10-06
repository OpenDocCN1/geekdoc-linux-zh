
量化谓词用于将一个值或多个值与一组值进行比较。在图 6–13 中显示了量化谓词的语法图（完整讨论请参阅 DB2 SQL 参考）。表达式的右侧是一个子选择、子查询、`WHERE` 子句，或通过集合操作符结合的这两者。

让我们检查 `SELECT` 语句中量化谓词的使用。首先查看原始查询：

```sql
SELECT cid, lname, fname FROM db2cert.candidate
```

| CID | LNAME | FNAME |
|---|---|---|
| 111 | Wong | Bill |
| 222 | Baklarz | George |
| 333 | Visser | Susan |
| 444 | Sheffield | Glen |
| 555 | Stittle | Jim |
| 666 | Street | Kevin |
| 777 | Nicol | Paul |

**图 6–14** 简单查询 (1)

```sql
SELECT cid FROM db2cert.test_taken
```

**图 6–15** 简单查询 (2)

```sql
SELECT cid, lname, fname FROM db2cert.candidate c
WHERE cid = SOME
  (SELECT tt.cid FROM db2cert.test_taken tt
  WHERE c.cid = tt.cid)
```

**图 6–16** 在 SELECT 语句中使用量化谓词

当指定 `SOME` 或 `ANY` 时，谓词对于子选择返回的至少一个值为真。当指定 `ALL` 时，由于我们定义的表之间的引用完整性约束，谓词对于子选择返回的每个值都真，在 `test_taken` 表中的 `cid` 值在 `candidate` 表中没有对应值。

# CASE 表达式

你可以使用 `CASE` 表达式为你的 SQL 语句和输出添加逻辑。考虑生成通过 DB2 Fundamentals 考试的候选人列表。

在报告中，你可能想打印测试的分数，但与其打印分数，你可能想打印消息。如果分数低于格分，你可能想打印 "Not Passed"。如果是在格分和 90 之间，你可能想打印 "Passed"，如果分数高于 90，你可能想打印 "Excellent"。以下使用 `CASE` 表达式的 SQL 语句实现了此：

```sql
SELECT fname, lname,
       CASE
           WHEN integer(SCORE) < 65 THEN 'Not Passed'
           WHEN SCORE <= 90 THEN 'Passed'
           ELSE
               'Excellent'
       END
FROM candidate c, test_taken tt
  WHERE c.cid=tt.cid
  AND char(number)='500'
```

**图 6–17** CASE 表达式

## 嵌套表表达式 (Nested Table Expressions)

嵌套表表达式是一种特殊的子查询。该子查询用于 SQL 语句的 FROM 子句。嵌套表表达式创建了局部临时表，这些表仅在定义它们的 SQL 语句中可见。

这些子查询可以被视为临时视图。你可以使用嵌套表表达式从分组后的表中进行查询，或者获得你期望从视图中得到的相同结果。

考虑获取 DB2 认证考试最高平均分的问题。为了收集此结果，你必须首先获取平均分，然后必须从该列表中选择最大值。

让我们使用嵌套表表达式来完成此请求：

```sql
SELECT MAX(avg_score)
FROM (
  SELECT number,
    avg(integer(score)) as avg_score
  FROM test_taken
  GROUP BY number
) AS averages
```

图 6–18 使用嵌套表表达式

在例例（图 6–18）中，嵌套子查询将创建一个临时表，外部查询将使用该表来获取最高平均分。这个临时表被称为 `averages`。

`number` 列被包含在子查询中，以便收集每项考试的平均分。子查询完成后，外部 SELECT 将能够获取嵌套表表达式中计算出的平均值的最大值。

使用嵌套表表达式相比视图的优势是，嵌套表表达式仅在查询执行期间存在，因此你不需要担心它们的维护。它们减少了对系统目录表的竞争，而且由于它们是在执行时创建的，因此可以使用主机变量进行定义。

**注意：** `TABLE` 子句也可以用于指示随后的子查询将创建一个临时表。该关键字也用于指示 TABLE 用户定义函数（UDF）。有关 UDF 的信息，请参阅第 325 页的“高级 SQL”。

## 标量全选择 (Scalar Fullselect)

标量全选择是一个只返回一个值的 SELECT 语句。这种类型的 SELECT 可以用于 SQL 语句的不同部分。它可以用于 select 列表，也可以用于 WHERE 子句。

标量全选择可用于将分组后的信息（如平均值或总和）与详细信息合并到单个查询中。

有时，你可能需要在报告中包含基于输入表信息的行数据。例如，你可能想要一份显示候选人 ID、平均分和 DB2 认证考试最高分的报告。如果没有临时表或视图的帮助，就无法无法收集这些信息。让我们看看如何使用标量全选择辅助检索这些数据。

```sql
SELECT cid,number,score,
(SELECT AVG(integer(score))
FROM test_taken) AS AVG_Score,
(SELECT MAX(integer(score))
FROM test_taken) AS MAX_Score
```

**图 6–19** 合并详细信息和聚合信息

在图 6–19 所示的示例中，我们使用两个标量全选择来检索聚合数据的信息。

第一个标量全选择计算 DB2 认证考试的平均分，第二个计算最高分。

观察产生平均值和最大值的 SQL 语句全它们。它们是只返回一个值的完整 SQL 语句。

现在，让我们扩展此 SQL 以计算每个候选人的平均分和最高分。

要完成此请求，你需要使用相关子查询。这是因为你需要确保 SELECT 语句每次只返回一个值。

相关子查询将允许你为每项 DB2 认证考试生成平均分和最高分：

```sql
SELECT cid,number,score,
(SELECT AVG(integer(score)))
FROM test_taken tt1
WHERE tt1.number=tt.number
AS AVG_Score,
(SELECT MAX(integer(score)))
FROM test_taken tt2
WHERE tt2.number=tt.number
AS MAX_Score
FROM test_taken tt
```

**图 6–20** 使用相关标量选择

检查图 6–20 示例中的 WHERE 子句。它们都引用了外部 SELECT 语句的表。WHERE 子句用于为 `test_taken` 表中的每个测试编号获取单独的平均值和最大值。

现在，让我们使用标量子查询创建一个列表，包含得分高于 DB2 基础考试平均分的候选人。

```sql
SELECT fname,lname,score
FROM candidate c, test_taken tt
WHERE c.cid=tt.cid
AND integer(tt.score) > (SELECT AVG(integer(score)))
FROM test_taken
WHERE number=test_id('500'))
```

**图 6–21** 在 WHERE 子句中使用标量子查询

在图 6-21 中，标量子查询被被用在 WHERE 子句中。该标量子查询计算 DB2 基础考试的平均分。

从标量子查询返回的值将与候选人的得分进行比较。通过这种方式，我们检索出得分高于平均值的候选人。

## 公用表表达式 (Common Table Expressions)

公用表表达式可以在 SQL 语句中多次引用的局部临时表。然而，该临时表仅在定义它的 SQL 语句持续期间存在。公用表表达式提供了之前过的嵌套表表达式的许多优势。

每当你引用公用表表达式，结果都是相同的。考虑一个列出在每个测试中获得最高分的候选人的报告。这可以使用三个公用表来实现。它们将被分别调用 `MAX500`、`MAX501` 和 `MAX502`。每一个都对应 DB2 考试的最高分。

在计算出每项测试的最高分后，使用这些值搜索特定的测试。示例如图 6–22 所示。

```sql
WITH MAX500 AS
(SELECT MAX(integer(score)) AS M500
FROM test_taken
WHERE number=test_id('500')),
MAX501 AS
(SELECT MAX(integer(score)) AS M501
FROM test_taken
WHERE number=test_id('501')),
MAX502 AS
(SELECT MAX(integer(score)) AS M502
FROM test_taken
WHERE number=test_id('502'))

SELECT fname, lname,score
FROM max500,max501,max502,candidate c, test_taken tt
WHERE c.cid=tt.cid
AND ((integer(score)=M500 and number=test_id('500'))
OR (integer(score)=M501 and number=test_id('501'))
OR (integer(score)=M502 and number=test_id('502')));
```

图 6–22 使用公用表表达式

`WITH` 子句用于定义公用表表达式。图 6–22 所示的示例定义了三个不同的公用表表达式：`MAX500`、`MAX501` 和 `MAX502`。观察用于分隔每个公用表表达式定义的逗号。

公用表表达式被用于其定义后的 SQL 语句。该 SQL 语句像对待普通表一样对待公用表表达式。

你可以根据需要多次引用公用表表达式。你甚至可以基于之前创建的公用表表达式创建一个公用行表达式。然而，你只能在定义它们的 SQL 语句中使用它们。

## 集合运算符 (Set Operators)

SQL 提供了一组用于实现关系运算的并（`UNION` 运算符）、交集（`INTERSECT` 运算符）和差集（`EXCEPT` 运算符）。

### 并 (Union)

`UNION` 操作允许将两个或多个不同 SQL 语句的结果合并为一个结果集。可以使用 `UNION` 运算符合并多个表或 SQL 语句；唯一的限制是每个表或 SQL 语句必须具有相同的列类型、数量和顺序。

假设你想合并每个 DB2 认证考试的最低分和最高分，并添加一个指示哪些值是最大值和最低值的字符串常量。

```sql
SELECT number,'Minimum:', MIN(integer(score))
FROM test_taken
GROUP BY number
UNION
SELECT number, 'Maximum:', MAX(integer(score))
FROM test_taken
GROUP BY number
ORDER BY number,2
```

图 6–23 UNION 运算符

`UNION` 操作符将两个或多个单独查询的结果显示为单一结果。在我们的示例中，第一个查询计算 `test_taken` 表的最低分。第二个查询计算最高分值。

两个查询具有相同的类型、顺序和列数。

在图 6–23 中，这两个 SQL 语句非常相似。然而，你可以使用 `UNION` 操作符结合两个完全不同的查询。只需记住结果行的限制即可。

`UNION` 操作符会移除结果集中的重复行。但在某些情况下，你可能需要列出 SQL 语句处理的所有行。

SQL 了一个了一个操作符子句，允许你保留 `UNION` 操作中涉及的所有行。这就是 `ALL` 子句。让我们在 `candidate` 表中创建所有名字（`fname`）和姓（`lname`）的列表。在图 6–24 所示的示例中，我们想要所有以字母 G 开头的名字，以及参加过 DB2 管理考试的候选人的所有姓。

这个示例无法使用 `OR` 操作符来处理，因为我们并不对那些参加过 DB2 管理考试的候选人的名字感兴趣。由于名字可能与姓相同，我们使用 `UNION ALL` 操作符来显示所有行。

```sql
SELECT fname FROM candidate
WHERE fname like'G%'
UNION ALL
SELECT lname FROM candidate c,test_taken tt
WHERE c.cid=tt.cid
AND char(number) = '501'
```

**图. 6–24** UNION ALL 示例

> **注意：** 始终尝试编写 `UNION ALL`。只有在不需要重复项时才编写 `UNION`。`UNION ALL` 子句提供了更好的性能。然而，你并不能总是用 `UNION` 替换 `UNION ALL`。

`UNION ALL` 操作为我们提供了一种强大的机制，正如我们将在讨论高级 SQL 时将看到的，在编写递归查询时是必须的。

### 交集 (INTERSECT 操作符)

交集集合操作在 DB2 中通过 `INTERSECT` 操作符实现。使用 `INTERSECT`，我们可以找到属于两个不同结果集的元素。

例如，我们想要一个在 `test_taken` 表和 `candidate` 表中都存在的候选人 ID 列表。这个需求可以被视为 `candidate IDs` 集合与 `test_taken` 中存在的 `candidates IDs` 集合的交集。

```sql
SELECT cid FROM candidate
INTERSECT
SELECT cid FROM test_taken
```

像 `union` 操作符一样，还有一个 `INTERSECT ALL` 操作符。如果你使用 `INTERSECT ALL` 操作符，结果集将返回重复值，这通常是理想的。

此示例所示的 SQL 语句等同于使用选择列表中的 `DISTINCT` 子句在 `candidate` 表和 `test_taken` 表进行连接操作。

### 差集 (Except 操作符)

差集集合操作是两个集合之间交集的补集。它在 DB2 中通过 `EXCEPT` 操作符实现。使用差集操作，我们可以找出结果集中的哪些元素不在另一个结果集中。

这一次，我们想知道哪些候选人 ID 不在 `test_taken` 表中。这实际上是：“向我显示所有候选人 ID，排除那些出现在 `test_taken` 表中的候选人 ID。”

使用 `EXCEPT` 操作符的查询如例所示：

```sql
SELECT cid FROM candidate
EXCEPT
SELECT cid FROM test_taken
```

示例的第一部分检索所有候选人 ID。查询的第二部分检索存在于 `test_taken` 表中的候选人 ID。最后，`EXCEPT` 操作执行差集操作，过滤掉那些不在 `test_taken` 表中的候选人 ID。如果没有 `EXCEPT` 操作符，查询将变得复杂。与其他集合操作符一样，还有一个 `EXCEPT ALL` 操作符，它不会从结果中消除重复。

> **注意：** 集合操作符（如 `UNION`、`INTERSECT` 和 `EXCEPT`）两个选择列表中的列必须具有相同的列结构。

## 数据修改

到为止，我们讨论了基本的 `SELECT` 语句。`SELECT` 语句允许你从数据库表中检索数据，并假设数据已经加载到表中。现在我们将集中于如何使用 SQL 将数据放入数据库表中。有三个主要的语句可以添加和更改存储在 DB2 数据库表中的数据。它们是 `INSERT`、`DELETE` 和 `UPDATE` 语句。

要执行这些操作，你必须对访问的表具有所需的权限。通常，这些权限的执行得更严格，因为它们允许最终用户修改数据记录。

### 插入数据记录

为了最初向 DB2 表填充数据，可以使用 `INSERT` 语句一次存储一条数据记录。该语句可以目标是直接向基表插入数据，或者可以使用视图。如果使用视图作为目标，请记住基表才是存储实际数据的地方。

使用 `INSERT` 语句填充的每一行都必须符合表约束、数据类型验证、动态（触发器）约束和引用完整性约束。如果在处理 `INSERT` 语句期间违反了这些任何一个条件，将发生 SQL 错误。

> 注意：请记住，你必须拥有必要的视图或表权限来执行 `INSERT` 语句。

第一个示例是一个简单的 `INSERT` 语句。该语句将为 DB2 数据传播 (#508) 考试的数据插入 `test` 表。

```sql
INSERT INTO db2cert.test
(number,name,type,cut_score,length,totaltaken,totalpassed) VALUES
('508','DB2 Data Propagation','P',NULL,90,0,0)
```

在这个示例中，我们指定了所有列。

### 操作对象

在接下来的示例中，我们指定了列的数量。根据你的列定义，你可能需要为列提供值。这意味着你必须为定义为 `NOT NULL` 的列提供值。

> **注意：** `VALUES` 子句中的列数必须与 `INSERT` 语句中的列数匹配。

让我们向 `test` 表插入一行。在这个示例中，我们使用 `DEFAULT` 关键字。只有当省略的列允许空或具有默认值时，这种方法才有效。当你向表的所有列插入数据时，如下所示。

```sql
INSERT INTO db2cert.test
(number,name,type,cut_score,length,totaltaken,totalpassed)
```

### 向特定列插入数据

有时你需要向特定列添加数据。未包含在 `INSERT` 语句中的每一列将接收其默认值。

这种操作只有在省略的列允许空或具有默认值时才能完成。这意味着你必须为定义为 `NULL` 的列提供值。
