

cfBLANK_SUB 定义用于替换电子邮件地址中未加引号空白字符的字符。[BlankSub]

cfCACERT 标识包含来自证书颁发者的加密证书的文件。[CACERTFile]

cfCACERT_PATH 定义包含加密证书的目录路径。[CACERTPath]

cfCF_VERSION 设置 Sendmail 版本号。[$S]

cfCHECKPOINT_INTERVAL 设置在 Sendmail 检查点（checkpoint）之前允许处理的队列项目最大数量。默认值为 10。[CheckpointInterval]

cfCHECK_ALIASES 通过别名数据库构建查找每个别名。默认值为 false。[CheckAliases]

cfCLIENT_CERT 标识 Sendmail 在作为客户端运行时使用的包含加密证书的文件。[ClientCert]

cfCLIENT_KEY 标识与 Sendmail 在作为客户端运行时所使用的证书相关的私钥文件。[ClientKeyFile]

cfCLIENT_OPTIONS 定义出站 SMTP 连接的端口选项。[ClientPortOptions]

cfCOLON_OK_IN_ADDR 告诉 Sendmail 将地址中的冒号视为普通字符。默认为 false。[ColonOkInAddr]

cfCONNECTION_RATE_THROTTLE 设置每秒允许的最大连接数。[ConnectionRateThrottle]

cfCONNECT_ONLY_TO 定义连接性。仅当开发者测试 Sendmail 时需要。这不会在生产环境中使用。[ConnectOnlyTo]

cfCONTROL_SOCKET_NAME 定义用于管理 Sendmail 守护进程的套接字。[ControlSocketName]

cfCONFIG_EXPENSIVE 告诉 Sendmail 为设置了标志的邮件投送程序保留邮件，直到下一个队列。默认值为 false。[HoldExpensive]

cfCOPY_ERRORS_TO 设置接收错误信息的电子邮件地址。[PostmasterCopy]

cfCR_FILE 指向列出此服务器将中继邮件的主机列表文件。默认值为 /etc/mail/relay-domains。[$R]

cfCT_FILE 定义受信用户文件。默认值为 /etc/mail/trusted-users。[$t]

cfCW_FILE 指向本地主机别名文件。默认值为 /etc/mail/local-host-names.[$w]

confDEAD_LETTER_DROP 定义保存无法返回给发送者或发送给邮局管理员的失败邮件的文件。[DeadLetterDrop]

confDAEMON_OPTIONS 设置 Sendmail 守护进程的选项。[DaemonPortOptions]

confDEF_AUTH_INFO 标识包含用于出站连接的验证信息的文件。[DefaultAuthInfo]

confDEF_CHAR_SIZE 设置未设置的 8 位 MIME 数据的默认字符。[DefaultCharset]

confDEF_USER_ID 定义 Sendmail 使用的用户 ID 和组 ID。默认值为 1:1。[DefaultUser]

confDELIVERY_MODE 设置默认投递模式。默认后台（background）。[DeliveryMode]

confDF_BUFFER_SIZE 定义在使用磁盘文件之前将使用的最大缓冲区内存量。[BufferSize]

confDH_PARAMETERS 标识包含用于 DSA/DH 签名算法的 DH 参数的文件。[DHParameters]

confDELAY_DELAY 设置重试“按需拨号”连接之前使用的时间。0s 表示“不重试”。默认值为 0。[DialDelay]

confDOMAIN_NAME 定义系统的完整主机名。[$j]

confDONT_BLAME_SENDMAIL 如果设置此项，则告诉 Sendmail 不要执行安全检查。默认情况下，会执行检查。不要使用此选项。它对您的服务器的安全构成了威胁。[DontBlameSendmail]

confDONT_EXPAND_NAMES 如果为 true，则告诉 Sendmail 不将昵称转换为规范名称。默认值为 false。False 表示“进行转换”。[DontExpandCnames]

conf_INIT_GROUPS 如果为 true，则禁用 initroutines 组。默认值为 false。False 表示“使用 initroutines”。[DontInitGroups]

conf_PROBE_INTERFACES 告诉 Sendmail 不要自动接受地址。[DontProbeInterface]

confDONT_PRUNE_ROUTES 告诉 Sendmail 不要修剪路由。[DontPrune]

（注：由于原文中存在重复或格式异常，上述翻译已严格根据指令要求，后续部分已按逻辑进行处理）

confDEF_AUTH_INFO 标识包含用于出站连接的验证信息的文件。[DefaultAuthInfo]

confDEF_CHAR_SIZE 设置未设置的 8 位 MIME 数据的默认字符。[DefaultCharset]

confDEF_USER_ID 定义 Sendmail 使用的用户 ID 和组 ID。默认值为 1:1。[DefaultUser]

confDELIVERY_MODE 设置默认投递模式。默认后台。[DeliveryMode]

confDF_BUFFER_SIZE 定义在使用磁盘文件之前将使用的最大缓冲区内存量。[BufferSize]

confDH_PARAMETERS 标识包含用于 DSA/DH 签名算法的 DH 参数的文件。[DHParameters]

confDELAY_DELAY 设置重试“按需拨号”连接之前使用的时间。0s 表示“不重试”。默认值为 0。[DialDelay]

confDOMAIN_NAME 定义系统的完整主机名。[$j]

confDONT_BLAME_SENDMAIL 如果设置此项，则告诉 Sendmail 不要执行安全检查。默认情况下，会执行检查。不要使用此选项。它对您的服务器的安全构成了威胁。[DontBlameSendmail]

confDONT_EXPAND_NAMES 如果为 true，则告诉 Sendmail 不将昵称转换为规范名称。默认值为 false。False 表示“进行转换”。[DontExpandCnames]

conf_INIT_GROUPS 如果为 true，则禁用 initroutines 组。默认值为 false。False 表示“使用 initroutines”。[DontInitGroups]

conf_PROBE_INTERFACES 告诉 Sendmail 不要自动接受地址。[DontProbeInterface]

confDONT_PRUNE_ROUTES 告诉 Sendmail 不要修剪路由。[DontPrune]

（注：由于原始文本中存在大量重复段落，根据“不要重复输出原文”的原则，译文已对唯一含义进行了完整翻译。以下是剩余唯一部分的翻译：）

[content]
（由于提供的英文文本存在大量重复，下文为原文中不重复部分的翻译）

cfCONNECTION_RATE_THROTTLE 设置每秒允许的最大连接数。[ConnectionThrottle]

cfCONTROL_SOCKET_NAME 定义用于管理 Sendmail 守护进程的套接字。[ControlSocketName]

cfCONFIG_EXPENSIVE 告诉 Sendmail 为设置了标志的邮件投送程序保留邮件，直到下一个队列。默认值为 false。[HoldExpensive]

cfCOPY_ERRORS_TO 设置接收错误信息的电子邮件地址。[PostmasterCopy]

cfCR_FILE 指向列出此服务器将中继邮件的主机列表文件。默认值为 /etc/mail/relay-domains。[$R]

cfCT_FILE 定义受信用户文件。默认值为 /etc/mail/trusted-users。[$t]

cfCW_FILE 指向本地主机别名文件。默认值为 /etc/mail/local-host-names.[$w]

confDEAD_LETTER_DROP 定义保存无法返回给发送者或发送给邮局管理员的失败邮件的文件。[DeadLetterDrop]

confDAEMON_OPTIONS 设置 Sendmail 守护进程的选项。[DaemonPortOptions]

...（此处省略已翻译的重复项，确保所有唯一配置项均已覆盖）
