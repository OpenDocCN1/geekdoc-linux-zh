
与小型选项文件一样，`my-medium.cnf` 文件旨在用于 MySQL 不是唯一重要应用程序的系统。此系统可用的总内存也较少 —— 在 32MB 到 64MB 之间 —— 但预计会有更一致的 MySQL 使用。

此文件中 `key_buffer_size` 设置为 16M，而 `sort_buffer` 值提高到 512K（针对 `mysqld` 服务器）。`table_cache` 设置为 64（允许更多的同时活动线程）。`net_buffer_length` 提高到 8K。

### my-large.cnf

`my-large.cnf` 示例文件旨在用于主要专门用于 MySQL 服务的计算机。它假设可用内存约为 512M。更多 MySQL 服务可用，并且性能更好。

服务器缓冲区允许更多的活动线程和更好的排序性能。系统假设的 512M 内存的一半分配给 `key_buffer` 变量（256M）。`sort_buffer` 大小提高到 1M。`table_cache` 允许许多更多同时用户（最多 256 个活动线程）。

### my-huge.cnf

与 `my-large.cnf` 文件一样，`my-huge.cnf` 文件期望计算机主要用于 MySQL。但是，其目标系统提供更多总内存（1G 到 2G 内存之间）。

排序缓冲区大小（`sort_buffer`）提高到 2M，而 `key_buffer` 设置为消耗 384M 内存。`table_cache` 大小加倍，以允许最多 512 个活动线程。

## 启动 MySQL 服务器

对于 Red Hat Linux，MySQL 服务器默认是关闭的。但是，开启它相当简单。`/etc/init.d/mysqld` 启动脚本随 `mysql-server` 包一起提供。要启动服务器，你可以手动运行 `mysqld` 启动脚本，或者设置它在系统每次启动时自动运行。

要手动启动 MySQL 服务器，请在终端窗口中作为 root 用户键入以下内容：

```text
# /etc/init.d/mysqld start
```

要设置 MySQL 服务器在计算机每次重启时自动启动，请作为 root 用户键入以下内容：

```text
# chkconfig mysqld on
```

这会将 `mysqld` 设置为在大多数多用户运行状态（级别 3、4 和 5）期间启动。要检查这些级别是否已启用该服务，请在终端窗口中键入 `chkconfig --list mysqld`。

### 检查 MySQL 服务器是否正常工作

你可以使用 `mysqladmin` 或 `mysqlshow` 命令来检查 MySQL 服务器是否正在运行。以下是如何使用 `mysqladmin` 命令检查 MySQL 服务器信息的示例。

```text
# mysqladmin -u root -p version proc
Enter password: ********
mysqladmin  Ver 8.23 Distrib 3.23.49, for redhat-linux-gnu on i386
Copyright (C) 2000 MySQL AB & MySQL Finland AB & TCX DataKonsult AB
This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL license

Server version		3.23.49
Protocol version	10
Connection		Localhost via UNIX socket
UNIX socket		/var/lib/mysql/mysql.sock
Uptime:			2 days 10 hours 47 min 35 sec

Threads: 1  Questions: 184  Slow queries: 0  Opens: 1  Flush tables: 3
Open tables: 1  Queries per second avg: 0.001

+----+------+-----------+------+---------+------+-------+--------------------+
| Id | User | Host      | db   | Command | Time | State | Info               |
+----+------+-----------+------+---------+------+-------+--------------------+
|  52 | root | localhost | mysql| Query   |  0   |       | show processlist   |
+----+------+-----------+------+---------+------+-------+--------------------+
```

此处显示的 `mysqladmin` 的两个选项均提供有用的信息。版本信息显示 `mysqladmin` 版本为 8.23，此 MySQL 服务器发行版分配的编号为 3.23.49。二进制包是为 i386 处理器上的 Red Hat Linux/GNU 创建的。与服务器通过本地主机上的 UNIX 套接字（`mysql.sock`）连接。服务器已运行 2 天 10 小时 47 分钟 35 秒。统计显示当前有一个线程（与服务器的连接）处于活动状态。服务器已收到 184 个请求。

`proc` 选项显示当前有一个客户端连接到服务器。该客户端以 root 用户身份登录到本地主机上的 MySQL。该客户端的 Id 为 52（你可以作为服务器管理员使用，如果你想要断开该用户的连接），目前正在查询 MySQL 数据库。

如果服务器当前未在运行，上述显示的 `mysqladmin` 命令将会导致失败消息：

```
mysqladmin: connect to server at 'localhost' failed.
```

建议的补救措施是尝试重新启动服务器（通过输入 `/etc/init.d/mysqld restart`）或确保套接字存在（`/var/lib/mysql/mysql.sock`）。

## 操作 MySQL 数据库

第一次启动 MySQL 服务器（使用前面描述的启动脚本）时，系统会为 MySQL 数据库创建初始授权表。这是通过运行 `mysql_install_db` 命令来实现的。

> 注意：如果由于某种原因授权表未初始化，你可以自行运行 `mysql_install_db` 命令（作为 root 用户）。多次运行该命令不会造成任何伤害。

`mysql_install_db` 命令让你从两个数据库开始：`mysql` 和 `test`。当你为这些数据库创建数据时，该信息分别存储在 `/var/lib/mysql/mysql` 和 `/var/lib/mysql/test` 目录中。

### 启动 mysql 命令

为了开始创建数据库和表，你可以使用 `mysql` 命令。在任何终端窗口中，通过输入以下内容打开你电脑上的 `mysql` 数据库：

```
# mysql -u root -p mysql
Enter password: ********
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 39 to server version: 3.23.49
Type 'help;' or '\h' for help. Type '\c' to clear the buffer
mysql>
```

当提示时，输入 root 用户的 MySQL 密码。会出现 `mysql>` 提示符，准备接收操作本地主机上 `mysql` 默认数据库的命令。如果你从另一台主机计算机连接到 MySQL 服务器，请在命令行中添加 `-h hostname`（其中 `hostname` 是运行 MySQL 服务器的计算机的名称或 IP 地址）。请记住，你可以登录为你创建的任何有效的 mysql 登录名，无论当前登录的是哪个 Linux 登录账户。

正如上面 `mysql` 文本注释所述，请确保在输入的每条命令末尾加上分号 (`;`) 或 `\g`。如果你输入命令后它似乎在等待更多输入，可能是因为你在末尾忘记加分号。

在开始使用 `mysql` 接口创建数据库之前，尝试使用 `status` 命令检查 MySQL 服务器的状态。以下是 `status` 命令输出的一个示例：
