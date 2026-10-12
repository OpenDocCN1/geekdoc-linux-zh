
## 表 9-1 *续*

| 选项 | 说明 |
| :--- | :--- |
| ConnectionCacheTimeout=5m | 空闲期间缓存连接保持打开状态的最长时间（以分钟计）。 |
| ConnectionRateThrottle=20 | 允许每秒接收连接的最大守护进程数量。将此值设置为 0 则允许每秒使用无限数量（即系统资源允许的最大限度）的守护进程。 |
| DefaultUser=8:12 | 邮件服务器的默认用户和组。UID 8 是 `/etc/passwd` 中用户 *mail* 的默认值，GID 12 是 `/etc/group` 中组 *mail* 的默认值。不建议更改。 |
| DeliveryMode=background | 在后台运行 sendmail。无需更改。 |
| EightBitMode=pass8 | 设置八位数据的处理方式。保持默认值即可。 |
| ForkEachJob=False | 当设置为 **True** 时，会分叉一个独立的进程来处理队列中的每条消息。无需更改。 |
| ForwardPath=$z/.forward,$w+$h:$Z/.forward+$h$Z/.forward | 搜索每个用户 *forward* 文件的路径。无需更改。 |
| HelpFile=/usr/lib/sendmail.hf | 设置帮助文件的位置。 |
| HoldExpensive=False | 当设置为 **True** 时，昂贵的邮件服务器（在 ML 文件中通过 **F=** 标志标记的邮件服务器）不允许立即连接。保持默认值。 |
| HostStatusDirectory=,hoststat | 设置主机状态信息的目录名称。默认值将目录设置为 */var/spool/mqueue/.hoststat*。无需更改。 |
| HostsFile=/etc/hosts | 设置主机文件名。无需更改。 |
| LogLevel=8 | 设置默认日志级别。无需更改。 |
| MatchGECOS=False | 当设置为 **True** 时，sendmail 会在 `/etc/passwd` 文件中执行模糊搜索，以查找每个密码条目的 GECOS 字段中“相似”的用户名。建议使用默认值。 |
| MaxDaemonChildren=40 | 任何时刻分叉的子进程的最大数量。 |
| MaxHopCount=30 | 消息在被拒绝之前可以被处理的最大时间长度。 |
| MaxMessageSize=5000000 | 消息的最大字节数。大于此大小的消息将不被接受。 |
| MeToo=False | 当别名包含发件人本身时，sendmail 会自动从扩展中移除发件人。如果此选项设置为 True，在此情况下发件人将收到邮件。您可能希望将此设置为 True，因为这可以减少因用户希望即使邮件源自其自身也能收到邮件而打来的技术支持电话。 |
| MinFreeBlocks=100 | sendmail 接受消息前必须存在的自由块的最小数量。这使您可以确保某人无法通过邮件轰炸（即向您的服务器发送大量大型邮件副本）来耗尽您的磁盘空间。您可能希望将此值增加到高于默认值的数值。 |
| MinQueueAge=10m | 消息必须在队列中停留至少指定的分钟数后才被处理。 |
| NoRecipientAction=add-to-undisclosed | 当消息不包含适当的收件人头部时，将执行指定的操作。默认值创建一个 To: undisclosed-recipients 头部。 |
| OldStyleHeaders=True | 切换旧/新头部格式。无需更改。 |
| OperatorChars=.:!*'"/[\]#+ | 标记分隔符字符的列表。无需更改。 |
| PrivacyOptions=needvrifyhelo, restrictmailq, restrictrctrout, gonawy | 有关详细信息，请参阅本章中“保护 sendmail”部分中关于确保隐私的内容。 |
| QueueDirectory=/var/spool/mqueue | 队列目录的完全限定路径名。 |
| QueueLimit=8 | 当系统负载平均值超过指定数字时，不要发送消息，而是将其放入队列。 |
| QueueSortOrder=Host | 设置队列排序顺序。默认值允许 sendmail 使用收件人的主机名对队列进行排序。您可以将其更改为 **Priority** 以按优先级头部排序，或更改为 **Time** 以按提交时间排序。 |
| RecipientFactor=30000 | 用于降低拥有大量收件人的消息的优先级。 |
| RefuseLimit=12 | 当系统负载平均值超过指定值时，拒绝传入连接。 |
| RetryFactor=90000 | 用于降低优先级。不建议更改。 |
| RunAsUser=mail | 指定 sendmail 为其所有子进程使用的用户名。换句话说，sendmail 分叉以处理实际请求的子进程并非以超级用户身份运行；因此，这增强了安全性。不建议更改。 |
| SendMIMErrors=True | 当设置为 True 时，错误消息使用 MIME 格式设置。不建议更改。 |
| SevenBitInput=False | 当设置为 True 时，消息将被转换为七位数据。请勿更改默认值。 |
| OSmtgGreetingMessage=$j Sendmail $v/$N; $b | 设置 sendmail 在建立连接时发出的问候消息。如果您不希望向外界透露您使用的 sendmail 版本，请从此行中移除 $v 和 $N 变量。这可能会为试图利用安全漏洞的人提供较少的线索。 |
| StatusFile=/var/log/sendmail.st | 状态文件的完全限定路径名。 |
| SuperSafe=True | 切换超级安全模式。建议使用默认设置。 |
| TempFileMode=0600 | 设置队列中临时文件的默认模式。 |
| Timeout.command=30m | SMTP 命令的默认超时值。 |
| Timeout.connect=3m | 连接的默认超时值。 |
| Timeout.datablock=1h | 数据块的默认超时值。 |
| Timeout.datafinal=1h | 数据中 *final* 的默认超时值。 |
| Timeout.datainit=5m | DATA 命令的默认超时值。 |
| Timeout.fileopen=60s | 打开 forward 和 include 文件的默认超时值。 |
| Timeout.helo=5m | HELO 命令的默认超时值。 |
| Timeout.hoststatus=10m | 主机状态在指定的超时周期后变为过期。 |
| Timeout.iconnect=10s | 连接的默认超时值。 |
| Timeout.initial=5m | 初始问候消息的默认超时值。 |
| Timeout.mail=10m | MAIL 命令的默认超时值。 |
| Timeout.misc=2m | NOOP 或 VERB 命令的默认超时值。 |
| Timeout.quereturn.non-urgent=7d | 非紧急消息退回给发件人之前的时间段长度。 |
| Timeout.quereturn.normal=5d | 普通消息退回给发件人之前的时间段长度。 |
| Timeout.quereturn.urgent=2d | 紧急消息退回给发件人之前的时间段长度。 |
| Timeout.quereturn=5d | 消息退回给发件人之前的时间段长度。 |
| Timeout.queuewarn.non-urgent=12h | 因未投递的非紧急消息而向发件人发送警告之前的时间段长度。 |
| Timeout.queuewarn.normal=6h | 因未投递的普通消息而向发件人发送警告之前的时间段长度。 |
| Timeout.queuewarn.urgent=2h | 因未投递的紧急消息而向发件人发送警告之前的时间段长度。 |
| Timeout.queuewarn=6h | 因未投递消息而向发件人发送警告之前的时间段长度。 |
| Timeout.quit=2m | QUIT 命令的默认超时值。 |
| Timeout.rcpt=30m | RCPT 命令的默认超时值。 |
| Timeout.reset=5m | RSET 命令的默认超时值。 |
| UnixFromLine=From $g $d | 定义 Unix 风格 From 行使用的格式。请勿更改默认值。 |
| UnsafeGroupWrites=True | 当设置为 **True** 时，诸如 `forward` 和 `include` 等文件如果可被组写入，则被视为不安全。请勿更改默认值。 |
| UseErrorsTo=False | 当设置为 **True** 且发生错误时，sendmail 使用 `ErrorsTo` 头部（如果可用）来报告错误。请勿更改默认值。 |

### P：优先级定义

P 行用于设置 Precedence: 头部字段的值。此类行的语法如下：

*P字段名* = 值

例如：

Pfirst-class=0

### V：配置版本级别

V 行用于与旧版本的配置保持兼容。您无需对这样的行进行任何更改。

### K：键文件声明

K 行用于定义映射。此类行的语法如下：

*K映射名 映射类 参数*

例如：

Kaccess hash -o /etc/mail/access.db

## 配置 /etc/mail/* 文件

本小节讨论位于 /etc/mail 目录中的 sendmail 配置文件。

