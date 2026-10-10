

![](img/5f6ba170efa3a607142589708531bef8_158_0.png)

图 4.12 - 准备 SQLJ 程序 myprg3.sqlj

# 4.5 pureQuery

至此，你应该对 JDBC 和 SQLJ 有了基本的了解。传统上，正如你可能注意到的那样，JDBC 和 SQLJ 编程需要一些繁琐的编程工作。这就是诸如 *Hibernate* 等**对象关系映射（ORM）框架**流行的原因之一。它们提供了一种数据访问抽象层，便于在你的面向对象的代码和关系数据库模型之间进行映射。然而，ORM 框架往往会在幕后为你生成所需的 SQL，而这些生成的 SQL 可能并非最优。此外，由于开发人员不再控制发送到数据库的 SQL，诊断性能问题和调优变得更加复杂。

为应对这些挑战，IBM 开发了 *pureQuery*。你可以将 pureQuery 视为位于 JDBC 之上的一个 API 薄层。它像 ORM 框架一样方便面向对象的代码与关系模型之间的映射；但它也赋予了你在 SQL 方面工作的灵活性。因此，pureQuery 的编程模型和工具有助于 Java 数据访问，通过生成使用最佳实践方法（如使用类似 JDBC 的批量更新）的代码来提高性能，并有助于问题定位。

除了 API 之外，pureQuery 还提供以下内容：

- 一个运行时，提供优化且安全的数据库访问
- 一个基于 Eclipse 的集成数据库开发环境，用于提高开发生产力
- 监控服务，为开发人员和 DBA 提供关于 Java 数据库应用程序性能的全新见解。

pureQuery 还允许你在不更改任何代码的情况下生成静态 SQL。这在不费吹灰之力的情况下解锁了静态 SQL 的优势。

pureQuery 的工具包含在产品 *Optim Development Studio* 中。API 和运行时随产品 Optim™ pureQuery Runtime 提供，并且作为开发用途免费打包在开发人员的机器上与 Optim Development Studio 一起使用。监控服务通过 Optim Development Studio 提供，并在更高级别上通过 IBM DB2 Performance Expert 和 Extended Insight 功能提供。

IBM Optim™ 产品组合提供了一个集成的、模块化的环境，用于在其生命周期内设计、开发、部署、操作、优化和治理企业数据。这被称为 *Optim 集成数据管理*。

> **注意：**
> 有关 pureQuery 和 Optim 集成数据管理的更多信息，可以在免费电子书 *Getting Started with pureQuery* 和 *Getting Started with IBM Data Studio for DB2* 中找到。这两本电子书都是该系列书籍的一部分。

## 4.6 练习

在这个练习中，你将练习编写小型的 JDBC 和 SQLJ 程序。

*步骤*

- 在 *Listing 4.12* 中，我们展示了一个示例，其中使用 **CallableStatement** 对象返回一个结果集。创建一个符合以下规格的 JDBC 程序：
    - 程序名称：`mylab4.java`
    - 该程序应使用以下语法执行：
        - `java mylab4 <userid> <password> <bonus>`
    - 使用 4 型驱动连接到 **SAMPLE** 数据库
    - 调用返回 2 个结果集的存储过程 "*high_bonus*"
    - 确保首先创建如下所示的 **high_bonus** 存储过程：

```sql
CREATE PROCEDURE HIGH_BONUS (IN p_bonus INT)
DYNAMIC RESULT SETS 2

-- This procedure lists the first name, last name, bonus, and
-- education level (edlevel) of the employees with a bonus amount
-- larger than the amount specified by the parameter p_bonus.
-- This information is in the EMPLOYEE table.
-- The procedure also returns another result set with the names
-- of all departments from the DEPARTMENT table.

P1: BEGIN
-- Declare cursor1
DECLARE cursor1 CURSOR WITH RETURN FOR
SELECT firstname, lastname, bonus, edlevel
FROM employee
WHERE bonus > p_bonus;

-- Declare cursor2
DECLARE cursor2 CURSOR WITH RETURN FOR
SELECT deptname
FROM department;

-- Cursor left open for client application
OPEN cursor1;
OPEN cursor2;
END P1
```

程序 *mylab4.java*（解决方案）包含在随附本书的 Exercise_Files_DB2_Application_Development.zip 文件中。

- 2. 在随附本书的 Exercise_Files_DB2_Application_Development.zip 文件中查找 *connectionContext.sqlj* 文件。准备此 SQLJ 程序并执行它。

# 4.7 总结

在本章中，你学习了使用 DB2 开发 Java 应用的基础知识。首先讨论了 JDBC，这是一种使用动态 SQL 访问数据库的标准 API。本章展示了如何连接到 DB2 数据库并发出不同类型的 JDBC 语句。然后，我们介绍了 SQLJ。虽然 SQLJ 并不那么流行，但 SQLJ 编程更紧凑，并且由于在 Java 程序中使用嵌入的静态 SQL，因此更适合性能。最后，我们简要介绍了 IBM 的 pureQuery。pureQuery 是 IBM 针对繁琐的 JDBC 编程和 ORM 框架缺乏灵活性的解决方案。

# 4.8 复习题

- 1. JDBC 和 SQLJ 之间的区别是什么？
- 2. DB2 9.7 支持哪些 JDBC 类型？
- 3. `db2jcc.jar` 和 `db2jcc4.jar` 之间的区别是什么？
- 4. 什么是迭代器？
- 5. 什么是默认上下文？
- 6. 以下哪项陈述是错误的？
    - A. `db2jcc.jar` 包含一个 JDBC 2 型驱动
    - B. `db2jcc4.jar` 包含一个 JDBC 2 型驱动
    - C. `db2jcc.jar` 包含一个 JDBC 4 型驱动
    - D. `db2jcc4.jar` 包含一个 JDBC 4 型驱动
    - E. 以上都不是
- 7. 以下哪项陈述是正确的？
    - A. pureQuery 允许开发人员轻松地在动态或静态 SQL 之间切换而无需更改代码
    - B. pureQuery 可以与 ORM 一起使用
    - C. pureQuery 包含在某些 Optim 产品中
    - D. 以上都是
    - E. 以上都不是
- 8. 以下哪项陈述是正确的？
    - A. JDBC 和 SQLJ 不能结合使用
    - B. JDBC 和 pureQuery 不能结合使用
    - C. SQLJ 和 pureQuery 不能结合使用
    - D. JDBC、SQLJ 和 pureQuery 可以结合使用
    - E. 以上都不是
- 9. 以下哪个不是有效的连接对象方法？
    - A. Statement
    - B. PreparedStatement
    - C. CallableStatement
    - D. ResultSetStatement
    - E. 以上都不是
- 10. 以下哪个不是有效的 SQLJ 概念？
    - A. 执行上下文
    - B. 连接上下文
    - C. 默认上下文
    - D. 命名迭代器
    - E. 位置迭代器

# 第 5 章 – 使用 C/C++ 进行应用开发

本章讨论了使用 C/C++ 结合 DB2 进行应用开发的各个方面，从设置开发环境到构建和运行应用程序。虽然在 *第 14 章，DB2 应用开发简介* 中已经讨论了嵌入 SQL，但我们将更详细地查看嵌入 SQL 编程如何在 C/C++ 程序中工作。本章还讨论了如何开发 ODBC 或 CLI 应用程序。在本章中，你将学习：

- 使用嵌入 SQL 编程 C/C++ 应用程序
- 构建具有嵌入 SQL 的 C/C++ 应用程序
- 使用 CLI/ODBC 编程 C/C++ 应用程序
- 构建具有 CLI/ODBC 的 C/C++ 应用程序

# 5.1 C/C++ DB2 应用程序：全局视图

当我们谈论数据库应用程序时，首先浮现在脑海中的是 SQL。SQL 是用于在关系数据库上执行数据定义语言（DDL）、数据控制语言（DCL）和数据操纵语言（DML）操作的语言。SQL 不是一种通用编程语言；由于 SQL 是一种非过程化语言，SQL 语句由数据库管理器执行，因此你不能执行用户定义的操作。这就是为什么数据库应用程序大多是通过结合 SQL 的能力与 C 或 C++ 等高级编程语言来开发的。在高级编程语言（也称为宿主语言）中开发应用程序，并将 SQL 语句嵌入该应用程序中，这被称为嵌入 SQL 编程。*图 5.1* 阐明了这一概念。嵌入 SQL 应用程序通常使用 C 或 C++ 开发。

![](img/5f6ba170efa3a607142589708531bef8_164_0.png)

