
当需要建立到互联网的拨号连接时，获取连接所需的时间可能会变化很大。`DialDelay` 选项允许指定秒数或分钟数，这代表 `sendmail` 在其初始连接尝试失败时将休眠的时间量。接下来的几行允许你定义当消息中没有收件人时发生什么：

```
# action to take if there are no recipients in the message
#0 NoRecipientAction=add-to-undisclosed
```

`NoRecipientAction` 选项指示 `sendmail` 在消息头部行中没有指定收件人时采取什么行动。有效参数包括 `add-apparently-to`（添加 "Apparently-To:" 头部行）、`add-bcc`（添加空的 "Bcc:" 头部行以符合 RFC 821）、`add-to`（添加包含来自消息"信封"中收件人的 "To:" 头部）、`add-to-undisclosed`（添加空的 "To: undisclosed-recipients:" 头部行）和 `none`（不作修改地投递消息）。接下来的几行可用于更改 `sendmail` 使用的根目录：

```
# chrooted environment for writing to files
#0 SafeFileEnvironment=/arch
```

`SafeFileEnvironment` 选项通过使用 `chroot` 系统调用，为将邮件投递到文件提供了更安全的位置。接下来的几行定义了地址中的冒号是否可用：

```
# are colons OK in addresses?
#0 ColonOkInAddr=True
```

`ColonOkInAddr` 选项确定冒号在地址中是否有效。默认值为 `False`，表示电子邮件地址中的冒号代表错误。接下来的几行定义了你在队列中可以处理多少作业：

```
# how many jobs can you process in the queue?
#0 MaxQueueRunSize=10000
```

`MaxQueueRunSize` 选项指示在一次队列运行期间可以处理的最大排队消息数。前一行将限制设置为 10,000 条消息。接下来的几行与扩展 CNAMES 有关：

```
# shall I avoid expanding CNAMES (violates protocols)?
#0 DontExpandCnames=False
```

`DontExpandCnames` 选项控制 `sendmail` 是否接受 CNAME 记录作为规范主机名。如果 `DontExpandCnames` 选项设置为 `True`，CNAME 记录在重写规则中被视为有效。如果设置为 `False`（默认值），CNAME 记录必须转换为有效的地址记录才能在重写规则中使用。接下来的几行与 SMTP 登录消息有关：

```
# SMTP initial login message (old $e macro)
O SmtgGreetingMessage=$j Sendmail $v/$Z; $b
```

`SmtgGreetingMessage` 选项定义了在客户端连接到本地机器上的 `sendmail` 守护进程时显示的横幅文本。在前一行中，`$j` 评估为本地机器的 FQDN；`$v` 和 `$Z` 分别代表配置文件和可执行程序版本；`$b` 是当前本地日期和时间。这打印出类似以下的一行：

```
220 al.mybox.com ESMP Sendmail 8.11.6-14/8.11.6-14;
 Mon, 6 May 2002 18:47:23 -0400
```

下一行定义了 `UnixFromLine`：

```
# UNIX initial From header format (old $1 macro)
O UnixFromLine=From $g $d
```

`UnixFromLine` 选项定义了邮件箱文件内用作消息分隔符的“From”头行的格式。`$g $d` 的默认值会打印发件人的电子邮件地址，随后是两个空格以及接收该消息时的本地日期和时间。接下来的行定义了如何处理嵌入式换行符：

```
# From: lines that have embedded newlines are unwrapped onto one line
#O SingleLineFromHeader=False
```

如果将 `SingleLineFromHeader` 选项设置为 `True`，“From:”头内的所有新行将被转换为空格。否则，拆分的头行将保留。接下来的行与 SMTP 如何响应未关联主机名的 HELO 请求有关：

```
# Allow HELO SMTP command that does not include a host name
#O AllowBogusHELO=False
```

如果将 `AllowBogusHELO` 选项设置为 `True`，则不会强制要求 HELO 命令后必须跟有主机名。如果设置为 `False`（默认值），则要求遵循 RFC 1123 指定的行为。接下来的行与引用特殊字符有关：

```
# Characters to be quoted in full name phrase (@,;:\\\\()[]{ } are automatic)
#O MustQuoteChars=.
```

默认情况下（根据 RFC 821），如果注释中列举的九个字符出现在地址的非地址部分（例如，用户名或昵称）中，则必须对其进行引用。可以在 `MustQuoteChars` 选项中指定 `.` 和 `’` 字符，以同样要求对其引用。接下来的行与分隔符字符有关：

```
# delimiter (operator) characters (old $o macro)
O OperatorChars=..:%!~/[]+
```

`OperatorChars` 选项列出了除 `sendmail` 已定义的 `(),<>;\"\r\n` 字符集外，可以在地址内用作分隔符的字符。不应修改此选项。接下来的行与 `initgroups` 有关：

```
# shall I avoid calling initgroups(3) because of high NIS costs?
#O DontInitGroups=False
```

`DontInitGroups` 选项（如果设置为 `True`）会强制 `sendmail` 不处理 `initgroups` 系统调用。如果组包含许多成员或使用了缓慢的名称服务，这将非常有用。默认值为 `False`。接下来的行与一个已过时的功能有关：

```
# are group-writable :include: and .forward files (un)trustworthy?
#O UnsafeGroupWrites=True
```

`UnsafeGroupWrites` 选项实际上已被 `DontBlameSendmail` 选项的各种参数所取代，该选项在本节开头已讨论过。接下来的行与发送错误有关：

```
# where do errors that occur when sending errors get sent?
#O DoubleBounceAddress=postmaster
# where to save bounces if all else fails
#O DeadLetterDrop=/var/tmp/dead.letter
```

`DoubleBounceAddress` 选项指定了由于无法投递先前错误消息而导致的错误消息的接收者。默认值是 `postmaster` 别名。`DeadLetterDrop` 选项设置了备用位置，用于保存无法写入其他位置的退回邮件（默认为 `/var/tmp/dead.letter`）。接下来的行与用于 `sendmail` 处理的用户 ID 有关：

```
# what user id do we assume for the majority of the processing?
#O RunAsUser=sendmail
```

通过使用 `RunAsUser` 选项，可以配置 `sendmail` 以非特权用户身份执行其大部分处理工作（除了读取配置文件和监听特权端口上的传入连接）。`RunAsUser` 选项指定用户的用户名或 UID。这听起来像是个好主意，但其副作用是要求非特权用户能够访问所有 `.forward` 文件、`include:` 文件以及队列目录。这可能需要广泛使用 `DontBlameSendmail` 选项，并可能导致比解决的问题更多的新问题。接下来的行与 SMTP 信封中的收件人有关：

```
# maximum number of recipients per SMTP envelope
#O MaxRecipientsPerMessage=100
```

`MaxRecipientsPerMessage` 选项指定每个消息中单独收件人数的上限，旨在阻止邮件垃圾（非请求的商业电子邮件或非请求的批量电子邮件），这些邮件通常发送给大型分发列表。默认情况下没有限制。接下来的行与获取本地名称有关：
