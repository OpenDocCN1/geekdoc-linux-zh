

![](img/5f6ba170efa3a607142589708531bef8_203_0.png)

图 5.30 – INSERT 操作输出

### 5.5.3.4.2 检索数据

使用 SELECT 语句检索查询结果包括将应用程序变量绑定到结果集的列，然后将数据行获取到应用程序变量中。为了检索结果集中的行，你需要：

- 将应用程序变量绑定到结果集的每一列。可以通过使用 `SQLBindCol()` 函数完成绑定。
- 通过反复调用 `SQLFetch()` 从结果集中获取数据行，直到返回 `SQL_NO_DATA_FOUND`。

列表 5.22 展示了函数 `FetchEmployeeInfo()`，演示了如何获取员工信息。我们将使用由问号 (?) 表示的参数标记。应用程序必须在执行语句之前将每个应用程序变量绑定到 SQL 语句中的参数标记。绑定是通过调用 `SQLBindParameter()` 函数完成的。

```c
/* perform Select operation */
int FetchEmployeeInfo(SQLHANDLE hdbc)
{
    int funcRc = 0;
    SQLRETURN rc = SQL_SUCCESS;
    SQLHANDLE hstmt; /* statement handle */

(1) /* SQL SELECT statement to be executed */
    SQLCHAR *stmt = (SQLCHAR *) "SELECT firstname, lastname, edlevel FROM employee WHERE empno >= ? ";

    sqlint32 empno = 0;

(2) struct
    {
        SQLINTEGER ind;
        SQLCHAR value[20];
    } firstname;   /* variable to be bound to the firstname column */

    struct
    {
        SQLINTEGER ind;
        SQLCHAR value[15];
    } lastname;   /* variable to be bound to the lastname column */

    struct
    {
        SQLINTEGER ind;
        SQLSMALLINT value;
    } edlevel;   /* variable to be bound to the edlevel column */

    /* set AUTOCOMMIT OFF */
(3) rc = SQLSetConnectAttr(hdbc, SQL_ATTR_AUTOCOMMIT,
      (SQLPOINTER)SQL_AUTOCOMMIT_OFF, SQL_NTS);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while handle allocation");
    funcRc = 1;
    exit(1);
}

/* allocate a statement handle */
(4) rc = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while allocating statement handle ");
    funcRc = 1;
    exit(1);
}

/* prepare the statement */
(5) rc = SQLPrepare(hstmt, stmt, SQL_NTS);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while preparing statement");
    funcRc = 1;
    exit(1);
}

/* bind empno to the statement */
(6) rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_LONG,
        SQL_INTEGER, 0, 0, &empno, 0, NULL);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while binding parameters");
    funcRc = 1;
    exit(1);
}

/* execute the statement for empno = 50006 */
empno = 50006;

/* execute the statement */
(7) rc = SQLExecute(hstmt);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while statement execution");
    funcRc = 1;
    exit(1);
}

/* bind column 1 to variable */
(8) rc = SQLBindCol(hstmt, 1, SQL_C_CHAR, firstname.value, 20,
        &firstname.ind);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while binding column");
    funcRc = 1;
    exit(1);
}

/* bind column 2 to variable */
(9) rc = SQLBindCol(hstmt, 2, SQL_C_CHAR, lastname.value, 15,
        &lastname.ind);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while binding column");
    funcRc = 1;
    exit(1);
}

/* bind column 3 to variable */
(10) rc = SQLBindCol(hstmt, 3, SQL_C_SHORT, &edlevel.value, 0,
        &edlevel.ind);
if(rc != SQL_SUCCESS)
{
    printf("\n Error while binding column");
    funcRc = 1;
    exit(1);
}

printf("\n\n  FIRSTNAME      LASTNAME     EDLEVEL  \n");
printf("  ---------    ---------   ------\n");

/* fetch each row and display  */
(11) rc = SQLFetch(hstmt);
if (rc == SQL_NO_DATA_FOUND)
{
    printf("\n  Data not found.\n");
}
while (rc != SQL_NO_DATA_FOUND)
{
    printf("  %8s %14s %8d \n", firstname.value, lastname.value, edlevel.value);
    /* fetch next row  */
    rc = SQLFetch(hstmt);
}

/* Commit the transaction  */
(12) rc = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);
if (rc != SQL_SUCCESS)
{
    printf("\n Error while committing the transaction");
    funcRc = 1;
    exit(1);
}

/* free the statement handle  */
(13) rc = SQLFreeHandle(SQL_HANDLE_STMT, hstmt);
if (rc != SQL_SUCCESS)
{
    printf("\n Error while freeing handle");
    funcRc = 1;
    exit(1);
}
return funcRc;
}
```

**列表 5.22 – 从表中获取数据**

在上述列表中：

- *(1)* `stmt` 变量包含 SELECT 语句。
- *(2)* 将要绑定到 firstname、lastname 和 edlevel 列的变量。
- *(3)* 使用 `SQLSetConnectAttr` 函数设置自动提交关闭。
- *(4)* 使用 `SQLAllocHandle` 函数分配语句句柄。
- *(5)* 使用 `SQLPrepare` 准备 SELECT 语句，因为语句中有参数标记。
- *(6)* 使用 `SQLBindParameter` 函数将 `empno` 变量绑定到语句。
- *(7)* 使用 `SQLExecute` 函数执行语句，对应 empno 为 50006。
- *(8)* 使用 `SQLBindCol` 函数将第 1 列绑定到变量 firstname。
- *(9)* 使用 `SQLBindCol` 函数将第 2 列绑定到变量 lastname。
- *(10)* 使用 `SQLBindCol` 函数将第 3 列绑定到变量 edlevel。
- *(11)* 使用 `SQLFetch` 函数获取每一行并显示结果。
- *(12)* 使用 `SQLEndTran` 函数提交事务。
- *(13)* 使用 `SQLFreeHandle` 函数释放已分配的语句句柄。

*图 5.31* 展示了上述代码片段的输出。

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
- *(4)* 使用 `SQLExecDirect()` API 直接执行删除 SQL 语句。语句句柄变量和 stmt 变量作为参数传递。
- *(5)* 使用 `SQLEndTran()` API 提交事务。连接句柄和 SQL_COMMIT 作为参数传递。
- *(6)* 使用 `SQLFreeHandle()` API 释放已分配的语句句柄。语句句柄作为参数传递。

*图 5.32* 展示了上述代码片段的输出。

![](img/5f6ba170efa3a607142589708531bef8_209_0.png)

图 5.32 – 从表中删除员工信息。

### 5.5.3.5 断开与数据库的连接

处理完 SQL 语句后，下一步是调用 `SQLDisconnect()` 来断开与数据库的连接。*列表 5.24* 展示了如何执行此操作。

