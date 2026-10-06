

## defer_transports

此项列出了需要延迟传输的传输协议。这将在本章节的“拨号服务器配置”中进行后续讨论。

## disable_dns_lookups

此项设置是否出于账户目的尝试将 IP 地址翻译为主机名。除非你的邮件服务器接收大量邮件，否则开启此项通常是一个好主意。

## relayhost

有时被称为 socalled，这是你将所有不属于 Postfix 服务器控制域范围的本地邮件转发到的机器。

## content_filter

内容过滤器子通常用于将你的邮件传递给病毒扫描器进行检查。内容过滤器定义了一个服务器和端口，你所有的邮件在重新插入 Postfix 工作流之前都会通过该服务器和端口进行处理。你定义的内容过滤器负责将你的邮件重新注入系统。

## mailbox_command

邮箱命令是用于将邮件投递到用户邮箱的程序。此的一个常见配置是 Cyrus deliver 程序，它将邮件消息注入用户的 IMAP 邮箱中。这将在本章节稍后讨论 Cyrus 时进行介绍。

## mailbox_transport

邮箱传输与 mailbox_command 非常相似。它不是使用特定程序来投递用户的邮件，而是使用一种可以在 `master.cf` 文件中用户定义的协议。它通常用于通过 LMTP（本地邮件传输协议）将邮件投递到 Cyrus IMAP 主机。在章节讨论 Cyrus 时，我们会简要提到 `master.cf`。

## smtpd_sender_restrictions

此项设置了客户端在连接 Postfix 服务器发送邮件时，其描述自身时的信息的限制。

## smtpd_client_restrictions

此项设置了通过 SMTP 连接到 Postfix 服务器的哪些限制条件。我们在本章节讨论垃圾邮件时会讨论这些设置。

## smtpd_helo_required

此项指定了是否可以使用 HELO 或 EHLO 命令启动 SMTP 连接。这应该在尝试限制非标准服务器发送邮件或通过你的服务器发送邮件时使用。如果你想对 HELO/EHLO 强制执行严格的规则，请也使用 `smtpd_helo_restrictions`。

## HELO AND EHLO

HELO 是握手的第一部分（之所以这样命名是因为这是我们礼貌地开始对话的方式）。当 SMTP 服务器接收来自客户端的 HELO 时，它会返回 SMTP 服务器自身的能力作为响应。随着 SMTP 的发展，增加了更多功能。为了向后兼容，HELO 命令响应的是 SMTP 服务器可以做什么的标准响应。如果 SMTP 客户端可以理解扩展 SMTP 命令，它可以使用 EHLO（扩展 HELO）开始对话。作为响应，SMTP 服务器会告诉客户端它拥有哪些额外功能。EHLO 的主要用途之一是启动安全套层 (SSL) SMTP 连接。

### smpd_helo_restrictions

如果设置了 HELO/EHLO 要求，你可以使用 HELO 限制来对连接机器的主机名执行严格检查。

### strict_rfc821_envelopes

如果你希望连接到 Postfix 的客户端严格使用 RFC 821 信封（完全限定并包含在括号内），则此选项将拒绝任何 `MAIL. FROM:` 和 `RCPT TO:` 非 RFC 地址。

> 设置此项可能是一个坏主意，因为有很多损坏的邮件服务器假设它们可以不带角括号运行，等等。

## smtpd_recipient_restrictions

此项处理 SMTP 传输（RCPT TO）中指定的接收者。你可以告诉 Postfix 检查接收者是否完全限定，或者接收者域名是否托管在 Postfix 安装主机上。

## smtpd_sasl_auth_enable

此项指定是否为连接的客户端启用 SMTP 认证。其本身允许用户对 Postfix 服务器进行认证，但你需要在 `smtpd_recipient_restrictions` 中添加 `permit_sasl_authenticated`，以便在用户成功认证后允许中继。你还需要正确设置 SASL（认证安全层）密码数据库以便进行查询。

### smtpd_use_tls

此项启用到 Postfix 服务器的传输安全层 (TLS) 加密连接。关于向你的邮件服务器提供加密链接的更多信息，请查看 www.aet.tu-de/personen/jaicke/postfix_tls/。

smtp_tls_use
此项启用 SMTP 请求。这将告诉 Postfix 创建 TLS 连接。要检查服务器是否接受 TLS 连接，请通过 Telnet 连接端口 25 <your_host>。如果服务器支持 TLS，它将向你返回扩展 HELO (EHLO) 响应。

alias_maps
别名的位置。这些可以存储在轻量级目录访问协议 (LDAP)、网络信息系统 (NIS) 或本地的别名文件中。

mailbox_size_limit
此项指定用户邮箱的最大大小。这仅适用于 mbox 格式。如果你使用 maildir 格式，它指的是单个文件的大小，而不是整体。

message_size_limit
此项指定进入或离开 Postfix 服务器的邮件的最大大小。

## Postfix Terminology and Use

我们讨论的配置选项代表了 Postfix 可以做的一部分。我们现在讨论它是如何工作的以及它为邮件管理员提供了什么。任何以 SMTP 开头的参数都控制入站 SMTP 连接。同样，任何以 SMTP 开头的参数都指向其他 SMTP 服务器连接。

## Configuring and Securing Your Relay Policy

Postfix 的中继策略（允许用户通过邮件服务器发送邮件）由 `mynetworks` 参数决定。`mynetworks` 参数告知哪些网络或特定主机被 Postfix 信任以便向任何目的地发送邮件。设置 `mynetworks` 参数后，你可以该变量显式告诉 Postfix 你信任的网络。图 17-1 显示了你的始终连接的企业邮件服务器的示例。你可以看到 `mynetworks` 参数的作用。默认情况下，`mynetworks` 参数包含你的本地网络 (127.0.0.0/8) 以及你在系统中配置的网络连接。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

**Figure 17-1:** 你的始终连接的企业邮件服务器的示例。你可以看到 `mynetworks` 参数的作用。默认情况下，`mynetworks` 参数包含你的本地网络 (127.0.0.0/8) 以及你在系统中配置的网络连接。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

**Figure 17-1:** 你的始终连接的企业邮件服务器的示例。你可以看到 `mynetworks` 参数的作用。默认情况下，`mynetworks` 参数包含你的本地网络 (127.0.0.0/8) 以及你在系统中配置的网络连接。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

**Figure 17-1:** 你的始终连接的企业邮件服务器的示例。你可以看到 `mynetworks` 参数的作用。默认情况下，`mynetworks` 参数包含你的本地网络 (127.0.0.0/8) 以及你在系统中配置的网络连接。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

**Figure 17-1:** 你的始终连接的企业邮件服务器的示例。你可以看到 `mynetworks` 参数的作用。默认情况下，`mynetworks` 参数包含你的本地网络 (127.0.0.0/8) 以及你在系统中配置的网络连接。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

**Figure 17-1:** 你的始终连接的企业邮件服务器的示例。你可以看到 `mynetworks` 参数的作用。默认情况下，`mynetworks` 参数包含你的本地网络 (127.0.0.0/8) 以及你在系统中配置的网络连接。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

**Figure 17-1:** 你的始终连接的企业邮件服务器的示例。你可以看到 `mynetworks` 参数的作用。默认情况下，`mynetworks` 参数包含你的本地网络 (127.0.0.0/8) 以及你在系统中配置的网络连接。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

**Figure 17-1:** 你的始终连接的企业邮件服务器的示例。你可以看到 `mynetworks` 参数的作用。默认情况下，`mynetworks` 参数包含你的本地网络 (127.0.0.0/8) 以及你在系统中配置的网络连接。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

要小心你放入 mynetworks 的内容，因为这是配置 Postfix 为开放中继最简单的方法。我们指出了第 17 章 – 邮件服务器 – Postfix, Sendmail 和 Cyrus 475

-   ♦ 允许来自以下机器的中继
-   ♦ 拒绝所有未经授权目的的中继

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

