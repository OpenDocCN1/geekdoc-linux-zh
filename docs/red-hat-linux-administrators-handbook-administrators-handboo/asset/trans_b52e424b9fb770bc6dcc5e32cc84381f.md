
```
rewrite: ruleset 96 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 3 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 0 input: kabir < @ ad-engine . com . >
rewrite: ruleset 199 input: kabir < @ ad-engine . com . >
rewrite: ruleset 199 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 98 input: kabir < @ ad-engine . com . >
rewrite: ruleset 98 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 198 input: kabir < @ ad-engine . com . >
rewrite: ruleset 90 input: < ad-engine . com > kabir < @ ad-engine . com . >
rewrite: ruleset 90 input: ad-engine . < com > kabir < @ ad-engine . com . >
rewrite: ruleset 90 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 90 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 95 input: < > kabir < @ ad-engine . com . >
rewrite: ruleset 95 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 198 returns: $# esmtp $ @ ad-engine . com . $ : kabir < @ ad-engine . com . >
rewrite: ruleset 0 returns: $# esmtp $ @ ad-engine . com . $ : kabir < @ ad-engine . com . >
```

地址 kabir@nitec.com 被重写为 kabir@ad-engine.com，并且 sendmail 显示它将通过 ESMTP（昂贵的 SMTP）邮件程序投递，因为 ad-engine.com 未列在 /etc/mail/sendmail.cw 中。如果列在其中，前面的测试将显示以下输出：

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset><address>
> 3,0 kabir@ad-engine.com
rewrite: ruleset 3 input: kabir @ ad-engine . com
rewrite: ruleset 96 input: kabir < @ ad-engine . com >
rewrite: ruleset 96 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 3 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 0 input: kabir < @ ad-engine . com . >
rewrite: ruleset 199 input: kabir < @ ad-engine . com . >
rewrite: ruleset 199 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 98 input: kabir < @ ad-engine . com . >
rewrite: ruleset 98 returns: kabir < @ ad-engine . com . >
rewrite: ruleset 198 input: kabir < @ ad-engine . com . >
rewrite: ruleset 198 returns: $# local $: kabir
rewrite: ruleset 0 returns: $# local $: kabir
```

请注意，使用的是 3,0 作为规则集，因为规则集 3 参与 domaintable 翻译，而规则集 0 参与地址解析。

## 测试 /etc/mail/* 数据库文件

只要你修改 /etc/mail/access、/etc/mail/aliases、/etc/mail/domaintable、/etc/mail/mailertable、/etc/mail/virtusertable 以及类似文件，请确保 sendmail 能够正确执行查找。例如，假设你刚刚在 /etc/mail/alias 文件中创建了以下别名：

```
root: kabir
```

在运行 newaliases 命令后，通过运行 sendmail -bt 来确认 sendmail 是否能够执行适当的别名查找。在地址测试模式提示符下，输入以下内容：

/map database name key

例如，要测试 /etc/mail/aliases 数据库中 root 别名，我可以运行

```
/map aliases root
```

其显示以下输出：

```
map_lookup: aliases (root) returns kabir
```

## 使用 sendmail 详细查看 SMTP 事务

你也可以使用 sendmail 来查看它如何将消息投递到目的地。例如，以下命令中的 -vt 选项会告诉 sendmail 以详细模式运行，并在输入中扫描 To:、From:、Cc: 和 Bcc: 标头：

```
sendmail -vt
```

运行上述命令后，它会等待用户输入。此时，你可以输入类似以下内容：

```
To: kabir@integrationlogic.com
From: someone@somewhere.com
Subject: Testing sendmail

This is a test.
```

输入简短消息，如上所示后，按 Ctrl+D 退出消息输入模式。然后 Sendmail 会显示类似以下的 SMTP 事务：

```
kabir@integrationlogic.com... Connecting to mail.integrationlogic.com via esmtp...
220 wormhole.integrationlogic.com ESMTP Sendmail 8.9.3/8.9.3; Sun, 21 Feb 1999 19:57:00 -0500
>> EHLO picaso.nitec.com
250-wormhole.integrationlogic.com Hello picaso.nitec.com {206.171.50.50}, pleased to meet you
250-EXPN
250-VERB
250-8BITMIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-XUSR
250 HELP
>> MAIL From:<kabir@picaso.nitec.com> SIZE=77
250 <kabir@picaso.nitec.com>... Sender ok
>> RCPT To:<kabir@integrationlogic.com>
250 <kabir@integrationlogic.com>... Recipient ok
>> DATA
354 Enter mail, end with "." on a line by itself
>>
.
250 TAA16439 Message accepted for delivery
kabir@integrationlogic.com... Sent
(TAA16439 Message accepted for delivery)
Closing connection to mail.integrationlogic.com.
>> QUIT
221 wormhole.integrationlogic.com closing connection
```

以 >> 开头的行是由本地 sendmail 服务器（picaso.nitec.com）发送到远程 sendmail 服务器（mail.integrationlogic.com）。这与我之前通过 Telnet 连接演示的内容非常接近。

## 使用 sendmail 调试标志

使用 -dX 选项（其中 X 为调试级别）与 -bv 结合使用，以查看 sendmail 对特定地址将采取什么操作。例如，

```
sendmail -bv -d0 kabir@nitec.com
```

在我的 sendmail 服务器上产生以下输出：

```
Version 8.9.3
Compiled with: MAP_REGEX LOG MATCHGECOS MIME7TO8 MIME8TO7 NAMED_BIND NETINET NETUNIX NEWDB NIS QUEUE SCANF SMTP USERDB XDEBUG

========== SYSTEM IDENTITY (after readcf) ===========
(short domain name) $w = picaso
(canonical domain name) $j = picaso.nitec.com
(subdomain name) $m = nitec.com
(node name) $k = picaso.nitec.com
========================================
```

kabir@nitec.com... deliverable: mailer local, user kabir

-d0 选项会导致 sendmail 显示有关 sendmail 本身的各种信息。最后一行显示 sendmail 将如何处理给定的地址。指定 -d 而不带任何调试级别数字会显示你想要的所有调试信息。

## 使用测试配置文件

当你修改 sendmail.cf 时，最好创建 /etc/sendmail.cf 文件的测试版本并仅修改测试副本，这样就不会丢失任何正在工作的配置。以下是如何测试新配置的方法：

- 1. 创建 /etc/sendmail.cf 的副本并使用新名称命名。对于本示例，将测试配置命名为 /etc/sendmail-test.cf。
- 2. 要使用新的测试配置文件运行 sendmail，请使用 -C 选项。例如，/usr/sbin/sendmail -C sendmail-test.cf 使用 /etc/sendmail-test.cf。
- 3. 如果你想为测试配置使用不同的队列（即不同于 /var/spool/mqueue），请使用 -Q 选项。例如，/usr/sbin/sendmail -C sendmail-test.cf -oQ /var/spool/test-mqueue 使用 /var/spool/test-mqueue 目录作为测试配置。

此时，你应该已按预期配置了 sendmail。

## 保护 Sendmail

作为最古老的邮件服务器之一，sendmail 曾出现过不少安全漏洞并受到指责。最近版本的 sendmail 是在严格的安全考虑下发布的。

### 保护配置文件

从 8.9.x 版本开始，sendmail 已收紧了配置文件权限的限制。例如，如果我运行 chmod -R 664 /etc/mail/* 来更改配置文件的权限，然后尝试重启 sendmail，我会收到以下错误消息：

```
Starting sendmail: /etc/sendmail.cf: line 93: fileclass:
cannot open /etc/mail/sendmail.cw: Group writable directory

WARNING: Group writable directory /etc/mail
/etc/mail/virtusertable.db: could not create:
Permission denied

WARNING: Group writable directory /etc/mail
/etc/mail/access.db: could not create: Permission denied

WARNING: Group writable directory /etc/mail
/etc/mail/domaintable.db: could not create:
Permission denied

WARNING: Group writable directory /etc/mail
/etc/mail/mailertable.db: could not create: Permission denied
```

总的来说，请执行以下操作以确保 sendmail 在你的系统上安全运行：

- 确保 /etc/sendmail.cf 和 /etc/mail/* 文件和目录仅可由超级用户或在 /etc/sendmail.cf 文件的 RunAsUser 行中指定的用户名读取。所有这些文件和目录应仅由超级用户写入。
- 不要为任何配置文件、目录或 sendmail 需要读取的任何其他文件启用组写权限。

在任何情况下都不应为任何配置文件启用组写访问。虽然 sendmail 允许你通过使用 DontBlame Sendmail 选项来禁用与文件权限和所有权相关的安全功能，但你应改为修复权限/所有权问题。
