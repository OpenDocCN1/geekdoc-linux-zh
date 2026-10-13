
## 启动 sendmail

安装后，`sendmail` 服务默认处于开启状态。要立即启动 `sendmail`，你可以重新启动机器，或直接运行 `/etc/init.d/sendmail start` 来启动服务器。启动和停止 `sendmail` 的过程与其他服务器进程没有区别。

### Red Hat Linux 可用的其他邮件服务器

开源版本的 `sendmail` 并不是 Red Hat Linux 可用的唯一邮件服务器，但它绝对是最常见的。以下列表描述了其他服务器，并提供了提供进一步信息的 URL。

- `Postfix` — `Postfix` MTA 是除 `Sendmail` 外随 Red Hat Linux 提供的唯一邮件服务器软件。由 Wietse Venema（`tcp_wrappers` 著名作者）编写，这款免费邮件服务器以安全性为设计目标，并在受限的 `chroot` 环境中以非特权用户身份执行大多数功能。服务器包含十多个小型程序（每个执行一个简单、独立的任务）和几个单一用途的队列。信息和源代码可在 `www.postfix.org` 找到。
- `Exim` — `Exim` MTA 是一款在 Linux 和其他 UNIX 系统上运行的免费邮件服务器（遵循 GNU）。该 MTA 包含针对未经请求的垃圾邮件和邮件炸弹的增强保护。有关 `Exim` 的更多信息，请访问 `Exim` 主页（`www.exim.org`）。
- `Qmail` — 该邮件服务器（由 Daniel J. Bernstein 编写）同样以安全性为首要考虑，提供安全可靠的消息传输、邮箱配额、虚拟域和反垃圾邮件功能。更多信息可在 `www.qmail.org/top.html` 获取。
- `Sendmail`（商业版） — 基于与开源 `sendmail` 相同的源代码，该产品以专为 Red Hat Linux（以及其他 Linux 和 UNIX 变体）构建的二进制可执行文件形式分发。`Sendmail` 高级消息服务器的定价基于你服务的邮箱数量。该产品提供简单安装、基于 Web 的管理和支持。详细信息可在 `www.sendmail.com` 找到。
- `Smail` — `Smail` 提供了与 `sendmail` 相同的许多功能，但配置起来稍微容易一些，且所需内存更少。源代码可从 `ftp://ftp.planix.com/pub/Smail/` 下载。

`sendmail` 接收到的传入消息会被处理并存储在 `/var/spool/mail` 目录中。该目录中的每个文件代表本地机器上的一个有效用户名。文件在添加用户时自动创建。拥有登录账户的人使用该目录及其用户账户名作为其传入邮箱（例如，`/var/spool/mail/johnq`）。

外出消息在等待发送时会进入 `/var/spool/mqueue` 目录。该目录中的文件名遵循一致的命名方案。前两个字符表示文件中存储的数据类型（见表 19-1）。后续字符基于处理该消息的 `sendmail` 进程的 PID 形成唯一的随机标识符。

## 表 19-1：/var/spool/mqueue 中的文件前缀

| 文件名前缀 | 存储的数据类型 |
| :--- | :--- |
| df | 构成电子邮件正文的数据。 |
| qf | 包含消息头和其他管理细节的队列控制文件。 |
| tf | `qf` 文件的临时副本，在投递错误时创建。 |
| xf | 尝试发送消息时生成的任何错误消息。 |

## 其他程序

发行版中还包含几个其他可执行程序。这些在表 19-2 中描述。

## 表 19-2：其他相关的 Sendmail 程序

| 程序 | 描述 |
| :--- | :--- |
| `mailq` | 显示邮件队列中等待处理的邮件摘要（该命令等同于 `sendmail -bp`）。 |
| `mailstats` | 显示消息数量和字节计数统计信息。 |
| `makemap` | 将文本文件（`/etc/mail/virtusertable`）翻译为哈希 Berkeley 数据库（`/etc/mail/virtusertable.db`）。该命令在启动时每次 `sendmail` 脚本启动时运行。 |
| `newaliases` | 将纯文本 `/etc/aliases` 文件翻译为哈希 Berkeley 数据库文件 `/etc/aliases.db`（该命令等同于 `sendmail -bi`）。 |
| `praliases` | 打印 `/etc/aliases` 中定义的所有别名。 |
| `procmail` | 未包含在 `sendmail` 包中，但用作 `sendmail` 的 MDA。（它包含在 Red Hat Linux 的 `procmail` 包中。） |
| `purgestat` | 清除存储主机状态信息的目录。该命令等于 `sendmail -bH`，默认情况下处于禁用状态。 |
| `rmail` | 通过 UUCP 处理传入邮件。 |
| `smrsh` | 为从 `sendmail` 运行程序实现受限 shell。 |

## sendmail 执行的日志记录

`sendmail` 执行的日志记录量可在 `sendmail.cf` 文件中进行配置，但默认级别已能很好地覆盖信息通知和错误消息。默认情况下，`syslog` 设施（`/etc/syslog.conf` 文件）将 `sendmail` 的日志信息存储在 `/var/log/maillog` 文件中。本节展示了该文件中的一些示例。

每次守护进程启动时（这也会导致哈希别名数据库被重新生成），都会在 `/var/log/maillog` 文件中写入类似以下的信息消息：

```
Feb 16 12:52:40 toys sendmail[1758]: alias database /etc/aliases
rebuild by root
Feb 16 12:52:40 toys sendmail[1758]: /etc/aliases: 63 aliases, longest
10 bytes, 625 bytes total
Feb 16 12:52:40 toys sendmail[1787]: starting daemon (8.12.8):
SMTP+queuing@01:00:00
```

每次发送或接收消息时，都会创建一条日志文件条目：

```
Feb 16 12:54:34 toys sendmail[1120]: 0AA01120: from=root, size=161,
class=0, pri=30161, nrcpts=1,
msgids<199907191254.0AA01120@toys.linuxtoys.net>, relay=root@localhost
Feb 16 12:54:35 toys sendmail[1127]: 0AA01120: to=jxpatt, ctagddr=root
(0/0), delay=00:00:01, xdelay=00:00:00, mailer=local, stat=Sent
```

日志甚至会显示人们尝试他们可能不应该尝试的事情。`wiz` 和 `debug` 命令在 `sendmail` 的早期版本中实现，被发现是巨大的安全问题。恶意人员可能会检查日志条目，例如下面代码示例中所示的内容，以确保你没有运行易受攻击的 `sendmail` 守护进程。此外，`expn` 和 `vrfy` 命令（可通过配置选项禁用）可能会泄露超出你希望分发的更多信息。

```
Feb 16 13:03:27 toys sendmail[699]: NOQUEUE: "wiz" command from
localhost
[127.0.0.1] (127.0.0.1)
Feb 16 13:03:29 toys sendmail[699]: NOQUEUE: "debug" command from
localhost [127.0.0.1] (127.0.0.1)
Feb 16 13:03:37 toys sendmail[701]: NOQUEUE: localhost [127.0.0.1]:
expn oracle
Feb 16 13:03:43 toys sendmail[702]: NOQUEUE: localhost [127.0.0.1]:
vrfy oracle
```
