
### 图 14–3 db2cli.ini 配置示例

图 14–3 显示了 `db2cli.ini` 文件的示例。CLI 配置文件中可以指定更多选项，但选择这些选项是因为它们会极大地影响应用程序的执行环境。此处所示的关键字和值可能不适用于你的环境。

第一行是关于该文件此部分的注释。该文件中可以配置多个数据库。即使在 `db2cli.ini` 文件中没有条目，仍然可以通过 DB2 CLI 程序访问默认别名 `[DB2CERT]` `DB2` 数据库，但如果没有针对 `DB2CERT` 数据库的节（section），将使用所有参数的默认值。这可能并不尽如人意。

数据库名称下方的五行包含关键字和对应的值。受支持的关键字定义在《DB2 V7.1 级别接口指南和参考》中，但让我们查看图 14–3 中定义的关键字并在表 14–6 中对其进行解释。

### 表 14–6 配置 DB2 CLI 环境

| 关键字 | 含义 |
| :--- | :--- |
| `CURSORHOLD` | 0 = 游标不保持（提交操作时游标被销毁）1 = 游标保持（默认）。该关键字的默认值为 1。这意味着游标在跨工作单元时保持。这与嵌入式 SQL 不同，因为除非 `DECLARE CURSOR` 语句包含 `WITH HOLD` 短语，否则所有游标都表现出不标标的行为。 |
| `TNXISOLATION` | 1 - 未提交读 2 - 游标稳定（默认）4 - 读写一致性 8 - 可重复读 32 - 不提交（仅限 DB2 for OS/400）。此关键字标识了用于并发的隔离级别。 |

### 表 14–6 配置 DB2 CLI 环境（续）

| 关键字 | 含义 |
| :--- | :--- |
| `DEFERREDPARE` | 0 = 不使用延迟准备。1 = 使用延迟准备（默认）。推迟发送 `PREPARE` 请求，直到发送相应的执行请求。 |
| `DB2DEGREE` | 0-32767/ANY（默认值）。设置执行 SQL 语句的并行度。 |
| `PATCH1` | 2。用于特定应用程序或环境的变通方案。 |
| `PATCH2` | 使用逗号分隔的字符串指定多个值，例如 `"7,16"`。 |
| `DEFERREDPARE` | (注：上表关键字重复，此处根据原文逻辑翻译，应保持对应关系) |

在 Windows 和 OS/2 平台上的客户端配置助手允许你在不直接编辑 `db2cli.ini` 文件的情况下配置 CLI 环境。该界面易于使用，并解释了每个参数。

**图 14–4** 客户端配置助手中的 CLI 设置

## 通过 ODBC 访问 DB2 数据库

要通过 ODBC 访问 DB2 数据库，执行 ODBC 应用程序的客户端需要以下条件：

- 必须安装 DB2 运行时客户端或服务器。如果数据库是远程的，必须已正确目录化以便连接。
- 必须安装 ODBC 驱动管理器。
- 必须安装并注册 DB2 的 ODBC 驱动程序。
- DB2 数据库必须注册为 ODBC 数据源。

安装 ODBC 应用程序的计算机上必须安装 ODBC 驱动管理器。对于所有微软操作系统，ODBC 驱动管理器均由微软提供。

必须安装并注册 DB2 的 ODBC 驱动程序或其他 DB2 的 ODBC 驱动程序。在安装 DB2 时，只要取消勾选的 ODBC 组件，微软 ODBC 驱动管理器和 DB2 ODBC 驱动程序就会自动安装。在 Windows 平台上，你可以从控制面板运行微软 ODBC 管理器以验证“IBM DB2 ODBC Driver”是否在列表中。在 UNIX 平台上，DB2 ODBC 驱动程序以及通过其访问的数据库使用主目录下的 `.odbc.ini` 和 `.odbcinst.ini` 文件指定。

必须向 ODBC 驱动管理器标识数据库为可用数据源。该数据源可以对系统所有用户可用（系统数据源），或仅对当前用户可用（用户数据源）。在 Windows 上，你可以使用 CCA 向驱动管理器注册数据源，如图 14–5 所示。通过 CCA 配置的数据库默认会被选为 ODBC 数据源，除非你明确取消勾选。对于 Windows 平台，这通过使用相应的 ODBC 管理工具或手动配置驱动管理器来实现。

## 开发考虑

对于 ODBC 应用程序开发，你需要获取 ODBC 软件开发工具包。

绑定 CLI 以及使用 `db2cli.ini` 或 CCA 配置 CLI 的步骤同样适用于 DB2 数据源的 ODBC 应用程序。这些步骤的执行方式与 CLI 应用程序相同。

# 支持 Java 编程

DB2 支持多种类型的 Java 程序。Applet（小程序）和应用程序（applications）是 Java 程序的两种主要类型。在解释如何为 DB2 编写 applet 和应用程序之前，让我们先检查这两种类型。

Java 应用程序依赖 DB2 客户端代码连接到 DB2 数据库。我们像启动其他应用程序一样，从桌面或命令行启动应用程序。DB2 JDBC 驱动程序处理应用程序中的 JDBC API 调用。这些对 DB2 JDBC 驱动程序的调用通过 Java 原生方法翻译为 DB2 CLI 调用。JDBC 驱动程序使用客户端上的 CLI 驱动向服务器发送请求，接收结果并将其传递给 Java 应用程序。因此，在应用程序执行的地方至少需要安装 DB2 运行时客户端代码。

![](img/06451013a7a38ae7d0597faa16c37ebb_738_0.png)

图 14–6 用于 DB2 的 Java 应用程序

Java applet 不需要在此其执行的系统上安装任何 DB2 客户端代码。你只需要在客户端机器上有一个支持 Java 的 Web 浏览器来运行你的 applet。通常，你会将 applet 嵌入超文本标记语言（HTML）页面中。当你加载 HTML 页面时，浏览器会将 Java applet 下载到你的机器，然后下载 Java 类文件和 DB2 的 JDBC 驱动程序。当你的 applet 调用 JDBC API 连接到 DB2 时，JDBC 驱动程序与位于 Web 服务器上的 DB2 JDBC 服务器建立单独的网络连接。JDBC 服务器通过 DB2 CLI 驱动程序与数据库通信，并通过单独连接将结果传回给客户端。

# 第 14 章开发考虑

![](img/06451013a7a38ae7d0597faa16c37ebb_739_0.png)

图 14–7 用于 DB2 的 Java applet

DB2 还支持在 Java 中使用自定义函数和存储过程。访问 DB2 数据库的 Java 程序可以使用 JDBC 或 SQLJ 接口来实现。JDBC API 允许你编写 Java 程序，对数据库执行动态 SQL 调用。SQLJ 扩展了 JDBC 以支持嵌入式 SQL。接几节将讨论如何使用 JDBC 和 SQLJ 为 DB2 编写 Java 程序。

# JDBC 编程

如果 DB2 应用程序或 applet 使用 JDBC，你需要熟悉 JDBC 规范并理解如何调用 JDBC API 来访问数据库并操作该数据库中的数据。在这里，我们介绍一些常用术语和结构，帮助你更好地理解用于 DB2 的 JDBC 程序。

# DB2 的 JDBC 驱动程序

DB2 JDBC 驱动程序在安装 DB2 客户端或服务器代码时安装。DB2 提供了一个应用驱动程序：`COM.ibm.db2.jdbc.app.DB2Driver`。对于在安装了 DB2（客户端或服务器）的机器上运行的应用程序，你会使用此驱动程序。DB2 还带有一个网络驱动程序：

```
COM.ibm.db2.jdbc.net.DB2Driver
```
当你的 Java 程序在没有安装 DB2 的机器上运行 applet 时，可以使用此驱动程序。驱动程序的类文件封装在 `db2java.zip` 中。

JDBC 类位于 `java.sql` 包中。

# SQLJ 编程

SQLJ 源文件包含嵌入静态 SQL 语句。尽管我们在上一节中涵盖了静态嵌入 SQL，但本节中将单独讨论 Java 嵌入式 SQL (SQLJ)。这是因为 Java 与 C 等传统宿主语言有所不同，而且因为 SQLJ 使用 JDBC 作为连接数据库和处理 SQL 错误等任务的基础。

SQLJ 程序使用 JDBC 作为与 DB2 通的运行时接口；然而，任何静态 SQL 语句在执行程序之前都需要数据库中存在应用程序包。SQLJ 程序与 DB2 之间的交互如图 14–8 所示。

![](img/06451013a7a38ae7d0597faa16c37ebb_740_0.png)

**图 14–8** SQLJ 与 DB2 的接口

由于 SQLJ 应用程序和 applet 通过 DB2 的 JDBC 支持访问数据库，它们需要 JDBC 类（`java.sql.*`）以及包含 `db2java.zip` 中的 DB2 JDBC 驱动程序类。替换 SQLJ 程序中嵌入 SQL 语句的 SQLJ 翻译器使用 `sqlj.zip` 中的类（位于 `sqllib/java` 目录）。然而，执行程序不需要 `sqlj.zip` 中的接口和类。要执行 SQLJ 程序，需要 SQLJ 运行时类（`sqllib/java/runtime.zip`）来验证身份并执行在预编译和绑定阶段绑定到数据库的任何 SQL 包。

# 存储过程构建器

DB2 附有一个存储过程构建器 (SPB)，这是一种辅助快速开发存储过程的图形应用程序。SPB 提供了一个单一开发环境，支持从工作站到 System/390 的整个 DB2 家族。

SPB 带有设计助手，引导你通过基本设计模式，帮助你创建 SQL 查询，并估计调用存储过程的性能成本。用 SPB 创建的存储过程是用 Java 实现的，所有的数据库连接都使用 Java 数据库连接 (JDBC) 进行管理。可以使用 JDBC、SQLJ 或 SQL 存储过程语言指定 SQL 语句。一旦你使用 SPB 开发了基本的 SQL 结构，如果你有非常复杂的存储过程逻辑，可以使用你的编辑器来修改该存储过程。

> **注意：** DB2 SPB 协助你创建存储过程的部分是。

# 存储过程构建器

![](img/06451013a7a38ae7d0597faa16c37ebb_742_0.png)

图 14–6 用于 DB2 的 Java 应用程序

注意：在 Windows 环境下，作为微软对象链接与嵌入（OLE）架构的一部分，DB2 可以作为 OLE 自动化控制程序。通过这种机制，DB2 可以作为外部 UDF（用户定义函数）调用 OLE 自动化对象的方法。

外部 UDF 在编写并生成为动态可加载库和类后，必须在数据库中注册。图 15–1 所示的 `congrat` 函数使用 `CREATE FUNCTION` 语句进行注册。

```
CREATE FUNCTION congrat(VARCHAR(30),VARCHAR(40))
  RETURNS CLOB(1K)
  EXTERNAL NAME 'congrat.a!congrat'
  LANGUAGE C
  PARAMETER STYLE DB2SQL
  DETERMINISTIC
  FENCED
  NO SQL
  NO EXTERNAL ACTION
  DISALLOW PARALLEL;
```

图 15–1 注册用户定义函数

源 UDF 的注册方式相同，只需指定父源函数即可。此示例允许我们为 `SCORE` 数据类型创建一个 `AVG` 函数：

```
CREATE FUNCTION AVG(SCORE)
  RETURNS SCORE
  SOURCE SYSIBM.AVG(DECIMAL);
```

这些 `CREATE FUNCTION` 语句会在 `SYSCAT.FUNCTIONS` 视图中为每个 UDF 放置一个条目。你可以在控制中心中查看注册到数据库的 UDF。

## 第 15 章 SQL 开发

使用 DB2，你还可以创建第三种类型的用户定义函数，称为表函数（table function）。表函数是一种向调用它的 SQL 语句返回表的 UDF。这意味着表函数只能在 `SELECT` 语句的 `FROM` 子句中引用。表函数提供了在 SQL 查询中包含外部数据的方法。表函数可以读取非 DB2 数据（例如操作系统文件或网络上的数据），将其表格化并以关系表的形式返回给 DB2，随后可以像任何其他关系表一样处理它。例如，后续示例中的 `appform` 表函数获取候选申请表，对其进行处理，并以适当的格式返回数据以插入 `CANDIDATE` 表中（候选人 ID 除外，它是自动生成的）：

```
CREATE FUNCTION appform(VARCHAR(30))
RETURNS TABLE (LNAME VARCHAR(30), FNAME VARCHAR(30),
INITIAL CHAR(1), HPHONE,
WPHONE, STREETNAME VARCHAR(8),
STREETNAME VARCHAR(20),
CITY VARCHAR(20),
PROV_STATE VARCHAR(30),
CODE CHAR(6), COUNTRY VARCHAR(20))
EXTERNAL NAME C '\udbf!appform'
LANGUAGE STYLE DB2SQL
NO SQL
DETERMINISTIC
NO EXTERNAL ACTION
FINAL CALL
DISALLOW PARALLEL
CARDINALITY 20;
```

图 15-2 用户定义表函数 - appform

如果我们想根据候选人的申请表插入新候选人，可以使用以下 `SELECT` 语句：

```
INSERT INTO CANDIDATE
SELECT SUBSTR(GENERATE_UNIQUE(),),1,9) AS CID,
LNAME, FNAME, INITIAL,
HPHONE, WPHONE,
STREETNO, STREETNAME, CITY,
PROV_STATE, CODE, COUNTRY
FROM appform('D:\DOCS\NEWFORM.TXT');
```

### 用户定义函数

**注意：** DB2 还提供了表函数用于从 OLE DB 提供程序访问数据。这允许你从各种关系和非关系数据数据源（包括 Oracle、Microsoft SQL Server 和 Microsoft Access）将数据整合到你的 DB2 数据库或应用程序中。

用户定义函数类似于 DB2 中的其他数据库对象，这意味着每个 UDF 都有一个关联的架构名称。理想情况下，调用每个 UDF 时应使用全限定。然而，这可能非常困难并限制 SQL 查询的灵活性。另一种方法是使用特殊寄存器 `CURRENT FUNCTION`，DB2 使用此路径来解析未限定的函数引用。在这种情况下，路径不是目录列表，而是名为 "SYSBM"SYFSUN" 或 "DB2CERT" 的架构名称列表。`SYFSUN` 是内置 UDF 使用的架构。请注意，创建 UDF 的权限与创建存储过程所需的权限相同。

有关各种类型的 UDF 以及 `CREATE FUNCTION` 语句中使用的参数的更多信息，请参阅《DB2 UDB V7.1 应用程序开发指南》。

## SQL 体标量函数

之前的示例提到了用户定义函数和表函数，这些函数使用 C、C++ 或 Java 等编程语言来创建与函数相关的逻辑。创建这些函数的另一种方法是通过使用 SQL 语句。

```
CREATE FUNCTION BONUS(salary int, bonus_percent int)
RETURNS INT
LANGUAGE SQL CONTAINS SQL
RETURN
  (salary * bonus_percent / 100
);
```

**图 15-3** 用户定义函数 - BONUS

`CREATE FUNCTION` 语句允许使用单个 SQL 语句计算返回的值。`BONUS` 函数接收工资值并根据百分比计算奖金。该函数现在可以用于任何 SQL 语句来为员工计算奖金：

```
VALUES bonus(30000,10);
1
----------
3000
```

**图 15–4** 使用 BONUS 函数

该函数可以在任何可以使用普通函数的 SQL 语句位置地方使用。图 15–5 展示了如何使用 `BONUS` 函数。

```
UPDATE EMPLOYEE
SET BONUS = BONUS(SALARY, 10);
```

**图 15-5** BONUS 函数的高级用法

函数体只能包含一个 SQL 语句。然而，图 15–6 中的 SQL 经过修改可以根据工资返回不同的值。

```sql
CREATE FUNCTION BONUS(salary int, bonus_percent int)
RETURNS INT
LANGUAGE SQL CONTAINS SQL
RETURN
  CASE
    WHEN salary < 20000 THEN (salary * bonus_percent / 100)
    WHEN salary < 50000 THEN (salary * bonus_percent / 200)
    ELSE 0
  END;
```

**图 15–6** 带逻辑的 BONUS 函数

以下 SQL 显示了结果：

```sql
VALUES bonus(10000,10);
1
----------
100
VALUES bonus(30000,10);
1
----------
150
VALUES bonus(60000,10);
1
----------
0
```

## SQL 体表函数

用户定义函数也可以使用单个 SQL 语句编写。这提供了 `salary < 20000 THEN (salary * bonus_percent / 100)` 的逻辑能力。表函数只能访问数据库表。图 15–7 中的示例创建一个返回 `TEST_TAKEN` 表信息的表 UDF。

```sql
CREATE FUNCTION GET_MARKS(
```
