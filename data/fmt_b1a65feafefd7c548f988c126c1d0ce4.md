
```
SELECT lname, fname, hphone
FROM db2cert.candidate c, db2cert.test_taken tt
WHERE c.cid=tt.cid
AND tcid=db2cert.center_id('TR01')
ORDER BY 1 DESC, 2
```

在此示例中，使用列位置指定排序顺序。因此，查询结果与上一个示例完全相同。

你可以使用别名重命名列。该别名可以在 `ORDER BY` 子句中被引用。

> **注意：** `ORDER BY` 子句必须是 SQL 语句中的最后一个子句。

## 派生列

在某些情况下，你需要对数据进行计算。SQL 语言内置了一些基本的数学和字符串函数。数学运算包括标准的加法、减法、乘法除法。

计算可以在 SQL 语句的 `WHERE` 子句或 `SELECT` 列表中定义。假设你需要计算 DB2 测试的通过率。通过率被定义为通过测试的候选人百分比（`totalpassed*100/totaltaken`）。以下 SQL 语句将为我们完成 500 号测试的计算：

```
SELECT number, totalpassed*100/totaltaken
FROM test
WHERE number=test_id('500')
```

在此示例中，输出列表的第二列是一个计算列。记住，如果你想将此列用于 `ORDER BY` 子句，必须使用列位置，除非你对其进行了命名（正如我们现在讨论的那样）。

> 注意：偶尔，派生列的结果可能不会按预期显示。使用 `totalpassed*100/totaltaken` 的示例将检索到值 66。由于 `totalpassed` 和 `totaltaken` 列都是整数，最终结果也是整数，小数部分被丢弃。如果这不是你想要的结果，你应该使用其他函数（如 `decimal`）来更改计算执行或显示的方式。

## 派生/计算列的命名

你可以为任何表达式指定列名。通过为派生（计算）列提供名称，`ORDER BY` 子句可以引用该派生名称，使 SQL 语句更具可读性。

以下 SQL 计算了通过 DB2 认证考试的人数百分比，并按通过率降序排列输出：

## 数据检索

```
SELECT number,totalpassed*100/totaltaken AS PassedRate
FROM test
ORDER BY PassedRate DESC
```

`AS` 子句用于重命名 `select` 列表中元素的默认名称。在此示例中，我们为列 `totalpassed` 除以 `totaltaken` 的结果命名为 `PassedRate`。命名的列在查询中用于指定用于输出排序的列。

## DB2 函数

在 DB2 中，提供了不同类型的函数。例如，DB2 提供的两种函数是标量函数和列函数（此处不讨论第三种函数表函数——有关此函数的详细信息请参阅 DB2 UDB V7.1 SQL 参考》）：

- 标量函数（也称为行函数）为结果表中的每一行提供一个结果。标量函数可以用任何允许表达式的地方。

- 列函数（也称为向量函数）。它们与一组行一起工作并提供结果。该组使用 `FULLSELECT` 指定，并可选地使用 `GROUP BY` 子句进行分组。

在本节中，我们将向你介绍 DB2 提供的一些 SQL 函数。SQL 函数按其实现类型分类。函数要么是内置的，要么是 DB2 的扩展，被称为用户定义函数 `UDFs`。

- 内置函数定义在 SQL 标准中，并由 DB2 提供。这些可以是标量函数、列函数或表函数。

- 用户定义函数 `UDFs` 未定义在 SQL 标准中，因为它们是当前 SQL 语言的扩展。这些函数可以由 DB2 管理员或应用程序开发人员开发。一旦了 UDF，任何具有适当权限的终端都可以调用它们。DB2 提供的一些新函数是标量 UDF。模式架构名为 `SYSFUN` 的函数由 DB2 提供。

> 注意：有关 UDFs 的详细信息，请参阅第 325 页的“高级 SQL”。

## 标量函数

标量函数应用于数据的每行，并产生每行的结果。标量函数可以用任何允许表达式的地方。如果我们想提供月份名称，可以使用 `MONTHNAME`。以下示例检索了参加考试的月份：

```
SELECT fname, MONTHNAME(date_taken)
FROM candidate c, test_taken tt
WHERE c.cid=tt.cid
```

以下示例获取任何 DB2 考试的最时长：

```
SELECT MAX(smallint(length)) FROM test
```

接下来的示例计算了所有测试中心的平均座位数。注意此示例中使用了列函数 `AVG`：

```
SELECT AVG(noseats) FROM test_center
```

## 列函数

列函数为一组行提供单个结果。许多常见查询可以使用列函数满足，它们包含了常见任务，例如查找一组数据的最小值、最大值或平均值。

## 分组值

许多查询需要某种程度的聚合数据。这在 SQL 中通过使用 `GROUP BY` 子来实现。

以下 SQL 语句获取每个国家的平均座位数：

```
SELECT country, AVG(noseats) FROM test_center GROUP BY country
```

此 SQL 语句获取每个国家的平均座位数，`GROUP BY` 子句告诉 DB2 将分组列表中指定列具有相同值的行分组在一起。在我们的示例中，我们将国家分不同的子集。随着子集的创建，DB2 计算每个组或每个子集的平均值，在这种情况下，是按每个国家进行计算。

## 第 6 章 操作数据库对象

当你将向量函数与其他元素（如列名、标量函数或计算列）结合时，必须使用 `GROUP BY` 子句。在这种情况下，你必须在 group by 列表中包含除列以外的所有元素。`GROUP BY` 列表中可以省略的唯一元素是常量值。

下一个 SQL 语句获取了一个包含 DB2 认证考试平均分数和最小测试长度的列表。我们如下按考试类型对此列表进行分组：

```
SELECT type, AVG(integer(cut_score)),
(smallint(length))
FROM test
GROUP BY type
```

可以使用 `ORDER BY` 子句对上一个示例的输出进行排序。注意，`ORDER BY` 子句应该是 SQL 语句中的最后一个子句。

在线分析处理（OLAP）应用程序在相同数据中使用不同级别的分组。DB2 通过实现超级分组或聚合功能来支持 OLAP 需求。面向 OLAP 的分组函数将在第 325 页的“高级 SQL”中讨论。

# 限制数据集的使用

到为止，我们已经讨论了如何根据行条件限制输出。在 SQL 中，也可以使用向量函数和 `GROUP BY` 子句来限制输出。

假设你想要一个所有参加过五场以上 DB2 认证考试的测试中心列表。

为了方便理解，让我们先获取每个测试中心参加的测试次数。

```
SELECT tcid, count(*) FROM test_taken GROUP BY tcid
```

我们使用 `COUNT` 函数来获取每个测试中心参加的测试总数。当你在 `COUNT` 函数中使用星号（`*`）时，表示你想要获取表中符合 SQL 语句中建立的标准的行数。在这个示例中，我们按 `tcid` 分组，因为在 `test_taken` 表中所有测试中心都有多次出现。`test_taken` 表中每个已参加的 DB2 认证考试都有一个条目。

最后，输出限制在那些参加了超过四场考试的测试中心。

```
SELECT tcid FROM test_taken
GROUP BY tcid HAVING COUNT(*) > 4
```

这引入了 `HAVING` 子句。`HAVING` 子句等同于组和向量函数的 `WHERE` 子句。`HAVING` 子句将结果集限制为仅满足其中指定条件的组。

在我们的示例中，只有参加了四场以上 DB2 认证考试的测试中心会被显示。

# 消除重复项

当你执行查询时，可能会在结果集中得到重复行。SQL 语言提供了一个特殊的子句来从输出中删除重复行。

以下 SQL 生成所有参加过测试的候选人的姓名和电话列表。在下面的示例中，我们使用 `DISTINCT` 子句从输出列表中消除重复行。

```
SELECT DISTINCT fname,wphone,hphone
FROM candidate c,test_taken tt
WHERE c.cid=tt.cid
```

`DISTINCT` 子句也可以与 `COUNT` 函数一起使用。当你在 `COUNT` 函数内部 `DISTINCT` 时，它不会计算特定列的重复条目。

假设你想统计有多少个不同的测试中心注册了候选人。

```
SELECT COUNT(DISTINCT char(tcid)) FROM test_taken
```

这个示例提供了在测试表中注册的测试中心数量。请记住，所有注册了 DB2 认证考试的候选人都均存储在该表中。

请确保你理解 `COUNT(*)` 和 `COUNT(DISTINCT colname)` 之间的区别。它们的语法非常相似，但功能不同。

# 搜索字符串模式

SQL 有一个强大的谓词，允许你搜索字符字符串列中的搜索模式。这就是 `LIKE` 谓词。

假设你想生成一个第一个名字以字母 G 开头的候选人列表。

```
SELECT fname,lname,wphone,hphone FROM candidate
WHERE fname LIKE 'G%' ORDER BY lname, fname
```

在此查询中，我们在 `LIKE` 谓词中使用了一个通配符字符。

在 SQL 中，百分号（`%`）是零或多个字符的占位符。搜索字符串（`G%`）可以替换为如 George、Gary、Ginger 和 Susan 等名字（由于百分号可以替换零或多个字符，搜索字符串也可以是单个字母 G）。

百分号可以用于搜索字符串的任何位置。它也可以根据需要使用任意次数。百分号不区分大小写，因此它可以代表大写或小写字母。然而，包含在你的搜索字符串中的常数字符是区分大小写的。

另一个与 `LIKE` 谓词一起使用的通配符是下划线（`_`）。该字符替换且仅替换一个字符。下划线字符可以代表任何字符。然而，下划线字符不能替换空字符。

之前的 SQL 可以被修改为包含所有候选人的姓名，以及那些名字第二个字母是小写字母“a”的候选人的电话。

```
SELECT fname, lname, wphone, hphone FROM candidate
WHERE fname LIKE '_a%' ORDER BY lname, fname
```

这个示例使用了两个与 `LIKE` 谓词配合的通配符字符。在这个示例中，搜索字符串可以包含名字，如 Paul、Gabriel 或 Natalie。（第一个字符可以是任何字符，小写字母“a”是字符串中的第二个字符，且字符串到此结束。）

# 搜索范围

SQL 还提供了 `RANGE` 运算符。该运算符用于限制在特定范围内的行。考虑列出认证考试分数在 60 到 75 之间的人员。

```
SELECT DISTINCT fname, lname,wphone,hphone
FROM candidate c,test_taken tt
WHERE c.cid=tt.cid
AND integer (score) BETWEEN 60 AND 75
```

`BETWEEN` 运算符也可以用于字符范围。除了分数要求外，此示例修改了 SQL 以包含姓氏在 B 和 G 之间的候选人。

```
SELECT DISTINCT fname, lname,wphone,hphone
FROM candidate c,test_taken tt
WHERE c.cid=tt.cid
AND lname BETWEEN 'B' AND 'G'
```

在这个示例中，第二个 `BETWEEN` 谓词包含字符值。我们需要指定值以包含所有以 G 开头的可能名字。

# 搜索空值

NULL 值表示实体特定情况的未知值。当我们不知道列的特定值时，可以使用 `NULL` 值。

假设我们想要一个所有尚未输入数的候选人列表。此条件用 `NULL` 值表示。

```
SELECT fname,lname,wphone,hphone
FROM candidate c,test_taken tt
WHERE c.cid=tt.cid AND score IS NULL
```

`IS` 谓词在示例中用于搜索 `NULL` 值。记住，NULL 值意味着“未知”。因为它没有特定的值，因此无法与其他值进行比较。你不能对空值使用条件操作符（如等号 `=`）。

# 搜索否定条件

`BETWEEN`、`IS` 和 `LIKE` 谓词始终查找符合特定条件的值。这些谓词也可以用于查找不符合特定标准的值。`NOT` 谓词可以用于查找相反条件，与 `LIKE`、`BETWEEN` 和 `IS` 谓词结合以完成如下例所示的搜索。

此示例将 `LIKE` 谓词与 `NOT` 结合。我们想要一个姓不以字母 S 开头的候选人列表。

```
SELECT DISTINCT fname,lname,wphone,hphone FROM candidate
WHERE lname NOT LIKE 'S%'
ORDER BY lname,fname
```

```sql
SELECT DISTINCT fname,lname,wphone,hphone
FROM candidate c, test_taken tt
WHERE c.cid=tt.cid
AND integer (score) NOT BETWEEN 60 and 75
```

在此示例中，`NOT` 谓词将排除 60 到 75 范围内的所有值。

否定也可以适用于 `NULL` 值。此 SQL 产生一个报告，搜索那些分配了座位号的候选人。这通过 `NOT NULL` 值来表示。

```sql
SELECT DISTINCT fname,lname,wphone,hphone
FROM candidate c, test_taken tt
WHERE c.cid=tt.cid AND seat_no IS NOT NULL
```

# 搜索一组值

在 SQL 中，可以根据一组值建立限制条件。假设你需要一份注册了 DB2 Fundamentals 考试和 DB2 Application Development 考试候选人的测试中心列表。可以使用以下语句进行查询：

```sql
SELECT DISTINCT name,phone
FROM test_center tc, test_taken tt
WHERE tc.cid=tt.cid
AND char(number) IN ('500','502')
```

`IN` 子句用于定义一组值。在示例中，我们使用一个常量值集。在特定情况下，SQL 语句也可以使用 `OR` 运算符来限制测试编号。

你也可以在 `IN` 子句中使用 `NOT` 谓词。在这种情况下，当某个值不存在于 `IN` 子句提供的值集中时，该条件为真。

你可以在 `IN` 子句中使用任意数量的值。然而，在某些情况下，值列表会非常长，此时使用另一个 SQL 语句来取这些值会更好。

# 第 6 章操作数据库对象

`IN` 谓词也可以用于根据条件定义值集。在这种情况下，`IN` 谓词还接受一个定义值集的 SQL 语句。当你使用 SQL 语句定义值集时，定义该值集的 SQL 语句被称为子查询。

# 子查询

子查询是用于另一个 SQL 语句内部的 SQL 语句。子查询可以与 `IN` 子句配合使用，指定 SQL 语句的搜索参数。

考虑一下在未知考试名称和编号的情况下，生成关于 DB2 认证考试数量报告的困难性。以下 SQL 产生一个报告，包含所有注册了 DB2 认证考试的测试中心。

在示例中，我们将使用单词 "DB2" 作为搜索字符串来查找 DB2 认证计划考试的编号：

```sql
SELECT DISTINCT name, phone
FROM test_center tc, test_taken tt
WHERE tc.tcid=tt.tcid
AND NUMBER IN
    (SELECT number FROM test
    WHERE name LIKE 'DB2%')
```

**图 6–11** 使用子查询

在此示例中，子查询作为 `IN` 子句的一部分出现。在子查询中，我们正在检索所有名称中包含 "DB2" 单词的测试编号。

正如上一个示例所示，子查询是一个标准的 SQL 语句。唯一的区别是子查询被用作限制条件。你永远看不到它的输出。我们仅使用子查询创建一个列表，稍后供外部 `SELECT` 语句使用。

此示例使用的子查询被称为**非相关子查询**。非相关子查询是指子查询检索的值与外部 `SELECT` 语句处理的行没有直接关联的查询。**相关子查询**是指子查询引用外部语句值的查询。

在下一个示例中，你想统计每个测试中心注册了多少候选人。这次你想在候选人数量附近显示中心名称。我们使用相关子查询来实现这一点。

```sql
SELECT tc.name, count(*)
FROM test_center tc, test t
WHERE tc.tcid IN
  (SELECT tcid FROM test_taken tt
 WHERE tt.number=t.number)
GROUP BY tc.name
```

**图 6–12** 相关子查询

观察此示例中子查询的 `WHERE` 子句。它引用了外部 `FROM` 子句中列出的表。

如果你将此查询写为非相关子查询，将得到不同的结果。在此示例中，你需要使用相关子查询以确保 `test_taken` 表中的所有行都被计数。当你使用非相关子查询时，你只会统计每个测试中心编号的出现次数。

> 注意：你应该理解子选择（sub-selects）和子查询（sub-queries）之间的区别。子选择是不包含 `ORDER` 子句、`UPDATE` 子句或 `UNION` 操作符的查询。子查询用于与 `IN` 子句配合使用，如前所述，指定 SQL 语句的搜索参数。

# 量化谓词
