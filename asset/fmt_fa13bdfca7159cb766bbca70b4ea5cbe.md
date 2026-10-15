
注意，我们已经将连接、结果以及 `mysql_fetch_row` 返回的行信息全部设为全局变量，以简化示例。在生产代码中，我们不建议这样做。

这里是我们打印数据的简单例程：

```
void display_row() {
    unsigned int field_count;

    field_count = 0;
    while (field_count < mysql_field_count(&my_connection)) {
        printf("%s ", sqlrow[field_count]);
        field_count++;
    }
    printf("\n");
}
```

将它附加到 `select2.c` 中，并添加声明和函数调用：

```
void display_row();

int main(int argc, char *argv[]) {
    int res;

    mysql_init(&my_connection);
    if (mysql_real_connect(&my_connection, "localhost", "rick",
        "bar", "rick", 0, NULL, 0)) {
    printf("Connection success!\n");

    res = mysql_query(&my_connection, "SELECT childno, fname,\n        age FROM CHILDREN WHERE age > 5");

    if (res) {
        printf("SELECT error: %s\n", mysql_error(&my_connection));
    } else {
        res_ptr = mysql_use_result(&my_connection);
        if (res_ptr) {
            while (sqlrow = mysql_fetch_row(res_ptr)) {
                printf("Fetched data...\n");
                display_row();
            }
        }
    }
}
```

# 第 5 章

现在将完成的产品保存为 `select3.c`。最后，如下如下编译并运行 `select3`：

```
gcc -I/usr/include/mysql select3.c -L/usr/lib/mysql -lmysqlclient -o select3
./select3
```

Connection success

Fetched data...

jenny 14

Fetched data...

andrew 10

Fetched data...

Alex 11

嗯，这说明它正在工作，尽管格式非常基础。我们还没有考虑到结果中的值。例如，如果我们想以表格的形式显示输出，我们需要以更结构化的形式同时获取数据以及关于数据的信息。我们该如何做呢？

与其使用定义为 `char` 的行对象（如果 `mysql_fetch_row` 直接返回），我们可以一次一个字段地将信息抓取到一个包含数据和元数据（关于返回数据的信息）的结构体中。这是通过 `mysql_fetch_field` 函数实现的：

```
MYSQL_FIELD *mysql_fetch_field(MYSQL_RES *result);
```

你需要反复调用它来逐个遍历字段。当没有更多字段需要处理时，将返回 `NULL`。返回的字段结构指针可用于访问存储在字段结构中关于列的各种信息。这些定义在 `mysql.h` 中：

| MYSQL FIELD 结构中的字段 | 含义 |
|---|---|
| `char *name;` | 列名，字符串格式。 |
| `char *table;` | 字段所属的表名。当你在查询多个表时，这通常更有用。注意对于计算值，因为 `MAX` 将有值。 |
| `char *def;` | 默认值。 |
| `enum field_types type;` | 类型。 |
| `unsigned int length;` | 长度。 |
| `unsigned int max_length;` | 最大长度。 |
| `unsigned int offset;` | 偏移量。 |
| `unsigned int precision;` | 精度。 |
| `unsigned int scale;` | 标点数。 |
| `unsigned int flags;` | 标志位。 |
| `unsigned int decimals;` | 十进制位数。 |
| `char *comment;` | 注释。 |
| `char *enum;` | 。 |

## MySQL

| MySQL 标志 | 含义 |
|---|---|
| `unsigned int flags;` | 标志位。这些标志关于列的定义，当你使用 `store_result` 时会设置。 |
| `enum field_types type;` | 类型非常多。常见的有： |
|  | - `FIELD_TYPE_DECIMAL` |
|  | - `FIELD_TYPE_LONG` |
|  | - `FIELD_TYPE_STRING` |
|  | - `FIELD_TYPE_VAR_STRING` |

一个特别有用的宏定义为 `IS_NUM`，如果字段类型是数值，则返回真，像这样：

```
if (IS_NUM(field_ptr->type)) printf("Numeric type\n");
```

在我们更新程序之前，我们应该提到一个函数：

```
MYSQL_FIELD *offset
MYSQL_RES *result;
```

这允许我们覆盖当前列，每次都会递增。我们现在有足够的信息来更新程序，显示所有可用内容。这并不优雅，但至少提供了信息。

还有其他函数允许获取字段数组并在列之间跳转。通常你只需要这里显示的函数，感兴趣的读者可以在 MySQL 手册找到更多信息。

## 杂函数

有一些 API 函数不属于我们目前涵盖的类别，但现在很有用。可能的情况下通过 `mysql_query` 接口操作数据库。例如，有一个用于创建数据库的 API `mysql_create_db`，但通常在 `mysql_query` 中使用 `CREATE DATABASE` 命令更容易，因为你只需要知道创建数据库的 SQL，而不是大量的专用 API 调用。

你可能需要的额外 API 调用：

| 函数 | 含义 |
|---|---|
| `mysql_get_client_info` | `char *mysql_get_client_info(void)` | 返回客户端使用的库版本信息。 |
| `mysql_get_host_info` | `char *mysql_get_host_info(MYSQL *connection);` | 返回服务器连接信息。 |
| `mysql_get_server_info` | `char *mysql_get_server_info(MYSQL *connection);` | 返回当前连接的服务器信息。 |
| `mysql_info` | `char *mysql_info(MYSQL *connection);` | 返回最近查询的信息，但仅适用于某些查询类型，通常是 INSERT 和 UPDATE 语句。否则返回 NULL。 |
| `mysql_select_db` | `int mysql_select_db(MYSQL *connection, const char *dbname);` | 将默认数据库更改为指定的数据库，前提是用户具有相应权限。成功时返回 0。 |
| `mysql_shutdown` | `int mysql_shutdown(MYSQL *connection);` | 如果你有相应权限，则关闭你连接的服务器。成功时返回 0。 |

## 资源

MySQL 的主要资源就是其主网站 http://www.mysql.com。

你可能感兴趣的书籍包括：Paul DuBois 著《MySQL》（New Riders 出，ISBN 0-7357-0921-1）以及 Randy Jay Yarger、George Reese 和 Tim King 著《MySQL & mSQL》（O'Reilly & Associates 出，ISBN 1-56592-434-7）。

## 总结

在本章，我们简要回顾了 MySQL。虽然它的功能没有 PostgreSQL那么全，但它仍然是一个非常强大的产品，拥有全面的基于 C 的 API。

我们学习了如何安装和配置基础 MySQL 数据库、一些相关的实用命令，然后查看了 C 语言的 API，这是访问 MySQL 数据库数据的多种编程语言之一。

MySQL 相比于 PostgreSQL 的主要优势在于性能。对于许多网站常见的只读访问，MySQL 的速度确实非常快。它的主要缺点是对标准 SQL 的支持较弱，并且缺乏对事务的支持。
