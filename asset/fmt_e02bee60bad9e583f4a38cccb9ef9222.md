
```bash
$ echo "my sendmail test" | /usr/sbin/sendmail user@remote.host
```

将 `user@remote.host` 替换为 `另一台系统` 上您接收电子邮件的地址。您需要向远程系统发送电子邮件，以确保 `sendmail` 正在中继您的电子邮件。

## 快速上手 2：配置服务器上的 SENDMAIL

如果您希望接收发送至您拥有的注册域名的入站电子邮件，您需要将 `sendmail` 设置为入站邮件服务器。此快速上手描述了如何设置此类服务器。该服务器

- 仅接受来自本地系统的出站电子邮件。
- 直接交付出站电子邮件至收件人系统，而不使用中继。
- 接受来自任何系统的入站电子邮件。

此服务器不中继源自其他系统的出站电子邮件。如果您希望本地系统充当中继，请参阅第 680 页的“access: 设置中继主机”。为了让此配置工作，您必须能够发出对端口 25 的出站连接并接受针对端口 25 的入站连接。

`sendmail.mc` 中将 `sendmail` 限制为仅接受来自本地系统入站电子邮件的行是

```
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```

要允许 `sendmail` 接受来自其他系统的入站电子邮件，请从上一行中移除参数 `Addr=127.0.0.1`：

```
DAEMON_OPTIONS(`Port=smtp, Name=MTA')dnl
```

默认情况下，`sendmail` 不使用远程 SMTP 服务器来中继电子邮件，因此无需更改任何设置即可使 `sendmail` 直接发送电子邮件到收件人系统。（快速上手 1 设置了 `SMART_HOST` 以中继电子邮件。）

一旦您重启了 `sendmail`，只要 DNS MX 记录（见第 780 页）指向本地系统，它就会接受发送给本地系统的邮件。如果您没有运行 DNS 服务器，您必须要求您的 ISP 设置一个 MX 记录。

## SENDMAIL 的工作原理

- **出站电子邮件**

当您发送电子邮件时，MUA 将电子邮件传递给 `sendmail`，`sendmail` 会在 `/var/spool/mqueue`（邮件队列）目录中创建两个文件，在 `sendmail` 处理该消息期间存储消息。为了为特定的电子邮件创建唯一的文件名，`sendmail` 会生成一个随机字符串，并在与该电子邮件相关的文件名中使用该字符串。`sendmail` 守护进程将消息主体存储在一个名为 `df`（数据文件）后跟生成字符串的文件中。它将在名为 `qf`（队列文件）后跟生成字符串的文件中存储头部和其他信息。

如果发生交付错误，`sendmail` 会创建消息的临时副本，并将其存储在以 `tf`（临时文件）开头的文件中，并在以 `xf` 开头的文件中记录错误。一旦电子邮件成功发送，`sendmail` 会从 `/var/spool/mqueue` 中删除与该电子邮件相关的所有文件。

- **入站电子邮件**

默认情况下，MDA 将在邮件池目录 `/var/spool/mail` 中用户的文件里以 mbox 格式存储传入的消息。在此目录中，每个用户都有一个以该用户的用户名命名的邮件文件。邮件保留在这些文件中，直到被收集，通常由 MUA 收集。一旦 MUA 从邮件池中收集了邮件，MUA 会按照用户的指示存储邮件，通常位于用户的家目录层次结构中。

- **mbox 与 maildir**

mbox 格式将所有用户的消息存储在单个文件中。为防止损坏，当进程向文件添加消息或从文件中删除消息时，该文件必须被锁定；您不能在 MTA 正在添加消息的同时删除消息。一种竞争格式 maildir 将每条消息存储在单独的文件中。此格式不使用锁，允许 MUA 在新邮件交付的同时读取和删除消息。此外，maildir 格式更能处理更大的邮箱。缺点是在使用 IMAP 等协议检查消息时，maildir 格式会增加开销。`dovecot` 软件包支持 mbox 和 maildir 格式。Qmail（见第 691 页），`sendmail` 的替代品，使用 maildir 格式的邮箱。

## 邮件日志

`sendmail` 守护进程将日志消息存储在 `/var/log/maillog` 中。其他邮件服务器，如 `dovecot` 的 `imap-login` 和 `pop3-login` 守护进程，也可能将信息记录到该文件中。以下是一个日志条目示例：

```bash
/var/log/maillog # cat /var/log/maillog
...
Mar 3 16:25:33 MACHINENAME sendmail[7225]: i23GPXvm0#7224: to=<user@localhost.localdomain>, ctIaddr=<root@localhost.localdomain> (0/0), delay=00:00:00, xdelay=00:00:00, mailer=local, pri=30514, dsn=2.0.0, stat=Sent
```

## 别名与转发

三个文件可以转发电子邮件：`.forward`（第676页）、`aliases`（下文将讨论）和 `virtusertable`（第682页）。第682页的表20-1比较了这三个文件。

- **et/aliases** 大多数情况下，当你发送电子邮件时，它会发给特定的人；接收者 `user@system` 映射到指定系统上的一个具体的、真实用户。有时你可能希望电子邮件发送给一类用户，而不是特定的接收者。用户类别的示例包括 `postmaster`、`webmaster`、`root` 和 `tech_support`。不同的用户可能会在不同的时间收到这些电子邮件，或者电子邮件可能会由一组用户共同回复。你可以使用 `/etc/aliases` 文件将入站地址映射到本地用户、文件、命令和远程地址。

`/etc/aliases` 中的每一行包含一个本地伪用户名，后跟冒号、空白和一个以逗号分隔的目标列表。默认安装包含许多别名，将某些伪用户的消息重定向到 `root`。这些别名的形式如下：

```
system:	root
```

向 `root` 账户发送消息是一种很好的方法，便于审查。然而，由于 `root` 的电子邮件很少被检查，你可能希望将副本发送给真实用户。以下行将发往本地系统 `abuse` 的邮件转发给 `root` 和 `alex`：

```
abuse:	root, alex
```

你可以使用这种类型的别名创建简单的邮件列表。例如，以下别名将发往本地系统 `admin` 的所有电子邮件的副本发送给几个用户，包括在另一个系统上的 Zach：

```
admin:	sam, helen, mark, zach@tcorp.com
```

通过在目标地址处指定绝对路径名，你可以将电子邮件定向到文件。以下别名在较不负责任的系统管理员中相当流行，将发往 `complaints` 的电子邮件重定向到 `/dev/null`（第469页），在那里它们会消失：

```
complaints:	/dev/null
```

你也可以通过在前加管道字符（`|`）来将电子邮件发送到命令的标准输入。这种技术通常与邮件列表软件（如 Mailman，第688页）一起使用。对于它维护的每个列表，Mailman 在别名文件中都有条目，例如以下针对 `mylist` 的条目：

```
mylist:	"/usr/lib/mailman/mail/mailman post mylist"
```

- **newaliases**: 编辑 `/etc/aliases` 后，你必须运行 `newaliases` 作为 `root` 或重启 `sendmail` 以重新创建 `sendmail` 读取的 `aliases.db` 文件。

- **praliases**: 你可以使用 `praliases` 列出当前由 `sendmail` 加载的别名：

```
$ /usr/sbin/praliases | tail -5
vcsa:root
webalizer:root
wnn:root
www:webmaster
xfs:root
```

- **~/.forward**: 系统范围的别名在许多情况下都有用，但非 root 用户无法创建或修改它们。有时你可能希望转发你自己的邮件：也许你希望来自几个系统的邮件去往一个地址，或者你只是想在另一个办公室工作一周期间转发你的邮件。`~/.forward` 文件允许普通用户转发他们的电子邮件。

`.forward` 文件中的行与前面描述的别名文件的右列相同：目标每行列出一个，可以是本地用户、远程电子邮件地址、文件名或由管道字符（`|`）引导的命令。

你转发的邮件不会进入你的本地邮箱。如果你想转发邮件并在本地邮箱中保留副本，你必须指定本地用户名，并在其前面加上反斜杠以防止无限循环。以下示例将 Sam 的电子邮件发送给本地系统上的他自己以及 `tcporp.com` 系统上的他：

```
$ cat ~sam/.forward
sam@tcporp.com
\sam
```

## 相关程序
