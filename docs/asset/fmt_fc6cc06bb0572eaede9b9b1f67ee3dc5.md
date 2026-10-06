
让我们向 `test_taken` 表插入一行。在下面的示例中，我们仅为 `CID`、`TCID`、`NUMBER` 和 `SEAT_NO` 列插入数据。

```
INSERT INTO db2cert.test_taken
(CID,TCID,NUMBER,SEAT_NO)
VALUES('888','TR01','508','1')
```

请记住，定义为 `USING DEFAULT` 但未在 `INSERT` 语句中的列将接收 `NULL` 值或默认值。

## 插入多行

可以使用单个 `INSERT` 语句向表中插入多行。例如，你可能想为候选人安排 DB2 认证考试。该候选人将在三个不同的日期参加考试：

```
INSERT INTO db2cert.test_taken
(CID,TCID,NUMBER,DATE_TAKEN,SEAT_NO)
VALUES
('888','TR01','500','2000-06-04','1'),
('888','TR01','501','2000-07-11','2'),
('888','TR01','502','2000-11-08','1')
```

**图. 6–25** 多行 `INSERT` 语句

在 6–25 中，我们用逗号分隔不同行的值。在使用单个语句插入多行时，你必须考虑所有行必须具有相同的列数、类型和顺序。

## 插入一组值

使用 SQL，你可以将 SELECT 语句的结果插入到相同或不同的表中。生成该结果集的 SQL 语句必须遵循以下不同规则：

- `SELECT` 语句中的列数必须与 `INSERT` 列列表中的列数相等。
- `SELECT` 列表中每个列的数据类型必须与 `INSERT` 列表中对应列的数据类型匹配。
- 只有在向表中的所有列都插入了值的情况下时，才能从 `INSERT` 列表中省略列名。
- 只有定义为允许 `NULL` 或定义为 `NOT NULL` 带有 `DEFAULT` 的列才能从 `INSERT` 列表中省略。

在某些情况下，创建与其他表相同的副本表可能是很有用的，这样你可以对这些表进行多次计算。下一个示例使用了一个名为 `test_passed` 的表，它是 `test_taken` 表的副本。此新表将用于提取通过了任何 DB2 认证考试的候选人的信息。

**图 6–26** 使用 `SELECT` 语句插入值

图 6–26 中 `fullselect` 所使用的 `select` 列表也可以用 `select` 星号 (`*`) 替换。这是因为 `test_passed` 表与 `test_taken` 表具有相同的列结构。然而，为了使此查询不受未来表修改的影响，建议使用 `select` 列表而不是星号。

当你使用 `SELECT` 语句向表插入数据时，必须将其括在括号中。你也可以使用表表达式通过 `INSERT` 子句将值插入到表或视图中。

## 插入大量数据

使用 `SELECT` 或 `VALUES` 语句向表插入数据可能非常有用。然而，不建议使用 `INSERT` 语句向表中加载大量数据，因为事务日志的开销可能会变得无法管理。

DB2 为你提供了两个专门用于将大量数据移动到表的工具。这些工具是 `IMPORT` 和 `LOAD`，在第 451 页的“维护数据”中描述。

虽然对于 DB2 UDB V7.1 并不新鲜，但在创建表时使用 `NOT LOGGED INITIALLY` 选项可以提高高大量插入的性能。此选项告诉 DB2 不要在当前工作单元期间对表的更改进行记录。对该表的后续更改将导致日志记录。如果未来的加载需要关闭日志，可以使用命令 `ALTER TABLE x ACTIVATE NOT LOGGED INITIALLY` 将表置回无日志状态。

在利用此功能之前，请确保你理解加载期间关闭日志的恢复影响。

## 更新数据记录

到目前，我们已经了 `INSERT` 语句作为将数据移动到 DB2 表的方法。你可能希望为一组数据记录更新某列的值。有一个 SQL `UPDATE` 语句可以指定该列及其新值。表或视图可以作为 `UPDATE` 语句的目标。

> 注意：记住，你必须拥有正确的权限才能执行 `UPDATE` 操作。

`UPDATE` 语句可以用两种形式使用：

- 搜索更新（Searched update）。这种类型的 `UPDATE` 语句用于更新表中的一行或多行。它需要一个 `WHERE` 子句来建立更新条件（即哪些行被更新）。
- 定位更新（Positioned update）。这种类型的 `UPDATE` 语句始终嵌入程序中。由于光标使用游标来更新光标所在的行，`UPDATE` 语句的目标行会发生变化。

### 第 6 章操作数据库对象

在本章中，我们关注搜索更新。

与 `INSERT` 语句类似，所有的数据库约束机制在 `UPDATE` 语句期间都会强制执行。存在特定的更新约束触发器和引用完整性约束，它们可能与插入约束不同。

例如，以下是一个更新候选人 ID 888 的 DB2 基础认证考试日期的事务。

```sql
UPDATE db2cert.test_taken
SET date_taken=date_taken + 3 days
WHERE char(cid)='888'
AND number=test_id('500')
```

在这个示例中，我们正在使用一种称为标记持续时间（labeled duration）的操作在原始日期基础上增加三天。

提供正确的 `WHERE` 子句是非常重要的，以避免更新非预期的数据记录。在这个示例中，我们需要指定谓词 `number=test_id('500')`，以避免更改该候选人可以安排的其他任何测试的日期。

> 注意：DB2 用于数据类型的标记持续时间包括：`YEARS`、`MONTHS`、`DAYS`、`HOURS`、`MINUTES`、`SECONDS` 和 `MICROSECONDS`。

`UPDATE` 语句也可以配合 `fullselects` 使用。在这种情况下，`fullselect` 必须返回的行在列数和数据类型上与被更新的行完全相同。注意，此 `fullselect` 必须只返回一行。

让我们使用 `SELECT` 语句更新某行以设置新值。候选人 ID 888 决定今天在位于加拿大多伦多的测试中心参加 DB2 基础测试。

```sql
UPDATE db2cert.test_taken
SET (date_taken, tcid)=
(SELECT current date, tcid FROM db2cert.test_center
WHERE substr(city,1,7)='Toronto'
AND country='Canada')
WHERE CHAR(tcid)='888' AND number=test_id('5000');
```

**图 6–27** 使用行 `fullselect` 更新数据

在图 6-27 中，我们在同一个操作中更新了两个不同的列。这些列在 `SET` 子句后的括号中指定。注意 `WHERE` 子句将限制将被更新的行。888 决定今天在位于加拿大多伦多的测试中心参加 DB2 基础测试。注意搜索更新中的 `WHERE` 子句，表中的所有数据将被更新。

更新 `date_taken` 和 `tcid` 列的 SQL 语句被称为行 `fullselect`。注意此 `fullselect` 可以被视为特殊情况。

> 注意：`CURRENT DATE` 是提供系统日期的特殊寄存器。其他的包括 `CURRENT TIME`、`CURRENT TIMESTAMP` 和 `USER`（授权 ID）。

## 更新大量数据

在有时，你需要更新特定表的许多行。这可以通过搜索更新完成。然而，这可能会分配大量的日志空间。你可以使用定位更新来完成更新，从而轻松控制提交频率。

## 删除数据

有很多方法可以从 DB2 数据库删除数据。要删除数据库中的所有数据，请执行 `DROP DATABASE`。这可能会删除比你预期更多，因为整个数据库及其配置将被物理删除。

也可以使用 `TABLESPACE` 或 `DROP TABLE` 语句删除数据。这些语句通常由 `SYSADM` 或 `DBADM` 发布，因为它们将删除大量数据。如果你希望删除表中的所有数据记录，执行 `DROP TABLE` 语句更容易更快。

要从表中删除单个数据记录或一组记录，应使用 `DELETE` 语句。`DELETE` 语句的语法与 `SELECT` 和 `INSERT` 语句不同，因为不能选择列，只能删除行。

`DELETE` 语句也可以配合视图使用。然而，`DELETE` 语句中的视图类型存在限制。

> 注意：记住，你必须拥有表的相应权限才能执行 `DELETE` 操作。

通常有两种 `DELETE` 语句：

- 搜索删除（Searched delete）。这种 `DELETE` 语句用于删除表中的一行或多行。它可以使用 `WHERE` 子句来建立删除条件。
- 定位删除（Positioned delete）。这种类型的 `DELETE` 操作始终嵌入程序中。它使用游标来删除光标所在的行。

在本节中，我们将关注搜索删除。

> 注意：以下内容仅用于向你展示如何使用 `DELETE` 语句并示例。

以下 SQL 语句将删除表中未加载电话号码的候选人。我们将使用搜索删除来完成这项任务。

## 数据修改

```sql
DELETE FROM db2cert.candidate
WHERE hphone IS NULL
AND wphone IS NULL
```

此示例使用 `WHERE` 子句删除符合特定标准的数据。

要验证 `DELETE` 语句的结果，可以执行具有相同 `WHERE` 子句的 `SELECT` 语句。如果 `DELETE` 执行成功，`SELECT` 将返回空集。

通过使用子查询（`subselect`），删除操作也可以变得更加复杂。下一个 SQL 语句删除了在任何年份 2 月参加过 DB2 认证考试的所有候选人。

```sql
DELETE FROM db2cert.candidate
WHERE cid IN (SELECT cid FROM db2cert.test_taken
      WHERE MONTH(date_taken)=2)
```

在此示例中，我们使用子查询来检索在2月份参加过 DB2 认证考试的候选人的 `cid` 值。此列表将用于搜索我们想要删除的候选人。

## 删除表中的所有行

如果你在 `DELETE` 语句中不指定搜索条件，则可以删除表中的所有行。你必须意识到此类语句的影响。然而，这并不是删除表中所有行的唯一方法。如果所有行都符合搜索条件，你也可以删除表中的所有行。

### 使用 `DELETE` 语句删除表中的所有行可能不是最高的方法。当表很大时，此类语句可能会消耗大量的日志空间。

如果创建表时使用了 `NOT LOGGED IN` 选项，则有一种方法可以在不物理删除表的情况下删除表的所有内容。使用以下命令告诉 DB2 丢弃记录（不记录日志）：`ALTER TABLE x ACTIVATE NOT LOGGED IN WITH EMPTY TABLE`。这种技术删除行的优点是依赖于该表的定义不会被删除。

## 视图分类

现在我们已经检查了各种 SQL DML 语句，让我们仔细观察视图。我们已经讨论过创建视图。现在我们将检查不同类型的视图。

视图根据其允许的操作进行分类。它们可以是：

- 可删除（Deletable）
- 可更新（Updatable）
- 可插入（Insertable）
- 只读（Read-only）

视图类型根据其更新能力确立。分类表示在使用视图时允许的 SQL 操作类型。

引用约束和检查约束是独立处理的。它们不会影响视图的分类。

例如，由于引用约束，你可能无法向表中插入值，那么你同样无法通过视图向表插入该值。然而，如果视图满足可插入视图的所有规则，它仍然会被认为是可插入视图。这是因为插入限制位于基表上，而不是视图定义上。

## 可删除视图

根据视图的定义方式，视图可以是可删除的。你可以对可删除视图成功地执行 `DELETE` 语句。要使视图被视为可删除，需要遵循以下几规则：

- 外部 `select` 的每个 `FROM` 子句仅标识一个基表（不带 `OUTER` 子句）、可删除视图（不带 `OUTER` 子句）、可删除的嵌套表表达式或可删除的公共表表达式。
- 外部 `select` 不使用 `VALUES` 子句。
- 外部 `select` 不使用 `GROUP BY` 或 `HAVING` 子句。
- 外部 `select` 的选择列表中不包含列函数。
- 外部 `select` 不使用集合操作（`UNION`、`EXCEPT` 或 `INTERSECT`），但 `UNION ALL` 除外。
- `UNION ALL` 操作数中的基表不能是同一张表，且每个操作数必须是可删除的。
- 外部 `select` 的选择列表不包含 `DISTINCT`。

视图必须满足上述所有规则才能被视为可删除视图。

```sql
CREATE VIEW deletable_view
(tcid,cid,number,date_taken,start_time,seat_no,score)
AS
SELECT tcid,cid,number,date_taken,
       start_time,seat_no,score
FROM db2cert.test_taken
WHERE tcid=center_id('TR01')
```

**图 6–28** 可删除视图的示例

图 6-28 所示的视图是可以删除的。它遵循可删除视图的所有规则。

## 可更新视图

可更新视图是可删除视图的一种特殊情况。当视图的至少一列是可更新时，可删除视图就变成了可更新视图。

当满足以下所有规则时，视图的列是更新的：

- 视图是可删除的。
- 该列对应基表的列（不使用解引用操作）且未指定 `READ ONLY` 选项。
- 如果视图的完整选择包含 `UNION ALL`，则 `UNION ALL` 操作数的所有对应列具有精确匹配的数据类型（包括长度或精度和标度）以及匹配的默认值。

```sql
CREATE VIEW updatable_view
(tcid,cid,number,current_date,current_time,seat_no,score)
AS
SELECT tcid,cid,number,CURRENT DATE,
       CURRENT TIME,seat_no,score
FROM db2cert.test_taken
WHERE tcid='TR01'
```

**图 6–29** 可更新视图的示例

图 6-29 所示的视图是可以删除的。它遵循可删除视图的所有规则。

## 可插入视图

可插入视图允许你使用视图插入行。当满足以下条件时，视图是可插入的：

- 它所有的列都是可更新的。
- 视图定义不包含 `UNION ALL`。

```sql
CREATE VIEW insertable_view
(number,name,total)
AS
SELECT number,name,total FROM db2cert.test_taken
```

**图 6–30** 可插入视图的示例

图 6-30 所示的视图是可以插入的。然而，尝试插入视图将失败。

## 只读视图

只读视图是非删除视图。如果视图不符合可删除视图的至少一条规则，则就是只读的。

`SYCAT.VIEWS` 目录视图中的 `READONLY` 列指示视图是只读的（R）。

让我们检查只读视图：

```sql
CREATE VIEW read_only_view
(name,work_phone,home_phone)
AS
SELECT DISTINCT fname,wphone,hphone
FROM db2cert.candidate c,db2cert.test_taken tt
WHERE c.cid=tt.cid
```

**图 6–31** 只读视图的示例

图 6-31 所示的视图不是可删除视图，因为它使用了 `DISTINCT` 子句且 SQL 语句涉及多个表。

## 失效视图

失效视图是不再用于 SQL 语句的视图。在发生以下情况时视图会失效：

- 视图定义依赖的权限被撤销。
- 视图定义依赖的对象（如表、别名或函数）被删除。
- 视图定义依赖的视图失效了。
- 视图定义的父视图（子视图）失效了。

# 第 7 章

## 高级 SQL

- 触发器 (`TRIGGERS`)
- 递归 SQL
- 外部连接 (`OUTER JOIN`)
- OLAP
- `CASE` 表达式
- 类型表
- 摘要表

本章将介绍 DB2 SQL 中发现的一些非常强大的功能。将讨论如触发器、递归、外部连接、OLAP 特性以及 `CASE` 表达式的使用。此外，我们还将讨论结构化类型、类型表、用户定义函数和摘要表。

## 触发器 (Triggers)

触发器是在定义的事件发生时将执行的一系列动作。触发事件可以可以是以下 SQL 语句：

- `INSERT`（插入）
- `UPDATE`（更新）
- `DELETE`（删除）

触发器是针对特定表定义的，一旦定义，触发器就会自动激活。一个表可以为其定义多个触发器，如果为给表定义了多个触发器，则触发器的激活顺序基于创建时间戳（触发器创建的顺序）。触发器定义存储在系统目录表中。你可以通过这些目录视图查看它们：

- `SYSCAT.TRIGGERS` - 包含触发器定义信息；每个定义的触发器对应一行
- `SYSCAT.TRIGDEP` - 包含触发器对某些其他对象的每个依赖项对应一行

## 触发器的用法 (Trigger Usage)

触发器的一些用途包括：

- 数据验证 - 确保新数据值在适当范围内。这与表检查约束相似，但它是一种更灵活的数据验证机制。
- 数据条件处理 - 使用在数据记录修改之前触发的触发器来实现。这允许对新数据值进行修改或根据预定义值进行条件处理。
- 数据完整性 - 可用于确保跨表依赖关系的维护。触发动作可能涉及更新相关表中的数据记录。这类似于引用完整性，但它是一个更灵活的替代方案。

## 触发器的激活 (Trigger Activation)

触发器可以按两种方式之一定义为触发（激活）：

- **触发前触发器 (before trigger)** 会在触发 SQL 语句执行之前，针对受影响行集中的每行触发。因此，触发器主体在新数据值被插入或更新到表之前看到这些值。
- **触发后触发器 (after trigger)** 会在语句成功完成后，针对受影响行集中的每行触发（取决于定义的粒度）。因此，触发器主体看到的表处于一致状态。（所有事务都已完成。）

关于触发器的另一个重要特性是它们可以触发其他触发器（或同一个触发器）或其他约束。这些被称为级联触发器。
