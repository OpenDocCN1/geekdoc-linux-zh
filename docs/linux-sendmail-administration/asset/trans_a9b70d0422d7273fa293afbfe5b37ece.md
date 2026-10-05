

# 目录 C Sendmail 变量、选项和标志

ResolverOptions=options 设置解析选项。可用选项有：debug, aonly, usevc, igntc, recurse, defnames, stayopen 和 dsnrc。该选项前可以加 (+) 号以启用或加减号 (-)以禁用。另一个选项 HasWildcardMX 在指定时不需要加 + 或 -。只需添加 HasWildcardMX 即可开启该选项。有关解析选项的更多信息，请参见 Craig Hunt 编写的《Linux DNS Server Administration》(Syex, 2000)。

RetryFactor=factor 因子用于在每次处理任务时降低其优先级，以便无法投递的邮件不会不断出现在队列顶端。默认值为 90,000。

RunAsUser=userid[:groupid] 定义 Sendmail 运行身份而非 root 身份的用户 ID 和组 ID。当 Sendmail 运行在维护良好的防火墙上时，这可能会增强安全性。通用情况下，这可能会降低安全性，因为这需要许多文件对该用户 ID 可读可写。

SafeFileEnvironment=directory 告诉 Sendmail 在写入文件之前切换到（chroot）指定的目录，并拒绝使用符号链接。

SaveFromLine 告诉 Sendmail 使用标头前面的 Unix 风格行。通常情况下，这些行会被丢弃。

SendMIMEErrors 告诉 Sendmail 以 MIME 格式发送错误消息。

ServerCertificate=file 识别当系统作为邮件服务器运行时，Sendmail 应该使用的证书文件。

ServerKey=file 识别当系统作为邮件服务器运行时，Sendmail 应该使用的私钥文件。

ServiceSwitch=path 定义一个文件路径，该文件列出了用于各种服务的方法。ServiceSwitchFile 包含以名称开头后跟服务方法的条目。Sendmail 会检查名为 aliases 和 hosts 的服务，并支持尽可能少的服务方法，假设所有这些方法已编译到此版本的 mail 程序中。在 Sendmail 8.11 中，ServiceSwitchFile 默认为 /etc/mail/service.switch。如果文件不存在，Sendmail 将使用以下服务方法：aliases 和 hosts，dns, nis, nisplus，最后是 hosts 文件。大多数 Linux 系统都有由 nswitch.conf 文件配置的内置切换功能，因此会被使用且该选项会被忽略。请参见《Linux DNS Server Administration》书书中关于 nswitch.conf 的描述。

SevenBitInput 导致 Sendmail 将输入剥离为七位，以兼容旧系统。这通常不是必要的。

SingleLineFromHeader 为了兼容某些版本的 Lotus Notes，导致 Sendmail 将带有嵌入换行符的 From: 行折叠为一行。

SingleThreadDelivery 告诉 Sendmail 不要同时向远程主机打开多个一个 SMTP 连接。此选项仅在也指定了 HostStatusDirectory 选项时有效。

SmtpGreetingMessage 定义了当远程主机连接到 SMTP 服务器端口时发送给该主机的问候。

StatusFile 告诉 Sendmail 在指定文件中记录摘要统计数据。默认情况下不记录摘要统计数据。

SuperSafe 告诉 Sendmail 在尝试即时投递时，为每封邮件创建一个队列文件。

TempfileMode=mode 设置队列文件的访问权限。mode 是八进制值。默认值为 0600。

Timeout.command=timeout 定义 Sendmail 在发布命令时等待的时间。

Timeout.connect=timeout 定义 Sendmail 等待连接的时间。

Timeout.control=timeout 定义 Sendmail 等待控制套接字传输完成的时间。

Timeout.datblock=timeout 定义 Sendmail 在 DATA 阶段等待数据块的时间。

Timeout.datafinal=timeout 定义 Sendmail 等待点号 (.) 结束 DATA 阶段响应的时间。

Timeout.datainit=timeout 定义 Sendmail 等待 DATA 命令响应的时间。

Timeout.fileopen=timeout 定义 Sendmail 等待文件打开的时间。

Timeout.helo=timeout 定义 Sendmail 等待 HELO 或 EHLO 命令响应的时间。

Timeout.hoststatus=timeout 定义 Sendmail 在决定信息过期前保留主机状态信息的时间。

Timeout.iconnect=timeout 定义 Sendmail 等待消息中第一个主机连接完成的时间。

Timeout.ident=timeout 定义 Sendmail 等待 ident 查询响应的时间。

Timeout.initial=timeout 定义 Sendmail 等待初始连接响应的时间。

Timeout.mail=timeout 定义 Sendmail 等待 MAIL 命令响应的时间。

Timeout.misc=timeout 定义 Sendmail 等待任何未被计时器覆盖的 SMTP 命令响应的时间。

Timeout.queuerturn=timeout 定义 Sendmail 在将消息返回给发送者之前在队列中保留的时间。

Timeout.queuerturn.non-urgent=timeout 定义 Sendmail 在将非紧急消息返回给发送者之前在队列中保留的时间。

Timeout.queuerturn.normal=timeout 定义 Sendmail 在将普通消息返回给发送者之前在队列中保留的时间。

Timeout.queuerturn.urgent=timeout 定义 Sendmail 在将紧急消息返回给发送者之前在队列中保留的时间。

Timeout.queewarn=timeout 定义 Sendmail 在警告发送者消息已入队列且尚未投递之前在队列中保留的时间。

Timeout.queewarn.non-urgent=timeout 定义 Sendmail 在警告发送者非紧急消息已入队列且尚未投递之前在队列中保留的时间。

Timeout.queewarn.normal=timeout 定义 Sendmail 在警告发送者普通消息已入队列且尚未投递之前在队列中保留的时间。

Timeout.queewarn.urgent=timeout 定义 Sendmail 在警告发送者紧急消息已入队列且尚未投递之前在队列中保留的时间。

Timeout.quit=timeout 定义 Sendmail 等待 QUIT 命令响应的时间。

Timeout.rcpt=timeout 定义 Sendmail 等待 RCPT 命令响应的时间。

Timeout.resolver.retrans=timeout 设置首次和非解析查询的重传间隔。

Timeout.resolver.retrans.first=timeout 设置给定查找首次解析查询的超时时间。

Timeout.resolver.retrans.normal=timeout 设置普通解析查询的超时时间。

Timeout.resolver.retry=retries 设置重传解析查询的次数。

Timeout.resolver.retry.first=retries 设置重传给定查找首次解析查询的次数。

Timeout.resolver.retry.normal=retries 设置重传普通解析查询的次数。

Timeout.rset=timeout 定义 Sendmail 等待 RSET 命令响应的时间。

TimeZoneSpec=tzinfo 将时区设置为 tzinfo。如果未设置 TimeZoneSpec，则使用系统默认值；如果为空，则使用用户的 TZ 环境变量。

TrustedUser=users 定义信任使用其他用户名发送邮件的用户列表。

TryNullMXlist 导致 Sendmail 直接连接到远程主机。

UnixFromLine=from 定义 Unix 风格表单格式。

UnsafeGroupWrites 防止 Sendmail 允许组可写的文件通过 :include 和 . 引用程序或写入文件。世界可写的文件始终受这些限制。

UseErrors 告诉 Sendmail 将错误消息返回给 Errors-T 头部列出的地址。通常，错误发送到信封的发送者地址。

DatabaseSpec=udbspec 定义用户数据库规范。

XscriptFileBufferSize=bytes 指定处理 xf 队列文件时使用的缓冲区内存大小。

# Mailer 标志

Mailer 标志在定义 定义的 F 字段中声明。每个er 标志通过代表该标志的单个字符来设置。例如，F=1sDFMe 设置了六不同的标志。表 C.5 列出了每个标志的单字符名称和功能。

