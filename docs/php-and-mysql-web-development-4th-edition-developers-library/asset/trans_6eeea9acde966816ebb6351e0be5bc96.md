
可以执行任意语句并显示结果的程序。以下示例展示了该程序的工作方式，包括 `SELECT` 和非 `SELECT` 语句，以及出现错误的语句：

```
$ . /exec_stmt
query> USE sampdb
Number of rows affected: 0
query> SELECT DATABASE(), USER()
+---------------------+----------------------+
| DATABASE()          | USER()               |
+---------------------+----------------------+
| sampdb              | sampadm@localhost    |
+---------------------+----------------------+
Number of rows returned: 1
query> SELECT COUNT(*) FROM president
+-------------+
| COUNT(*)    |
+-------------+
| 42          |
+-------------+
Number of rows returned: 1
query> SELECT last_name, first_name FROM president ORDER BY last_name LIMIT 3
+-----------+-----------+
| last_name | first_name|
+-----------+-----------+
| Adams     | John      |
| Adams     | John Quincy|
| Arthur    | Chester A.|
+-----------+-----------+
Number of rows returned: 3
query> CREATE TABLE t (i INT)
Number of rows affected: 0
query> SELECT j FROM t
Could not execute statement
Error 1054 (42S22): Unknown column 'j' in 'field list'
query> USE mysql
Could not execute statement
Error 1044 (42000): Access denied for user 'sampadm'@'localhost' to database 'mysql'
```

## 7.6 编写包含 SSL 支持的客户端

MySQL 包含 SSL 支持，你可以使用它来编写通过安全连接访问服务器的自己的程序。为了展示如何实现这一点，本节描述了修改 `exec_stmt` 以生成一个名为 `exec_stmt_ssl` 的类似客户端的过程。该客户端外观上与此前差不多，但允许建立加密连接。要使 `exec_stmt_ssl` 正常工作，MySQL 必须已构建 SSL 支持，并且服务器必须以标识其证书和密钥文件的正确选项启动。你还需要在客户端端拥有证书和密钥文件。有关更多信息，请参阅第 13.3 节，“设置安全连接”。

B&amp;B 发行版包含一个源文件 `exec_stmt_ssl.c`，可以从中构建客户端程序 `exec_stmt_ssl`。以下流程描述了如何从 `exec_stmt.c` 开始创建 `exec_stmt_ssl.c`：

- 将 `exec_stmt.c` 复制为 `exec_stmt_ssl.c`。后续步骤适用于 `exec_stmt_ssl.c`。

- 为了使编译器能够检测 SSL 支持是否可用，MySQL 头文件 `my_config.h` 适当定义了符号 `HAVE_OPENSSL`。这意味着在编写与 SSL 相关的代码时，你需要使用以下结构，以便在无法使用 SSL 时忽略该代码：

```
#ifdef HAVE_OPENSSL

SSL-related code here... 

#endif
```

你不需要显式包含 `my_config.h`，因为它是被 `my_global.h` 包含的，而 `exec_stmt_ssl.c` 已经包含了后者文件。

- 修改包含选项信息结构的 `my_opts` 数组，使其包含标准 SSL 相关选项（如 `--ssl-ca`、`--ssl-key` 等）的条目。最简单的方法是通过 `#include` 指令将 `sslopt-longopts.h` 文件的内容包含到 `my_opts` 数组中。做出更改后，`my_opts` 看起来像这样：

```
static struct my_option my_opts[]=  /* option information structures */
{
  {"help", '?', "Display this help and exit", 
   NULL, NULL, NULL},
  GET_NO_ARG, NO_ARG, 0, 0, 0, 0, 0, 0},
  {"host", 'h', "Host to connect to",
   (uchar **) &opt_host_name, NULL, NULL},
  GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0, 0},
  {"password", 'p', "Password", 
   (uchar **) &opt_password, NULL, NULL},
  GET_STR, OPT_ARG, 0, 0, 0, 0, 0, 0},
  {"port", 'P', "Port number", 
   (uchar **) &opt_port_num, NULL, NULL},
  GET_UINT, REQUIRED_ARG, 0, 0, 0, 0, 0, 0},
  {"socket", 'S', "Socket path", 
   (uchar **) &opt_socket_name, NULL, NULL},
  GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0, 0},
  {"user", 'u', "User_name", 
   (uchar **) &opt_user_name, NULL, NULL},
  GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0, 0},

#include <sslopt-longopts.h>

( NULL, 0, NULL, NULL, NULL, NULL, GET_NO_ARG, NO_ARG, 0, 0, 0, 0, 0, 0 )
};
```

`sslopt-longopts.h` 是一个公共的 MySQL 头文件。其内容如下（略微重新格式化）：

```
#ifdef HAVE_OPENSSL
{"ssl", OPT_SSL_SSL,
"Enable SSL for connection (automatically enabled with other flags).
Disable with --skip-ssl"},
{uchar **} oopt_use_ssl, {uchar **} oopt_use_ssl, 0,
GET_BOOL, NO_ARG, 0, 0, 0, 0, 0),
{"ssl-ca", OPT_SSL_CA,
"CA file in PEM format (check OpenSSL docs, implies --ssl)"},
{uchar **} oopt_ssl_ca, {uchar **} oopt_ssl_ca, 0,
GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0),
{"ssl-capath", OPT_SSL_CAPATH,
"CA directory (check OpenSSL docs, implies --ssl)"},
{uchar **} oopt_ssl_capath, {uchar **} oopt_ssl_capath, 0,
GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0),
{"ssl-cert", OPT_SSL_CERT, "X509 cert in PEM format (implies --ssl)"},
{uchar **} oopt_ssl_cert, {uchar **} oopt_ssl_cert, 0,
GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0),
{"ssl-cipher", OPT_SSL_CIPHER, "SSL cipher to use (implies --ssl)"},
{uchar **} oopt_ssl_cipher, {uchar **} oopt_ssl_cipher, 0,
GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0),
{"ssl-key", OPT_SSL_KEY, "X509 key in PEM format (implies --ssl)"},
{uchar **} oopt_ssl_key, {uchar **} oopt_ssl_key, 0,
GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0),
#endif MYSQL_CLIENT
{"ssl-verify-server-cert", OPT_SSL_VERIFY_SERVER_CERT,
"Verify server's \"Common Name\" in its cert against hostname used
when connecting. This option is disabled by default."},
{uchar **} oopt_ssl_verify_server_cert,
{uchar **} oopt_ssl_verify_server_cert, 0,
GET_BOOL, NO_ARG, 0, 0, 0, 0, 0),
#endif
#endif /* HAVE_OPENSSL */
```

- 由 `sslopt-longopts.h` 定义的选项结构引用了 `OPT_SSL_SSL`、`OPT_SSL_KEY` 等值。这些用于短选项代码，必须由你的程序定义，可以通过在 `my_opts` 数组定义之前添加以下行来实现：

```
#ifdef HAVE_OPENSSL
enum options_client
{
    OPT_SSL_SSL=256,
    OPT_SSL_KEY,
    OPT_SSL_CERT,
    OPT_SSL_CA,
    OPT_SSL_CAPATH,
    OPT_SSL_CIPHER,
    OPT_SSL_VERIFY_SERVER_CERT
};
#endif
```

在编写自己的应用程序时，如果某个程序也定义了其他选项的代码，请确保这些 `OPT_SSL_XXX` 符号的值与这些代码不同。

- `sslopt-longopts.h` 中与 SSL 相关的选项结构引用了一组用于存储选项值的变量。为了声明这些变量，使用 `#include` 指令将 `sslopt-vars.h` 文件的内容包含到你的程序中，放在 `my_opts` 数组定义之前。`sslopt-vars.h` 看起来像这样：

```
#ifdef HAVE_OPENSSL
static my_bool opt_use_ssl = 0;
static char *opt_ssl_ca    = 0;
static char *opt_ssl_capath = 0;
static char *opt_ssl_cert  = 0;
static char *opt_ssl_cipher = 0;
static char *opt_ssl_key    = 0;
#endif
#ifdef MYSQL_CLIENT
static my_bool opt_ssl_verify_server_cert= 0;
#endif
#endif
```

- 在 `get_one_option()` 例程中，在末尾附近添加一行，包含 `sslopt-case.h` 文件：

```
static my_bool
get_one_option (int optid, const struct my_option *opt, char *argument)
{
switch (optid)
{
case '?' :
    my_print_help (my_opts); /* print help message */
    exit (0);
case 'p': /* password */
	if (!argument) /* no value given; solicit it later */
		ask_password = 1;
	else		/* copy password, overwrite original */
	{
		opt_password = strdup (argument);

		if (opt_password == NULL)
		{
			print_error (NULL, "could not allocate password buffer");
			exit (1);
		}

		while (*argument)
			*argument++ = 'x';

		ask_password = 0;
	}
	break;
#include <sslopt-case.h>
}
return (0);
}
```

**sslopt-case.h** 为 `switch()` 语句包含了额外的分支，以检测是否提供了任何 SSL 选项，并在如此时设置 `opt_use_ssl` 变量。它看起来像这样：

```
#ifdef HAVE_OPENSSL
case OPT_SSL_KEY:
case OPT_SSL_CERT:
case OPT_SSL_CA:
case OPT_SSL_CAPATH:
case OPT_SSL_CIPHER:
/*
	Enable use of SSL if we are using any ssl option
	One can disable SSL later by using --skip-ssl or --ssl=0
*/
opt_use_ssl= 1;
break;
#endif
```

其效果是，在选项处理完成后，可以通过检查 `opt_use_ssl` 的值来确定用户是否希望使用安全连接。

如果你使用上述流程，通常的 `load_defaults()` 和 `handle_options()` 例程将自动为你解析与 SSL 相关的选项并设置它们的值。你唯一需要做的其他事情是在连接到服务器之前将 SSL 选项信息传递给客户端库，如果选项表明该

