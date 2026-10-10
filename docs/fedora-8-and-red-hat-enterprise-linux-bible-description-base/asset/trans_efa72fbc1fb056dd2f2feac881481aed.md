
## 程序

| 程序 | 描述 |
| :--- | :--- |
| newaliases | 将纯文本 `/etc/aliases` 文件转换为哈希的 Berkeley 数据库文件 `/etc/aliases.db`（该命令等同于 `sendmail -bi`）。 |
| praliases | 打印 `/etc/aliases` 中定义的所有别名。 |
| procmail | 不包含在 sendmail 软件包中，但用作 sendmail 的 MDA（邮件交付代理）。（它包含在 Fedora 和 RHEL 的 procmail 软件包中。） |
| purgestat | 清除存储主机状态信息的目录。该命令等同于 `sendmail -bH`，默认情况下是禁用的。 |
| rmail | 通过 UUCP（Unix to Unix Copy，Unix 到 Unix 复制）处理传入邮件。 |
| smsh | 实现了一个受限 Shell，用于从 sendmail 运行程序。 |

### sendmail 执行的日志记录

sendmail 执行的日志记录量可在 `sendmail.mc` 文件中配置，但默认级别提供了对信息通知和错误消息的良好覆盖。默认情况下，syslog 设施配置文件（`/etc/syslog.conf`）指示 syslog 将来自 sendmail 的日志信息存储在 `/var/log/maillog` 文件中。本节将展示该文件中的几个示例。

每次守护进程启动时（这也会导致哈希别名数据库重新生成），都会在 `/var/log/maillog` 文件中写入类似以下的信息消息：

```text
May  16 12:52:40 toys sendmail[1758]: alias database /etc/aliases
rebuild by root
May  16 12:52:40 toys sendmail[1758]: /etc/aliases: 63 aliases, longest
10 bytes, 625 bytes total
May  16 12:52:40 toys sendmail[1787]: starting daemon (8.12.8):
SMTP+queueing@01:00:00
```

每次发送或接收消息时，都会创建一个日志文件条目：

```text
May  16 12:54:34 toys sendmail[1120]: 0AA01120: from=root, size=161,
   class=0, pri=3 0161, nr_cpts=1,
   msgid=<199907191254.OAA01120@toys.linuxtoys.net>, relay=root@localhost
May  16 12:54:35 toys sendmail[1127]: 0AA01120: to=jkpatt, ctkadd=root
   (0/0), delay=00:00:01, xdelay=00:00:00, mailer=local, status=Sent
```

除了显示正常的邮件服务器活动外，日志还显示人们尝试入侵你的邮件服务器的时间。`fix` 和 `debug` 命令是在早期版本的 sendmail 中实现的，并被发现是一个巨大的安全问题。你可能会看到如下代码示例中所示的日志文件条目，这是怀有恶意意图的人为确保你没有运行存在漏洞的 sendmail 守护进程而进行的检查。此外，`expn` 和 `vrfy` 命令（可通过配置选项禁用）可能会泄露比你愿意分发更多的信息。

```text
May 16 13:03:27 toys sendmail[699]: NOQUEUE: "wiz" command from localhost  [127.0.0.1]  (127.0.0.1)
May 16 13:03:29 toys sendmail[699]: NOQUEUE: "debug" command from localhost  [127.0.0.1]  (127.0.0.1)
May 16 13:03:37 toys sendmail[701]: NOQUEUE: localhost  [127.0.0.1]:  expn oracle
May 16 13:03:43 toys sendmail[702]: NOQUEUE: localhost  [127.0.0.1]:  vrfy oracle
```

### 配置 sendmail

要配置 sendmail 设施，你需要编辑 `/etc/mail` 和 `/etc` 中的配置文件，然后由 sendmail 启动脚本使用这些文件来生成数据库文件。这些数据库文件反过来又被 sendmail 守护进程用于控制你的 sendmail 服务器的行为。一旦配置好 sendmail，你就可以开始添加用户账户，以便在你的服务器上拥有邮箱。本部分描述的配置 sendmail 的一般步骤如下：

1. **获取域名** — 你需要一个唯一的互联网域名来分配给你的邮件服务器。你可以从许多不同的地方购买互联网域名，然后让你域名的 DNS 邮件交换（MX）记录指向你正在创建的邮件服务器。
2. **配置基本 sendmail 设置** — 在这一步中，你编辑 `/etc/mail/sendmail.mc` 文件。该文件定义了其他配置文件和日志文件的位置，以及允许你配置 sendmail 守护进程的一些行为。
3. **定义传出邮件访问** — 与你的邮件服务器相关的最关键的安全问题是它接受哪些邮件消息以中继到其他邮件服务器。通过编辑 `/etc/mail/access` 文件，你可以指明你的服务器将接受哪些主机和用户进行本地投递或中继。
4. **配置虚拟服务器** — 默认情况下，sendmail 假设你正在为该服务器所属的域的域名设置邮件服务器。要使单台计算机上的 sendmail 成为多个域名的邮件服务器（称为虚拟服务器），你需要在 `/etc/mail/local-host-names` 文件中定义每个域名。
5. **配置虚拟用户** — 使用 `/etc/mail/virtusertable` 配置文件，你可以指示 sendmail 守护进程如何处理它收到的、为其配置要处理的用户和域名的邮件。此文件提供了很大的灵活性，允许你将发往特定用户的邮件引导至特定邮箱，转发到不同的邮件地址，或以各种方式拒绝该邮件。
6. **添加用户账户** — 你需要为在邮件服务器上拥有邮箱的每个用户添加一个用户账户。
7. **启动 sendmail 并生成数据库文件** — 启动 sendmail 服务会导致两个主要操作发生：它运行 sendmail 服务器守护进程，并将你的配置文件编译成 sendmail 可以使用的数据库文件。如果服务器已经在运行，你可以简单地编译配置文件，使任何新设置生效，而无需重启服务器。

以下各小节详细说明了这些步骤中的每一个。

## 第 19 章：设置邮件服务器

### 获取域名

为了让人们能够向你的邮件服务器上的用户发送邮件，你必须拥有自己的域名。第 25 章描述了如何获取自己的域名并设置 DNS 服务器。对于你的邮件服务器，关键问题是确保 DNS 服务器上你域名的 MX 记录指向你邮件服务器的地址。

> **注意：** 你的 ISP（互联网服务提供商）可能不允许你在住宅互联网账户上拥有私有邮件服务器。为了执行此规定，ISP 可能会阻止发往 25 端口的数据包。你可能需要联系他们开放该端口，然后才能在该连接上设置邮件服务器。由于许多垃圾邮件以及其他邪恶（或至少控制不当）的电子邮件服务器试图隐藏在动态 IP 地址之后，许多 ISP 既不允许使用动态 IP 地址的电子邮件地址，也不接受从这些服务器发送的电子邮件。

### 配置基本 sendmail 设置 (sendmail.mc)

你的 sendmail 服务器的大部分配置来自 `/etc/mail/sendmail.mc` 文件中的信息。由于该文件设置了 sendmail 的默认值，这些值在大多数情况下都可以使用，你可能不需要对 sendmail.mc 做太多修改。然而，我建议你逐步阅读本节，以便了解你的邮件服务器是如何配置的。

你对 sendmail.mc 文件所做的更改不会立即生效。首先，你必须编译 sendmail.mc 设置以生成 `/etc/mail/sendmail.cf` 文件。我在“启动 sendmail 并生成数据库文件”一节中描述了如何做到这一点。

生成的 `/etc/mail/sendmail.cf` 文件包含超过 1,800 行的设置和注释，用于指导你的 sendmail 守护进程的行为。你在 sendmail.mc 文件中使用的 m4 宏与 sendmail.cf 文件中的最终设置不同。

> **注意：** m4 实用程序可用于处理包含 IEEE Standard 1003.1-2001 格式（第 12.2 节，实用程序语法指南）宏的文本文件。有关 m4 实用程序的详细信息，请输入 `info m4`。

要查找在 sendmail.cf 文件中找到的某个设置应使用哪些宏，请参考 `/usr/share/doc/sendmail/README.cf` 文件。如果你有兴趣了解 sendmail.cf 文件内容的详细信息，我在 Fedora 和 Red Hat Enterprise Linux Bible 网站（www.wiley.com/go/fedora8bible）上包含了 sendmail.cf 的详细描述。

