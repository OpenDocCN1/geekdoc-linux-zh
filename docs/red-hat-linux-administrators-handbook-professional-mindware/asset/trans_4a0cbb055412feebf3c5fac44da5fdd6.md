
```
/etc/mail/mailer table.db: could not create: Permission
denied
```

一般而言，为了确保 sendmail 在系统中安全运行，请执行以下操作：

- 确保 /etc/sendmail.cf 和 /etc/mail/* 文件及目录仅允许超级用户或您在 /etc/sendmail.cf 文件的 RunAsUser 行中指定的用户名读取。所有这些文件和目录应仅允许超级用户写入。
- 不要为任何 sendmail 需要读取的配置文件、目录或其他文件启用组写权限。

在任何情况下，您都不应为任何配置文件启用组写访问权限。虽然 sendmail 允许您通过使用 Dont BlameSendmail 选项来禁用与文件权限和所有权相关的安全功能，但如果 sendmail 在日志文件中报告了任何权限/所有权问题，您应该修复该问题，而不是禁用检查。切勿禁用 sendmail 中的检查。如果您希望保持安全检查不变，请确保存放 .forward 文件的用户主目录不允许任何组写入。.forward 文件本身应具有 644 (rw-r--r--) 的权限设置。此外，确保 sendmail 读取文件路径中的任何目录都禁用了组写访问权限。

在确认文件/目录级权限已正确设置，且 sendmail 没有因文件和目录的权限/所有权问题而抛出任何警告或错误信息后，请确保日志记录已正确启用。默认情况下，sendmail 通过 syslog 写入日志，因此在 /etc/syslog.conf 文件中包含以下行：

```
mail.*				/var/log/maillog
```

您可以按喜好更改日志文件名；通常，此文件命名为 mail.log 或 mail1.log。此外，请确保您在 /etc/logrotate.d/syslog 文件中包含如下一条目：

```
/var/log/maillog {
postrotate
		/usr/bin/killall -HUP syslogd
endscript
}
```

这会在 logrotate 处理 /var/log/maillog 文件后重启 syslogd。

# 确保更严格的运行模式和隐私

您可以强制 sendmail 在客户端连接到您的服务器时严格遵循 SMTP 协议，并且您可以控制用户如何与 sendmail 交互。您可以通过使用如下的选项行来实现：

```
O PrivacyOptions=needvrfyhelo, restrictmailq, restrictqrun, goaway
```

PrivacyOptions 的值如表 9-3 所示。

## 表 9-3 sendmail 的隐私选项

| 选项 | 说明 |
|:-------------|:--------------------------------|
| public | 允许公开访问 |
| needmailhelo | 客户端在发出 MAIL 命令前必须使用 HELLO 或 EHLO |
| needexpnhelo | 客户端在发出 EXPN 命令前必须使用 HELLO 或 EHLO |
| noexpn | 客户端不能使用 EXPN 命令 |
| needvrfyhelo | 客户端在发出 VRFY 命令前必须使用 HELLO 或 EHLO |
| novrfy | 客户端不能使用 VRFY 命令 |
| notrn | 客户端不能使用 TRN 命令 |
| noverb | 客户端不能使用 VERB 命令 |
| restrictmailq | 限制使用 mailq 命令。设置此选项时，只有超级用户以及队列目录的所有者和组所有者才能运行 mailq 命令 |
| restrictqrun | 限制 -q 选项。设置此选项时，只有超级用户以及队列目录的所有者才能使用此选项 |
| norereceipts | 成功时不返回成功代码 |
| goaway | 不允许 SMTP 状态查询 |
| authwarnings | 在消息中插入 X-Authentication-Warning: 头 |

# 采取反垃圾邮件措施

在这个大量非应邀电子邮件的时代，您的 sendmail 服务器可能会遭受外部人员的滥用。向成千上万的人发送非应邀电子邮件的人通常使用他人的邮件服务器来为他们肮脏的工作服务。这被称为第三方邮件中继漏洞。

# 应对第三方邮件中继漏洞

直到最近，sendmail 默认允许任何人进行邮件中继。换句话说，与您或您的组织完全无关的人可以使用您的 sendmail 服务器作为 SMTP 邮件中继，向您所不知道的人发送邮件。在这种情况下，发送者和接收者对您或您的组织都是未知且无关的。以前这是被允许的，因为它为邮件管理员提供了定位邮件连接问题的调试功能。然而，群发邮件者（或垃圾邮件发送者）如今在互联网上泛滥成灾，他们寻找未受保护的中继服务器来执行他们的大量邮件任务。这滥用了您的系统资源，并可能使您或您的组织面临法律纠纷。

许多司法管辖区现在正在通过针对非应邀电子邮件的法律，根据这些法律，相关方可能需要对损害承担财务责任。如果您的邮件服务器卷入与垃圾邮件相关的法律事务，处理该事务并证明您的无辜可能需要大量的法律和财务资源。此外，如果您的服务器卷入此类邮件发送，许多收件人将简单地认为您积极参与了此事，他们很可能会向您发送数百封愤怒的电子邮件，并将您列入垃圾邮件发送者黑名单。这会损害您或您组织的声誉。它还可能干扰您的邮件连接操作，因为许多邮件服务器在同意与某个域交换邮件之前会检查垃圾邮件发送者黑名单。

检查您的邮件服务器是否存在中继漏洞的最简单方法之一是访问 `http://maps.vix.com/tsi/ar-test.html`，这是由邮件滥用预防系统 (MAPS) 传输安全倡议 (TSI) 网站提供的。在目标主机条目框中输入您的邮件服务器的主机名，并点击 **GO** 按钮，以确定您的邮件服务器是否存在中继攻击漏洞。

如果您希望允许一个或多个域使用您的 sendmail 服务器进行中继，请将它们添加到 `/etc/mail/relay-domains` 文件。此外，如果您希望阻止已知的垃圾邮件发送者发送垃圾电子邮件，请使用 `/etc/mail/access` 文件明确拒绝他们访问您的邮件服务器。

# 将垃圾邮件发送者送入黑洞

邮件滥用预防系统的实时黑洞列表（**RBL**）可用于自动阻止已知的垃圾邮件发送者使用您的 sendmail 服务器。RBL 的网站位于 `http://maps.vix.com/`。

您可以将 RBL 视为已知垃圾邮件发送者的数据库。通过查询该数据库，您可以找出某个域是否是垃圾邮件发送者，并拒绝来自相关域的服务。MAPS RBL 是一个基于 DNS 的垃圾邮件检查和阻止系统，可以查询以确定特定 IP 地址是否因垃圾邮件发送而被阻止。您可以以两种方式使用 RBL。

- 只需与 MAPS RBL 签署协议，将整个数据库传输到本地主机，并为您自己的使用创建一个本地 RBL。
- 按个案查询主 RBL 数据库。

最新版本的 sendmail（**8.11.x**）附带 RBL。最新版本的 Red Hat Linux RPM 在 `/etc/sendmail.cf` 中启用了 RBL，因此您无需做任何配置操作。以下是如何在 sendmail 中测试 RBL 配置的方法。

1. 运行以下内容：
   `sendmail -bt`
2. 在地址测试模式提示符处，输入：
   `.D{client_addr}127.0.0.1`
   `Basic_check_relay <>`
   输出看起来如下：
   `ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)`
   Enter `<ruleset> <address>`
3. 现在，使用 127.0.0.2（RBL 提供的测试 IP，在 RBL 中被阻止）重复上述测试。您应该看到类似以下内容的输出：

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)

Enter <ruleset> <address>
> .D(client_addr)127.0.0.2
> Basic_check_relay <>

rewrite: ruleset 190     input: < >

rewrite: ruleset 190 returns: $$ error $$ 5 . 7 . 1
$ : "Mail from " 1 2 7 . 0 . 0 . 2 * * refused by blackhole site rbl.maps.vix.com. Email from your server is blocked. Contact your local Systems Administrator or ISP."
```

如您所见，该 IP 在 RBL 中被黑洞化或列入黑名单，因此 sendmail 将不允许其中继消息。

您还可以使用 Russell Nelson 制作的自动回复器进行实际测试。根据自动回复器所有者的说法，您必须从您想要测试其 RBL 阻止功能的服务器向 nelson-rbl-test@crynwr.com 发送邮件。预期会从 ns.crnwr.com 收到一条包含 SMTP 对话的回复。如果您收到另一条来自 linux.crnwr.com 的回复，则说明您的 RBL 设置未起作用。

> **提示**
> 如果您想知道哪些邮件交易因 RBL 而被拒绝，只需运行 `grep "maps.vix.com" /var/log/mail log` 即可查看被拒绝的请求。

