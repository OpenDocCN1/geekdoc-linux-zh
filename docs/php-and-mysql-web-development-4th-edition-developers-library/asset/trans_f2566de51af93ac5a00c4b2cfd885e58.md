
## 7.6 编写包含 SSL 支持的客户程序

用户希望建立 SSL 连接。请通过调用 `mysql_ssl_set()` 来实现，且该调用需位于 `mysql_init()` 之后、`mysql_real_connect()` 之前。调用顺序如下所示：

```c
/* initialize connection handler */
conn = mysql_init (NULL);
if (conn == NULL)
{
    print_error (NULL, 'mysql_init() failed (probably out of memory)');
    exit (1);
}

#define HAVE_OPENSSL
/* pass SSL information to client library */
if (opt_use_ssl)
    mysql_ssl_set (conn, opt_ssl_key, opt_ssl_cert, opt_ssl_ca,
                   opt_ssl_capath, opt_ssl_cipher);
#if (MYSQL_VERSION_ID >= 50023 && MYSQL_VERSION_ID < 50100) \
    || MYSQL_VERSION_ID >= 50111
    mysql_options (conn,MYSQL_OPT_SSL_VERIFY_SERVER_CERT,
                   (char*)&opt_ssl_verify_server_cert);
#endif
#endif

/* connect to server */
if (mysql_real_connect (conn, opt_host_name, opt_user_name, opt_password,
                opt_db_name, opt_port_num, opt_socket_name, opt_flags) == NULL)
{
    print_error (conn, 'mysql_real_connect() failed');
    mysql_close (conn);
    exit (1);
}
```

此代码并未测试 `mysql_ssl_set()` 是否返回错误。如果您提供给该函数的信息存在问题，将在调用 `mysql_real_connect()` 时导致错误。用于确定是否调用 `mysql_options()` 的复杂测试反映了 `MYSQL_OPT_SSL_VERIFY_SERVER_CERT` 的添加：该特性在 MySQL 5.0 中始于版本 5.0.23，在 MySQL 5.1 中始于版本 5.1.11。

编译 `exec_stmt_ssl.c` 以生成 `exec_stmt_ssl` 程序，然后运行它。假设 `mysql_real_connect()` 调用成功，您可以继续执行语句。如果您使用适当的 SSL 选项调用 `exec_stmt_ssl`，与服务器之间的通信应通过加密连接进行。为了确定是否如此，请执行以下语句：

```sql
SHOW STATUS LIKE 'Ssl_cipher'
```

如果正在使用加密算法，`ssl_cipher` 的值将非空。（为了方便起见，示例发行版中包含的 `exec_stmt_ssl` 版本实际上会为您执行该语句并报告结果。）

## 7.7 使用嵌入式服务器库

MySQL 包含一个嵌入式服务器库，`libmysql`（它以可链接到应用程序中的形式包含 MySQL 服务器）。这使您能够创建基于 MySQL 的独立应用程序，而非通过网络连接到独立服务器程序的客户应用程序。

要编写嵌入式服务器应用程序，必须满足两个要求。首先，必须安装嵌入式服务器库：

- 如果您是从源代码构建，请在运行 `configure` 时使用 `--with-embedded-server` 选项来启用该库。这对 MySQL 5.0 和 5.1 同样适用。
- 如果您想使用二进制发行版，必须使用 MySQL 5.1，因为 5.0 的二进制发行版不包含 `libmysql`。5.1 的当前版本包含 `libmysql`。然而，如果您使用 RPM 包，请注意有一个单独的“embedded”（嵌入式）RPM 包，必须安装它以支持 `libmysql`。

其次，您需要在应用程序中包含少量代码来启动和关闭服务器。

在确保满足这两个要求之后，只需编译应用程序并链接嵌入式服务器库（`-lmysql`），而不是常规客户端库（`-lmysqlclient`）。该服务器库的设计使得，如果您编写了一个使用它的应用程序，只需链接适当的库，就可以轻松生成该应用程序的嵌入式版本或客户/服务器版本。之所以可行，是因为常规客户端库包含用于执行初始化和终结的接口函数，这些函数适用于客户/服务器通信，而不适用于与嵌入式服务器的通信。

### 7.7.1 编写嵌入式服务器应用程序

编写使用嵌入式服务器的应用程序与编写在客户/服务器环境中运行的应用程序差别不大。事实上，如果您从一个编写为客户/服务器应用程序的程序开始，您可以轻松将其转换为使用嵌入式服务器。以下程序描述了如何从 `exec_stmt.c` 开始生成一个名为 emapp 的嵌入式应用程序：

- 1. 将 `exec_stmt.c` 复制到 `emapp.c`。后续步骤适用于 `emapp.c`。（之所以从 `exec_stmt.c` 而不是 `exec_stmt_ssl.c` 开始，是因为在单个应用程序内部建立的连接不需要使用 SSL。）
- 2. 将 `mysql_embed.h` 添加到程序使用的 MySQL 头文件列表中：

```c
#include <my_global.h>
#include <mysys.h>
```

```c
#include <m_string.h>   /* for strdup() */
#include <mysql.h>
#include <mysql_embed.h>
#include <my_getopt.h>
```

- 3. 嵌入式应用程序既包含客户端部分，也包含服务器端部分，因此它可以处理一组用于客户端的选项，另一组用于服务器。例如，名为 embapp 的应用程序可能从选项文件中读取 [client] 和 [embapp] 组用于客户端部分。为此，请修改 client_groups 数组的定义，使其看起来像这样：

```c
static const char *client_groups[] =
{
  "client", "embapp", NULL
};
```

这些组中的选项可以按照常规方式由 load_defaults() 和 handle_options() 处理。然后定义另一组选项组列表供服务器端使用。按照惯例，此列表应包含 [server] 和 [embedded] 组，以及 [appname_server] 组，其中 appname 是您的应用程序名称。对于名为 embapp 的程序，特定于应用程序的组将是 [embapp_server]，因此组名称列表声明如下：

```c
static const char *server_groups[] =
{
  "server", "embedded", "embapp_server", NULL
};
```

- 4. 在启动与服务器的通信之前调用 mysql_library_init()，修改该调用以传递任何需要由服务器处理的选项。一个好的位置是在调用 mysql_init() 之前。
- 5. 在使用完服务器之后调用 mysql_library_end()。一个好的位置是在调用 mysql_close() 之后。

进行这些更改后，embapp.c 中的 main() 函数看起来像这样：

```c
int
main (int argc, char *argv[])
{
int opt_err;

MY_INIT (argv[0]);
load_defaults ('my', client_groups, &argc, &argv);

if ((opt_err = handle_options (&argc, &argv, my_opts, get_one_option)))
exit (opt_err);

/* solicit password if necessary */
if (ask_password) 
    opt_password = get_tty_password (NULL);

/* get database name if present on command line */
if (argc > 0)
{
    opt_db_name = argv[0];
    --argc; **argv;
}

/* initialize embedded server library */
if (mysql_library_init (0, NULL, (char **) server_groups))
{
    print_error (NULL, "mysql_library_init() failed");
    exit (1);
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

while (1)
{
    char  buff[10000];

    fprintf (stderr, "query> ");       /* print prompt */
    if (fgets (buf, sizeof (buf), stdin) == NULL) /* read statement */
        break;
    if (strcmp (buf, "quit\n") == 0 || strcmp (buf, "\\q\n") == 0)
        break;
    process_statement (conn, buf);      /* execute it */
}

/* disconnect from server */
mysql_close (conn);
/* shut down embedded server library */
mysql_library_end ();
exit (0);
```

### 7.7.2 生成应用程序可执行二进制文件

要为 embapp 生成嵌入式服务器可执行二进制文件，请链接 `-lmysql-d` 库，而不是 `-lmysqlclient` 库。`mysql_config` 实用程序在这里很有用。正如它可以显示链接常规客户端库时要使用的标志一样，它也可以显示嵌入式服务器所需的标志：

```bash
% mysql_config --libmysql-d-libs
-L'/usr/local/mysql/lib/mysql' -lmysql-d-lz-lm
```

因此，要生成 embapp 的嵌入式版本，请使用类似以下的命令：

```bash
% gcc -c -o'mysql_config --include' embapp.c
% gcc -o embapp embapp.o '`mysql_config --libmysql-d-libs`'
```

> 注意
> 
> 在这些命令中，您可能需要使用 C++ 编译器（如 `g++`），而不是 C 编译器。

此时，您拥有一个包含访问 MySQL 数据库所需所有内容 的嵌入式应用程序。但是，请确保在运行 embapp 时，它不要尝试使用与同一机器上可能已经运行的任何独立服务器相同的数据目录。

此外，在 Unix 下，应用程序必须以能够访问数据目录的权限运行。您可以以拥有数据目录的用户身份登录并运行 embapp，或者将其设置为 setuid 程序，使其在启动时将用户 ID 更改为该用户。例如，要设置 embapp 以名为 `mysql` 的用户权限运行，请以 root 身份执行以下命令：

```bash
# chown mysql embapp
# chmod 4755 embapp
```

或者，让嵌入式应用程序使用不同的数据目录。您可以将 `datadir` 选项放在选项文件的 `[embapp_server]` 组中来指定位置。（这是应用程序服务器半部分的选项组。）

如果您决定想要生成一个在客户/服务器环境中操作的、非嵌入式版本的应用程序，请将其链接到常规客户端库。您可以像这样构建它来实现：

```bash
% gcc -c -o'mysql_config --include' embapp.c
% gcc -o embapp embapp.o '`mysql_config --libs`'
```

