

# 启用 chkconfig mysqld

这会将 `mysqld` 设置为在大多数多用户运行状态（级别 3、4 和 5）期间启动。要检查服务是否已针对这些级别启用，请在终端窗口中输入 **chkconfig --list mysqld**。

# 检查 MySQL 服务器是否正在运行

您可以使用 `mysqladmin` 或 `mysqldshow` 命令来检查 MySQL 服务器是否正在运行。以下是如何使用 `mysqladmin` 命令检查 MySQL 服务器信息的示例。

```bash
# mysqladmin -u root -P version proc
Enter password: ********
MySQLadmin  Ver 8.23 Distrib 3.23.58, for redhat-linux-gnu on i386
Copyright (C) 2000 MySQL AB & MySQL Finland AB & TCX DataKonsult AB
This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL license

Server version		3.23.58
Protocol version		10
Connection		Localhost via UNIX socket
UNIX socket		/var/lib/mysql/mysql.sock
Uptime:			2 day 10 hours 47 min 35 sec

Threads: 1  Questions: 184  Slow queries: 0  Opens: 1  Flush tables: 3
Open tables: 1 Queries per second avg: 0.001

+----+------+-----------+------+---------------------+------+------------------------+
| Id | User | Host      | db   | Command | Time | State | Info                 |
+----+------+-----------+------+---------------------+------+------------------------+
| 52 | root | localhost: |      | Query   | 0    |    | show processlist      |
+----+------+-----------+------+---------------------+------+------------------------+
```

此处显示的 `mysqladmin` 的两个选项均提供了有用的信息。版本信息显示 `mysqladmin` 的版本为 8.23，而该 `mysql` 服务器发行版编号为 3.23.58。二进制软件包是为 i386 处理器上的 Linux/GNU PC 版本创建的。与服务器通过本地主机上的 UNIX 套接字（`mysql_.sock`）连接。服务器已运行 2 天 10 小时 47 分 35 秒。统计数据显示，目前有一个线程（与服务器的连接）处于活动状态。共有 184 个请求发送给服务器。

`proc` 选项显示当前有一个客户端连接到服务器。该客户端以 root 用户身份登录到本地主机上的 MySQL。具有 Id 52 的客户端（这告诉您用户是谁，作为服务器管理员，如果您想断开用户连接，可以使用此信息）目前正在查询 MySQL 数据库。

如果服务器当前未运行，前一个示例中显示的 `mysqladmin` 命令将导致错误信息：
mysqladmin: 无法连接到本地主机 (`localhost`) 上的服务器。

建议的补救措施是尝试重新启动服务器（输入 `service mysql restart`）或确保套接字存在（`/var/lib/mysql/mysql.sock`）。

# 处理 MySQL 数据库

第一次启动 MySQL 服务器（使用前面描述的启动脚本）时，系统会为 MySQL 数据库创建初始权限表。它通过运行 `mysql_install_db` 命令来完成此操作。

`mysql_install_db` 命令为您启动了两个数据库：`mysql` 和 `test`。当您为这些数据库创建数据时，这些信息将分别存储在 `/var/lib/mysql/mysql` 和 `/var/lib/mysql/test` 目录中。

由于 MySQL 根用户不必是系统的根用户（只要您拥有 MySQL 根用户的密码），您可以以任何用户身份登录 Fedora。在以下示例中，请确保在运行显示的命令时提供 MySQL 根用户密码。

## 启动 `mysql` 命令

要开始创建数据库和表，您可以使用 `mysql` 命令。在任何终端窗口中，通过输入以下内容打开计算机上的 `mysql` 数据库：

```bash
$ mysql -u root -p mysql
Enter password: ********

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 39 to server version: 3.23.58

Type 'help;' or '\h' for help. Type '\c' to clear the buffer

mysql>
```

按照提示输入 root 用户的 MySQL 密码。（如果未设置密码，您可以跳过 `-p` 选项。）出现 `mysql>` 提示符，准备接受用于处理本地主机上 `mysql` 默认数据库的命令。如果您从另一台主机计算机连接到 MySQL 服务器，请在命令行中添加 `-h hostname`（其中 `hostname` 是运行 MySQL 服务器的计算机的名称或 IP 地址）。请记住，无论您当前登录的是哪个 Linux 登录账户，您都可以使用创建的任何有效 `mysql` 登录名进行登录。

正如 MySQL 监视器的欢迎文本所注意到的，请务必以分号 (;) 或 \g 结尾每个您输入的命令。如果您输入一个命令后它似乎正在等待更多输入，这通常是因为您忘记在末尾添加分号。

在使用 `mysql` 接口创建数据库之前，请尝试使用 status 命令检查 MySQL 服务器的状态。以下是 status 命令输出的一个示例：

```mysql
mysql> status
--------------------
mysql  Ver 11.18_Distrib 3.23.58, for pc-linux-gnu (i686)
Connection id:          43
Current database:       mysql
Current user:           root@localhost
Current pager:          stdout
Using outfile:          ''
Server version:         3.23.58
Protocol version:       10
Connection:             localhost via UNIX socket
Client character-set:   latin1
Server character-set:   latin1
UNIX socket:            /var/lib/mysql/mysql.sock
Uptime:                 1 day 2 hours 57 min 19 sec

Threads: 1  Questions: 136  Slow queries: 0  Opens: 12
Flush tables: 1  Open tables: 6 Queries per second avg: 0.001
--------------------
```

状态信息告诉您 MySQL 服务器的版本（11.18）和发行版（3.23.58）。输出还提醒您当前的数据库（`mysql`）和您的用户名（`root@localhost`）。您可以查看服务器已运行多长时间（Uptime）。您还可以查看当前有多少线程处于活动状态以及已经执行了多少命令来查询此服务器（Questions）。

## 使用 mysql 创建数据库

在交互式 `mysql` 会话中，您可以创建和修改数据库和表。如果您尚未连接到 `mysql` 会话，请键入以下命令（假设 `mysql` 用户名为 root）：

```bash
$ mysql -u root -p
Enter password: ********
mysql>
```

创建 MySQL 数据库的一般步骤包括创建数据库名称，将新数据库标识为当前数据库，创建表，以及向表中添加数据。在连接到 mysql> 会话时，您可以运行以下过程来创建一个示例数据库。

1. 要创建新的数据库名称，请在 mysql> 提示符下使用 CREATE DATABASE 命令。例如，要创建一个名为 allusers 的数据库，请键入以下内容：
   ```mysql
   mysql> CREATE DATABASE allusers;
   ```
   此操作会在 /var/lib/mysql 目录中创建一个名为 allusers 的数据库。（虽然您不必对上面显示的命令使用大写字母，但这有助于将命令与数据库实体区分开来。）

   > **注意：** 或者，您可以使用 mysqladmin 命令从命令行创建数据库。例如，要使用 mysqladmin 创建名为 allusers 的数据库，您可以键入以下内容：`mysqladmin -u root -p create allusers`

2. 要查看您的 mysql 服务器可用的数据库，请在 mysql> 命令提示符下键入以下内容：
   ```mysql
   mysql> SHOW DATABASES;
   +--------------------+
   | Database           |
   +--------------------+
   | allusers           |
   | mysql              |
   | test               |
   +--------------------+
   3 rows in set (0.00 sec)
   ```
   此处显示的数据库名为 allusers、mysql 和 test。allusers 数据库是在上一步中创建的。mysql 数据库包含用户访问数据。test 数据库是自动创建的，用于创建测试 mysql 数据库。

3. 要处理您刚刚创建的数据库（allusers），您需要将 allusers 设置为当前数据库。为此，请在 mysql> 命令提示符下键入以下内容：
   ```mysql
   mysql> USE allusers;
   Database changed
   ```

4. 为数据库创建表需要一些规划和理解表语法。您可以键入以下命令和列信息来尝试创建表。有关创建表和使用不同数据类型的更详细信息，请参阅本章后面的“理解 MySQL 表”部分。
   要创建一个名为 names 的表，请在 mysql> 提示符下使用以下 CREATE TABLE 命令：
   ```mysql
   mysql> CREATE TABLE names (
   -> firstname varchar(20) not null,
   ```

