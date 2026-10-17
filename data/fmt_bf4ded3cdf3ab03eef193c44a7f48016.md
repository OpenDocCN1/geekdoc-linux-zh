
```sql
CREATE TABLE CANDIDATE
(
CID CANDIDATE_ID NOT NULL,
LNAME VARCHAR(10) NOT NULL,
FNAME VARCHAR(8) NOT NULL,
INITIAL CHAR(1),
HPHONE,
WPHONE PHONE,
STREETNO VARCHAR(8),
STREETNAME VARCHAR(15) NOT NULL,
CITY VARCHAR(10) NOT NULL,
PROV_STATE VARCHAR(10) NOT NULL,
CODE CHAR(6) NOT NULL,
COUNTRY VARCHAR(10) NOT NULL,
CERT_DBA CHAR(1) NOT NULL WITH DEFAULT,
CERT_APP CHAR(1) NOT NULL WITH DEFAULT,
PRIMARY KEY (CID)
);
```

`图 15–12` `CANDIDATE` 表的定义

该表的定义中使用了许多用户定义类型（UDT）。例如，创建了一个名为 `CANDIDATE_ID` 的 UDT，用于表示该个人的唯一标识符。在表定义的后续，创建了多个字段用于存储考者在表中的地址信息。这些多个字段可以组合为一个结构化数据类型定义，如图 15–13 所示。

```sql
CREATE TYPE ADDRESS_TYPE AS
(
STREETNO VARCHAR(8),
STREETNAME VARCHAR(15),
CITY VARCHAR(10),
PROV_STATE VARCHAR(10),
CODE CHAR(6),
COUNTRY VARCHAR(10)
)
MODE DB2SQL WITH FUNCTION ACCESS INSTANTIABLE;
```

`图 15–13` 创建结构化数据类型

既然定义已经创建，我们可以将其作为表创建的一部分：

```sql
CREATE TABLE CANDIDATE
(
CID CANDIDATE_ID NOT NULL,
LNAME VARCHAR(10) NOT NULL,
FNAME VARCHAR(8) NOT NULL,
INITIAL CHAR(1),
HPHONE PHONE,
WPHONE PHONE,
ADDRESS ADDRESS_TYPE NOT NULL,
CERT_DBA CHAR(1) NOT NULL WITH DEFAULT,
CERT_APP CHAR(1) NOT NULL WITH DEFAULT,
PRIMARY KEY (CID))
```

`图 15–14` 创建带有地址结构的 `CANDIDATE` 表

结构化数据类型的使用可以帮助简化具有许多共同元素的表定义。这使得使用面向对象的技术开发应用程序变得更加容易。你的结构化数据类型可以包含其他结构化数据类型作为 UDT 嵌套在其中。

在表定义中使用这些数据类型时，你需要注意一些管理上的变化。第一个变化是元素如何插入到表中。关系模型始终假设一列包含一个值。由于这种限制，需要一些新的运算符来允许将结构插入到表中。例如，`INSERT` 命令需要知道如何插入一个结构。

为了说明这些新运算符的使用，我们将创建一个具有 `COMPENSATION` 结构化数据类型的新表。

## 第 15 章 开发 SQL

```sql
CREATE TYPE COMPENSATION AS
(
  SALARY INT,
  BONUS INT,
  COMMISSION INT
)
MODE DB2SQL WITH FUNCTION ACCESS INSTANTIABLE; -- 将 INSTANTABLE 修正为 INSTANTIABLE
```

`图 15–15` 创建 `COMPENSATION` 数据类型

`COMPENSATION` 结构包含了组成个人薪水的三个元素。该结构将用于创建 `EMPLOYEE` 表。

```sql
CREATE TABLE EMPLOYEE
(
  NAME CHAR(10),
  PAY COMPENSATION
)
```

`图 15–16` 使用 `COMPENSATION` 数据类型创建 `EMPLOYEE` 表

此时，我们需要向 `EMPLOYEE` 表插入一些信息。要向 `PAY` 列插入值，我们使用 `COMPENSATION` 构造函数（类似于强制转换函数）：

```sql
INSERT INTO EMPLOYEE VALUES (
  'Shirley'..SALARY(30000)..BONUS(1000)..COMMISSION(3000)
)
```

`图 15–17` 向 `EMPLOYEE` 表插入结构

`COMPENSATION` 构造函数告诉 `DB2` 随其后的字段构成了结构的一部分，双点符号“..” 组合了这些元素。由于 `PAY` 列被定义为 `COMPENSATION` 类型，因此需要的值必须强制转换为 `COMPENSATION` 类型。

对开发者来说的是，你还可以生成一个 `PAY` SQL 体函数，使语法更具可读性。

```sql
CREATE FUNCTION PAY(A INT, B INT, C INT)
RETURNS COMPENSATION
LANGUAGE SQL
RETURN COMPENSATION(A, B, C);
```

`图 15–18` 创建 `PAY` 函数（注：此处文本破碎，已根据标准 SQL 逻辑重建）

现在插入结构的 SQL 可以简化为：

```sql
INSERT INTO EMPLOYEE VALUES (
  'Shirley'..SALARY(30000)..BONUS(1000)..COMMISSION(3000)
)
```

`图 15–19` 使用 `PAY` 构造函数

数据插入表后，你使用使用点符号来提取元素。当你定义了结构化数据类型时，`DB2` 生成的结果相同：

```sql
SELECT NAME, PAY.SALARY, PAY.BONUS, PAY.COMMISSION
FROM EMPLOYEE;
```

| NAME | SALARY | BONUS | COMMISSION |

|---|---|---|---|

| SHLEY | 30000 | 1000 | 3000 |

| KATRINA | 40000 | 2000 | 6000 |

`图 15–20` 从 `EMPLOYEE` 表查询信息

在为列创建转换（transforms）时，开发者或 DBA 应该理解用户如何解释该列。之前定义的转换函数将 `PAY` 列表示为字符字符串。对于一个期望从数据库返回单个值的用户来说，这可能很奇怪。一个更直观的定义是让 `SHOW_PAY` 函数通过相加所有列来计算员工的实际 `PAY`。图 15–26 中的 SQL 创建了一个返回三个 `PAY` 元素之的函数。

```sql
CREATE FUNCTION SHOW_PAY (P FOR COMPENSATION)
RETURNS INT
LANGUAGE SQL
RETURN P.SALARY + P.BONUS + P.COMMISSION;

SELECT NAME, SHOW_PAY(PAY) FROM EMPLOYEE;

NAME             2
----------------
SHIRLEY          34000
KATRINA          48000

SELECT * FROM EMPLOYEE;

NAME             PAY
------------------
SHIRLEY          34000
KATRINA          48000
```

`图 15–26` 用于显示 `PAY` 列的替代函数

创建一个像 `SHOW_PAY` 这样返回单个值的函数的优势是，它现在可以在常规 SQL 语句中使用，根据个人的总薪资来选择记录。例如，以下的 SQL 语句将仅返回总薪资大于 45000 的员工。

```sql
SELECT * FROM EMPLOYEE
WHERE SHOW_PAY(PAY) > 45000;

NAME             PAY
------------------
KATRINA          48000
```

`图 15–27` 用于显示 `PAY` 列的替代函数

用户定义结构化数据类型和用户定义函数是 `DB2` 中的强大功能。开发组可以创建在数据库内部使用的通用结构和程序。这可以对数据定义进行更好的控制，并通过使用 UDFs 鼓励更多的代码复用。

## 模式 (Schemas) 与别名 (Aliases)

在本节中，我们将讨论两个数据库对象：模式和别名，这些对象在之前的章节中尚未详细讨论。

## 模式 (Schema)

模式是一个数据库实体，代表 `DB2` 数据库中一组命名的对象集合。模式名称实际上是所访问对象完全限定名的一部分。当使用 SQL `CREATE <db object>` 语句定义数据库对象时，应在数据库对象的名称中提供限定符或模式名称。
