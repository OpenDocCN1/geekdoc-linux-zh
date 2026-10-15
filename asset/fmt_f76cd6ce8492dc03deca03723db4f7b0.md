
```conf
smtpd_delay_reject = yes
smtpd_helo_required = yes
smtpd_helo_restrictions =
- permit_mynetworks,
- reject_invalid_hostname,
- reject_non_fqdn_hostname,
- permit
smtpd_data_restrictions =
- reject_unauth_pipelining,
- permit
smtpd_sender_restrictions =
- permit_mynetworks,
- reject_non_fqdn_sender,
- reject_unknown_sender_domain.
- permit
smtpd_recipient_restrictions =
- permit_mynetworks,
- reject_unknown_recipient,
- reject_unauth_destination,
- permit
```

第 1 行是使用后续任何限制块的必要，它告诉你的远程 Postfix 等待接收到远程邮件服务器的命令（即任何作为你邮件服务器客户端的 SMTP 守护进程）后，再根据后续的规则拒绝邮件。`smtpd_delay_reject` 阶段是必要的，因为如果在它们有机会浪费你一些时间之前就拒绝邮件，某些 SMTP 服务器会表现异常。第 2 行拒绝来自任何未能使用 SMTP RFC 要求的 `HELO` 或 `EHLO` 短语正确识别身份的邮件服务器的邮件。这节省了你检查任何后续规则的时间。

第 3 至 7 行、第 8 至 10 行、第 11 至 15 行以及第 16 至 20 行是应用于你的邮件服务器与远程邮件服务器交互的不同部分的规则链：

- 第 3 至 7 行识别了对远程邮件服务器用于向你的 Postfix 邮件服务器标识身份的 `HELO` 或 `EHLO` 命令的限制。第 4 行立即允许来自 Postfix 网络列出的任何邮件服务器的连接。第 5 行拒绝使用错误格式主机名标识身份的远程邮件服务器的连接。第 6 行拒绝未使用完全限定域名（fqdn）标识身份的远程邮件服务器的连接。第 7 行表示你的邮件服务器将接受通过之前测试的邮件服务器的 `HELO` 或 `EHLO` 命令。

- 第 8 至 10 行识别了对远程邮件服务器向你的邮件服务器发送命令的限制。第 9 行拒绝过快向你的邮件服务器发送命令的连接。许多邮件发送者这样做是为了加速投递——毕竟它们有海量邮件要发送，无法浪费时间（除了你的时间）。第 10 行表示你的邮件服务器将接受未通过之前测试的邮件服务器发送的数据，允许进入下一组测试。

- 第 11 至 15 行识别了你的服务器接收的邮件（使用 SMTP `MAIL FROM` 命令）的限制。第 12 行立即允许 Postfix networks 参数列出的任何邮件服务器的连接。第 13 行拒绝任何未被识别为完全限定域名的发送者的邮件。（注意：本地网络可能使用此类主机名，但已经允许了它们。）第 14 行拒绝来自未知域发送者的邮件。第 15 行表示你的邮件服务器将接受未通过之前测试的发送者的邮件，允许进入下一组测试。

- 第 16 至 20 行识别了你的服务器接收的邮件收件者（使用 SMTP `RCPT TO` 命令）的限制。第 17 行立即允许 Postfix networks 参数列出的任何邮件服务器的连接。第 18 行拒绝当前服务器不是最终目标且目标不是有效域名的邮件。第 19 行拒绝收件者不在当前邮件服务器提供的域名中，或不在你的邮件服务器将转发的域名中（在 `relayhost` 参数中标识）的邮件。这防止了你的邮件服务器被用作开放中继。第 20 行表示你的邮件服务器将接受收件人通过测试的邮件，允许邮件服务器开始实际处理和投递传入邮件。

本节所示的示例命令可以显著减少你收到的传入垃圾邮件。当你有机会尝试这些内容后，你可能想要尝试添加其他类似的命令。要获得拒绝传入垃圾邮件的其他检查的完整列表，请参阅 `postconf` 在线参考信息中的文件部分（`man 5 postconf`）获取更多信息，这些信息也可以在 `www.postfix.org/postconf.5.html` 等位置找到。

# 将 MailScanner、SpamAssassin 和 ClamAV 与 Postfix 集成

MailScanner 是一款快速且强大的工具，用于扫描传入邮件中的垃圾邮件，并可以可选配置扫描传入邮件中的病毒。Ubuntu MailScanner 软件包要求系统中已安装 SpamAssassin 软件包（在第 7 章的“自动检查垃圾邮件”节中讨论过），以便它在执行完自己的垃圾邮件检查后调用 SpamAssassin 软件包，从而最大限度地捕获并标记传入的垃圾邮件。

## 注意

MailScanner 软件包始终声称它正在扫描病毒，即使它并没有这样做。这是因为配置文件中包含一个你想要使用的病毒扫描器设置，该设置默认为“无（none）”。别担心；我会解释如何修复它。

我在本章的“安装 Postfix 及其伙伴”节中曾建议你安装 MailScanner 和 ClamAV 病毒扫描软件包。如果你还没有安装，请返回该节以查看有关如何安装这些软件包的信息。

一旦安装完成，将 MailScanner 添加到 Postfix 链链中将非常简单：

-   在你的 Postfix 主配置文件 `main.cf` (`/etc/postfix/main.cf`) 的末尾添加以下行：

```
header_checks = regexp:/etc/postfix/header_checks
```

-   使用你喜爱的文本编辑器创建文件 `/etc/postfix/header_checks`，内容如下：

```
^Received:/ / HOLD
```

此行告诉 Postfix 扫描每条传入邮件，检查行开头是否存在字符串 `"Received:"` 实例，并且将任何匹配的邮件（即所有邮件）投递到 `HOLD` 队列。`HOLD` 队列是一个临时暂存区域，你将在该区域扫描传入的邮件。保存此文件并继续下一步。

-   使用你喜爱的文本编辑器打开 MailScanner 配置文件 (`/etc/MailScanner/MailScanner.conf`)，以便配置 MailScanner 使其与你 Ubuntu 系统上安装的 Postfix 正常工作。（默认情况下，Ubuntu MailScanner 软件包的配置类似于 Debian 系统，因此它的配置是为配合 exim 邮件服务器使用的。）

-   找到 `Run As User` 条目，删除 `Run As User = postfix` 行开头的井号（#），并确保任何其他以 `Run As User` 开头的行开头都有井号。这些条目现在应该像像所示：

```
# Run As User = mail
Run As User = postfix
# Run As User = Debian-exim-
```

-   找到 `Run As Group` 条目，删除 `Run As Group = postfix` 行开头的井号，并确保任何其他以 `Run As Group` 开头的行开头都有井号。这些条目现在应该像所示：

```
# Run As Group = mail
Run As Group = postfix
# Run As Group = Debian-exim
```

-   找到 `Incoming Queue Dir` 条目，将其值更改为 `/var/spool/postfix/hold`。该条目现在应该像所示：

```
Incoming Queue Dir = /var/spool/postfix/hold
```

-   找到 `Outgoing Queue Dir` 条目，将其值更改为 `/var/spool/postfix/incoming`。该条目现在应该像所示：

```
Outgoing Queue Dir = /var/spool/postfix/incoming
```

-   找到 `MTA` 条目，将其值更改为 `postfix`。该条目现在应该像所示：

```
MTA = postfix
```

-   找到 `Virus Scanners` 条目，将其值设置为 `clamav`。该条目现在应该像所示：

```
Virus Scanners = clamav
```

-   保存 `/etc/MailScanner/MailScanner.conf` 文件，并继续下一步。

-   使用以下命令确保 Postfix 用户和用户组拥有 MailScanner 工作目录以及它存储（隔离）疑似含有病毒文件的目录的所有权，以便 Postfix 邮件服务器可以向这些目录写入：

```
sudo chown -R postfix:postfix /var/spool/MailScanner
```

# 第三部分：面向系统管理员的 Ubuntu

12. 使用你喜爱的文本编辑器修改文件 `/etc/default/mailscanner`，并删除包含 `run_mailscanner` 变量行开头的井号。该行应该像所示：
