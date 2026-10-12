
前面的 Kmailertable、Kvirtuser 和 Kaccess 行定义了关键的数据库文件。您可以通过向邮件表数据库（/etc/mail/mailertable，其会创建 /etc/mail/mailertable.db 文件）添加定义，将特定地址的邮件路由到特定服务器。

虚拟用户表数据库（/etc/mail/virtusertable.db）由 /etc/mail/virtusertable 文本文件的哈希输出创建。访问列表（/etc/mail/access.db）数据库由 /etc/mail/access 文件创建，可让您丢弃并拒绝某些用户的电子邮件以防止垃圾邮件。请参阅侧边栏“转发电子邮件和阻止垃圾邮件”，其中描述了如何设置虚拟用户和访问列表数据库。

```
CPREDIRECT
DZ8.12.8
```

CPREDIRECT 行将文本 REDIRECT 添加到类 P 中。这与重定向功能（在 m4 配置文件中启用）一起使用，可为不再活跃的账户创建别名。例如，如果 /etc/aliases 中有以下内容：

```
jeff: jeff@newplace.com.REDIRECT
```

## 转发电子邮件和阻止垃圾邮件

/etc/mail 中的 mailertable、virtusertable 和 access 文件可以根据地址设置转发或丢弃电子邮件。mailertable 文件可将特定域的电子邮件转发到选定的服务器。例如，此 mailertable 条目将 handsonhistory.com 的邮件转发到 mxl.linuxtoys.net：handsonhistory.com smtp:[mxl.linuxtoys.net]

virtusertable 文件通常用于在多个域中重定向特定用户的邮件。以下是可能出现在 virtusertable 文件中的映射示例：videotech@myotherbox.org hadji sales@verysmallcompany.com george@wehavenomoney.com

第一行将发往 videotech@myotherbox.org 的邮件重定向到本地用户账户 hadji。第二行将发往 sales@verysmallcompany.com 的邮件重定向到远程用户 george@wehavenomoney.com。

同样，访问列表数据库由 /etc/mail/access 创建。它可根据邮件头中包含的地址、主机名、域名或 IP 地址有选择地接受、拒绝、中继或丢弃任何消息：ads@freestuff.net → DISCARD junkmail.com REJECT coupons.junkmail.com OK spam.junkmail.com 550 Unsolicited bulk email will be stored and handled for a fee of $500/KB

前述块中的第一行会丢弃（不发送任何错误消息）来自 ads@freestuff.net 的所有邮件。第二行拒绝来自 junkmail.com 域的所有邮件，并向发件人返回一般投递状态消息。第三行通过允许来自 coupons.junkmail.com 的邮件来覆盖之前的设置，而第四行则向令人讨厌的 spam.junkmail.com 域返回指定的错误代码。

mailertable、virtusertable 和 access 文件的内容在 sendmail 服务启动时都会合并到各自的 .db 文件中。更改这些文件中的任何一个后，输入 `/etc/init.d/sendmail restart` 使更改生效。

发送到本地机器上 jeff@ 的任何邮件都会导致向原始发件人返回一条信息性消息，指示地址已更改。原始邮件不会转发到前述 jeff@ 示例中列出的地址。DZ8.12.8 行设置宏 Z，其中包含 sendmail 守护进程的完整版本信息。

## sendmail 选项

`sendmail.cf` 文件包含可在 Red Hat Linux 系统上为 sendmail 设置的长选项列表。选项定义在 Options 块之后开始。以下是示例：

```
O SevenBitInput=False
# O EightBitMode=pass8
```

`SevenBitInput` 选项表示 sendmail 不应清除所有邮件消息每个字节中的最高有效位。`EightBitMode` 选项规定 sendmail 应如何处理未明确标记为 8 位的消息数据。`pass8` 选项允许任何 8 位数据不经更改即可传递；`mimefy` 将任何未指定的数据转换为 MIME 编码类型；`strict` 拒绝任何未标记的 8 位数据。请注意，此选项对指定为 8 位的数据无效。下一行与别名文件相关：

```
O AliasWait=10
O AliasFile=/etc/aliases
```

在重建别名数据库之前，sendmail 会执行多次检查，以确保没有其他进程正在尝试执行相同操作。`AliasWait` 选项指定 sendmail 在等待和执行检查之间交替的分钟数。`AliasFile` 选项指定包含邮件别名的纯文本文件的位置。下一行与 sendmail 的磁盘空间分配方式相关：

```
O MinFreeBlocks=100
#O MaxMessageSize=1000000
```

`MinFreeBlocks` 选项指定如果接受该消息会导致存储消息的文件系统上可用空闲块少于 100 个（100K），则该消息将被拒绝。如果取消注释，`MaxMessageSize` 可对传入电子邮件消息的最大大小施加限制（前一行中为 1MB）。By

默认情况下，消息大小没有限制。下一行将字符替换为空格：

```
O BlankSub= .
```

`BlankSub` 选项用指定的字符（此处为 .）替换电子邮件地址中的空白字符（这是非法字符）。下一行避免使用昂贵的邮件程序：

```
O HoldExpensive=False
```

如果 MDA 定义（本节后面会解释）包含选项 F=c，则邮件程序被归类为昂贵，这只是表示传递该邮件可能涉及缓慢的连接或其他处理延迟。`HoldExpensive` 选项允许由昂贵 MDA 处理的消息排队而不是立即处理。前一行禁用此选项。下一行与检查点队列相关：

```
#O CheckpointInterval=10
```

当向多个地址传递消息（例如邮件列表）时，sendmail 有时需要记录哪些收件人已收到消息。`CheckpointInterval` 选项设置在 qf 文件更新之间处理的收件人地址数量。前一行被注释掉了，但默认值仍为 10。下一行与投递模式相关：

```
O DeliveryMode=background
```

四个可能的 `DeliveryMode` 值如下：

- `background` — Sendmail 分叉（分离）出一个副本并异步处理消息。默认模式为 background。
- `deferred` — 消息被排队，所有处理，包括 DNS 查找和数据库访问，均推迟到队列运行时。
- `interactive` — 队列在前台同步处理。
- `queueonly` — 与 `deferred` 类似，但主机名会立即解析，数据库也会立即查询。

下一行与错误消息头和错误模式相关：

```
#O ErrorHeader=/etc/mail/error-header
#O ErrorMode=print
```

`ErrorHeader` 选项允许将指定文件中的文本包含在返回给发件人的所有投递状态消息中，以及来自 xf 文件的任何错误消息。`ErrorMode` 选项提供了五种可能的方法来向在尝试发送邮件时遇到问题的本地机器用户显示错误消息：

- `e` — 向发件人发送错误消息，但成功终止。
- `m` — 发送错误消息并以错误代码退出。
- `p` — 打印错误到用户的终端并将消息保存到 ~/dead.letter。（默认）
- `q` — 静默忽略所有投递错误。
- `w` — 将错误消息写入用户的终端。

下一行与电子邮件消息中的 From 行相关：

```
#O SaveFromLine=False
```

默认情况下，SaveFromLine 选项被禁用（False）。结果是邮件消息中以文本“From”开头的行（一个区分一条消息的结束与下一条消息的头的特殊标记）在投递的消息中会被 > 前缀。下一行与临时文件的权限相关：

```
O TempFileMode=0600
```

TempFileMode 选项将临时文件的文件权限设置为仅可由文件所有者读取。其他模式强烈不建议使用。下一行与 GECOS 字段相关：

```
#O MatchGECOS=False
```

MatchGECOS 选项允许 sendmail 将邮件投递到根据 /etc/passwd 文件中 GECOS 字段指定的用户全名的转换形式。例如，如果用户 wharris 的全名（根据 GECOS 字段）是 Wayne Harris，则该用户可以作为 wharris@mybox.com、Wayne_Harris@mybox.com 或 Wayne.Harris@mybox.com 接收邮件。不建议使用此选项，因为它可能导致歧义，并且用户可以更改其 GECOS 字段，从而破坏 sendmail 的常规投递机制。

下一行与跳数相关：

```
#O MaxHopCount=25
```

MaxHopCount 选项指定在消息被退回给发件人作为无法投递之前的最大跳数（消息从一台机器传输到另一台机器）。默认值为 25。下一行与 sendmail 帮助文件相关：

```
O HelpFile=/etc/mail/helpfile
```

HelpFile 选项列出包含在线帮助文本的文件名。要查看此数据，请执行命令 telnet localhost 25 并输入 help。也可以通过 help 命令名称使用 help 命令为大多数 SMTP 命令提供帮助。下一行与用作终止符的点相关：

```
#O IgnoreDots=False
```

IgnoreDots 选项决定了 sendmail 在收到包含单行单个句点的消息时的行为。如果选项不存在、被注释或为 False，则单个句点被视为消息的结束（RFC 821 中指定的行为）。If the
