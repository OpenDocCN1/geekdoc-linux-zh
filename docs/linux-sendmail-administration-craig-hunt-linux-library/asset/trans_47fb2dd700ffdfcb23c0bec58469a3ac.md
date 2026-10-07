

ControlSocketName=path 定义用于管理守护进程连接的 Unix 控制接字路径。默认情况下未定义定义。

DaemonPortOptions=options 设置 SMTP 服务器选项。options 关键字为 key=value 键值对。这些选项有：

- Name=type，其中 type 是守护进程的类型。type 可以是 MTA 或 MSA。
- Port=portnumber，其中 portnumber 是任何有效端口号。通过端口或 /etc/services 中找到名称进行指定。MTA 的默认端口为 25，MSA 的默认端口为 587。
- Addr=mask，其中 mask 是点十进制表示法或网络名称指定的 IP 地址掩码。默认是 INADDR_ANY，接受所有地址。
- Family=addressfamily，其中 addressfamily 是有效的地址族。默认是 IN，允许使用 IP 地址。
- Listen=n，其中 n 是允许的队列连接数。默认值是 10。
- SndBufSize=n，其中 n 是发送缓冲区大小。
- RcvBufSize=n，其中 n 是接收缓冲区大小。
- DataFileBufferSize=bytes 定义用于缓冲数据文件的最大内存量。
- DeadLetterFile=file 定义存储无法返回给发送者或邮主账户消息的文件。
- DefaultAuthInfo=file 定义包含导出连接所需的认证信息的文件。
- Charset=charset 定义位于 MIME Content-Type 头部中的字符集，其中八位数据被转换为七位格式。默认是 unknown-utf8。此选项会被邮件描述符的 Charset 字段覆盖。
- DefaultUser=user[:group] 为默认设置中没有 S 标志的邮件发送程序设置用户 ID 和组 ID。如果省略 group，则使用 /etc/passwd 文件中与用户关联组。默认是 1:1。
- DeliveryMode=mode 以指定的交付模式启动 Sendmail。模式可以是交互式、后台、队列或延迟的。默认是后台。Sendmail 可以在运行期间更改模式。
- DHParameters=parameters 定义 Sendmail 在 DSA/DH 加密时使用的 DH 参数。
- DialDelay=delay，其中 delay 是 Sendmail 在按需网络上重试失败连接之前等待的秒数。默认是 0（不重试）。
DontBlameSendmail=options 禁用 Sendmail 的安全性检查。禁用安全性通常是一个坏主意，因此此选项应在绝对必要时使用。表 C.4 列出了逗号分隔的关键字以及每个对安全性的影响。

表 C.4 DontBlameSendmail 选项的可能设置

| 关键字 | Sendmail 含义 |
| --- | --- |
| AssumeSafeChown | 所选命令是安全的，因为它仅对 root 用户可用。 |
| ClassFileInsafeDirPath | 接受类文件的所在的目录路径 |
| DontWarnForwardFileInsafeDirPath | 不对 .forward 文件的路径发出警告 |
| ErrorHeaderInsafeDirPath | 接受不安全目录下的错误头文件 |
| FileDeliveryToHardLink | 允许交付到硬链接文件 |
| FileDeliveryToSymLink | 允许交付到符号链接文件 |
| ForwardFileInsafeDirPath | 即使在不安全目录中也接受 .forward 文件 |
| ForwardFileInsafeDirPathSafe | 即使在不安全目录中也接受来自 .forward 文件的引用 |
| ForwardIngroupWritableDirPath | 即使在组可写目录中也接受 .forward 文件 |

附录 C Sendmail 变量、选项和标志

**表 C.4** DontBlameSendmail 选项的可能设置（续）

| 关键字 | Sendmail 含义 |
| --- | --- |
| GroupWritableAliasFile | 即使是组可写的也接受别名文件 |
| GroupWritableDirPathSafe | 接受所有组可写目录为“安全的”。 |
| GroupWritableForwardFileSafe | 即使是组可写的也接受 .forward 文件 |
| GroupWritableIncludeFileSafe | 即使是组可写的也接受 :include: 文件 |
| HelpFileInUnsafeDirPath | 即使在不安全目录中也接受帮助文件 |
| IncludeFileInsafeDirPath | 接受来自不安全目录的 :include: 文件 |
| IncludeFileInsafeDirPathSafe | 即使在不安全目录中也接受来自 :include: 文件的程序引用 |
| IncludeFileIngroupWritableDirPath | 即使在组可写目录中也接受 :include: 文件 |
| InsufficientEntropy | 如果 SSL 的随机生成器不足，则使用 STARTTLS |
| LinkedAliasFileInWritableDir | 即使是可写目录中的链接也接受别名文件 |
| LinkedClassFileInWritableDir | 从可写目录中的链接文件中加载类值 |
| LinkedForwardFileInWritableDir | 即使是可写目录中的链接也接受 .forward 文件 |

表 C.4 DontBlameSendmail 选项的可能设置（续）

| 关键字 | Sendmail 含义 |
| --- | --- |
| LinkedIncludeFileInWritableDir | 接受可写目录中的链接 :include 文件 |
| LinkedMapInWritableDir | 接受可写目录中的链接数据库文件 |
| LinkedServiceSwitchInWritableDir | 接受可写目录中的链接服务切换文件 |
| MapInsafeDirPath | 接受不安全目录中的数据库文件 |
| NonRootSafeAddr | 当 Sendmail 不以 root 身份运行时，不将文件和程序标记为不安全 |
| RunProgramInsafeDirPath | 运行可写目录中的程序 |
| RunWritableProgram | 运行组和所有人可写的程序 |
| Safe | 开启所有安全性检查。这是默认值。 |
| TrustStickyBit | 如果设置了粘滞位，则信任组和所有人 |
| WorldWritableAlias | 即使是所有人可写的也接受别名文件 |
| WriteMapToHardLink | 即使是硬链接也写入数据库文件 |
| WriteMapToSymLink | 写入符号链接 |

附录 Sendmail 变量、选项和标志

表 C.4 DontBlameSendmail 选项的可能设置（续）

| 关键字 | Sendmail 含义 |
| --- | --- |
| WriteStatsToHardLink | 如果是真正的硬链接，则写入状态文件 |
| WriteStatsToSym | 如果是符号链接，则写入状态文件 |

DontExpandCnames 禁用别名到规范名称的转换。
DontInitGroups 将用户的邮件交付代理路由限制为使用 /etc/passwd 文件与该用户相关的组。这用于减轻 NIS 服务器的负载。
DontProbeInterfaces 如果为 true，则停止 Sendmail 将网络接口的名称和地址添加到 w 中。默认是 false，因此接口和地址存储在 w 中。

DontPruneRoutes 防止 Sendmail 优化显式邮件路由。通常，Sendmail 会使路由尽可能直接。然而，对于位于防火墙后的系统，优化路由可能并不合适。

DoubleBounce=address 告诉 Sendmail 向哪里发送发送错误消息时发生错误的报告。address 的默认是 postmaster。

EightBitMode=action 指定如何处理未声明的八位数据。可能的操作有：s–严格，拒绝未声明的八位数据；m–mime，将数据转换为 MIME 格式；以及 p—原封不动地发送数据。

ErrorHeader=file-or-message 指定附加在输出错误消息前面的文件或消息。如果 file-or-message 是文件路径，它必须以斜线开头。如果未定义此选项，则不在错误消息前添加任何内容。

ErrorMode=action 告诉 Sendmail 如何处理错误消息。如果未定义此选项，则打印错误消息。有效的操作有：

- *打印错误消息*。
- 返回错误状态但不发送错误消息。
- 将错误消息邮件回传给发送者。
- 将错误消息写入用户的终端。
- 将错误消息回传给发送者，但始终给出零退出状态。

