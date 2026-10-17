
要使 MySQL 服务器在计算机每次重新启动时启动，请以 root 身份输入以下内容：

```
# chkconfig mysqld on
```

这将设置 `mysqld` 在大多数多用户运行状态（级别 3、4 和 5）期间启动。要检查该服务是否已为这些级别打开，请从终端窗口输入 `chkconfig --list mysqld`。

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

这里显示的两个 `mysqladmin` 选项都提供了有用的信息。版本信息显示 `mysqladmin` 版本为 8.23，此 mysql 服务器发行版的编号为 3.23.57。二进制包是为 i686 处理器上的 PC 版本 Linux/GNU 创建的。与服务器的连接是通过本地主机上的 UNIX 套接字（`/var/lib/mysql/mysql.sock`）进行的。服务器已运行 2 天 10 小时 47 分钟 35 秒。统计数据显示，目前有一个线程（与服务器的连接）处于活动状态。服务器已收到 184 次请求。

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

如上文 mysql 文本所述，请确保为你输入的每个命令以分号（`;`）或 `\g` 结尾。如果输入命令后似乎在等待更多输入，很可能是因为你忘了在末尾加上分号。

在开始使用 mysql 接口创建数据库之前，请尝试使用 `status` 命令检查 MySQL 服务器的状态。以下是 `status` 命令输出的示例：

```
mysql> status
-------------------------------
mysql Ver 11.18 Distrib 3.23.57, for pc-linux-gnu (i686)

Connection id: 43

Current database: mysql

Current user: root@localhost

Current pager: stdout

Using outfile: ''

Server version: 3.23.57

Protocol version: 10

Connection: Localhost via UNIX socket

Client charset: latin1

Server charset: latin1

UNIX socket: /var/lib/mysql/mysql.sock

Uptime: 1 day 2 hours 57 min 19 sec

Threads: 1 Questions: 136 Slow queries: 0 Opens: 12

Flush tables: 1 Open tables: 6 Queries per second avg: 0.001
-------------------------------
```

状态信息会告诉你 MySQL 服务器的版本（11.18）和发行版（3.23.57）。输出还会提醒你当前数据库（`mysql`）和你的用户名（`root@localhost`）。你可以看到服务器已运行的时间（Uptime）。你还可以看到当前活跃的线程数以及查询该服务器的命令数（Questions）。

## 使用 mysql 创建数据库

在交互式 mysql 会话中，你可以创建和修改数据库和表。如果尚未连接到 mysql 会话，请输入以下命令（假设 mysql 用户名为 root）：

```
# mysql -u root -p

Enter password: ********

mysql>
```
