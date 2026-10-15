
到为止，我们分别讨论了每个外连接操作。现在，我们将展示一个更复杂的示例，在单个查询中结合了两个外连接。让我们显示所有候选人及其相应的分数。

## 外连接 (Outer Join)

要创建此查询，我们需要两个外连接。第一个外连接将获取所有候选人及其分数，包括没有安排或参加任何测试的候选人。第二个外连接将检索测试表中的所有测试，即使没有候选人安排或参加这些测试。

```sql
SELECT c.cid, t.name, score
FROM (db2cert OUTER JOIN db2cert.test_taken tt
  LEFT JOIN ON tt.cid=c.cid)
  FULL OUTER JOIN db2cert.test t
  ON tt.number = t.number
ORDER BY c.cid
```

图 7–14 一个 SQL 语句中的两个外连接

第一个外连接包含在括号内。括号的使用是为了可读性，并表示先解析左外连接。此左外连接收集了所有的候选人 ID。我们在这里只需要左外连接。由于引用完整性约束，`test_taken` 表只能包含 `candidate` 表中存在的候选人。

第二部分是全外连接。通过此外连接，我们获取候选人参加的所有测试（左外连接的结果），并将它们与 `test` 表中的所有测试进行连接。尽管 `test_taken` 表只能包含 `test` 表中存在的测试编号，但我们这次仍然需要全连接，因为此外连接的左侧部分（即第一次连接的结果）可能包含测试编号的 NULL 值。`test` 表不包含空值，因此我们需要使用全外连接。

SQL 语句的输出如图 7–15 所示。

## 第 7 章 高级 SQL

| CID | NAME | SCORE |
|---|---|---|
| 111 | DB2 Fundamentals | 65 |
| 111 | DB2 Administration | 73 |
| 111 | DB2 Application Development | 67 |
| 222 | DB2 Fundamentals | 55 |
| 222 | DB2 Application Development | 53 |
| 222 | DB2 Application Development | 75 |
| 333 | DB2 Fundamentals | 82 |
| 333 | DB2 Administration | - |
| 333 | DB2 Application Development | 92 |
| 444 | - | - |
| 555 | - | - |
| 666 | - | - |
| 777 | - | - |
| 888 | - | - |

选中了 14 条记录。

图 7–15 两个外连接结合的结果

## OLAP 特性

数据库通常持有大量数据，这些数据可以每天进行更新、查询和插入。数据被不断删除、更新、删除和插入的数据库被称为联机事务处理 (`OLTP`) 系统。持有大量数据且没有繁重事务负载但一直有大量并发查询执行的数据库被称为决策支持系统 (`DSS`)。某些决策支持系统的查询少，但每个查询都可能非常复杂。这些允许用户通过执行联机分析处理 (`OLAP`) 从不同的角度检查数据。

数据库需要提供关系型数据的多维度视图，且不会对性能产生显著影响。`DB2` 通过多种连接方法、`SQL` 语句和其他特性提供了这种能力。接下来的几节将解释 `DB2` 中增强 `OLAP` 性能的数据库技术。

## 星型模型 (STAR Schemas)

星型模型的概念如图 7–16 所示。高度规范化的数据库视图通常需要与对象相关的多个属性。这些属性包含在独立的表中。

| Fact Table | Test Center | PK |
| --- | --- | --- |
| Dimension Table | Center ID | |
| Primary Key | Name | |
| Foreign Key | No.Seats | |
| | Test Taken | FK |
| | Candidate_ID Center ID Test ID Date Score |
| | Candidate ID Name Phone |
| | Test ID Name Cut Score |

图 7–16 `DB2` 数据库中的星型模型

星型设计具有以下特征：

- 有一个大的事实表（Fact Table），包含关联维度表的数据。图 7–16 中，事实表是 `test_taken` 表。它包含了每次测试的详细信息，包括具体参加了哪个测试、在哪个中心参加以及谁参加了。
- 有若干较小的维度表（Dimension Table），通常持有行数较少的实体描述信息。图 7–16 中，维度表是 `test`、`candidate` 和 `test_center`。
- 星型模型涉及维度表的主键支持事实表的外键。维度表外键的组合通常形成事实表的一个小子集。图 7–16 中，外键是 Candidate ID、Center ID 和 Test ID。

这种方法允许在事实表中存储尽可能少的属性。这样做的好处是事实表通常很大，该表中的任何重复数据在存储和访问上都是非常昂贵的。

`OLAP` 模型（如星型模型）经常用于大型数据库。这些模型使得访问这些数据库中的数据变得非常重要以最佳方式进行。否则，架构中涉及的连接可能会导致性能低下。

### OLAP 索引

典型的星型模型（`STAR` schema）包含大量的索引。这是由于 `OLAP` 环境中的查询具有即时性特征。这种环境通常没有持续的插入或更新活动，因此不必因为索引维护而遭受显著的性能下降。

`OLAP` 环境中索引的首要考虑因素是便于表连接和输出排序。这对于定义了多个索引的事实表尤为重要，特别是针对关联维度表的外键列的索引。在这种环境中，多个索引的益处提升了针对事实表的查询性能。定义在表上的索引可以是单列索引，也可以是多列索引。

在 `OLAP` 环境中使用多个索引时，还有某些需要考虑的问题。首先是多个索引需要一定的空间，取决于每个索引中列的数量和索引的大小；其次是构建索引时（可能在批量加载期间）会产生巨大的一次性成本。

### 星型连接 (STAR Joins)

针对使用星型模型设计的数据库，典型查询由多个引用维度表中值的局部谓词组成，并包含连接维度表和事实表的连接谓词，如图 7–17 所示。这类查询被称为星型连接。

在这个示例中，我们查找了加拿大公民在小型测试中心每年参加 `DB2` 测试的平均分。星型连接查询很难高效执行，因为没有单一谓词可以显著减少事实表行的基数，尽管连接谓词的组合产生了一个小的结果集。连接结果中涉及的维度表越多，规划低效访问路径的可能性就越大。为了高效地执行星型连接查询，优化器可以执行多次索引访问。

```sql
SELECT t.name, YEAR(tt.date_taken) AS year,
AVG(integer(tt.score)) AS avgsc
FROM test t, test_taken tt, test_center tc,
candidate c
WHERE c.cid = tt.tcid AND
tc.tcid = tt.tcid AND
t.number = tt.number AND
t.name LIKE 'DB2%'' AND
c.country='Canada' AND
tc.noseats < 10
GROUP BY t.name, YEAR(tt.date_taken);
```

图 7–17 星型连接

### 超分组 (Super Grouping)

我们现在来讨论被称为超分组函数（super grouping functions）的 `OLAP` 功能。这些函数用于从多个维度分析数据。维度可以被看是对一组表上不同层级的聚合。超分组被用于描述 `OLAP` 特性，因为它们允许在单次数据扫描中检索多个聚合级别。

### 多组分组 (Grouping Sets)

`GROUP BY` 子句中的 `GROUPING SETS` 规范用于在单个 `SQL` 语句中生成多个聚合组。此功能用于根据不同的分组准则生成聚合数据。使用 `GROUPING SETS`，可以计算原本需要通过集合操作（如 `UNION`）来组合不同聚合结果集的聚合。

假设我们知道以下信息：

- 在测试中心参加了多少测试？
- 每个测试中心参加了多少种类型的测试？

为了收集这些信息，我们首先需要按测试中心对测试进行计数，然后统计每个测试中心参加的测试数量。这个需求需要不同的分组集：一个按测试中心分组，另一个按测试名称和测试中心分组。请看下面的示例和结果：

```sql
SELECT tt.tcid,t.name,count(*)
FROM db2cert.test_taken tt, db2cert.test t
WHERE tt.number=t.number
GROUP BY
GROUPING SETS (tt.tcid, (tt.tcid,t.name))
```

**图. 7–18** SQL 语句中使用的分组集

| TCID NAME | 3 |
|---|---|
| TR01 | 3 |
| TX01 | 6 |
| TR01 DB2 Development | 2 |
| TR01 DB2 Administration | 2 |
| TX01 DB2 Application Development | 2 |
| TX01 DB2 Fundamentals | 2 |

选中了 7 条记录。

**图. 7–19** 分组需求的结果，即

`GROUPING SETS` 规范通过列出 `test_taken` 表的 `tcid` 列来计算第一个需求（即每个测试中心参加的测试数量）。然后，第二个需求（按测试中心和名称划分的测试数量）通过列出 `test_taken` 表的 `tcid` 列和 `test` 表的 `name` 列来计算。这种第二次分组与使用 `GROUP BY TT.TCID, T.NAME` 编写的常规 `GROUP BY` 相同。

如图 7–19 所示的结果，分组集可以由一列或多列形成。

### 添加总计 (Adding a Grand Total)

使用 `GROUPING SETS` 规范，你可以为查询添加一个总计。图 7–18 所示的示例没有显示所有测试中心参加的测试总数。这可以通过向分组列表中添加总计来计算。

当组被创建时，空值会被添加到那些在特定组中没有值的列中。这样，总计行除总计本身以外的所有列都将显示空值。

让我们看看下一个示例。这个示例与图 7–18 中的示例相似，但这次我们包含了总计，并使用 `GROUPING` 函数将生成的空值转换为字符字符串。

```sql
SELECT tt.tcid,t.name,count(*)
FROM db2cert.test_taken tt, db2cert.test t
WHERE tt.number=t.number
GROUP BY
  GROUPING SETS (tt.tcid, (tt.tcid,t.name))
```

**图. 7–20** 带有总计的分组集

| 1 | 2 |
|---|---|
| All Tests | 9 |
| TR01 All Tests | 3 |
| TX01 All Tests | 6 |
| TR01 DB2 Development | 2 |
| TR02 DB2 Fundamentals | 1 |
| TX01 DB2 Administration | 2 |
| TX01 DB2 Application Development | 2 |
| TX01 DB2 Fundamentals | 2 |

选中了 8 条记录。

### 识别分组添加的值 (Recognizing Group Added Values)

在分组中使用数据包含空值的情况。在这种情况下，区分空值和分组生成的值非常重要。`DB2` 提供了 `GROUPING` 函数，通过给这些生成值赋值 1 来识别它们。

### OLAP 功能

> **注意：** `GROUPING` 函数仅返回值 1 或 0。1 (1) 表示该值是由 `DB2` 生成的，0 表示不是。

现在，让我们在 `CASE` 表达式中使用 `GROUPING` 函数来区分带有空值的组和普通的空值。为了保持查询简洁，示例将对 `tcid` 列使用 `CASE` 表达式。

```sql
SELECT
CASE
  WHEN GROUPING(tt.tcid)=1
    THEN 'All'
  WHEN GROUPING(tt.tcid)=0
    THEN char(tt.tcid)
END,
VALUE(t.name),'All Tests'),
GROUPING(tt.tcid) AS grouped_tcid,
GROUPING(t.name) AS grouped_name,
COUNT(*)
FROM db2cert.test_taken tt, db2cert.test t
WHERE tt.number=t.number
GROUP BY
  GROUPING SETS (tt.tcid, (t.name,tt.tcid),())
```

**图. 7–22** 使用分组函数识别添加的空

| 1 | | GROUPED_TCID | GROUPED_NAME | 5 |
|---|---|---|---|||
| All All Tests | 0 | 1 | 9 |
| TR01 All Tests | 0 | 0 | 1 |
| TX01 All Tests | 0 | 1 | 6 |
| TR01 DB2 Application Development | 0 | 0 | 0 |
| TR02 DB2 Fundamentals | 0 | 0 | 2 |
| TX01 DB2 Administration | 0 | 0 | 2 |
| TX01 DB2 Application Development | 0 | 0 | 2 |
| TX01 DB2 Fundamentals | 0 | 0 | 2 |

选中了 8 条记录。

**图. 7–23** 分组函数的结果

`CASE` 表达式对 `tcid` 列使用 `GROUPING` 函数。如果返回值为 1，则打印 All。在我们的示例中，All 表示

# 第 7 章 高级 SQL

该行包含一个分组添加的空值。由空生成的值代表所有测试中心。如果 `GROUPING` 函数返回 0，则意味着该行的 `tcid` 列的值不是由 `DB2` 生成的。

图 2 所示的 `GROUPING` 函数将根据特定行 `tt.tcid` 和 `t.name` 列的值显示 1 或 0。`GROUPING(tt.tcid)` 的值为 1 意味着该行是基于 `tcid` 列的汇总分组（total grouped）。

## ROLLUP

前一节中所示的 `GROUPING SETS` 规范允许你在单次数据扫描中创建不同层级的聚合。然而，你需要指定你想要的每个组。在某些情况下，你需要创建一个报告，其中需要对每个分组列进行总计。这时就需要像 `ROLLUP` 这样的超级分组（super group）功能。

`ROLLUP` 分组可以在单次数据扫描中生成各种组。这将允许你在创建控制分段报表时，查看不同级别的聚合结果。

假设你需要一份显示以下内容的报告：

- 每个国家参加了多少次？
- 每个国家和测试中心参加了多少次？
- 每个国家、测试中心和测试名称参加了多少次？
- 参加测试的总数是多少？

为了满足这一需求，我们将使用 `ROLLUP` 分组，它将生成请求的聚合。`SQL` 语句如图 7–24 所示。

```sql
SELECT
c.country,
tt.tcid,
ubstr(t.name,1,27) as test_name,
count(*) as tests_taken
FROM db2cert.test_taken tt, db2cert.test t, db2cert.candidate c
WHERE tt.number=t AND tt.tcid=c
GROUP BY ROLLUP (c.country,tt.tcid,t.name)
ORDER BY c.country,tt.tcid,t.name
```

**图 7–24** 使用 `ROLLUP`

生成的报告允许你对信息进行汇总（roll up）和下钻（drill down）。你可以从总计级别到国家、测试中心和测试名称对报告进行分析。

## OLAP 特性

| 国家 | TCID 测试名称 | 参加次数 |
| --- | --- | --- |
| 加拿大 | TX01 DB2 Administration | 2 |
| 加拿大 | TX01 DB2 Application Development | 2 |
| 加拿大 | TX01 DB2 Fundamentals | 2 |
| 加拿大 | TX01 - | 6 |
| 加拿大 | - | 2 |
| 德国 | TR01 DB2 Application Development | 2 |
| 德国 | TR01 DB2 Fundamentals | 1 |
| 德国 | TR01 - | 3 |
| 德国 | - | 9 |

图 7–25 `ROLLUP` 操作符的结果。

已选择 10 条记录。

> 注意：`ROLLUP` 操作没有交换律；你指定组的顺序非常重要。`ROLLUP (COUNTRY, TCID, NAME)` 的结果集与 `ROLLUP(TCID, COUNTRY, NAME)` 不同。

像 `ROLLUP` 这样的超级分组操作是基于 `GROUPING SETS` 操作构建的。图 7–24 所示的 `ROLLUP` 等于 `GROUPING SETS ((COUNTRY, TCID, NAME), (COUNTRY, TCID),COUNTRY, ())`。这就是为什么它们被认为是超级分组操作。

## CUBE

从图 7–24 所示的 `ROLLUP` 操作得到的结果集中，有一些组是无法使用的。这些组包括仅按测试中心或仅按测试编号参加的测试次数。

`CUBE` 操作获取分组列表中形成的所有组组合。`CUBE` 操作分组列表中列出的组将进行排列，以计算此列表中所有可能的组。这创建了构建数据立方体（cube of data）所需聚合。
