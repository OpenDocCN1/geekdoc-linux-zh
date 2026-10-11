
反斜杠。这一点在第 7.4.7.1 节“处理包含特殊字符的字符串”中进行了讨论。

语句处理的一个简单大纲如下：

```c
if (mysql_query (conn, stmt_str) != 0)
{
    /* 失败；报告错误 */
}
else
{
    /* 成功；查明语句产生的效果 */
}
```

`mysql_query()` 和 `mysql_real_query()` 对于成功的语句返回零，对于失败的语句返回非零值。称某个语句“成功”意味着服务器接受该语句为合法并能够执行它。这并不指示该语句所产生的任何效果。例如，它并不表示 `SELECT` 语句选择了任何行，或者 `DELETE` 语句删除了任何行。检查语句实际产生的效果涉及额外的处理过程。

语句可能因多种原因失败。失败的常见原因包括：

-   它包含语法错误。
-   它在语义上是非法的——例如，引用不存在表的语句。
-   你没有足够的权限来访问语句引用的表。

语句可以分为两大类：修改行的语句和返回结果集（一组行）的语句。诸如 `INSERT`、`DELETE` 和 `UPDATE` 等语句会修改行，并返回一个计数以指示受影响的行数。

诸如 `SELECT` 和 `SHOW` 等语句返回结果集。在 MySQL C API 中，此类语句返回的结果集由 `MYSQL_RES` 数据类型表示。在 MySQL C API 中，有一个结构体包含行的数据值，以及关于这些值的信息（如列名和数据值长度）。结果集为空（即包含零行）是合法的。

## 7.4.1 处理修改行的语句

要处理修改行的语句，请使用 `mysql_query()` 或 `mysql_real_query()` 发出该语句。如果语句成功，可以通过调用 `mysql_affected_rows()` 来查明插入、删除或更新了多少行。

以下示例展示了如何处理修改行的语句：

```c
if (mysql_query (conn, 'INSERT INTO my_tbl SET name = 'My Name'') == 0)
{
    print_error (conn, 'INSERT statement failed');
}
else
{
    printf("INSERT statement succeeded; number of rows affected: %lu\n",
           (unsigned long) mysql_affected_rows(conn));
}
```

请注意，`mysql_affected_rows()` 的结果在打印时被强制转换为 `unsigned long`。该函数返回 `my_ulonglong` 类型的值，但尝试直接打印该类型的值在某些系统上可能不起作用。将值强制转换为 `unsigned long` 并使用 `%lu` 打印格式可以解决此问题。同样的原则也适用于返回 `my_ulonglong` 值的任何其他函数，例如 `mysql_num_rows()` 和 `mysql_insert_id()`。如果你希望你的客户端程序能够跨不同系统移植，请记住这一点。

`mysql_affected_rows()` 返回受语句影响的行数，但“受影响行数”的含义取决于语句的类型。对于 `INSERT`、`REPLACE` 或 `DELETE`，它是插入、替换或删除的行数。对于 `UPDATE`，它是更新的行数，这意味着 MySQL 实际修改的行数。如果行的内容与要更新的内容相同，MySQL 不会更新该行。这意味着，尽管某行可能因 `UPDATE` 语句的 WHERE 子句而被选中更新，但它实际上可能并未被更改。

`UPDATE` 语句中“受影响行数”的这种含义实际上是一个有争议的点，因为有些人希望它意味着“匹配的行数”——即被选中更新的行数，即使更新操作实际上并未更改其值。如果你的应用程序需要这种含义，你可以在连接服务器时通过在 `mysql_real_connect()` 的 flag 参数中传递 `CLIENT_FOUND_ROWS` 值来请求这种行为。

## 7.4.2 处理返回结果集的语句

返回数据的语句以结果集的形式返回，该结果集在通过调用 `mysql_query()` 或 `mysql_real_query()` 发出语句后检索。重要的是要意识到，在 MySQL 中，`SELECT` 并非唯一返回行的语句。诸如 `SHOW`、`DESCRIBE`、`EXPLAIN` 和 `CHECK TABLE` 等语句也会返回行。对于所有这些语句，在发出语句后必须执行额外的行处理过程。

处理结果集涉及以下步骤：

-   1. 通过调用 `mysql_store_result()` 或 `mysql_use_result()` 生成结果集。这些函数在成功时返回 `MYSQL_RES` 指针，在失败时返回 `NULL`。稍后，我们将回顾 `mysql_store_result()` 和 `mysql_use_result()` 之间的区别，以及选择其中一个而非另一个的条件。目前，我们的示例使用 `mysql_store_result()`，它立即从服务器检索行并在客户端内存中对其进行缓冲。

-   2. 对结果集的每一行调用 `mysql_fetch_row()`。该函数返回 `MYSQL_ROW` 值，当没有更多行时返回 `NULL`。`MYSQL_ROW` 值是指向表示该行中每列值的字符串数组的指针。

# 第 7 章 使用 C 编写 MySQL 程序

你对每一行数据的处理取决于你的应用程序。例如，你可以打印列值或对它们进行某种统计计算。

-   3. 完成对结果集的处理后，调用 `mysql_free_result()` 来释放其使用的内存。如果你忽略此操作，你的应用程序将会发生内存泄漏。对于长时间运行的应用程序，正确处置结果集尤为重要。否则，你会注意到系统逐渐被消耗越来越多系统资源的过程所占满。

以下示例概述了如何处理返回结果集的语句：

```c
MYSQL_RES *res_set;

if (mysql_query (conn, "SHOW TABLES FROM sampdb") != 0)
{
    print_error (conn, "mysql_query() failed");
}
else
{
    res_set = mysql_store_result (conn); /* 生成结果集 */
    if (res_set == NULL)
    {
        print_error (conn, "mysql_store_result() failed");
    }
    else
    {
        /* 处理结果集，然后释放它 */
        process_result_set (conn, res_set);
        mysql_free_result (res_set);
    }
}
```

该示例将结果集处理的细节隐藏在另一个函数 `process_result_set()` 中，该函数我们尚未定义。通常，处理结果集的操作基于类似于这样的循环：

```c
while ((row = mysql_fetch_row (res_set)) != NULL)
{
    /* 对行内容执行某些操作 */
}
```

`mysql_fetch_row()` 返回一个 `MYSQL_ROW` 值，该值是指向值数组的指针。如果将返回值分配给名为 `row` 的变量，则可以通过 `row[i]` 访问行中的每个值，其中 `i` 的范围是从 0 到该行中列数减 1。关于 `MYSQL_ROW` 数据类型，有几个重要注意事项：

-   `MYSQL_ROW` 是指针类型，因此将该类型的变量声明为 `MYSQL_ROW *row`，而不是 `MYSQL_ROW row`。
-   所有数据类型（包括数值类型）的值在 `MYSQL_ROW` 数组中均以字符串形式返回。如果你想将某个值视为数字，必须自行转换字符串。
-   `MYSQL_ROW` 数组中的字符串以 null 结尾。但是，如果某列可以包含二进制数据，它可能包含 null 字节，因此你不应该将该值视为以 null 结尾的字符串。获取列长度以查明列值的长度。（第 7.4.6 节“使用结果集元数据”讨论了如何确定列长度。）
-   SQL NULL 值在 `MYSQL_ROW` 数组中由 C NULL 指针表示。除非你知道某列被声明为 `NOT NULL`，否则你应该始终检查该列的值是否为 `NULL`，否则你的程序可能会因尝试解引用 `NULL` 指针而崩溃。

你对每一行数据的处理取决于你的应用程序的目的。为了说明目的，我们只需将每一行打印为以制表符分隔的列值集合即可。要做到这一点，需要知道行的列值包含多少列。该信息由另一个客户端库函数 `mysql_num_fields()` 返回。

以下是 `process_result_set()` 的代码：

```c
void
process_result_set (MYSQL *conn, MYSQL_RES *res_set)
{
    MYSQL_ROW row;
    unsigned int i;

    while ((row = mysql_fetch_row (res_set)) != NULL)
    {
        for (i = 0; i < mysql_num_fields (res_set); i++)
        {
            if (i > 0)
                fputc ('\t', stdout);
            printf ("%s", row[i] != NULL ? row[i] : "NULL");
        }
        fputc ('\n', stdout);
    }
    if (mysql_errno (conn) != 0)
        print_error (conn, "mysql_fetch_row() failed");
    else
        printf ("Number of rows returned: %lu\n",
                (unsigned long) mysql_num_rows (res_set));
}
```

`process_result_set()` 以制表符分隔的格式显示每一行的内容（将 `NULL` 值显示为单词“`NULL`”），然后打印检索到的行数计数。该计数可通过调用 `mysql_num_rows()` 获得。与 `mysql_affected_rows()` 类似，`mysql_num_rows()` 也返回 `my_ulonglong` 值，因此你应该将其值强制转换为 `unsigned long` 并使用 `%lu` 格式进行打印。但请注意，与接受连接句柄参数的 `mysql_affected_rows()` 不同，`mysql_num_rows()` 接受结果集指针作为其参数。

