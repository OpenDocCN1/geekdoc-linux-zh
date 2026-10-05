

# 表 C.1 单字符名称保留变量（续）

| 变量 | 存储的内容 |
| --- | --- |
| m | 本地域的名称。 |
| M | 用于伪装出站邮件的名称。 |
| n | 用于错误消息的发送者名称。 |
| p | 作为邮件投递代理运行的 Sendmail 进程的 PID。 |
| r | 接收消息时使用的协议。 |
| R | LOCAL_RELAY 的名称。 |
| s | 发送者机器的主机名。 |
| S | SMART_HOST 中继的名称。 |
| t | 当前日期的数值表示。 |
| u | 接收者的用户名。 |
| U | 覆盖 `k` 变量值的本地 UUCP 名称。 |
| v | 正在运行的 Sendmail 版本号。 |
| V | 类 V 主机的 UUCP 中继的名称。 |
| w | 本地系统的主机名。 |
| W | 类 W 主机的 UUCP 中继的名称。 |
| x | 递送者的全名。 |
| X | 类 X 主机的 UUCP 中继的名称。 |
| Y 所有其他主机的 UUCP 中继的名称。 |
| z | 接收者的主目录。 |
| Z | 版本号。 |
| - | 由 ident 验证的发送者地址。 |

## 414 附录 C Sendmail 变量、选项和标志

当前版本的 Sendmail 变量具有多字符名称。表 C.2 列出了使用长名称的变量。

## 表 C.2 长名称保留变量

| 变量 | 存储的内容 |
| --- | --- |
| {auth_auth} | 经过验证的用户身份。 |
| {auth_author} | 授权用户的身份。 |
| {auth_ssf} | AUTH 使用的加密密钥的位数。 |
| {auth_type} | 使用的认证机制类型。 |
| {bodytype} | 来自 ESMTP BODY 参数的值。 |
| {cert_issuer} | 证书颁发机构的区分名。 |
| {cert_subject} | 证书的区分名。 |
| {cipher_bits} | 用于连接的加密密钥长度。 |
| {cipher} | 用于连接的加密技术。 |
| {client_addr} | 连接到 TCP 端口 25 的远程客户端的 IP 地址。 |
| {client_name} | 连接到 TCP 端口 25 的客户端的标准名称。 |
| {client_port} | 远程客户端使用的源端口。 |
| {client_resolve} | 关键字 OK、FAIL、FORGED 或 TEMP，表示使用客户端 IP 进行反向 DNS 查找的结果。 |
| {currHeader} | 头部处理期间当前头部的内容。 |
| {daemon_addr} | 守护进程接受邮件的网络接口的 IP 地址。通常为 0.0.0.0 表示所有接口。 |
| {daemon_family} | 正在使用的协议族。通常为 inet 表示 TCP/IP。其他值为 inet6、so_，和 ns。 |
| {daemon_flags} | 由 DaemonPortOption 命令设置的标志（如果有）。 |
| {daemon_info} | 关于守护进程的一般信息。 |

## 表 C.2 长名称保留变量（续）

| 变量 | 存储的内容 |
|---|---|
| {daemon_name} | 守护进程名称，除非由 DaemonPortOptions 命令定义了名称，否则通常为 Daemon1。 |
| {daemon_port} | 守护进程监听的端口，通常为 25。 |
| {deliveryMode} | 当前的投递模式。 |
| {envid} | 来自 Mail From: 头部的 DSN ENVID 值。 |
| {hdrlen} | 存储在 `(currHeader)` 中的字符串长度。 |
| {hdr_name} | 头部处理期间当前头部的名称。 |
| {if_addr} | 当前传入连接使用的网络接口的 IP 地址。 |
| {if_name} | 分配给当前传入连接的网络接口的主机名。 |
| {mail_addr} | 来自 MAIL From: 信封头部创建投递三元组的用户邮件地址。 |
| {mail_host} | 来自 MAIL From: 信封头部创建投递三元组的主机名。 |
| {mail_mailer} | 来自 MAIL From: 信封头部创建投递三元组的投递器。 |
| {MessageIdCheck} | 来自传入 Message-id: 头部的值。 |
| {ntries} | 投递尝试次数。 |
| {opMode} | 来自 sendmail 命令行的运行模式。 |
| {queue_interval} | 由 `-q` 命令行选项定义的队列运行之间的时间。 |
| {rcpt_addr} | 来自 RCPT To: 信封头部创建投递三元组的用户邮件地址。 |

## 416 C Sendmail 变量、选项和标志

表 C.2 长名称保留变量（续）

| 变量 | 存储的内容 |
| {rcpt_host} | 来自 RCPT To: 信封头部创建投递三元组的主机名。 |
| {rcpt_mailer} | 来自 RCPT To: 信封头部创建投递三元组的投递器。 |
| {server_addr} | 远程服务器的 IP 地址。 |
| {server_name} | 用于连接的远程服务器名称。 |
| {tls_version} | 连接使用的 TLS 版本。 |
| {verify} | 验证结果。 |

## 类变量

上一节中的变量只能包含单个值。持有多个值的变量被称为“类”（classes）。表 C.3 列出了所有的类。

## 表 C.3 Sendmail 变量

| 类 | 存储的值 |
|---|---|
| B | 被处理的域。 |
| e | MIME 类型。初始化为 rfc822。 |
| E | 用户名。 |
| G | 应该被掩码的域。 |
| k | 用户列表。 |
| L | 本系统的域。 |
| m | 此处的主机名。 |

## 表 C.3 类变量（续）

| 类 | 存储的值 |
|---|---|
| M | 应该被掩码的域。 |
| n | MIME 子类型。初始化为 multipart/signed。 |
| N | 主机名。 |
| O | 不可使用的字符。 |
| P | 伪域。 |
| R | 应该被中继的域。 |
| s | MIME 类型。 |
| t | 用户。 |
| U | UUCP 主机。 |
| V | 本系统的 UUCP 主机。 |
| w | 主机名。 |
| W | 本系统的 UUCP 主机。 |
| X | 本系统的 UUCP 主机。 |
| Y | 主机名。 |
| Z | 域。 |
| . | 字面点。 |
| [ | 字面括号。 |
| {LDAPRoute} | 基于 LDAP 路由的域。 |
| {VirthHost} | 主机。 |

## 选项

大量的 Sendmail 选项设置在 `sendmail.cf` 文件中第 7 节描述了 `sendmail.cf` 的 Options 部分并提供了若干选项示例。完整的选项列表所示：

- AliasFile=[type:]path 指定别名文件的位置。
- AuthMechanisms=list 列出支持的认证机制。
- AuthOptions 列出 SMTP auth 命令支持的选项。
- AllowBogusHELO 允许 Sendmail 接受不包含主机名的非法 HELO SMTP 命令。
- AutoRebuildAliases 导致 Sendmail 在需要时自动重建别名数据库。
- BlankSub=c 使用 c 作为空白替换字符来替换地址中未引号的空格。
- CACERTFile=filename 指定包含颁发机构证书的文件。
- CACERTPath=path 定义指向包含各种证书颁发机构证书的目录路径。
- CheckAliases 告诉 Sendmail 在重建别名数据库时检查每个别名的投递地址是否有效。
- CheckpointInterval=n 导致 Sendmail 在处理完 n 个项目后对队列进行检查点。
- ClassFactor=factor factor 是 Priority 中值更高的消息的倍数。
- AliasWait=timeout 定义 Sendmail 在启动期间等待 @: 条目在别名数据库中出现的时间。

