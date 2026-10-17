
此选项指示 SQL 过程在结束时将保留在内存中（`YES`）还是否（`NO`）。

## PROGRAM TYPE

此选项指定 SQL 过程将作为子程序（`SUB`）还是主程序（`MAIN`）运行。

## SECURITY

此选项指示 SQL 过程如何与外部安全产品交互以控制对非 SQL 资源的访问。可能的值包括：

- `DB2`。SQL 过程不需要特殊的外部环境。如果它访问受外部安全产品保护的资源，将使用与 SQL 过程关联的授权 ID。`DB2` 是默认值。
- `USER`。应为 SQL 过程建立外部安全环境。如果访问受安全产品保护的资源，将使用调用过程的用户授权 ID 进行访问。
- `DEFINER`。应为 SQL 过程建立外部安全环境。如果访问受安全产品保护的资源，将使用过程所有者的授权 ID 进行访问。

## RUN OPTIONS

此选项指示用于 SQL 过程的语言环境运行时选项。

## 返回时提交 (COMMIT ON RETURN)

此选项指示从 SQL 过程返回时是否自动发出 `COMMIT`，无论 SQL 过程中是否显式编写了 `COMMIT` 或 `ROLLBACK`。默认值为 `No`。

## STOP AFTER SYSTEM DEFAULT FAILURES 或 CONTINUE AFTER FAILURE

此选项指示在某些失败后 SQL 过程是否进入停止状态。可能的值包括：

- `STOP AFTER SYSTEM DEFAULT FAILURES`。使用 `install-DSNTIPX` 上的 `MAX ABEND COUNT` 来确定将 SQL 过程放入停止状态之前允许的失败次数。这是默认值。
- `STOP AFTER nn failures`。指示在 `nn` 次失败后将 SQL 过程放入停止状态。`nn` 可以是 1 到 32767 之间的整数。
- `CONTINUE AFTER FAILURE`。指定此 SQL 过程在任何失败后都不会进入停止状态。

## 总结

SQL 过程使用 `CREATE PROCEDURE` 语句定义。该语句定义了过程名称、参数以及其他属性。

SQL 过程逻辑在 `CREATE PROCEDURE` 语句的主体中定义。主体通常是一个由声明和随后的过程语句组成的复合语句。`DECLARE` 语句用于声明变量、数据类型以及可选的默认值。`SET`、`SELECT...INTO` 和 `VALUES` 等语句也可用于为变量赋值。

本章演示了带有某些过程语句的简单过程。其他 SQL PL 语句将在本书其余部分详细讨论。

# 第 3 章

# SQL PL 语言元素概述

在本章中，你将学习到：

- DB2 数据类型及其值的范围
- 如何处理大对象（large objects）
- 如何选择合适的数据类型
- 如何处理用户定义数据类型 (`UDTs`)
- 如何处理数据、时间和以及字符串数据
- 如何使用生成列（generated columns）
- 如何使用 `SEQUENCE` 对象和 `IDENTITY` 列

现在你已经学习了基础的 DB2 SQL 存储过程结构，在讨论该语言的任何更高级特性之前，是时候对 DB2 SQL PL 语言元素及其用法进行概述了。本章涵盖的主题许多决策——例如选择合适的数据类型，以及 `SEQUENCE` 对象、`IDENTITY` 列和生成列的使用——通常是在数据库设置和创建表期间完成的任务。在 SQL 存储过程、用户定义函数 (`UDFs`) 和触发器中参数和局部变量的数据类型选择（这些在书的其余部分将有详细介绍），大部分需要与底层表中的列定义相匹配。

## DB2 数据类型

数据类型告诉你是列或变量中可以存储什么类型的数据，以及该处值的大小可能有多大。DB2 中的数据类型分为两类：

- 内置数据类型
- 用户定义数据类型

### 有效 DB2 内置数据类型及其值范围

内置数据类型由 DB2 提供。DB2 支持满足你业务需求的大多种数据类型。图 3.1 显示了 DB2 内置数据类型的总结。

![](img/9d51a546e0768370c360e261a8d35de5_63_0.png)

**图 3.1** DB2 内置数据类型。

> 注意
>
> DB2 for LUW 仅为了向后兼容支持 `LONG VARCHAR` 和 `VARGRAPHIC` 数据类型。它们已被弃用，这意味着这些数据类型在未来将不再被支持。请改用 `VARCHAR` 和 `VARGRAPHIC`。

DB2 for iSeries 和 zSeries 支持 `ROWID` 数据类型。`ROWID` 数据类型用于唯一标识某行。使用 `ROWID` 的查询将直接导航到该行，因为列的含义包含了该行的位置。当行被插入表时，除非提供了值，否则 DB2 会为 `ROWID` 生成一个值。如果提供了，它必须是之前生成的值。`ROWID` 的值无法更新，即使在表空间重组后也不会改变。一个表中只能有一个 `ROWID` 列。

DB2 中有六种数值数据类型。它们的精度和值范围列于表 3.1。

#### 表 3.1 DB2 内置数值数据类型

| 数据类型 | 精度（位数） | 数据值范围 |
| :--- | :--- | :--- |
| `SMALLINT` | 5 | -32,768 到 32,767 |
| `INTEGER` | 10 | -2,147,483,648 到 2,147,483,647 |
| `BIGINT` | 19 | -9,223,372,036,854,775,808 到 9,223,372,036,854,775,808 |
| `DECIMAL`/`NUMERIC` | LUW, zSeries: 31 iSeries: 63 | LUW, zSeries: 31 位以内的任何值；iSeries: 63 位以内的任何值。 |
| `REAL` | LUW, iSeries: 24 zSeries: 21 | LUW: 最小 `REAL` 值 -3.402E+38 最大 `REAL` 值 +3.402E+38 最小正 `REAL` 值 +1.175E-37 最大负 `REAL` 值 -1.175E-37 iSeries: 最小 `REAL` 值 -3.4E+38 最大 `REAL` 值 +3.4E+38 最小正 `REAL` 值 +1.18E-38 最大负 `REAL` 值 -1.18E-38 zSeries: 最小 `REAL` 值 -7.2E+75 最大 `REAL` 值 +7.2E+75 最小正 `REAL` 值 +5.4E-79 最大负 `REAL` 值 -5.4E-79 |
| `DOUBLE` | 53 | LUW: 最小 `DOUBLE` 值 -1.79769E+308 最大 `DOUBLE` 值 +1.79769E+308 最小正 `DOUBLE` 值 +2.225E-307 最大负 `DOUBLE` 值 -2.225E-307 iSeries: 最小 `DOUBLE` 值 -1.79E+308 最大 `DOUBLE` 值 +1.79E+308 最小正 `DOUBLE` 值 +2.23E-308 最大负 `DOUBLE` 值 -2.23E-308 |

#### 表 3.1 DB2 内置数值数据类型（续上）

| 数据类型 | 精度（位数） | 数据值范围 |
| :--- | :--- | :--- |
| | | zSeries: 最小 `REAL` 值 -7.2E+75 最大 `REAL` 值 +7.2E+75 最小正 `REAL` 值 +5.4E–79 最大负 `REAL` 值 -5.4E–79 |

DB2 支持单字节和双字节字符字符串。DB2 使用双字节来表示字符串。其长度列于表 3.2。

#### 表 3.2 DB2 内置字符串类型

| 数据类型 | 最大长度 |
| :--- | :--- |
| `CHAR` | LUW, iSeries: 255 zSeries: 255 |
| `VARCHAR` | LUW, iSeries: 32760 zSeries: 32760 |
| `LONG VARCHAR` (仅 LUW) | 2147483647 |
| `CLOB` | 2147483647 |
| `GRAPHIC` | LUW, iSeries: 16383 zSeries: 16383 |
| `VARGRAPHIC` | LUW, iSeries: 32767 zSeries: 32767 |
| `DBCLOB` | 2147483647 |
| `BINARY` (仅 iSeries) | 32760 |
| `VARBINARY` (仅 iSeries) | 32767 |
| `BIT` | 2147483647 |

### 表 3.3 时间类型

| 描述 | 范围 |
| :--- | :--- |
| 最小 `DATE` 值 | 0001-01-01 |
| 最大 `DATE` 值 | 9999-12-31 |
| 最小 `TIME` 值 | 00:00:00 |
| 最大 `TIME` 值 | 23:59:59 |
| 最小 `TIMESTAMP` 值 | 0001-01-01-00:00:00 |
| 最大 `TIMESTAMP` 值 | 9999-12-31-23:59:59.999999 |

## 使用用户定义的区分类型

**用户定义的区分类型**是简单的用户定义数据类型（`UDT`），它们在现有的 DB2 数据类型基础上定义。DB2 还支持其他类型的 `UDT`，其定义范围由本书界定。在本书中，`UDT` 仅指代用户定义的区分类型。

`UDT` 可为你的数据赋予语义含义。创建 `UDT` 的语法如图 3.3 所示。

```
--CREATE DISTINCT TYPE--distinct-type-name--AS-------------------------------------
-->| source-data-type |--WITH COMPARISONS--------------------<<-
CREATE DISTINCT TYPE syntax
```

**图 3.3** `source-data-type`

`*source-data-type*` 可以是本章中讨论的任何 DB2 内置数据类型。`WITH COMPARISONS` 子句允许你在 `UDT` 上使用系统提供的针对源数据类型的操作符。对于 `BLOB`、`CLOB`、`DBCLOB`、`LONG VARCHAR`、`LONG VARGRAPHIC` 或 `DATALINK` 源数据类型，不允许使用 `COMPARISONS` 子句。

> 注意
>
> 在适用于 iSeries 和 zSeries 的 DB2 UDB 中，`COMPARISON` 子句是可选的。对于所有允许的源数据类型（`DATALINK` 除外），将创建比较运算符函数。

你可以使用 `UDT` 来强制执行业务规则，并防止不同数据被不当使用，因为 DB2 SQL PL 强制强类型。强数据类型在比较不同数据类型时需要更显式的强制转换，因为数据类型不会进行隐式转换。

为了向你展示一个示例，假设你定义了以下两个变量：

```
DECLARE v_in_mile DOUBLE;
DECLARE v_in_kilometer DOUBLE;
```

没有任何东西能阻止你执行如下错误操作：

```
IF (v_in_mile > v_in_kilometer)
```

该操作是没有意义的，因为在不转换其中一个的情况下，你无法比较英里和公里。但 DB2 无法识别这一点。对于 DB2 来说，这两个变量都是浮点数。将它们相加或直接比较它们是完全正常的。`UDT` 可用于防止此类错误。

## 第 3 章 SQL PL 元素概述

你可以创建两个新数据类型：`miles`和公里。

```
CREATE DISTINCT TYPE miles AS DOUBLE WITH COMPARISONS;
CREATE DISTINCT TYPE kilometers AS DOUBLE WITH COMPARISONS;
```

然后你可以使用 `UDT` 代替声明你的变量：

```
DECLARE v_in_mile miles;
DECLARE v_in_kilometer kilometers;
```

现在，如果你尝试执行相同的语句，将收到一个 SQL 错误：

```
SQL0401N The data types of the operands for the operation ">" are not
compatible. LINENUMBER=7. SQLSTATE=42818
```

```
IF (v_in_mile = v_in_kilometer)
```

如果这个错误是在预期之中，你可能会惊讶地发现以下语句也会导致相同的 SQL 错误：

```
IF (v_in_mile > 30.0)
```

这里发生了什么？答案是 DB2 要求你显式地将 `DOUBLE` 和米数据类型强制转换为 `miles` 数据类型。

当你创建一个用户定义的区分类型时，DB2 会为你生成两个强制转换函数：一个用于从 `UDT` 强制转换到源数据类型，另一个用于转换回来。

在此示例中，对于 `miles` `UDT`，你有这两个函数：

```
MILES
DOUBLE (MILES)
```

同样，对于 `kilometers` `UDT`，你有这两个函数：

```
KILOMETERS (DOUBLE)
DOUBLE (KILOMETERS)
```

为了使这两个语句生效，需要使用强制转换函数重写：

```
IF (v_in_mile > MILES(DOUBLE(v_in_kilometer)/1.6))
IF (v_in_mile > miles(30.0))
```

## 数据操作

你必须对 `v_in_kilometers` 进行两次强制转换，除非你手动创建，否则英里和公里之间没有强制转换函数。添加 1.6 的倍数是为了将公里转换为英里。

DB2 对数据操作有许多内置支持。由于处理日期、时间和字符串数据涉及复杂性，因此了解如何对这些数据类型使用系统提供的功能尤为重要。

## 处理日期和时间

日期和是数据库管理系统（`DBMS`）之间差异最大的数据类型。本节展示了一些基本日期时间操作的示例。你可以使用适当的 DB2 特殊寄存器提取当前日期、时间和时间戳：

```
SELECT CURRENT DATE FROM SYSIBM.SYSDUMMY1;
SELECT CURRENT TIME FROM SYSIBM.SYSDUMMY1;
SELECT CURRENT TIMESTAMP FROM SYSIBM.SYSDUMMY1;
```

`CURRENT DATE`、`CURRENT TIME` 和 `CURRENT TIMESTAMP` 是三个 DB2 特殊寄存器。另一个用于日期时间操作的有用 DB2 特殊寄存器是 `CURRENT TIMEZONE`。你可以使用它来获取经过 GMT/CUT 调整的 `CURRENT TIMESTAMP` 时间。你只需要从 `CURRENT TIME` 或 `CURRENT TIMESTAMP` 中减去 `CURRENT TIMEZONE` 寄存器即可：

```
SELECT CURRENT TIME - CURRENT TIMEZONE FROM SYSIBM.SYSDUMMY1;
SELECT CURRENT TIMESTAMP - CURRENT TIMEZONE FROM SYSIBM.SYSDUMMY1;
```

给定日期、时间或时间戳，你可以使用以下函数独立提取（年、月、日、小时、分、秒和微秒部分）：

```
SELECT YEAR (CURRENT TIMESTAMP) FROM SYSIBM.SYSDUMMY1;
SELECT MONTH (CURRENT TIMESTAMP) FROM SYSIBM.SYSDUMMY1;
SELECT DAY (CURRENT TIMESTAMP) FROM SYSIBM.SYSDUMMY1;
SELECT HOUR (CURRENT TIMESTAMP) FROM SYSIBM.SYSDUMMY1;
SELECT MINUTE (CURRENT TIMESTAMP) FROM SYSIBM.SYSDUMMY1;
SELECT SECOND (CURRENT TIMESTAMP) FROM SYSIBM.SYSDUMMY1;
SELECT MICROSECOND (CURRENT TIMESTAMP) FROM SYSIBM.SYSDUMMY1;
```

你也可以从时间戳中独立提取日期和时间：

```
SELECT DATE (CURRENT TIMESTAMP) FROM SYSIBM.SYSDUMMY1;
SELECT TIME (CURRENT TIMESTAMP) FROM SYSIBM.SYSDUMMY1;
```

## 第 3 章 SQL 语言元素概述

日期时间计算非常直观：

```
SELECT CURRENT DATE + 1 YEAR FROM SYSIBM.SYSDUMMY1;
SELECT CURRENT DATE + 3 MONTHS + 15 DAYS FROM SYSIBM.SYSDUMMY1;
SELECT CURRENT DATE + 5 HOURS - 3 MINUTES + 10 SECONDS FROM SYSIBM.SYSDUMMY1;
```

DB2 还提供了许多日期时间函数用于简单的日期时间操作。完整列表请参考文档。

## 处理字符串

与日期相比，字符串操作相对简单。大量使用了内置函数。你可以使用 `CONCAT` 函数或 `||` 运算符进行字符串拼接。以下两个示例完全相同：

```
SELECT CONCAT('ABC', 'DEF') FROM SYSIBM.SYSDUMMY1;
SELECT 'ABC' || 'DEF' FROM SYSIBM.SYSDUMMY1;
```

## 使用生成列

LUW 允许将列声明为生成列。它是从表达式推导出行值的列，用于将业务逻辑嵌入表定义中。生成列的语法如图 3.4 所示。

```
|--column-name--|
| data-type |
|--GENERATED--+--ALWAYS--+AS--+--(generation-expression)--|-
|--BY DEFAULT-|
```

**图 3.4** LUW 生成列语法

在插入行时为列生成值。支持两种选项：`GENERATED ALWAYS` 和 `GENERATED DEFAULT`。对于 `GENERATED ALWAYS` 标识列，DB2 对生成的值具有完全控制权，并保证唯一性。如果指定了显式值，将引发错误。另一方面，`GENERATED DEFAULT` 不保证唯一性。只有在插入时未指定值时，DB2 才会为列生成值。
