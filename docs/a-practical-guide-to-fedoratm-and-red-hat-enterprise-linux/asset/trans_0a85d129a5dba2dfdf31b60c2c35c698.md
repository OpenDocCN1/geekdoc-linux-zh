
## 邮件日志

**sendmail** 守护进程将日志信息存储在 `/var/log/maillog` 文件中。其他邮件服务器（如 Dovecot）也可能将此文件作为日志记录目标。以下是一个日志条目的示例：

```
# cat /var/log/maillog
...
Jun 18 11:55:46 guava sendmail[12159]: r5IItJ1L500127: to=ogs@osbello.com, ctagdr=es@anguava.example.com (1000/1400), delay=00:00:01, xdelay=00:00:01, mailer=esmtip, pri=120315, relay=esm1-smt1-in-1.google.com, [74.125.129.27], dsn=2.0.0, stat=Sent (OK 1371581746 04s18594494pac.163 - gsmsp)
```

每个日志条目以时间戳开头，接着是发送邮件的**系统名称**、邮件服务器名称（**sendmail**）以及唯一的标识符。收件人的地址位于 **to**= 标签之后，发件人的地址位于 **from**= 标签之后。其他字段提供了邮件投递程序（mailer）的名称以及发送消息所花费的时间。如果消息发送成功，**stat**= 标签后面会跟随 **Sent**。

当 **sendmail** 发送消息时，该消息会被标记为 **Sent**；**Sent** 并不代表消息已投递。如果由于后续环节中发生错误导致消息未投递，发件人通常会收到一封邮件，告知该邮件未被投递并说明原因。

有关日志文件的更多信息，请参阅 **sendmail** 文档。如果你发送和接收大量邮件，**maillog** 文件可能会变得相当大。*logrotate*（第 618 页）的 syslog 条目会定期归档并轮换这些文件。

## 别名与转发

你可以使用 *aliases*、*~/.forward*（第 474 页）和 *virtusertable*（第 753 页）文件来转发邮件。第 753 页的表 20-1 比较了这三个文件。

大多数时候发送邮件时，邮件会发送给特定的人：收件人 **user@system** 映射到指定系统上的一个真实用户。然而，有时你可能希望邮件发送给一类用户，而不是某个特定收件人。用户类别的例子包括 **postmaster**、**webmaster**、**root** 和 **tech.support**。不同的用户可能在不同的时间接收此类邮件，或者邮件可能发送给一组用户。你可以使用 */etc/aliases* 文件将本地地址和用户类别映射到本地用户、文件、命令，以及本地和非本地地址。

*/etc/aliases* 文件中的每一行包含一个本地（伪）用户名称，后跟一个冒号、空白字符，以及逗号分隔的目标列表。默认安装中包含许多将特定伪用户消息重定向到 **root** 的别名。它们的格式如下：

```
adm:	root
```

向 *root* 账户发送消息是使其易于审阅的好方法。然而，由于 *root* 的邮件很少被查看，你可能希望将副本发送给一个真实用户。你可以设置一个别名，将邮件转发给多个用户。以下行将发送至本地系统 *abuse* 的邮件转发给 *sam* 和 *max*，同时也发送给 *root*：

```
abuse:	root, sam, max
```

将发送至许多特殊账户的邮件转发给 **root** 很常见。如果 Zach 需要阅读发送给 **root** 并转发过来的邮件，你可以逐个修复每个别名。或者，你可以简单地在 **aliases** 文件*末尾*添加以下一行（在此情况下，顺序很重要）。这一行将发送给 **root** 并转发过来的所有邮件转发给 Zach：

```
root:          zach
```

你可以使用这种类型的别名创建简单的邮件列表。例如，以下别名将发送至本地系统 **admin** 的所有邮件副本发送给包括 Zach 在内的多个用户，Zach 位于另一个系统上：

```
admin:        sam, helen, max, zach@example.com
```

你可以通过指定绝对路径名代替目标地址，将邮件定向到一个文件。以下别名在缺乏责任心的系统管理员中很流行，它将发送至 **complaints** 的邮件重定向到 /dev/null（第 503 页），邮件在那里消失：

```
complaints:      /dev/null
```

你还可以在命令前加上管道符号 (|)，将邮件发送至该命令的标准输入。Mailman（第 762 页）等邮件列表软件常用此技术。对于它维护的每个列表，Mailman 在 aliases 文件中有诸如 **painting_class** 的条目，如下所示：

```
painting_class:  "|/var/lib/mailman/mail/mailman post painting_class"
```

### newaliases

编辑 /etc/aliases 之后，你必须以 **root** 权限运行 **newaliases**，或者重启 **sendmail**，以重新创建 **sendmail** 读取的 /etc/aliases.db 文件。

### praliases

你可以使用 **praliases** 列出 **sendmail** 当前加载的别名：

```
# praliases | head -5
@: @
abuse: root
adm: root
amanda: root
daemon: root
```

### ~/.forward

系统范围的别名在许多情况下很有用，但**非 root** 用户无法创建或更改它们。有时你可能希望转发自己的邮件：也许你希望来自多个系统的邮件到达同一个地址，或者也许你想在另一个办公室工作时转发你的邮件。~/.forward 文件允许普通用户转发他们的电子邮件。

.forward 文件中的行与前面本部分中介绍的 aliases 文件的右列相同：目标每行列出一个，可以是本地用户、远程电子邮件地址、文件名或前面带有管道符号 (|) 的命令。你转发的邮件不会到达你的本地邮箱。如果你希望转发邮件并在本地邮箱中保留副本，必须指定你的本地用户名并在前面加上反斜杠，以防止无限循环。以下示例将 Sam 的电子邮件发送至本地系统上的 Sam 自身以及 example.com 系统上的 Sam：

```
$ cat ~/.forward
sams@example.com
\sam
```

## 相关程序

**sendmail** sendmail 软件包包含几个程序。主要程序 **sendmail** 从标准输入读取并发送电子邮件给参数指定的收件人。你可以从命令行使用 **sendmail** 来检查邮件投递系统是否正常工作，以及将脚本的输出通过电子邮件发送。示例请参见第 744 页。命令 **apropos sendmail** 显示与 **sendmail** 相关的文件和实用工具列表。

**mailq** **mailq** 实用工具显示发件邮件队列的状态。当队列中没有消息时，它报告队列为空。除非是临时性问题，队列中的消息通常表明本地或远程 MTA 配置存在问题，或者存在网络问题。

```
$ mailq
/var/spool/mqueue is empty
Total requests: 0
```

**mailstats** **mailstats** 实用工具报告自其显示在首行的日期以来 **sendmail** 发送和接收的消息数量及大小：

```
$ mailstats
Statistics from Fri Dec 27 16:02:34 2013
 M msgsfr bytes_from msgsto bytes_to msgsrej msgsdis msgsqur Mailer
 0 0 0K 17181 103904K 0 0 0 prog
 4 368386 4216614K 136456 1568314K 20616 0 0 esmtp
 9 226151 26101362K 479025 12776528K 4590 0 0 local
 T 594537 30317976K 632662 14448746K 25206 0 0
 C 694638 499700 146185
```

在上面的输出中，每个邮件投递程序（mailer）由第一列标识，该列显示邮件投递程序的编号；并由最后一列标识，该列显示邮件投递程序的名称。第二到第五列显示邮件投递程序发送和接收的消息数量及总大小。第六、第七和第八列分别显示被拒绝、丢弃和隔离的消息数量。以 T 开头的行列出列总计，以 C 开头的行列出 TCP 连接数量。

## 配置 sendmail

sendmail 配置文件位于 /etc/mail 中，其中主要配置文件是 **sendmail.cf**。该目录包含其他文本配置文件，如 **access**、**mailertable** 和 **virtusertable**。 **sendmail** 守护进程不直接读取这些文件，而是读取同一目录中对应的 *.db 文件。

