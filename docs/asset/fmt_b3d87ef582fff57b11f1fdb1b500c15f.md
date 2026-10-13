
你也可以使用 `sendmail` 来查看它如何将消息投递到目的地。例如：

```
sendmail -vt
```

这里 `-vt` 选项告诉 `sendmail` 以详细模式运行并扫描输入中的 `To:`、`From:`、`Cc:` 和 `Bcc:` 头部。运行上述命令后，它会等待用户输入。此时你可以输入类似以下内容：

```
To: kabir@integrationlogic.com
From: someone@somewhere.com
Subject: Testing sendmail

This is a test.

.
```

输入如上所示的简短消息后，按 `Ctrl+D` 退出消息输入模式。`sendmail` 然后会显示类似以下所示的 SMTP 事务：

```
kabir@integrationlogic.com... Connecting to mail.integrationlogic.com. via esmtp...
220 wormhole.integrationlogic.com ESMTP Sendmail 8.10.1/8.10.1; Sun, 21 Feb 1999 19:57:00 -0500
>> EHLO picaso.nitec.com
250-wormhole.integrationlogic.com Hello picaso.evoknow.com [206.171.50.50], pleased to meet you
250-EXPN
250-VERB
250-8BITMIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-XUSR
250 HELP
>> MAIL From:<kabir@picaso.evoknow.com> SIZE=77
250 <kabir@picaso.evoknow.com>... Sender ok
>> RCPT To:<kabir@integrationlogic.com>
250 <kabir@integrationlogic.com>... Recipient ok
>> DATA
354 Enter mail, end with "." on a line by itself
>> .
250 TAA16439 Message accepted for delivery
kabir@integrationlogic.com... Sent
(TAA16439 Message accepted for delivery)
Closing connection to mail.integrationlogic.com.
>> QUIT
221 wormhole.integrationlogic.com closing connection
```

以 `>>` 开头的行是由本地 `sendmail` 服务器（`picaso.nitec.com`）发送到远程 `sendmail` 服务器（`mail.integrationlogic.com`）的。

## 使用 sendmail 调试标志

你可以使用 `-dX` 选项（其中 `X` 为调试级别）与 `-bv` 结合使用，以查看 `sendmail` 对特定地址采取什么操作。例如：

```
sendmail -bv -d0 kabir@evoknow.com
```

这在我的 `sendmail` 服务器上产生以下输出：

```
Version 8.10.1
    Compiled with: MAP_REGEX LOG MATCHGECOS MIME7TO8 MIME8TO7 NAMED_BIND NETINET NETUNIX NEWDB NIS QUEUE SCANF SMTP USERDB XDEBUG

============ SYSTEM IDENTITY (after readcf) ============
    (short domain name) $w = picaso
    (canonical domain name) $j = picaso.evoknow.com
    (subdomain name) $m = evoknow.com
    (node name) $k = picaso.evoknow.com
==========================================================

kabir@evoknow.com... deliverable: mailer local, user kabir
```

如你所见，`-d0` 选项会导致 `sendmail` 显示有关 `sendmail` 本身的各种信息。前述输出中的最后一行显示 `sendmail` 将如何处理给定的地址。如果你指定 `-d` 而不带任何调试级别数字，你将看到所有你想要的调试信息。

## 使用测试配置文件

当你在 `sendmail.cf` 上试验时，最好创建 `/etc/sendmail.cf` 文件的测试版本并仅修改测试副本。这样，你不会丢失任何正在工作的配置。以下是如何测试新配置的方法。

- 创建 `/etc/sendmail.cf` 的副本并使用新名称。这里我假设你将测试配置命名为 `/etc/sendmail-test.cf`。
- 要使用新的测试配置文件运行 `sendmail`，请使用 `-C` 选项。例如，`/usr/sbin/sendmail -Csendmail-test.cf` 使用 `/etc/sendmail-test.cf`。
- 如果你想为测试配置使用不同的队列（即不同于 `/var/spool/mqueue`），请使用 `-oQ` 选项。例如，`/usr/sbin/sendmail -Csendmail-test.cf -oQ/var/spool/test-mqueue` 使用 `/var/spool/test-mqueue` 目录作为测试配置。

此时，你应该已按要求配置了 `sendmail`。以下部分讨论有关你的 `sendmail` 配置的几个安全问题。

## 保护 sendmail

作为最古老的邮件服务器之一，`sendmail` 曾出现过不少安全漏洞并受到指责。最新版本的 `sendmail` 是在严格的安全考虑下发布的。

### 保护你的配置文件

从 8.9.x 版本开始，`sendmail` 已收紧了配置文件权限的限制。例如，如果我运行 `chmod -R 664 /etc/mail/*` 来更改配置文件的权限，然后尝试重启 `sendmail`，我会收到以下错误消息：

```
Starting sendmail: /etc/sendmail.cf: line 93: fileclass: cannot open /etc/mail/sendmail.cw: Group writable directory

WARNING: Group writable directory /etc/mail
/etc/mail/virtusertable.db: could not create: Permission denied

WARNING: Group writable directory /etc/mail
/etc/mail/access.db: could not create: Permission denied

WARNING: Group writable directory /etc/mail
/etc/mail/domaintable.db: could not create: Permission denied

WARNING: Group writable directory /etc/mail
/etc/mail/mailertable.db: could not create: Permission denied
```

总的来说，你应执行以下操作以确保 `sendmail` 在你的系统上安全运行：

- 确保 `/etc/sendmail.cf` 和 `/etc/mail/*` 文件和目录仅可由 `root` 用户或你在 `/etc/sendmail.cf` 文件中 `RunAsUser` 行指定的用户名读取。所有这些文件和目录应仅可由 `root`（或其他超级用户）写入。
- 不要为任何配置文件、目录或 `sendmail` 需要读取的任何其他文件启用组写权限。

在任何情况下都不应为任何配置文件启用组写访问。虽然 `sendmail` 允许你使用 `DontBlameSendmail` 选项禁用与文件权限和所有权相关的安全功能，但我强烈建议你修复权限/所有权问题，而不是禁用 `sendmail` 中的检查。如果你想保持安全检查不变，请确保存放 `.forward` 文件的用户主目录不被任何组写入。`.forward` 文件本身应具有 `644`（`rw-r--r--`）权限设置。你还应确保 `sendmail` 读取的任何文件的路径中的目录均已禁用组写访问。如果你必须使用 `DontBlameSendmail` 选项引入安全漏洞，请阅读 `sendmail` 提供的文档以了解如何使用此功能。
