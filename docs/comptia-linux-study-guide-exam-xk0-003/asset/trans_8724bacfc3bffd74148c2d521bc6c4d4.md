
管理访问无需密码。若要设置密码，请键入以下命令：

```
$ mysqladmin -u root password newpassword
```

当然，请将 newpassword 更改为您想要使用的密码。如果您的系统已经设置了 root 密码，您可以使用另一个命令来更改它：

```
$ mysqladmin -u root -p'oldpassword' password newpassword
```

某些发行版（例如 Ubuntu）包含安装脚本，在安装软件时会提示您输入 MySQL root 密码。因此，您可能不需要键入这些命令。

通常，MySQL 是使用 SysV 启动脚本（例如 /etc/init.d/mysqld）来启动和停止的。第 4 章更详细地介绍了 SysV 启动脚本，如果您需要帮助来启动或停止 MySQL，请参阅该章节。您可以使用 ps 来验证 MySQL 是否正在运行；搜索名为 mysqld 的进程：

```
# ps ax | grep mysql
1948 ? S 0:00 /bin/sh /usr/sbin/mysqld_safe
2013 ? S1 33:30 /usr/sbin/mysqld --basedir=/usr\
--datadir=/var/lib/mysql --user=mysql --pid-file=/var/run/mysql/mysqld.pid
--skip-locking --port=3306 --socket=/var/run/mysql/mysql.sock
2014 ? S 0:00 logger -p daemon.err -t mysqld_safe -i -t mysql
30933 pts/0 S+ 0:00 grep mysql
```

在这个例子中，/usr/sbin/mysqld 程序是 MySQL 服务器，因此它肯定正在运行。此输出还显示了用于启动该程序的选项。此查询还发现了另外三个与 MySQL 相关的进程，包括用于搜索 MySQL 的 grep 命令。请确保你找到了 mysqld（守护进程，其名称以 d 结尾）；mysql 程序是客户端，即使服务器没有运行，它也可能正在运行。如果您找不到正在运行的 MySQL 守护进程，请尝试使用其 SysV 启动脚本，如果失败，请搜索您的日志文件以查找启动服务器时可能出错的原因。

## 测试 MySQL 连接

为了测试 MySQL 的基本操作，您应首先确保服务器正在运行，如上所述。然后您可以启动 SQL 客户端。对于 MySQL 而言，这个程序被称为 mysql：

```
$ mysql
```

如果客户端能够连接到服务器，您将看到一个 mysql> 提示符。如果服务器未运行或无法联系，您将看到一条错误消息。要验证 mysql 客户端与其服务器的连接状态，您可以使用 STATUS 命令：

```
mysql> STATUS;
--------------------------
mysql Ver 14.12 Distrib 5.0.51a, for debian-linux-gnu (x86_64) using readline 5.2

Connection id:			29
```

还会出现几行额外的状态信息。您可以浏览这些内容以了解更多细节，例如正在使用的服务器版本以及其已运行了多长时间。

如果您刚刚安装了 MySQL，可能没有定义任何数据库。要了解定义了什么，您可以使用 SHOW DATABASES 命令：

```
mysql> SHOW DATABASES;
+--------------------+
| Database			|
+--------------------+
| information_schema |
+--------------------+
1 row in set (0.00 sec)
```

这些操作应该足以验证 MySQL 的基本功能。不过，您可能无法轻松进入，特别是如果您使用除 MySQL 服务器运行所在计算机以外的其他计算机来测试服务器操作。（如果网络操作在您的安装中很重要，您绝对应该测试网络访问，以确保防火墙或其他网络问题不会导致问题。）如果您收到“无法连接到 MySQL 服务器”的消息，那么 MySQL 服务器可能没有运行，或者网络配置正在阻止对服务器的访问。如果您收到“访问被拒绝”的消息，问题在于身份验证——您必须指定合法的帐户和密码。

要连接到远程服务器、使用特定的 MySQL 帐户或发送特定的 MySQL 密码，您必须分别使用 --host（或 -h）、--user（或 -u）或 --password（或 -p）选项。例如，要以密码 e4bUg7TQ 连接到在 third.luna.edu 上运行的 MySQL 服务器上的 dbuser，您可能键入以下内容：

```
$ mysql --host=third.luna.edu -u dbuser -pe4bUg7TQ
```

![](img/9903a4d3f7abd8dcbef1035fa04a3406_542_0.png)

使用长选项名称时，您必须在选项名称及其值之间包含等号，如本例中的 --host 选项所示。短选项形式不使用等号。对于密码，您不能在短选项名称（-p）和密码之间包含空格。您可能更喜欢使用长形式（如 --password=e4bUg7TQ）以提高可读性。如果您包含 -p 选项但省略密码，mysql 会提示您输入。

## 摘要

网络服务器多种多样，Linux 提供了处理所有常见网络协议的程序。这些包括用于配置客户端网络设置的 DHCP，用于解析主机名和 IP 地址的 DNS，用于管理网络时间的 NTP，用于与 Windows 进行文件共享的 SMB/CIFS，用于与 Linux 和 Unix 进行文件共享的 NFS，用于跨平台文件传输的 FTP，用于网络浏览的 HTTP，用于跨平台 GUI 访问的 VNC，用于推送电子邮件的 SMTP，用于拉取电子邮件的 POP 和 IMAP，以及用于数据库访问的 SQL。

尽管这些服务器共享某些共同特征，例如可以通过 SysV 启动脚本或超级服务器启动，但每个协议和服务器都是独特的。事实上，对于许多协议，有多种服务器可用，并且每个服务器都可以有自己独特的配置风格。因此，您必须研究您安装和运行的每个服务器，以确定如何最好地管理它。

## 考试要点

- 解释 Samba 和 NFS 最适合部署在哪里。Samba 是 SMB/CIFS 协议套件的实现，最常用于 Windows 系统的文件和打印机共享；因此，Samba 最适合作为 Windows 客户端的服务器。相比之下，NFS 是作为 Unix 系统的文件共享协议设计的，因此最适合用于与 Unix 或 Linux 客户端共享文件。

- 描述 Samba 和 NFS 配置文件。Samba 通过 smb.conf 进行配置，通常存储在 /etc/samba 或 /etc/samba.d 中。全局 Samba 选项出现在 [global] 部分，后续部分定义特定的共享。NFS 通过 /etc/exports 进行配置，其中列出了要导出的目录，每行一个。每行还包含可以挂载该导出的计算机或网络列表，以及挂载选项。

**总结 FTP 和 HTTP 之间的区别。** 文件传输协议 (FTP) 是一种基于登录的协议，用于传输文件。超文本传输协议 (HTTP) 通常不需要登录（尽管一些网站确实实现了登录功能）。FTP 是一种旧协议，有一些怪癖，例如需要使用两个网络连接。万维网（简称为 WWW 或 Web）建立在 HTTP 之上，使 HTTP 成为当今互联网上极其重要的协议。

**描述常见的 Web 服务器脚本工具。** 通用网关接口 (CGI) 是一种通用机制，使 Web 服务器能够运行普通的 Linux 程序或脚本（用 Perl、Python、C 或 Linux 支持的任何其他语言编写）以动态生成 Web 页面。PHP 和 Tomcat 是更专门化的语言，专为 Web 使用而设计。它们在 Samba 中需要额外的配置，但对于 Web 目的可能更容易编程。

**解释 rdesktop 和 VNC 的用途。** `rdesktop` 程序 enables 访问提供 Windows 特有的远程桌面协议 (RDP) 用于远程登录访问的 Windows 计算机。VNC 可以填充类似的角色，但 VNC 是一个跨平台工具；服务器可以运行 Windows、Mac OS、Linux 或各种其他操作系统。

**描述 SQL 和 MySQL 的用途。** 结构化查询语言 (SQL) 是一种常见的数据库语言；它用于存储可由个人或程序检索的数据。SQL 是支持网络的，这意味着数据库用户可以存在于托管数据库的计算机之外的其他计算机上。MySQL 是 Linux 上 SQL 的常见实现；它包括客户端、服务器和支持程序。

