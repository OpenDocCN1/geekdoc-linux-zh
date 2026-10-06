
```
$ -t mx google.com
go.com mail is handled by 20 alt1.aspmx.1.google.com
google.com mail is handled by 10 aspmx.1.google.com
google.com mail is handled by 40 alt3.aspmx.1.google.com
google.com mail is handled by 30 alt2.aspmx.1.google.com
google.com mail is handled by 50 alt4.aspmx.1.google.com.
```

Google 列出了邮件服务器，每个都有不同的优先级级别：10、20、30、40 和 50（虽然记录可以任何顺序显示，但优先级数字决定了尝试的顺序）。值越小优先级越高，因此远程 MTA 会首先尝试投递到 `aspmx.l.google.com`。如果失败，它可以自由尝试列表中的下一个。

然而，通过发布虚假的 MTA，Google 承诺其中任何一个对于为 `google.com` 的用户投递邮件都是有效的。

如果一个域名没有在 DNS 中发布 MX 记录，MTA 可以尝试将域名解析为地址并投递邮件。如果失败，该域名可能不接受电子邮件，邮件应该被退回（bounce）。在电子邮件术语中，退回是指电子邮件在链条的某一点被拒绝。大多数情况下，用户可以预期收到一封回执邮件，指示邮件未投递成功。某些系统不会为不存在的用户或伪造用户名的垃圾邮件发送者返回退回信息，后者会产生大量的退回。

## 邮件投递代理

邮件投递代理（MDA）像 MTA 一样通过 SMTP 接收电子邮件，并将其投递到目的地使用的任何格式的本地邮箱中。有时它将电子邮件写入给用户的平铺文件；有时出于性能考虑，将其写入数据库。

MDA 在 MTA 的身份下，也有机会执行别名（aliasing）和转发（forwarding）。当用户希望以不同的名称接收电子邮件时，就会发生别名。例如，而不是为现有账户创建账户，这样你可以让你的销售地址公开，但将所有电子邮件发送给特定用户的账户。这允许你可以在无需公开更改的情况下切换目标，并且意味着人们只需要检查一个邮箱。

转发与别名类似，不同在于重定向到了不同的电子邮件系统。`joe@example.com` 可能想将其所有电子邮件发送到他拥有独立电子邮件地址的手机上。某些组织为了控制电子邮件而禁止这种行为，或者可能对邮件可以转发到何处有规定。某些 MDA 还允许用户创建自己的转发规则。

MDA 通常是 MTA 的功能。MTA 可能会自己投递邮件，或者在确定电子邮件应该在本地投递时，将邮件传递给外部命令。

一旦 MDA 处理了消息并将其投递到邮箱，电子邮件即被认为已投递。读取电子邮件取决于收件者。

## 邮件服务器

拼图的最后一部分是邮件服务器，它读取用户的邮箱并允许接收者读取电子邮件。通常，用户在发送电子邮件时使用的同一个 MUA（邮件用户代理）读取邮件。该 MUA 可以使用发送消息时相同的私有协议连接到邮件服务器。如果使用 SMTP 发送电子邮件，则需要使用其他工具，因为 SMTP 仅用于发送消息而非读取。

邮局协议（POP）或互联网消息访问协议（IMAP）用于 MUA 从邮件服务器上读取电子邮件。POP 主要用于将电子邮件下载到本地计算机并从计算机中删除，而 IMAP 通常将邮件留在服务器上并通过网络读取。

POP 非常简单，因为它设计之初是为了将电子邮件传输到客户端并从服务器上删除。IMAP 设计用于在客户端上镜像功能，以便在服务器端执行更多工作；因此它支持文件夹和搜索。

MDA 和邮件服务器之间紧密关联，因为 MDA 必须以邮件服务器可以读取的位置和格式写入电子邮件，但它们不需要是同一种软件。

## 创建别名和转发电子邮件

当 MTA 决定收到的电子邮件需要投递时，它会检查别名文件（aliases）。别名文件通常位于 `/etc/aliases`。别名文件的格式为 `alias: destination`。例如：

```
sales: bob
```

在这种情况下，发送到 `sales` 的邮件将投递给 `bob`。你可以通过逗号为单个别名设置多个目标：

```
sales: bob, alice
```

在这种情况下，发送到 `sales` 的邮件将同时投递给 `bob` 和 `alice`。你也可以使用完全域名作为目标：

```
sales: bob@example.com
```

别名文件还支持注释，以井号（`#`）开头。

```
# 这是一个注释
sales: bob
```

当你对 `/etc/aliases` 文件进行更改时，必须运行 `newaliases` 命令来更新 MTA 用于查找的 `/etc/aliases.db` 文件。

## 提交更改

对 `/etc/aliases` 的更改立即生效。你必须运行 `newaliases` 命令来更新 `/etc/aliases.db` 文件。此命令必须以 `root` 身份运行，因为该文件的权限不允许用户修改。

如果没有问题，`newaliases` 命令不会返回任何内容。如果存在格式问题，你会收到错误：

```
newaliases
warning: /etc/aliases, line 96: need name:value pair
```

如果你忘记运行 `newaliases`，服务器通常会在日志（通常是 `/var/log/messages`）中提示：

```
warning: database /etc/aliases.db is older than source file /etc/aliases
```

这表明更改 `/etc/aliases` 后没有运行 `newaliases`。

## 其他类型的别名

你已经看到别名如何映射到其他本地账户，例如让 Rebecca 接收发往人力资源邮件。除了投递到本地账户，你还可以对邮件进行更多操作。别名文件也接受完全域名。如果你在别名文件中有这样一行：

```
isaac: i.smith@example.com
```

任何发送到别名账户的电子邮件都将发回 MTA 并指向 `i.smith@example.com`。别名的目标也可以是一个文件：

```
support: /var/log/support.please.ignore
```

这将所有发送到 `support` 账户的邮件重定向到 `/var/log` 中的一个文件。想象一下如果管理员不需要处理那些讨厌的用户，工作会变得多么容易！如果文件名以管道符（`|`）为前缀，目标也可以是一个脚本：

```
support: | /usr/local/bin/new_ticket.sh
```

在这种情况下，电子邮件将传递给一个脚本，该脚本预计会将电子邮件录入新的工单中。

## 用户自定义转发

用户可以通过在其主目录下放置一个名为 `.forward`（注意前面的点）的文件，并在其中包含转发指令来定义自己的转发规则。

## 核心主题

`/.forward` 文件中的指令与 `/etc/aliases` 文件中的指令相同。格式上的唯一区别是不需要指定别名用户，因为用户就是 `~/.forward` 文件的所有者。因此，如果用户 Isaac 有一个包含 `i.smith@example.com` 的 `~/.forward` 文件，他所有的邮件都将重定向到外部地址。

需要记住的一点是别名可以指向其他别名。如果 Isaac 想要将邮件重定向到外部并在本地保留一份，他需要对本地别名进行转义，以防止其被重新处理为外部重定向：

```bash
\isaac
i.smith@example.com
```

## 管理队列

MTA（邮件传输代理）接收消息并将其存储在队列中以便稍后处理。队列允许 MTA 在目标 MTA 未处于监听状态时稍后处理电子邮件，或者发送一个错误指示你的 MTA 应该稍后重试连接。`mailq`（邮件队列）命令显示队列，如示例 17-8 所示。

## 示例 17-8 邮件队列

点击此处查看代码图片

```
# mailq
-Queue ID- --Size-- ---Arrival Time ----Sender/Recipient---
AC1687363* 3229 Tue Apr 14 05:48:57 MAILER-DAEMON cfxvvrsi@example.com
451817349 651 Sat Apr 11 13:06:09 nginx@www.noreply.com
(connect to example.org[172.16.33.111]):25: Connection timed out)
example.org jermainwillillams@example.com
```

## 核心主题

此命令查看 `/var/spool/mqueue` 中的邮件队列文件并将其显示在屏幕上。你可以从示例 17-8 中看到队列中有了两条消息。在那里看到邮件是正常的，因为拼写错误和垃圾邮件会导致邮件被投递到各种配置错误的服务器。

如果你正在研究向往特定目的地的投递问题，邮件队列是一个很好的地方，因为你可以在那里看到等待发送的电子邮件。日志（通常为 `/var/log/maillog`）也是查看每封邮件历史计数情况的好地方。

![](img/16cd7204aa58beaaf530d67f50f15fc5_601_0.png)

`mailq` 实际上是 `sendmail` 的命令，但由于大多数发行版都实现了兼容层，它会根据你选择的 MTA 运行相应的命令。例如，Postfix 使用 `postqueue-p`，exim 使用 `-bp`，qmail 使用 `-read`。

`newaliases` 也是一个 sendmail 兼容命令！

## 总结

打印涉及一系列离散步骤，将打印作业从应用程序传输到最终打印机。CUPS（通用 Unix打印系统）使用互联网打印协议（IPP）进行通信，而不是旧的基于行打印机远程（LPR）的命令。一系列命令行工具允许你启用和禁用打印机及队列，并查询和修改正在处理的任务。

电子邮件与打印非常相似，都有离散的步骤。邮件传输代理（MTA）负责将邮件移动到目标的大部分工作，依靠邮件投递代理（MDA）完成将邮件投递到用户邮箱的最后工作。

邮件别名用于将电子邮件从一个用户重定向到另一个用户，即使第一个用户并不存在。用户还可以设置自己的转发规则，例如将电子邮件发送到另一个账户或通过过滤器传递。

## 考试复习任务

正如引言中“如何使用本书”部分所提到的，你有几种备习考试的选择：此处的练习题、第 21 章“最终准备”以及 DVD 上的模拟考试。

## 复习所有核心主题

复习本章中最重要的主题，这些主题在页外外边上用“核心主题”图标标记。表 17-2 列出了这些核心主题的参考以及它们所在的页码。

![](img/16cd7204aa58beaaf530d67f50f15fc5_602_0.png)

| 核心主题元素 | 描述 | 页码 |
| :--- | :--- | :--- |
| 段落 | 配置页面位于 http://localhost:631 | 470 |
| 列表 | 各种打印机状态 | 475 |
| 段落 | `lp` 和 `lpr` 命令用于打印 | 478 |
| 段落 | 使用 `-n lpr` 打印多份 | 478 |
| 段落 | `lpstat` 查看队列状态 | 479 |
| 段落 | `lp` 命令在默认打印机上操作；`-P` 选择不同的打印机 | 479 |
| 段落 | 不带任务号的 `lprm` 会删除第一个任务 | 480 |
| 段落 | `cups` 命令直接获取队列名称 | 480 |
| 段落 | `cupsenable` 启用已停止的打印机 | 481 |
| 段落 | CUPS Web 界面默认不响应其他主机请求 | 481 |
| 列表 | 关键配置文件列表 | 482 |
| 列表 | 当前的 Linux MTAs | 486 |
| 段落 | 邮件别名位于 `/etc/aliases` | 489 |
| 段落 | 别名后必须跟 `newaliases` | 490 |
| 段落 | 用户可以在 `.forward` 文件中设置邮件转发命令 | 491 |
| 段落 | `mailq` 显示邮件队列状态并必须以 root 身份运行 | 491 |
| 段落 | `mailq` 是兼容性命令，`aliases` 也是 | 492 |

表 17-2 第17 章核心主题

## 术语定义

定义本章的以下关键术语并在词表中检查你的答案：

- 打印缓存器 (print spooler)
- 打印队列 (print queue)
- 行打印机远程 (line printer remote)
- 互联网打印协议 (Internet Printing Protocol)
- 通用 Unix打印系统 (Common Unix Printing System)
- CUPS 后端 (CUPS backend)
- 邮件代理 (Mail Agent)
- 邮件传输代理 (Mail Transfer Agent)
- 简单邮件传输协议 (Simple Mail Transfer Protocol)
- 中继 (relay)
- Sendmail
- Postfix
- Qmail
- Exim
- 退 (bounce)
- 邮件投递代理 (Mail Delivery Agent)
- 别名 (aliasing)
- 转发 (forwarding)

## 复习题

这些复习题的答案在附录 A 中。

1. 访问在与浏览器同一台机器运行的 CUPS 管理界面的正确 URL 是？

   a. http://localhost

   b. https://localhost:631

   c. http://localhost:631

   d. http://localhost:389

2. 下列哪个打印机状态指示打印机出了问题？

   a.空闲 (Idle)

   b. 处理中 (Processing)

   c. 已停止 (Stopped)

   d. 暂停 (Paused)

3. 如何确定哪些任务正在发送到默认打印机？

4. 如果你正在研究向特定目的地的投递问题，邮件队列是一个很好的查看点，因为你可以在那里看到等待发送的邮件。日志（通常为 `/var/log/maillog`）也是查看每封邮件历史计数情况的好地方。

5. 你的一个打印机 CentralArea 出现了故障，在几天内无法修复。与其让队列等待修复，你如何处理打印出现问题？

6. 以下哪些是作为守护进程运行的邮件传输代理示例？

   a. Sendmail

   b. Qmail

   c. Exim

   d. Postfix

7. 你被要求将所有邮件从 hr@yourcompany.com 送到 rebecca@yourcompany.com 和 edward@yourcompany.com。你需要的文件名称是？

8. 在文件中添加邮件别名后，你应该运行哪个命令？

   a. mailq

   b. update-aliases

   c. postmap

   d. newaliases

9. 一位用户向你询问如何将邮件发送到她的另一个账户 j.smith@example.com，而不是在本地读取。你给她的指令是什么？

   a. 将 `sendmail -f j.smith@example.com` 到 `~/.forward`。

   b. 将 `j.smith@example.com` 添加到 `~/.aliases`。

   c. 将 `j.smith@example.com` 添加到 `/etc/aliases`。

   d. 将 `j.smith@example.com` 添加到 `~/.aliases`。

| 基础知识章节 | 该章节涵盖的问题 |
|---|--- |
| 维护系统时间 | 1-3 |
| 系统日志 | 4-6 |
| 日志轮转 | 7-8 |

**表 18-1** “我认识这些吗？”基础知识章节到问题的映射

- 1. Linux 系统时钟的源是

    a. 主板上的实时时钟

    b. 网络时间协议守护进程 (NTP)

    c. Linux 内核

    d. GPS 时钟

- 2. 如果你在 2015 年 4 月 26 日晚上 8:19 运行 `date "+%Y %m %d %H %M"`，你会看到哪个结果？

    a. 2015 04 26 20 19

    b. 2015-04-26 8:19

    c. 1430097577

    d. Sun Apr 26 8:19:45pm CDT 2015

- 3. 如果运行 `hwclock -w`，会发生什么？

    a. 硬件时钟的时间以本地时间显示

    b. 软件时钟时间将被复制到硬件时钟。

    c. 硬件时钟时间将被复制到软件时钟。

    d. 硬件时钟的时间以 UTC 显示。

- 4. 如果你的 `syslog.conf` 文件包含如下行

    * ` .notice;mail.none /var/log/foo`

    哪些消息会进入 `/var/log/foo`？（选择两项）

    a. kernel.warning

    b. cron.info

    c. mail.err

    d. cron.err

- 5. 哪个命令可以从命令行向 syslog 记录消息？

    a. `logger This is a message`

    b. `log This is a message`

    c. `syslog "This is a message"`

    d. `echo "This is a message" | syslogd`

- 6. 如何实时查看 systemd 日志？

    a. `tail -f /var/log/journal/*`

    b. `journalctl | tail -f`

    c. `journalctl -f`

    d. `journalctl --continuous`

- 7. 你配置了 `logrotate` 来轮转自定义应用程序的文件，但日志似乎没有写入新文件——它们仍然写入带时间戳的文件。这可能需要什么？（选择两项）
