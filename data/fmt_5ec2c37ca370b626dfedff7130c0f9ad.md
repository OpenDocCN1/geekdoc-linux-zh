
```
% mysql_config --libs
-L'/usr/local/mysql/lib/mysql' -lmysqlclient -lz -lcrypt -lnsl -lm
```

- 链接嵌入式服务器的标志：

```
% mysql_config --libmysqld-libs
-L'/usr/local/mysql/lib/mysql' -lmysqld -lz -lcrypt -lnsl -lm
```

上面显示的输出仅作为示例，但在您的系统上可能有所不同。

### G.2 C API 数据类型

MySQL C 客户端库的数据类型旨在表示您在与服务器会话过程中处理的信息类型。有用于连接本身、查询结果、结果集中的行以及元数据（关于组成结果集的列的描述性信息）的类型。在以下讨论中，“列”和“字段”是同义词。

#### G.2.1 标量数据类型

MySQL 的标量数据类型表示诸如非常大的整数、布尔值以及字段或行偏移量之类的值。

- `my_bool`

  一种布尔类型，用于 `mysql_change_user()` 和 `mysql_thread_init()` 的返回值。

- `my_ulonglong`

  一种长整型，用于返回行数或其他可能非常大的数的函数，例如 `mysql_affected_rows()`、`mysql_num_rows()` 和 `mysql_insert_id()`。要打印 `my_ulonglong` 值，请将其强制转换为 `unsigned long` 并使用 `%lu` 格式。例如：

```
printf ("Row count = %lu\n", (unsigned long) mysql_affected_rows
        (conn));
```

如果您不这样做，在某些系统上值将无法正确打印，因为使用 `printf()` 打印 long long 值没有标准。然而，如果要打印的值实际上可能超过 `unsigned long` 允许的最大值（2^32 - 1），那么强制转换也不会起作用。您需要检查您的 `printf()` 文档，看看是否有某种特定于实现的方法来打印该值。例如，可能会有 `%llu` 格式说明符可用。

- `MYSQL_FIELD_OFFSET`

  此数据类型由 `mysql_field_seek()` 和 `mysql_field_tell()` 等函数使用，用于表示当前结果集中 `MYSQL_FIELD` 结构集内的偏移量。

- `MYSQL_ROW_OFFSET`

  此数据类型由 `mysql_row_seek()` 和 `mysql_row_tell()` 等函数使用，用于表示当前结果集行集合内的偏移量。

#### G.2.2 非标量数据类型

MySQL 的非标量类型表示结构体或数组。任何 `MYSQL`、`MYSQL_RES` 或 `MYSQL_SWT` 结构的实例都应被视为“黑盒”。也就是说，您应该仅引用结构体本身，而不是引用结构体内部的成员。`MYSQL_ROW`、`MYSQL_FIELD`、`MYSQL_BIND` 和 `MYSQL_TIME` 类型没有相同的限制。这些结构体中的每一个都有成员，您可以直接访问这些成员以获取作为查询结果返回的数据和元数据。`MYSQL_BIND` 和 `MYSQL_TIME` 结构体也用于向服务器传输数据和从服务器接收结果。

- `MYSQL`

  主要的客户端库类型是 `MYSQL` 结构体，用于连接句柄。句柄包含与服务器连接状态的信息。要与服务器建立会话，请先使用 `mysql_init()` 初始化 `MYSQL` 结构体，然后将其传递给 `mysql_real_connect()`。建立连接后，使用句柄发出 SQL 语句、生成结果集、获取错误信息等。完成连接后，将句柄传递给 `mysql_close()`，之后您不应再使用它。

- `MYSQL_FIELD`

  客户端库使用 `MYSQL_FIELD` 结构体来表示结果集中列的元数据，每列一个结构体。可以通过调用 `mysql_num_fields()` 来确定该集合中 `MYSQL_FIELD` 结构体的数量。您可以通过调用 `mysql_fetch_field()` 来访问连续的字段结构体，或者使用 `mysql_field_tell()` 和 `mysql_field_seek()` 在结构体之间来回移动。

  `MYSQL_FIELD` 结构体对于呈现或解释数据行内容非常有用。它看起来像这样：

```
typedef struct st_mysql_field {
    char *name;
    char *org_name;
    char *table;
    char *org_table;
    char *db;
    char *catalog;
    char *def;
    unsigned long length;
    unsigned long max_length;
    unsigned int name_length;
    unsigned int org_name_length;
    unsigned int table_length;
    unsigned int org_table_length;
    unsigned int db_length;
    unsigned int catalog_length;
    unsigned int def_length;
    unsigned int flags;
    unsigned int decimals;
    unsigned int charsetnr;
    enum enum_field_types type;
} MYSQL_FIELD;
```

`MYSQL_FIELD` 结构体成员具有以下含义：

1. `char *name`

   列名，作为以空字符终止的字符串。对于作为表达式结果计算的列，`name` 是该表达式的字符串形式。如果列或表达式被赋予别名，则 `name` 是别名。例如，以下查询会导致 `name` 值为 `"mycol"`、`"4*(mycol+1)"`、`"mc"` 和 `"myexpr"`：

```sql
SELECT mycol, 4*(mycol+1), mycol AS mc, 4*(mycol+1) AS myexpr ...
```

2. `char *org_name`

   此成员类似于 `name`，但列别名被忽略。也就是说，`org_name` 表示原始列名。对于作为表达式结果计算的列，`org_name` 是空字符串。

3. `char *table`

   列所在的表名，作为以空字符终止的字符串。对于从视图中选择的列，`table` 是视图名称。如果表或视图被赋予别名，则 `table` 是别名。对于作为表达式结果计算的列，`table` 是空字符串。例如，如果您发出如下查询，第一列的表名是 `mytbl`，而第二列的表名是空字符串：

```sql
SELECT mycol, mycol+0 FROM mytbl ...
```

### G. MySQL C API 结构体

#### G.1 MYSQL_FIELD

- `char *org_table`

  该成员与 `table` 类似，但会忽略表别名。也就是说，`org_table` 表示原始表名。对于从视图中选择的列，`table` 是底层表名。对于作为表达式结果计算得出的列，`org_table` 是空字符串。

- `char *db`

  包含该列的表所在的数据库，作为以空字符结尾的字符串。对于作为表达式结果计算得出的列，`db` 是空字符串。

- `char *catalog`

  目录名称。目前，此值始终为 "def"。

- `char *def`

  列的默认值，作为以空字符结尾的字符串。`MYSQL_FIELD` 结构体中的此成员仅在通过调用 `mysql_list_fields()`（一个已弃用的函数）获取结果集时设置，否则为 NULL。

  也可以通过执行 `DESCRIBE tbl_name` 或 `SHOW COLUMNS FROM tbl_name` 语句并检查结果集来获取表列的默认值。

- `unsigned long length`

  列的长度，如创建表时使用的 `CREATE TABLE` 语句中指定的那样。对于作为表达式结果计算得出的列，长度由表达式中的元素决定。

- `unsigned long max_length`

  结果集中实际存在的最长列值的长度。例如，如果结果集中的字符串列包含值 "Bill"、"Jack" 和 "Belvidere"，则该列的 `max_length` 值为 9。
