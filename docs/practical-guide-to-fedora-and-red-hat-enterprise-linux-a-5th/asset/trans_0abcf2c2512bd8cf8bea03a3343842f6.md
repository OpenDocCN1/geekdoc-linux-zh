
## 前提条件

安装以下软件包：

- `sendmail`（必需）
- `sendmail-cf`（配置 `sendmail` 时必需）
- `squirrelmail`（可选；提供 Webmail，见第 686 页）
- `spamassassin`（可选；提供垃圾邮件过滤功能，见第 682 页）
- `mailman`（可选；提供邮件列表支持，见第 688 页）
- `dovecot`（可选；提供 IMAP 和 POP 入站邮件服务器守护进程）

运行 `chkconfig` 以便在系统进入多用户模式时启动 `sendmail`（默认情况下，`sendmail` 不会在单用户模式下运行）：

```bash
# /sbin/chkconfig sendmail on
```

启动 `sendmail`。由于 `sendmail` 通常正在运行，您需要重启它以使 `sendmail` 重新读取其配置文件。即使 `sendmail` 未运行，以下重启命令也能正常工作——它只是无法关闭 `sendmail`：

```bash
# /sbin/service sendmail restart
Shutting down sm-Client: [ OK ]
Shutting down sendmail: [ OK ]
Starting sendmail: [ OK ]
Starting sm-Client: [ OK ]
```

运行 `chkconfig` 以便在系统进入多用户模式时启动 SpamAssassin 守护进程 `spamd`（在此配置中通常会安装 SpamAssassin）：

```bash
# /sbin/chkconfig spamassassin on
```

与 `sendmail` 类似，SpamAssassin 通常也在运行。重启它以便 `spamd` 重新读取其配置文件：

```bash
# /sbin/service spamassassin restart
Stopping spamd: [ OK ]
Starting spamd: [ OK ]
```

IMAP 和 POP 协议由多个守护进程实现。有关这些守护进程及其启动方法的信息，请参见第 689 页。

## 注意事项

- **防火墙**
  SMTP 服务器通常使用 TCP 端口 25。如果运行 SMTP 服务器的系统启用了防火墙，您需要打开此端口。使用防火墙配置窗口中的“信任服务”选项卡（见第 824 页），勾选标有 *Mail (SMTP)* 的复选框以打开此端口。有关更通用的信息，请参见详细介绍 `iptables` 的第 25 章。

- **cyrus**
  本章涵盖 `dovecot` 软件包中包含的 IMAP 和 POP3 服务器。Fedora/RHEL 还在 `cyrus-imapd` 软件包中提供了 IMAP 和 POP3 服务器。

## 更多信息

- **sendmail**: www.sendmail.org
- IMAP: www.imap.org
- IMAP 和 POP3: www.dovecot.org
- IMAP 和 POP3: cyrusimap.web.cmu.edu
- SquirrelMail: www.squirrelmail.org
- Postfix: www.postfix.org/docs.html（替代 MTA，见第 691 页）
- Qmail: qmail.area.com
- Mailman: www.list.org
- **procmal**: www.procmal.org
- SpamAssassin: spamassassin.org
- 垃圾邮件数据库: razor.sourceforge.net

## 快速上手 1：配置客户端上的 sendmail

**您可能不需要配置 sendmail 来发送电子邮件**

在 **sendmail** 正在运行的情况下，执行第 673 页“测试”部分中描述的命令。只要 **sendmail** 能够向外连接到端口 25，您就不需要按照本节所述设置 **sendmail** 使用 SMTP 中继。如果您收到了测试发送的邮件，可以跳过本节。

此快速上手配置了一个出站 **sendmail** 服务器。该服务器

- 使用远程 SMTP 服务器（通常是 ISP）将出站电子邮件中继到其目的地（SMTP 中继）。
- 仅向 SMTP 服务器发送源自本地系统的电子邮件。它不转发源自其他系统的电子邮件。
- 不处理入站电子邮件。正如常见的情况一样，您需要使用 POP 或 IMAP 来接收电子邮件。

要设置此服务器，您必须编辑 /etc/mail/sendmail.mc 并重启 **sendmail**。

`sendmail.mc` 中下一行开头的 `dnl` 表示该行是注释：

```
dnl define(`SMART_HOST', `smtp.your.provider')dnl
```

您可以忽略行尾的 `dnl`。要指定远程 SMTP 服务器，您必须在编辑器中打开 `sendmail.mc` 并修改上述行，删除行首的 `dnl`，并将 `smtp.your.provider` 替换为您 ISP 的 SMTP 服务器的 FQDN（请向您的 ISP 获取此名称）。请小心不要更改行中的反引号 (` ` `) 和单引号 (` ' `)。如果您的 ISP 的 SMTP 服务器位于 `smtp.myisp.com`，您将把该行更改为

```
define(`SMART_HOST', `smtp.myisp.com')
```

## 不要更改反引号 (`) 或单引号 (')

请小心不要更改 **sendmail.mc** 任何行中的反引号 (`) 或单引号 (')。这些符号控制 `m4` 预处理器如何将 **sendmail.mc** 转换为 **sendmail.cf**。如果您未保留这些符号，**sendmail** 将无法正常工作。

当您重启它时，**sendmail** 会由您编辑的 **sendmail.mc** 文件重新生成 **sendmail.cf** 文件：

```bash
# /sbin/service sendmail restart
```

使用以下命令测试 **sendmail**：

```bash
$ echo "my sendmail test" | /usr/sbin/sendmail user@remote.host
```

将 *user@remote.host* 替换为 *另一台系统* 上您接收电子邮件的地址。您需要向远程系统发送电子邮件，以确保 **sendmail** 正在中继您的电子邮件。

## 快速上手 2：配置服务器上的 SENDMAIL

如果您希望接收发送至您拥有的注册域名的入站电子邮件，您需要将 **sendmail** 设置为入站邮件服务器。此快速上手描述了如何设置此类服务器。该服务器

- 仅接受来自本地系统的出站电子邮件。
- 直接交付出站电子邮件至收件人系统，而不使用中继。
- 接受来自任何系统的入站电子邮件。

此服务器不中继源自其他系统的出站电子邮件。如果您希望本地系统充当中继，请参阅第 680 页的“access: 设置中继主机”。为了让此配置工作，您必须能够发出对端口 25 的出站连接并接受针对端口 25 的入站连接。

**sendmail.mc** 中将 **sendmail** 限制为仅接受来自本地系统入站电子邮件的行是

```
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```

要允许 **sendmail** 接受来自其他系统的入站电子邮件，请从上一行中移除参数 **Addr=127.0.0.1**：

```
DAEMON_OPTIONS(`Port=smtp, Name=MTA')dnl
```

默认情况下，**sendmail** 不使用远程 SMTP 服务器来中继电子邮件，因此无需更改任何设置即可使 **sendmail** 直接发送电子邮件到收件人系统。（快速上手 1 设置了 **SMART_HOST** 以中继电子邮件。）

一旦您重启了 sendmail，只要 DNS MX 记录（见第 780 页）指向本地系统，它就会接受发送给本地系统的邮件。如果您没有运行 DNS 服务器，您必须要求您的 ISP 设置一个 MX 记录。

## SENDMAIL 的工作原理

- **出站电子邮件**
  当您发送电子邮件时，MUA 将电子邮件传递给 sendmail，sendmail 会在 /var/spool/mqueue（邮件队列）目录中创建两个文件，在 sendmail 处理该消息期间存储消息。为了为特定的电子邮件创建唯一的文件名，sendmail 会生成一个随机字符串，并在与该电子邮件相关的文件名中使用该字符串。sendmail 守护进程将消息主体存储在一个名为 `df`（数据文件）后跟生成字符串的文件中。它将在名为 `qf`（队列文件）后跟生成字符串的文件中存储头部和其他信息。

  如果发生交付错误，sendmail 会创建消息的临时副本，并将其存储在以 `tf`（临时文件）开头的文件中，并在以 `xf` 开头的文件中记录错误。一旦电子邮件成功发送，sendmail 会从 /var/spool/mqueue 中删除与该电子邮件相关的所有文件。

- **入站电子邮件**
  默认情况下，MDA 将在邮件池目录 /var/spool/mail 中用户的文件里以 mbox 格式存储传入的消息。在此目录中，每个用户都有一个以该用户的用户名命名的邮件文件。邮件保留在这些文件中，直到被收集，通常由 MUA 收集。一旦 MUA 从邮件池中收集了邮件，MUA 会按照用户的指示存储邮件，通常位于用户的家目录层次结构中。

- **mbox 与 maildir**
  mbox 格式将所有用户的消息存储在单个文件中。为防止损坏，当进程向文件添加消息或从文件中删除消息时，该文件必须被锁定；您不能在 MTA 正在添加消息的同时删除消息。一种竞争格式 maildir 将每条消息存储在单独的文件中。此格式不使用锁，允许 MUA 在新邮件交付的同时读取和删除消息。此外，maildir 格式更能处理更大的邮箱。缺点是在使用 IMAP 等协议检查消息时，maildir 格式会增加开销。`dovecot` 软件包支持 mbox 和 maildir 格式。Qmail（见第 691 页），sendmail 的替代品，使用 maildir 格式的邮箱。

## 邮件日志

sendmail 守护进程将日志消息存储在 /var/log/maillog 中。其他邮件服务器，如 dovecot 的 `imap-login` 和 `pop3-login` 守护进程，也可能将信息记录到该文件中。以下是一个日志条目示例：

```bash
/var/log/maillog # cat /var/log/maillog
...
Mar 3 16:25:33 MACHINENAME sendmail[7225]: i23GPXvm0#7224: to=<user@localhost.localdomain>, ctIaddr=<root@localhost.localdomain> (0/0), delay=00:00:00, xdelay=00:00:00, mailer=local, pri=30514, dsn=2.0.0, stat=Sent
```
