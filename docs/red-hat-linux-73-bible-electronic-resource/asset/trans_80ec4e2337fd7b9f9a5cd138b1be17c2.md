
第一列和最后一列指示 MDA。最后一行显示每列的总计。以下是一个示例：

```
Statistics from Mon May 6 13:05:24 2002
M msgsfr bytes_from msgsto bytes_to msgsrej msgdis Mailer
4 414 3845K 23 894K 0 0 smtp
8 10 19K 8 13K 0 0 local
====================================================
T 424 3864K 31 907K 0 0
```

接下来的几行与时区处理方式有关：

```
# time zone handling:
# if undefined, use system default
# if defined but null, use TZ envariable passed in
# if defined and non-null, use that info
#O TimeZoneSpec=
```

TimeZoneSpec 选项允许显式选择本地时区，从而覆盖 TZ 环境变量中存在的值。接下来的几行与 sendmail 使用的 UID 和 GID 有关：

```
# default UID (can be username or userid:groupid)
O DefaultUser=8:12
```

DefaultUser 选项指定了 sendmail 投递邮件时切换到的默认用户的 UID 和 GID。在此情况下，它被设置为 mail:mail（UID 8 和 GID 12）。接下来的几行与用户数据库文件的位置有关：

```
# list of locations of user database file (null means no lookup)
O UserDatabaseSpec=/etc/mail/userdb.db
```

UserDatabaseSpec 选项允许指定另一个数据库，该数据库可以重定向传入消息并重写传出消息的头部字段。接下来的几行可用于创建回退连接：

```
# fallback MX host
#O FallbackMXhost=fall.back.host.net

# if we are best MX host for a site, try directly instead of config err
O TryNullMXList=true
```

FallbackMXHost 选项可用于没有可靠互联网连接的站点，在这些站点中，将消息中继到具有更好连接的另一台主机比在本地机器上排队邮件更可取。

如果发送消息的主机同时也是接收主机的 MX（邮件交换器）主机，则所有具有更高 MX 优先级的邮件交换器都被视为无效。如果这导致没有可用的邮件交换器，并且 TryNullMXList 选项设置为 False，消息将退回给发件人。如果该选项设置为 True，sendmail 会在将消息作为无法投递退回之前，尝试直接向接收主机发送邮件。接下来的几行与对高负载平均值的响应有关：

```
# load average at which we just queue messages
#O QueueLA=8

# load average at which we refuse connections
#O RefuseLA=12
```

QueueLA 选项指定了系统负载平均值达到该点时，邮件不会立即投递，而是排队以供稍后处理。RefuseLA 选项设置了不再接受传入邮件的负载平均值点。接下来的几行与子进程和新连接的数量有关：

```
# maximum number of children we allow at one time
#O MaxDaemonChildren=12

# maximum number of new connections per second
#O ConnectionRateThrottle=0
```

Sendmail 分叉自身的一个副本以处理每个传入消息并处理队列。MaxDaemonChildren 选项限制了原始 sendmail 进程可同时存在的子进程数量。虽然这听起来是个好主意，但它也使得某人更容易通过占满所有可用的子进程对你的机器实施拒绝服务攻击。

一个更好的解决方案（如果你必须限制传入连接）是使用 ConnectionRateThrottle 选项。而不是拒绝超过特定阈值的所有连接，ConnectionRateThrottle 选项会减慢消息接受的速度。以使用值 3 为例，如果 8 个连接同时到达，3 个立即得到处理；3 个在一秒延迟后得到处理；剩余的 2 个在两秒延迟后得到处理。接下来的几行与队列作业的处理过程有关：

```
# deliver each queued job in a separate process?
#O ForkEachJob=False
```

ForkEachJob 选项指示 sendmail 分叉自身的一个副本以处理队列中的每个独立消息。这对于内存有限的机器可能有用，但通常不应使用（或设置为 False）。接下来的几行与消息优先级有关：

```
# work recipient factor
#O RecipientFactor=30000

# work class factor
#O ClassFactor=1800

# work time factor
#O RetryFactor=90000

# shall we sort the queue by hostname first?
#0 QueueSortOrder=priority

# minimum time in queue before retry
#0 MinQueueAge=30m
```

ClassFactor 和 RecipientFactor 选项可用于根据消息的优先级类别或收件人数量来更改队列中消息的优先级。RetryFactor 选项可用于更改队列中已经过处理但无法投递的消息的优先级。QueueSortOrder 选项可以选择确定队列优先级的方法，可以设置为 host（队列中的消息根据接收主机和优先级排序）、priority（传统的优先级尺度）和 time（基于提交顺序）。MinQueueAge 设置失败的邮件传输在缓冲区中等待以重试传输的最短时间。接下来的几行与字符集有关：

```
# default character set
#0 DefaultCharSet=iso-8859-1
```

DefaultCharSet 选项定义了在将 8 位消息转换为 7 位消息时使用的 MIME 类型。接下来的几行定义了 service.switch 文件的位置：

```
# service switch file (ignored on Solaris, Ultrix, OSF/1, others)
#0 ServiceSwitchFile=/etc/mail/service.switch
```

由于 /etc/nsswitch.conf 文件已经指定了解析各种数据库请求的顺序，因此 ServiceSwitchFile 选项即使被定义也会被忽略。最好将其保留为注释状态。接下来的几行允许你重新定义 /etc/hosts 文件的位置：

```
# hosts file (normally /etc/hosts)
#0 HostsFile=/etc/hosts
```

HostsFile 选项指定了包含本地自定义的 IP 地址到主机名转换的文件的完整路径。默认值是 /etc/hosts。接下来的几行与连接失败时的拨号延迟有关：

```
# dialup line delay on connection failure
#0 DialDelay=10s
```

当需要建立到互联网的拨号连接时，获取连接所需的时间可能会变化很大。DialDelay 选项允许指定秒数或分钟数，这代表 sendmail 在其初始连接尝试失败时将休眠的时间量。接下来的几行允许你定义当消息中没有收件人时发生什么：

```
# action to take if there are no recipients in the message
#0 NoRecipientAction=add-to-undisclosed
```

NoRecipientAction 选项指示 sendmail 在消息头部行中没有指定收件人时采取什么行动。有效参数包括 add-apparently-to（添加 "Apparently-To:" 头部行）、add-bcc（添加空的 "Bcc:" 头部行以符合 RFC 821）、add-to（添加包含来自消息"信封"中收件人的 "To:" 头部）、add-to-undisclosed（添加空的 "To: undisclosed-recipients:" 头部行）和 none（不作修改地投递消息）。接下来的几行可用于更改 sendmail 使用的根目录：

```
# chrooted environment for writing to files
#0 SafeFileEnvironment=/arch
```

SafeFileEnvironment 选项通过使用 chroot 系统调用，为将邮件投递到文件提供了更安全的位置。接下来的几行定义了地址中的冒号是否可用：

```
# are colons OK in addresses?
#0 ColonOkInAddr=True
```

ColonOkInAddr 选项确定冒号在地址中是否有效。默认值为 False，表示电子邮件地址中的冒号代表错误。接下来的几行定义了你在队列中可以处理多少作业：

```
# how many jobs can you process in the queue?
#0 MaxQueueRunSize=10000
```

MaxQueueRunSize 选项指示在一次队列运行期间可以处理的最大排队消息数。前一行将限制设置为 10,000 条消息。接下来的几行与扩展 CNAMES 有关：

```
# shall I avoid expanding CNAMES (violates protocols)?
#0 DontExpandCnames=False
```

DontExpandCnames 选项控制 sendmail 是否接受 CNAME 记录作为规范主机名。如果 DontExpandCnames 选项设置为 True，CNAME 记录在重写规则中被视为有效。如果设置为 False（默认值），CNAME 记录必须转换为有效的地址记录才能在重写规则中使用。接下来的几行与 SMTP 登录消息有关：

```
# SMTP initial login message (old $e macro)
O SmtgGreetingMessage=$j Sendmail $v/$Z; $b
```

SmtgGreetingMessage 选项定义了在客户端连接到本地机器上的 sendmail 守护进程时显示的横幅文本。在前一行中，$j 评估为本地机器的 FQDN；$v 和 $Z 分别代表配置文件和可执行程序版本；$b 是当前本地日期和时间。这打印出类似以下的一行：

```
220 al.mybox.com ESMP Sendmail 8.11.6-14/8.11.6-14;
 Mon, 6 May 2002 18:47:23 -0400
```
