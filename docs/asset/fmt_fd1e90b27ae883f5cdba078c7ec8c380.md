
## 描述

Postfix SMTP+LMTP 客户端实现了 SMTP 和 LMTP 邮件投递协议。它处理来自队列管理器的消息投递请求。每个请求都指定了队列文件、发送者地址、投递的域名或主机以及接收者信息。该程序期望从 `master(8)` 进程运行。

SMTP+LMTP 客户端会更新队列文件并将接收者标记为已完成，或者通知队列管理器稍后重试投递。投递状态报告将根据情况发送到 `bounce(8)`、`defer(8)` 或 `trace(8)` 守护进程。

SMTP+LMTP 客户端会查找目标主机的邮件交换地址列表，按优先级排序，并连接到列出的每个地址，直到找到有响应的服务器为止。

当服务器不可用或由于可恢复错误状况导致邮件投递失败时，SMTP+LMTP 客户端将尝试将邮件投递到备用主机。

在邮件事务成功后，连接可能会保存到 `scache(8)` 连接缓存服务器，以便任何 SMTP+LMTP 客户端在后续事务中使用它。

默认情况下，对于活动队列中存在大量邮件的目的，会临时启用连接缓存。可以为特定目的永久启用连接缓存。

# SMTP 目的语法

SMTP 目的具有以下形式：

`domainname`
`domainname:port`

查找指定域名的邮件更改器，并连接到指定的端口（默认：`smtp`）。
`[hostname]`
`[hostname]:port`

查找指定主机的地址（地址），并连接到指定的端口（默认：`smtp`）。
`[address]`
`[address]:port`

连接到指定地址的主机，并连接到指定的端口（默认：`smtp`）。IPv6 地址必须格式化为 `[ipv6:address]`。

# LMTP 目的语法

LMTP 目的具有以下形式：

`unix:pathname`
连接到绑定到指定路径的本地 UNIX 域服务器。如果进程在 chroot 环境下运行，则绝对路径将相对于 Postfix 队列目录进行解释。

`inet:hostname`

`inet:hostname:port`

`inet:[address]`

`inet:[address]:port`

连接到指定本地或远程主机上的指定端口。如果没有指定端口，则连接到 `services(4)` 中定义为 `lmtp` 的端口。如果未找到此类服务，将使用 `lmtp_tcp_port` 配置参数（默认值为 24）。IPv6 地址必须格式化为 `[ipv6:address]`。

# 安全

SMTP+LMTP 客户端对安全具有中等敏感。它与网络上的 SMTP 或 LMTP 服务器以及 DNS 服务器通信。SMTP+LMTP 客户端可以在固定的低权限下以 chroot 运行。

# 标准

`RFC 821` (SMTP 协议) `RFC 822` (ARPA 互联网文本消息) `RFC 1651` (SMTP 服务扩展) `RFC 1652` (8bit-MIME 传输) `RFC 1870` (消息大小声明) `RFC 2033` (LMTP 协议) `RFC 2034` (SMTP 增强错误代码) `RFC 2045` (MIME: 互联网消息体格式) `RFC 2046` (MIME: 媒体类型) `RFC 2554` (AUTH) `RFC 2821` (SMTP 协议) `RFC 2920` (SMTP 管道化) `RFC 3207` (STARTTLS) `RFC 3461` (DSN) `RFC 3463` (增强状态码) `RFC 4954` (AUTH) `RFC 5321` (SMTP 协议)

# 诊断

问题和事务被记录到 `syslog(8)`。

根据 `notify_classes` 的设置，管理员将收到退信（bounces）的通知。

# 缺陷

SMTP+LMTP 连接缓存与 TLS 不兼容。

SMTP+LMTP 连接缓存假设 SASL 凭据有效。

# 配置参数

在 Postfix 2.3 版本之前，`smtp_xxx` 参数在 SMTP 中具有部分可用功能。

本文仅描述不简单的与 LMTP 相关的参数。

下文仅提供摘要。示例请参阅 `postconf(5)`。

# 兼容性控制

`ignore_mx_lookup_error` (no)
忽略没有响应的 DNS 查询。

`smtp_always_send_ehlo` (yes)
在 SMTP 会话开始始终发送 EHLO。

`smtp_never_send_ehlo` (no)
在 SMTP 会话开始从不发送 EHLO。

`smtp_defer_if_no_mx_address` (no)
当 MX 记录解析为 IP 地址时延迟投递。

`smtp_line_length_limit` (998)
Postfix 将的消息头部和正文最大长度。

`smtp_pix_workaround_delay_time` (10s)
Postfix 暂停的时间。

`smtp_pix_workaround_threshold` (500s)
在开启 smtp fixup 的防火墙之前，队列需要多长时间。

`smtp_pix_workarounds` (disable_delay_ctrl)
指定 CISCO 防火墙解决方案的列表。

`smtp_pix_workaround_maps` (empty)
按远程 SMTP 地址索引的查找表，包含针对特定目的 CISCO PIX 防火墙的解决方案。

`smtp_quote_rfc5321_envelope` (yes)
按照 RFC 5321 要求对 Postfix SMTP 客户端 MAIL FROM 和 RCPTO 命令中的地址加引号。

`smtp_reply_filter` (empty)
逐行转换远程 SMTP 服务器回复的机制。

`smtp_skip_5xx_greeting` (yes)
跳过以 5XX 状态码打招呼的 SMTP 服务器。

`smtp_skip_quit_response` (yes)
等待 Postfix QUIT 命令的响应。

适用于 Postfix 2.0 及更版本：

`smtp_skip_4xx_greeting` (yes)
跳过以 4XX 状态码打招呼的 SMTP 服务器。

适用于 Postfix 2.2 及更高版本：

`smtp_discard_ehlo_keyword_address_maps` (empty)
按远程 SMTP 服务器地址索引的查找表，包含 Postfix SMTP 客户端忽略的 EHLO 关键字（pipelining, strttls, auth 等）。

将忽略来自远程 SMTP 服务器的 EHLO 响应。

## `smtp_discard_ehlo_keywords` (空)

一个不区分大小写的 EHLO 关键字列表（pipelining, startles, auth 等），Postfix SMTP 客户端将从来自远程 SMTP 服务器的 EHLO 响应中忽略这些关键字。

## `smtp_generic_maps` (空)

一个可选的查找表，用于在 Postfix SMTP 客户端中执行地址重写，通常用于在跨 Internet 发送邮件时将本地有效地址转换为全局有效地址。

在 Postfix 2.2.9 及更高版本可用：

## `smtp_cname_overrides_servername` (取决于版本)

允许 DNS CNAME 记录覆盖 Postfix SMTP 客户端用于日志、SASL 密码查找、TLS 策略决策或 TLS 证书验证时使用的服务器名称（servername）。

在 Postfix 2.3 及更高版本中可用：

## `lmtp_discard_lhlo_keyword_address` (空)

以 LMTP 服务器地址为索引的查找表，其中包含不区分大小写的 LHLO 关键字列表（pipelining, startles, auth 等），Postfix LMTP 客户端将从来自远程 LMTP 服务器的 LHLO 响应中忽略这些关键字。

## `lmtp_discard_lhlo_keywords` (空)

一个不区分大小写的 LHLO 关键字列表（pipelining, startles, auth 等），Postfix LMTP 客户端将从来自远程 LMTP 服务器的 LHLO 响应中忽略这些关键字。

在 Postfix 2.4.4 及更高版本可用：

## `send_cyrus_sasl_authzid` (否)

当使用默认设置“no”向远程 SMTP 或 LMTP 服务器进行验证时，不发送 SASL 身份 ID (authzid)；仅发送 SASL 身份 ID (authcid) 以及客户端密码。

在 Postfix 2.5 及更高版本中可用：

## `smtp_header_checks` (空)

用于 Postfix SMTP 客户端的受限 `header_checks(5)` 表。

## `smtp_mime_header_checks` (空)

用于 Postfix SMTP 客户端的受限 `mime_header_checks(5)` 表。

## `smtp_nested_header_checks` (空)

用于 Postfix SMTP 客户端的受限 `nested_header_checks(5)` 表。

## `smtp_body_checks` (空)

用于 Postfix SMTP 客户端的受限 `body_checks(5)` 表。

在 Postfix 2.6 及更高版本可用：

## `tcp_windowsize` (0)

针对破坏 TCP 窗口缩放的路由器的可选变。

在 Postfix 2.8 及更高版本中可用：

## `smtp_dns_resolver_options` (空)

用于 Postfix SMTP 客户端的 DNS 解析器选项。
在 Postfix 2.9 及更高版本可用：

## `smtp_per_record_deadline` (否)

更改 `smtp_*timeout` 限制的行为，从每次读取或写入系统调用的时间限制更改为发送或接收完整记录（一个 SMTP 命令行、SMTP 响应行、SMTP 消息内容行或 TLS 协议消息）的时间限制。

## `smtp_send_dummy_mail_auth` (否)

是否在 SASL 验证的 SMTP 会话中向 MAIL FROM 命令中追加 "AUTH<=>" 选项。

# MIME 处理控制

在 Postfix 2.0 及更高版本可用：

`disable_mime_output_conversion` (否)
禁用 8BITIME 格式到 7BIT 格式的转换。

`mime_boundary_length_limit` (2048)
MIME 多部分边界字符串的最大长度。

`mime_nesting_limit` (100)
MIME 解析器处理的最大递归深度。

# 外部内容检查

在 Postfix 2.1 及更高版本可用：
`smtp_send_xforward_command` (否)

当 Postfix SMTP 服务器的 EHLO 响应宣布支持 XFORWARD 时，发送非标准的 XFORWARD 命令。

# SASL 验证控制

`smtp_sasl_auth_enable` (否)
在 Postfix SMTP 客户端中启用 SASL 验证。

`smtp_sasl_password_maps` (空)
可选的 Postfix SMTP 客户端查找表，每个远程主机名或域名对应一个用户名:密码 条目，或者在启用了发送者相关验证时对应一个发送者地址。

`smtp_sasl_security_options` (noplaintext, anonymous)
Postfix 客户端 SASL 安全选项；从 Postfix 2.3 开始，可用功能列表取决于通过 `smtp_sasl_type` 选择的 SASL 客户端实现。

在 Postfix 2.2 及更高版本可用：

`smtp_sasl_mechanism_filter` (空)
如果为空，则是一个 Postfix SMTP 客户端过滤器，用于过滤远程 SMTP 服务器提供的 SASL 机制列表。

在 Postfix 2.3 及更高版本中可用：

`smtp_sender_dependent_authentication` (否)
在 Postfix SMTP 客户端中启用发送者相关验证；这仅在使用 SASL 验证可用，并且会禁用 SMTP 连接缓存以确保来自不同发送者的邮件使用适当的凭据。

`smtp_sasl_path` (空)
Postfix SMTP 客户端传递给 SASL 插件实现的特定实现信息，该实现是通过通过 `smtp_sasl_type` 选择的。

`smtp_sasl_type` (cyrus)
Postfix SMTP 客户端用于验证时应使用的 SASL 插件。

在 Postfix 2.5 及更高版本中可用：

`smtp_sasl_cache_name` (空)
一个可选的表，用于防止与相同的远程 SMTP 主机名、用户名和密码重复发生 SASL 验证失败。

`smtp_sasl_cache_time` (90)
SASL 缓存的有效期。

`smtp_sasl_soft_bounce` (yes)
当远程 SMTP 服务器拒绝 SASL 验证时退回邮件。

在 Postfix 2.9 及更高版本可用：

`smtp_send_dummy_mail_auth` (否)
是否在 SASL 验证的 SMTP 会话中向 MAIL FROM 命令中追加 “AUTH<=>” 选项。

# STARTTLS 支持

关于 STARTTLS 的详细信息请参考 README。

`smtp_tls_security_level` (空)
Postfix SMTP 客户端使用的 TLS 安全级别；当指定为空时，将使用过时的 `smtp_tls`。

用于用于 TLS 加密 SMTP 会话的 Postfix 客户端 TLS 选项。

`smtp_tls_starttls_timeout` (300)
TLS 启动期间的时间限制。

`smtp_tls_ca` (空)
包含受信任 CA 的证书文件。

`smtp_tls_path` (空)
用于验证远程 SMTP 服务器的证书目录。

`smtp_tls_cert_file` (空)
Postfix SMTP 客户端使用的 PEM 格式证书。

`smtp_tls_mandatory_ciphers` (medium)
Postfix SMTP 客户端使用的强制 TLS 等。

`smtp_tls_exclude_ciphers` (空)
Postfix SMTP 客户端中排除的加密类型。

`smtp_tls_mandatory_exclude_ciphers` (空)
Postfix SMTP 客户端中排除的加密类型。

`smtp_tls_dcert_file` (empty)
Postfix SMTP 客户端使用的 DSA 证书。

`smtp_tls_dkey_file` (empty)
Postfix SMTP 客户端使用的 DSA 密钥。

`smtp_tls_key_file` (empty)
Postfix SMTP 客户端使用的 RSA 密钥。

`smtp_tls_loglevel` (empty)
启用额外的 TLS 日志。

`smtp_tls_note_starttls` (否)
记录启用 TLS 的远程 SMTP 服务器主机名。

`smtp_tls_policy_maps` (空)
带有目的地的 TLS 策略查找表；当指定不为空时，覆盖过时的 `smtp_tls_per_site`。

`smtp_tls_mandatory_protocols` (!SSLv2)
Postfix SMTP 客户端使用的强制 SSL/TLS 协议列表。

`smtp_tls_scert_verifydepth` (9)
SMTP 证书验证深度。

`smtp_tls_secure_match` (nextthop, dot-nextthop)
Postfix SMTP 客户端在“secure”级别验证证书。

`smtp_tls_session_cache_database` (empty)
包含可选客户端缓存的文件名。

`tls_session_cache_timeout` (3600s)
客户端缓存的过期时间。

`smtp_tls_verify_match` (hostname)
Postfix SMTP 客户端在“verify”级别验证证书。

`tls_daemon_random_bytes`(32)
`smtp(8)` 或 `smtpd(8)`进程向 `tlsmgr(8)` 服务器请求的伪随机字节数，用于种子其内部随机数生成器 (PRNG)。

`tls_high_cipherlist` (ALL:EXPORT!MEDIUM:+RC4@STRENGTH)
“HIGH”级加密。

`tls_medium_cipherlist` (ALL:EXPORT:+RC4@STRENGTH)
“MEDIUM”级或更高级别的加密。

`tls_low_cipherlist` (ALL:EXPORT:+RC4@STRENGTH)
“LOW”级或更高级别的加密。

`tls_export_cipherlist` (ALL:EXPORT:+RC4@STRENGTH)
“EXPORT”级或更高级别的加密。

`tls_null_cipherlist` (eNULL!:aNULL)
提供身份验证但不加密的“NULL”级加密。

在 Postfix 2.4 及更高版本可用：

`smtp_sasl_tls_verified_security_options` ($smtp_sasl_security_options)
用于具有已验证服务器证书的 TLS 加密 SMTP 会话的 SASL 验证选项。

在 Postfix 2.5 及更高版本可用：

`smtp_tls_fingerprint_cert_match` (空)
“fingerprint”TLS 安全级别允许的远程服务器证书指纹列表 (`smtp_tls_security_level` = fingerprint)。

`smtp_tls_fingerprint_digest` (md5)
用于构建 SMTP 服务器证书指纹的消息摘要算法。

指纹。

在 Postfix 2.6 及更高版本可用：
`smt_tls_protocols` (!SSLv2)

- Postfix SMTP 客户端在使用机会性 TLS加密时将排除或包含的 TLS 协议列表。

`smtp_tls_ciphers` (export)
Postfix SMTP 客户端在使用机会性 TLS加密时使用的最小 TLS 密套等级。

`smtp_tls_eccert_file` (empty)
包含 PEM 格式的 Postfix SMTP 客户端 ECDSA 证书的文件。

`smtp_tls_eckey_file` (Smtp_tls_eccert_file)
包含 PEM 格式的 Postfix SMTP 客户端 ECDSA 私钥的文件。

在 Postfix 2.7 及更高版本可用：
`smt_tls_block_early_mail_reply` (no)

- 尝试基于 TLS 协议漏洞（CVE-2009-35555）检测邮件劫持攻击，攻击者会在 Postfix SMTP 客户端的 TLS 会话中插入恶意的 HELO、MAIL、RCPT、DATA 命令。

在 Postfix 2.8 及更高版本可用：
`tls_disable_workarounds` (参见 ‘postconf -d’ 输出)

- 要禁用的 OpenSSL 错误变通方案列表或位掩码。

# 过时的 STARTTLS 控制

以下配置参数是为了兼容 2.3 之前的 Postfix 版本而存在的。这些支持将在未来的发布中移除。

**`smtp_use_tls` (no)**
机会性模式：当远程 SMTP 服务器宣布支持 STARTTLS 时使用 TLS，否则以明文形式发送邮件。

**`smtp_enforce_tls` (no)**
强制模式：要求远程 SMTP 服务器使用 TLS 加密，且从不明文发送邮件。

**`smtp_tls_enforce_peername` (yes)**
在强制 TLS 加密的情况下，要求远程 SMTP 服务器的主机名与远程 SMTP 服务器证书中的信息匹配。

**`smtp_tls_per_site` (empty)**
可选的查找表，根据下一跳目的地和远程 SMTP 服务器主机名定义 Postfix SMTP 客户端 TLS 使用策略。

**`smtp_tls_cipherlist` (empty)**
过时的 Postfix < 2.3 控制，用于控制 Postfix SMTP 客户端的 TLS 密套列表。

# 资源和速率控制

`smtp_destination_concurrency_limit` ($default_destination_concurrency_limit)
通过 smtp 消息传递传输向目标进行并行投递的最大数量。

`smtp_destination_recipient_limit` ($default_destination_recipient_limit)
smtp 传递传输每条消息允许的最大接收者数量。

`smtp_connect_timeout` (30s)
Postfix SMTP 客户端完成 TCP 连接的时间限制，或为 0（使用操作系统的内置时间限制）。

`smtp_helo_timeout` (30s)
Postfix SMTP 客户端发送 HELO 或 EHLO 命令以及接收远程 SMTP 服务器初始响应的时间限制。

`lmptp_lhlo_timeout` (30s)
Postfix LMTP 客户端发送 LHLO 命令以及接收远程 LMTP 服务器初始响应的时间限制。

`smtp_xforward_timeout` (30s)
Postfix SMTP 客户端发送 XFORWARD 命令以及接收远程 SMTP 服务器响应的时间限制。

`smtp_mail_timeout` (30s)
Postfix SMTP 客户端发送 MAIL FROM 命令以及接收远程 SMTP 服务器响应的时间限制。

`smtp_rcpt_timeout` (30s)
Postfix SMTP 客户端发送 SMTP RCPT 命令以及接收远程 SMTP 服务器响应的时间限制。

`smtp_data_init_timeout` (120s)
Postfix SMTP 客户端发送 SMTP DATA 命令以及接收远程 SMTP 服务器响应的时间限制。

`smtp_data_xer_timeout` (180s)
Postfix SMTP 客户端发送 SMTP 邮件内容的时间限制。

`smtp_data_done_timeout` (600s)
Postfix SMTP 客户端发送 SMTP “.,,”以及接收远程 SMTP 服务器响应的时间限制。

`smtp_quit_timeout` (300s)
Postfix SMTP 客户端发送 QUIT 命令以及接收远程 SMTP 服务器响应的时间限制。

在 Postfix 2.1 及更高版本可用：

`smtp_mx_address_limit` (5)
Postfix SMTP 客户端查找邮件交换器后可能产生的 MX（邮件交换器）IP 地址的最大数量，或为 0（不限制）。

`smtp_mx_session_limit` (2)
Postfix 放弃之前的最大 SMTP 会话数。

`smtp_timeout` (20s)
Postfix SMTP 客户端发送 RSET 命令以及接收远程 SMTP 服务器响应的时间限制。

在 Postfix 2.2 及更高版本可用：
`ltmp_timeout` (empty)
Postfix 放弃之前的最大 LMTP 连接数。

`smtp_cache_on_demand` (yes)
临时启用 SMTP 缓存。

`smtp_time_limit` (300s)
Postfix 客户端保持开启的时间。

在 Postfix 2.3 及更高版本可用：
`smtp_connection_timeout` (5s)
SMTP 连接开启状态下的时间限制。

在 Postfix 2.7 及更高版本可用：
`smtp_tcp_port` (no)
SMTP 客户端连接的默认 TCP 端口。

在 Postfix 2.9 及更高版本可用：
`smtp_protocol_timeout` (30s)
Postfix SMTP 客户端建立或接收连接的时间限制。

# 故障排除控制

`debug_peer_level` (2)
当远程客户端或服务器匹配时，日志级别的增量。

`debug_peer_list` (empty)
导致调试日志级别增加的模式列表。

`error_notice` (postmaster)
邮件投递问题的通知接收者。

`internal_mail_filter` (empty)
哪些类邮件受内部过滤。

`notify_classes` (resource, software)
报告给 postmaster 的错误类别。

# 杂项控制

`best_mx_transport` (empty)
当 Postfix 检测到“返回自身”错误条件时，投递邮件的地方。

`config_directory` (参见 ‘postconf -d’ 输出)
main.cf 和 master.cf 配置文件的位置。

`daemon_timeout` (18000s)
Postfix 守护进程在处理请求时被守护计时器终止前允许的时间。

`delay_logging_resolution` (2)
记录秒级数值时，小数点后的最大位数。

`disable_dns_lookups` (no)
Postfix SMTP 和 LMTP 客户端中的 DNS 查找。

`inet_interfaces` (all)
该邮件系统接收的网络接口地址。

`inet_protocols` (all)
Postfix 在建立或接受连接时尝试使用的 Internet 协议。

`ipc_timeout` (3600s)
通过内部通道发送或接收信息的时间限制。

`ltmp_assume_final` (no)
当远程 LMTP 服务器不支持 DSN 时，假设执行最终投递，并将“已传递”状态通知为“已交付”。

`ltmp_tcp_port` (24)
SMTP客户端连接的默认 TCP 端口。

`max_idle` (100s)
空闲的 Postfix 守护进程在等待传入连接前被动终止前的最大等待时间。

`max_use` (100)
Postfix 守护进程在被动终止前服务的最大传入连接数。

`process_id` (read-only)
Postfix 命令或守护进程的进程标识符。

`process_name` (read-only)
Postfix 命令或守护进程的进程名称。

`proxy_interfaces` (empty)
通过代理或网络地址转换单元接收邮件的网络接口地址。

`smtp_address_preference` (any)
Postfix SMTP 客户端尝试的地址类型（“ipv6”、“ipv4”或“any”），

当一个目标同时具有 IPv6 和 IPv4 地址且 MX 偏好值相等时。

**`smtp_bind_address` (空)**

一个可选的数值地址，Postfix 客户端在建立 IPv4 连接时应绑定到该地址。

**`smtp_bind_address6` (空)**

一个可选的数值地址，Postfix 客户端在建立 IPv6 连接时应绑定到该地址。

**`smtp_helo_name` ($hostname)**

EHLO 或 HELO 命令中的主机名映射。

**`lmtp_lhlo_name` ($hostname)**

LMTP LHLO 命令中的主机名映射。

**`smtp_host_lookup` (dns)**

Postfix 客户端用于查找主机 IP 地址的机制。

**`smtp_randomize_addresses` (yes)**

随机化相同 MX 优先级的地址顺序。

**`syslog_facility` (mail)**

postconf -d 输出的 syslog 设施名。

**`syslog_name` (见‘postconf -d’)**

在 syslog 记录中附加的系统名称，例如“smtpd”变为“postfix/smtpd”。

**`fallback_relay` (空)**

对于找不到或无法访问的 SMTP 目标，可选的中继列表。适用于 Postfix 2.2 及早期版本。

**`smtp_fallback_relay` ($fallback_relay)**

对于找不到或无法访问的 SMTP 目标，可选的中继列表。适用于 Postfix 2.3 及更高版本。

## SEE ALSO

（见 postconf -d）

# README FILES

使用 `postconf readme_directory` 或 `postconf_directory` 查找此信息。

# LICENSE

Secure Mailer 许可随此软件分发。

# AUTHOR(S)

Wietse Venema IBM T. Watson Research Box 704 Yorktown Heights, NY 合作者：Jon Ribbons Oaktree Internet Solutions Ltd., Internet House, Canal Basin, Coventry, CV1LY, United Kingdom 最初支持：Till Franke SuSE Rhein/Main AG 65760 Eschborn, Germany 最初支持：Lutz Jaenicke Cottbus Allgemeine Elektrotechnik Universitaplatz-3-4 Cottbus, Germany 修订并支持：Victor Duchov Morgan Stanley

# LNSTAT

+ > NAME

instat - 统一 Linux 网络统计

## SYNOPSIS

instat [options]

## DESCRIPTION

本手册页简要介绍了 instat 命令。
**Instat** 是旧 rtstat 程序的通用且功能更完整的替代品。除了路由缓存统计，它还支持 Linux 内核通过 /proc/net/stat/ 提供的任何统计信息。

## OPTIONS

instat 支持以下选项：

- -h, --help 显示选项摘要。
- -V, --version 显示程序版本。
- -c, --count 打印 <count> 个间隔。
- -d, --dump 转储可用文件/键。
- -f, --file <file> 使用的统计文件。
- -i, --interval <intv> 将间隔设置为 ‘intv’ 秒。
- -k, --keys k,k,k... 仅指定的键。
- -s, --subject [0-2] 指定标题显示。“0’表示无标题，“1’在程序启动时打印标题，“2’每隔 20 行打印一次标题。
- -w, --width n,n,n… 每个字段的宽度。

# USAGE EXAMPLES

# instat -d 获取支持的统计文件列表。

# instat -k arp_cache:entries,rt_cache:in_hit,arp_cache:destroys 选择的文件和键。

# instat -i 10 使用 10 秒的间隔。

# instat -f ip_conrack 仅对指定文件进行统计。

# instat -s 0 完全不打印标题。

# instat -s 20 在启动时和每 20 行打印一次标题。

# instat -c -1 -i 1 -f rt_cache -k entries,in_hit,in_slow_tot 每秒显示字段 rt_cache 的键 entries、in_hit 和 in_slow_tot 的统计信息。

## SEE ALSO

ip(8)， 以及 /usr/share/doc/iproute-3.10.0/README.lnstat（Debian 中的 iproute-doc 包）

## AUTHOR

Instat 由 Harald Welte <laforge@gnumonks.org> 编写。

本手册页由 Michael Prokop <mika@grml.org> 为 Debian 项目编写（也可供使用）。

# LOAD_POLICY

+ > NAME

load_policy - 将新的 SELinux 策略加载到内核

## SYNOPSIS
```
