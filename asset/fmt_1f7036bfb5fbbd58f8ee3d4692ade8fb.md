
`-url jdbc:db2://localhost:50000/sample` 是连接数据库所需的 URL

`-user rfchong` 是连接数据库的用户 ID

`-password mypasswd` 是连接数据库的密码

`myprg3_SJProfile0.ser` 是要定制以在数据库中创建包的文件名

输出看起来如下 *列表 4.26* 所示。

```
[jcc][sqlj]
[jcc][sqlj]  Begin Customization
[jcc][sqlj]  Loading profile: myprg3_SJProfile0
[jcc][sqlj]  Customization complete for profile myprg3_SJProfile0.ser
[jcc][sqlj]  Begin Bind
[jcc][sqlj]  Loading profile: myprg3_SJProfile0
[jcc][sqlj]  Driver defaults(user may override):  BLOCKING ALL
VALIDATE BIND STATIC READ_ONLY YES
[jcc][sqlj]  Fixed driver options: DATETIME ISO DYNAMICRULES BIND
[jcc][sqlj]  Binding package MYPRG301 at isolation level UR
[jcc][sqlj]  Binding package MYPRG302 at isolation level CS
[jcc][sqlj]  Binding package MYPRG303 at isolation level RS
[jcc][sqlj]  Binding package MYPRG304 at isolation level RR
[jcc][sqlj]  Bind complete for myprg3_SJProfile0
```

**列表 4.26 - 运行 DB2 定制器的输出**

不会创建任何输出文件，但带有嵌入式 SQL 语句和访问计划的包将存储在数据库中。

(3) 运行程序。之前创建的包将在运行时使用。

```
D:\>java myprg3 <userid> <password>
Successful connection to the database!
Successful retrieval of record. Column 'IBMREQD' has a value of 'Y'
Successful Disconnection from database
End of Program
```

下方的图 4.12 显示了准备程序 `myprg3.sqlj` 的所有输出。

![](img/5f6ba170efa3a607142589708531bef8_158_0.png)

图 4.12 - 准备 SQLJ 程序 `myprg3.sqlj`

## 4.5 pureQuery

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
>
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

程序 `mylab4.java`（解决方案）包含在随附本书的 `Exercise_Files_DB2_Application_Development.zip` 文件中。

- 2. 在随附本书的 `Exercise_Files_DB2_Application_Development.zip` 文件中查找 `connectionContext.sqlj` 文件。准备此 SQLJ 程序并执行它。

## 4.7 总结
