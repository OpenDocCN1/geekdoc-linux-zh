
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "sql.h"
#include "sqlext.h"

****************************************************************/
* 检查函数的返回值。如果它表示错误，
* 调用 `SQLError()` 获取错误详细信息，打印输出
* 并退出；否则，直接返回。
/****************************************************************/

void
check_return(RETCODE rc,
    HENV henv,
    HDBC hdbc,
    HSTMT hstmt)
{
    CHAR state_str[SQL_MAX_MESSAGE_LENGTH];
    SDWORD native_error;
    CHAR error_msg[SQL_MAX_MESSAGE_LENGTH];
    SQLWORD error_msg_avail = SQL_MAX_MESSAGE_LENGTH - 1;
    SQLINTEGER error_msg_len;
    RETCODE local_rc;

    if (rc != SQL_ERROR && rc != SQL_SUCCESS_WITH_INFO)
    {
        return;
    }

    local_rc = SQLError(henv,
hdbc,
hstmt,
state_str,
    &native_error,
error_msg,
error_msg_avail,
    &error_msg_len);

    if (local_rc != SQL_SUCCESS && rc != SQL_SUCCESS_WITH_INFO)
    {
        fprintf(stderr, "Uninterpretable error: exiting\n");
        exit (EXIT_FAILURE);
    }

    if (rc == SQL_SUCCESS_WITH_INFO)
    {
        fprintf(stderr, "Warning %s: %s\n", state_str, error_msg);
        return;
    }
```

```c
fprintf(stderr, "Fatal Error: %s\n", state_str, error_msg);
exit(EXIT_FAILURE);
/* ... */
int main(void) {
    HENV henv = SQL_NULL_HENV;
    HDBC hdc = SQL_NULL_HDBC;
    HSTMT hstmt = SQL_NULL_HSTMT;
    RETCODE rc;

    char buf[257];
    short buflen;

    printf("Initialize the environment structure.\n");
    SQLAllocEnv(&henv);

    printf("Initialize the connection structure.\n");
    SQLAllocConnect(henv, hdc);

    printf("Load the ODBC driver.\n");
    rc = SQLDriverConnect(hdc,
                            0,
                            "DSN=baseball;UID=mylogin;PWD=password",
                            SQL_NTS,
                            (CHAR*)buf,
                            sizeof(buf),
                            &buflen,
                            SQL_DRIVER_COMPLETE);
    check_return(rc, henv, hdc, hstmt);

    printf("Initialize the statement structure.\n");
    SQLAllocStmt(henv, hdc, &hstmt);

    /* Now, do something */
    printf("Create table table \"foo\".\n");
    rc = SQLExecDirect(hstmt, "CREATE TABLE foo (bar INTEGER)", SQL_NTS);
    check_return(rc, henv, hdc, hstmt);

    printf("Insert values into table \"foo\".\n");
    rc = SQLExecDirect(hstmt, "INSERT INTO foo(bar) VALUES (1)", SQL_NTS);
    check_return(rc, henv, hdc, hstmt);

    check_return(rc, henv, hdc, hstmt);
}
```

`complete_connect_string` 提供 ODBC 驱动程序可以写入完整连接字符串的地址；即已经根据初始化文件中提取的定义进行了“填充”的连接字符串。此缓冲区长度至少为 255 字节。

`complete_connect_string_max` 提供 `complete_connect_string` 所指向的数组的长度（以字节为单位）。

`complete_connect_string_length` 指向一个变量，ODBC 驱动程序可以将其写入到 `complete_connect_string` 指向的缓冲区中的文本长度写入该变量。如果完整连接字符串长于 `complete_connect_string_max` 给出的值，驱动程序将对其进行截断。

最后，`completion_flag` 提供一个标志，告诉驱动程序在连接未完成时应该如何处理。它识别以下值：

- `SQL_DRIVER_PROMPT`—显示一个显示连接字符串取值的提示框。在驱动程序尝试连接到远程数据源之前，用户必须进行确认。无论连接字符串是否完整（即包含加载驱动程序和连接数据源所需的所有信息），都会显示提示框。

- `SQL_DRIVER_COMPLETE`—如果连接字符串包含加载驱动程序和连接所需的所有信息，则执行连接。否则，显示提示框并请求更多信息。

- `SQL_DRIVER_COMPLETE_REQUIRED`—与 `SQL_DRIVER_COMPLETE` 相同，但所有对于连接数据源并非必需的字段都显示为灰色。

- `SQL_DRIVER_NOPROMPT`—如果连接字符串不完整，则失败。

大多数 Linux ODBC 驱动程序不使用提示框，因此这四个标志在实际上都等同于 `SQL_DRIVER_NOPROMPT`。在我们的程序中，如下调用此函数：

```
rc = SQLDriverConnect(hdbc,
               0,
               "DSN=baseball;UID=login;PWD=password",
               SQL_NTS,
               (CHAR*)buf,
               &buflen,
               SQL_DRIVER_COMPLETE);
```

注意第三个参数的格式，它提供了连接字符串。如你所见，它由三个用分号隔开的变量=值对对组成。变量 `DSN` 命名数据源；ODBC 驱动管理器使用此字符串来查找用户 ODBC 初始化文件中定义的数据源设置。变量 `UID` 给出用户标识符，变量 `PWD` 设置用户密码。如果您愿意，还可以设置其他 ODBC 变量，甚至覆盖用户 ODBC 初始化文件中的一个或多个设置。

## 语句资源的分配

在我们连接到数据库后，可以为 SQL 语句分配资源。为了这样做，如下调用函数 `SQLAllocStmt()`：

```
RETCODE SQLAllocStmt(HDBC hdc, HSTMT* hstmt)
```

`hdc` 提供数据库连接的句柄，该句柄是通过调用 `SQLAllocConnect()` 获取并通过调用 `SQLDriverConnect()` 初始化的。

`hstmt` 指向一个变量，ODBC 驱动程序可以将新分配语句的句柄写入该变量。在我们的程序中，如下调用它：

```
SQLAllocStmt(hdc, hstmt)
```

对于每个数据库连接，我们可以分配多个语句。其中某些是异步执行的——即“在后台”执行——而我们也可以同步执行。

## 错误处理
