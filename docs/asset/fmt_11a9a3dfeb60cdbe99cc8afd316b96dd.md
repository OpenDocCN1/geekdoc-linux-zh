
![](img/5f6ba170efa3a607142589708531bef8_207_0.png)

*图 5.31* – 从表中获取员工信息

### 5.5.3.4.3 删除数据

*列表 5.23* 展示了函数 `DeleteEmployeeInfo()`。它调用 `SQLExecDirect` 来删除员工信息。

```c
/* Perform Delete operation */
int DeleteEmployeeInfo(SQLHANDLE hdbc)
{
    int funcRc = 0;
    SQLRETURN rc = SQL_SUCCESS;
    SQLHANDLE hstmt; /* statement handle */

    /* SQL DELETE statement to be executed */
(1) SQLCHAR *stmt = (SQLCHAR *) "DELETE FROM employee WHERE empno >= 50006";

    /* set AUTOCOMMIT OFF */
(2) rc = SQLSetConnectAttr(hdbc, SQL_ATTR_AUTOCOMMIT, (SQLPOINTER)SQL_AUTOCOMMIT_OFF, SQL_NTS);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while setting Auto Commit OFF");
    funcRc = 1;
    exit(1);
}

/* allocate a statement handle */
(3) rc = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while allocating statement handle");
    funcRc = 1;
    exit(1);
}

/* directly execute the statement */
(4) rc = SQLExecDirect(hstmt, stmt, SQL_NTS);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while statement execution");
    funcRc = 1;
    exit(1);
}

/* Commit the transaction */
(5) rc = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while committing transaction");
    funcRc = 1;
    exit(1);
}

/* free the statement handle */
(6) rc = SQLFreeHandle(SQL_HANDLE_STMT, hstmt);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while freeing handle");
    funcRc = 1;
    exit(1);
}
printf("\n Employee Deleted successfully");
return funcRc;
}
```

**列表 5.23 – 删除员工信息**

在上述列表中：

- *(1)* `stmt` 变量包含 SQL DELETE 语句。
- *(2)* 使用 `SQLSetConnectAttr` 函数设置自动提交关闭。
- *(3)* 使用 `SQLAllocHandle()` 函数分配语句句柄。连接句柄和语句句柄作为参数传递。
- *(4)* 使用 `SQLExecDirect()` API 直接执行删除 SQL 语句。语句句柄变量和 `stmt` 变量作为参数传递。
- *(5)* 使用 `SQLEndTran()` API 提交事务。连接句柄和 `SQL_COMMIT` 作为参数传递。
- *(6)* 使用 `SQLFreeHandle()` API 释放已分配的语句句柄。语句句柄作为参数传递。

*图 5.32* 展示了上述代码片段的输出。

![](img/5f6ba170efa3a607142589708531bef8_209_0.png)

图 5.32 – 从表中删除员工信息。

#### 5.5.3.5 断开与数据库的连接

处理完 SQL 语句后，下一步是调用 `SQLDisconnect()` 来断开与数据库的连接。*列表 5.24* 展示了如何执行此操作。

## 清单 5.24 — 从数据库断开连接

在上面的清单中：

- 1. 使用 `SQLDisconnect` API 从数据库断开连接。将连接句柄变量作为参数传入。

```c
/* disconnect from the database */
(1) rc = SQLDisconnect(*pHdbc);
(2) if (rc != SQL_SUCCESS)
{
    printf("\n\nERROR while disconnecting from database.\n");
    funcRc = 1;
    exit(1);
}
printf("\n\nDisconnect from %s database successfully.", dbAlias);
```

- 2. 检查断开连接是否成功。

#### 5.5.3.6 释放句柄

CLI 应用程序的最后一步是释放所有已分配的句柄。要释放已分配的句柄，DB2 CLI 提供了 `SQLFreeHandle` API，它接受句柄类型和句柄变量作为参数。在调用 `SQLFreeHandle()` 之前，应用程序必须调用 `SQLDisconnect()`。如果在 `SQLDisconnect()` 返回之前调用 `SQLFreeHandle()`，将返回 `SQL_ERROR`，且连接仍然有效。*清单 5.25* 展示了如何释放句柄。

## 清单 5.25 – 释放已分配的环境和连接句柄

在上面的清单中：

- 1. 使用 `SQLFreeHandle` 释放已分配的连接句柄。

```c
/* free connection handle */
(1) rc = SQLFreeHandle(SQL_HANDLE_DBC, *pHdbc);
    if (rc != SQL_SUCCESS)
    {
        printf("\n\nERROR while freeing connection handle.\n");
        funcRc = 1;
        exit(1);
    }
    printf("\n\nFree connection handle successfully.");

/* free environment handle */
(2) rc = SQLFreeHandle(SQL_HANDLE_ENV, *pHenv);
    if (rc != SQL_SUCCESS)
    {
        printf("\n\nERROR while freeing environment handle.\n");
        funcRc = 1;
        exit(1);
    }
    printf("\n\nFree environment handle successfully.\n");
```

- 2. 使用 `SQLFreeHandle` 释放已分配的环境句柄。

*图 5.33* 展示了 *清单 5.24* 和 *5.25* 中上述代码片段的输出结果。

![](img/5f6ba170efa3a607142589708531bef8_211_0.png)

**图 5.33** - 释放已分配的句柄

> **注意：**
>
> 本节中展示的所有代码片段均提取自程序 `cli_odbc.c`，该程序包含在随本书提供的 `Exercise_Files_DB2_Application_Development.zip` 文件中。在构建应用程序之前，请确保更改程序中第 52 行和第 53 行的用户 ID 和密码。

### 5.5.4 构建 ODBC/CLI 应用程序

你可以手动通过命令行构建 ODBC/CLI 应用程序，也可以使用 DB2 提供的脚本进行构建。

#### 5.5.4.1 通过命令行构建 ODBC 或 CLI 应用程序

通过命令行构建 ODBC 应用程序涉及以下步骤：

1) 在 Windows 上使用以下命令编译应用程序

```c
cl -Zi -Od -cC -W2 -DWIN32 cli_odbc.c
```

*图 5.34* 展示了上述命令的输出结果

![](img/5f6ba170efa3a607142589708531bef8_212_0.png)

**图 5.34 – 编译应用程序**
