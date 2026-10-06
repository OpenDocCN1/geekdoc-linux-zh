

# 第五部分 高级主题

当 Linux 系统启动时。你可以在发行版的启动脚本中创建一个链接，以引用 MySQL 启动脚本，该脚本位于：

```
/usr/local/mysql/support-files/mysql.server
```

此脚本将使用 Linux 用户账户自动启动 MySQL 服务。

# 安全 MySQL 用户账户

MySQL 服务器安装还有最后一步。MySQL 服务器维护着的一组用户账户，用于控制对数据库对象的访问。默认情况下，MySQL 服务器有一个名为 root 的主管理员。遗憾的是，该账户没有密码。更改 root 用户账户的密码是一个非常明智的主意。你可以在 Linux 命令行提示符下使用 mysqladmin 命令来执行此操作：

```
$ mysqladmin -u root password newpasswd
```

其中 newpasswd 是你为为 root 用户账户分配的新密码文本。

# MySQL 客户端界面

MySQL 数据库的门户是 mysql 命令行界面程序。本节描述了 mysql 客户端程序以及如何使用它与你的数据库交互。

# 连接到服务器

mysql 客户端程序允许你使用任何用户账户和密码连接到网络上任何位置 MySQL 服务器。默认情况下，如果你在命令行中不带任何参数输入 mysql 程序，它将尝试使用登录用户名连接到运行在同一 Linux 系统上的 MySQL 服务器。

这很可能不是你想要连接数据库的方式。有一系列命令参数，允许你不仅可以控制连接到哪个 MySQL，还可以控制 mysql 界面的行为。表 24-1 显示了你可以配合 mysql 程序使用的命令行参数。

如你所见，有很多命令行选项可以修改你登录到 MySQL 服务器的日志。

默认情况下，mysql 客户端程序尝试使用你的 Linux 登录名登录 MySQL 服务器。如果该名称没有在 MySQL 中配置为用户账户，则你需要使用 -u 参数指定你的登录：

```
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with : or g.
Your MySQL connection id is 7
Server version: 5.0.45 Source distribution
```

输入 'help?' 或 '\h' 获取帮助。输入 '\c' 清除缓冲区。

```
mysql>
```

# 表 24-1

# mysql 命令行参数

| 参数 | 描述 |
| --- | --- |
| -A | 禁用自动重哈希。 |
| -b | 错误后禁用蜂鸣声。 |
| -B | 不使用历史文件。 |
| -C | 压缩客户端和服务器之间发送的所有信息。 |
| -D | 指定要使用的数据库。 |
| -e | 执行指定的语句并退出。 |
| -E | 垂直显示查询输出，每行一个数据字段。 |
| -f | 如果发生 SQL 错误则继续。 |
| -G | 启用命名 SQL 命令。 |
| -h | 指定 MySQL 服务器的主机名（默认是 localhost）。 |
| -H | 以 HTML 代码形式显示查询输出。 |
| -i | 忽略函数名后的空格。 |
| -N | 不在结果中显示列名。 |
| -o | 忽略命令行中指定的默认数据库外的语句。 |
| -p | 指定用户账户的密码。 |
| -P | 指定用于网络连接的 TCP 端口号。 |
| -q | 不缓存每个查询结果。 |
| -r | 在进行转义转换的情况下显示列值。 |
| -s | 静默模式。 |
| -S | 指定连接到 localhost 的套接。 |
| -t | 以表格形式显示输出。 |
| -T | 程序退出时显示调试信息、内存和 CPU 统计。 |
| -u | 指定用于登录的用户账户。 |
| -U | 仅允许指定键值的 UPDATE 和 DELETE 语句。 |
| -v | 详细模式。 |
| -w | 如果无法建立连接，则等待并重试。 |
| -X | 以 XHTML 代码形式显示查询输出。 |

# 第五部分 高级主题

p 参数告诉 MySQL 查询用于登录的用户账户的密码。一旦你登录到服务器，就可以开始输入命令了。

# mysql 命令

mysql 程序使用两种不同类型的命令：

- 特殊 mysql 命令
- 标准 SQL 语句

mysql 程序使用它自己的命令命令，允许你轻松地控制环境并检索有关 MySQL 服务器的信息。表 24-2 显示了这些命令。

你可以直接从 mysql 提示符使用完整命令或快捷命令：

```
mysql> \s

MySQL Ver 14.12 Distrib 5.0.45, for redhat-linux-gnu (i386) using readline 5.0

Connection: 10
Current database: root@localhost
Current user: Not in use
SSL:
Current pager: stdout
Using outfile:
Using delimiter: :
Server version: 5.0.45 Source distribution
Protocol version: 10
Connection: Localhost via UNIX socket
Server charset: latin1
Db charset: latin1
Client charset: latin1
Conn. charset: latin1
UNIX socket: /var/lib/mysql/mysql.sock
Uptime: 4 hours 15 min 22 sec
```

Threads: 1 Queries: 53 Slow queries: 0 Opens: 23 Flush tables: 1 Open tables: 17 Queries per second avg: 0.003

```
mysql>
```

mysql 程序实现了 MySQL 服务器支持的所有结构化查询语言（SQL）命令。“创建数据库对象”章节将详细讨论这些。

646

# 表 24-2

# mysql 命令

| 命令 | 快捷方式 | 描述 |
| --- | --- | --- |
| ? | \? | 帮助。 |
| clear | \c | 清除命令。 |
| connect | \r | 连接到数据库。 |
| delimiter | \d | 设置 SQL 隔符。 |
| edit | \e | 命令行编辑器命令。 |
| go | \g | 将命令发送到 MySQL 服务器。 |
| exit | \q | 退出 mysql 程序。 |
| help | \h | 显示帮助。 |
| nopager | \n | 禁用分页器并将输出到 STDOUT。 |
| note't | \t | 不发送输出到。 |
| output | \t | 将输出追加到文件。 |
| pager | \P | 设置分页器命令。 |
| print | \p | 输出当前命令。 |
| prompt | \R | 更改 mysql 提示符。 |
| quit | \q | 退出 mysql 程序（与 exit 同等）。 |
| refresh | \# | 重建表。 |
| source | \. | 执行指定文件中的脚本。 |
| status | \s | 从 MySQL 服务器检索状态。 |
| system | \! | 在系统上执行 shell 命令。 |
| tee | \T | 将所有输出追加到文件。 |
| use | \u | 使用另一个数据库。 |
| charset | \C | 更改另一个字符集。 |
| warnings | \W | 每个语句后显示警告。 |
| nowarning | \w | 每个语句后不显示警告。 |

# 高级主题

mysql 程序实现的一种常用 SQL 命令是 SHOW。使用此命令可以提取有关 MySQL 服务器的信息，例如创建的数据库和表：

```
mysql> SHOW DATABASES;
+----------------------+
| Database             |
+----------------------+
| Information_schema   |
| mysql                 |
+----------------------+
2 rows in set (0.04 sec)

mysql> USE mysql;
Database changed
mysql> SHOW TABLES;
+----------------------+
| Tables_in_mysql     |
+----------------------+
| columns_priv         |
| db                   |
| help_category        |
| help_keyword         |
| help_relation        |
| help_topic          |
| host                 |
| proc                 |
| procs_priv           |
| tables_priv          |
| time_zone            |
| time_zone_leap_second|
| time_zone_name       |
| time_zone_transition |
| time_zone_transition_type|
| user                 |
+----------------------+
17 rows in set (0.00 sec)
```

在这个例例中，我使用了 SHOW SQL 命令显示在 MySQL 服务器上配置的数据库，然后使用 USE SQL 命令连接到单个数据库。你的 mysql 会话一次只能连接到一个数据库。

你会注意到在每个命令后我都添加了分号。分号表示向 mysql 程序发送的结束。如果你不使用分号，它会提示更多数据：

```
mysql> SHOW
  -> DATABASES;
```

648

