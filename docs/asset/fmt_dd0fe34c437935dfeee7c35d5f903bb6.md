
```c
/* initialize the CLI application by calling a helper utility function defined in utilcli.c */
rc = CLIAppInit(dbAlias, user, pswd, &henv, &hdbc, (SQLPOINTER)SQL_AUTOCOMMIT_ON);
if (rc != 0)
{
    return rc;
}
```

### 清单 5.18 – 使用实用程序函数初始化 CLI 应用程序

上述代码将执行 CLI 应用程序的初始化，将数据库名称（别名）、用户 ID、密码、环境句柄变量和连接句柄变量作为参数。

![](img/5f6ba170efa3a607142589708531bef8_203_0.png)

图 5.30 – INSERT 操作输出

### 5.5.3.4.2 检索数据

使用 `SELECT` 语句检索查询结果包括将应用程序变量绑定到结果集的列，然后将数据行获取到应用程序变量中。为了检索结果集中的行，你需要：

- 将应用程序变量绑定到结果集的每一列。可以通过使用 `SQLBindCol()` 函数完成绑定。
- 通过反复调用 `SQLFetch()` 从结果集中获取数据行，直到返回 `SQL_NO_DATA_FOUND`。

列表 5.22 展示了函数 `FetchEmployeeInfo()`，演示了如何获取员工信息。我们将使用由问号 (`?`) 表示的参数标记。应用程序必须在执行语句之前将每个应用程序变量绑定到 SQL 语句中的参数标记。绑定是通过调用 `SQLBindParameter()` 函数完成的。
