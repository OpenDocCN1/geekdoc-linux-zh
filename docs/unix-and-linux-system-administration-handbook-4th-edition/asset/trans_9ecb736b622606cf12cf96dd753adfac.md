

如果您考虑以某种形式启用中继，请查阅 `cf/README` 中的 **sendmail** 文档，以确保您不会无意中成为垃圾邮件发送者的朋友。完成后，请让其中一个中继检查站点验证您没有无意中创建开放中继——请尝试 spamhelp.org。

## 用户或站点黑名单

如果您有本地用户或主机需要阻止邮件，请使用

```
`FEATURE(\`blacklist_recipients')`
```

它支持在您的 access 文件中包含以下类型的条目：

```
To:nobody@                         ERROR:550 Mailbox disabled for this user
To:printer.mydomain                  ERROR:550 This host does not accept mail
To:user@host.mydomain                 ERROR:550 Mailbox disabled for this user
```

这些行会阻止向任意主机上的用户 nobody、主机 printer 以及某台机器上特定用户的地址发送传入邮件。使用 To: 标签可让这些用户发送消息，只是不能接收它们；某些打印机具有这种功能。

要为传入电子邮件包含 DNS 风格的黑名单，请使用 dnsbl 功能：

```
FEATURE(\`dnsbl', \`zen.spamhaus.org')
```

此功能会使 **sendmail** 拒绝来自其 IP 地址位于 spamhaus.org 维护的三个已知垃圾邮件发送者黑名单（SBL、XBL 和 PBL）中的任何站点的邮件。其他列表编目了运行开放中继的站点以及可能成为垃圾邮件发送者庇护所的已知地址块。这些黑名单是通过对 DNS 系统的巧妙调整分发的；因此得名 dnsbl。参见第 766 页，了解系统工作原理的更完整解释。

您可以向 dnsbl 功能传递第三个参数来指定您希望返回的错误消息。如果省略此参数，**sendmail** 将从包含记录的 DNS 数据库返回固定的错误消息。

您可以多次包含 dnsbl 功能以检查不同的滥用者列表。

## 节流、速率和连接限制

表 20.12 列出了几种 **sendmail** 控制项，当客户端行为看起来可疑时可减慢邮件处理速度。

**表 20.12**  **sendmail 的“减速”配置原语**

| 原语 | 描述 |
|---|---|
| `BAD_RCPT_THROTTLE` | 减慢收集地址的垃圾邮件发送者 |
| `MAX_RCPTS_PER_MESSAGE` | 如果消息收件人过多则延迟投递 |
| `ratecontrol` feature | 限制传入连接的速率 |
| `conncontrol` feature | 限制同时连接的数量 |
| `greet_pause` feature | 延迟 HELO 响应，要求严格遵守 SMTP |

在 `BAD_RCPT_THROTTLE` 选项中设置的无此登录计数达到限制后，`sendmail` 在每次拒绝的 RCPT 命令后休眠一秒，将垃圾邮件发送者的地址收集速度降至爬行。为将该阈值设为 3，请使用

```
define(`confBAD_RCPT_THROTTLE', `3')
```

设置 `MAX_RCPTS_PER_MESSAGE` 选项会导致发送者将额外收件人排队以便稍后投递。这是对收件人数量可疑地大的消息的一种廉价形式的灰名单。

ratecontrol 和 conncontrol 功能允许对每个主机或每个网络限制接受传入连接的速率以及同时连接的数量。两者均使用 `/etc/mail/access` 文件来指定限制以及应适用的域，前者使用键字段中的标签 `ClientRate:`，后者使用标签 `ClientConn:`。要启用速率控制，请在您的 `.mc` 文件中插入如下行：

```
FEATURE(`ratecontrol', `nodelay', `terminate')
FEATURE(`conncontrol', `nodelay', `terminate')
```

然后，将要控制的主机或网络及其限制阈值的列表添加到您的 `/etc/mail/access` 文件中。例如，行

```
ClientRate:192.168.6.17    2
ClientRate:170.65.3.4     10
```

将主机 192.168.6.17 和 170.65.3.4 分别限制为每分钟两个新连接和十个新连接。行

```
ClientConn:192.168.2.8    2
ClientConn:175.14.4.1      7
ClientConn:                     10
```

为 192.168.2.8 设置两个同时连接的限制，为 175.14.4.1 设置七个，同时为所有其他主机设置十个同时连接。

另一个不错的功能是 `greet_pause`。当远程 MTA 连接到您的 **sendmail** 服务器时，SMTP 协议规定它必须等待您的服务器的欢迎问候后再发言。然而，垃圾邮件发送者立即发出 EHLO/HELO 命令很常见。这种行为部分可以解释为垃圾邮件发送工具对 SMTP 协议实现的不足，但也可能是旨在为垃圾邮件发送者节省时间的特性。不管原因如何，这种行为都很可疑，被称为“slamming”。

`greet_pause` 功能使 **sendmail** 在连接开始时等待指定时间后再向新朋友发送问候。如果远程 MTA 没有等待被正确问候，并在计划的尴尬时刻发出 EHLO 或 HELO 命令，**sendmail** 将记录错误并拒绝来自远程 MTA 的后续命令。

