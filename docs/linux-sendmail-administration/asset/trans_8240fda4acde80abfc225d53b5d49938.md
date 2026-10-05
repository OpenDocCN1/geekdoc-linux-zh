

# 附录 A m4 命令参考

confOLD_STYLE_HEADERS True 让 Sendmail 将不含特殊字符的头部视为旧样式头部。默认值为 true。[OldStyleHeaders]

confOPERATORS 定义地址操作符字符。默认值为 `:%!^/[[]]+`。[OperatorChars]

confPID_FILE 指定 PID 文件的路径。[PidFile]

confPRIVACY_FLAGS 设置限制某些邮件命令的使用。默认值为 warnings（警告）。[PrivacyOptions]

confPROCESS_TITLE_PREFIX 标识在该系统中被用作 `ps` 列表中进程标题前缀的字符串。[ProcessTitlePrefix]

confQUEUE_FACTOR 定义一个值，用于计算当系统加载时何时队列尝试投递的邮件。默认值为 600000。[QueueFactor]

confQUEUE_LA 当达到此负载值时，告诉 Sendmail 直接将邮件发送到队列。默认值为 8。[QueueLA]

confQUEUE_SORT_ORDER 告诉 Sendmail 按优先级（Priority）或主机（Host）顺序对队列进行排序。默认是 Priority。[QueueSortOrder]

confRAND_FILE 如果 Sendmail 在编译时没有包含 `HASURAND` 标志，则标识包含由 STARTTLS 随机数据的文件。[RandFile]

confRECEIVED_HEADER 定义 `Received:` 头部格式。默认值为 `$?$sfrom $. $?$(?s|$_ $) $ j $(v/$2)$?r with $r. id $i$?u for $u.; $b`。

confREFUSE_LA 定义拒绝传入连接的负载值。默认值为 12。[RefuseLA]

confREJECT_MSG 定义邮件因访问控制数据库被拒绝时显示的消息。默认值为 `50 Access denied.`（拒绝访问）。

confRELAY_MAILER 定义中继的默认投递器名称。默认值为 `relay`。

confFRRT_IMPLIES_DSN 告诉 Sendmail 将 `Return-Receipt-To:` 头部解释为投递状态通知（DSN）请求。默认值为 false。[RrtImpliesDsn]

confRUN_AS_USER 告诉 Sendmail 以指定用户运行以读取和投递邮件。仅用于没有普通用户账户的防火墙系统。[RunAsUser]

confSAFE_FILE_ENV 告诉 Sendmail 在写入文件之前 `chroot` 到此目录。通常 Sendmail 不执行 `chroot`。[SafeFileEnvironment]

confSAFE_QUEUE 告诉 Sendmail 在尝试投递之前创建一个队列文件。[SuperSafe]

# 完整命令参考

confSAVE_FROM_LINES 告诉 Sendmail 不要丢弃 Unix 的 `From` 行，这是通常的做法。[SaveFromline]

confSEPARATE_PROC True 告诉 Sendmail 使用单独进程投递消息。默认值为 false。[ForkEachJob]

confSERVER_CERT 标识当此系统作为服务器运行时，使用的加密证书文件。[ServerCertFile]

confSERVER_KEY 标识当此系统作为服务器运行时，包含与加密证书配合使用的私钥的文件。[ServerKeyFile]

confSERVICE_SWITCH_FILE 定义服务切换文件的路径。默认值为 `/etc/mail/service.switch`。[Serviceswitch]

confSEVEN_BIT_INPUT True 强制输入为 7 位。默认值为 false。[SevenBitInput]

confSINGLE_LINE_FROM_HEADER True 强制将多行 `From:` 压缩为单行。默认值为 false。[SingleLineFromHeader]

confSINGLE_THREAD_DELIVERY True 如果也定义了 `HostStatusDirectory`，则强制单线程邮件投递。默认值为 false。[SingleThreadDelivery]

confSMTP_LOGIN_MSG 定义 SMTP 问候消息。默认值为 `$j Sendmail v$/S; $b`。[SMTPGreetingMessage]

confSMTP_MAILER 定义 SMTP 连接的投递器；必须是 `smtp`、`smtp8` 或 `esmtp`。默认值为 `esmtp`。

confTEMP_FILE_MODE 设置临时文件的模式。默认值为 `0600`。[TempFileMode]

confTIME_ZONE 设置来自系统（`USE_SYSTEM`）或 `TZ` 变量（`USE_TZ`）。默认值为 `USE_SYSTEM`。[TimeZoneSpec]

confTO_COMMAND 设置等待命令的最大时间。默认值为 `1h`。[Timeout.command]

confTO_CONNECT 设置等待连接的最大时间。[Timeout.connect]

confTO_CONTROL 设置控制套接字事务完成的最大时间。默认为两分钟（`2m`）。[Timeout.control]

confTO_DATBLOCK 设置 DATA 阶段等待数据块的最大时间。默认值为 `1h`。[Timeout.datablock]

confTO_DATAFINAL 设置等待结束符 `.` 响应的最大时间。默认值为 `1h`。[Timeout.datafinal]

confTO_DATAINIT 设置等待 DATA 命令响应的最大时间。默认值为 `5m`。[Timeout.datainit]

confTO_FILEOPEN 设置等待文件打开的最大时间。默认值为 `60s`。[Timeout.fileopen]

confTO_HELO 设置等待 HELO 或 EHLO 响应的最大时间。默认值为 `5m`。[Timeout.helo]

confTO_HOSTSTATUS 设置过期主机信息的计时器。默认值为 `30m`。[Timeout.hoststatus]

confTO_CONNECT 设置等待对主机首次连接尝试的最大时间。[Timeout.connect]

confTO_IDENT 设置等待 ident 查询响应的最大时间。默认值为 `30s`。[Timeout.ident]

confTO_INITIAL 设置等待初始连接的最大时间。[Timeout.initial]

confTO_MAIL 设置等待 `MAIL` 命令的最大时间。默认值为 `5m`。[Timeout.mail]

confTO_MISC 设置等待其他命令的最大时间。默认值为 `2m`。[Timeout.misc]

confTO_QUEUERT_NONURENT 设置等待非紧急邮件的最大时间。默认值为 `5m`。[Timeout.queuert.nonurgent]

confTO_QUEUERTN_NORMAL 设置等待普通邮件的最大时间。默认值为 `2m`。[Timeout.queuert.normal]

confTO_QUEUERTN_URGENT 设置等待紧急邮件的最大时间。默认值为 `1h`。[Timeout.queuert.urgent]

confTO_QUEUEARN 设置等待队列的最大时间。默认值为 `5d`。[Timeout.queue]

confTO_QUEUEARN_NONURENT 设置等待非紧急邮件的最大时间。默认值为 `30m`。[Timeout.queuearn.nonurgent]

confTO_QUEUEARN_NORMAL 设置等待普通邮件的最大时间。默认值为 `1h`。[Timeout.queuearn.normal]

confTO_QUEUEARN_URGENT 设置等待紧急邮件的最大时间。[Timeout.queuearn.urgent]

confTO_QUEUEWARN 设置等待警告的最大时间。默认值为 `4h`。[Timeout.queewarn]

confTO_QUIT 设置等待 `QUIT` 命令的最大时间。默认值为 `2m`。[Timeout.quit]

confTO_RCPT 设置等待 `RCPT` 命令的最大时间。默认值为 `1h`。[Timeout.rcpt]

confTO_RESOLVER_RETRANS 设置解析重传的计时器（秒）。[Timeout.resolver.retrans]

confTO_RESOLVER_RETRANS_FIRST 设置第一次尝试解析重传的计时器（秒）。[Timeout.resolver.retrans.first]

confTO_RESOLVER_RETRANS_NORMAL 设置首次尝试后解析重传的计时器（秒）。[Timeout.resolver.retrans.normal]

confTO_RESOLVER_RETRY 设置解析查询的总次数。[Timeout.resolver.retry]

confTO_RESOLVER_RETRY_FIRST 设置第一次尝试解析重试的次数。[Timeout.resolver.retry.first]

confTO_RESOLVER_RETRY_NORMAL 设置首次尝试后解析重试的次数。[Timeout.resolver.retry.normal]

confTO_RSET 设置等待 `RSET` 命令的最大时间。默认值为 `5m`。[Timeout.rset]

confTRUSTED_USER 定义控制 Sendmail 进程和 Sendmail 创建的文件的用户。[TrustedUser]

confTRUSTED_USERS 添加允许以用户名发送邮件的用户列表。始终包含 `root`、`ucpd` 和 `daemon`。[$==]

RY_NULL_MX_LIST 当 MX 记录指向本地主机时，让 Sendmail 直接连接远程主机。默认值为 false。[TryNullMXList]

confSAFE_GROUP_WRITES `:include` 和 `.` 转发文件。默认值为 false。[UnsafeGroupWrites]

confUSERDB_SPEC 定义用户数据库文件的路径。[UserDatabaseSpec]

confERRORS_TO True 让 Sendmail 使用 `Errors-To` 头部投递错误。默认值为 false。[UserErrorsTo]

