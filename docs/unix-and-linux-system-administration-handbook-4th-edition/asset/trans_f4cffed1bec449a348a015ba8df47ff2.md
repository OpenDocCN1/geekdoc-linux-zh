

## 表 20.11 基本 sendmail 配置选项

|  | 选项名称 | 描述（默认值） |
|---|---|---|
| 资源 | MAX_DAEMON_CHILDREN | 最大子进程数*（无限制） |
|  | MAX_MESSAGE_SIZE | 单条消息的最大字节数（无限） |
|  | MIN_FREE_BLOCKS | 接受邮件所需的最小文件系统空间（100） |
|  | TO_lots_of_stuff | 各种事物的超时设置（多种） |
|  | DELAY_LA | 减慢投递的负载平均值（0 = 无限制） |
|  | FALLBACK_MX | 参见第 803 页说明（无默认值） |
|  | FAST_SPLIT | 在收件人排序并在队列间拆分时抑制 MX 查找（1 = true） |
| 性能 | HOST_STATUS_DIRECTORY | 参见第 803 页说明（无默认值） |
|  | MCI_CACHE_SIZE | 缓存的开放外发 TCP 连接数（2） |
|  | MCI_CACHE_TIMEOUT | 保持缓存连接开放的时间（5m） |
|  | MIN_QUEUE_AGE | 作业必须在队列中停留的最短时间；使繁忙机器更好地处理队列（0） |
|  | QUEUE_LA | 应将邮件排队而不是立即投递的负载平均值（8 * #CPUs） |
|  | REFUSE_LA | 拒绝邮件的负载平均值（12 * #CPUs） |
| 安全和垃圾邮件 | AUTH_MECHANISMS | 用于 Cyrus SASLᵇ 的 SMTP 认证机制 |
|  | CONNECTION_RATE_THROTTLE | 通过限制接受邮件连接的速率来减缓 DOS 攻击（无限制） |
|  | DONT_BLAME_SENDMAIL | 覆盖 sendmail 的安全和文件检查；不要随意更改！（安全） |
|  | MAX_MIME_HEADER_LENGTH | 设置 MIME 头的最大大小（无限制）ᶜ |
|  | MAX_RCPTS_PER_MESSAGE | 减缓垃圾邮件投递；推迟额外收件人并发送临时错误消息（无限） |
|  | PRIVACY_FLAGS | 限制 SMTP 提供的信息（authwarnings） |
| 杂项 | DOUBLE_BOUNCE_ADDRESS | 捕获大量垃圾邮件；某些站点使用 /dev/null，但这可能会隐藏严重问题（postmaster） |
|  | LDAP_DEFAULT_SPEC | LDAP 数据库的映射规范，包括服务器运行的主机和端口（未定义） |

a. 更具体地说，同时可以运行的最大子进程数。当达到限制时，sendmail 拒绝连接。此选项可以防止（或制造）拒绝服务攻击。
b. 默认值为 EXTERNAL GSSAPI KERBEROS V4 DIGEST-MD5 CRAM-MD5；不要添加 PLAIN LOGIN，因为密码会以明文传输。这在内部可能可以接受，但在互联网上除非连接也通过 SSL 或 TLS 保护，否则不行。
c. 此选项可以防止用户代理缓冲区溢出。256/128* 是一个不错的值——意味着每个头 256 字节，每个参数 128 字节。

将这些与诸如灰名单（第 764 页）、使用 amavisd-new 进行内容扫描（第 769 页）以及用于电子邮件认证的新 DNS 记录（第 767 页）等技术结合起来，你或许就能与垃圾邮件发送者抗衡。

## 中继控制

sendmail 接受传入邮件，查看信封地址，决定邮件应去往何处，然后将其传递给适当的投递目的地。该目的地可以是本地的，也可以是投递链中更远的另一个传输代理。当传入消息没有本地收件人时，处理它的传输代理就被称为充当中继。

只有在访问数据库（参见第 785 页）中标记为 RELAY 的主机，或列在 /etc/mail/relay-domains 中的主机才允许提交邮件进行中继。某些类型的中继是有用且合法的。你如何区分应中继的消息和应拒绝的消息？中继实际上仅在三种情况下是必要的：

- 当传输代理充当无法通过其他方式访问的主机的网关时；例如，不总是开机（笔记本电脑、Windows PC）和虚拟主机。在这种情况下，所有你希望中继的收件人都位于同一域内。
- 当传输代理是其他不太智能主机的外发邮件服务器时。在这种情况下，所有发件人的主机名或 IP 地址都是本地的（或至少可枚举的）。
- 当你同意为另一个站点充当备份 MX 目的地时。

任何其他似乎需要中继的情况可能只是糟糕设计的迹象（支持移动用户的情况可能除外）。你可以通过指定一个集中服务器来接收邮件，并使用 POP 或 IMAP 进行客户端访问，从而避免上述第一种中继用途。第二种情况应始终允许，但仅限于你自己的主机。你可以检查 IP 地址或主机名。在第三种情况下，你可以将另一站点列入访问数据库，并仅允许该站点 IP 地址块的中继。

尽管 sendmail 默认情况下关闭了中继，但已添加了多个功能来重新打开中继，无论是完全打开还是有限且受控的方式。这些功能如下列出以供完整性考虑，但我们的建议是你在打开权限时要谨慎。access_db 功能是允许有限中继的最安全方式：

- FEATURE(`relay_entire_domain') – 仅允许为你的域中继
- RELAY_DOMAIN(`domain, ...') – 添加更多要中继的域
- RELAY_DOMAIN_FILE(`filename') – 同上；从文件获取域列表
- FEATURE(`relay_hosts_only') – 影响 RELAY_DOMAIN，accessdb

如果你使用 SMART_HOST 或 MAIL_HUB 指定将邮件路由通过特定邮件服务器机器，则需要做出例外。该服务器必须设置为从本地主机中继邮件。配置如下：

```
FEATURE(`relay_entire_domain')
```
