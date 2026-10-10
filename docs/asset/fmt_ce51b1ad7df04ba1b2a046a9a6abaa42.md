
```bash
$ sudo service postgresql-8.4 status
Running clusters: 8.4/main
```

将 `postgresql-8.4` 替换为你系统上安装的 `postgresql-9.1` 或任何其他版本，或者如果你不确定 init 脚本的名称，可以直接检查 `/etc/init.d` 或 `/etc/rc.d/init.d` 目录。

或者，你可以使用 `ps` 命令：

```bash
$ ps -ef | grep postgres
postgres 1629 1 0 Jul10 7 00:00:06 /usr/lib/postgresql/8.4/bin/postgres -D /var/lib/postgresql/8.4/main -c config_file=etc/postgresql/8.4/main/postgresql.conf
postgres 1631 1629 0 Jul10 7 00:00:30 postgres: waker process
postgres 1632 1629 0 Jul10 7 00:00:30 postgres: writer process
postgres 1633 1629 0 Jul10 7 00:00:08 postgres: autovacuum launcher process
postgres 1634 1629 0 Jul10 7 00:00:04 postgres: stats collector process
```

与 MySQL 不同，即使 PostgreSQL 进行基本安装，也会有多个进程正在运行并负责不同的任务。此外，由于 PostgreSQL 默认监听与 MySQL 不同的端口（`5432`），当你运行 `netstat` 时，你需要 `grep` 该端口：

```bash
$ sudo netstat -lnp | grep :5432
tcp 0 0 127.0.0.1:5432 0.0.0.0:* LISTEN 1629/postgres
tcp6 0 0 ::1:5432 ::* LISTEN 1629/postgres
```

请注意，监听该端口的进程的 ID（`1629`）与 `ps` 输出中的第一个进程相同。如果没有获取到任何输出，请尝试 `grep` `postgres` 而不是端口号，以查看 `postgres` 是否正在监听其他任何端口（或者直接查看不带 `grep` 命令的 `netstat` 输出）。还要注意，在这种情况下，PostgreSQL 仅监听本地主机 IP（`127.0.0.1:5432`），因此只有同一服务器上的进程才能访问数据库——如果这是你唯一的需求，这是一个安全的默认设置。如果你需要其他服务器能够访问数据库，而 PostgreSQL 仅监听 `127.0.0.1`，你需要重新配置 PostgreSQL，使其监听你想要使用的网络接口的 IP，或者监听所有接口（`0.0.0.0`）。

#### 获取数据库指标

当你试图排查数据库中的问题时，服务器指标可能有用，但来自数据库本身的指标更有用。MySQL 和 PostgreSQL 都允许你访问它们的指标，但正如你将看到的，它们的做法完全不同。

##### MySQL

要从 MySQL 中提取指标，你将使用 `mysqladmin` 工具，该工具应作为你系统上 MySQL 客户端软件的一部分安装（这也意味着你可以在另一个系统上安装该软件，通过网络潜在地连接到数据库，并提取这些数据）。我们将使用 `mysqladmin` 提取的最基本（也可能是最直接有用）的数据是通过 `status` 命令获取的：

```bash
$ mysqladmin -u root -p status
Enter password:
Uptime: 2680987  Threads: 1  Questions: 17494181  Slow queries: 0  Opens: 2096 Flush tables: 1  Open tables: 64  Queries per second avg: 6.525
```

以下是这些值分别代表什么，摘自 `mysqladmin` 的手册页：

- **Uptime**

MySQL 服务器已运行的秒数

- **Threads**

活跃线程（客户端）的数量

- **Questions**

服务器启动以来来自客户端的问题（查询）数量

- **Slow queries**

耗时超过 `long_query_time` 秒的查询数量

- **Opens**

服务器打开的表的数量

- **Flush tables**

服务器执行的 `flush-s`、`refresh` 和 `reload` 命令的数量

- **Open tables**

当前打开的表的数量

- **Queries per second avg**

数据库每秒接收的查询的平均数量

对于许多数据库故障排除，这些值可能足以让你建立一个基线，并识别何时某个数值出现异常，特别是线程、慢查询和每秒查询数指标。当然，如果你想要更详细的信息，也可以通过 `extended-status` 命令获取：

```bash
$ mysqladmin -u root -p extended-status
Enter password:

+------------------------------------+
| Variable_name          | Value    |
+------------------------------------+
| Aborted_clients        | 0        |
| Aborted_connects       | 5        |
| Binlog_cache_disk_use  | 0        |
| Binlog_cache_use       | 0        |
| Bytes_received         | 3264109643 |
| Bytes_sent             | 49337359253 |
| . . .                      |            |
| Threads_cached         | 7        |
| Threads_connected      | 1        |
| Threads_created        | 6575     |
| Threads_running        | 1        |
| Uptime                 | 2683061  |
| Uptime_since_flush_status | 2683061 |
+------------------------------------+
```

`extended-status` 命令将提供 `status` 命令的所有信息，加上大量其他指标，这些指标可用于帮助为你的数据库建立基线，以便你可以看出何时出现异常情况。

##### PostgreSQL

PostgreSQL 收集并列出性能统计的方式与 MySQL 大不相同。首先，你需要编辑你的 `postgresql.conf` 文件（例如，在 Ubuntu 系统上，该文件位于 `/etc/postgresql/8.4/main/`），并确保 `track_activities` 和 `track_counts` 选项设置为 `on`。它们很可能默认为 `on`，但如果你需要更改这些变量，之后需要重启 PostgreSQL 才能使更改生效。

一旦启用了统计收集，数据将存储在数据库中的特殊表中。与 MySQL 不同，你将使用 SQL 命令从这些表中提取数据。完整的统计表列表记录在官方 PostgreSQL 文档中，但以下部分将列出一些特别有用的表。不过，在此之前，请确保你已成为 `postgres` 用户（或数据库中具有超级用户权限的其他用户），以便你可以发送查询：

```bash
# su - postgres
$ psql
psql (8.4.12)
Type "help" for help.
```

#### pg_stat_activity

`pg_stat_activity` 表显示每个当前正在运行的服务器进程的信息，包括它正在访问哪个数据库、使用哪个系统进程、哪个用户正在访问它、当前查询以及查询运行时间长短的数据。当你知道某个特定数据库进程占用大量 CPU 时间，并想知道它正在执行什么查询时，该表特别有价值。要查看表中的所有数据，请使用标准的 `select` 语句：
