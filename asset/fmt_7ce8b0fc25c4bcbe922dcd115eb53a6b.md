
```c
static void
print_error (MYSQL *conn, char *message)
{
    fprintf (stderr, "%s\n", message);
    if (conn != NULL)
    {
        fprintf (stderr, "Error %u [%s]: %s\n",
                 mysql_errno (conn), mysql_sqlstate (conn), mysql_error (conn));
    }
}

/* initialize connection handler */
conn = mysql_init (NULL);
if (conn == NULL)
{
    print_error (NULL, "mysql_init() failed (probably out of memory)");
    exit (1);
}

/* connect to server */
if (mysql_real_connect (conn, opt_host_name, opt_user_name, opt_password,
                       opt_db_name, opt_port_num, opt_socket_name, opt_flags) == NULL)
{
    print_error (conn, "mysql_real_connect() failed");
    mysql_close (conn);
    exit (1);
}
```

错误检查逻辑基于这样一个事实：`mysql_init()` 和 `mysql_real_connect()` 在失败时都会返回 `NULL`。请注意，如果 `mysql_init()` 失败，我们会将 `NULL` 作为参数传递给 `print_error()`。这会导致它不调用 MySQL 错误报告函数，因为传递给这些函数的连接句柄不能被假定包含任何有意义的信息。相比之下，如果 `mysql_real_connect()` 失败，我们可以将连接句柄传递给 `print_error()`。该句柄不会包含对应于有效连接的信息，但它会包含可以通过错误报告函数提取的诊断信息。此外，还可以将句柄传递给 `mysql_close()`，以释放 `mysql_init()` 可能为其自动分配的任何内存。（不过，不要将句柄传递给其他客户端例程！因为它们大多假定存在有效连接，你的程序可能会崩溃。）

本章中其余的程序都会执行错误检查，你自己的程序也应该这样做。这看起来可能增加了工作量，但从长远来看，实际上工作量更少，因为你花费在追踪细微问题上的时间更少了。在第 8 章“使用 Perl DBI 编写 MySQL 程序”和第 9 章“使用 PHP 编写 MySQL 程序”中，我也将采用这种检查错误的方法。

### 运行时指定连接参数

现在，我们准备着手处理让用户在运行时指定连接参数，而不是使用硬编码默认参数的任务。`connect1` 客户端程序存在一个显著缺点，即连接参数被直接写入源代码中。要更改这些值中的任意一个，你必须编辑源文件并重新编译它。这并不方便，特别是如果你打算让程序可供他人使用的话。在运行时指定连接参数的一种常见方法是使用命令行选项。例如，MySQL 发行版中的程序接受两种形式之一的参数，如以下表格所示。

| 参数 | 长选项形式 | 短选项形式 |
|:---|:---|:---|
| 主机名 | `--host=host_name` | `-h host_name` |
| 用户名 | `--user=user_name` | `-u user_name` |
| 密码 | `--password` 或<br>`--password=your_pass` | `-p` 或<br>`-pyour_pass` |
| 端口号 | `--port=port_num` | `-P port_num` |
| 套接字名称 | `--socket=socket_name` | `-S socket_name` |

为了与标准 MySQL 客户端保持一致，我们的 `connect2` 客户端程序将接受相同的格式。由于客户端库包含选项处理的支持，因此这很容易做到。此外，`connect2` 将具备从选项文件中提取信息的能力。这使你能够将连接参数放入 `~/.my.cnf`（即主目录下的 `.my.cnf` 文件）或任何全局选项文件中。这样，每次运行程序时就不必在命令行上指定这些选项。客户端库使得检查 MySQL 选项文件并从中获取相关值变得轻而易举。只需在程序中增加几行代码，就可以使其具备识别选项文件的能力，而无需自己编写代码重新发明轮子。（有关选项文件语法的描述，请参见 E.2.2 节“选项文件”。）

在展示 `connect2` 中选项处理的工作原理之前，我们将开发两个示例程序来说明其中涉及的一般原理。这些示例展示了选项处理是如何相当简单地工作，而没有连接 MySQL 服务器和处理语句带来的额外复杂性。

> **注意**
>
> MySQL 还提供了另外两个与建立连接相关的选项。`--protocol` 指定连接协议（TCP/IP、Unix 套接字文件等），而 `--shared-memory-base-name` 指定在 Windows 上用于共享内存连接的共享内存名称。本章不涵盖这两个选项，但 sampbd 发行版包含一个名为 `protocol1` 的程序的源代码，展示了如何使用它们（如果你感兴趣的话）。

#### 7.3.2.1 访问选项文件内容

为了读取选项文件中的连接参数值，请调用 `load_defaults()` 函数。`load_defaults()` 会查找选项文件，解析你感兴趣的各种选项组的内容，并改写你程序的参数向量（即 `argv[]` 数组）。它将这些选项组中的信息以命令行选项的形式添加到 `argv[]` 的开头。这样，这些选项看起来就像是在命令行上指定的。当解析命令行选项时，你可以在正常的选项处理代码中看到这些连接参数。这些选项被添加到 `argv[]` 中命令名称之后、其他参数之前（而不是在末尾），因此任何在命令行上指定的连接参数都会出现在 `load_defaults()` 添加的选项之后，从而覆盖它们。

下面是一个名为 `show_argv` 的小程序，演示如何使用 `load_defaults()` 并说明它是如何修改你的参数向量的：

```c
/*
 * show_argv.c - show effect of load_defaults() on argument vector
*/

#include <my_global.h>
#include <my_sys.h>
#include <mysql.h>

static const char *client_groups[] = { "client", NULL };

int
main (int argc, char *argv[])
{
 int i;

 printf ("Original argument vector:\n");
 for (i = 0; i < argc; i++)
 printf ("arg %d: %s\n", i, argv[i]);

 MY_INIT (argv[0]);
 load_defaults ("my", client_groups, &argc, &argv);

 printf ("Modified argument vector:\n");
 for (i = 0; i < argc; i++)
 printf ("arg %d: %s\n", i, argv[i]);

 exit (0);
}
```

选项文件处理代码涉及几个组成部分：

- `client_groups[]` 是一个字符字符串数组，指示你想要获取选项的选项文件组名称。客户端程序通常至少在列表中包含 `client`（代表 `[client]` 组），但你可以列出任意多的组。数组的最后一个元素必须是 `NULL`，以指示列表的结束位置。

- `MY_INIT()` 是一个初始化宏。我们之前使用过它，但这里的关键点是 `MY_INIT()` 调用 `my_init()` 执行 `load_defaults()` 所需的一些设置操作。

- `load_defaults()` 读取选项文件。它接受四个参数：选项文件名称中使用的前缀（这通常应该是 `"my"`）、列出你感兴趣的选项组名称的数组，以及你的程序参数计数和向量的地址。不要传递计数和向量的 *值*。而是传递它们的地址，因为 `load_defaults()` 需要修改它们的值。特别是，即使 `argv` 已经是一个指针，你仍然传递 `&argv`，即该指针的地址。

`show_argv` 打印其参数两次，以展示 `load_defaults()` 对参数数组的影响。首先，它打印在命令行上指定的参数。然后，它调用 `load_defaults()` 并再次打印参数数组。
