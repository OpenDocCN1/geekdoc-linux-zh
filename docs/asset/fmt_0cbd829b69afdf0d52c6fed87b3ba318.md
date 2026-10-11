
正如你可能注意到的，每个 ODBC 调用都返回一个类型为 `RETCODE` 的值。该值表示被调用的函数是否成功；在大多数情况下，程序在继续下一次调用之前应该检查此值。

ODBC 调用会返回以下代码之一来指示其是否成功：

- `SQL_SUCCESS`—调用成功。
- `SQL_SUCCESS_WITH_INFO`—调用成功，但驱动程序希望向应用程序提供额外信息。
- `SQL_NO_DATA_FOUND`—信息请求（即 SELECT 语句）未返回数据，或者应用程序已检索到所有数据。
- `SQL_ERROR`—发生错误。应用程序可以请求错误的详细描述。
- `SQL_INVALID_HANDLE`—调用使用了无效的句柄。
- `SQL_STILL_EXECUTING`—如果语句正在异步执行，且应用程序拥有其状态的信息，则返回此值。

许多调用除了这些值之外还返回其他值。如果函数返回 `SQL_ERROR` 或 `SQL_SUCCESS_WITH_INFO`，你可以调用 `SQLGetDiag()` 获取进一步信息。该函数具有以下语法：

### 第 14 章 ♦ 编程 API—扩展示例 471

```
RETCODE SQLError( HENV    henv,
                    HDBC    hdbc,
                    HSTMT   hstmt,
                    UCHAR*   sql_state_string,
                    SWORD   sql_native_error,
                    UCHAR*   error_message,
                    SWORD   FAR* error_message_maximum) )
```

`henv`、`hdbc` 和 `hstmt` 分别给出 ODBC 环境、数据源连接和语句的句柄。根据所检查错误的性质，`hstmt` 或 `hdc` 可能为 `NULL`。

`sql_state_string` 指向一个字符数组，`SQLError()` 可以向其中写入描述 SQL 状态的字符串。该字符串是由一个或多个字母前头的四位数字。ODBC 标准定义了与任何给定 ODBC 调用相关的错误，帮助你调试程序。

`sql_native_error` 指向一个变量，`SQLError()` 可以向其中写入原生错误代码。此错误代码特定于数据源。`SWORD` 是 `long` 的类型定义。

`error_message` 指向一个字符数组，`SQLError()` 可以向其中写入描述错误的字符串。

`error_message_maximum` 提供此字符数组的长度。如果此值超过 `error_message`，驱动程序将截断消息。

`error_len` 指向一个变量，`SQLError()` 向其写入它想要写入的消息长度。`check_return()` 检查每个 ODBC 调用的返回值并调用 `SQLError`：

```
local_rc = SQLError(henv,
                    hdbc,
                    hstmt,
                    state_str,
                    &native_error,
                    error_msg,
                    error_msg_avail,
                    &error_len);
```

`check_return()` 在发生错误时打印诊断消息。

472 第 IV 部分 应用程序

## 执行 SQL 语句

在我们分配了资源、连接了数据库并学会了如何处理错误后，就可以对数据库进行任何操作了。正如你想象的，ODBC 提供了丰富的与数据库的调用。我们在后面的示例中探索这些调用；对于第一个示例，我们查看这些调用中最简单的 `ExecDirect()`。它以文本形式接收语句并直接在数据库上执行。`ExecDirect()` 具有以下语法：

```
RETCODE SQLEecDirect (
    hstmt,
    UCHAR* statement_text,
    SDWORD statement_length)
```

`hstmt` 提供语句的句柄，正如调用 `SQLAllocStmt()`。

`statement_text` 提供执行语句的字符数组地址。

`statement_length` 提供 `statement_text` 的长度（以字节为单位）。常量 `SQL_NTS` 表示 `statement_text` 是 C-NULL 终止字符串。

在列表 14-1 中，我们可以如下使用：

```
rc = SQExecDirect(hstmt, "CREATE TABLE foo (bar INTEGER)", SQL_NTS);
rc = SQExecDirect(hstmt, "INSERT INTO foo(bar) VALUES (1)", SQL_NTS);
rc = SQExecDirect(hstmt, "INSERT INTO foo(bar) VALUES (2)", SQL_NTS);
rc = SQExecDirect(hstmt, "INSERT INTO foo(bar) VALUES (3)", SQL_NTS);
rc = SQExecDirect(hstmt, "DROP TABLE foo", SQL_NTS);
```

每个调用都将字符串字面量作为 `statement_text`。第一个调用创建一个名为 `foo` 的表。接下来三个调用向 `foo` 插入整数。最后一个删除 `foo`。

## 释放资源并断开连接

在我们完成数据库操作后，必须关闭连接并释放资源。我们按照分配和打开的反相反顺序执行。

我们的第一个任务是释放语句。为了这样做，我们使用调用 `SQLFreeStmt()` 它具有以下语法：

```
RETCODE SQLFreeStmt(HSTMT hstmt)
```

其中 `hstmt` 提供语句句柄。

下一步是断开数据源连接。为了做到，我们调用 `SQLDisconnect()`。它的语法如下：

```
RETCODE SQLDisconnect(HDBC hdbc)
```

其中 `hdbc` 提供数据源句柄。

接下来，我们通过 `SQLFreeConnect()` 释放为数据源连接分配的资源。它的语法如下：

```
RETCODE SQLFreeConnect(HDBC hdbc)
```

其中 `hdbc` 提供数据源句柄。

最后，我们通过 `SQLFreeEnv()` 释放为 ODBC 环境分配的资源。它的语法如下：

```
RETCODE SQLFreeEnv(HENV henv)
```

其中 `henv` 提供环境句柄。

列表 14-1 如下调用它们：

```
SQLFreeStmt(hstmt, SQL_DROP);
SQLDisconnect(hdbc);
SQLFreeConnect(hdbc);
SQLFreeEnv(henv);
```

## 将变量绑定到参数

此时，你已经看到了 ODBC 程序的框架。回顾一下，一个程序包含以下步骤：

1. 初始化 ODBC 环境。
2. 初始化数据源并打开它的连接。
3. 初始化语句。
4. 对数据源执行一条或多条指令。
5. 检查返回值是否存在错误。
6. 释放资源并退出。

既然你已经了解如何构建 ODBC 程序以及如何使用它来操作数据源，我们就可以开始一些实际工作了。

列表 14-1 调用函数 `SQLExecDirect` 来创建表并填充数据。如果你只想执行静态 SQL 指令，这样做是可以的，这些指令可以直接编译到你的程序中。然而，在大多数情况下，你会希望使用变量来动态构建 SQL 语句。

ODBC 为你提供了这种方法。在 ODBC 中，动态构建 SQL 语句是一个两步过程：

1. 准备 SQL 语句。SQL 语句中的每个变量都绑定到应用程序中的一个变量上。
2. 执行语句。SQL 语句中每个变量的值从其应用程序中对应的变量中读取。

列表 14-2 展示了如何准备和执行 SQL 语句。列表 14-2 的大部分内容是列表 14-1 的重复，因此我们在这里打印出说明如何准备、绑定和执行语句的代行：

### 列表 14-2：准备 SQL 语句

```
printf("PREPARE an INSERT statement.\n")
rc = SQLPrepare(hstmt, "INSERT INTO bar VALUES (?)", SQL_NTS);
check_return(rc, henv, hdbc, hstmt);
printf("Bind a variable to the ? within the INSERT statement.\n")
rc = SQLBindParameter(hstmt,
                       (UWORD) 1,
                       SQL_PARAM_INPUT,
```
