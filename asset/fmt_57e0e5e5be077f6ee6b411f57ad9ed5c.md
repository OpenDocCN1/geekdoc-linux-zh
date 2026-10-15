
对于 Fedora 和 RHEL，MySQL 服务器默认是关闭的。然而，打开它相当简单。`/etc/init.d/mysqld` 启动脚本随 `mysql-server` 包一起提供。要启动服务器，你可以运行 `mysqld` 启动脚本使其立即启动，然后设置它在每次系统启动时都启动。

要立即启动 MySQL 服务器，请以 root 用户身份在终端窗口中输入以下命令：

```
# service mysqld start
```

若需设置 MySQL 服务器在计算机每次重启时都自动启动，请以 root 身份输入以下命令：

```
# chkconfig mysqld on
```

这会将 `mysqld` 设置为在大多数多用户运行状态（级别 3、4 和 5）下启动。若要检查该服务是否已针对这些级别启用，请在终端窗口中输入 `chkconfig --list mysqld`。

## 检查 MySQL 服务器是否正在运行

你可以使用 `mysqladmin` 或 `mysqlshow` 命令来检查 MySQL 服务器是否已启动并正在运行。下面是一个使用 `mysqladmin` 命令检查 MySQL 服务器信息的示例。

```
# mysqladmin -u root -p version proc
Enter password: ******
mysqladmin Ver 8.41 Distrib 5.0.45, for redhat-linux-gnu on i386
Copyright (C) 2000-2006 MySQL AB

This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL license

Server version		5.0.45
Protocol version		10
Connection		Localhost via UNIX socket
UNIX socket		/var/lib/mysql/mysql.sock
Uptime:				2 days 10 hours 47 min 35 sec

Threads: 2 Questions: 184 Slow queries: 0 Opens: 11 Flush tables: 1 Open
tables: 0 Queries per second avg: 0.004
```

此处展示的两个 `mysqladmin` 选项均提供有用信息。版本信息显示 `mysqladmin` 的版本为 8.41，而该 MySQL 服务器发行版的编号为 5.0.45。该二进制包是为 i386 处理器上的 PC 版 Linux/GNU 创建的。与服务器通过本地主机上的 UNIX 套接字（`mysql.sock`）进行连接。服务器已运行 2 天 10 小时 47 分 35 秒。统计数据显示，当前有一个活动线程（与服务器建立的连接）。已有 184 个请求发送至服务器。

`proc` 选项显示当前有一个客户端已连接到服务器。该客户端以 `root` 用户身份登录到 `localhost` 上的 MySQL。ID 为 2 的客户端（这告知你该用户是谁，如果你希望断开该用户的连接，作为服务器管理员，你可以使用此信息）当前正在查询 MySQL 数据库。

如果服务器当前未运行，上述示例中显示的 `mysqladmin` 命令将导致错误消息：

```
mysqladmin: connect to server at 'localhost' failed.
```

建议的补救措施是尝试重启服务器（输入 `service mysqld restart`）。

## 操作 MySQL 数据库

首次启动 MySQL 服务器（使用前面描述的启动脚本）时，系统会创建 MySQL 数据库的初始授权表。它是通过运行 `mysql_install_db` 命令来完成此操作的。

`mysql_install_db` 命令开始时为你提供两个数据库：`mysql` 和 `test`。当你为这些数据库创建数据时，相关信息将分别存储在 `/var/lib/mysql/mysql` 和 `/var/lib/mysql/test` 目录中。

由于 MySQL root 用户不一定是系统 root 用户（只要你拥有 MySQL root 用户的密码），你可以以任何你选择的用户身份登录 Fedora 或 RHEL。在以下示例中，确保在运行所示命令时提供 MySQL root 用户密码。

> **注意：** 如果你使用的是旧的 ISAM 表而不是 MyISAM，MySQL 5.0 已移除对 ISAM 表的支持。你需要使用如下语句将你的表转换为 MyISAM：
>
> ```
> ALTER TABLE table ENGINE=MYISAM
> ```
>
> 其中 `table` 是你的表名。有关升级到 MySQL 5.0 的更多信息，请参阅 MySQL 参考手册（[http://dev.mysql.com/doc/refman/5.0/en/upgrade.html](http://dev.mysql.com/doc/refman/5.0/en/upgrade.html)）。

### 启动 mysql 命令

要开始创建数据库和表，你可以使用 `mysql` 命令。从任意终端窗口，输入以下命令以打开你计算机上的 mysql 数据库：

```
$ mysql -u root -p mysql
Enter password: ********
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 39
Server version: 5.0.45 Source distribution

Type 'help;' or '\h' for help. Type '\c' to clear the buffer
mysql> 
```

按照提示输入 root 用户的 MySQL 密码。（如果没有设置密码，你可以跳过 `-P` 选项。）出现 `mysql>` 提示符，准备接受操作本地主机上 mysql 默认数据库的命令。如果你正从另一台主机计算机连接到 MySQL 服务器，请在命令行中添加 `-h hostname`（其中 `hostname` 是运行 MySQL 服务器的计算机的名称或 IP 地址）。请记住，无论当前登录的是哪个 Linux 登录帐户，你都可以使用任何创建的有效 mysql 登录进行登录。

> **注意：** 你可以但*不建议*通过在 `mysql` 命令行末尾附加 `-P` 选项（例如，`-PMys/Password`）来直接输入密码。虽然这样可以省去单独输入密码的步骤，但它可能会向那些有权访问你机器的人暴露你的密码。

正如 MySQL 监视器欢迎文本所指出的，请确保输入的每一条命令都以分号（`;` 或 `\;`）结尾。如果你输入了一条命令，而它似乎正在等待更多输入，那很可能是因为你忘记在末尾加分号。

在开始使用 `mysql` 接口创建数据库之前，请尝试使用 `status` 命令检查 MySQL 服务器的状态。以下是 `status` 命令输出示例：

```
mysql> status
--------------------------
mysql  Ver 14.12 Distrib 5.0.45, for redhat-linux-gnu (i386) using readline 5.0

Connection id: 26
Current database: mysql
Current user: root@localhost
Current pager: stdout
Using outfile: ''
Server version: 5.0.45
Protocol version: 10
Connection: Localhost via UNIX socket
Server charset: latin1
Db charset: latin1
Client charset: latin1
Conn. charset: latin1
UNIX socket: /var/lib/mysql/mysql.sock
Uptime: 1 day 2 hours 57 min 19 sec

Threads: 1 Questions: 136 Slow queries: 0 Opens: 12
Flush tables: 1 Open tables: 6 Queries per second avg: 0.001
```

状态信息告诉你 MySQL 服务器的版本（14.12）和发行版（5.0.45）。输出还提醒了你当前的数据库（`mysql`）和你的用户名（`root@localhost`）。你可以看到服务器运行了多长时间（`Uptime`）。你还可以看到当前有多少活动线程，以及已执行了多少条查询该服务器的命令（`Questions`）。

## 使用 mysql 创建数据库
