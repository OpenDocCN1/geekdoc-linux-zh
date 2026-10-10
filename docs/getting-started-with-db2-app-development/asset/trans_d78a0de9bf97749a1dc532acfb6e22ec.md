

## 5.3.3 开发嵌入式 SQL C/C++ 应用程序的步骤

开发带有嵌入式 SQL 的 C/C++ 应用程序涉及以下步骤：

- 1. 包含所需的头文件
- 2. 声明宿主变量
- 3. 连接到数据库
- 4. 执行 SQL 语句
- 5. 处理 SQL 错误
- 6. 提交事务
- 7. 断开与数据库的连接

我们将逐一探讨每个步骤。*清单 5.1* 展示了一个基本模板，可用于编写具有嵌入式 SQL 应用程序所需结构的 C 语言程序。

```c
/* (1) Include required header files */
#include <stdio.h>
#include <sqlca.h>

/* (2) Declaration of host variables */
EXEC SQL BEGIN DECLARE SECTION;
...
EXEC SQL END DECLARE SECTION;

/* Declaration of SQLCA structure */
EXEC SQL DECLARE SQLCA;

/* Declaration of main function */
void main()
{
    /* (3) Connect to the database */
    EXEC SQL CONNECT TO <database name>;

    /* Error handling to check connection is successful */
    if (SQLCODE < 0)
    {
        printf("\n Error while connecting to database\n");
        printf("\n Returned SQLCODE = %d\n", SQLCODE);
        exit(1);
    }
    else
    {
        printf("\n Connect to database successfully\n");
    }

    /* (4) Execute SQL statements */
    EXEC SQL SELECT <col1>, <col2> INTO :var1, :var2
    FROM <table name> WHERE <condition>;

    /* Error handling to check SQL statement executed successfully */
    if (SQLCODE < 0)
    {
        printf("\n Error while executing SQL statement\n");
        printf("\n Returned SQLCODE = %d\n", SQLCODE);
        exit(1);
    }

    /* (6) Commit the transaction */
    EXEC SQL COMMIT;

    /* Error handling to check SQL statement executed successfully */
    if (SQLCODE < 0)
    {
        printf("\n Error while Committing data\n");
        printf("\n Returned SQLCODE = %d\n", SQLCODE);
        exit(1);
    }

    /* (7) Disconnect from the database */
    EXEC SQL DISCONNECT FROM <database name>;

    /* Error handling to check whether disconnection is successful */
    if (SQLCODE < 0)
    {
        printf("\n Error while disconnecting from database\n");
        printf("\n Returned SQLCODE = %d\n", SQLCODE);
        exit(1);
    }
    else
    {
        printf("\n Disconnect from database successfully\n");
    }
}
```

**清单 5.1 – 嵌入式 SQL C 程序模板**

*清单 5.1* 中编号的每个项目将在以下各小节中详细讨论。

> **注意：**
> 上述模板位于文件 `template.sqc` 中，该文件包含在随书附带的 `Exercise_Files_DB2_Application_Development.zip` 文件中。

### 5.3.4 嵌入式 SQL C/C++ 应用程序示例

为了说明前几节中提到的不同步骤，我们将使用一个示例应用程序。该应用程序用于员工管理系统，您可以从表中添加、更新、检索和删除员工信息。*图 5.8* 提供了该应用程序功能概述。

![](img/5f6ba170efa3a607142589708531bef8_173_0.png)

**图 5.8 – 嵌入式 SQL C/C++ 示例应用程序功能**

*表 5.4* 描述了 *图 5.8* 中显示的功能。

| 功能 | 操作 |
| :--- | :--- |
| AddEmployeeInfo() | 向表中插入新的员工信息 |
| UpdateEmployeeInfo() | 更新表中的员工薪资 |
| FetchEmployeeInfo() | 从表中检索员工信息 |
| DeleteEmployeeInfo() | 从表中删除员工信息 |

**表 5.4 – 不同操作对应的功能**

> **注意：**
> 本节中显示的所有代码片段均摘自程序 `embeddedC.sqc`，该程序包含在随书附带的文件 `Exercise_Files_DB2_Application_Development.zip` 中。

#### 5.3.4.1 包含所需的头文件

创建嵌入式应用程序的第一步是包含所需的头文件。`sqlca.h` 可能是与 SQL 相关的最重要的头文件，其余头文件则取决于您的 C 应用程序的具体功能。*清单 5.2* 列出了嵌入式 SQL C 应用程序所需的典型头文件。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sqlca.h>
```

**清单 5.2 – 包含所需的头文件**

### 5.3.4.2 声明宿主变量

正如在 *第 1 章 - DB2 应用程序开发简介* 中讨论的，嵌入式 SQL 应用程序借助宿主变量与 C/C++ 宿主语言进行通信。在此第二步中，您必须在程序的顶部 DECLARE 部分中声明宿主变量。宿主变量 DECLARE 部分以 EXEC SQL BEGIN 关键字开始，并以 EXEC SQL END 关键字结束，如 *清单 5.3* 所示。

```c
EXEC SQL BEGIN DECLARE SECTION;
sqlint32 hempno;              /* to store employee id */
char hfirstrname[20];        /* to store employee first name */
char hlastname[20];          /* to store employee last name */
char hedlevel[4];            /* to store employee education level */
double hsalary ;             /* to store employee salary */
double hnewsalary;           /* to store employee new salary */
char hdynstmt[16384];        /* to store SQL statements*/
EXEC SQL END DECLARE SECTION;
```

**清单 5.3 – 声明宿主变量**

### 5.3.4.3 连接到数据库

在能够对数据库执行操作之前，您需要建立连接。数据库连接可以是隐式的，也可以是显式的。隐式连接是指用户 ID 被假定当前用户 ID 的连接。显式连接则需要在连接语句中指定用户 ID 和密码。在 C/C++ 应用程序中，可以通过执行以下语句建立隐式数据库连接：

```c
EXEC SQL CONNECT TO sample;
```

如果您想建立显式连接，请使用以下语句：

```c
EXEC SQL CONNECT TO sample USER administrator USING admin123;
```

*清单 5.4* 显示了带有错误处理的连接语句

```c
(1) EXEC SQL CONNECT TO sample; /* Database name is SAMPLE*/
(2) if (SQLCODE < 0)
{
    printf("\n ERROR WHILE DATABASE CONNECTION\n");
    printf("\n SQLCODE = %d", SQLCODE);
    rc = 1;
    exit(1);
}
else
{
    printf("\n CONNECT TO DATABASE SUCCESSFULLY\n");
}
```

**清单 5.4 – 连接到数据库**

让我们回顾 *清单 5.4* 中显示的每一项：

- 1. 此语句建立了与 **sample** 数据库的连接。
- 2. 此语句检查连接是否成功。SQLCODE 是 DB2 中的一个特殊变量，在语句执行后设置。当 SQLCODE 小于零时，语句因错误而完成。如果 SQLCODE 等于零，语句成功完成；如果大于零，语句带有警告完成。

*图 5.9* 提供了上述代码片段的输出。

![](img/5f6ba170efa3a607142589708531bef8_175_0.png)

**图 5.9 – 连接语句的输出**

如果您包含 **utilemb.h** 头文件，还可以使用随 DB2 示例程序提供的 **Dbconn** 实用函数连接到数据库。*清单 5.5* 展示了如何使用 Dbconn 实用函数。

```c
(1) rc = DbConn(dbAlias, user, pwd);
(2) if (rc != 0)
{
    printf("\n Error while connecting to database");
    return rc;
}
```

**清单 5.5 – 使用 Dbconn 实用函数连接到数据库**

让我们回顾 *清单 5.5* 中显示的每一项：

- 1. 此语句使用 Dbconn 实用函数建立与 sample 数据库的连接。该函数接受用户 ID、密码和数据库名称作为参数。
- 2. 此语句检查连接是否成功。

> **注意：**
> 随 DB2 C 语言示例程序提供的实用函数位于目录 `<DB2_install_path>\sqllib\samples\c`（在 Windows 上）和 `<DB2_install_path>/sqllib/samples/c`（在 Linux 上）。对于 C++，请查找 “cpp” 子目录，例如 `<DB2_install_path>\sqllib\samples\cpp`（在 Windows 上）

### 5.3.4.4 执行 SQL 语句

要执行 SQL 语句，需要 EXEC SQL 关键字来指示 SQL 语句的开始，并且必须以分号 (;) 结尾。在本节中，我们将了解如何执行静态和动态 SQL 语句，并执行诸如 INSERT、SELECT、UPDATE 和 DELETE 之类的不同操作。

#### 5.3.4.4.1 向表中插入数据

让我们看看下面 *清单 5.6* 中展示的函数 **AddEmployeeInfo()**。该函数用于将员工信息插入到 EMPLOYEE 表中。

```c
int AddEmployeeInfo()
{
    int rc = 0;
    printf("\n==============================");
    printf("\n ADD EMPLOYEE INFORMATION");
    printf("\n==============================");
    /*
    EXEC SQL INSERT INTO employee(empno, firstname, lastname, edlevel, salary)
           VALUES (50001, 'RAUL', 'CHONG', 21, 6000),
                  (50002, 'JAMES', 'Ji', 20, 5786),
                  (50003, 'MIN', 'YAO', 20, 5876),
                  (50004, 'IAN', 'HAKES', 19, 5489),
                  (50005, 'VINEET', 'MISHRA', 19, 5600);
    */
    if(SQLCODE < 0)
    {
        printf("\n ERROR WHILE ADDING EMPLOYEE INFORMATION");
        printf("\n RETURNED SQLCODE = %d", SQLCODE);
        rc = -1;
    }
    else
    {
        printf("\n EMPLOYEE ADDED SUCCESSFULLY ");
    }
}
```

**清单 5.6 – 向表中插入数据**

