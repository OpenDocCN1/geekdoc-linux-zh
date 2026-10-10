
Natasha Tolub 设计了本书的封面。

Susan Visser 协助出版了本书。

# 第 1 章 — DB2 应用开发简介

IBM® DB2® 是一款强大的数据服务器软件，用于管理关系数据和 XML 数据。它不仅为数据库管理员提供了灵活性，也为数据库开发人员提供了灵活性。无论您使用哪种语言来开发程序，DB2 软件（"DB2"）都提供了您作为应用程序一部分处理数据库所需的驱动程序、适配器及扩展。此外，使用 DB2 Express-C，您可以零成本开发应用程序，没有数据库大小限制，并享有与其他版本 DB2 相同级别的编程语言支持。使用 DB2 Express-C 开发一次，您就可以在任何 DB2 版本上运行，而无需对应用程序进行任何修改。

在本章中，您将了解：

- 使用存储过程和用户定义函数进行的服务器端编程
- 使用不同编程语言进行的客户端编程

## 1.1 DB2 应用开发：全景图

DB2 为数据库开发人员提供了灵活性，使其能够利用服务器端开发功能，如存储过程和用户定义函数，同时，应用程序开发人员可以使用他们选择的编程语言开发客户端应用程序。这种灵活性在图 1.1 中进行了说明。

![](img/5f6ba170efa3a607142589708531bef8_23_0.png)

**图 1.1 - DB2 软件适用于每个人：数据库开发人员和应用程序开发人员**

在 *图 1.1* 中，左侧代表客户端机器，应用程序程序员在此开发并运行他的程序。在此客户端机器上，除了操作系统外，根据正在开发的应用程序类型，可能还安装了 IBM 数据服务器客户端。IBM 数据服务器客户端包含所需的连接驱动程序，如 JDBC 驱动程序和 ODBC/CLI 驱动程序。也可以访问 `http://ibm.com/db2/express` 上的 IBM DB2 Express-C 网站独立下载这些驱动程序。

使用诸如 IBM Data Studio、InfoSphere™ Data Architect (IDA)、Rational® Software Architect (RSA)、Rational Application Developer (RAD) 等编程工具，您可以使用期望的编程语言开发您的应用程序。支持这些语言的 API 库也包含在 IBM 数据服务器客户端中，因此当您连接到 DB2 服务器时，所有这些程序指令都会使用这些 API 适当地翻译为 DB2 理解的 SQL 或 XQuery 语句。*表 1.1* 提供了前述工具的简要描述。

| 工具名称 | 描述 |
| :--- | :--- |
| IBM Data Studio | IBM Data Studio 是一个免费的基于 Eclipse 的工具，允许用户管理其数据服务器并开发存储过程、函数和数据 Web 服务。欲了解更多信息，请参阅电子书 *Getting started with IBM Data Studio for DB2*。 |
| InfoSphere Data Architect (IDA) | IDA 是用于数据建模的工具。它帮助您构建数据库逻辑设计和物理设计。欲了解更多信息，请参阅 |
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

存储过程是一种可以封装 SQL 语句和业务逻辑的数据库应用程序对象。将部分应用逻辑保留在数据库中可以提高性能，因为这减少了应用程序与数据库之间的网络流量。此外，存储过程提供了一个集中位置来存储代码，以便其他应用程序可以重用相同的存储过程。要调用存储过程，请使用 `CALL` 语句。在 DB2 中，你可以使用多种语言开发存储过程，包括 SQL PL、PL/SQL、Java、C/C++、CLR、OLE 和 COBOL。以下示例展示了如何从 DB2 命令窗口或 Linux® shell 创建和调用 SQL PL 存储过程：

```
db2 create procedure P1 begin end
db2 call P1
```

在示例中，过程 `P1` 是一个空的存储过程，它什么都不做。该示例说明了创建存储过程有多么简单。要开发逻辑更复杂的存储过程，我们建议你使用包含调试器的 IBM Data Studio。

### 1.2.2 用户定义函数

用户定义函数 (UDF) 是一种允许用户使用自己的逻辑扩展 SQL 语言的数据库应用程序对象。函数通常作为包含在函数中的业务逻辑的结果，总是返回一个或多个值。要调用函数，请将其用在 SQL 语句中，或者使用 `values` 函数。在 DB2 中，你可以使用多种语言开发 UDF，包括 SQL PL、PL/SQL、Java、C/C++、OLE DB、CLR。

这个简单的示例展示了如何从 DB2 命令窗口或 Linux shell 创建和调用 SQL PL UDF：

```
db2 create function F1() returns integer begin return 1000; end
db2 values F1
```

在示例中，函数 `F1` 是一个返回整数值 1000 的函数。`VALUES` 语句可用于调用该函数。与存储过程一样，我们建议你使用 IBM Data Studio 创建函数。

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

在这个示例中，触发器在表 `T1` 的 INSERT 操作之前触发。触发器将插入该值（这是一个 XML 文档），但会调用 `XMLVALIDATE` 函数使用给定的架构验证此 XML 文档。*第 15 章 DB2 pureXML* 更详细地介绍了 XML 和 XML 架构。

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
