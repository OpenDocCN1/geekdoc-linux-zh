
关系数据库包实现不同的函数集。然而，几乎每个数据库包都实现了以下函数。我们按照 MySQL 实现的方式向大家介绍它们。

## SUM(), AVG()

汇总函数 `SUM()` 相加其作为参数的列的内容。汇总函数 `AVG()` 给出其作为参数的列的平均值（即算术平均值）。

列表 3-32 中的脚本扩展了列表 3-31 以演示 `AVG()`：

### 列表 3-32：AVG()

```sql
SELECT SUM(home_team_runs),
SUM(visiting_team_runs),
SUM(home_team_runs) + SUM(visiting_team_runs),
AVG(home_team_runs),
AVG(visiting_team_runs),
AVG(home_team_runs) + AVG(visiting_team_runs)
FROM game
WHERE home_team = 'White Sox';
```

其输出是：

`353    280    633    4.7703    3.7838    8.5541`

## MIN(), MAX()

汇总函数 `MIN()` 返回传递给其参数的列中的最小值。汇总函数 `MAX()` 返回传递给其参数的列中的最大值。

列表 3-33 展示了这些函数。它给出了白袜队在主场比赛时主队和客队得分的最小最大值。

### 列表 3-33：MIN() 和 MAX()

返回：

`0    0    19    11`

正如你所预期的，主队或客队得分的最低数为零。白袜队在主场比赛中的最高分为 19 分；在主场被对手攻入的分为 11 分。

## COUNT(), COUNT(*)

汇总函数 `COUNT()` 和 `COUNT(*)` 计算给定的 `SELECT` 语句生成的行数。

这两种计数形式的区别在于 `COUNT()` 取列名作为参数，而 `COUNT(*)` 不考虑任何给定的列而计算行数。然而，这两种者的行为完全相同——它们都计算 `SELECT` 语句生成的行数——所以没有理由使用 `COUNT()`。我们将考察限制在 `COUNT(*)` 上。

你可能会好奇知道给定的 `SELECT` 语句生成的行数有什么用。答案是这些信息可以回答广泛的问题，其中大多数问题以“频率是多少……”、“有多少……”等短语开头。例如，假设你想知道白袜队在家场被封零多少次。列表 3-34 中的脚本使用 `COUNT(*)` 来找到答案：

### 列表 3-34：封零（Shutouts）

```sql
SELECT COUNT(*)
FROM game
WHERE home_team = 'White Sox'
  AND
  home_team_runs = 0;
```

答案是：

`5`

也就是说，白袜队曾在场被封零。

## GROUP BY 子句

正如你看到的，当你想要汇总行时，`GROUP BY` 子句非常好。

### GROUP BY 的语法

`GROUP BY` 子句的语法与 `ORDER BY` 子句完全相同。例如，假设你想按列名分组。列表 3-34 中的脚本使用 `COUNT(*)` 找到答案：白袜队曾在被封零。`GROUP BY` 子句告诉 SQL 引擎分组。

当我们考虑到汇总函数时，`SELECT` 语句的语法如下：

```sql
SELECT [ DISTINCT|ALL ] column_name | constant arithmetic_expression | \
function ( column_name ) [, , ... ]
FROM table_name [, , ... ]
WHERE [ restrict_expression ] [ join_expression ]
ORDER BY column_name, [, , ... ] [ ASC|DESC ]
UNION
SELECT select_statement
```

## 列别名（Aliases for columns）

在此处，你可能会问是否有一种方法可以将此 `SELECT` 语句的输出按被封零次数进行排序，而不是按球队名称。这是一个真正的问题；毕竟，你不能将 `COUNT(*)` 函数放入 `ORDER BY` 子句。然而，这是可以的如果我们为列使用别名。

SQL 允许你使用列编号作为 `GROUP BY` 和 `ORDER BY` 子句中的列别名。列编号是由 `SELECT` 语句字段名子句中列命名的顺序决定的。在列表 3-36 中，`home_team` 是第 1 列，函数 `COUNT(*)` 输出是第 2 列。这种方法让你能够识别没有名称列，因为它是通过表达式或函数构建的。

例如，列表 3-37 对封零次数排序：

### 列表 3-37：表达式的降序排序

```sql
SELECT home_team, COUNT(*)
FROM game
WHERE home_team_runs = 0
GROUP BY home_team
ORDER BY 2 DESC;
```

`ORDER BY 2` 子句告诉 SQL 引擎按第二列的内容排序，该列是由 `COUNT(*)` 函数构建的。输出是：

```
Rangers 7
Angels 5
White Sox 5
Twins 5
```

所以，现在我们可以清楚地看到游骑队是在主场被封零次数最多的球队。

另一种使用别名的方法是为表达式分配字符串名称，然后在 SELECT 语句其余部分使用该名称。为表达式命名使用关键字 `AS`。

例如，列表 3-38 中的脚本重写了列表 3-37，以使用字符串作为 `COUNT(*)` 函数的别名：

### 列表 3-38：字符串别名

```sql
SELECT home_team, COUNT(*) AS shutouts
FROM game
WHERE home_team_runs = 0
GROUP BY home_team
ORDER BY shutouts DESC;
```

此脚本的输出与列表 3-37 相同；但此脚本具有更高的可读性优势。

当你开始编写复杂的 SELECT 语句时，这种为表达式取别的能力非常有用。

## 其他函数

在本节中，我们集中于最常用的函数——那些对整列数据进行摘要的函数。然而，大多数数据库包提供了丰富的函数集。这些包括三角函数；分析或转换文本的函数；格式化日期时间数据的函数以及其他杂项函数。

### IFNULL()

这些杂项函数中最实用的之一是 `IFNULL()` 函数。`IFNULL()` 允许你在给定表达式为 NULL 时设置查询返回的内容。

`IFNULL()` 接受两个参数：第一个参数是待评估的表达式，第二个参数是当第一个表达式求值为 NULL 时要打印的值。第二个参数的类型必须与第一个参数相匹配；也就是说，如果第一个是输出字符串的表达式，那么第二个必须是字符串；而如果第一个是输出数值的表达式，第二个参数则必须是数字。

例如，列表 3-39 重写了列表 3-29 以使用 `IFNULL()`：

### 列表 3-39：演示 IFNULL()

```sql
SELECT DISTINCT team.team_name, IFNULL(game.home_team_runs, -1)
FROM team
LEFT JOIN game ON team.team_name = game.home_team
ORDER BY team_name;
```

由于 `home_team_runs` 是数值列，`NULL()` 的第二个参数也必须是数字。运行时，此脚本输出以下内容：

```
Angels 8
Angels 10
Angels 4
Angels 3
ers 0
Brewers 15
Cardinals -1
Cubs -1
Dodgers -1
Expos -1
```

在数据库没有某某球队的比赛信息的情况下，引擎不再打印字符串 NULL，而是打印 -1。

`NULL()` 在数据库引擎返回其他值来表示 NULL 的情况下特别有用。例如，某些引擎在整数列为 NULL 时会返回零；如果零是该列中的合法值，那么你就需要使用 `NULL()` 将 NULL 映射到另一个未使用的值。

某些数据库包使用 `ISNULL()` 而不是 `ISNULL()`；然而，其语法和行为是相同的。

## 添加新函数

许多数据库包允许你编写新函数并将其添加到数据库引擎中。PostgreSQL 和 MySQL 都支持此功能。

编写函数并将其添加的方法在不同数据库包之间差异很大。在大多数情况下，你必须是一个相当熟练的 C 语言程序员。更多信息请参阅你数据库包自带的文档。

## 子查询 (Sub-SELECTS)

之前，我们描述了 SELECT 语句的 UNION 子句。该子句允许我们使用 SELECT 语句；使我们能够轻松地执行如果没有它将难以或无法完成的任务。

SQL 还允许你嵌套 SELECT 语句：SELECT 语句中 WHERE 子句内的表达式可以是一个 SELECT 语句。这些嵌套的 SELECT 语句并不常用，但它们确实能让你回答某些否则难以或无法回答的问题。
