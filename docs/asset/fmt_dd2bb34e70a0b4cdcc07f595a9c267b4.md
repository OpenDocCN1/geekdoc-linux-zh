
```
DELETE FROM db2cert.candidate
WHERE cid IN (SELECT cid FROM db2cert.test_taken
WHERE MONTH(date_taken)=2)
```

在此示例中，我们使用子查询来检索在 2 月份参加过 DB2 认证考试的候选人的 `CID` 值。此列表将用于搜索我们想要删除的候选人。

# 删除表中的所有行

如果你在 `DELETE` 语句中没有指定搜索条件，则将删除表中的所有行。你必须意识到这种语句的影响。然而，这并不是删除表中的所有行的唯一方法。如果所有行都符合搜索条件，也将删除表中的所有行。

使用 `DELETE` 语句删除表中的所有行可能不是最高效的方法。当表很大时，这种语句会消耗大量的日志空间。

> **注意：** 如果创建表时使用了 `NOT LOGGED INITIALLY` 选项，则有一种方法可以在不物理删除表的情况下删除表的所有内容。使用以下命令告诉 DB2 丢弃行内容（不记录）：`ALTER TABLE . . . ACTIVATE NOT LOGGED INITIALLY WITH EMPTY TABLE`。使用这种技术删除行的优点是，依赖于该表的定义不会被删除。

![](img/ca7cfad01341360e684d5dd2379b19e9_353_0.png)

# 视图分类

现在我们已经检查了各种 SQL DML 语句，让我们仔细观察视图。我们已经讨论过创建视图。现在我们来检查不同类型的视图。

视图根据它们允许的操作进行分类。它们可以是：

- 可删除 `Deletable`
- 可更新的 `Updatable`
- 可插入 `Insertable`
- 只读 `Read-only`

视图类型根据其更新能力建立。分类表示允许对视图执行的 SQL 操作类型。

引用约束和检查约束是被独立处理的。它们不会影响视图的分类。

例如，由于引用约束，你可能无法向表中插入一个值。如果你使用该表创建视图，也无法通过该视图插入该值。然而，如果视图满足可插入视图的所有规则，它仍然被视为可插入视图。这是因为插入限制是在基础表上，而不是在视图定义上。

# 可删除视图

根据视图的定义方式，你可以对可以成功发布 `DELETE` 语句的视图。可删除视图需要遵循几条规则才能被视为可删除的：

- 外部 `fullselect` 的每个 `FROM` 子句仅标识一个基础表（不带 `outer` 子句）、可删除的视图（不带 `outer` 子句）、可删除的嵌套表表达式或可删除的公共表表达式。
- 外部 `fullselect` 不使用 `VALUES` 子句。
- 外部 `fullselect` 不使用 `GROUP BY` 或 `HAVING` 子句。
- 外部 `fullselect` 在其选择列表中不包含列函数。
- 外部 `fullselect` 不使用集合操作（`UNION`、`EXCEPT` 或 `INTERSECT`），`UNION ALL` 除外。
- `UNION ALL` 操作数中的基础表不能是同一个表，且每个操作数必须是可删除的。
- 外部 `fullselect` 的选择列表不包含 `DISTINCT`。

视图必须满足列出的所有规则才能被视为可删除视图。

# 第 6 章操作数据库对象

```
CREATE VIEW deletable_view
(tcid,cid,number,date_taken,start_time,seat_no,score)
AS
SELECT tcid,cid,number,
       start_time,seat_no,score
FROM db2cert.test_taken
WHERE tcid=center_id('TR01')
```

**图. 6–30** 可删除视图的示例

图 6–30 所示的视图是可以删除的。它遵循了可删除视图的所有规则。

# 可更新视图

可更新视图是可删除视图的一种特例。当视图的至少一列是可更新的时，可删除视图就变成了可更新视图。

当满足以下所有条件时，视图的列是可更新的：

- 视图是可删除的。
- 视图使用 `UNION ALL` 且未指定 `READ ONLY` 选项。
- `UNION ALL` 的操作数的所有列类型完全匹配。

```
CREATE VIEW updatable_view
(tcid,cid,number,date_taken,start_time,seat_no,score)
AS
SELECT tcid,cid,number,
       start_time,seat_no,score
FROM db2cert.test_taken
WHERE tcid=center_id('TR01')
```

*(注：此处根据上下文逻辑补全了示例代码的完整性，原文中代码有截断）*

```
CREATE VIEW updatable_view
(tcid,cid,number,date_taken,start_time,seat_no,score)
AS
SELECT tcid,cid,number,
       start_time,seat_no,score
FROM db2cert.test_taken
WHERE tcid=center_id('TR01')
```

**图. 6–31** 可更新视图的示例

图 6–31 所示的视图是可以更新的。它满足可更新的的规则。

# 可插入视图

可插入视图允许通过视图插入行。

-视图是可插入的：

```
CREATE VIEW updatable_view
(tcid,cid,number,date_taken,start_time,seat_no,score)
AS
SELECT tcid,cid,number,
       start_time,seat_no,score
FROM db2cert.test_taken
WHERE tcid=center_id('TR01')
```

*(注：此处根据上下文逻辑补全了示例代码的完整性，原文中代码有截断）*

```
CREATE VIEW updatable_view
(tcid,cid,number,date_taken,start_time,seat_no,score)
AS
SELECT tcid,cid,number,
       start_time,seat_no,score
FROM db2cert.test_taken
WHERE tcid=center_id('TR01')
```

**图. 6–31** 可更新视图的示例

图 6–31 所示的视图是可以更新的。它满足可更新的的规则。

# 可插入视图

可插入视图允许通过视图插入行。

-视图是可插入的：

```
CREATE VIEW insertable_view
(number,name,totalaken)
AS
SELECT number,name,totalaken FROM db2cert.test
```

**图. 6–32** 可插入视图的示例

图 6–32 所示的视图是可以插入的。然而，由于某些列不接受空值，尝试使用视图插入将失败。这是因为视图定义中没有包含这些列。

# 只读视图

只读视图是非可删除视图。如果视图不符合可删除视图的至少一条规则，则可以是只读的。

`SYSCAT.VIEWS` 视图中的 `READONLY` 列指示视图为只读 `R`。

让我们检查一个只读视图：

```
CREATE VIEW read_only_view
(name,work_phone,home_phone)
AS
SELECT DISTINCT fname,wphone,hphone
FROM db2cert.candidate c,db2cert.test_taken tt
WHERE c.cid=tt.cid
```

**图. 6–33** 只读视图的示例

图 6–33 所示的视图不可删除，因为它使用了 `DISTINCT` 子句且 SQL 语句涉及多个表。

# UNION ALL 的视图

通过 `UNION ALL` 连接连接的视图已支持多个版本。只要 DB2 能够确定相应的命令应用于哪个表，`SELECT`、`DELETE` 和 `UPDATE` 操作符就是允许的。

几个示例将阐明其工作原理。

考虑四个创建用于表示每年季度销售情况的表。所有表的定义都如图 6–34 所示。

```sql
CREATE TABLE Q1SALES
(
  store int      not null,
  tx_date date    not null,
  item int        not null,
  quantity int    not null
);
CREATE TABLE Q2SALES LIKE Q1SALES;
CREATE TABLE Q3SALES LIKE Q1SALES;
CREATE TABLE Q4SALES LIKE Q1SALES;
```

**图 6–34** 代表全年销售情况的多个表

这些表可以通过 `UNION ALL` 合并，以创建一个涵盖全年的单一视图，如图 6–35 所示。
