
system locking is not in use

option `--set-variable` (`-O`) 的可能变量有：

back log current value: 50

db_cache_size current value: 8388600

db_log_buffer_size current value: 0

db_max_lock current value: 10000

db_lock_max current value: 10000

binlog_cache_size current value: 32768

connect_timeout current value: 5

table_cache current value: 64

thread_concurrency current value: 10

thread_cache_size current value: 0

tmp_table_size current value: 33554432

thread_stack current value: 65536

wait_timeout current value: 28800

服务器启动后，你可以通过运行带有 `variables` 选项的 `mysqladmin` 命令来查看实际正在使用的值。（将输出通过给 `less` 命令以便翻页查看信息。）以下是一个示例（如果你没有存储密码，此处会提示你输入密码）：

```
# mysqladmin variables | less
| Variable_name | Value                               |
|------------------------------------------------------|
| back_log | 50                                |
| basedir | /usr/                             |
| bdb_cache_size | 8388600                             |
| bdb_log_buffer_size | 32768                            |
| bdb_home | /var/lib/mysql/                     |
| bdb_max_lock | 10000                              |
| bdb_logdir |                                |
| bdb_shared_data | OFF                          |
| bdb_tmpdir | /tmp/                              |
|                                      |
| tmp_table_size | 33554432                         |
| tmpdir | /tmp/                           |
| version | 8.7                               |
| wait_timeout | 28800                            |
|------------------------------------------------------|
```

## 使用配置文件

在 `/usr/share/mysql/` 提供了示例 `mycnf` 文件。要使用其中一个文件，请执行以下操作：

1. 保留旧的 `my.cnf` 备份：

   `# mv my.cnf my.cnf.old`

2. 将使用的 `mycnf` 文件复制到 `/etc/`。例如，要使用 `medium.cnf`，输入：

   `# cp /usr/share/mysql/medium.cnf /etc/my.cnf`

3. 以 root 身份使用任何文本编辑器编辑 `my.cnf` 以进一步调优你的 MySQL 变量。

### small.cnf

此文件适用于内存小于 64MB 偶尔使用的系统。使用此选项文件，MySQL 无法处理大量数据，但对计算机性能造成负担。对于 `mysqld` 服务器，缓冲区大小设置得较低——`sort_buffer` 为 64K，`key_buffer` 为 16K。`thread_stack` 仅为 64K，`net_buffer_length` 为 2K。`table_cache` 设置为 4。

### medium.cnf

与 `small.cnf` 文件一样，`medium.cnf` 文件适用于 MySQL 不是唯一运行程序的系统。该系统可用内存较少——在 32MB 到 64MB 之间——但会有更频繁的 MySQL 使用。此文件中 `key_buffer` 大设置为 16M，而 `mysqld` 服务器的 `sort_buffer` 值增加到 512K。`table_cache` 允许更多并发线程（64 个），并增加到 8K。

### large.cnf

`large.cnf` 示例文件主要用于 MySQL 服务的计算机。它假设有 512M 的可用内存。服务器缓冲区允许更多活动线程和更好的排序性能。系统假设 512M 内存的一半分配给 `key_buffer` 变量（256M）。`sort_buffer` 增加到 1M。`table_cache` 允许更多并发用户（最多 256 个活动线程）。

### huge.cnf

与 `large.cnf` 文件一样，`huge.cnf` 文件预期计算机主要用于 MySQL。然而，为该系统提供了更多的总内存（1G 到 2G 内存之间）。排序缓冲区大小（`sort_buffer`）增加到 2M，而 `key_buffer` 设置为消耗 384M 内存。`table_cache` 增加了一倍，允许 512 个活动线程。

## 启动 MySQL 服务器

对于 Fedora，MySQL 服务器默认是关闭的。然而，开启它非常简单 `getetc/init.d/mysqld` 启动脚本随 `mysql-server` 包一起交付。要启动服务器，你可以运行 `mysqld` 启动脚本立即启动，然后将其设置为在系统每次启动时自动启动。

# 第 24 章：设置 MySQL 数据库服务器

要立即启动 MySQL 服务器，请在终端窗口中以用户输入以下命令：

```bash
# service mysqld start
```

要设置 MySQL 服务器在每次计算机重启时自动启动，请以 root 用户输入以下命令：

```bash
# chkconfig mysqld on
```

这将 `mysqld` 设置为在大多数多用户运行状态（级别 3、4 和 5）下启动。要检查这些级别是否已开启服务，请在终端窗口输入 `chkconfig --list mysqld`。

## 检查 MySQL 服务器是否正在运行

你可以使用 `mysqladmin` 或 `mysqlshow` 命令检查 MySQL 服务器是否已启动。以下是使用 `mysqladmin` 命令检查 MySQL 服务器信息的示例。

```bash
# mysqladmin -u root -p version proc
Enter password: ********
mysqladmin Ver 8.23 Distrib 3.23.58, for redhat-linux-gnu on i386
Copyright (C) 2000 MySQL AB & MySQL Finland AB & TC TCX DataKonsult AB
本软件不提供任何保证。这是一款免费软件，欢迎在 GPL 许可证下对其进行修改和重新发布
```

| 服务器版本 | 3.23.58 |

| :--- | :--- |

| 协议版本 | 10 |

| 连接 | 通过 UNIX socket 连接 localhost |

| UNIX socket | /var/lib/mysql/mysql.sock |

| 运行时间: | 2 天 10 小 47 分 35 秒 |

线程: 184 查询: 1 开启: 1 刷新表: 3

打开表: 1 每秒查询: 0.001

| Id | User | Host | db | Command | Time | State | Info |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 52 | root | localhost! | | Query | 0 | | show processlist |

这里显示的 `mysqladmin` 两个选项都提供了有用信息。版本显示 `mysqladmin` 版本为 8.23，分配给此 MySQL 服务器发行版的数字为 3.23.58。该二进制包是为 i686 处理器上的 PC 版本的 Linux/GNU 创建的。与服务器的连接通过本地主机上的 UNIX socket (`mysql.sock`) 实现。服务器已运行 2 天 10 小 47 分 30 秒。统计数据显示当前有一个活动线程（与服务器的连接）。向服务器已发送了 184 次请求。

# 第四部分：Fedora 网络和服务器设置

`proc` 选项显示当前有一个客户端连接到服务器。该客户端已以 root 用户身份在 `localhost` 登录 MySQL。Id 为 52 的客户端（如果你作为服务器管理员，想断开该用户的连接，则可以使用此 Id）当前正在查询 MySQL 数据库。

如果服务器此时没有运行，上一个示例中显示的 `mysqladmin` 将导致失败消息：

```bash
mysqladmin: connect to server at 'localhost' failed.
```

建议的解决办法是重启服务器（通过输入 `service mysqld restart`）或确保 socket 文件存在 (`/var/lib/mysql/mysql.sock`)。

## 操作 MySQL 数据库

首次启动 MySQL 服务器（使用之前描述的启动脚本）时，系统会为 MySQL 数据库创建初始权限表。这是通过运行 `mysql_install_db` 命令实现的。

`mysql_install_db` 命令从两个数据库开始：`mysql` 和 `test`。当你为这些数据库创建数据时，这些信息将分别存储在 `/var/lib/mysql/mysql` 和 `/var/lib/mysql/test` 目录。

## 启动 mysql 命令

要开始创建数据库和表，你可以使用 `mysql` 命令。从任何终端窗口，通过输入以下内容打开你计算机上的 `mysql` 数据库：

```bash
# mysql -u root -p mysql
Enter password: ********
```

```bash
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection is 39 to server version: 3.23.58
Type 'help' or 'h' for help. Type '\c' to clear the buffer
```

```mysql
mysql>
```

按照提示输入 root 用户的 MySQL 密码。（如果没有设置密码，可以跳过 `-p` 选项）。出现 `mysql>` 提示符，准备好接受操作 `localhost` 上 `mysql` 默认数据库的命令。如果你从另一个主机连接到 MySQL 服务器，请添加 `-h hostname`（`hostname` 是运行 MySQL 服务器的计算机名称或 IP 地址）。记住，你也可以登录你创建的任何有效 `mysql` 账户，无论你当前登录哪个 Linux 账户。

正如 MySQL 监控器的欢迎信息所示，请确保输入的每个命令都以分号（`;`）或 `\g` 结束。如果你输入了一个命令而它似乎在等待更多输入，可能是因为你忘记在末尾加分号了。

在开始使用 `mysql` 界面创建数据库之前，请尝试使用 `status` 命令检查 MySQL 服务器的状态。以下是 `status` 命令的输出示例：

```mysql
mysql> status
-----------------
mysql Ver 11.18 Distrib 3.23.58, for pc-linux-gnu (i686)

Connection id:      43
Current database: mysql
Current user:      root@localhost
Current pager:    stdout
Using outfile:      "
Server version:    3.23.58
Protocol version:   10
Connection:         localhost via UNIX socket
UNIX socket:       /var/lib/mysql/mysql.sock
Uptime:            2 days 10 hours 47 min 35 sec

Threads: 184 Queries: 1 Opens: 1 Flush tables: 3
Open tables: 1 queries per second: 0.001
-----------------
```

状态信息告诉你有 MySQL 服务器的版本 (11.18) 和发行版 (3.23.58)。输出还提醒了你当前所在的数据库 (`mysql`) 和你的用户 (`root@localhost`)。你可以看到服务器已运行了多久，当前有多少个活动线程以及运行了多少命令。

## 使用 mysql 创建数据库

在交互式 `mysql` 会话中，你可以创建和修改数据库及表。如果你还没有连接到 `mysql` 会话，请输入以下命令（假设用户为 root）：

```bash
# mysql -u root -p
Enter password: ********
mysql>
```

创建数据库的通用步骤包括：创建数据库名称、将新数据库标识为当前数据库、创建表以及向表中添加数据。当你连接到 `mysql` 会话时，可以运行以下过程来创建表。

- 1. 要创建一个新的数据库名称，在 `mysql>` 提示符下使用 `CREATE DATABASE` 命令。例如，要创建一个名为 `allusers` 的数据库，请输入：

```mysql
mysql> CREATE DATABASE allusers;
```

此操作会在 `/var/lib/mysql` 目录下创建一个名为 `allusers` 的数据库。（虽然此处显示的命令不一定使用大写，但有助于将命令与数据库条目区分开。）

> 注意：或者，你也可以使用 `mysqladmin` 从命令行创建数据库。例如，使用 `mysqladmin` 创建名为 `allusers` 的数据库，你可以输入：

`mysqladmin -u root -p create allusers`

- 2. 要查看你的 MySQL 服务器上有哪些数据库，在 `mysql>` 提示符下输入：

```mysql
mysql> SHOW DATABASES;
+----------------------+
| Database             |
+----------------------+
| allusers             |
| mysql               |
| test                 |
+----------------------+
3 rows in set (0.00 sec)
```

这里显示的数据库名为 `allusers`、`mysql` 和 `test`。`allusers` 数据库是上一步创建的。`mysql` 数据库包含用户访问数据。`test` 数据库是为测试 `mysql` 数据库而自动创建的。

- 3. 要操作你创建的数据库 (`allusers`)，你需要将 `allusers` 设置为你的当前数据库。为此，在 `mysql>` 命令提示符下输入：

```mysql
mysql> USE allusers;
Database changed
```

- 4. 为你的数据库创建表需要一些规划和对语法的理解。你可以输入以下命令和列信息来尝试创建表。有关创建表和使用不同数据类型的更详细信息，请参阅本章节稍后部分的“理解 MySQL 表”章节。

要创建一个名为 `names` 的表，在 `mysql>` 提示符下使用以下 `CREATE TABLE` 命令：

```mysql
mysql> CREATE TABLE names (
-> firstname varchar(20)  not null,
```

## 第 24 章：设置 MySQL 数据库服务器 885

```sql
- lastname varchar(20) not null,
- streetaddr varchar(30) not null,
- city varchar(20) not null,
- state varchar(20) not null,
- zipcode varchar(10) not null
);
Query OK, 0 rows affected (0.00 sec)
```

你现在已经为 `allusers` 数据库创建了一个名为 `names` 的表。每个表都包含 `firstname`、`lastname`、`streetaddr`、`city`、`state` 州和 `zipcode` 列。每列允许的记录长度在 10 到 30 个字符之间。虽然 MySQL 支持多种数据库格式，由于此处没有指定，使用的是默认的 MyISAM 数据库类型。

有了数据库和一个表，你现在可以向表中添加数据了。

## 向 MySQL 数据库表添加数据

在创建数据库且表结构到位后，你就可以开始操作数据库了。你可以通过在 `mysql` 会话期间期间手动输入每条记录来向 MySQL 数据库添加数据，也可以将数据添加到纯文本文件中并将该文件加载到数据库中。

## 手动输入数据

为了继续本节，我假设你已经打开了一个交互式的 `mysql` 会话，并且已经按照上一节所述创建了数据库和表。如果你还没有连接到 `mysql` 会话，请输入以下命令（假设 `mysql` 用户名为 root）：
