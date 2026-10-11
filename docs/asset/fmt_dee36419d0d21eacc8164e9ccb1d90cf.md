
```
-rw-r--r-- root root 1756 Aug 14 08:48 file1
-rw-r--r-- root root 160 Aug 14 08:48 file2
-rw-r--r-- root root 1039996 Aug 14 08:39 file3
drwxr-xr-x 2 root root 4096 Aug 14 08:50 stuff
226 Directory send OK.
ftp>
```

上述输出显示了三个文件和一个子目录。要将 `file3` 下载到本地计算机的当前目录，可以使用以下命令：

```
ftp> get file3
local: file3 remote: file3
227 Entering Passive Mode (192,168,0,1,137,36)
150 Opening BINARY mode data connection for file3(1039996 bytes).
226 Transfer complete.
ftp>
```

同样，要将远程计算机上的当前目录更改为 `/root/`，并将本地计算机当前目录下的 `file4` 副本上传到那里，同时查看结果并退出 `ftp` 实用程序，您可以在 `ftp` 提示符使用以下命令：

```
ftp> cd stuff
250 Directory changed.
ftp> pwd
257 "/root"
ftp> put file4
227 Entering Passive Mode (192,168,0,1,70,35)
150 Opening BINARY mode data connection for file4.
226 Transfer complete.
ftp> ls
227 Entering Passive Mode (192,168,0,1,70,35).
150 Here comes the directory listing.
total 2064
-rw-r--r-- root root 1756 Aug 14 08:48 file1
-rw-r--r-- root root 160 Aug 14 08:48 file2
-rw-r--r-- root root 1039996 Aug 14 08:39 file3
drwxr-xr-x 2 root root 4096 Aug 14 08:50 stuff
226 Directory send OK.
ftp> bye
221 2.0 Goodbye
```

### 电子邮件服务

除了使用 浏览器或命令行 `FTP` 外，许多 Linux 发行版默认不安装电子邮件守护进程。因为 `systemd` 需要发送电子邮件，您必须安装邮件传输代理（MTA）。MTA 负责接收、路由和递送邮件。常用的 MTA 是 `Postfix`，它默认配置在端口 `25` 接收邮件。要测试这一点，可以使用 `telnet` 命令连接端口 `25`，如下所示：

```
[root@server1]# telnet localhost 25
Connected to localhost.
Escape character is '^
220 server1.class ESMTP Postfix
EHLO sample.com
250-server1.class
250-PIPELINING
250-SIZE 102400
250-VRFY
250-ETRN
250-ENHSTATUS
250-8BITIME
250-DSN
quit
221 2.0 Goodbye
Connection closed by foreign host.
[root@server1]#
```

MTA 负责处理递邮件。要发送和接收邮件，您需要一个邮件用户代理（MUA）。MUA 是您用于与电子邮件交互的软件。从远程服务器检索邮件，MUA 使用 `POP3` 或 `IMAP` 等邮件访问协议。`POP3`（邮局协议第三版）从服务器下载邮件并通常会删除。`IMAP`（互联网消息访问协议）允许您在服务器上管理邮件。

要在本地 Linux 系统上检查邮件，可以使用 `mail` 命令，如下：

```
[root@server1]# mail
Mail version 8.1.2/01/15/2019. Type ? for help.
"/var/spool/mail/root": 13 messages 6 ten unread
U 1 Cron Daemon Sat Jul 11 07:01 26/9881 "Cron"
U 2 logwatch@localhost.l Mon Jul 20 11:43 42/1528 "Logwatch"
U 3 logwatch@localhost.l Tue Jul 21 12:32 151/4669
N 4 jason.eckert@trios.com Wed Sep 29 15:53 11/430
& 4:
Message 4:
From jason.eckert@trios.com Wed Sep 29 15:53:25 2019
Return-Path: <jason.eckert@trios.com>
Date: Wed, 29 Sep 2019 15:52:36 -0400
From: jason.eckert@trios.com
Status: R
```

Hey dude

```
& q
[root@server1]#
```

## 712 第 13 章 配置网络服务和云技术

注意

`mail` 命令是第 1 章中描述的邮件代理（MUA）的一个示例。

每个用户的电子邮件都存储在 `/var/sp/mail` 目录下以用户命名的文件中。

例如，用户 `bob` 的邮件将存储在 `/var/sp/mail/bob` 文件中。

要转发电子邮件，用户可以创建一个 `~/.forward` 文件，列出目标邮箱地址。发送给该用户的任何邮件将自动转发到目标邮箱地址。

`mailq` 命令可用于排查邮件投递。默认情况下，`mailq` 显示所有等待投递的邮件以及未投递的原因。

`/etc/aliases` 文件包含了用于标识系统上不同用户的其他电子邮件。从所示 `/etc/aliases` 文件条目中，你可以使用 `postmaster`、`bin`、`daemon` 或 `root` 来引用 root 用户。

```
[root@server1 ~]# head-17 /etc/aliases
# See man 5 aliases for format
postmaster: root
bin: root
daemon: root
adm: root
[root@server1 ~]# _
```

如果你修改了 `/etc/aliases` 文件，需要运行 `newaliases` 命令以便根据 `/etc/aliases` 文件中的条目重新构建别名数据库（`/etc/aliases.db`）。`Postfix` 守护仅使用别名数据库。

虽然 `Postfix` 通常配置为接受和路由本地邮件，但你也可以将邮件转发到互联网上的其他服务器，并使用 `POP` 和 `IMAP` 接受来自网络的连接。要做到这一点，你必须编辑其配置文件：`/etc/postfix/main.c`。至少应修改或添加的一组常用行如表 13-4 所示。

| 表 13-4 配置 Postfix 时需要修改或添加的 /etc/postfix/main.c 示例行 |

| :--- | :--- |

| 行 | 更改 |

| mydomain = sample.com | 设置邮件域名；更改为所需的名称 |

| myorigin = $mydomain | 设置对该域名的本地访问 |

| inet_interfaces = all | 配置 Postfix 在所有接口上监听邮件 |

| mydestination = $myhostname, localhost.$mydomain, $mydomain | 配置邮件的目标域名 |

| mynetworks_style = class | 信任来自本地网络计算机的邮件 |

### 数据库服务

数据库是以后表格形式存储重要信息的大文件。表格将信息组织成列表。在列表中，关于特定项目的一组信息被称为记录（record）。例如，在客户邮寄地址列表中，单条记录包含客户的姓、名、街道地址、城市和邮政编码。记录中的各种信息类别称为字段（fields）。例如，在我们的客户邮寄地址示例中，一个字段包含城市信息，依此类推。

大多数数据库由几十个或数百个表组成，存储应用程序使用的信息。在大型数据库中，某些表中的信息可以与同一数据库中其他表中的信息相关。这些数据库通过关系型数据库链接，其中的表通常通过共同字段链接。

图 13-8 显示了一个包含两个具有相关 `EmployeeID` 字段表的简单关系型数据库。

| EmployeeID | FirstName | LastName | Address | ZIP | Home Phone | Mobile Phone |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
