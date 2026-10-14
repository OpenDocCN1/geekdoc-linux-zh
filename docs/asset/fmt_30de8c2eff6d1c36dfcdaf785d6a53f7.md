
```
5 reject_invalid_hostname,

6 reject_non_fqdn_hostname,

7 permit

8 smtp_data_restrictions =

9 reject_unauth_pipelining,

10 permit

11 smpd_sender_restrictions =

12 permit_mynetworks,

13 reject_non_fqdn_sender,

14 reject_unknown_sender_domain,

15 permit

16 smpd_recipient_restrictions =

17 permit_mynetworks.

18 reject_unknown_recipient_domain,

19 reject_unauth_destination,

20 permit
```

第 1 行是必须，以便根据后续规则拒绝邮件之前使用任何后续限制块（即：远程 SMTP 守护进程等待直到它从邮件服务器或你邮件服务器的客户端接收到某些命令）。`smpd_delay_reject` 短语是必要的，因为如果你在某些服务器有机会等待至少一段时间之前就拒绝邮件，某些服务器会表现异常。第 2 行拒绝来自任何未能使用 SMTP RFC 中的 HELO 或 EHLO 短语正确标识自身身份的邮件服务器的邮件。这节省了你检查任何后续结果的时间。

第 3 到 7 行、第 8 到 10 行、第 11 到 15 行以及第 16 到 20 行是应用于你的邮件服务器与下一组测试的不同部分的规则链。

- 第 3 行触发对 HELO 或 EHLO 命令的限制，这些命令被远程邮件服务器用于向你的 Postfix 服务器标识身份。第 4 行立即允许来自 Postfix `mynetworks` 参数列表中任何邮件服务器的连接。第 5 行拒绝来自使用格式错误的主名标识身份的远程邮件服务器的连接。第 7 行表示你的邮件服务器可以使用未通过之前测试的邮件服务器的 HELO 或 EHLO 命令，并允许你进入下一组。
- 第 8 行标识了对远程服务器向你的邮件服务器发送命令方式的限制。第 9 行告诉服务器拒绝发送到你的邮件服务器的速度过快或在你的邮件服务器接受快速连接之前发送的命令。批量邮件服务器会自动这样做以尝试加速——毕竟，如果你有十亿个目标要发送，它们无法负担浪费时间（除了你的时间）。第 10 行表示你的邮件服务器将接受未通过之前测试的邮件服务器的额外数据，并允许你进入下一组测试。
- 第 11 到 15 行标识了你服务器正在接收的邮件的发送者（使用 SMTP MAIL 命令标识）。第 12 行立即允许来自 `networks` 参数列表中且未使用完全限定域名（FQDN）标识的任何邮件服务器的连接。（注意，来自本地网络可能使用短主机名，我们已经允许了来自它们的邮件。）第 14 行拒绝来自不可信域名的服务器的邮件。第 15 行表示你的邮件服务器将接受未通过之前测试的服务器的邮件，并允许你进入下一组。
- 第 16 到 20 行标识了你服务器正在接收的邮件的接收者（使用 SMTP RCP 命令标识）。第 17 行立即允许来自 `mynetworks` 参数列表中任何邮件服务器的连接。第 18 行拒绝接收者不是有效域名的邮件。第 19 行拒绝未指定接收者的邮件。第 20 行表示你的邮件服务器将接受未通过之前测试的服务器的邮件，并允许你处理。

## 第四部分 附录

### 设置邮件服务器

Postfix 提供了许多我在此处没有使用的其他检查，例如本节所示示例命令将显著减少入站邮件的数量。有关可以拒绝入站垃圾邮件的其他检查的完整列表，postfix 的在线参考（man 5）也可以通过 `www.postfix.org/postfix.html` 在线访问。

### 将 MailScanner、SpamAssassin 和 ClamAV 集成到 Postfix 中

`MailScanner` 是一个快速、强大的工具，用于扫描邮件中的垃圾邮件，并可以可选地配置扫描病毒。Ubuntu `MailScanner` 软件包要求系统安装了 `SpamAssassin` 软件包（在第 9 章“检查垃圾邮件”中讨论过），以便它在执行完自己的检查后可以调用 `SpamAssassin`，以最大化它能捕获的变化。

> `MailScanner` 总是声称它正在扫描病毒，即使它并没有这样做。这是因为它的配置文件包含一个你想要使用的病毒扫描器设置，该设置默认为空。不要担心；我将解释如何修复。

我在在本章的“安装 Postfix 及其伙伴”部分中建议你安装 `MailScanner` 和 `ClamAV` 软件包。如果你愿意，请回到该部分查看有关安装这些软件包的信息。

一旦安装，非常容易将 `MailScanner` 添加到 postfix 链中：

1. 在你的 Postfix `main.cf` 配置文件（`etc/postfix/main.cf`）末尾添加以下行：
2. 使用你喜欢的文本编辑器创建 `/etc/postfix/header_checks` 文件，内容如下：

```
/Received:/ HOLD
```

此行告诉 Postfix 扫描每条入站消息行开头的字符串 "Received:"，并将任何匹配的邮件（将是所有邮件）移动到 HOLD 队列。HOLD 队列是你用于扫描入站邮件的临时存储区域。保存此文件并进行下一步。

3. 使用你喜欢的文本编辑器打开 `MailScanner` 配置文件（`etc/MailScanner/MailScanner.conf`），以便配置 `MailScanner` 在安装了 Postfix 的 Ubuntu 系统上正常工作。（默认情况下，Ubuntu `MailScanner` 软件包是按照 Debian 系统配置的，因此是为出站邮件服务器配置的。）

# 第四部分 额外章节

4. 找到 `Run As` 条目，删除 `Run As User = postfix` 所在行开头的 `#` 号，并确保任何其他以 `Run User =` 开头的行开头都有 `#` 号。这些条目现在应该如下：

```
# Run As User = mail

Run As User = postfix

# Run As User = Debian-exim
```

5. 找到 `Run As Group`，删除 `Run As Group = postfix` 所在行开头的 `#` 号，并确保任何其他以 `As Group = Group` 开头的行开头都有 `#` 号。这些条目现在应该如下：

```
# Run As Group = mail

Run As Group = postfix

# Run As Group = Debian-exim
```

6. 找到 `Incoming Queue Dir` 并将其值更改为 `/var/spool/postfix/hold`。
该条目现在应该如下：

```
Incoming Queue Dir = /var/spool/postfix/hold
```

7. 找到 `Outgoing Queue Dir` 并将其值更改为 `/var/spool/postfix/incoming`。该条目现在应该如下：

```
Outgoing Queue Dir = /var/spool/postfix/incoming
```

8. 找到 `MTA` 条目并将其值更改为 `postfix`。该条目现在应该如下：

```
MTA = postfix
```

9. 找到 `Virus Scanners` 条目并将其值设置为 `clamav`。该条目现在应该如下：

```
Virus Scanners = clamav
```

10. 使用 `/etc/MailScanner/MailScanner.conf` 文件继续操作，并将 `MailScanner` 的工作目录以及它存储怀疑包含病毒的文件（隔离文件）的目录进行分组，以便 postfix 服务器可以写入这些目录：

```
sudo chown -R postfix:postfix /var/spool/MailScanner
```

11. 使用你喜欢的文本编辑器修改 `/etc/default/mailscanner` 文件，并删除包含 `run_mailscanner` 变量所在行开头的 `#` 号。该行看起来应该如下：

```
run_mailscanner=1
```

304

# 设置邮件服务器

启用此变量将导致你的系统在下次启动时自动启动 `MailScanner`。保存文件并退出文本编辑器。

现在，使用以下命令首次启动 `MailScanner`：

```
sudo check_mailscanner
```
