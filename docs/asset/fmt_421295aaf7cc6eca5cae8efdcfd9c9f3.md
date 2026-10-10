
MDC 索引还可以与其他索引进行 AND/OR 逻辑操作（如果它们存在的话）。这意味着 MDC 索引可以在需要使用其他索引之前减小结果集。使用 MDC 表还可能减少对许多已有的额外索引的需求。

![](img/ca7cfad01341360e684d5dd2379b19e9_276_0.png)

# 加载与删除处理

可以使用 DB2 随带的高速 `LOAD` 命令对 MDC 表进行加载。加载器感知 MDC 表的结构，因此将生成适当的信息块。它还将利用删除活动期间可能创建的现有空闲区段（free extents）。

MDC 表的一个重要方面是删除后对现有空间的回收。当某个区段由于删除操作而被清空记录时，DB2 将此区段释放回表空间以供将来使用。对于标准 SQL 表，在下发重组命令之前，空间不会被回收。在 MDC 的情况下，空闲空间对用户立即可用，消除了重组表的需要。但在长时间推移下，区段内的页面可能会碎片化（行溢出），DBA 可能希望对 MDC 表运行重组命令。在大多数情况下，这是一种非常少见的活动。

# MDC 性能

初步测试表明，MDC 可以将某些查询的速度提高 50% 以上。这种改进大部分源于缩短记录块的搜索和访问时间。选择单个记录仍然需要传统的索引来确保良好的性能，但 MDC 将显著提高对组记录的访问。这种收益适用于事务型（OLTP）和业务智能（BI）工作负载。

等等，再次查看原文：“但 MDC 将显著提高对组记录的访问。这种收益可以适用于事务型（OLTP）和业务智能（BI）负载。”

对于 OLTP 负载，MDC 表提高了性能。对于 BI 负载，MDC 表将提供更优的性能。

# 视图 278

视图是使用 `CREATE VIEW` 语句创建的虚拟表。一旦定义了视图，可以使用 DML 语句进行访问，就像访问表一样。视图是一个临时结果，仅在查询处理期间可用。我们将在第 343 页的“高级 SQL”中讨论。

通过视图，你可以让应用程序访问表的子集，并验证所插入或更新的数据。视图可以具有与原始表列名不同的列名。视图的使用为应用程序和终端用户查看数据提供了灵活性。

下方显示了一个示例视图。底层表 `EMPLOYEE` 拥有 `SALARY` 和 `COMM` 列。出于安全考虑，此视图根据 `ID`、`NAME`、`DEPT`、`JOB` 和 `HIREDATE` 列创建。此外，我们限制了对 `DEPT` 的访问。此定义仅显示部门为 10 的员工信息。

```sql
CREATE VIEW EMP_VIEW1
(EMPID, EMPNAME, DEPT, JOBTITLE, HIREDATE)
AS SELECT ID,NAME,DEPT,JOB,HIREDATE FROM EMPLOYEE
WHERE DEPT=10;
```

视图定义后，可以指定访问权限。这提供了数据安全性，因为可以访问的是受限的视图。正如我们所看到的，视图可以包含 `WHERE` 子句来限制某些行，也可以包含列子集来限制某些列的数据。

视图中的列名不需要与基表的列名匹配。表名有一个关联模式（schema），视图名亦然。

一旦定义了视图，可以使用 `SELECT`、`INSERT`、`UPDATE` 和 `DELETE` 等 DML 语句（带限制的）。数据库管理员可以决定为一组用户在视图上提供比基表更高的权限。

该选项确保数据库中被修改数据的完整性。如果在执行 `INSERT` 或 `UPDATE` 操作期间违反了条件，将返回 SQL 错误。

图 5–26 是一个带有 `CHECK OPTION` 的视图定义示例。需要 `WITH CHECK OPTION` 来确保条件始终被检查。你希望 `DEPT` 始终为 10。这将限制 `DEPT` 列的输入值。当使用视图插入新值时，始终会强制执行 `WITH CHECK OPTION`。

```
CREATE VIEW EMP_VIEW2
(EMPNO,ENAME,DEPTNO,JOBTITLE,HIREDATE)
AS SELECT EMPNO,ENAME,DEPT,JOB,HIREDATE from EMPLOYEE
WHERE DEPT=10
WITH CHECK OPTION;
```

**图 5–26** 使用 WITH CHECK OPT 的视图定义

如果将图 5–26 中的视图用于 `INSERT` 语句，如果 `DEPTNO` 列的值不为 10，则该行将被拒绝。需要记住的一点是，如果没有指定 `CHECK OPTION`，则在修改数据期间将不会进行数据验证。

如果将图 5–26 中的视图用于 `SELECT` 语句，则会调用条件（`WHERE` 子句），结果表将仅包含匹配的数据行。换句话说，`WITH CHECK OPTION` 不影响 `SELECT` 语句的结果。

在以下视图中必须指定 `WITH CHECK OPTION`：

- 使用 `READ ONLY` 选项定义的视图（只读视图）
- 引用了 `NODENUMBER` 或 `PARTITION` 函数（非确定性函数，例如 `RAND`）或具有外部操作的函数的视图
- 类型视图（有关类型化视图的详细信息，请参阅第 343 页的“高级 SQL”）

## 嵌套视图定义

如果一个视图基于另一个视图，则必须评估的谓词数量取决于 `WITH CHECK OPTION` 的指定。

如果定义视图时**没有** `CHECK OPTION`，则该视图的定义不会用于任何插入或更新操作的数据有效性检查。然而，如果该视图直接或间接地依赖于另一个带有 `WITH CHECK OPTION` 定义的视图，则该父视图的定义将用于任何插入或更新操作的检查。

## 数据库对象的管理

如果使用 `WITH CASCED CHECK OPTION` 或仅 `WITH CHECK OPTION`（`CASCED` 是 `WITH CHECK OPTION` 的默认值）定义视图，则视图的定义将用于任何插入或更新操作的检查。此外，视图将从其所依赖的任何可更新视图继承搜索条件。即使这些视图不包含 `CHECK OPTION`，这些条件也会被继承。然后，继承的条件将相乘，以符合适用于该视图或任何基于该视图的视图的插入或更新操作的约束。

例如，如果视图 `v2` 基于视图 `v1`，且 `v2` 的检查选项使用 `WITH CASCED CHECK OPTION` 定义，则对视图 `v2` 执行 `INSERT` 和 `UPDATE` 语句时，两个视图的谓词都将被评估。图 5–27 显示了一个使用 `WITH CASCED CHECK OPTION` 的 `CREATE view` 语句。`EMP_VIEW3` 创建在视图 `EMP_VIEW2` 之上的，而 `EMP_VIEW2` 是带有 `CHECK OPTION` 创建的（图 5–26）。如果你想向 `EMP_VIEW3` 插入或更新记录，该记录应具有 `DEPTNO=10` 且 `EMPNO>20` 值。

> 注意：注意，如果 `EMP_VIEW2` 不包含 `CHECK OPTION`，则对 `EMP_VIEW3` 的插入或更新操作将强制执行 `DEPTNO=10` 条件。

```
CREATE VIEW EMP_VIEW3 AS
SELECT EMPNO,EMPNAME,DEPTNO FROM EMP_VIEW2
WHERE EMPNO >20
WITH CASCED CHECK OPTION;
```

**图 5–27** 使用的视图定义

在创建视图时也可以指定 `LOCAL CHECK OPTION`。如果在创建视图时使用 `LOCAL CHECK OPTION`，该视图将从其所依赖的任何可更新视图继承搜索条件。即使这些视图不包含 `CHECK OPTION`，这些条件也会被继承。例如，请参考图 5–28 中的示例。

```
CREATE TABLE T1
(C1 INT, C2 INT, C3 INT, C4 INT, C5 INT);
CREATE VIEW V1 AS
SELECT * FROM T1 WHERE C1=1;
CREATE VIEW V2 AS
SELECT * FROM V1 WHERE C2=1 WITH CHECK OPTION;
CREATE VIEW V3 AS
SELECT * FROM V2 WHERE C3=1;
CREATE VIEW V4 AS
SELECT * FROM V3 WHERE C4=1 WITH LOCAL CHECK OPTION;
CREATE VIEW V5 AS
SELECT * FROM V4 WHERE C5=1 WITH CASCED CHECK OPTION;
```

**图 5–28** 嵌套表和视图

我们创建了一个表和五个视图。`v2` 依赖 `v1`，`v3` 依赖 `v2`，`v4` 依赖 `v3`，`v5` 依赖 `v4`。`v2` 带有 `CHECK OPTION`，而 `v4` 带有 `LOCAL CHECK OPTION`。

让我们对这些视图测试一些插入语句：

- 1. 此插入语句成功，因为 `v1` 不包含 `CHECK OPTION`。

`INSERT INTO V1 VALUES (2,1,1,1,1);`

- 2. 下一个插入语句将报错，因为 `v2` 带有 `CHECK OPTION`，且值不符合 `v2` 的定义。

`INSERT INTO V2 VALUES (1,2,1,1,1);`

- 3. 此插入语句成功，因为 `v2` 不包含 `LOCAL CHECK OPTION`，这意味着 `v2` 的定义不被用于检查。

`INSERT INTO V2 VALUES (2,1,1,1,1);`
