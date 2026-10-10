
```bash
# mysqladmin -u root -p version proc
Enter password: ******
mysqladmin  Ver 8.4.2 Distrib 5.1.39, for redhat-linux-gnu on i386
Copyright (C) 2000-2008 MySQL AB, 2008 Sun Microsystems, Inc.
This software comes with ABSOLUTELY NO WARRANTY. This is free software, and you are welcome to modify and redistribute it under the GPL license

Server version		5.1.39
Protocol version	10
Connection		Localhost via UNIX socket
UNIX socket		/var/lib/mysql/mysql.sock
Uptime:			2 days 10 hours 47 min 35 sec

Threads: 2  Questions: 184  Slow queries: 0  Opens: 15  Flush tables: 1  Open tables: 8  Queries per second avg: 0.25
--------------------------------------------------
| Id | User | Host | db | Command | Time | State | Info |
--------------------------------------------------
| 3  | root | localhost | | Query | 0 | | show processlist |
--------------------------------------------------
```

此处显示的 `mysqladmin` 的每个选项都提供有用的信息。版本信息显示 `mysqladmin` 的版本为 8.4.2，并且分配给此 MySQL 服务器发行版的编号为 5.1.39。二进制软件包是为 i386 处理器上的 Linux/GNU PC 版本创建的。到服务器的连接是通过本地主机上的 UNIX 套接字（`/var/lib/mysql/mysql.sock`）进行的。服务器已运行 2 天 10 小时 47 分钟 35 秒。统计数据显示，当前有一个线程（到服务器的连接）处于活动状态。共有 184 个请求发送到服务器。

`proc` 选项显示当前有一个客户端连接到服务器。该客户端以 root 用户身份登录到本地主机的 MySQL。具有 Id 为 3 的客户端（这告诉您用户是谁，允许您作为服务器管理员使用该信息断开用户连接）正在查询 MySQL 数据库。

如果此刻服务器未运行，前一个示例中显示的 `mysqladmin` 命令将导致失败消息：

```bash
mysqladmin: connect to server at 'localhost' failed.
```

建议的补救方法是尝试重启服务器（通过输入 `service mysqld restart`）。

### 获取更多 MySQL 软件包

虽然本章主要关注从命令行使用和管理 MySQL 数据库，但也有一些图形工具可用于处理 MySQL 数据库。特别是，`mysql-administrator` 软件包包含用于连接到 MySQL 服务器的 GUI 软件。要安装 `mysql-administrator` 软件包，请以 root 用户身份输入以下内容：

```bash
# yum install mysql-administrator
```

如果您熟悉 MySQL，您可以直接使用 MySQL Administrator 连接到您的 MySQL 数据库（假设它已在运行）。如果您对 MySQL 是新手，我建议您遵循本章中的操作步骤，以熟悉 MySQL 的工作方式以及如何从命令行使用它。

要启动 MySQL Administrator，请输入 `mysql-administrator`。如果您的 MySQL 数据库服务器正在运行（如本章后面所述），请输入服务器主机名（例如 `localhost`）、用户名（例如 `root`）和密码。MySQL Administrator 窗口将显示，如图 23-1 所示。

![Figure 23-1](img/c78bdcb5b7842a0d73dcc98921f872a2_868_0.png)

**图 23-1：使用 MySQL 管理员窗口连接到你的 MySQL 数据库。**

此时，你可以使用 MySQL 管理员窗口来查找有关 MySQL 服务器的信息，备份和恢复数据，或者选择“目录（Catalogs）”以显示每个数据库的信息。你甚至可以选择“健康（Health）”选项来查看有关服务器机器活动和使用情况的各种信息。（如果你想尝试另一种图形化 MySQL 实用工具，请查看 `mysql-query-browser` 软件包。该工具专为设计 MySQL 表和运行查询而制作。）

## 配置 MySQL 服务器

与 Fedora 中的大多数服务器软件一样，MySQL 服务器依赖启动脚本和配置文件来提供服务。服务器活动会记录在 `/var/log` 目录下的 `mysqld.log` 文件中。还有用于管理 MySQL 活动的 `mysql` 用户和组账户。以下各节将描述这些组件如何协同工作。

### 使用 mysql 用户/组账户

安装 MySQL 软件时，它会自动创建一个 `mysql` 用户账户和一个 `mysql` 组账户。这些用户和组账户被分配给 MySQL 文件和活动。这样，某人就可以管理 MySQL 服务器，而无需拥有 root 权限。

`mysql` 用户条目在 `/etc/passwd` 文件中显示如下：

```
mysql:x:27:482:MySQL Server:/var/lib/mysql:/bin/bash
```

刚才显示的 `mysql` 条目表明，`mysql` 用户的 UID 为 27，GID 为 482。识别此用户账户的文本字符串是 `MySQL Server`。主目录是 `/var/lib/mysql`，默认 shell 是 `/bin/bash`。识别出的主目录将包含为你定义的 MySQL 服务器每个数据表持有的目录。

`mysql` 的组条目更简单。`/etc/group` 文件中的以下条目表明 `mysql` 组的组 ID（GID）为 482。

```
mysql:x:482:
```

如果你关心与 MySQL 相关的文件的所有权，你会发现大多数这些文件都将 `mysql` 指定为拥有每个文件的用户账户和组账户。这使得由 `mysql` 用户运行的守护进程能够访问数据库文件。

### 添加管理用户

要管理 MySQL，你必须至少拥有一个管理账户。默认情况下，root 用户对你的 MySQL 服务器数据库拥有完全访问权限，并且没有分配密码。一旦 `mysqld` 服务器正在运行，你可以使用 `mysqladmin` 命令为 root 用户分配密码。要将 root 用户添加为 MySQL 管理员，请登录为 root 用户，并从终端窗口输入以下任一命令（替换为你自己的主机名和密码）：

```
# mysqladmin -u root password 'myownpassw'
# mysqladmin -u root -h myhost.example.com password 'myownpassw'
```

> **提示：** 如果你的密码中包含也被 shell 解释为元字符的字符，请将密码包含在引号中。

运行此命令后，MySQL root 用户可以使用密码运行任何 MySQL 管理命令。如果你忘记了或重置了你的 MySQL 密码，请参阅此处信息：`http://dev.mysql.com/doc/refman/5.0/en/resetting-permissions.html`。

MySQL 维护一个与操作系统维护的列表不同的用户和密码列表。如果在命令行中没有提供用户名（如上所示的 `-u root`），MySQL 假设你想使用当前的 Fedora 用户名登录到 MySQL。然而，你仍然需要提供该用户的 MySQL 密码（而不是 Fedora 密码）才能使用 MySQL 服务。

要进行 MySQL 管理，只需在你要运行的 MySQL 命令的命令行中添加 `-u root` 参数。在创建 MySQL 账户之后，Linux root 用户与 MySQL root 用户账户之间没有关联。通常你会为这两个账户使用不同的密码。

**提示：** 为了避免每次运行 MySQL 客户端命令时都要输入密码的麻烦，你可以在其中一个选项文件的 `[client]` 组下添加一个密码选项。最安全的方法是创建 root 用户主目录中的一个 `.my.cnf` 文件，该文件只能由 root 访问（`chmod 600 /root/.my.cnf`），并包含以下行（将显示的最后参数替换为你的密码）：
