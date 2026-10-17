
`hdbc` 是你设置选项的数据库连接。

`option` 是标识你正在设置的选项常量。

`parameter` 是你为常量设置的值。该参数的性质随选项而异——在某些情况下它是标志，而在其他情况下它是指针或文件句柄。`UDWORD` 是 `unsigned long` 的别名。

可以使用此调用设置的选项范围太多，无法在此处介绍；详情请参阅 ODBC 参考书。但在在本例中，你可以使用此调用来确定数据库是否自动提交 SQL 语句。要操作自动提交，将选项设置为 `SQL_AUTOCOMMIT`，并将参数设置为 `SQL_AUTOCOMMIT_OFF` 或 `SQL_AUTOCOMMIT_ON`，取决于你想要关闭或开启自动提交。

## SQL 解释器

我们的最后一个 ODBC 示例 列表 14-10 实现了一个通用的 SQL 解释器。我们展示了以下内容的源代码：

### 列表 14-10：基于 ODBC 的 SQL 解释器

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sql.h>
#include <sqlext.h>
/*
```

### 列表 14-10（续）

```c
int
get_statement(char* sql_buffer )
{
    char buffer[200];
    char* semi_ptr;
    sql_buffer[0] = '\0';
    while (1) {
        printf("OK> ");
        fflush(stdout);
        gets(buffer);
        if (!strcmp(buffer, "exit") ||
            !strcmp(buffer, "Exit") ||
            !strcmp(buffer, "EXIT")) {
            return (0);
        }
        strcat(sql_buffer, buffer);
        strcat(sql_buffer, " **");
    }
    /* 分号表示 SQL 语句的结束 */
    if ((semi_ptr = strchr(sql_buffer, ':')) != NULL) {
        *semi_ptr = '\0';
        printf("%s\n", buffer);
        fflush(stderr);
        return (1);
    }
}
/*
void
check_return(RETCODE rc,
              HENV henv,
              HDBC hbdc,
              HSTMT hstmt) {
    UCHAR state_str[SQL_MAX_MESSAGE_LENGTH];
    SWORD native_error;
    UCHAR error_msg[SQL_MAX_MESSAGE_LENGTH];
    SWORD error_msg_avail = SQL_MAX_MESSAGE_LENGTH - 1;
    SWORD error_msg_len;
    RETCODE local_rc;
```
```c
if (rc = SQL_ERROR && rc != SQL_SUCCESS_WITH_INFO)
{
  return;
}
local_rc = SQLError (henv,
  hdbc,
  hstmt,
  state_str,
  &native_error,
  error_msg,
  error_msg_avail,
  &error_msg_len);
```
```c
if (local_rc = SQL_SUCCESS && rc != SQL_SUCCESS_WITH_INFO)
{
  fprintf(stderr, "Uninterpretable error: exiting\n");
  exit (EXIT_FAILURE);
}
```
```c
if (rc == SQL_SUCCESS_WITH_INFO)
{
  fprintf(stderr, "Warning: %s:%s\n", state_str, error_msg);
  return;
}
```
```c
fprintf(stderr, "Fatal Error %s:%s\n", state_str, error_msg);
exit (EXIT_FAILURE);
*/
```
```c
main
(void)
{
  HENV henv = SQL_NULL_HENV;
  HDBC hdbc = SQL_NULL_HDBC;
  HSTMT hstmt = SQL_NULL_HSTMT;
  RETCODE rc;
  char sql_statement_text[1000];
  char fetch_buffer[1000];
  SWORD number_cols;
  char column_name[50];
  SWORD type;
  SWORD scale;
  SWORD nullable;
  UDWORD precision;
  SDWORD null_indicator;
  char buf[257];
  short buflen;
```

### 列表 14-10（续）

```c
SQLAllocEnv(&henv);
SQLAllocConnect(henv, &hdbc);
rc = SQLDriverConnect(hdbc,
0,
"*DSN=baseball;UID=mylogin;PWD=password*",
SQL_NTS,
(CHAR*) buf,
sizeof(buf),
&bufl,
SQL_DRIVER_COMPLETE);
check_return (rc, henv, hdbc, hstmt);
```
```c
rc = SQLAllocStmt(hdbc, &hstmt);
check_return (rc, henv, hdbc, hstmt);
```
```c
while (1)
{
    if (!statement(sql_statement_text))
    {
        break;
    }
    rc = SQLExDirect(hstmt, sql_statement_text, SQL_NTS);
    check_return (rc, henv, hdbc, hstmt);
```
```c
rc = SQLNumResultCols(hstmt, &number_cols);
check_return (rc, henv, hdbc, hstmt);
```
```c
if (number_cols == 0)
{
    continue;
}
```
```c
while (1)
{
    rc = SQLFetch(hstmt);
    check_return (rc, henv, hdbc, hstmt);
```
```c
if (rc == SQL_NO_DATA_FOUND)
{
    break;
}
```
```c
for (i = 1; i <= number_cols; i++)
{
    rc = SQLDescribeCol(hstmt,
i,
(UCHAR*) column_name,
sizeof(column_name),
NULL,
&type,
&precision,
&scale,
&nullable);
```
```c
check_return(rc, henv, hdbc, hstmt);
printf("%s", column_name);
```
```c
rc = SQLGetData(hstmt,
1,
SQL_CHAR,
fetch_buffer,
sizeof(buffer),
&null_indicator);
check_return(rc, henv, hdbc, hstmt);
```
```c
if (null_indicator == SQL_NULL_DATA)
{
    printf("\n");
}
else
{
    printf("%s", fetch_buffer);
}
```
```c
SQLFreeHandle(SQL_HANDLE_STMT, hstmt);
SQLFreeHandle(SQL_HANDLE_DBC, hdbc);
SQLFreeHandle(SQL_HANDLE_ENV, henv);
return 0;
}
```

- ✦ 设置游标—在所有示例中，我们都使用“原生”游标：我们每次读取一行数据，直到绘制完游标。然而，ODBC 允许你使用多种类型的游标。这些包括可滚动游标，你可以在游标的内容中向前或向后滚动。
