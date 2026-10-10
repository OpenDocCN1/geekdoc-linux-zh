
服务器名称、一个冒号以及 VNC 会话编号。例如，你可能输入以下命令：

```
$ vncviewer bluebox.luna.edu:1
VNC server supports protocol version 3.8 (viewer 3.3)
Password:
```

如果你输入了正确的密码，`vncviewer` 会在终端中显示更多文本，并打开一个窗口显示远程计算机的桌面。许多其他操作系统也有可用的 VNC 客户端；请查阅原始 VNC 或 TightVNC 网站以了解这些客户端。这些非 Linux 的 VNC 客户端与 Linux VNC 客户端的工作方式非常相似，但它们更侧重于使用对话框来输入服务器的主机名和密码。

VNC 的一个重要缺点是，用户通常必须在服务器计算机上启动 VNC 服务器，然后才能在客户端计算机上运行 VNC 客户端程序。在某些情况下，这一要求并不是主要问题。例如，如果你正坐在工作站前，并且知道近期内需要从另一个位置使用该工作站，你可以在离开工作站之前启动服务器。但在其他情况下，你可能需要使用文本模式登录工具登录到 VNC 服务器计算机，以启动 VNC 服务器。此过程需要两次登录，这很麻烦。更重要的是，这意味着你必须在服务器计算机上运行两个登录协议，从而增加了其安全暴露面。

## 部署 MySQL

结构化查询语言（SQL），如其全称所暗示的那样，是一种用于从数据库检索数据的语言。在实践中，SQL 在几种不同的数据库产品中实现。因此，你应该了解一下 Linux 上可用的 SQL 产品。安装了 SQL 软件包后，你就可以开始学习 SQL 使用原则并运行 SQL 产品。

### 选择 SQL 软件包

SQL 是一种访问数据的语言，而具体的 SQL 软件包则实现该语言。这种区别类似于网络协议（如 SMTP）与实现该协议的服务器（如 sendmail 和 Postfix）之间的区别。原则上，你可以使用任何 SQL 软件包来满足你的 SQL 数据库需求。在实践中，使用 SQL 存储数据的具体产品可能与特定软件包配合使用效果更好（甚至可能需要特定软件包）。Linux 中一些更常见的选择包括：

-   **MySQL**：Sun 公司拥有此 SQL 实现，并已在 GPL 许可下发布。大多数主要的 Linux 发行版都在其软件包数据库中包含 MySQL。对于完整安装，你可能需要安装多个软件包，如客户端、服务器以及可能的开发工具。你可以在 http://www.sun.com/software/products/mysql/ 了解更多。
-   **PostgreSQL**：此 SQL 实现源于早期的 Ingres 软件（名称 *PostgresSQL* 是 *post-Ingres SQL* 的压缩形式）。它基于 BSD 许可证提供，并且在大多数 Linux 发行版中作为多个软件包提供。与 MySQL 类似，你通常需要安装客户端、服务器以及可能的额外支持软件包。PostgreSQL 的总部网站是 http://www.postgresql.org。
-   **SQLite**：该软件包基于 http://www.sqlite.org，是一个实现 SQL 的库。因此，它不是一个独立的数据库；相反，它是作为一种为程序提供对程序内 SQL 数据库功能访问的方式而设计的。如果你安装了使用 SQLite 的程序，你的发行版的软件包管理器应该会为你安装相关的库。如果你想编写一个需要数据库访问的程序，又不想安装完整的客户端-服务器 SQL 软件包，如 MySQL 或 PostgreSQL，那么 SQLite 可能正是你需要的。

Linux 上有几十种其他 SQL 数据库产品。对于学习 SQL 来说，MySQL 或 PostgreSQL 就足以满足需求，或者如果你偏好其他完整的实现也可以使用。不过，如果你有使用 SQL 的具体目的，你应该更深入地研究 SQL 软件包。你可能需要特定的产品以保持与其他软件的兼容性，或者你需要一个提供特定功能的 SQL 软件包。Linux+ 考试目标仅按名称提及 MySQL。

正如刚刚提到的，一些 SQL 软件包，包括 MySQL 和 PostgreSQL，采用客户端-服务器模型：一个程序（服务器）管理数据库，而另一个程序（客户端）为用户提供对数据库的访问。此类实现可以跨网络运行，使多个客户端系统上的用户能够访问集中式的数据库服务器。

## 使用 MySQL

为了学习 SQL，你应该能够访问 SQL 数据库。为了演示目的，我以 MySQL 作为参考。其他 SQL 实现与我在这里描述的内容相似，但一些细节有所不同。从管理角度来看，你需要知道如何设置 MySQL 配置选项、如何启动和停止服务器，以及如何测试其是否正常工作。实际上使用 MySQL 执行数据库查询是一个复杂的主题，超出了本书或 Linux+ 考试的范畴。

## 配置、启动和停止 MySQL

MySQL 的主配置文件名为 *my.cnf*，通常存储在 `/etc` 或 `/etc/mysql` 中。你应该浏览此文件以熟悉一些关键的 MySQL 选项。不过，除非你知道需要更改默认设置，否则在初始阶段应谨慎更改此文件的内容。

你必须执行的一项初始配置任务是设置 MySQL 根密码。就像 Linux 本身一样，MySQL 需要一个管理员（root）用户；然而，MySQL 的 root 与 Linux 的 root 账户不同。默认的 MySQL 安装可能不需要密码即可进行管理员访问。要启用密码，请键入以下命令：

```
$ mysqladmin -u root password newpassword
```

当然，将 `newpassword` 更改为你想要使用的密码。如果你的系统已经设置了根密码，你可以使用另一个命令更改它：

```
$ mysqladmin -u root -p'oldpassword' password newpassword
```

![](img/a78bc63f22351f522ba5ec1fa0c060d2_540_0.png)

一些发行版，如 Ubuntu，包含安装脚本，在安装软件时会提示你输入 MySQL 根密码。因此，你可能不需要键入这些命令。

通常，MySQL 使用 SysV 启动脚本，如 `/etc/init.d/mysqlld`，进行启动和停止。第 4 章更详细地介绍了 SysV 启动脚本，因此如果你需要帮助启动或停止 MySQL，请查阅该章节。你可以使用 `ps` 验证 MySQL 是否正在运行；搜索名为 `mysqlld` 的进程：

```
# ps ax | grep mysql
1948 ? S 0:00 /bin/sh /usr/bin/mysqlld_safe
2013 ? S1 33:30 /usr/sbin/mysqlld --basedir=/usr --datadir=/var/lib/mysql --user=mysql --pid-file=/var/run/mysqlld/mysqlld.pid --skip-locking --port=3306 --socket=/var/run/mysqlld/mysqlld.sock
2014 ? S 0:00 logger -p daemon.err -t mysqlld_safe -i -t mysqlld
30933 pts/0 S+ 0:00 grep mysql
```

在此示例中，`/usr/sbin/mysqlld` 程序是 MySQL 服务器，因此它肯定正在运行。此输出还显示了用于启动该程序的选项。此查询还发现了其他三个与 MySQL 相关的进程，包括用于搜索 MySQL 的 `grep` 命令。务必找到 `mysqlld`（守护程序，其名称以 `d` 结尾）；`mysql` 程序是客户端，即使服务器未运行，它也可能在运行。如果你找不到正在运行的 MySQL 守护程序，请尝试使用其 SysV 启动脚本，如果失败，请搜索日志文件以查找启动服务器时可能出错的原因。

### 测试 MySQL 连接

为了测试 MySQL 的基本操作，你应首先确保服务器正在运行，如上文所述。然后你可以启动 SQL 客户端。对于 MySQL 来说，该程序名为 `mysql`：

```
$ mysql
```

如果客户端能够连接到服务器，你将看到 `mysql>` 提示符。如果服务器未运行或无法联系，你将看到错误消息。要验证 `mysql` 客户端与其服务器连接的状态，你可以使用 `STATUS` 命令：

```
mysql> STATUS;
---------------
mysql  Ver 14.12 Distrib 5.0.51a, for debian-linux-gnu (x86_64) using readline 5.2
Connection id:		29
```

还会出现几行额外的状态信息。你可以浏览这些信息以了解更多细节，例如正在使用的服务器版本以及其运行了多长时间。

如果你刚刚安装了 MySQL，可能没有定义任何数据库。要了解已定义的内容，你可以使用 `SHOW DATABASES` 命令：

```
mysql> SHOW DATABASES;
+--------------------+
| Database         |
+--------------------+
| information_schema |
+--------------------+
1 row in set (0.00 sec)
```

这些操作应该足以验证 MySQL 的基本功能。不过，你可能不会那么容易访问，特别是如果你使用除运行 MySQL 服务器的计算机以外的其他计算机来测试服务器操作。（如果你的安装中网络操作很重要，你绝对应该测试网络访问，以确保防火墙或其他网络问题不会导致问题。）如果你收到 `Can’t connect to MySQL server` 消息，那么很可能是 MySQL 服务器未运行或网络配置正在阻止对服务器的访问。如果你收到 `Access denied` 消息，问题在于身份验证——你必须指定合法的帐户和密码。

要连接到远程服务器、使用特定的 MySQL 帐户或发送特定的 MySQL 密码，你必须分别使用 `--host`（或 `-h`）、`--user`（或 `-u`）或 `--password`（或 `-p`）选项。例如，要以 `dbuser` 身份连接运行在 `third.luna.edu` 上的 MySQL 服务器，密码为 `e4blug7IQ`，你可能需要键入以下内容：

```
$ mysql --host=third.luna.edu -u dbuser -pe4blug7IQ
```

