

等等。然后通过调用`mysql_stmt_bind_param()`将这些结构绑定到语句上。

1. 调用`mysql_stmt_execute()`来执行该语句。

2. 如果语句是修改数据而非产生结果集（例如，如果它是`INSERT`或`UPDATE`语句），则调用`mysql_stmt_affected_rows()`来确定受该语句影响的行数。

3. 如果语句会产生结果集，若要获取有关结果集的元数据，请调用`mysql_stmt_result_metadata()`。为了获取行数据，你再次使用`MYSQL_BIND`结构，但这次它们作为接收从服务器返回的数据的容器，而不是发送给服务器的数据来源。你必须为结果集中的每一列设置一个`MYSQL_BIND`结构。这些结构包含关于你期望从服务器每行接收到的值的信息。通过调用`mysql_stmt_bind_result()`将这些结构绑定到语句处理器，然后反复调用`mysql_stmt_fetch()`以获取每一行。每次获取之后，你可以访问当前行的列值。

在调用`mysql_stmt_fetch()`之前，你可以执行的一个可选操作是调用`mysql_stmt_store_result()`。如果你这样做，结果集的行将从服务器一次性获取并缓冲在客户端内存中。此外，通过调用`mysql_stmt_num_rows()`可以确定结果集中的行数，否则该函数将返回零。

获取结果集后，调用`mysql_stmt_free_result()`来释放与之相关的内存。

4. 如果你想重新执行该语句，返回到步骤 4。

5. 如果你想使用该处理器准备一个不同的语句，返回到步骤 2。

6. 当你不再需要该语句处理器时，通过调用`mysql_stmt_close()`将其销毁。如果在客户端连接关闭时，服务器仍与该连接关联有已准备的语句，服务器会自动将它们销毁。

客户端应用程序可以准备多个语句，然后按照应用程序适当的顺序逐个执行它们。

以下讨论描述如何编写一个简单的程序，该程序向表中插入一些行，然后检索它们。程序中处理`INSERT`语句的部分说明了如何在语句中使用占位符，并在执行已准备的语句时向服务器传输数据值以便绑定。处理`SELECT`语句的部分说明了如何检索通过执行已准备语句产生的结果集。你可以在sampldb发行版的capi目录中的`prepared.c`和`process_prepared_statement.c`文件中找到该程序的源代码。我不会展示连接设置的代码，因为它与早期程序的类似。

程序中使用已准备语句的主要部分看起来像这样：

```c
void
process_prepared_statements (MYSQL *conn)
{
    MYSQL_STMT *stmt;
    char         *use_stmt = "USE sampldb";
    char         *drop_stmt = "DROP TABLE IF EXISTS t";
    char         *create_stmt =
        "CREATE TABLE t (i INT, f FLOAT, c CHAR(24), dt DATETIME)";

    /* select database and create test table */
    if (mysql_query (conn, use_stmt) != 0
        || mysql_query (conn, drop_stmt) != 0
        || mysql_query (conn, create_stmt) != 0)
    {
        print_error (conn, "Could not set up test table");
        return;
    }

    stmt = mysql_stmt_init (conn);  /* allocate statement handler */
    if (stmt == NULL)
    {
        print_error (conn, "Could not initialize statement handler");
        return;
    }

    /* insert and retrieve some records */
    insert_rows (stmt);
    select_rows (stmt);

    mysql_stmt_close (stmt);        /* deallocate statement handler */
}
```

首先，我们选择一个数据库并创建一个测试表。该表包含四种不同数据类型的列：一个INT，一个FLOAT，一个CHAR，和一个DATETIME。正如我们将看到的，这些不同的数据类型需要以略有不同的方式处理。

在表创建后，我们调用`mysql_stmt_init()`来分配一个已准备语句处理器，插入和检索一些行，然后释放处理器。所有实际的工作都在`insert_rows()`和`select_rows()`函数中进行，我们将很快介绍。对于错误处理，该程序还使用了一个名为`print_stmt_error()`的函数，它类似于早期程序中使用的`print_error()`函数，但调用了专门针对已准备语句的错误函数：

```c
static void
print_stmt_error (MYSQL_STMT *stmt, char *message)
{
    fprintf (stderr, "%s\n", message);
    if (stmt != NULL)
    {
        fprintf (stderr, "Error %u (%s): %s\n",
            mysql_stmt_errno (stmt),
            mysql_stmt_sqlstate (stmt),
            mysql_stmt_error (stmt));
    }
}
```

`insert_rows()`函数负责向测试表中添加新行：

```c
static void
insert_rows (MYSQL_STMT *stmt)
{
    char           *stmt_str = "INSERT INTO t (i,f,c,d,t) VALUES (?,?,,?)";
    MYSQL_BIND   param[4];
    int            my_int;
    float          my_float;
    char           my_str[26]; /* ctime( ) returns 26-character string */
    MYSQL_TIME   my_DateTime;
    unsigned long my_str_length;
    time_t         clock;
    struct tm     *cur_time;
    int            i;

    printf ("Inserting records...\n");

    if (mysql_stmt_prepare (stmt, stmt_str, strlen (stmt_str)) != 0)
    {
        print_stmt_error (stmt, "Could not prepare INSERT statement");
        return;
    }

    /*
     * zero the parameter structures, and then perform all parameter
     * initialization that is constant and does not change for each row
     */
    memset ((void *) param, 0, sizeof (param));

    /* set up INT parameter */
    param[0].buffer_type = MYSQL_TYPE_LONG;
    param[0].buffer = (void *) &my_int;
    param[0].is_unsigned = 0;
    param[0].is_null = 0;
    /* buffer_length, length need not be set */

    /* set up FLOAT parameter */
    param[1].buffer_type = MYSQL_TYPE_FLOAT;
    param[1].buffer = (void *) &my_float;
    param[1].is_null = 0;
    /* is_unsigned, buffer_length, length need not be set */

    /* set up CHAR parameter */
    param[2].buffer_type = MYSQL_TYPE_STRING;
    param[2].buffer = (void *) my_str;
    param[2].buffer_length = sizeof( my_str);
    param[2].is_null = 0;
    /* is_unsigned need not be set, length is set later */

    /* set up DATETIME parameter */
    param[3].buffer_type = MYSQL_TYPE_DATETIME;
    param[3].buffer = (void *) &my_datetime;
    param[3].is_null = 0;
    /* is_unsigned, buffer_length, length need not be set */

    if (mysql_stmt_bind_param (stmt, param) != 0)
    {
        print_stmt_error (stmt, "Could not bind parameters for INSERT");
        return;
    }

    for (i = 1; i <= 5; i++)
    {
        printf ("Inserting record $d...\n", i);

        (void) time (&clock); /* get current time */

        /* set the variables that are associated with each parameter */

        /* param[0]: set my_int value */
        my_int = i;

        /* param[1]: set my_float value */
        my_float = (float) i;

        /* param[2]: set my_str to current ctime() string value */
        /* and set length to point to var that indicates my_str length */
        (void) strcpy (my_str, ctime (&clock));
        my_str[24] = '\0';  /* chop off trailing newline */
        my_str_length = strlen (my_str);
        param[2].length = &my_str_length;

        /* param[3]: set my_datetime to current date and time components */
        cur_time = localtime (&clock);
        my_datetime.year = cur_time->tm_year + 1900;
        my_datetime.month = cur_time->tm_mon + 1;
        my_datetime.day = cur_time->tm_mday;
        my_datetime.hour = cur_time->tm_hour;
        my_datetime.minute = cur_time->tm_min;
        my_datetime.second = cur_time->tm_sec;
        my_datetime.second_part = 0;
        my_datetime.neg = 0;

        if (mysql_stmt_execute (stmt) != 0)
        {
            print_stmt_error (stmt, "Could not execute statement");
            return;
        }

        sleep (1);  /* pause briefly (to let the time change) */
    }
}
```

`insert_rows()`的总体目的是向测试表中插入五行，每行将包含这些值：

- 一个从 1 到 5 的 INT 值。
- 一个从 1.0 到 5.0 的 FLOAT 值。
- 一个 CHAR 值。为了生成这些值，我们将调用`ctime()`系统函数来获取“当前”时间的字符串值。`ctime()`返回具有此格式的值：`Sun Sep 19 16:47:23 CDT 2004`
- 一个 DATETIME 值。这也将是“当前”时间的值，但存储在一个 MYSQL_TIME 结构中。二进制协议使用 MYSQL_TIME 结构来传输 DATETIME、TIMESTAMP、DATE 和 TIME 值。

