
如所述，表层次结构创建一个层次表（H-Table）。表层次结构中类型表的所有列和所有行都存储在一个层次表中。让我们看看示例中的 `PERSON_HIERARCHY` 表（它是我们示例的层次表），并查看针对类型表的 `SELECT` 语句是如何处理的。注意，层次表不能通过 SQL 语句直接操作。请看以下三个示例：

```sql
SELECT * FROM Person;
SELECT * FROM Emp;
SELECT * FROM OUTER(Emp);
```

结果如图 7–61 所示。该图显示了示例的层次表以及查询结果。

# 第 7 章 高级 SQL

## Person_Hierarchy

```sql
Select * from Person
select * from Emp
```

| OID | NAME | BIRTHYEAR SALARY DEPT SPECIALITY MAJOR ARCHVM |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 10 John | 1968 | | | | |
| 20 Paul | 1961 | | | | |
| 30 Pat | 1970 | 60000 | 10 | | |
| 40 Hitomi | 1977 | 65000 | 20 | | |
| 90 Lou | | | | | |
| 50 Sam | 1968 | 60000 | 40 | | |
| 60 utta | 1961 | 95000 | 30 | | |
| 70 Rich | 1941 | 90000 | 30 | | | |
| 80 Herb | 1962 | 120000 | 30 | | | |
| 100 Franzi | 1975 | | | | | 2.50 |
| 110 Herb | 1980 | | | | | 1.70 |

```sql
Select * from OUTER(Emp)
```

图 7–61 示例：层次表的逻辑视图（H表）

**注意：** 记住不能直接从层次表中查询。

现在来看其他示例。此示例插入了一个 OID 为 200、出生于 1968 年、工资为 65000 且在 ITSO 部门工作的员工 TETSU。

```sql
INSERT INTO Emp (Oid, Name, Birthyear, Dept)
VALUES(Emp_t(200,'Tetsu',1968,65000,(SELECT Oid FROM Dept WHERE Name='itsso')));
```

下一个示例选择所有 1970 年之后出生且年薪超过 50000 的员工属性。

```sql
SELECT * FROM emp WHERE birthyear > 1970 AND salary > 50000
```

是从 EMP 和 PROF 表检索的。结果如下：

| OID | NAME | BIRTHYEAR | SALARY | DEPT |
| :--- | :--- | :--- | :--- | :--- |
| 40 | Hitomi | 1977 | 65000 | 20 |

下一个示例选择所有在 1965 年之前出生的学生或人员（排除员工和教授）。

```sql
SELECT * FROM Person Birthyear < 1965 AND DEREF(oid) IS OF DYNAMIC (Student_t,ONLY Person_t)
```

此示例使用了 TYPE 谓词，将动态类型与类型列表进行比较。如已解释，如果动态类型在列表中，则谓词为真。在我们的示例中，指定了 `STUDENT_T` 和 `PERSON_T`（带有 `ONLY` 关键字）。因此，只返回类型为 `STUDENT_T`、其子类型（尽管 `STUDENT_T` 没有任何子类型）或 `PERSON_T` 的行。结果为：

| OID | NAME | BIRTHYEAR |
| :--- | :--- | :--- |
| 20 | Paul | 1961 |

让我们来看看引用列示例。记住 `DEPT` 表和 `EMP` 表具有图 7–62 所示的相互引用关系。

图 7–62 引用列

下一个示例查找员工姓名、工资、Dept->Name 部门名称以及 Dept->Budget 预算。它选择预算大于 $500000 的员工。

```sql
SELECT Name, Salary, Dept->Name, Dept->Budget FROM Emp
WHERE Dept->Budget > 500000;
```

注意部门名称和部门预算是从 `dept` 表检索的，该表被 `Emp` 表及其子表 `PROF` 表的引用列 `dept` 引用。结果如下：

| NAME | SALARY | NAME | BUDGET |
| :--- | :--- | :--- | :--- |
| Sam | 60000 | itsso | 1000000 |
| Uta | 95000 | headq | 500000 |
| Rich | 90000 | headq | 500000 |
| Herb | 120000 | headq | 500000 |
| Tetsu | 65000 | itsso | 500000 |

## 汇总表

汇总表是定义基于查询结果的表。因此，汇总表通常包含基于其定义所在的表（或多个表）中存在的数据预计算结果。如果 DB2 优化器确定动态查询在汇总表的执行比在基表更高效，则查询将在汇总表执行，你将比其他情况下更快获得结果。

注意：DB2 第 8 版本引入了物化查询表（materialized query table）术语。物化查询表是基于查询结果定义的表，其数据是以从物化查询表定义的表中提取的预计算结果的形式。包含 `GROUP BY` 子句的物化查询表 `fullselect` 会对 `fullselect` 中引用的表进行数据汇总。此类物化查询表称为汇总表。汇总表是物化查询表的一种特殊类型。

当优化器确定可以使用汇总表的数据而不是访问基表来回答查询时，查询重写函数将访问汇总表。

### 创建摘要表

可以通过 `CREATE TABLE` 语句创建摘要表。图 7–64 显示了用于创建摘要表的 `CREATE TABLE` 语句。

```sql
CREATE SUMMARY TABLE Dept_group
AS (SELECT workdept,
    SUM(Salary) AS Salary,
    SUM(Bonus) AS Bonus
FROM Employee GROUP BY workdept)
DATA INITIALLY DEFERRED
REFRESH DEFERRED;
```

图 7–64 创建摘要表

在此示例中，使用了 `SUMMARY` 关键字来指示这是一个摘要表；但是，如果你愿意，可以省略该关键字。`AS` 关键字后接完整的 `SELECT` 语句意味着这是一个摘要表。摘要表的列属性由此完整的 `SELECT` 语句定义。

更新摘要表中的数据有两种选项：延迟刷新（deferred refresh）和立即刷新（immediate refresh）。这在 `CREATE TABLE` 语句中使用 `REFRESH DEFERRED` 或 `REFRESH IMMEDIATE` 来指定。上一个示例使用了 `REFRESH DEFERRED`，这意味着摘要表中的数据反映的是执行 `REFRESH TABLE` 语句时的查询结果。`REFRESH IMMEDIATE` 意味着作为 `DELETE`、`INSERT` 或 `UPDATE` 语句一部分对底层表进行的更改立即级联到摘要表。

`DATA INITIALLY DEFERRED` 子句表示在 `CREATE TABLE` 语句执行时不向表中插入数据，`REFRESH TABLE` 语句是填充表的唯一方法。

注意：创建摘要表后，该表处于检查等待（check-pending）状态。使用 `REFRESH TABLE` 语句或带有 `IMMEDIATE` 选项的 `SET INTEGRITY` 语句可以让你退出检查等待状态。

图 7–65 显示了使用 `REFRESH IMMEDIATE` 选项创建摘要表的 `CREATE TABLE` 语句。

```sql
CREATE SUMMARY TABLE dept_group2
AS (SELECT workdept,
   count(*) as recount,
   SUM(salary) AS salary,
   SUM(bonus) AS bonus
FROM employee GROUP BY workdept)
DATA INITIALLY DEFERRED
REFRESH IMMEDIATE);
```

图 7–65 创建带有 REFRESH IMMEDIATE 的摘要表

注意：摘要表不能通过 `INSERT`、`UPDATE` 或 `DELETE` 语句直接修改。

#### CURRENT REFRESH AGE 特殊寄存器
