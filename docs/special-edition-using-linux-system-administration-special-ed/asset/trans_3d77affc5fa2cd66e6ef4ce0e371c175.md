

```
sort_buffer              | 2097144
table_cache              | 64
thread_stack             | 65536
tmp_table_size           | 1048576
tmpdir                   | /tmp/
version                  | 3.22.30
wait_timeout             | 28800
```

最后，你可以使用 `mysqlshow` 命令做进一步测试，以显示现有的数据库、表和记录。例如，要显示现有表的列表，可直接使用不带任何参数的命令：

```
# /usr/local/bin/mysqlshow
+-----------+
| Databases |
+-----------+
| mysql     |
| test      |
+-----------+
```

## 设置 root 密码

当初始授权表安装完成后，root 用户没有密码。这是一个巨大的安全漏洞，因为任何拥有 shell 访问权限的用户都可以作为 root 数据库用户使用 MySQL 服务器。在确认服务器正常运行后，你的首要任务就是设置 root 密码。

为此，请使用 `mysqladmin` 命令：

```
# /usr/local/bin/mysqladmin -u root password <new password>
```

设置密码后，大多数操作都需要指定用户名和密码。例如，上面用到的 `mysqladmin version` 命令现在需要这样执行：

```
# /usr/local/bin/mysqladmin -u root --password=<password> version
```

## 编辑配置文件

你可以使用选项文件为所有 MySQL 应用程序（如 `mysqladmin`、`mysql` 或 `mysqld`）指定默认启动选项。可以创建三个可能的选项文件：

-   `/etc/my.cnf`
-   `/usr/local/var/my.cnf`
-   `~/.my.cnf`

MySQL 应用程序将按此顺序读取这些文件，后面选项文件中的设置始终优先于前面的文件。

选项文件由一系列一般形式的节组成：

```
    [<section name>]
    <option entry>
    <option entry>
    <option entry>
    etc.
```

节名称通常是将应用选项条目的应用程序名称，因此一个典型的选项文件可能采用以下形式：

```
[mysqld]
<option entry>
<option entry>
<option entry>
etc.
```

```
[mysqladmin]
<option entry>
<option entry>
<option entry>
etc.
```

```
[mysql]
<option entry>
<option entry>
<option entry>
etc.
```

选项条目反映了可以在命令行中发出的可能的长选项。对于任何命令，你都可以使用该命令的 `--help` 选项获取可能的选项列表：

```
# /usr/local/bin/mysqladmin --help
/usr/local/bin/mysqladmin  Ver 7.15 Distrib 3.22.30, for pc-linux-gnu on i686
TCX Datakonsult AB, by Monty
This software comes with NO WARRANTY: see the file PUBLIC for details.

Administer program for the mysqld daemon
Usage: bin/mysqladmin [OPTIONS] command....

  -#, --debug=...        Output debug log. Often this is `d:t:o,filename`
  -f, --force            Don't ask for confirmation on drop database; with
                        multiple commands, continue even if an error occurs
  -?, --help             Display this help and exit
  -C, --compress         Use compression in server/client protocol
  -h, --host=#           Connect to host
  -p, --password[=...]   Password to use when connecting to server
                        If password is not given it's asked from the tty
  -P, --port=...         Port number to use for connection
  -i, --sleep=sec        Execute commands again and again with a sleep between
  -r, --relative        Show difference between current and previous values
                        when used with -i. Currently works only with
                        extended-status
  -s, --silent           Silently exit if one can't connect to server
  -S, --socket=...       Socket file to use for connection
  -t, --timeout=...      Timeout for connection to the mysqld server
  -u, --user=#           User for login if not current user
  -V, --version          Output version information and exit
  -w, --wait[=retries]   Wait and retry if connection is down

Where command is one or more of: (Commands may be shortened)
    create database        Create a new database
    drop database          Delete a database and all its tables
    extended-status         Gives an extended status message from the server
    flush-hosts             Flush all cached hosts
    flush-logs              Flush all logs
    flush-status            Clear status variables
    flush-tables            Flush all tables
    flush-privileges        Reload grant tables (same as reload)
    kill id,id,...          Kill mysql threads
    password new-password   Change old password to new-password
    ping                    Check if mysqld is alive
    processlist              Show list of active threads in server
    reload                  Reload grant tables
    refresh                 Flush all tables and close and open logfiles
    shutdown                Take server down
    status                  Gives a short status message from the server
    variables               Prints variables available
    version                 Get version info from server

Default options are read from the following files in the given order:
/etc/my.cnf -> ~/.my.cnf
The following groups are read: mysqld, mysqladmin, client
The following options may be given as the first argument:
--print-defaults             Print the program argument list and exit
--no-defaults                Don't read default options from any options file
--defaults-file=#            Only read default options from the given file #
```

长选项是指以两个破折号开头的选项，例如 `--compress` 或 `--port=<port>`。

这些选项在选项文件中采用了略有不同的形式，如表 24.3 所示。

**表 24.3 选项文件中的选项**

| 命令行格式 | 选项文件格式 |
|---|---|
| `--<option>` | `<option>` |
| `--<option>=<value>` | `<option>=<value>` |
| `--set-variable`<br>`<variable>=<value>` | `set-variable=<variable>=<value>` |

例如，在 `/etc/my.cnf` 或 `/usr/local/var/my.cnf` 中的典型全局选项文件可能如下所示：

```
[client]
port=3306
socket=/tmp/mysql.sock

[mysqld]
port=3306
socket=/tmp/mysql.sock
set-variable = max_allowed_packet=1M

[mysqldump]
quick
```

**注意：** client 节适用于多个应用程序，包括 `mysql`、`mysqladmin` 和 `mysqldump`。

请注意这三种选项类型的使用：无值的选项、有值的选项以及设置为默认值的变量。

`mysql` 客户端、`mysqld` 和 `mysqladmin` 的常用选项如表 24.4 所示。

### 表 24.4 `mysql`、`mysqld` 和 `mysqladmin` 的常用选项

| 选项 | 应用程序 | 描述 |
|---|---|---|
| `--basedir=<directory>` | `mysqld` | 使用指定路径作为安装目录。 |
| `--bind-address=<IP address>` | `mysqld` | 在具有多个 IP 地址的系统上绑定到指定地址。 |
| `--compress` | `mysql`, `mysqladmin` | 在客户端/服务器协议中使用压缩。 |
| `--database=<database>` | `mysql` | 连接到服务器上指定的数据库。 |
| `--datadir=<directory>` | `mysqld` | 使用指定路径作为数据库和日志文件目录。 |
| `--execute=<command>` | `mysql` | 执行指定命令然后退出。 |
| `--force` | `mysql`, `mysqladmin` | 删除数据库时不要请求确认。 |
| `--host=<host>` | `mysql`, `mysqladmin` | 连接到指定的主机。 |
| `--html` | `mysql` | 生成 HTML 输出。 |
| `--log=<file>` | `mysqld` | 将错误记录到指定文件。 |
| `--password` | `mysql`, `mysqladmin` | 提示输入密码。 |
| `--password=<password>` | `mysql`, `mysqladmin` | 使用指定的密码。 |
| `--port=<port>` | `mysqld`, `mysql`, `mysqladmin` | 使用指定端口连接到服务器。 |
| `--skip-name-resolve` | `mysqld` | 不解析主机名。 |
| `--skip-networking` | `mysqld` | 不启用通过 TCP/IP 的连接。 |

