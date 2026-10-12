
`ForkEachJob`为每个从队列投递的条目运行一个独立的进程，这以速度为代价减少了处理队列所需的内存量。

`ForwardPath=path`定义搜索`.forward`文件的路径。可以通过冒号分隔来定义多个路径。默认值为`$z/. sw=$z/`，`forward`。

`HelpFile=path`定义帮助文件的路径。

`Expensive`告知`Sendmail`对设置了（`expensive`）`mail`标志的传出投递器队列邮件。通常，邮件会立即投递。

`HostsFile=path`定义`hosts`文件的路径。默认值为`/etc/hosts`。

`HostStatusDirectory=path`定义存储状态信息的目录。

`IgnoreDots`导致`Sendmail`忽略输入消息中的点。`SMTP`邮件中的点会被忽略，因为它们用于标记邮件消息的结束。

`LDAPDefaultSpec=specification`定义用于`LDAP`数据库的默认规范。

`LogLevel=n`告知`Sendmail`在日志文件中存储多少详细信息。`n`默认值为`9`，这通常提供了足够的详细信息。

`MatchGECOS`电子邮件地址中的用户名将与别名数据库和`passwd`文件中的用户名进行比对，以确定用户是否为本地用户。此选项增加了对`passwd`文件中`GECOS`字段的检查。

`MaxAliasRecursion=n`别名在最终解析为实际邮件之前会指向其他别名。此选项定义了别名在解析为邮件地址时可以嵌套的深度。`n`的默认值为`10`。

`MaxDaemonChildren=n`告知`Sendmail`，当有`n`个子进程正在处理输入邮件时，拒绝连接。通常情况下，`Sendmail`不对子进程设置任何任意限制。

`MaxHeadersLength=bytes`定义了所有头部信息总和允许的最大长度。

`MaxCount=n`告知`Sendmail`，当消息被处理超过`n`次时，假设其为循环邮件。默认值为`25`。

`MaxSizeSize=n`设置在响应`ESMMTP EHLO`命令时通告的最大消息大小。大于此大小的消息将被拒绝。

`MaxMimeHeaderLength=size`定义`MIME`头部字段的最大长度。

`MaxQueueRunSize=n`设置单次队列运行可以处理的条目最大数量。默认无限制。

`MaxRecipientsPerMessage=n`限制单条消息的最大接收者数量。如果未指定，则不受限制。

`MeToo`告知`Sendmail`将消息的副本发回给发送者。

`MinFreeBlocks=n`告知`Sendmail`，除非队列有`n`个空闲磁盘块，否则拒绝输入邮件。

`MinQueueAge=n`告知`Sendmail`跳过任何在队列中少于`n`分钟的任务。

`MustQuoteChars=[]`定义添加到集合中的字符列表。如果指定了`MustQuoteChars`但未指定字符值，则会将`.`和`'`添加到标准的带引号字符集中。

`NoRecipientAction=action`告知`Sendmail`当消息没有有效的接收者头部时该做什么。`action`可以是：

- `none`原封不动地传递消息。
- `add-to`使用信封中的接收者地址添加一个`To`头部。
- `add-apparently-to`添加一个`Apparently-To:`头部。
- `add-to-undisclosed`添加一个`To: undisclosed-recipients;`头部。
- `add-bcc`添加一个空的`Bcc:`头部。

`OldStyleHeaders`允许空格分隔名称。通常情况下，用逗号分隔名称。

`OperatorChars=chars`列出用于在地址重写中确定标记的操作符字符。

`Pidfile=path`指定`Sendmail PID`的路径。

`PostmasterCopy=username`告知`Sendmail`将错误消息的副本发送给`username`。默认是不向该账户发送错误消息副本。

`PrivacyOptions=options`设置`SMTP`协议选项。`options`值是包含一个或多个关键字的逗号分隔列表：

- `public`允许使用所有命令。
- `needmailhelo`在接受`MAIL From:`头部之前，需要有效的`HELO`或`EHLO`命令。
- `needexpnhello`在接受`EXPN`命令之前，需要有效的`HELO`或`EHLO`命令。
- `noexpn`禁用`EXPN`命令。
- `needvrfyhelo`在接受`VRFY`命令之前，需要有效的`HELO`和`EHLO`命令。
- `novrf`禁用`VRFY`命令。
- `restrictmail`限制对队列目录有访问权限的用户使用`mailq`命令。
- `restrictqrun`告知`Sendmail`只有`root`用户和队列目录的所有者允许运行队列。
- `norecept`告知`Sendmail`不要返回确认投递成功的邮件。
- `goaway`禁用所有`SMTP`状态查询。
- `authwarnings`告知`Sendmail`在消息中插入`X-Authentication-Warning:`头部。

`ProcessTitlePrefix=prefix`定义了一个用于进程状态报告标题的字符串。

`QueueDirectory=path`定义队列目录。

`QueueFactor=factor`这是一个数值，用于结合当前负载与负载平均限制之差以及邮件优先级，以确定邮件是否应该队列或立即发送。其思路是当系统当前负载过大时对邮件进行队列。默认值为`600,000`。

`QueueLA=n`告知`Sendmail`当系统负载平均值超过`n`时队列邮件。默认值为`8`。

`QueueSort=sequence`定义队列排序的序列。优先级排序是默认。有效的序列值有：

- `h`按主机名序列排序。
- `t`按提交时间序列排序。
- `p`按邮件优先级排序。

`RandFile=file`指向一个包含用于加密技术的伪随机数据的文件。这仅在编译选项`HASURANDOM`不可用时使用。

`RecipientFactor=factor`告知`Sendmail`取每个接收者的任务的较低值，以便使接收者数量大的任务优先级较低。默认值为`30,000`。

`RefuseLA=n`告知`Sendmail`当系统负载平均值超过`n`时拒绝传入的`SMTP`连接。默认值为`12`。

## 目录 C Sendmail 变量、选项和标志

`ResolverOptions=options`设置解析选项。可用选项有：`debug`、`aonly`、`usevc`、`igntc`、`recurse`、`defnames`、`stayopen`和`dsnrc`。该选项前可以加（`+`）号以启用或加减号（`-`）以禁用。另一个选项`HasWildcardMX`在指定时不需要加`+`或`-`。只需添加`HasWildcardMX`即可开启该选项。有关解析选项的更多信息，请参见`Craig Hunt`编写的《`Linux DNS Server Administration`》(`Syex`, `2000`)。

`RetryFactor=factor`因子用于在每次处理任务时降低其优先级，以便无法投递的邮件不会不断出现在队列顶端。默认值为`90,000`。

`RunAsUser=userid[:groupid]`定义`Sendmail`运行身份而非`root`身份的用户`ID`和组`ID`。当`Sendmail`运行在维护良好的防火墙上时，这可能会增强安全性。通用情况下，这可能会降低安全性，因为这需要许多文件对该用户`ID`可读可写。

`SafeFileEnvironment=directory`告诉`Sendmail`在写入文件之前切换到（`chroot`）指定的目录，并拒绝使用符号链接。

`SaveFromLine`告诉`Sendmail`使用标头前面的`Unix`风格行。通常情况下，这些行会被丢弃。

`SendMIMEErrors`告诉`Sendmail`以`MIME`格式发送错误消息。

`ServerCertificate=file`识别当系统作为邮件服务器运行时，`Sendmail`应该使用的证书文件。

`ServerKey=file`识别当系统作为邮件服务器运行时，`Sendmail`应该使用的私钥文件。

`ServiceSwitch=path`定义一个文件路径，该文件列出了用于各种服务的方法。`ServiceSwitchFile`包含以名称开头后跟服务方法的条目。`Sendmail`会检查名为`aliases`和`hosts`的服务，并支持尽可能少的服务方法，假设所有这些方法已编译到此版本的`mail`程序中。在`Sendmail 8.11`中，`ServiceSwitchFile`默认为`/etc/mail/service.switch`。如果文件不存在，`Sendmail`将使用以下服务方法：`aliases`和`hosts`，`dns`、`nis`、`nisplus`，最后是`hosts`文件。大多数`Linux`系统都有由`nswitch.conf`文件配置的内置切换功能，因此会被使用且该选项会被忽略。请参见《`Linux DNS Server Administration`》书书中关于`nswitch.conf`的描述。
