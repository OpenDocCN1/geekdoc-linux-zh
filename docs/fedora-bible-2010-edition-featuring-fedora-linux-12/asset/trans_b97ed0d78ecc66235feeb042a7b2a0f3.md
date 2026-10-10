
如果默认设置不够用，请重新配置您站点的 sendmail 安装。第三个软件包包含文档文件，有助于解释当前版本的一些细节。

sendmail 二进制软件包包含在 Fedora 发行版中。sendmail 和 sendmail-cf 软件包位于随本书附带的 Fedora DVD 上。要从 Fedora 安装所有三个软件包，请运行以下命令：

```
# yum install sendmail sendmail-cf sendmail-doc
```

由于 sendmail 是入侵者的常见目标，在继续操作之前，立即申请可用的 sendmail 更新是个好主意。您可以使用 yum 命令或 PackageKit 实用工具来完成此操作。要使用 yum 更新 sendmail，请输入：

```
# yum update "sendmail*"
```

## Fedora 的其他邮件服务器

sendmail 的开源版本并不是 Fedora 系统可用的唯一邮件服务器，但确实是最常见的。以下列表描述了其他服务器，并提供了获取更多信息的 URL：

- **Postfix** — 与 sendmail 一样，Postfix MTA 也包含在 Fedora 中。由 Wietse Venema（以 tcp_wrappers 闻名）编写，这个免费邮件服务器在设计时考虑了安全性，并且大多数功能都在受限的 chroot 环境中以非特权用户身份执行。该服务器包含十多个小型程序（每个执行简单且不同的任务）以及几个单一用途的队列。您可以在 [www.postfix.org](http://www.postfix.org) 找到更多信息和源代码。

- **Exim** — Exim MTA 是一个在 Linux 和其他 UNIX 系统上运行的免费邮件服务器（基于 GPL 协议）。Exim 包含在 Fedora 发行版中。该 MTA 包括用于检查和路由邮件的灵活功能。请从 Exim 主页（[www.exim.org](http://www.exim.org)）了解有关 Exim 的更多信息。

- **Qmail** — 同样将安全视为高优先级，这个邮件服务器（由 Daniel J. Bernstein 编写）提供安全可靠的邮件传输、邮箱配额、虚拟域和反垃圾邮件功能。更多信息可从 [www.qmail.org/top.html](http://www.qmail.org/top.html) 获取。

- **Smail** — Smail 提供与 sendmail 许多相同的功能，但配置稍简单且所需内存较少。Smail 最适合中小型邮件服务器。Smail 项目页面位于 [www.weird.com/~woods/projects/smail.html](http://www.weird.com/~woods/projects/smail.html)。源代码可从 [ftp://ftp.planix.com/pub/Smail/](ftp://ftp.planix.com/pub/Smail/) 下载。

## 启动 sendmail

安装后，sendmail 服务默认已启用，尽管它只接受在本地系统上发送的传入邮件。若要立即启动 sendmail，您可以重启机器，或者只需运行 `service sendmail start` 来启动服务器。启动和停止 sendmail 的过程与其他服务器进程类似。

默认情况下，sendmail 接收的传入消息会被处理并存储在 `/var/spool/mail` 目录中。此目录中的每个文件代表本地机器上的一个有效用户名。文件会在第一次向该用户发送电子邮件时（或者如果文件缺失）自动创建。拥有登录账户的人使用此目录及其用户账户名作为其传入邮箱（例如，`/var/spool/mail/johnq`）。

传出消息在等待发送时放在 `/var/spool/mqueue` 目录中。此目录中的文件名遵循一致的命名方案。前两个字符指示文件中存储的数据类型（见表 18-1）。后续字符构成基于处理该消息的 sendmail 进程的 PID 的唯一随机标识符。

### 表 18-1: /var/spool/mqueue 中的文件前缀

| 文件名前缀 | 存储的数据类型 |
| :---- | :---- |
| qf | 构成电子邮件消息主体的数据。 |
| qf | 包含消息头和其他管理细节的队列控制文件。 |
| tf | qf 文件的临时副本，如果在投递过程中发生错误则创建。 |
| xf | 尝试发送消息时生成的任何错误消息。 |

## 其他程序

发行版中包含其他几个可执行程序。这些程序在表 18-2 中有描述。

### 表 18-2: 其他相关的 sendmail 程序

| 程序 | 描述 |
| :---- | :---- |
| mailq | 显示等待在邮件队列中处理的消息摘要（该命令等同于 `sendmail -bp`）。 |
| mailstats | 显示消息数量和字节数统计信息。 |
| makemap | 将文本文件（`/etc/mail/virtuser table`）转换为哈希化的 Berkeley 数据库（`/etc/mail/virtuser table.db`）。此命令在 sendmail 脚本每次启动时运行。 |
| newaliases | 将纯文本 `/etc/aliases` 文件转换为哈希化的 Berkeley 数据库文件 `/etc/aliases.db`（该命令等同于 `sendmail -bi`）。 |
| praliases | 打印出在 `/etc/aliases` 中定义的所有别名。 |
| procmail | 未包含在 sendmail 软件包中，但用作 sendmail 的 MDA。（它包含在 Fedora 的 procmail 软件包中。） |
| purgestat | 清除存储主机状态信息的目录。该命令等同于 `sendmail -bH`，默认情况下是禁用的。 |
| rmail | 通过 UUCP（Unix to Unix Copy）处理传入邮件。 |
| smrsh | 实现一个受限 shell，用于从 sendmail 运行程序。 |

## sendmail 执行的日志记录

sendmail 执行的日志记录量可以在 `sendmail.mc` 文件中配置，但默认级别提供了对信息通知和错误消息的良好覆盖。默认情况下，syslog 设施配置文件（`/etc/syslog.conf`）指示 syslog 将来自 sendmail 的日志信息存储在 `/var/log/maillog` 文件中。本节显示了该文件的一些示例。

每次守护进程启动时（这也会导致哈希别名数据库重新生成），类似以下信息的消息会写入 `/var/log/maillog` 文件：

```
May 16 12:52:40 toys sendmail[1758]: alias database /etc/aliases rebuilt by root
May 16 12:52:40 toys sendmail[1758]: /etc/aliases: 63 aliases, longest 10 bytes, 625 bytes total
May 16 12:52:40 toys sendmail[1787]: starting daemon (8.14.3): SMTP+queueing@01:00:00
```

每次发送或接收消息时，都会创建一个日志文件条目：

```
May 16 12:54:34 toys sendmail[1120]: OAA01120: from=root, size=161, class=0, pri=3 0161, nrcpts=1, msgid=<199907191254.OAA01120@toys.linuxtoys.net>, relay=root@localhost
May 16 12:54:35 toys sendmail[1127]: OAA01120: to=jkpat, ctagid=root (0/0), delay=00:00:01, xdelay=00:00:00, mailer=local, stat=Sent
```

除了显示正常的邮件服务器活动外，日志还显示人们试图闯入您的邮件服务器。`wiz` 和 `debug` 命令是在早期版本的 sendmail 中实现的，被发现是一个巨大的安全问题。您可能会看到日志文件条目，例如以下代码示例所示，这是恶意人员检查您是否运行了易受攻击的 sendmail 守护进程。此外，`expn` 和 `vrfy` 命令（可以通过配置选项禁用）可能会泄露比您愿意分发的更多信息。

```
May 16 13:03:27 toys sendmail[699]: NOQUEUE: "wiz" command from localhost [127.0.0.1] (127.0.0.1)
May 16 13:03:29 toys sendmail[699]: NOQUEUE: "debug" command from localhost [127.0.0.1] (127.0.0.1)
May 16 13:03:37 toys sendmail[701]: NOQUEUE: localhost [127.0.0.1] :
     expn oracle
May 16 13:03:43 toys sendmail[702]: NOQUEUE: localhost [127.0.0.1] :
     vrfy oracle
```

## 配置 sendmail

要配置 sendmail 设施，您编辑 `/etc/mail` 和 `/etc` 中的配置文件，这些文件随后被 sendmail 启动脚本用于生成数据库文件。反过来，这些数据库文件被 sendmail 守护进程用于控制您的 sendmail 服务器的行为。一旦配置了 sendmail，您可以开始添加用户账户以在服务器上拥有邮箱。本节中我描述的 sendmail 配置的一般步骤是：

- **获取域名**：您需要一个唯一的互联网域名分配给您的邮件服务器。您可以从许多不同的地方购买互联网域名，然后让您的域名 DNS 邮件交换（MX）记录指向您正在创建的邮件服务器。

- **配置基本 sendmail 设置**：在此步骤中，您编辑 `/etc/mail/sendmail.mc` 文件。该文件定义了其他配置和日志文件的位置，以及允许您配置 sendmail 守护进程的一些行为。

- **定义传出邮件访问**：与您的邮件服务器相关的最关键安全问题是其接受转发到其他邮件服务器哪些邮件消息。通过编辑 `/etc/mail/access` 文件，您可以指示您的服务器将从哪些主机和用户接受用于本地投递或转发的邮件。

- **配置虚拟服务器**：默认情况下，sendmail 假设您正在为服务器所属域的邮件服务器进行设置。要使单台计算机上的 sendmail 成为多个域的邮件服务器（称为虚拟服务器），您需要在 `/etc/mail/local-host-names` 文件中定义每个域名。（`local-host-names` 文件在 sendmail 软件包中。不过，它初始是空的。）

- **配置虚拟用户**：使用 `/etc/mail/virtusertable` 配置文件，您可以指示 sendmail 守护进程如何处理它接收到的为其配置要处理的指定用户和域的邮件。此文件为您提供很大的灵活性，可以将发给特定用户的邮件引导到特定邮箱，转发到不同的邮件地址，或以各种方式拒绝该邮件。virtusertable 文件在 sendmail 软件包中，尽管最初只包含注释。

- **添加用户账户**：对于默认的 sendmail 安装，您需要为每个在您的邮件服务器上拥有邮箱的用户添加一个用户账户。

- **启动 sendmail 并生成数据库文件**：启动 sendmail 服务会导致两个主要操作发生：它运行 sendmail 服务器守护进程，并且如果您安装了 sendmail-cf 软件包，它将您的配置文件编译为数据库文件，从而
