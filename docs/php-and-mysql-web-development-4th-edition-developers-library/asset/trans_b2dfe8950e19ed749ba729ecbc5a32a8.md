

标准客户端库包含 *mysql_library_init*() 和 *mysql_library_end*() 的版本，这些版本执行针对客户端/服务器通信的初始化和终结操作，而不是针对嵌入式服务器的通信。

## 7.8 使用多语句执行

MySQL 客户端库支持多语句执行功能。这使您可以向服务器发送一个由分号分隔的多个语句组成的字符串，然后依次获取结果集。

多语句执行默认未启用，因此您必须告知服务器您希望使用它。有两种方法可以做到这一点。第一种方法是在连接时，在 *mysql_real_connect*() 的 *flags* 参数中添加 *CLIENT_MULTI_STATEMENTS* 选项：

```C
opt_flags |= CLIENT_MULTI_STATEMENTS;
if (mysql_real_connect (conn, opt_host_name, opt_user_name, opt_password,
    opt_db_name, opt_port_num, opt_socket_name, opt_flags) == NULL)
{
    print_error (conn, "mysql_real_connect() failed");
    mysql_close (conn);
    exit (1);
}
```

另一种方法是使用 *mysql_set_server_option*() 为现有连接启用该功能。例如：

```C
if (mysql_set_server_option (conn, MYSQL_OPTION_MULTI_STATEMENTS_ON) != 0)
    print_error (conn, "Could not enable multiple-statement execution");
```

哪种方法更优？如果程序不使用存储过程，则两种方法都适用。如果程序使用存储过程并调用返回结果集的 CALL 语句，则第一种方法更好。这是因为 *CLIENT_MULTI_STATEMENTS* 也会开启 *CLIENT_MULTI_RESULTS* 选项，如果存储过程尝试返回结果但未启用该选项，则会发生错误。（更理想的做法可能是将 *CLIENT_MULTI_RESULTS* 添加到 *mysql_real_connect*() 的 *flags* 参数中，因为这明确表明您正在启用该选项。）

两个函数提供了在处理多个结果集时检查结果获取当前状态的基础：

- *mysql_more_results*() 如果有更多结果可用则返回非零值，否则返回零。
- *mysql_next_result*() 返回状态，如果仍有结果可用，则启动下一个结果集的获取。如果有更多结果可用，状态为零；如果没有，则为 -1；如果发生错误，则为大于零的值。

您可以将结果获取代码放入循环中，从而使用这些函数。在使用常规代码获取一个结果后，检查是否还有尚未获取的结果。如果有，则执行循环的另一次迭代。如果没有，则退出循环。根据您如何构建循环，可能根本不需要调用 `mysql_more_results()`。这是因为您也可以从 `mysql_next_result()` 的返回值判断是否还有更多结果可用。

在第 7.4.3 节“通用语句处理程序”中，我们编写了一个函数 `process_statement()`，用于执行语句并获取结果或显示受影响的行数。通过将结果获取代码放入循环并整合 `mysql_next_result()`，我们可以编写一个类似的函数 `process_multi_statement()`，它可以获取多个结果：

```C
void
process_multi_statement (MYSQL *conn, char *stmt_str)
{
  MYSQL_RES *res_set;
  int         status;
  int         keep_going = 1;

  if (mysql_query (conn, stmt_str) != 0)  /* the statement(s) failed */
  {
    print_error (conn, "Could not execute statement(s)");
    return;
  }

  /* the statement(s) succeeded; enter result-retrieval loop */
  do {
    /* determine whether current statement returned data */
    res_set = mysql_store_result (conn);
    if (res_set)          /* a result set was returned */
    {
      /* process rows and then free the result set */
      process_result_set (conn, res_set);
      mysql_free_result (res_set);
    }
    else                  /* no result set was returned */
    {
      /*
       * does the lack of a result set mean that the statement didn’t
       * return one, or that it should have but an error occurred?
       */
      if (mysql_field_count (conn) == 0)
      {
        /*
         * statement generated no result set (it was not a SELECT,
         * SHOW, DESCRIBE, etc.); just report rows-affected value.
         */
        printf ("Number of rows affected: %lu\n",
                (unsigned long) mysql_affected_rows (conn));
      }
      else /* an error occurred */
      {
        print_error (conn, "Could not retrieve result set");
        keep_going = 0;
      }
    }
    /* determine whether more results exist */
    /* 0 = yes, -1 = no, >0 = error */
    status = mysql_next_result (conn);
    if (status != 0)  /* no more results, or an error occurred */
    {
      keep_going = 0;
      if (status > 0)   /* error */
        print_error (conn, "Could not execute statement");
    }
  } while (keep_going);
}
```

如果愿意，您可以只需测试 mysql_next_result() 的结果是否为零，如果非零则退出循环。这种简单策略的缺点是，如果没有更多结果，您将无法判断是正常到达末尾还是发生了错误。换句话说，您将不知道该打印错误消息。

## 7.9 使用服务器端预编译语句

在本章前面的部分中，SQL 语句处理代码是基于 MySQL 客户端库提供的一组函数，这些函数以字符串形式发送和检索所有信息。本节讨论如何使用二进制客户端/服务器协议。二进制协议支持服务器端预编译语句，并支持以原生格式传输数据值。

并非所有语句都可以预编译。预编译语句 API 适用于以下语句：CREATE、TABLE、DELETE、DO、INSERT、REPLACE、SELECT、SET、UPDATE 以及大多数 SHOW 变体。支持的语句列表在 MySQL 5.1 中大幅扩展。请参阅 MySQL 5.1 参考手册了解当前确切的支持列表。

要使用二进制协议，必须创建语句处理程序。使用此处理程序，向服务器发送语句以进行“预编译”或预处理。服务器分析该语句，记住它，并向客户端库返回有关该语句的信息，这些信息存储在语句处理程序中。该语句的进一步处理使用此处理程序。

要预编译的语句可以通过包含 "?" 字符进行参数化，以指示稍后执行语句时将提供数据值的位置。例如，您可能会预编译一个类似这样的语句：

```SQL
INSERT INTO score (event_id, student_id, score) VALUES (?, ?, ?)
```

该语句包含三个 `'` 字符，充当参数标记或占位符。稍后，您可以提供要绑定到占位符的数据值。执行语句时，这些数据值将完成语句。通过参数化语句，使其可重用：相同的语句可以执行多次，每次使用一组新的数据值。这意味着您只需发送一次语句文本。每次执行语句时，只需发送数据值即可。对于重复执行语句，这提供了性能提升：

- 服务器只需分析一次语句，而不是每次执行时都分析。
- 减少了网络开销，因为每次执行只发送数据值，而不是整个语句。
- 数据值无需转换为字符串形式即可发送，从而减少了执行开销。例如，前面 INSERT 语句中指定的三个列均为 INT 列。如果使用 mysql_query() 或 mysql_real_query() 执行类似的 INSERT 语句，则需要将数据值转换为字符串以包含在语句文本中。使用预编译语句接口时，数据值单独以二进制格式发送。
- 获取结果时也无需转换。由预编译语句返回的结果集中，非字符串值以二进制格式返回，无需转换为字符串形式。

与原始非二进制协议相比，二进制协议也有一些缺点：

- 使用难度更大，因为传输和接收数据值需要更多的设置。
- 二进制协议不支持所有语句。例如，USE 语句不起作用。
- 对于交互式程序，最好使用原始协议。在这种情况下，从用户接收的每个语句只执行一次。使用预编译语句的好处很小，因为预编译语句为重复执行的语句提供了最大的效率提升。

使用预编译语句的一般步骤包括以下几个步骤：

1. 调用 mysql_stmt_init() 分配一个语句处理程序。该函数返回指向处理程序的指针，您在后续步骤中使用该指针。
2. 调用 mysql_stmt_prepare() 向服务器发送要预编译的语句，并将其与语句处理程序关联。服务器确定语句的某些特征，例如它是什么类型的语句、包含多少个参数标记，以及执行时是否会产生结果集。
3. 如果语句包含任何占位符，在可以执行它之前，必须为每个占位符提供数据。为此，为每个参数设置一个 MYSQL_BIND 结构。每个结构指示一个参数的数据类型、其值、是否为 NULL，

