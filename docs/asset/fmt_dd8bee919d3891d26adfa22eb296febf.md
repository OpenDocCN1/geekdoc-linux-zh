
# DB2 Command Window #1 示例

DB2 Command Window #1 代表一个打开游标或结果集（`select * from staff`）并获取 35 条记录的应用程序。在同一个事务中（因为在这个窗口中我们没有发布任何 commit 语句），应用程序打开了相同的游标，并看到了 35 条记录，即使 DB2 Command Window #2 中的应用程序插入（但未提交）了一条新记录。

## 第 13 章 – 并发与锁定

接下来，DB2 Command Window #2 应用程序执行了插入的提交，因此当 DB2 Command Window #1 应用程序第三次打开游标时，结果集多返回了一行（幻读），获取了 36 条记录。这个例子说明了幻读问题：在同一个事务中，同一个游标返回了更多行。我们正在使用 `CS` 隔离级别，正如本章前面提到的，`CS` 不防止幻读。

- 在尝试后续步骤之前，清理之前插入的记录：

从 DB2 Command Window #1 执行：

```
db rollback
```

从 DB2 Command Window #2 执行：

```
db delete from staff where id = 400
db select * from staff
```

这再次返回了 35 条记录。

- 从 DB2 Command Window #2 执行：

```
db connect to sample
db +c insert into staff (id,name) values (400, 'test')
```

该语句将如预期地挂起。

由于在 DB2 Command Window #1 的 `SELECT` 语句中了 `With RR` 子句，此隔离级别防止了会更改结果集的插入操作。这个例子说明了 `RR` 隔离级别可以防止幻读问题。

- 在继续练习的第 2 部分之前进行清理：

从 DB2 Command Window #2 执行：

```
Ctrl-C（中断）
```

从 DB2 Command Window #1 执行：

```
db rollback
```

## 第 2 部分：测试幻读问题和 RR 隔离级别

步骤：

1. 将当前已提交设置为开启：

打开一个 DB2 命令行窗口并执行：

```
db2 update db cfg for sample using CUR_COMMIT on
db2 force applications
```

关闭窗口。

2. 像第 1 部分一样打开两个 DB2 命令行窗口，让一个在另一个上面。然后执行以下：

从 DB2 Command Window #1：

```sql
db2 connect to sample
db2 +c select from staff
```

从 DB2 Command Window #2：

```sql
db2 connect to sample
db2 +c select * from staff
```

3. 打开两个 DB2 命令行窗口，执行以下操作：

从 DB2 Command Window #1（写入者）：

```sql
db2 connect to sample
db2 +c update staff set name = 'Chong' where id = 10
```

从 DB2 Command Window #2（读者）：

```sql
db2 connect to sample
db2 +c select * from staff
```

此 `SELECT` 语句将等待 DB2 Command Window #1 应用程序释放排斥锁（X）。如你所示，`CS` 的默认行为允许的并发性较低。

- 窗口 1：

```
db rollback
```

- DB2 Command Window #2：

```
db rollback
```

# 第三部分 – 学习 DB2：应用程序开发

## 第 14 章 – DB2 应用开发简介

IBM DB2 是一款强大的数据服务器软件，用于管理关系型和 XML 数据。它不仅为数据库管理员提供了灵活性，也为数据库开发者提供了便利。无论你使用哪种语言开发程序，DB2 都能提供所需的驱动程序、适配器和扩展，让你作为应用程序的一部分与数据库进行交互。此外，通过 DB2 Express-C，你可以免费开发应用程序，且没有数据库大小限制，并具有与 DB2 其他版本相同级别的编程语言支持。使用 DB2 Express-C 开发的程序可以在不对应用程序进行任何修改的情况下运行在任何 DB2 版本上。

> **注意：**
>
> 本节仅是对 DB2 应用开发的介绍。作为“DB2 校园系列”的一部分，正在开发一系列 25 多种免费在线书籍，其中包含一本专门针对 DB2 应用开发的书籍。该系列的其他书籍还包括非 DB2 技术，如 Java、PHP、Ruby on Rails、Python、Perl、Web 2.0、SOA、Eclipse、开源开发、云计算等！其他书籍将更详细地介绍 IBM 的 pureQuery、Data Studio 和 InfoSphere Data Architect。这些书籍将从 2009 年 10 月开始介绍。

### 14.1 DB2 应用开发：概览

DB2 为数据库开发者提供了灵活性，可以利用存储过程和用户定义函数等服务器端开发功能；而应用程序开发者可以使用他们选择的编程语言开发客户端应用程序。这种灵活性在图 14.1 所示。

**图 14.1** DB2 适用于所有人：数据库和应用程序开发者

| 客户端 | DB2 服务器 |
| :--- | :--- |
| 开发工具 | 数据库 |
| IBM Data Studio, IDA, RSA, RAD, Visual Studio, ZenCore | 存储过程 用户定义函数 |
| 编程应用程序接口 (API) | 触发器 |
| C++, Cobol, FORTRAN 中的嵌入静态与动态 SQL, ODBC, JDBC/SQL, ADO, ADO.NET, OLE DB, PHP 等 | 操作系统 |
| IBM 数据服务器客户端 / 驱动程序 | 操作系统 |
| 操作系统 | |

在图 14.1 中，左侧代表客户端机器，应用程序程序员在上面开发并运行其程序。在该客户端机器上，除了操作系统之外，根据开发的应用程序类型，可能会安装 IBM 数据服务器。IBM 数据服务器包含了所需的连接驱动程序，例如 JDBC 驱动程序和 ODBC/CLI 驱动程序。这些驱动可以通过访问 IBM DB2 Express-C 网站 `http://ibm.com/db2/express` 下载。

使用 IBM Data Studio、InfoSphere Data Architect (IDA)、Rational Software Architect (RSA)、Rational Application Developer (RAD) 等编程工具，你可以用所需的编程语言开发应用程序。支持这些语言的 API 库也包含在 IBM 数据服务器客户端中，因此当你连接到 DB2 服务器时，所有指令都会通过这些 API 适当翻译为 DB2 可理解的 SQL 或 XQuery 语句。表 14.1 提供了上述工具的简要描述。

| 工具名称 | 说明 |
| :--- | :--- |
| IBM Data Studio | IBM Data Studio 是一个基于 Eclipse 的工具，允许用户管理数据并开发存储过程、函数和数据 Web 服务。书中之前介绍过 IBM Data Studio。 |
| InfoSphere Data Architect (IDA) | IDA 是一个用于数据建模的工具。它可以帮助你构建数据库的逻辑设计和物理设计。 |
| Rational Software Architect (RSA) | RSA 是一个基于 Eclipse 的软件工程工具，帮助你开发 UML 图。 |
| Rational Application Developer (RAD) | RAD 是一个用于软件开发者的基于 Eclipse 的快速应用程序开发工具。 |
| Visual Studio | Microsoft Visual Studio 是一个 IDE，允许你在 Windows 平台上使用 Microsoft 技术开发应用程序。 |
| ZendCore | 以前称为 ZendCore for IBM，这是一个用于开发 PHP 应用程序的免费 IDE。 |

**表 14.1 - 帮助你用 DB2 开发应用程序的工具**

图 14.1 的右侧展示了包含一个数据库的 DB2 服务器。该数据库内部有存储过程、用户定义函数和触发器。我们将在接下来的章节中更详细地描述所有这些对象。

## 14.2 服务器端开发

DB2 中的服务器端开发意味着应用程序对象是在 DB2 数据库上开发和存储的。本节将简要讨论以下应用程序对象：

- 存储过程
- 用户定义函数 (UDFs)
- 触发器

### 14.2.1 存储过程

存储过程是一种数据库应用程序对象，可以封装 SQL 语句和业务逻辑。将部分应用程序逻辑保留在数据库中可以提高性能，因为减少了应用程序与数据库之间的网络流量。此外，存储过程为存储代码提供了一个集中位置，因此其他应用程序可以重用相同的存储过程。要调用存储过程，使用 `CALL` 语句。在 DB2 中，你可以使用多种语言开发存储过程，包括 SQL、Java、C++、CLR、OLE 和 COBOL。下面是一个如何从 DB2 命令行窗口或 Linux 终端创建并调用 SQL PL 存储过程的简单示例：

```
db2 create procedure P1 begin end
db2 call P1
```

在示例中，过程 `P1` 是一个空存储过程，没有执行任何操作。该示例展示了创建存储过程是多么简单。要开发具有复杂逻辑的存储过程，我们建议你使用包含调试器的 IBM Data Studio。

### 14.2.2 用户定义函数

用户定义函数 (UDF) 是一种允许用户通过其逻辑扩展 SQL 的数据库应用程序对象。

> **注意：** 原文此处内容与 14.2.1 重复，疑为排版错误，此处保留原文结构但去除重复示例代码块。

### 14.2.3 触发器

触发器是一种在表或视图上自动执行操作的对象。触发器在定义对象时会触发。触发器通常不被视为应用程序对象；但数据库管理员会编写。由于需要代码，我们在本节中包含了触发器。

```sql
create trigger validate no cascade before insert on T1
referencing NEW as N
for each row
begin atomic
set (N.xmlcol) = XMLVALIDATE(N.xmlcol according to xmlschema idchema);
end
```

在此示例中，触发器在表 `T1` 上执行 `INSERT` 操作之前触发。触发器将插入值（这是一个 XML 文档），但将调用 `XMLVALIDATE` 函数来验证该 XML 文档。第 15 章 pureXML 将更多讨论 XML 和 Schema。

## 14.3 客户端开发

顾名思义，在客户端开发中，应用程序开发者在客户端编写程序，然后使用 DB2 提供的应用程序接口 (API) 连接并访问 DB2 数据库。在本节中我们将介绍：

- 嵌入 SQL
- 静态 SQL 与动态 SQL
- CLI 和 ODBC
- JDBC、SQLJ 和 pureQuery
- OLE DB
- ADO.NET
- PHP
- Ruby on Rails
- Perl
- Python

### 14.3.1 嵌入 SQL

嵌入 SQL 应用程序是将 SQL 嵌入到主机语言（如 C、C++、COBOL）中的应用程序。嵌入 SQL 应用程序可以包含后续章节描述静态或动态 SQL。图 14.2 显示了如何构建嵌入 SQL 应用程序。

**图 14.2** 构建嵌入 SQL 应用程序

| 文件 | 说明 | 过程 |
| :--- | :--- | :--- |
| hello.sqc | 含有 SQL 和 C 代码 | 预编译 |
| hello.c | 只有代码无嵌入 SQL | 编译 |
| hello.bnd | 只有 SQL | 绑定 |
| hello.exe | 需要正确的包才能成功运行 | 可执行文件 |

```c
// hello.sqc
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char *argv[]) {
 EXEC SQL BEGIN DECLARE SECTION;
 char dbname[15];
 char userid[8];
 EXEC SQL END DECLARE SECTION;
 // 连接到数据库
 EXEC SQL CONNECT TO :dbname USER :userid
 USING :psw;
 if (sqlcode != 0) {
 printf("%n *** Error ***\n", sqlcode);
 }
}
```

在图中，C 语言程序 `hello.sqc` 包含了嵌入 SQL。C 语言的嵌入 SQL API 使用 `EXEC SQL`（如图 14.2 所示）来允许预编译过程区分嵌入 SQL 语句与实际的 C 代码。你可能还会在 `hello.sqc` 的列举中注意到某些变量以冒号为前缀，例如 `:dbname`、`:userid` 和 `:psw`。这些被称为主机变量。主机变量来自宿主语言，在嵌入 SQL 语句中被引用。

带有 `bind` 选项的预编译命令（也称为 `prep` 命令）会生成两个文件：仅包含 SQL 语句的 `hello.bnd` 文件和仅包含 C 代码的 `hello.c` 文件。将使用 `bind` 命令编译 bind 文件，以获取存储在数据库中的包。包包含了编译后的/可执行的 SQL 以及 DB2 检索数据时遵循的访问路径。要使用 bind 连接，数据库必须存在。在图底部，`hello.c` 像任何普通 C 程序一样被编译和链接。生成的可执行文件 `hello.exe` 必须与存储在数据库中的包匹配才能成功执行。

### 14.3.2 静态 SQL 与动态 SQL

静态 SQL 语句是指在预编译时就能完全确定 SQL 结构的语句。例如：

```sql
SELECT lastname, salary FROM employee
```

在这个示例中，语句中引用的列名（`lastname`、`salary`）和表名（`employee`）在预编译时是完全已知的。以下示例也是静态 SQL 语句：

```sql
SELECT lastname, salary FROM employee WHERE firstname = :fname
```

在这个示例中，主机变量 `:fname` 作为嵌入 SQL 语句的一部分。虽然主机变量的值在运行时未知，但它的数据类型来自程序，且所有其他对象（列名、表名）在提前都是完全已知的。DB2 对这些主机变量进行估计以提前计算访问计划；这仍然被视为静态 SQL。

在运行应用程序之前，你会对静态执行的 SQL 语句进行预编译、绑定和编译。静态 SQL 用于统计信息变化不大的数据库。现在让我们来看一个动态 SQL 的例子：

```sql
SELECT ?, ? FROM ?
```

在这个示例中，语句引用的列名和表名直到运行时才未知。因此，访问计划仅在运行时根据当时的可用统计信息进行计算。这类语句被视为动态 SQL 语句。

某些编程 API（使用 JDBC 和 ODBC）无论 SQL 语句是否包含已知对象，始终使用动态 SQL。例如，`SELECT lastname, salary FROM employee` 语句的所有列名和表名都是提前已知的，通过 JDBC 或 ODBC，你不需要预编译这些语句。语句的所有访问计划都在运行时计算。

通常，使用两条语句将 SQL 语句视为动态的：

- `PREPARE`：该语句准备或编译 SQL 语句，以计算检索数据的访问计划
- `EXECUTE`：该语句执行 SQL

或者，你也可以在一个语句中执行 `PREPARE` 和 `EXECUTE`：`EXECUTE IMMEDIATE`。

列表 14.1 显示了一个被准备并执行的嵌入 C 动态语句的示例。

```c
strcpy(hvStmtDyn, "SELECT name FROM EMP WHERE dept = ?");
PREPARE StmtDyn FROM :hvStmtDyn;
EXECUTE StmtDyn USING 1;
EXECUTE StmtDyn USING 2;
```

**列表 14.1 - 使用 PREPARE 和 EXECUTE 的嵌入 C 动态语句**

列表 14.2 显示与列表 14.1 相同的示例，但使用了 `EXECUTE IMMEDIATE` 语句。

```sql
EXECUTE IMMEDIATE 'SELECT name FROM EMP where dept = 1';
EXECUTE IMMEDIATE 'SELECT name FROM EMP where dept = 2';
```

**列表 14.2 - 使用 EXECUTE IMMEDIATE 的嵌入 C 动态语句**
