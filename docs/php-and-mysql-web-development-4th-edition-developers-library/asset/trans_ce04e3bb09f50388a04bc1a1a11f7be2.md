

- `STMT_ATTR_CURSOR_TYPE` 指示在调用 `mysql_stmt_execute()` 时为语句使用何种类型的游标。`arg` 指向一个 *unsigned long*，它可以设置为 `CURSOR_TYPE_NO_CURSOR`（这是默认值）或 `CURSOR_TYPE_READ_ONLY`。

- `STMT_ATTR_PREFETCH_ROWS` 指示当使用游标时，每次从服务器获取多少行数据。`arg` 指向一个设置为行数的 *unsigned long*。该值应至少为 1（这是默认值）。

以下示例启用了结果集的 max_length 计算：

```c
my_bool attr = 1;
if (mysql_stmt_attr_set (stmt, STMT_ATTR_UPDATE_MAX_LENGTH, &attr) == 0)
    printf ("Attribute set successfully\n");
else
    printf ("Could not set attribute\n");
```

如果属性设置成功，`mysql_stmt_attr_set()` 返回零；如果属性类型未知，则返回非零值。

- **签名：**
    - `my_bool mysql_stmt_bind_result (MYSQL_STMT *stmt, MYSQL_BIND *bind_array);`

给定预编译语句句柄 `stmt`，`mysql_stmt_bind_result()` 函数提供一个 `MYSQL_BIND` 结构体数组，用于获取结果集的行。`bind_array` 是 `MYSQL_BIND` 结构体数组的地址。数组中必须为结果集中的每一列包含一个结构体。每次调用 `mysql_stmt_fetch()` 获取结果集的一行时，列值将返回到 `MYSQL_BIND` 结构体中。如果绑定操作成功，`mysql_stmt_bind_result()` 返回零，否则返回非零值。

必须在获取行之前将结构体绑定到结果集的列，并且结构体指向的缓冲区必须足够大以存储获取的值。在获取结果集时调用 `mysql_stmt_bind_result()` 将列绑定到不同的 `MYSQL_STMT` 结构体是允许的。`mysql_stmt_fetch()` 使用的是最近的绑定。

- **签名：**
    - `void mysql_stmt_data_seek (MYSQL_STMT *stmt, my_ulonglong row_num);`

定位到结果集的特定行。`row_num` 的值范围可以从 0 到 `mysql_stmt_num_rows(stmt)-1`。如果 `row_num` 超出范围，结果将不可预测。

`mysql_stmt_data_seek()` 要求整个结果集已检索到客户端内存中，因此只有在你执行语句后调用了 `mysql_stmt_store_result()` 的情况下才能使用它。

`mysql_stmt_data_seek()` 与 `mysql_stmt_row_seek()` 不同，后者使用 `mysql_stmt_row_tell()` 返回的行偏移值，而不是行号。

- **签名：**
    - `unsigned int mysql_stmt_field_count (MYSQL_STMT *stmt);`

在调用 `mysql_stmt_prepare()` 并使用语句句柄之后，可以调用此函数。它返回执行语句时将生成的结果集中的列数。如果语句不会产生结果集（例如，如果它是 INSERT 或 UPDATE），`mysql_stmt_field_count()` 返回零。

- **签名：**
    - `int mysql_stmt_fetch (MYSQL_STMT *stmt);`

在对返回结果集的预编译语句成功调用 `mysql_stmt_execute()` 之后，可选地调用 `mysql_stmt_store_result()` 将结果集检索到客户端内存，然后调用 `mysql_stmt_fetch()` 获取结果行的数据。首先必须通过调用 `mysql_stmt_bind_result()` 将用于获取结果列的缓冲区绑定到 `MYSQL_BIND` 结构体。

如果成功获取了一行，`mysql_stmt_fetch()` 返回零；如果没有更多行可获取，返回 `MYSQL_NO_DATA`；如果发生错误，返回 1。成功获取后，列值将出现在绑定到结果的 `MYSQL_BIND` 结构体中。

- **签名：**
    - `int mysql_stmt_fetch_column (MYSQL_STMT *stmt, MYSQL_BIND *bind, unsigned int col_num, unsigned long offset);`

此函数从当前结果集行中获取单列的数据。成功时返回零，发生错误时返回非零值。`bind` 是一个 `MYSQL_BIND` 结构体，应设置为指示要检索的值类型、检索到的缓冲区以及要检索的数据长度（数量）。`col_num` 指示要获取哪一列。其值范围可以从 0 到 `mysql_stmt_field_count(stmt)-1`。`offset` 指示列值中开始值检索的偏移量；0 表示值的开头。

- **签名：**
    - `my_bool mysql_stmt_free_result (MYSQL_STMT *stmt);`

释放与给定语句句柄相关联的结果集所使用的内存。成功时返回零，否则返回非零值。未获取的行将被丢弃。你必须为句柄生成的每个结果集调用 `mysql_stmt_free_result()`。

# 1172 附录 G C API 参考

- **签名：**
    - `my_ulonglong mysql_stmt_insert_id (MYSQL_STMT *stmt);`

此函数是 `mysql_insert_id()` 的预编译语句等价物。在你调用 `mysql_stmt_execute()` 执行生成 `AUTO_INCREMENT` 值的语句之后使用它。

`mysql_stmt_insert_id()` 返回一个 `my_ulonglong` 值；有关打印此类型值的注意事项，请参见第 G.2.1 节“标量数据类型”。

- **签名：**
    - `my_ulonglong mysql_stmt_num_rows (MYSQL_STMT *stmt);`

如果你已通过调用 `mysql_stmt_store_result()` 将结果检索到客户端内存，则返回结果集中的行数。如果你没有调用 `mysql_stmt_store_result()`，`mysql_stmt_num_rows()` 返回零。

`mysql_stmt_num_rows()` 返回一个 `my_ulonglong` 值；有关打印此类型值的注意事项，请参见第 G.2.1 节“标量数据类型”。

- **签名：**
    - `int mysql_stmt_store_result (MYSQL_STMT *stmt);`

通常，执行预编译语句生成的结果集是未缓冲的，调用 `mysql_stmt_fetch()` 会逐行从服务器获取行。在执行语句之后、获取结果集之前调用 `mysql_stmt_store_result()` 会导致结果被检索并缓存在客户端内存中；因此，对 `mysql_stmt_fetch()` 的调用将从缓冲结果中返回行。调用 `mysql_stmt_store_result()` 还使结果集变得“可定位”，并使你可以使用 `mysql_stmt_data_seek()`、`mysql_stmt_row_seek()` 和 `mysql_stmt_row_tell()`。这些函数通过定位缓存在客户端内存中的结果集的行列位置来工作。

出于性能原因，结果集元数据中每列的 max_length 值默认不会计算。如果你希望在调用 `mysql_stmt_store_result()` 时计算此值，请使用 `mysql_stmt_set_attr()` 函数启用语句句柄的 `STMT_UPDATE_MAX_LENGTH_FLAG` 属性。

你可以调用 `mysql_stmt_fetch()` 获取结果集的行，而无需先调用 `mysql_stmt_store_result()`。在这种情况下，行将逐个从服务器检索。

在执行不产生结果集的语句后调用 `mysql_stmt_store_result()` 没有效果。

- **签名：**
    - `MYSQL_ROW_OFFSET mysql_stmt_row_seek (MYSQL_STMT *stmt, MYSQL_ROW_OFFSET offset);`

定位到结果集的特定行。`mysql_stmt_row_seek()` 类似于 `mysql_stmt_data_seek()`，但偏移量值不是行号。`offset` 是一个 `MYSQL_ROW_OFFSET` 值，必须从调用 `mysql_stmt_row_tell()` 或 `mysql_stmt_row_seek()` 获取，或者为零以定位到第一行。

`mysql_stmt_row_seek()` 要求整个结果集已检索到客户端内存中，因此只有在你执行语句后调用了 `mysql_stmt_store_result()` 的情况下才能使用它。

- **签名：**
    - `MYSQL_ROW_OFFSET mysql_stmt_row_tell (MYSQL_STMT *stmt);`

返回表示结果集中当前行位置的偏移量。这不是行号；该值只能传递给 `mysql_stmt_row_seek()`，不能传递给 `mysql_stmt_data_seek()`。

`mysql_stmt_row_tell()` 要求整个结果集已检索到客户端内存中，因此只有在你执行语句后调用了 `mysql_stmt_store_result()` 的情况下才能使用它。

## G.3.10 管理例程

本节中的函数使你可以控制服务器操作的各个方面。

- **签名：**
    - `int mysql_refresh (MYSQL *conn, unsigned int options);`

此函数的效果类似于 `SQL` **FLUSH** 和 **RESET** 语句，除了你可以告诉服务器同时刷新多种类型的内容。`mysql_refresh()` 成功时返回零，失败时返回非零值。

`options` 值应由以下列表中显示的一个或多个值组成。你必须有 **RELOAD** 权限才能执行这些操作。

- **REFRESH_GRANT**

重新加载授权表内容。这等效于发出 **FLUSH PRIVILEGES** 语句。

- **REFRESH_HOSTS**

刷新主机缓存。这等效于发出 **FLUSH HOSTS** 语句。

