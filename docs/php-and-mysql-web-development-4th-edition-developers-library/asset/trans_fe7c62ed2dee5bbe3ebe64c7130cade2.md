
到不支持 MySQL 4.1 中实现的更安全密码哈希算法的服务器。

-   `MYSQL_SET_CHARSET_DIR`
    指定字符集文件所在目录的路径名。`arg` 应指向一个包含目录路径名的以 null 结尾的字符串。该目录位于客户端主机上；此选项在客户端需要访问未编译到客户端库中但有定义文件可用的字符集时使用。

-   `MYSQL_SET_CHARSET_NAME`
    指明要使用的默认字符集的名称。`arg` 应指向一个包含字符集名称的以 null 结尾的字符串。

-   `MYSQL_SHARED_MEMORY_BASE_NAME`
    指明用于共享内存连接的共享内存名称。`arg` 应指向一个包含该名称的以 null 结尾的字符串。此选项仅用于 Windows 客户端，且仅适用于启用了共享内存支持的 Windows 服务器连接。

对于使用 `MYSQL_READ_DEFAULT_FILE` 或 `MYSQL_SET_CHARSET_DIR` 选项指定的 Windows 路径名，`'\'` 字符可以表示为 `'/'` 或 `'\\'`。

如果您使用 `mysql_options()` 配合 `MYSQL_READ_DEFAULT_FILE` 或 `MYSQL_READ_DEFAULT_GROUP` 选项，使 `mysql_real_connect()` 读取选项文件，则识别以下选项：

```
character-sets-dir=charset_directory_path
compress
connect-timeout=seconds
database=db_name
debug
default-character-set=charset_name
disable-local-infile
host=host_name
init-command=stmt
interactive-timeout=seconds
local-infile[={0|1}]
max-allowed-packet=size
multi-queries
multi-results
multi-statements
password=your_pass
pipe
port=port_num
protocol=protocol_type
report-data-truncation
return-found-rows
secure-auth
shared-memory-base-name=name
socket=socket_name
ssl-ca=file_name
ssl-capath=dir_name
ssl-cert=file_name
ssl-cipher=str
ssl-key=file_name
timeout=seconds
user=user_name
```

如果在选项文件中发现 host、user、password、database、port 或 socket 选项的实例，且 `mysql_real_connect()` 对应的参数非 NULL，则这些实例会被覆盖。

`multi-results` 选项等同于在 `mysql_real_connect()` 的 flags 参数中传递 `CLIENT_MULTI_RESULTS`。`multi-queries` 或 `multi-statements` 等同于在 `mysql_real_connect()` 的 flags 参数中传递 `CLIENT_MULTI_STATEMENTS`（这也启用了 `CLIENT_MULTI_RESULTS`）。`timeout` 被识别但已废弃；请改用 `connect-timeout`。

以下示例中 `mysql_options()` 调用的效果是设置连接选项，使得 `mysql_real_connect()` 从 [client] 和 [mygroup] 组中读取 `C:/my.ini.extra` 的信息，使用命名管道和 10 秒的超时间连接，并在建立连接后执行 `SET NAMES 'utf8'` 语句。

```c
MYSQL *conn;
unsigned int timeout;

if ((conn = mysql_init (NULL)) == NULL)
   ... deal with error ...

mysql_options (conn, MYSQL_READ_DEFAULT_FILE, "C:/my.ini.extra");
mysql_options (conn, MYSQL_READ_DEFAULT_GROUP, "mygroup");
mysql_options (conn, MYSQL_OPT_NAMED_PIPE, NULL);
timeout = 10;
mysql_options (conn, MYSQL_OPT_CONNECT_TIMEOUT, (char *) &timeout);
mysql_options (conn, MYSQL_INIT_COMMAND, "SET NAMES 'utf8'");
if (mysql_real_connect (conn, ...) == NULL)
   ... deal with error ...
```

```
int
mysql_ping (MYSQL *conn);
```

检查由 conn 指示的连接是否仍然有效。如果不是，且自动重连未被禁用，mysql_ping() 将使用最初建立连接时使用的相同参数重新连接。因此，您不应在未首先成功调用 mysql_real_connect() 的情况下调用 mysql_ping()。如果连接有效或成功重建，返回零；如果发生错误，返回非零值。

```
MYSQL *
mysql_real_connect (MYSQL *conn,
const char *host_name,
const char *user_name,
const char *password,
const char *db_name,
unsigned int port_num,
const char *socket_name,
unsigned long flags);
```

连接到服务器并返回指向连接处理器的指针。conn 应该是指向已通过 mysql_init() 初始化的现有连接处理器的指针。返回值是成功连接时处理器的地址，或发生错误时为 NULL。

如果连接尝试失败，您可以将 conn 处理器值传递给 mysql_errno() 和 mysql_error() 以获取错误信息。但是，您不应将 conn 值传递给任何假设连接已成功建立的其他客户端库例程。

其余参数指示如何连接到服务器。对于指定为 NULL 或零的参数，其值可以由 mysql_real_connect() 读取的选项文件中的选项提供。客户端可以通过使用 MYSQL_READ_DEFAULT_FILE 或 MYSQL_READ_DEFAULT_GROUP 选项调用 mysql_options() 来使 mysql_real_connect() 读取选项文件。

host_name 指示 MySQL 服务器主机的名称。表 G.6 显示了针对 Unix 和 Windows 客户端的各种 host_name 值所使用的客户端连接协议。除非您已通过使用 MYSQL_OPT_PROTOCOL 选项调用 mysql_options() 显式指定协议，否则该表适用。名称 *localhost* 在 Unix 系统中具有特殊含义。它表示您希望使用 Unix 套接字而非 TCP/IP 连接进行连接。若要使用 TCP/IP 连接到运行在本地主机上的服务器，请传递 *127.0.0.1*（包含本地主机回环接口 IP 地址的字符串）作为 host_name 值，而不是传递字符串 *localhost*。

### 表 G.6 按服务器主机名类型划分的客户端连接协议

| 主机名 | Unix 连接 | Windows 连接 |
| :------- | :-------------- | :----------------- |
| 值    | 协议        | 协议           |
| 主机名 | 到指定主机的 TCP/IP 连接 | 到指定主机的 TCP/IP 连接 |
| IP 号| 到指定主机的 TCP/IP 连接 | 到指定主机的 TCP/IP 连接 |
| 本地主机| 到本地主机的 Unix 套接字文件连接 | 到本地主机的共享内存连接（如果可用），否则为 TCP/IP 连接 |
| 127.0.0.1| 到本地主机的 TCP/IP 连接 | 到本地主机的 TCP/IP 连接 |
| . (句点)| 不适用 | 到本地主机的命名管道连接 |
| NULL     | 到本地主机的 Unix 套接字文件连接 | 先尝试命名管道连接，失败后回退到 TCP/IP |

user_name 是您的 MySQL 用户名。如果此项为 NULL，客户端库将发送默认名称。在 Unix 下，默认值为您的登录名。在 Windows 下，如果设置了 user 环境变量，则默认值为您在该变量中指定的名称，否则为“ODBC”。

password 是您的密码。如果此项为 NULL，仅当用户授权表条目中与您用户名和连接来源主机匹配的密码为空白时，您才能连接。

db_name 是要使用的默认数据库。如果此项为 NULL，则不选择默认数据库。

port_num 是用于 TCP/IP 连接的端口号。如果此项为 0，则使用默认端口号。

socket_name 是在 Unix 下连接“localhost”时使用的 Unix 套接字文件名，或在 Windows 下命名管道连接时使用的管道名称。如果此项为 NULL，则使用默认的套接字或管道名称。

端口号和套接字文件名根据 host_name 的值使用，如表 G.6 中所述。

flags 值可以是以下列表中显示的一个或多个值，或为 0 以指定无选项。这些选项影响服务器的操作。

-   CLIENT_COMPRESS
-   CLIENT_FOUND_ROWS
    指定对于 UPDATE 语句，服务器应返回匹配的行数而非更改的行数。使用此选项可能会阻碍 MySQL 优化器并使更新变慢。
-   CLIENT_IGNORE_SIGPIPE
    防止客户端库安装 SIGPIPE 信号的处理程序。这对于安装自身处理程序的应用程序可能很有用。
-   CLIENT_IGNORE_SPACE
    通常，内置函数的名称必须立即跟随开始参数列表的括号，中间没有空格。此选项告诉服务器允许在函数名称和参数列表之间存在空格，这也具有将所有函数名称变为保留字的效果。
-   CLIENT_INTERACTIVE
    将客户端标识为交互式客户端。这告诉服务器可以在客户端处于非活动状态一段时间后关闭连接，该时间等于服务器的 interactive_timeout 变量值。通常，wait_timeout 变量的值被使用。
-   CLIENT_LOCAL_FILES
    启用 LOAD DATA LOCAL 的使用。如果服务器已配置为始终不允许 LOAD DATA LOCAL，这将无效。
-   CLIENT_MULTI_RESULTS
    启用使用 mysql_more_results() 和 mysql_next_result() 函数获取多个结果集。如果程序使用 CALL 语句调用返回结果集的任何存储过程，则必须指定此选项。否则，将发生错误。
-   CLIENT_MULTI_STATEMENTS
    启用多语句执行。当此功能开启时，您可以在单个字符串中向服务器发送多条语句。此选项还启用 CLIENT_MULTI_RESULTS，以便可以获取多个结果集。
-   CLIENT_NO_SCHEMA
    禁止使用 db_name.tbl_name.col_name 语法。如果指定此选项，服务器仅允许在语句中使用 tbl_name.col_name、tbl_name 或 col_name 形式的引用。

标志值是位值，因此您可以使用 | 或 + 运算符以加法方式将它们组合。例如，以下表达式是等效的：

```
CLIENT_COMPRESS | CLIENT_ODBC
CLIENT_COMPRESS + CLIENT_ODBC
```

