
### 启动 sendmail

一旦安装完成，`sendmail` 服务默认开启。若要立即启动 `sendmail`，你可以重启机器或直接运行 `service sendmail start` 来启动服务器。启动和停止 `sendmail` 的过程与任何其他服务过程类似。

## 用于 Fedora 或 Red Hat Linux 的其他邮件服务器

`sendmail` 的开源版本不是 Fedora 和 Red Hat Linux 系统可用的邮件服务器，但它绝对是最常见的。以下列表描述了其他服务器并提供了进一步信息的 URL：

- Postfix — 像 Sendmail 一样，Postfix MTA 包含在 Fedora 中。由 Wietse Venema 编写的此免费邮件服务器是为安全设计的，在非特权运行并具有多种功能。关于它的可以访问 [www.linux.org](http://www.linux.org/wiki/mail/sendmail-postfix) 更多信息见 [postfix.org](http://www.postfix.org)。
- Exim — Exim 是一个在 Linux 和其他 Unix 上运行的免费邮件服务器（遵循 GPL），包含了检查邮件的灵活功能。更多信息可以访问 [exim.org](http://www.exim.org)。
- Qmail — 此邮件服务器以安全为优先考虑，提供了可靠的邮件传输。更多信息可以访问 [qmail.com](http://www.qmail.com)。
- Sendmail (商业版) — Sendmail, Inc. (www.sendmail.com) 提供了基于相同代码的产品，面向企业级部署。
- Smail 提供了许多与 `sendmail` 相同的功能，但配置更简单且占用内存较少。Smail 最适用于中小型邮件服务器。Smail 项目页面可以访问 [weird.com/-/projects/snail.html](http://www.weird.com/-/projects/snail.html)。源代码可以从 [ftp.planix.com/pub/snail](http://ftp.planix.com/pub/snail) 下载。

默认情况下，`sendmail` 接收的传入邮件处理并存储在 `/var/spool/mail` 目录中。该目录下的每个文件代表一个有效的用户名。当第一次向该用户发送电子邮件（或者该文件不存在）时，会自动创建该文件。登录用户使用此目录和用户名作为他们的收件箱（例如 `/var/spool/mail/johnk`）。

输出邮件在等待发送时进入 `/var/spool/mqueue` 目录。此目录中的文件名遵循特定的命名方案。前两个字符指示文件中存储的数据类型（见表 19-1）。剩余字符根据处理该消息的 `sendmail` 进程的 PID 形成唯一标识。

#### 表 19-1 /var/spool/mqueue 中的文件前缀

| 文件名前缀 | 存储的数据类型 |
|---|---|
| df | 构成电子邮件正文的数据 |
| qf | 包含邮件头和其他管理细节的队列控制文件 |
| tf | qf文件的临时副本 |
| xf | 尝试发送时产生的任何错误消息 |

### 其他程序

发行版中还包含了其他可执行程序。这些描述在表 19-2 中。

#### 表 19-2: 其他相关 Sendmail 程序

| 程序 | 描述 |
|---|---|
| mailq | 显示邮件队列中等待的消息摘要（该命令等同于 sendmail -bp）。 |
| mailstats | 显示消息数量和字节数统计。 |
| makemap | 将文本文件 (/etc/mail/virtusertable) 转换为哈希伯克利数据库 (/etc/mail/virtusertable.db)。 |

## 第 19 章：设置邮件服务器 759

| 程序 | 说明 |
| --- | --- |
| | 每次 sendmail 脚本启动时运行的命令。 |
| newaliases | 将纯文本文件 /etc/aliases 转换为哈希处理过的伯克利数据库文件 /etc/aliases.db（该命令等同于 sendmail -bi）。 |
| prallases | 打印 /etc/aliases 中定义的所有别名。 |
| procmail | 不包含在 sendmail 软件包中，但用作 sendmail 的 MDA（邮件传输代理）。在 Fedora 和 RHEL 中通过 procmail 包包含。） |
| purgestat | 清除存储主机状态信息的目录。该命令等同于 sendmail -bH，默认情况下是禁用的。 |
| rmail | 通过 UUCP 处理入站邮件。 |
| smrsh | 实现一个受限 shell，用于从 sendmail 运行程序。 |

## sendmail 执行的日志

`sendmail` 执行的日志量可以在 `sendmail.mc` 文件中配置，但默认级别对信息通知和错误消息提供了良好的覆盖。默认情况下，`syslog` 配置文件 (`/etc/syslog.conf`) 告诉 `syslog` 将 `sendmail` 的日志信息存储在 `/var/log/maillog` 文件中。本节显示了文件的文件的示例。

每次守护进程启动时，`/var/log/maillog` 文件会出现类似下面的信息消息（这也会缓存哈希别名数据库以便重新生成）：

```
May 16 12:52:40 sendmail [1758]: alias database /etc/aliases
rebuilt by root
May 16 12:52:40 sendmail [1758]: /etc/aliases: 63 aliases, longest
10 bytes, 625 bytes total
May 16 12:52:40 sendmail [1787]: starting daemon (8.12.8):
SMTP+queueing@01:00:00
```

每当发送或接收消息时，都会创建一个日志文件：

```
May 16 12:54:34 sendmail [1120]: OA0A110: from=root, size=161
class=0, pri=3 0161, nrctpt=3,
msgid=199907191254.OA0A110@toys.linux.net), relay=root@localhost
May 16 12:54:35 sendmail [1127]: OA0A112: to=jkapt, ctladdr=root
(0/0), delay=00:05:01, xdelay=00:00:00, mailer=local, stat=Sent
```

除了正常的邮件服务器活动外，日志还会显示人们尝试入侵你的邮件服务器。`wiz` 和 `debug` 命令在 `sendmail` 的早期版本中实现，被发现是一个巨大的安全问题。你可能会看到日志条目，如下代码示例所示，因为怀有恶意的人会检查以确保你没有运行有漏洞的 `sendmail` 守护进程。此外，`expr vrfy` 命令（可以通过配置选项禁用）可能会提供比你想要发布的更多的信息。

```
May 16 13:03:27 toys sendmail[699]: NOQUEUE: "wiz" command from
localhost [127.0.0.1]
May 16 13:03:29 toys sendmail[699]: NOQUEUE: "debug" command from
localhost [127.0.0.1]
May 16 13:03:37 toys sendmail[701]: NOQUEUE: localhost [127.0.0.1]: exnp oracle
May 16 13:03:43 toys sendmail[702]: NOQUEUE: localhost [127.0.0.1]: vrfy oracle
```
