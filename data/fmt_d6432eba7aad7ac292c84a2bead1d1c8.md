
# sendmail 邮件投递与配置

## 投递到本地系统

默认情况下，`sendmail` 将投递给本地用户的邮件投递到他们的邮件堆池目录 `/var/spool/mqueue`，并采用 `mbox` 格式。在该目录中，每个用户都有一个以用户名命名的邮件文件。邮件保留在这些文件中，直到被收集（通常由 MUA 收集）。一旦 MUA 从邮件堆池中收集了邮件，MUA 将用户指定的邮件存储在（通常是）用户的目录。

## 投递到非本地系统

`sendmail` 处理投递到非本地系统邮件的方案取决于其配置方式：它可以将邮件发送到 `smarthost`，可以将邮件发送到目标域名 DNS MX 记录所指向的系统，也可以拒绝发送该邮件。

## mbox 与 maildir

`mbox` 格式将用户的所有消息存储在一个文件中。为了防止损坏，进程在文件中添加或删除消息时必须锁定该文件；因此，MUA 不能在 MTA 添加消息的同时删除消息。另一种竞争格式 `maildir` 将每条消息存储在单独的文件中。这种格式不使用锁，允许 MUA 在邮件投递到同一用户用户的同时，删除该用户的消息。此外，`maildir` 格式能够更好地处理更大的信箱。缺点是当你使用 IMAP 等协议检查消息时，`maildir` 格式会增加开销。`dovetail` 包同时支持 `mbox` 和 `maildir` 格式。`Qmail`（见第 732 页）作为 `sendmail` 的替代方案仅支持 `maildir` 格式。

![](img/1e024b9f135a8b3cebc6731238212d84_787_0.png)

## 邮件日志

`sendmail` 守护进程将日志消息存储在 `/var/log/maillog`。其他邮件服务器（如 `Dovecot`）也可能将信息记录在此文件中。以下是一个日志条目示例：

```
/var/log/maillog
Dec 14 15:27:37 sendmail[4466]: oBenbP2Q004446:
to=<msgs@sobell.com> ctladdr=<sams@example.com> (500/500)
delay=00:00:02, xdelay=00:00:02, mailer=relay, pri=120289,
smtp.smtp.com [72.143.213], dsn=2.0.0, stat=OK
id=1PSSeq-001Um-3e
```

每个日志条目以时间戳、发送端系统名称、邮件服务器名称（`sendmail`）和一个唯一标识码开头。接收者地址位于 `tos` 标签之后，发送者地址紧随其后。附加字段提供了邮件器的名称和发送消息所需。如果邮件发送正确，`stat` 标签后跟随 `Sent`。

当 `sendmail` 发送邮件时，该邮件被标记为 `Sent`；`Sent` 并不表示消息已投递。如果由于下游错误导致邮件未投递，用户通常会收到一封邮件告知其未投递以及原因。

有关日志文件的更多信息，请参阅 `sendmail` 文档。如果你发送和接收大量邮件，`maillog` 文件可能会变得很大。`logrotate`（见第 621 页）的 syslog 条目会定期存档并轮转这些文件。

## 别名与转发

你可以使用 `aliases`、`~/forward`（见第 737 页）和 `virtualable`（见第 743 页）文件来转发邮件。第 743 页的表 20-1 对比了这三个文件。

大多数情况下，你发送邮件是给特定个人的；接收者 `user@system` 映射到指定系统上的真实用户。有时，你可能希望发送给一类用户而不是特定的接收者。类的示例使用了 `postmaster`、`webmaster` 和 `tech_support`。不同用户可能在不同时间收到此邮件，或者邮件可能会发送一组用户。你可以使用 `/etc/aliases` 将本地地址和类映射到用户、文件、命令以及非本地地址。

`/etc/aliases` 中的每行都包含一个本地（伪）用户的名称，后面跟着冒号、空格和逗号分隔的目标列表。默认安装包含许多别名，它们将某些伪匿名用户的消息重定向到 `root`。它们的格式如下所示：

```
adm:
```

向 `root` 账户发送消息是使之易于检查的良好方法。但是，由于 `root` 账户很少被检查，你可能想将副本发送给真实用户。你可以设置别名来将邮件转发给多个用户。或者，你也可以简单地在 `aliases` 的末尾添加以下行（顺序很重要）。此行将所有发送到本地系统的邮件除了发送到 `root` 之外还发送到：`abuse: root, sam, max`。

你可以使用这种别名创建简单的邮件列表。例如，以下别名会将本地系统发送的每封邮件的副本发送给几个用户，包括位于不同系统上的 Zach：`admin: sam, helen, zach@example.com`。

你可以通过在命令前加上管道符 (`|`) 来将邮件直接重定向到命令的标准输入。这种技术常被 `Mailman` 等邮件列表软件使用。对于每个列表，`Mailman` 在 `aliases` 文件中维护条目，例如用于 `painting_class` 的条目：`painting_class: "/var/lib/mailman/mail/painting_class"`。

在编辑 `/etc/aliases` 后，你必须以 `root` 权限运行 `newaliases` 或重启 `sendmail` 以重新创建 `sendmail` 读取的 `/etc/aliases.db` 文件。你可以使用 `newaliases` 列出当前 `sendmail` 创建的条目：

```
newaliases | head -5
abuse: root
amanda:
```

此行将所有发送到本地系统的邮件除了 `root` 之外还发送到：`abuse: root, sam, max`。

别名在很多情况下很有用，但你可能想将副本发送给真实用户。你可以设置别名来将邮件转发给多个用户。

```
cat ~/.forward
example.com
sam
```

## 相关程序

`sendmail` 软件包包含几个程序。主程序 `sendmail` 从标准输入读取并发送到参数指定的接收者。参见第 734 页的示例。命令 `apropos sendmail` 显示与 `sendmail` 相关的文件和实用。

`mailq` 工具显示输出队列的状态。当队列没有消息时，它报告队列为空。除非是暂时的，队列中的消息通常意味着本地或远程 MTA 配置存在网络问题。

```
mailq
/var/spool/mqueue is empty
Total requests: 0
```

`mailstats` 工具报告了自第一行显示的日期以来 `sendmail` 发送和接收的消息数量和大小：

```
# mailstats
Statistics from Fri Dec 24 16:02:34 2010
M msgsfr bytes_from msgsto bytes_to msgsrej msgsdis Mailer
M 0 0 OK 17181 103904K 0
4 368386 4216634K 136456 1568314K 20616 0 esmtp
9 226151 26101632K 239235 12776528K 4590 0 local
T 594537 3031976K 632662 14448746K 25206 0
C 694638 499700
```

在上述输出中，每个邮件器通过第一列（显示邮件器编号）和最后一列（显示邮件器名称）来标识。第二列到第五列显示了邮件器发送和接收的消息数和总大小。第六列和第七列显示被拒绝和丢弃的消息数。以 `T` 开头的行列列总量，以 `C` 开头的行显示 TCP 连接数。

## 配置 sendmail

`sendmail` 配置文件位于 `/etc/mail`，其中主配置文件是 `sendmail.cf`。该目录包含其他文本配置文件，例如 `access`、`mailertable` 和 `virtusetable`。`sendmail` 守护进程并不读取这些文件，而是读取同一目录下的 `*.db` 文件。

你可以使用 `makemap` 或在 `/etc/mail` 目录下执行 `make` 命令来生成 `*.db` 文件，尽管这一步通常不是必要的：当你运行 `sendmail` 初始化脚本（第 733 页）时，它会自动生成它们。

## sendmail.mc 与 sendmail.cf

`sendmail.cf` 文件并非供直接编辑，其中包含一个针对此的大型警告：

```
$ cat /etc/mail/sendmail.cf
######################################################################
####
##### 不要编辑此文件！只编辑源 .mc 文件。
#####
######################################################################
```
