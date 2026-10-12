
```
# mysqladmin variables | less
```

| 变量名 | 值 |
|---|---|
| back_log | 50 |
| basedir | /usr/ |
| db_cache_size | 8388600 |
| db_log_buffer_size | 32768 |
| db_home | /var/lib/mysql/ |
| db_max_lock | 10000 |
| db_logdir |  |
| db_shared_data | OFF |
| db_tmpdir | /tmp/ |
|  | ... |
|  | ... |
| tmp_table_size | 33554432 |
| tmpdir | /tmp/ |
| version | 3.23.57 |
| wait_timeout | 28800 |

如果你发现默认 MySQL 系统附带的选项和变量设置并不完全符合你的需求，你不必从头开始。mysql 包附带的示例 my.cnf 文件可以让你从一组更接近你需要的选项和变量开始。

## 使用示例 my.cnf 文件

示例 my.cnf 文件可在 `/usr/share/doc/mysql-server*` 目录中使用。要使用其中一个文件，请执行以下操作：

- 1. 保留旧 my.cnf 文件的副本：
    ```sh
    # mv /etc/my.cnf /etc/my.cnf.old
    ```

- 2. 将你想要的示例 my.cnf 文件复制到 `/etc/my.cnf` 文件。例如，要使用 my-medium.cnf 文件，请输入以下内容：
    ```sh
    # cp /usr/share/doc/mysql-server*/my-medium.cnf /etc/my.cnf
    ```

- 3. 使用任何文本编辑器以 root 用户身份编辑新的 `/etc/my.cnf` 文件，以进一步调整你的 MySQL 变量和选项。

以下段落描述了每个示例 my.cnf 文件：

### my-small.cnf

此选项文件推荐用于内存小于 64MB 且仅偶尔用于 MySQL 的计算机系统。使用此选项文件，MySQL 将无法处理大量使用，但也不会拖累计算机的性能。

对于 mysqld 服务器，缓冲区大小设置得很低——`sort_buffer` 仅为 64K，`key_buffer` 为 16K。`thread_stack` 仅设置为 64K，`net_buffer_length` 仅为 2K。`table_cache` 设置为 4。

### my-medium.cnf

与小型选项文件一样，my-medium.cnf 文件适用于 MySQL 不是唯一重要应用程序运行的系统。该系统可用的总内存量也很少——在 32MB 到 64MB 之间——然而预计会有更一致的 MySQL 使用。

此文件中的 `key_buffer` 大小设置为 16M，而 mysqld 服务器的 `sort_buffer` 值提高到 512K。`table_cache` 设置为 64（允许更多同时线程处于活动状态）。`net_buffer_length` 提高到 8K。

### my-large.cnf

my-large.cnf 示例文件适用于主要用于 MySQL 服务的计算机。它假设约有 512M 的可用内存。

服务器缓冲区允许更多活动线程和更好的排序性能。系统假设的 512M 内存的一半分配给 `key_buffer` 变量（256M）。`sort_buffer` 大小提高到 1M。`table_cache` 允许更多同时用户（最多 256 个活动线程）。

### my-huge.cnf

与 my-large.cnf 文件一样，my-huge.cnf 文件也期望计算机主要用于 MySQL。然而，其预期系统提供的总内存要多得多（内存介于 1G 和 2G 之间）。

排序缓冲区大小（`sort_buffer`）提高到 2M，而 `key_buffer` 设置为消耗 384M 内存。`table_cache` 大小加倍，以允许多达 512 个活动线程。

## 启动 MySQL 服务器

对于 Red Hat Linux，MySQL 服务器默认处于关闭状态。但是，要将其打开却相当简单。/etc/init.d/mysqld 启动脚本随 mysql-server 包提供。要启动服务器，你可以手动运行 mysqld 启动脚本，也可以将其设置为每次系统启动时启动。

要手动启动 MySQL 服务器，请以 root 用户身份从终端窗口输入以下内容：

```
# service mysqld start
```

要使 MySQL 服务器在计算机每次重新启动时启动，请以 root 身份输入以下内容：

```
# chkconfig mysqld on
```

这将设置 mysqld 在大多数多用户运行状态（级别 3、4 和 5）期间启动。要检查该服务是否已为这些级别打开，请从终端窗口输入 `chkconfig --list mysqld`。

## 检查 MySQL 服务器是否正在工作

你可以使用 `mysqladmin` 或 `mysqlshow` 命令来检查 MySQL 服务器是否正在运行。以下是使用 `mysqladmin` 命令检查 MySQL 服务器信息的示例。

```
# mysqladmin -u root -p version proc
Enter password: *******
mysqladmin  Ver 8.23 Distrib 3.23.57, for pc-linux-gnu on i686
Copyright (C) 2000 MySQL AB & MySQL Finland AB & TCX DataKonsult AB
This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL license

Server version                 3.23.57
Protocol version               10
Connection                     Localhost via UNIX socket
UNIX socket                    /var/lib/mysql/mysql.sock
Uptime:                        2 days 10 hours 47 min 35 sec

Threads: 1  Questions: 184  Slow queries: 0  Opens: 1  Flush tables: 3
Open tables: 1  Queries per second avg: 0.001

+-----------------------------------+-----------------------------------+
| Id | User | Host | db | Command| Time | State | Info |
+-----------------------------------+-----------------------------------+
|  52 | root | localhost| mysql| Query | 0 | | show processlist |
+-----------------------------------+-----------------------------------+
```

| ID | 用户 | 主机 | 数据库 | 命令 | 时间 | 状态 | 信息 |
|---|---|---|---|---|---|---|---|
| 52 | root | localhost | mysql | Query | 0 |  | show processlist |

这里显示的两个 `mysqladmin` 选项都提供了有用的信息。版本信息显示 `mysqladmin` 版本为 8.23，此 mysql 服务器发行版的编号为 3.23.57。二进制包是为 i686 处理器上的 PC 版本 Linux/GNU 创建的。与服务器的连接是通过本地主机上的 UNIX 套接字（`mysql.sock`）进行的。服务器已运行 2 天 10 小时 47 分钟 35 秒。统计数据显示，目前有一个线程（与服务器的连接）处于活动状态。服务器已收到 184 次请求。

`proc` 选项显示目前有一个客户端连接到服务器。该客户端以 root 用户身份登录到 localhost 上的 MySQL。具有 Id 为 52 的客户端（如果你想断开用户连接，作为服务器管理员你可以使用它）目前正在查询 MySQL 数据库。
如果服务器此刻未运行，上面显示的 `mysqladmin` 命令将导致失败消息：

```
mysqladmin: connect to server at 'localhost' failed.
```

建议的补救措施是尝试重新启动服务器（通过输入 `/etc/init.d/mysqld restart`）或确保套接字存在（`/var/lib/mysql/mysql.sock`）。

## 使用 MySQL 数据库

第一次启动 MySQL 服务器（使用前面描述的启动脚本）时，系统会为 MySQL 数据库创建初始授权表。它通过运行 `mysql_install_db` 命令来执行此操作。

> 注意：如果由于某种原因授权表未初始化，你可以自己以 root 用户身份运行 `mysql_install_db` 命令。多次运行该命令不会造成任何伤害。

`mysql_install_db` 命令为你提供了两个数据库：`mysql` 和 `test`。当你为这些数据库创建数据时，这些信息分别存储在 `/var/lib/mysql/mysql` 和 `/var/lib/mysql/test` 目录中。

### 启动 mysql 命令

要开始创建数据库和表，你可以使用 `mysql` 命令。从任何终端窗口，通过输入以下内容打开计算机上的 `mysql` 数据库：

```
# mysql -u root -p mysql
Enter password: ********

Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 39 to server version: 3.23.57
Type 'help;' or '\h' for help. Type '\c' to clear the buffer
mysql>
```

按提示输入 root 用户的 MySQL 密码。出现 `mysql>` 提示符，准备接受用于在本地主机上使用 `mysql` 默认数据库的工作命令。如果从另一台主机计算机连接到 MySQL 服务器，请在命令行中添加 `-h hostname`（其中 `hostname` 是 MySQL 服务器运行的计算机的名称或 IP 地址）。请记住，你也可以以任何有效的 `mysql` 登录名登录，而不管你当前使用的是哪个 Linux 登录帐户。

