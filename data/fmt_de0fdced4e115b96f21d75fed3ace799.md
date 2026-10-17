
# 是否交付经过 MIME 封装的错误消息？

`0 SendMimeErrors=True`

`SendMimeErrors` 选项定义了交付状态通知消息是经过 MIME 编码还是保持纯文本。接下来的几行与用于转发电子邮件的搜索路径有关：

```bash
# 转发文件搜索路径
0 ForwardPath=$z/.sw$/.forward
```

`ForwardPath` 选项指定了单个用户 `_forward` 文件的搜索路径。在前行中，`$z` 代表用户的家目录，`$sw` 表示本地机器的主机。例如，如果 `/home/kabzon` 是本地机器用户 `kabzon` 的家目录，sendmail 将首先查找文件 `/home/kabzon/.forward.al`，然后是 `/home/kabzon/.forward`。如果这两个文件都不存在，邮件将投递到收件箱文件 `/var/spool/mail/kabzon`。接下来几行与连接上如何使用缓存有关：

```bash
# 连接缓存大小
0 ConnectionCacheSize=2
```

```bash
# 连接缓存超时
0 ConnectionTimeout=5m
```

与其每次向主机建立新连接、发送消息、关闭连接然后再向同一台主机建立另一个连接，连接缓存允许 sendmail 通过一个连接向同一台机器发送多条邮件。此 `ConnectionCacheSize` 选项可以减少创建和销毁连接的开销。默认值 2 表示最多可以维持两个连接。`ConnectionTimeout` 值指定了连接可以维持的最长时间。默认值为 300s，即 5 分钟。接下来几行与主机状态目录和线程交付有关：

```bash
# 主机状态目录
0 HostDirectory=.hoststat
```

```bash
# 单线程交付（需要 HostDirectory）
0 SingleThreadDelivery=False
```

`HostDirectory` 选项可以相对于队列目录 `/var/spool/mqueue`（如果没有指定完整路径）创建一个目录，存储所有 sendmail 已建立连接机器的信息。此选项默认未设置，因为其实现可能会消耗资源。`SingleThreadDelivery` 选项确保对任何给定主机最多只有一个连接。这同样可能并不理想。

接下来的几行与 `Errors-To` 头部有关：

```bash
# 使用 Errors-To: 头部
0 UseErrorsTo=False
```

`UseErrorsTo` 选项允许 sendmail 利用或忽略 `Errors-To:` 头部。如果设置为 `True`，任何交付错误将报告给头文件中指定的地址。否则，该行将被忽略。该选项默认设置为 `False`，因为这种行为违反了 RFC 1123。接下来几行与日志级别有关：

```bash
# 日志级别
0 LogLevel=9
```

`LogLevel` 设置了发送到 syslog 设施的日志优先级和严重程度。范围从0（只报告严重错误）到9（记录最大调试信息以及更重要的消息）。除非你在跟踪邮件交付问题需要查看大量的调试信息，否则默认值 9 提供了合适的细节。接下来几行与如何向消息发送者发送消息有关

```bash
# 即使在别名展开中也发送给我？
0 OMeToo=True
```

`MeToo` 选项选择了当消息发送者也是邮件列表成员时 sendmail 的行为。除非指定了 `True`，否则发送者不会接收该消息（基于如果发送者写了消息，发送者就不再次看到它）。接下来几行与是否评估地址有关：

```bash
# 在 newaliases 中验证右侧？
0 CheckAliases=False
```

如果将值设置为 `True`，`CheckAliases` 选项将评估列左侧的地址，并保证右侧地址的有效交付。默认值为 `False`。接下来几行与旧式头部有关：

```bash
# 如果没有特殊标点符号，默认将消息使用旧式头部？
0 OldStyleHeaders=True
```

# 第 19 章 ✦ 设置邮件服务器

收件者列表最初是用空格分隔的。最近，使用了逗号，因为收件者名称中经常包含空格。当设置为 `True` 时，`OldStyleHeaders` 选项允许使用逗号分隔的列表，但未加引号的空格会被转换为逗号。如果该选项设置为 `False`（默认值），不常用的逗号将转换为 `BlankSub` 选项指定的字符。接几行与 SMTP 守护进程选项有关：

```bash
# SMTP 守护进程选项
# DaemonPortOptions=Name=MTA
#0 DaemonPortOptions=Port=587, Name=MSA, M=E
```

```bash
# SMTP 客户端选项
#0 ClientPortOptions=Address=0.0.0.0
```

`DaemonPortOptions` 可用于限制 `sendmail` 监听传入连接的端口号和网络、同时连接数以及 TCP/IP 发送和接收缓冲区的大小。`ClientPortOptions` 与 `DaemonPortOptions` 相同，区别在于它作用于出连接而不是传入连接。接几行与隐私有关：

```bash
# 隐私标志
#0 PrivacyOptions=authvarnings,norvry,noexpn,restrictgrun
```

`PrivacyOptions` 可用于要求传入连接严格遵守 SMTP 行为，禁用 `EXPN` (noxpn) 或 `VRFY` (norvry) 功能，禁用回执，并限制可以运行 `mailq` 和 `sendmail -q` 命令的用户。`mailq` 命令显示队列中的所有项，而 `PrivacyOptions` 还启用了 "X-Authentication-Warning" 头部行。接几行与错误消息的副本有关：

```bash
# 谁（如果有的话）应该接收错误消息的副本
#0 PostMasterCopy=Postmaster
```

`PostMasterCopy` 选项可以指定一个（或多个）地址，这些地址将接收发送给消息发送者的任何状态通知副本。默认是不发送任何副本。接几行与邮件队列有关：

```bash
# 仅队列函数的斜率
#0 QueueFactor=600000
```

```bash
# 队列目录
#0 QueueDirectory=/var/spool/mqueue
```

位于 www.unlt.com 的额外内容

`QueueFactor` 选项考虑当前的系统负载平均值，并可以实现一个截止值，使得出站消息进入队列而不是立即发送。`QueueDirectory` 选项指定了队列中的出站消息的位置。该目录中的文件名前缀在本章较前的表 19-1 中描述。接几行与 `sendmail` 使用的超时超时有关：

```bash
# 超时（其中许多项）
#0 Timeout.initial=5m
#0 Timeout.connect=1m
#0 Timeout.connect=5m
#0 Timeout.hello=5m
#0 Timeout.mail=10m
#0 Timeout.rot=1h
#0 Timeout.timeout=5m
#0 Timeout.datablock=1h
#0 Timeout.datafinal=1h
#0 Timeout.rset=5m
#0 Timeout.quit=2m
#0 Timeout.misc=2m
#0 Timeout.command=1h
#0 Timeout.ident=30s
#0 Timeout.fileopen=
#0 Timeout.queueturn=5d
#0 Timeout.queueturn.normal=5d
#0 Timeout.queueturn.urgent=2d
#0 Timeout.queueturn.non-urgent=7d
#0 Timeout.queueewarn=4h
#0 Timeout.queueewarn.normal=4h
#0 Timeout.queueewarn.urgent=1h
#0 Timeout.queueewarn.non-urgent=12h
#0 Timeout.hoststatus=30m
#0 Timeout.resolver.retrans=5s
#0 Timeout.resolver.retrans.first=5s
#0 Timeout.resolver.retrans.normal=5s
#0 Timeout.resolver.retry=4
#0 Timeout.resolver.retry.first=4
#0 Timeout.resolver.retry.normal=4
```
