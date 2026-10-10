
| 工具 | 描述 |
| :--- | :--- |
| InfoSphere Data Architect | 参见电子书 *《InfoSphere Data Architect 入门》*。 |
| Rational Software Architect (RSA) | RSA 是一款基于 Eclipse 的工具，旨在支持软件工程，帮助你开发 UML 图。 |
| Rational Application Developer (RAD) | RAD 是一款面向软件开发人员的基于 Eclipse 的快速应用开发工具。 |
| Visual Studio | Microsoft® Visual Studio 是一款 IDE，允许你使用 Microsoft 技术在 Windows® 平台上开发应用程序。 |
| Aptana Studio | 这是一款用于开发 PHP 应用程序的免费 IDE。 |

表 1.1 - 可用于使用 DB2 软件开发应用程序的工具

在图 1.1 的右侧，展示了一个包含一个数据库的 DB2 服务器。在该数据库中，存储有存储过程、用户定义函数和触发器。我们将在接下来的章节中详细描述所有这些对象。

值得一提的是，IBM 在 Amazon 云上以及 IBM 开发和测试云上提供 DB2。如果你或你的公司没有预算购买用于开发或生产需求的服务器，云是一个完美的替代方案，因为它允许你按分钟“租用”计算能力。关于 DB2 云服务的详细信息将在后续章节中讨论。

## 1.2 服务器端开发

DB2 软件中的服务器端开发意味着应用程序对象在 DB2 数据库上进行开发和存储。本节将简要讨论以下应用程序对象：

- 存储过程
- 用户定义函数 (UDF)
- 触发器

### 1.2.1 存储过程

存储过程是一种可以封装 SQL 语句和业务逻辑的数据库应用程序对象。将部分应用逻辑保留在数据库中可以提高性能，因为这减少了应用程序与数据库之间的网络流量。此外，存储过程提供了一个集中位置来存储代码，以便其他应用程序可以重用相同的存储过程。要调用存储过程，请使用 CALL 语句。在 DB2 中，你可以使用多种语言开发存储过程，包括 SQL PL、PL/SQL、Java、C/C++、CLR、OLE 和 COBOL。以下示例展示了如何从 DB2 命令窗口或 Linux® shell 创建和调用 SQL PL 存储过程：

```
db2 create procedure P1 begin end
db2 call P1
```

在示例中，过程 P1 是一个空的存储过程，它什么都不做。该示例说明了创建存储过程有多么简单。要开发逻辑更复杂的存储过程，我们建议你使用包含调试器的 IBM Data Studio。

### 1.2.2 用户定义函数

用户定义函数 (UDF) 是一种允许用户使用自己的逻辑扩展 SQL 语言的数据库应用程序对象。函数通常作为包含在函数中的业务逻辑的结果，总是返回一个或多个值。要调用函数，请将其用在 SQL 语句中，或者使用 values 函数。在 DB2 中，你可以使用多种语言开发 UDF，包括 SQL PL、PL/SQL、Java、C/C++、OLE DB、CLR。

这个简单的示例展示了如何从 DB2 命令窗口或 Linux shell 创建和调用 SQL PL UDF：

```
db2 create function F1() returns integer begin return 1000; end
db2 values F1
```

在示例中，函数 F1 是一个返回整数值 1000 的函数。VALUES 语句可用于调用该函数。与存储过程一样，我们建议你使用 IBM Data Studio 创建函数。

### 1.2.3 触发器

触发器是一种在表或视图上自动执行操作的对象。在定义触发器的对象上发生的触发动作会导致触发器被触发。触发器通常不被视为应用程序对象；因此，数据库开发人员通常不编写触发器，但数据库管理员会。由于需要一些编码，我们将触发器包含在本节中。以下是一个触发器的示例：

```
create trigger myvalidate no cascade before insert on T1
  referencing NEW as N
  for each row
    begin atomic
      set (N.myxmlcol) = XMLVALIDATE(N.myxmlcol
    according to xmlschema id myxmlschema);
    end
```

在这个示例中，触发器在表 T1 的 INSERT 操作之前触发。触发器将插入该值（这是一个 XML 文档），但会调用 XMLVALIDATE 函数使用给定的架构验证此 XML 文档。*第 15 章 DB2 pureXML* 更详细地介绍了 XML 和 XML 架构。

## 1.3 客户端开发

顾名思义，在客户端开发中，应用程序开发人员在其客户端上编写程序，然后使用随 DB2 提供的应用程序编程接口 (API) 连接并访问 DB2 数据库。在本节中，我们讨论：

- 嵌入式 SQL
- 静态 SQL 与动态 SQL
- CLI 和 ODBC
- JDBC、SQLJ 和 pureQuery
- OLE DB
- ADO.NET
- PHP
- Ruby on Rails
- Perl
- Python

### 1.3.1 嵌入式 SQL

***嵌入式 SQL 应用程序*** 是指将 SQL 嵌入到宿主语言（如 *C*、*C++* 或 COBOL）中的应用。嵌入式 SQL 应用程序可以包含下一节中描述的静态 SQL 或动态 SQL。*图 1.2* 展示了嵌入式 SQL 应用程序的构建方式。

![](img/5f6ba170efa3a607142589708531bef8_27_0.png)

在图中，C 程序 `hello.sqc` 包含嵌入式 SQL。C 语言的嵌入式 SQL API 使用 **EXEC SQL**（在 *图 1.2* 中高亮显示）以便预编译过程区分嵌入式 SQL 语句和实际的 C 代码。你或许还注意到，在 `hello.sqc` 列表中，一些变量以冒号作为前缀，例如 `:dbname`、`:userID` 和 `:psw`。这些被称为宿主变量。宿主变量是从宿主语言中引用的、在嵌入式 SQL 语句中使用的变量。

使用带有 **bindfile** 选项发出 **precompile** 命令（也称为 **prep** 命令）会生成两个文件，包含仅 SQL 语句的 `hello.bnd` 绑定文件和包含仅 C 代码的 `hello.c` 文件。绑定文件将使用 **bind** 命令进行编译，以获取存储在数据库中的 **package**（包）。包包括编译/可执行的 SQL 以及 DB2 用于检索数据的访问路径。要发出 **bind** 命令，必须存在与数据库的连接。在图的底部，`hello.c` 文件像任何常规 C 程序一样被编译和链接。生成的可执行文件 `hello.exe` 必须与存储在数据库中的包匹配才能成功执行。

### 1.3.2 静态 SQL 与动态 SQL

静态 SQL 语句是指在预编译时 SQL 结构完全已知的语句。例如：

```
SELECT lastname, salary FROM employee
```

在这个示例中，语句中引用的列名（*lastname*、*salary*）和表名（*employee*）在预编译时是完全已知的。以下示例也是一个静态 SQL 语句：

```
SELECT *lastname*, *salary* FROM *employee* WHERE *firstnm* = :fname
```

在第二个示例中，宿主变量 *:fname* 被用作嵌入式 SQL 语句的一部分。虽然宿主变量的值在运行时之前未知，但其数据类型是从程序中已知的，并且所有其他对象（列名、表名）都是提前完全已知的。DB2 软件使用这些宿主变量的估计值来提前计算访问路径；因此，这种情况仍被视为静态 SQL。

你在运行应用程序之前预编译、绑定并编译静态执行的 SQL 语句。静态 SQL 最适合用于统计数据变化不大的数据库。现在让我们再看一个示例：

```
SELECT *?, *?* FROM *?*
```

在这个示例中，语句引用的列和表的名称直到运行时才可知。因此，访问计划仅在运行时计算，并使用当时可用的统计数据。这类语句被视为 *动态* SQL 语句。

某些编程 API，如 JDBC 和 ODBC，无论 SQL 语句是否包含已知对象，始终使用动态 SQL。例如，语句 *SELECT* *lastname*, *salary* FROM *employee* 的所有列和表名都是提前已知的，但通过 JDBC 或 ODBC，你不预编译语句。所有语句的访问计划都在运行时计算。

通常，使用两个语句将 SQL 语句视为动态：

- **PREPARE**：该语句准备或编译 SQL 语句，计算用于检索数据的访问计划
- **EXECUTE**：该语句执行 SQL

或者，你可以在单个语句中执行 **PREPARE** 和 **EXECUTE**：**EXECUTE IMMEDIATELY**

*清单 1.1* 展示了一个嵌入式 C 动态 SQL 语句的示例，该语句被准备并执行。

```
strcpy (hvStmtDyn, "SELECT *name* FROM emp WHERE dept = *?*" );
PREPARE Stmt tDyn FROM :hvStmtDyn;
EXECUTE StmtDyn USING 1;
EXECUTE StmtDyn USING 2;
```

*清单 1.1* - 使用 **PREPARE** 和 **EXECUTE** 的嵌入式 C 动态 SQL 语句

*清单 1.2* 展示了与 *清单 1.1* 相同的示例，但使用了 **EXECUTE IMMEDIATELY** 语句

