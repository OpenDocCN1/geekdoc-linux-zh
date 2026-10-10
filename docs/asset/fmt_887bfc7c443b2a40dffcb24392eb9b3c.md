
`CURRENT REFRESH AGE`特殊寄存器指定了一个数据类型为`DECIMAL(20,6)`的时间戳持续。该持续时间自延迟刷新摘要表处理`REFRESH TABLE`语句以来的最大时间。它决定了摘要表是否可以优化查询的处理。`SET REFRESH AGE`语句允许你更改`CURRENT REFRESH AGE`寄存器的值。该值必须是0或9999999999999（年、月、日、分、秒）。

- 零（0）意味着只有使用`REFRESH IMMEDIATE`定义的摘要表可以优化查询的处理。
- 9999999999999意味着任何使用`DEFERRED`或`REFRESH IMMEDIATE`定义的摘要表都可以用于优化查询的处理。

注意：关键字`ANY`是9999999999999的简写。`CURRENT REFRESH AGE`的初始值为0。如果你希望DB2优化器考虑使用延迟刷新摘要表，你必须如下所示将`CURRENT REFRESH AGE`特殊寄存器设置为`ANY`或9999999999999：

```sql
SET CURRENT REFRESH AGE ANY
```

### 使用摘要表的考虑因素

在创建摘要表时有一些考虑因素。摘要表定义的完整`SELECT`不得包含：

- `FROM`子句中对视图（详情请阅DB2 UDB V8.1 SQL Reference）、摘要表或表的引用
- 引用类型表达式或基于这些类型的唯一类型表达式
- 具有外部动作的函数
- 依赖于物理特征的函数（例如`PARTITION`）
- 对系统对象的表或视图引用（也不应指定）

你应该注意的其他考虑因素：

- 摘要表不支持`IMPORT`或`LOAD`。
- 摘要表上无法创建唯一索引。
- 如果在`ALTER TABLE`语句中指定摘要表，则`ALTER`限于`NOT logged initially`、`locksize`、`append`或`volatile`。

此外，如果你使用`REFRESH IMMEDIATE`选项创建摘要表，则存在以下考虑因素：

- 摘要表定义中的完整`SELECT`必须是一个子查询，且不能包含：
  - 非确定性函数
  - 标量完整`SELECT`
  - 带有完整`SELECT`的谓词
  - 特殊寄存器
- 子查询中必须包含`GROUP BY`子句。
- 选择列表必须具有`COUNT(*)`函数或`COUNT_BIG(*)`，且不能有`DISTINCT`。
- 选择列表中仅允许`SUM`（非空列）、`COUNT`或`COUNT_BIG`函数（不带`DISTINCT`），其他选择列表项必须包含在`GROUP BY`子句中。
- 所有`GROUP BY`项必须包含在选择列表中。
- 不允许分组集（包括`CUBE`和`ROLLUP`）或对常数进行分组。
- 不允许`HAVING`子句。

# 摘要表

### 摘要表的系统目录信息

系统目录表维护有关摘要表以及普通表的信息。以下是`LIST TABLES`命令的输出。`type`列中的值`S`表示该表是摘要表。

| 表/视图 |  | 类型 | 创建时间 |
| :--- | :--- | :--- | :--- |
| DEPT_GROUP | AUSRES33 | S | 1999-04-19-16.21.49 |
| DEPT_GROUP | AUSRES33 | S | 1999-04-19-16.21.48 |

图 7–66 LIST TABLES命令的输出显示摘要表

### 用户维护的摘要表

在某些情况下，用户已经在生成汇总数据。例如，在将原始数据加载到数据库之前，可能会运行夜间批作业来按商店、地区和国家计算销售额。在这种，将这些数据放入用户定义的摘要表中可能有利。

用户维护的摘要表与系统摘要表的区别在于摘要表的创建和加载由用户控制。由于数据是由用户生成的，DB2不刷新这些信息，因此用户必须定期更新表。此外，DB2会假设摘要表中的信息是正确的，如果用户没有加载有效信息，则可能会产生错误的结果。

要创建用户维护的摘要表，必须在`CREATE TABLE`命令末尾添加`MAINTAINED BY USER`选项。图 7–64中的示例在以下示例为用户维护的摘要表（见图 7–67）：

```sql
CREATE SUMMARY TABLE UMST_EMPLOYEE AS (
  SELECT
    WORKDEPT, COUNT(*) AS EMPCOUNT,
    SUM(SALARY) AS TOTSALARY,
    SUM(BONUS) AS TOTBONUS
  FROM EMPLOYEE GROUP BY WORKDEPT
) DATA INITI DEFERRED REFRESH MAINTAINED BY USER;
```

图 7–67 创建用户定义的摘要表

一旦创建了表，用户就可以从应用程序加载数据并根据这些信息优化查询。在加载数据之前，必须将摘要表退出检查等待状态（见图 7–68）：

```sql
SET INTEGRITY FOR UMST_EMPLOYEE ALL IMMEDIATE UNCHECKED;
```

图 7–68 重置检查等待条件

发布`CHECK INTEGRITY`命令后，用户可以使用`insert`语句加载此表。例如，可以使用以下SQL从`EMPLOYEE`表用当前信息加载此摘要表：

```sql
INSERT INTO UMST_EMPLOYEE
SELECT * FROM (
  SELECT WORKDEPT, COUNT(*), SUM(SALARY), SUM(BONUS)
  FROM EMPLOYEE
  GROUP BY WORKDEPT
) AS T;
```

图 7–69 加载摘要表

## 设置当前维护的表类型以优化 = NONE;

**图 7–70** 优化设置

将寄存器设置为`NONE`将防止在SQL处理过程中使用任何摘要表（summary tables）。但是，如果您希望利用已创建的摘要表，则应将此值设置回来。请注意，此特殊寄存器可以包含四个值之一：

- *ALL*
指定在优化动态SQL查询处理时，要考虑由此特殊寄存器控制的所有可能的维护表类型（包括现在和未来）。
- *NONE*
指定在优化动态SQL查询处理时，不考虑任何由此特殊寄存器控制的类型类型。
- *SYSTEM*
指定在优化动态SQL查询处理时，可以考虑系统维护的延迟刷新物化查询表（refresh-deferred materialized query tables）（即时物化查询表始终会被考虑）。
- *USER*
指定在优化动态SQL查询处理时，可以考虑用户维护的延迟刷新物化查询表。

除了此寄存器外，用户还需要设置`REFRESH AGE`以确保DB2将使用这些用户维护的摘要表。如果该值设置为`0`，DB2将仅考虑物化查询表。

## 设置 REFRESH AGE

**图 7–71** 当前刷新值

## 物化查询表

物化查询表（materialized query table）是一种基于查询结果的表，其定义基于一个或多个表，并由DB2自动维护。以下两个SQL语句强调了摘要表和物化查询表之间的区别。第一个示例（图 7–72）是一个带有`GROUP BY`子句的典型摘要表。第二个示例（图 7–73）是包含两个表连接的物化查询表，且没有任何聚合函数。它们都需要在刷新之前使用。

```
CREATE SUMMARY TABLE Dept_group
AS (SELECT workdept,
    SUM(Salary) AS Salary,
    SUM(Bonus) AS Bonus
    FROM Employee GROUP BY workdept)
DATA INITIALLY DEFERRED
REFRESH DEFERRED;
```

```
CREATE SUMMARY TABLE EPL
AS (SELECT EMPNO, LASTNAME, DEPT, DEPTNAME
FROM EMPLOYEE E, DEPARTMENT D
WHERE E.DEPT = D.DEPT)
DATA INITIALLY DEFERRED
REFRESH DEFERRED;
```

图 7–73 物化查询表

物化查询表可以用于预连接表。如果物化表包含了所需的列和行，这将允许优化器跳过连接。

## 序列

许多应用程序需要使用序列号来跟踪发票号、客户号和其他在需要新项目时递增的对象。DB2可以通过标识列（identity columns）在表中自动递增值（参见第220页的“标识列”）。这种技术对于单表非常有效，但生成跨多个表的唯一值可能不是最方便的方法。

DB2中的`SEQUENCE`对象允许DBA或开发人员创建一个程序控制的递增值，它可以用于不同的表。图 7–74显示了使用整数类型创建示例序列号：
