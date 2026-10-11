

## G.3.9.2 预编译语句的构建与例程

本节中的函数允许你将预编译的 SQL 语句发送到服务器。每个字符串必须由单个 SQL 语句组成，并且不应以分号字符（`;`）或 `\v` 序列结尾。`;` 和 `\v` 是 `mysql` 客户端程序的约定，而非 C 客户端库的约定。

要查看一个演示如何使用其中许多函数的示例程序，请参阅第 7.9 节，“使用服务器端预编译语句”。

### `mysql_stmt_bind_param`

- **签名：** `my_bool mysql_stmt_bind_param (MYSQL_STMT *stmt, MYSQL_BIND *bind_array);`
- **描述：** 给定一个预编译语句句柄 `stmt`，`mysql_stmt_bind_param()` 函数将一组数据值绑定到语句中的“?” 占位符。`bind_array` 是 `MYSQL_BIND` 结构体数组的地址。数组中必须包含与预编译语句中每个占位符相对应的结构体。如果绑定操作成功，`mysql_stmt_bind_param()` 返回零，否则返回非零值。

### `mysql_stmt_close`

- **签名：** `my_bool mysql_stmt_close (MYSQL_STMT *stmt);`
- **描述：** 关闭预编译语句句柄并释放与之相关的任何资源。这包括取消句柄可能存在的任何待处理结果。如果成功，`mysql_stmt_close()` 返回零，否则返回非零值。
- **注意：** 在关闭语句句柄后，请勿尝试将其用于进一步的操作。如果在连接关闭时服务器仍有与给定客户端连接相关联的预编译语句，它将丢弃这些语句。

### `mysql_stmt_init`

- **签名：** `MYSQL_STMT * mysql_stmt_init (MYSQL *conn);`
- **描述：** 分配并初始化一个 `MYSQL_STMT` 句柄。返回指向该句柄的指针，如果无法分配句柄，则返回 `NULL`。
- **注意：** 当使用完毕时，你应当使用 `mysql_stmt_close()` 释放该句柄。

### `mysql_stmt_execute`

- **签名：** `int mysql_stmt_execute (MYSQL_STMT *stmt);`
- **描述：** 执行与给定语句句柄关联的预编译语句。如果语句执行成功，返回零；否则返回非零值。
- **前置条件：** 在执行语句之前，如果语句包含任何“?” 占位符，你必须通过调用 `mysql_stmt_bind_param()` 将数据值绑定到该语句。
- **执行后：** 在成功执行后，根据语句是否返回结果集来确定其结果。对于不返回结果集的语句，调用 `mysql_stmt_affected_rows()` 以确定插入、删除或更新的行数。对于返回结果集的语句，元数据变得可用，并可通过 `mysql_stmt_result_metadata()` 获取。要获取结果，请使用 `mysql_stmt_bind_result()` 将结果缓冲区绑定到列，使用 `mysql_stmt_fetch()` 获取行，并使用 `mysql_stmt_free_result()` 释放结果集。

### `mysql_stmt_prepare`

- **签名：** `int mysql_stmt_prepare (MYSQL_STMT *stmt, const char *stmt_str, unsigned long length);`
- **描述：** 给定一个指定为带计数字符串的 SQL 语句，`mysql_stmt_prepare()` 将语句发送到服务器以进行预编译以备后续执行，并将语句句柄 `*stmt*` 与该预编译语句关联。语句文本由 `*stmt_str*` 给出，其长度由 `*len*`（或 `*cnt*`）指示。该字符串可以包含二进制数据（包括空字节）。
- **返回值：** 如果成功，`mysql_stmt_prepare()` 返回零；如果失败，返回非零值。
- **参数：** 语句可以包含 `'?'` 字符作为参数标记，以指示在执行时数据值应绑定到语句的位置。

### `mysql_stmt_reset`

- **签名：** `my_bool mysql_stmt_reset (MYSQL_STMT *stmt);`
- **描述：** 将预编译语句句柄重置为调用 `mysql_stmt_prepare()` 后所处的状态。

### `mysql_stmt_result_metadata`

- **签名：** `MYSQL_RES * mysql_stmt_result_metadata (MYSQL_STMT *stmt);`
- **描述：** 在成功调用 `mysql_stmt_execute()` 后，如果预编译语句是返回结果集的语句，`mysql_stmt_result_metadata()` 返回关于由此产生的列的元数据。返回值是指向 `MYSQL_RES` 结构体的指针。结果集结构体类似于调用 `mysql_store_result()` 后获得的非预编译语句的结构体，除了它不包含任何数据。你可以通过将该结构体指针传递给接受 `MYSQL_RES` 参数的函数来获取列的信息，例如 `mysql_fetch_field()`、`mysql_fetch_fields()` 和 `mysql_num_fields()`。当你使用完该结构体后，请将其传递给 `mysql_free_result()` 以将其释放。
- **注意：** 如果预编译语句不是返回结果集的语句，`mysql_stmt_result_metadata()` 返回 `NULL`，以表示没有可用的元数据信息。

### `mysql_stmt_send_long_data`

- **签名：** `my_bool mysql_stmt_send_long_data (MYSQL_STMT *stmt, unsigned int param_num, const char *data, unsigned long length);`
- **描述：** 此函数可用于分块发送长 BLOB 或 TEXT 值。`*param_num*` 指示调用适用的参数。它可以是 `0` 到 `mysql_stmt_param_count(stmt)-1` 之间的任意值。`*data*` 是指向包含要发送数据缓冲区的指针，`*length*` 指示要发送的字节数。

## G.3.9.3 预编译语句结果集处理例程

当执行预编译语句产生结果集时，本节的函数允许你检索该集并访问其内容。

要查看一个演示如何使用其中许多函数的示例程序，请参阅第 7.9 节，“使用服务器端预编译语句”。

### `mysql_stmt_affected_rows`

- **签名：** `my_ulonglong mysql_stmt_affected_rows (MYSQL_STMT *stmt);`
- **描述：** 此函数是 `mysql_affected_rows()` 的预编译语句等价物，不同之处在于你在调用 `mysql_stmt_execute()` 之后调用它。对于不返回结果集的语句，`mysql_stmt_affected_rows()` 返回通过执行该语句插入、删除或更新的行数。对于返回结果集的语句，此函数的行为类似于 `mysql_num_rows()`。
- **注意：** `mysql_stmt_affected_rows()` 返回一个 `my_ulonglong` 值；有关打印此类型值的说明，请参阅第 G.2.1 节，“标量数据类型”。

### `mysql_stmt_attr_get`

- **签名：** `my_bool mysql_stmt_attr_get (MYSQL_STMT *stmt, enum enum_stmt_attr_type attr_type, void *attr);`
- **描述：** 获取预编译语句句柄属性。有关允许的 `attr_type` 属性值的说明，请参阅 `mysql_stmt_attr_set()` 的描述。`attr` 是指向应写入属性值的变量的指针。（例外：在 MySQL 5.1.7 之前，获取 `STMT_ATTR_UPDATE_MAX_LENGTH` 属性时，传入指向 `unsigned int` 的指针，而不是指向 `my_bool` 的指针。）
- **示例：**
```cpp
my_bool attr;
if (mysql_stmt_attr_get (stmt, STMT_ATTR_UPDATE_MAX_LENGTH, &attr) == 0)
    printf ("Attribute gotten successfully\n");
else
    printf ("Could not get attribute\n");
```
- **返回值：** 如果成功获取属性，`mysql_stmt_attr_get()` 返回零；如果属性类型未知，则返回非零值。

### `mysql_stmt_attr_set`

- **签名：** `my_bool mysql_stmt_attr_set (MYSQL_STMT *stmt, enum enum_stmt_attr_type attr_type, const void *attr);`
- **描述：** 设置预编译语句句柄属性。`attr_type` 指示要设置哪个属性，`attr` 是指向包含属性值的变量的指针。
- **`attr_type` 的允许值：**
  - `STMT_ATTR_UPDATE_MAX_LENGTH` 控制 `mysql_stmt_store_result()` 是否计算结果集列的 `max_length` 元数据值。要启用或禁用此属性，请传入指向设置为 `true` 或 `false` 的 `my_bool` 的 `attr` 值。默认情况下，禁用 `max_length` 计算。

### `mysql_stmt_error`

- **签名：** `const char * mysql_stmt_error (MYSQL_STMT *stmt);`
- **描述：** 返回一个以空字符结尾的字符串，其中包含最近一次调用的、返回了状态的预编译语句例程的错误消息。如果没有发生错误，返回值是空字符串（这是零长度字符串 `""`，而不是 `NULL` 指针）。尽管通常你是在已经知道发生错误之后才调用 `mysql_stmt_error()`，但返回值本身可用于检测是否发生了错误：
- **示例：**
```cpp
const char *err = mysql_stmt_error (stmt);
if (err[0] == 0)          /* empty string */
    printf ("Everything is okay\n");
else
    printf ("Something is wrong!\n");
```

### `mysql_stmt_sqlstate`

- **签名：** `const char * mysql_stmt_sqlstate (MYSQL_STMT *stmt);`
- **描述：** 返回一个以空字符结尾的字符串，其中包含最近一次调用的、返回了状态的预编译语句例程的 SQLSTATE 错误代码。此代码是一个五个字符的字符串。SQLSTATE 值取自 ANSI SQL 和 ODBC 标准。值为 `"00000"` 表示“无错误”。值为 `"HY000"` 表示“一般错误”。该值用于那些尚未分配更具体 SQLSTATE 代码的 MySQL 错误。
- **示例：**
```cpp
if (strncmp (mysql_stmt_sqlstate (stmt), "00000") == 0)
    printf ("Everything is okay\n");
else
    printf ("Something is wrong!\n");
```

