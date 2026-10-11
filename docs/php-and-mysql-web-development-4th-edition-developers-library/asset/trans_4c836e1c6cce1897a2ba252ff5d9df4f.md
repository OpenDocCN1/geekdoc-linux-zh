

MYSQL_TIME 用于 DATETIME、TIMESTAMP、DATE 和 TIME 类型，但结构中不适用于特定类型的成员将被忽略。例如，month、year 和 day 成员不适用于 TIME 值，而 hour、minute 和 second 成员不适用于 DATE 值。

MYSQL_TIME 结构包含多个成员，但只有一些成员应被视为公共成员。公共成员如下所示：

```c
typedef struct st_mysql_time
{
  unsigned int  year;
  unsigned int  month;
  unsigned int  day;
  unsigned int  hour;
  unsigned int  minute;
  unsigned int  second;
  unsigned long second_part;
  my_bool       neg;
  ...
} MYSQL_TIME;
```

成员的使用方式如下：

- **year, month, day**
  - 包含日期部分的时值中的年、月、日部分。
- **hour, minute, second, second_part**
  - 包含时间部分的时值中的时、分、秒和小数秒部分。
- **neg**
  - 一个标志，指示 MYSQL_TIME 结构中容纳的时值是否为负数。

## G.2.3 访问器宏

mysql.h 包含一些宏，使您能够更便捷地测试 MYSQL_FIELD 成员。IS_NUM() 测试 type 成员；此处列出的其他宏测试 flags 成员。

- **IS_NUM()** 如果列中的值具有数字类型，则为 true（非零）：
  ```c
  if (IS_NUM (field->type))
    printf ("Field %s is numeric\n", field->name);
  ```
- **IS_PRI_KEY()** 如果列是主键的一部分，则为 true：
  ```c
  if (IS_PRI_KEY (field->flags))
    printf ("Field %s is part of primary key\n", field->name);
  ```
- **IS_NOT_NULL()** 如果列不能包含 *NULL* 值，则为 true：
  ```c
  if (IS_NOT_NULL (field->flags))
    printf ("Field %s values cannot be NULL\n", field->name);
  ```
- **IS_BLOB()** 如果列是 *BLOB* 或 *TEXT*，则为 true。然而，此宏测试的是 *flags* 成员中已弃用的 *BLOB_FLAG* 位，因此 `IS_BLOB()` 也被弃用。

## G.3 C API 函数

C API 的客户端库函数在以下各部分中详细描述，按类别分组，并在类别内按字母顺序列出。某些参数名称在函数描述中反复出现，并具有以下约定含义：

- *conn* 是指向服务器连接的 `MYSQL` 连接处理器的指针。
- *res_set* 是指向 `MYSQL_RES` 结果集结构的指针。
- *field* 是指向 `MYSQL_FIELD` 列信息结构的指针。
- *row* 是来自结果集的 `MYSQL_ROW` 数据行。
- *row_num* 是结果集中的行号，从 0 到小于行数（即行数减一）。
- *col_num* 是结果集中某行中的列号，从 0 到小于列数（即列数减一）。
- *stmt* 是预编译语句的处理程序。

为简洁起见，如果这些参数在其所出现的函数描述中未提及，您可以假设其含义如前所述。

### G.3.1 客户端库初始化和终止例程

本节描述用于初始化和终止 C API 库的例程。实际上有两个此类库，但它们接口相同，因此特定程序可以根据链接时选择的库来生成可执行映像，从而使用其中任何一个库：

- `libmysqlclient` 用于连接独立 MySQL 服务器的程序。
- `libmysqld` 用于在程序本身中包含嵌入服务器的程序。

通过在程序中使用 `mysql_library_init()` 和 `mysql_library_end()` 例程来初始化和终止客户端库，您可以使用相同的源代码来生成针对独立服务器的客户端或使用嵌入服务器的客户端，具体取决于您在链接时选择的库。有关链接适当的 C API 库的信息，请参见第 G.1 节“编译和链接”。

**mysql_library_end** (void);

终止客户端库。您应该在完成与服务器通信后调用此函数。如果程序使用嵌入服务器库，则此例程将关闭嵌入服务器。

此例程在 MySQL 5.0.3 中引入。在 5.0.3 之前，您可以调用 `mysql_server_end()`。

**mysql_library_init** (int argc, char **arg, char **groups);

初始化客户端库。成功时返回零，否则返回非零值。此函数必须在调用其他任何 mysql_xxxx() 函数之前调用。如果程序使用嵌入服务器库，则此例程将初始化嵌入服务器。

如果程序使用嵌入服务器，*argc* 和 *arg* 参数类似于传递给 C 程序中 *main*() 的标准参数：*argc* 是参数计数；如果没有参数，*argc* 应为零。否则，*argc* 应为传递给服务器的参数数量。*arg* 是包含参数的以空字符结尾的字符串数组。请注意，*arg*[0] 将被忽略。

*groups* 参数是一个由以空字符结尾的字符串组成的数组，指示嵌入服务器应读取哪些选项文件组。数组的最后一个元素应为 *NULL*。如果 *group* 本身为 *NULL*，则服务器默认读取 [server] 和 [embedded] 选项文件组。*groups* 数组中的组名应不带周围的 ‘[’ 和 ‘]’ 字符。

此例程在 MySQL 5.0.3 中引入。在 5.0.3 之前，您可以调用 `mysql_server_init()`。

**mysql_server_end** (void);

此例程是 `mysql_library_end()` 的同义词，但可在 MySQL 5.0.3 之前使用。

**mysql_server_init** (int argc, char **arg, char **groups);

此例程是 `mysql_library_init()` 的同义词，但可在 MySQL 5.0.3 之前使用。

### G.3.2 连接管理例程

这些函数使您能够建立和终止与服务器的连接，设置影响连接建立方式的选项，重新建立已超时的连接，以及更改连接的某些方面，例如当前用户名或字符集。

典型的序列包括调用 `mysql_init()` 来初始化连接处理器，调用 `mysql_real_connect()` 来建立连接，并在完成后调用 `mysql_close()` 来终止连接。如果需要指示特殊选项或设置加密的 SSL 连接，请在 `mysql_init()` 之后、`mysql_real_connect()` 之前调用 `mysql_options()` 或 `mysql_ssl_set()`。

- **mysql_change_user** (MYSQL *conn, const char *user_name, const char *password, const char *db_name);

更改由 *conn* 指定的连接的用户和默认数据库。该数据库成为不包含数据库限定符的表引用的默认数据库。如果 *db_name* 为 *NULL*，则不选择默认数据库。

如果用户被允许连接到服务器，并且如果指定了数据库，则该用户有权访问该数据库，`mysql_change_user()` 将返回 true。否则，函数失败，当前用户和数据库保持不变。

使用 `mysql_change_user()` 更改当前用户比关闭连接并使用不同参数重新打开连接要快。此函数也可用于为在执行过程中为不同用户提供服务的程序实现持久连接。

- **void mysql_close** (MYSQL *conn);

关闭由 *conn* 指定的连接。当您完成服务器会话时调用此例程。如果连接处理器是由 `mysql_init()` 自动分配的，`mysql_close()` 将释放它。

如果尝试打开连接失败，则无需调用 `mysql_close()`。但是，如果 `mysql_init()` 分配了处理器，您可能会希望这样做，以便可以将其释放。

- **void mysql_get_character_set_info** (MYSQL *conn, MY_CHARSET_INFO *cs_info);

获取当前客户端字符集的信息。*cs_info* 指向应放置信息的 *MY_CHARSET_INFO* 结构。该结构如下所示：

```c
typedef struct character_set
{
  unsigned int    number;  /* Character set number  */
  unsigned int    state;   /* Character set state   */
  const char      *cname;  /* Collation name        */
  const char      *name;   /* Character set name    */
```

