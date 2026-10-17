
## 示例 3.8

被雇一周后，Sancho 想要联系 Don Quixote。他对 `who` 命令足够熟悉，可以检查这位善良的 Don 今天早上是否在网络上。

```bash
$ who>Enter
root console Jul 9 07:30
quixer tty2 Jul 9 08:10
perez tty3 Jul 9 08:15
nicholas tty4 Jul 9 08:18
dulcean tty5 Jul 9 08:10
panzanzan tty6 Jul 9 08:10
```

`who` 命令的输出仅仅是当前登录用户的列表，以及他们的工作站和最后登录的时间。

通常在命令后添加 `-u` 和 `-m` 选项。`who -u` 的响应显示所有用户名、它们各自的、工作站名称、登录时间以及正在运行的进程的标识。

`who -m` 的响应与 `who am i` 相同，如示例 3.9 所示。对于这两个命令，系统都会响应输入命令的人的用户名、用户的工作站名称以及用户的登录时间。

## finger 命令

`finger` 命令显示有关登录用户的信息，如示例 3.1 所示。默认响应格式是全用户名、登录时间、用户主目录和用户 shell。你可以使用 `finger` 命令查询远程系统。但你必须知道远程系统的正确名称。

## 示例 3.10

一个早上，Don Quixote 打算给 Sancho 发送消息，但需要知道 Sancho 是否在系统中。以下是他如何使用 finger 的：

```bash
[username@hostname]$ finger<Enter>
Login Name Tty Login Time Phone
root tty 2 Jul 10 07:30
quixoted tty 2 Jul 10 11:16
```

不带选项使用 `finger` 会给他所有登录用户的列表。同样，用户并不多。如果他想检查 Sancho，可以输入：

```bash
$ finger pansasan<Enter>
Login: pansasan Name: (null)
Directory:/home/pansasan Shell: /bin/bash
Since Tue Jul 17 8:32 (CST) on tty6
No mail.
No Plan.
```

所以，Don Quixote 知道 Sancho 在系统中。但那些其他信息是什么呢？

用户可以创建 `.project` 和 `.plan` 文件（请注意文件名以点开头，我们称之为点，以表示它们通常是隐藏的），以增强通过 `finger` 命令查询时收到的响应。详细过程超出了本书的范围，但我们将提供一个快速的概述。假设理发师 Nicholas（用户名 `nicholas`）使用 `vi` 等文本编辑器（详情请见第 10 章“vi 编辑器”）在他的主目录下创建了隐藏文件 `.plan` 和 `.project`。在创建这些文件时，他必须记住对其他人拥有 `r` 权限以及对其他人 `nicholas` 主目录拥有 `x` 权限。（文件和目录权限将在第 6 章“Linux 文件权限”中详细讨论）。当用户带 `nicholas` 用户名参数调用 `finger` 命令时，将获得 Nicholas 写入这些文件的所有信息。

# 发送和接收邮件：mail 命令

`mail` 命令是一个交互式命令，用于发送和接收邮件消息。

## 发送邮件

要向同一系统上的另一个用户发送消息，格式如下：

```
$ mail username<Enter>
```

要向同一系统上的多个用户发送消息，请在 `mail` 命令后输入所有用户名，并用空格隔开每个：

```
$ mail username username2<Enter>
```

要向另一个系统上的用户发送消息，输入用户名，后跟 `@` 和系统名称：

```
$ mail username@hostname<Enter>
```

要向另一个系统上的多个用户发送消息，请用空格分隔 `username@hostname`。

示例 3.11 显示了一个用户如何向同一系统（即同一主机）上的另一个用户发送邮件，以及向不同系统的用户发送邮件。请注意，每当调用 `mail` 命令时，系统都会响应 `Subject`（主题）提示。输入一行将出现在接收者收件箱列表中的描述文字，然后按回车。现在，你可以输入任何想与接收者交流的内容。完成消息后，按回车并按 `Ctrl-D`。系统会响应 `Cc`（抄送）提示。如果你想向其他人发送消息副本，请输入他们的用户名。完成后，按 `Ctrl-D`。系统会发送消息并响应 shell 提示符（通常是 `$` 符号）。

## 示例 3.11 使用 mail 命令发送邮件

知道桑丘（Sancho）今天在系统中，堂吉霍（Quixote）向他发送了一条消息：

```
$ mail sancho<Enter>
Subject: Meeting at Toboso<Enter>
Sancho! Don't forget the meeting tonight at Lady Dulcinea's
signed, Quixote de Mancha
```

如果高贵的骑士堂吉霍想要给另一个系统上的用户发送消息怎么办？知道杜尔西内亚（Dulcinea）在托波索索（Toboso）家里工作，以下是他可能输入的内容：

```
$ mail dulcinea@hostname<Enter>
Subject: Meeting Still OK?<Enter>
我（你忠诚的游侠骑士）、我们的同志们今晚在托波索索与你见面方便吗？我们想讨论一下未来的计划。我已经擅自通知了理发师桑丘和佩雷斯神父。得到你的许可后，我将通知其他人。
signed, Quixote de Mancha
```

## 接收邮件

每当你登录时，系统都会通知你是否有等待处理的邮件（位于 `/var/spool/mail/` 目录下，其中 `username` 指你的用户名）。当有新消息到达时，会有邮件通知，但邮件内容本身不会显示。系统管理员可以自定义 shell（换句话说是系统）定期检查所有邮箱文件；例如，每 60 秒检查一次。如果 shell 在用户的 `/var/spool/mail/username` 中检测到新消息，就会显示 `You have mail`（你有邮件）通知。系统管理员还可以自定义此邮件通知的其他方面。也就是说，查看消息的格式简单为：

```
$ mail<Enter>
```
