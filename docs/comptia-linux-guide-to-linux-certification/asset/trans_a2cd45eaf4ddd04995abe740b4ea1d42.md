

## 配置 PostgreSQL

PostgreSQL 是一个强大的 SQL 服务器，提供了许多功能。尽管许多 Linux 服务器发行版允许您在 Linux 安装过程中安装 PostgreSQL SQL，但您也可以在之后轻松地从软件存储库中安装它。在安装过程中，PostgreSQL 安装程序会在 `/etc/passwd` 和 `/etc/shadow` 文件中创建一个名为 `postgres` 的用户，其主目录为 `/var/lib/postgresql`，外壳为 `/bin/bash`。

接下来，您可以按照以下步骤准备使用 PostgreSQL：

-   使用 `passwd postgres` 命令为 `postgres` 用户设置密码。
-   可选修改 PostgreSQL 配置文件 `postgresql.conf`。该文件的位置因 Linux 发行版而异，但通常存储在 `/var/lib/postgresql` 目录或 `/etc/postgresql` 目录下。
-   启动 PostgreSQL 守护进程并将其配置为在启动时自动运行。

### 配置 PostgreSQL 数据库

要配置 PostgreSQL 数据库，您必须先以 `postgres` 用户身份登录。然后，您可以执行几个 PostgreSQL 命令行实用程序之一来创建和管理数据库。这些命令总结在表 13-6 中。

例如，以 `postgres` 用户登录后创建一个名为 `sampled` 的数据库，您可以使用以下命令：

```
[root@server1 -]$ createdb sampledb
[root@server1 -]$
```

| 命令 | 描述 |
| --- | --- |
| clusterdb | 将 PostgreSQL 数据库关联到另一台服务器上的数据库 |
| createdb | 创建 PostgreSQL 数据库 |
| createlang | 允许新的编程语言与 PostgreSQL 一起使用 |
| createuser | 创建 PostgreSQL 用户 |
| dropdb | 删除 PostgreSQL 数据库 |
| droplang | 移除 PostgreSQL 中对编程语言的支持 |
| dropuser | 删除 PostgreSQL 用户 |
| pg_dump | 备份 PostgreSQL 数据库设置 |
| pg_dumpall | 备份 PostgreSQL 数据库集群设置 |
| pg_restore | 恢复 PostgreSQL 数据库设置 |
| psql | PostgreSQL 实用程序 |
| reindexdb | 重新索引 PostgreSQL 数据库 |
| vacuumdb | 分析并重新生成内部 PostgreSQL 数据库统计信息 |

**表 13-6** *PostgreSQL 命令行实用程序*

接下来，您可以运行 **psql** 命令，使用交互式 PostgreSQL 实用程序连接到 `employee` 数据库，在那里您可以获取有关可执行大多数数据库管理任务的 SQL 和 psql 命令的信息。

```
[root@server1 ~]$ psql sampledb
psql (9.3.4)
Type "help" for help.

sampledb=# help
You are using psql, the command-line interface to PostgreSQL.
Type: \copyright for distribution terms
     \h for help with SQL commands
     \? for help with psql commands
     \q or terminate with semicolon to execute query
     \q to quit

sampledb=#
```

您可以使用适当的 SQL 语句在 PostgreSQL 实用程序中创建表并添加记录。以下输出展示了如何：1) 创建一个名为 "employee" 的表，该表包含三个字段（Name、Dept、Title），每个字段允许 20 个字符的信息；2) 添加三条员工记录；以及 3) 显示结果。

```
sampledb=# CREATE TABLE employee (Name char(20), Dept char(20), Title char(20));
CREATE TABLE
sampledb=# INSERT INTO employee VALUES ('Jeff Smith','Research','Analyst');
INSERT 0 1
sampledb=# INSERT INTO employee VALUES ('Mary Wong','Accounting','Manager');
INSERT 0 1
sampledb=# INSERT INTO employee VALUES ('Pat Clarke','Marketing','Coordinator');
INSERT 0 1
sampledb=# SELECT * from employee;
```

| name | dept | title |
|---|---|---|
| Jeff Smith | Research | Analyst |
| Mary Wong | Accounting | Manager |
| Pat Clarke | Marketing | Coordinator |

(3 rows)

```
sampledb=#
```

![](img/c27875544958897d817484d558c208c8_634_0.png)

**注意**

在 PostgreSQL 实用程序中输入的每条 SQL 语句必须以 `;` 元字符结尾。

除了 SQL 语句之外，PostgreSQL 实用程序还有许多内置命令。这些命令以 `\` 字符开头，可用于获取数据库信息或在 PostgreSQL 实用程序内执行功能。最常见的这些内置命令列在表 13-7 中。

| 命令 | 描述 |
|---|---|
| \l | 列出可用数据库 |
| \c database_name | 连接到不同的数据库 |
| \d | 列出当前数据库中的表 |
| \d table_name | 列出表中的字段 |
| \q | 退出 PostgreSQL 实用程序 |

**表 13-7** 常见的内置 PostgreSQL 实用程序命令

### 章节摘要

-   DHCP、DNS、NTP 和 NIS 被称为基础设施服务，因为它们为网络上的其他计算机提供网络相关服务。
-   DHCP 服务器向其他计算机租用 IPv4 或 IPv6 配置。两种最常见的 DHCP 服务器是 `dhcpd` 和 `udhcpd`。
-   DNS 服务器为网络上的其他计算机提供名称解析服务。每个 DNS 服务器可以包含几个区域，这些区域存储可解析名称的资源记录。
-   Linux 计算机可以使用存储在计算机 BIOS 中的系统时间，或者从网络中的 NTP 服务器获取时间。NTP 服务器从一个由多个层级组成的层次化组织中的其他 NTP 服务器获取时间。两种最常见的 NTP 服务器是 `ntpd` 和 `chronyd`。
-   NIS 服务器向配置为 NIS 客户端的其他 Linux 计算机提供如 `/etc/passwd` 和 `/etc/shadow` 等关键配置文件。
-   Apache 服务器使用 HTTP 协议将其文档根目录中的网页共享给网络上的计算机。
-   Samba 可用于使用 SMB 协议向 Linux、UNIX、Macintosh 和 Windows 计算机共享文件。
-   NFS 可用于在 Linux、UNIX 和 Macintosh 系统之间原生共享文件。NFS 客户端通过挂载 NFS 服务器上的共享目录来访问这些文件。
-   FTP 可用于向任何拥有 FTP 客户端实用程序的计算机共享文件，并且是互联网上最常见的文件共享方法。现代 Linux 系统上最常见的 FTP 守护进程是 `vsftpd`。
-   邮件服务器将电子邮件从一个用户投递到系统中的另一个用户。它们还接受来自用户的新邮件并将其中继到互联网上的其他邮件服务器进行投递。Linux 系统上最常用的邮件服务器是 Postfix。

许多大型应用程序将其数据存储在数据库服务器上的数据库中。这些应用程序使用 SQL 语句在跨网络的数据库中添加入、操作和检索信息。PostgreSQL 是一种常见的数据库服务器，提供了高级配置和实用程序。

## 关键术语

**ab (Apache benchmark) 命令** 一个可用于获取如 Apache 等 Web 服务器性能基准的命令。

**apachectl 命令** 一个可用于启动、停止和重启 Apache Web 服务器以及检查 Apache 配置文件中语法错误的命令。

**Berkeley Internet Name Domain (BIND)** 所有 DNS 服务器和 DNS 配置文件都遵循的标准。

**BIND 配置实用程序** 一个可用于生成和修改 DNS 名称守护程序所使用的文件的图形化实用程序。

**BusyBox DHCP 守护进程 (udhcpd)** 一个轻量级 Linux 守护进程，用于向网络上的其他计算机提供 IPv4 地址。

**Chrony NTP 守护进程 (chronyd)** 一个在 Linux 计算机上提供快速时间同步服务的守护进程。

**chronync 命令** 一个可用于查询 NTP 服务器或客户端状态以及将系统时间与 NTP 服务器同步的命令。

**curl 命令** 一个可用于从 Web 服务器获取网页的命令。

**数据库** 一个包含组织成表格的数据的文件。

**日期与时间实用程序** Fedora 20 中的一个图形化实用程序，可用于设置系统的日期、时间和时区信息。

**DHCP 守护进程 (dhcpd)** 用于向网络上的其他计算机提供 IPv4 和 IPv6 地址的最常见的 Linux 守护进程。

**指令** 配置文件中的一行。

**文档根目录** Web 服务器上存储 Web 内容以分发给 Web 浏览器的目录。

**DNS 缓存文件** 包含顶级 DNS 服务器 IP 地址的文件。

**dumpleases 命令** 一个可用于从 BusyBox DHCP 守护进程 (udhcpd) 获取当前 DHCP 租约的命令。

**导出** 使用 NFS 将目录共享给其他计算机。

**字段** 数据库表中记录内的属性。

**文件传输协议 (FTP)** 用于在诸如互联网等网络上传输文件的最常见的协议。

**正向查找** 一种 DNS 名称解析请求，其中 FQDN 被解析为 IP 地址。

