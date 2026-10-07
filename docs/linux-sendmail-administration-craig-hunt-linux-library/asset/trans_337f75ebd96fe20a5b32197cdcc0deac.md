

# 表 C.2 长名称预留变量（续）

| 变量 | 存储的内容 |
| --- | --- |
| (daemon_name) | 守护进程名称，除非通过 DaemonPortOptions 命令定义了守护进程名称，否则为 Daemon1。 |
| (daemon_port) | 守护进程监听的端口，通常为 25。 |
| (deliveryMode) | 当前的交付模式。 |
| (envid) | 来自 Mail From: 头的 DSN ENVID 值。 |
| (hdrlen) | 存储在 {currHeader} 中的字符串长度。 |
| (hdr_name) | 头部处理期间当前的头部名称。 |
| (if_addr) | 当前传入连接使用的网络接口的 IP 地址。 |
| (if_name) | 分配给当前传入连接使用的网络接口的主机名。 |
| (mail_addr) | 来自 MAIL From: 信头创建的邮件交付三元组的用户邮件地址。 |
| (mail_host) | 来自 MAIL From: 信头创建的邮件交付三元组的主机名。 |
| (mail_mailer) | 来自 MAIL From: 信头创建的邮件交付三元组的邮件传输代理名称。 |
| (MessageIdCheck) | 来自传入的 Message-Id: 头的值。 |
| (ntries) | 尝试次数。 |
| (opMode) | 来自 sendmail 命令行的运行模式。 |
| (queue_interval) | 由 -q 命令行选项定义的队列运行间隔时间。 |
| (rcpt_addr) | 来自 RCPT To: 信头创建的邮件交付三元组的用户邮件地址。 |
| (rcpt_host) | 来自 RCPT To: 信头创建的邮件交付三元组的主机名。 |
| (rcpt_mailer) | 来自 RCPT To: 信头创建的邮件交付三元组的邮件传输代理名称。 |
| (server_addr) | 发出连接的远程服务器的 IP 地址。 |
| (server_name) | 发出连接的远程服务器名称。 |
| (tls_version) | 用于连接的 TLS/SSL 版本。 |
| (verify) | 验证过程的结果。 |

## 类变量

上一节涵盖的变量只能存储单个值。存储多个值的变量称为类。表 C.3 列出了所有类变量。

## 表 C.3 Sendmail 类变量

| 类 | 存储的值 |
| --- | --- |
| B | bestmx-is-local 进程中包含的域名。 |
| e | 支持的 MIME 内容传输编码。初始化为 7bit、8bit 和 binary。 |
| E | 不应被伪装的用户名。 |
| G | 应该在 generics（通用表）中查找的域名。 |
| k | 本系统的 UUCP 名称列表。 |
| L | 不被转发到 MAIL_HUB 或 LOCAL_RELAY 的本地用户。 |
| m | 此主机的本地域名。 |

## 表 C.3 Sendmail 类变量（续）

| 类 | 存储的值 |
| --- | --- |
| M | 应该被伪装的域名。 |
| n | 永远不应被 8bit 或 7bit 编码的 MIME 体类型。初始化为 multipart/signed。 |
| N | 不应被伪装的主机和域名。 |
| O | 不能在本地用户名中使用的字符。 |
| P | 伪域名，例如 REDIRECT。 |
| R | 本系统将转发邮件的域名。 |
| s | 可以递归处理的 MIME 消息子类型。初始化为 rfc822。 |
| t | 受信用户列表。 |
| U | 本地连接的 UUCP 主机。 |
| V | 通过 $V 定义的中继到达的 UUCP 主机。 |
| w | 本系统的主机名别名。 |
| W | 通过 $W 定义的中继到达的 UUCP 主机。 |
| X | 通过 $X 定义的中继到达的 UUCP 主机。 |
| Y | 直接连接的“智能”UUCP 主机。 |
| Z | 使用域名的直接连接的 UUCP 主机。 |
| . | 字面点（.）。 |
| [ | 字面左括号（[）。 |
| {LDAPRoute} | 可以根据 LDAP 查找路由的域名列表。 |
| {VirtHost} | 有效虚拟主机名的主机和域名列表。 |

## 选项

大量的 Sendmail 选项设置在 sendmail.cf 文件中。第 7 章描述了 sendmail.cf 文件的 Options 部分，并提供了若干选项示例。完整的选项列表所示。

- AliasFile=[type]:path, [type]:path... 指定别名文件的位置。type 是别名文件的路径。type 是别名数据库类型。有效的类型有 implicit（隐式）、hash（哈希）、dbm、stab（内部符号表）或 nis。所选数据库类型必须编译到系统中的 Sendmail 中。type 默认为 implicit。
- AliasWait=timeout 定义了 sendmail 在启动期间等待别名数据库中出现 @:entry 的时间。@:entry 标志着别名数据库的结束。
- AuthMechanisms=list 列出支持的认证机制。
- ClientOptions=options 定义 Sendmail 作为客户端使用的非标准设置。options 是由逗号分隔的 keyword=value 对列表。
- Addr=address 定义客户端使用的网络接口地址。address 可以是点进制地址或主机名。默认使用任何可用接口。
- Family=protocol 定义连接使用的协议族。inet，即 TCP/IP 。
- ColonOKn 告诉 sendmail 接受邮件地址中的冒号。用于路由结构（nodename:user）或 RFC 822 组结构（groupname:member1, member2, ...）。
- ConnectionCacheSize=n 是 sendmail 可以缓存的连接数。默认为二。零会在发送数据后立即关闭连接，这是 sendmail 的传统方式。
- ConnectionCacheTimeout=timeout timeout 是空闲连接保持的时间。在超时 分钟后将其关闭。默认为五分钟。
- ConnectionRateThrottle=n 限制每秒接受的传入连接数。默认为零，表示无限制。
- CheckpointInterval=n 使 sendmail 在处理 n 个项目后进行队列检查点。默认为 10。
- ClassFactor=factor 用于有利于头部信息的倍数。默认为 1800。
- ClientCertFile=file 指定包含客户端使用的证书的文件。
- ClientKeyFile=file 指定包含客户端使用的私钥的文件。
- Port=port 定义客户端用于发出连接的源端口。port 可以通过数字或名称指定。如果使用名称，则在 /etc/services 中定义。默认情况下连接的源端口由系统生成。
- BlankSub=c 使用空白替换字符。
- CERTPath=path 定义包含证书的目录路径。
- CERTificate=filename 指定包含证书授权机构的文件。
- SndBufSize=size 定义发送缓冲区的大小。
- RcvBufSize=bytes 定义接收缓冲区的大小。
- Modifier=flags 定义客户端的守护进程标志。只有一个可用的标志是 h。h 标志告诉客户端在 SMTP HELO 或 EHLO 命令中使用分配给接口的名称。
- ConnectOnlyTo=address 仅用于测试，因为它将所有 SMTP 连接限制到单个目标地址。
- AutoRebuild 告诉 sendmail 在需要时自动重建数据库。
- AliasAliases 添加此检查会减慢数据库。

