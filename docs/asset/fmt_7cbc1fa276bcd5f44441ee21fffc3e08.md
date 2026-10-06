
# 第 24 章：设置 MySQL 数据库服务器

| Variable_name | Value |
| :--- | :--- |
| bdb_lock_max | 当前值: 10000 |
| binlog_cache_size | 当前值: 32768 |
| connect_timeout | 当前值: 5 |
| table_cache | 当前值: 64 |
| thread_concurrency | 当前值: 10 |
| thread_cache_size | 当前值: 0 |
| tmp_table_size | 当前值: 1048576 |
| thread_stack | 当前值: 65536 |
| wait_timeout | 当前值: 28800 |

服务器启动后，你可以运行带有 `variables` 选项的 `mysqladmin` 命令查看实际使用的值。（将输出通过给 `less` 命令以便翻页查看信息）。以下是一个示例：

```
# mysqladmin variables less
```

| Variable_name | Value |
| :--- | :--- |
| ansi_mode | OFF |
| back_log | 50 |
| basedir | /usr/ |
| bdb_cache_size | 838860 |
| bdb_log_buffer_size | 32768 |
| bdb_home | /var/lib/mysql/ |
| bdb_max_lock | 10000 |
| bdb_logdir | |
| bdb_shared_data | OFF |
| bdb_tmpdir | /tmp/ |
| tmp_table_size | 1048576 |
| tmpdir | /tmp/ |
| version | 3.23.49 |
| wait_timeout | 28800 |

如果你认为默认 MySQL 系统自带的选项和变量设置并不完全适合你，你不需要从头开始。mysql 软件包附的示例 `my.cnf` 文件可以让你从一组更接近你需求的选项和变量开始。

## 使用示例的 my.cnf 文件

示例的 `my.cnf` 文件位于 `/usr/share/doc/mysql-server*` 目录下。要使用这些文件之一，请执行以下操作：

1. 保留旧 `my.cnf` 文件的副本：

```
# mv /etc/my.cnf /etc/my.cnf.old
```

2. 将你想要的示例 `my.cnf` 文件复制到 `/etc/my.cnf` 文件。例如，要使用 `my-medium.cnf` 文件，输入以下内容：

```
# cp /usr/share/doc/mysql-server/*/my-medium.cnf /etc/my.cnf
```

3. 使用任何文本编辑器（作为 root 用户）编辑新的 `/etc/my.cnf` 文件，以进一步调整你的 MySQL 变量和选项。

以下段落描述了每个示例 `my.cnf` 文件：

### my-small.cnf

该选项文件适用于内存小于 64MB 且仅偶尔运行 MySQL 的计算机系统。使用这些选项，MySQL 将无法处理大量并发使用，但不会影响计算机的性能。

对于 `mysqld` 服务器，缓冲区大小很低——`sort_buffer` 仅为 64K，`key_buffer` 仅为 16K。`thread_stack` 设置为 64K，`net_buffer_length` 仅 2K。`table_cache` 设置为 4。

### my-medium.cnf

与选项文件一样，`my-medium.cnf` 文件适用于 MySQL 不是运行的唯一重要程序的系统。该系统的总内存也较小——在 32MB 到 64MB 之间——但预期会有更的 MySQL 工作。

此文件中，`key_buffer_size` 设置为 16M，而 `mysqld` 服务器的 `sort_buffer` 值提高到 512K。`table_cache` 设置为 64（允许更多并发线程活跃）。`net_buffer_length` 提高到 8K。

### my-large.cnf

`my-large.cnf` 示例文件适用于主要用于 MySQL 服务的计算机。它假设有约 512M 的可用内存。提供了更多的 MySQL 服务，并且执行得更好。

服务器缓冲区允许更多的活动线程和更好的排序性能。系统假设的 512M 内存中有一半被分配给 `key_buffer` 变量 (256M)。`sort_buffer` 增大到 1M。`table_cache` 允许更多的并发用户（多达 256 个活动线程）。

### my-huge.cnf

与 `my-large.cnf` 文件一样，`my-huge.cnf` 文件期望计算机主要用于 MySQL。然而，它预期的系统提供了更多的总内存（1G 到 2G 内存之间）。

当 `key_buffer` 设置为 384M 内存时，排序缓冲区大小 (`sort_buffer`) 增大到 2M。`table_cache` 增加了一倍，允许允许 512 个活动线程。

## 启动 MySQL 服务器

对于 Red Hat Linux，MySQL 服务器默认关闭的。然而，开启它非常简单。`/etc/init.d/mysql` 启动脚本由 `mysql-server` 软件包提供。要启动服务器，你可以手动运行 `mysqld` 启动脚本，或将其设置为每次启动时启动。

要手动启动 MySQL 服务器，在终端窗口中以 root 用户身份输入以下内容：

```
# mysqld start
```

要在计算机每次重新启动时自动启动 MySQL 服务器，以 root 用户身份输入：

```
# chconfig on
```

要检查多用户状态（3、4、5 级）的服务是否开启，输入：

```
# chconfig --list
```

## 检查 MySQL 服务器正在运行

你可以使用 `mysqladmin` 命令检查 MySQL 服务器是否已运行。以下是使用 `mysqladmin` 命令检查 MySQL 服务器信息的示例。

```
# mysqladmin -u root -p version
Enter password: ********

mysqladmin Ver 8.23 Distrib 3.23.51, for pc-linux-gnu

Copyright (C) 2000 MySQL AB

此软件是免费的，欢迎在 GPL 许可下修改和分发

Server Version: 3.23.51

Protocol version: 10

Connection: Localhost via UNIX socket

UNIX socket: /var/lib/mysql/mysql.sock

Uptime: 1 day 0 hours 47 min 35 sec

Threads: 1

Questions: 184

Slow queries: 0

Opens: 12

Flush tables: 1

Open tables: 6
```

| Id | User | Host | Command | Time | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 52 | root | localhost | Query | 0 | show processlist |

这里显示的每个 `mysqladmin` 选项提供了有用信息。版本信息显示 `mysqladmin` 版本为 8.23，分配给此 MySQL 服务器的版本是 3.23.51。二进制包为 Linux/GNU (on the i86 processor) 创建。连接通过 localhost 上的 UNIX socket (`mysql.sock`)。服务器运行了 2 小时 47 分 35 秒。统计数据显示有一个活动线程（连接到服务器）。向服务器发送了 184 次请求。proc 显示客户端以 root 用户身份登录 MySQL。Id 为 52 的客户端（你可以作为服务器管理员）正在查询 MySQL 数据库。

如果服务器现在没有运行，上述 `mysqladmin` 命令将导致错误消息：

```
mysqladmin: connect to server at 'localhost' failed.
```

建议的解决方法是尝试重启服务器（通过 `/etc/init.d/mysql restart`）或确保 socket 存在 (`/var/lib/mysql/mysql.sock`)。

## 操作 MySQL 数据库

当你第一次启动 MySQL 服务器（使用之前描述的启动脚本）时，系统为 MySQL 数据库创建权限表。这是通过运行 `mysql_install_db` 命令实现的。

> 注意：由于某些原因权限表未初始化，你可以自己运行 `mysql_install_db` 命令（作为 root 用户）。多次运行该命令没有副作用。

`mysql_install_db` 命令提供了两个数据库：`mysql` 和 `test`。当你为这些数据库创建数据时，信息分别存储在 `/var/lib/mysql/mysql` 和 `/var/lib/mysql/test` 目录。

## 启动 mysql 命令

要创建数据库和表可以使用 `mysql` 命令。在终端窗口输入以下内容打开计算机上的 mysql 数据库：

```
# mysql -u root -p mysql
Enter password: ********
Welcome to the MySQL monitor. Commands end with ; or \
Your connection id is 39 to server version: 3.23.51
Type 'help' or 'h' for help. Type 'c' to clear the buffer
mysql>
```

按照提示输入 root 用户的 MySQL 密码。出现 `mysql>` 提示符，准备接受处理 localhost MySQL 默认数据库的命令。如果你从任何其他主机连接 MySQL 服务器，请向命令行添加 `-h hostname`（hostname 是运行 MySQL 服务器的计算机的名称或 IP 地址）。记住，无论你当前登录哪个 Linux 账户，都可以作为任何有效的 MySQL 登录。

如上文所述，确保你输入的每个命令都以分号 (`;`) 或反斜杠 (`\`) 结束。如果你输入了一个命令并似乎在等待更多输入，可能是因为你忘记在结尾加分号了。

在使用 mysql 接口创建数据库之前，尝试使用 `status` 命令检查 MySQL 服务器的状态。以下是 `status` 命令的输出示例：

```
mysql> status
-----------------------
mysql Ver 11.18 Distrib 3.23.51, for pc-linux-gnu (1386)
Connection id: 43
Current database: mysql
Current user: root@localhost
Current pager: ''
Using output: ''
Server version: 3.23.51
Protocol version: 10
Connection: Localhost via UNIX socket
Client charset: latin
Server charset: latin
IX socket: /var/lib/mysql/mysql.sock
Uptime: 1 day 2 hours 57 min 19 sec
Threads: 1
Questions: 136
Slow queries: 0
Opens: 12
Flush tables: 1
Open tables: 6
Queries per sec avg: 0.061
```

`status` 信息告诉你关于 MySQL 服务器的版本 (11.18) 和发行版本 (3.23.51)。输出还提醒了你当前的数据库 (`mysql`) 和你的用户名 (`root@localhost`)。你可以看到服务器运行的时间 (`Uptime`)。你可以

另请查看当前活跃的线程数以及查询此服务器运行了多少条命令（问题）。

## 使用 mysql 创建数据库

在交互式 mysql 会话中，你可以创建和修改数据库及表。如果你尚未连接到 mysql 会话，请输入以下命令（假设 mysql 用户名为 root）：

```
# mysql -u root -p
Enterter password: ********
mysql>
```

创建 MySQL 数据库的通用步骤包括创建数据库名称、将新数据库标识为当前数据库、创建表以及向表中添加数据。在连接到 mysql 会话期间，你可以运行该程序来创建一个示例数据库。

- 1. 若要创建一个新数据库，请在 `mysql>` 提示符下使用 `CREATE DATABASE` 命令。例如，要创建一个名为 `allusers` 的数据库，请输入以下内容：
`mysql> CREATE DATABASE allusers;`

此操作将在 `/var/lib/mysql` 目录下创建一个名为 `allusers` 的数据库。

> 注意：你也可以使用 `mysqladmin` 命令从命令行创建数据库。例如，要使用 `mysqladmin` 创建名为 `allusers` 的数据库，你可以输入以下内容：`mysqladmin -u root -p create allusers`

- 2. 要查看你的 mysql 服务器上有哪些可用数据库，请在 `mysql>` 下输入以下内容：`mysql> SHOW DATABASES:`
|----------------------|
| Database |
|----------------------|
| allusers         |
| mysql            |
| test             |
|----------------------+
3 rows in set (0.00 sec)

此处显示的数据库名为 `allusers`、`mysql` 和 `test`。`allusers` 数据库是上一步中创建的。`mysql` 数据库包含用户访问数据。`test` 数据库是为创建测试 mysql 数据库而自动。

- 3. 要操作我们刚刚创建的数据库 (`allusers`)，你需要将 `allusers` 设置为你的当前数据库。要为此，请在 `mysql>` 命令提示符下输入以下内容：

```
mysql USE allusers;
Database changed
```

- 4. 为你的数据库创建表需要一些规划以及对表语法的理解。你可以输入以下命令和列信息来尝试创建表。有关创建表和使用不同数据类型的更多详细信息，请参考本章中的“理解 MySQL 表”部分。

在 `mys>` 提示符下，使用以下 `CREATE TABLE` 命令创建一个名为 `"names"` 的表：

```
mysql CREATE TABLE names (
  -- firstname varchar(20 not null,
  -- lastname varchar(20) not null,
  -- streetaddr varchar(30) not null,
  -- city varchar(20) not null,
  -- state varchar(20) not null,
  -- zipcode varchar(10) not null
);
Query OK, 0 rows affected (0.00 sec)
```

你已经为名为 `allusers` 的数据库创建了一个名为 `names` 的表。它包含了名为 `firstname`、`streedaddr`、`city`、`state` 和 `zipcode` 的列。每列允许记录长度在 10 到 30 个字符之间。虽然 MySQL 支持多种不同的数据库格式，由于此处未指定，因此使用了默认的 MyISAM 数据库类型。

创建数据库后，你可以向表中添加数据。

## 向 MySQL 数据库表添加数据

在创建数据库且表结构到位后，你可以开始操作数据库。你可以通过在 mysql 会话期间手动输入每条记录，或通过将数据添加到文本文件中并加载到数据库中向你的 MySQL 数据库添加数据。

## 手动输入数据

为了执行本节的操作，我假设你已经打开了一个交互式 mysql 会话，并且已按照上一节所述创建了数据库和表。如果你尚未连接到 mysql 会话，请输入以下命令（假设 mysql 用户名为 root）：

```
# mysql -u root -p
Enter password: ********
mysql>
```

向 MySQL 数据库添加条目，以下步骤描述了如何查看可用表并手动将数据加载到这些表中。随后的步骤描述了如何创建一个包含数据库数据的文本文件以及如何将该文件加载到你的数据库中。

- 1. 若要将你想使用的数据库设置为当前数据库（在此例中为 `allusers`），在 `mysql>` 提示符下输入以下命令：

```
mysql> USE allusers;
Database changed
```

- 2. 要查看与当前数据库关联的表，请在 `mysql>` 提示符下输入以下命令：

```
mysql> SHOW tables;
|--------------------|
| Tables in allusers |
|--------------------|
| names             |
|--------------------|
1 row in set (0.00 sec)
```

你可以看到，为止为 `allusers` 数据库定义的表名为 `"names"` 的表。

- 3. 要显示 `"names"` 表的格式，请在 `mysql>` 提示符下输入以下命令：

```mysql
mysql> DESCRIBE names;
```
