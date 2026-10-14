
---

## 配置参数

如果你有 Linux 和 SMTP 协议的背景，Postfix 的配置格式非常容易理解，这是它的优势之一。接下来的章节提供了配置文件选项的详细说明，并描述了参数的用途。

### `queue_directory`

当 Postfix 接收邮件时，邮件会被保留在邮件队列中进一步处理，直到投递到用户的信箱。每封邮件都存储在队列目录中的单独文件中，供 Postfix 在需要时进行取。这就是邮件队列的位置。

### `command_directory`

这是所有基于 Postfix 的命令的位置。

### `daemon_directory`

这是 Postfix 服务器进程的位置。

### `mail_owner`

这显示了运行 Postfix 的用户身份。

### `unknown_local_recipient_reject_code`

当系统中不存在该用户（用于邮件投递）时，这是返回给客户端的 SMTP 代码。在这种情况下，450 表示服务临时不可用。这告诉发送邮件的服务器应该在稍后日期重试，而不是产生永久错误并丢失邮件。

### `debug_peer_level`

如果你需要调试邮件接收过程中的任何问题，`debug_peer_level` 设置了当主机名在 debug peer 列表中连接时 Postfix 的行为。如果你想对特定的 SMTP 连接进行调试，必须在 `main.cf` 文件中添加 `debug_peer_list` 条目。

### `debugger_command`

如果你需要调试 Postfix 的运行时间，此参数指定了要使用的调试器。

### `sendmail_path`

由于 `sendmail` 通常是 Unix 的事实 MTA（邮件传输代理），Postfix 提供了一个兼容邮件的服务接口，允许专门设计为通过 `sendmail` 命令发送查询邮件的应用程序运行。这为该 提供了命令的位置。

### `newaliases_path`

当你向别名映射中添加账户时，需要运行 `newaliases` 来让 Postfix 知晓这些。这是 `newaliases` 命令的位置。我们在章节稍后将详细讨论别名。

### `mailq_path`

`mailq` 命令用于查询 Postfix 邮件队列。当你需要知道什么时，它非常有用。

### `setgid_group`

出于安全考虑，Postfix 不允许用户写入队列。此参数指定了要使用的组。

### `man_directory`

这是 Postfix 手页的位置。

### `sample_directory`

这是示例文件的位置。

### `readme_directory`

这是文档的位置。

### `mailpool_directory`

这是邮件池的位置。

### `canonical_maps`

显示了规范映射（canonical map）的位置。

### `virtual_maps`

显示了虚拟映射（virtual map）的位置。

### `relocated_maps`

当用户移动（更具体地说，邮件系统），重定位映射（relocated map）用于通知发送者已移动。

### `transport_maps`

显示了传输映射（transport map）的位置。如果你想将特定域的所有流量路由到特定主机，可以在传输映射中指定传输条目。

### `sender_canonical_maps`

显示了发送者重写映射的位置。如果你想指定规范映射来重写发出的邮件地址，则 `main.cf` 文件中存在 `sender_canonical_maps` 条目。

### `masquerade_exceptions`

显示了地址伪装异常。我们将在章节的“向外界展示”部分讨论此。

### `masquerade_classes`

列出了要去伪装的内容。

### `myhostname`

这是运行 Postfix 的服务器的名称。Postfix 在启动时会检查系统主机名，此命令允许你修复 Postfix 认为它运行在另一台机器上。我们将在“配置始终运行服务器”部分讨论主机名参数如何适配 Postfix。

### `program_directory`

这是 Postfix 服务器辅助程序的位置。

### `inet_interfaces`

显示了 Postfix 监听入站 SMTP 连接的网络接口。这有助于限制从多接口服务器接收邮件的来源。

## `defer_transports`

此项列出了需要延迟传输的传输协议。这将在本章节的“拨号服务器配置”中进行后续讨论。

## `disable_dns_lookups`

此项设置是否出于账户目的尝试将 IP 地址翻译为主机名。除非你的邮件服务器接收大量邮件，否则开启此项通常是一个好主意。

## `relayhost`

有时被称为 socalled，这是你将所有不属于 Postfix 服务器控制域范围的本地邮件转发到的机器。

## `content_filter`

内容过滤器子通常用于将你的邮件传递给病毒扫描器进行检查。内容过滤器定义了一个服务器和端口，你所有的邮件在重新插入 Postfix 工作流之前都会通过该服务器和端口进行处理。你定义的内容过滤器负责将你的邮件重新注入系统。

## `mailbox_command`

邮箱命令是用于将邮件投递到用户邮箱的程序。此的一个常见配置是 Cyrus deliver 程序，它将邮件消息注入用户的 IMAP 邮箱中。这将在本章节稍后讨论 Cyrus 时进行介绍。

## `mailbox_transport`

邮箱传输与 `mailbox_command` 非常相似。它不是使用特定程序来投递用户的邮件，而是使用一种可以在 `master.cf` 文件中用户定义的协议。它通常用于通过 LMTP（本地邮件传输协议）将邮件投递到 Cyrus IMAP 主机。在章节讨论 Cyrus 时，我们会简要提到 `master.cf`。

## `smtpd_sender_restrictions`

此项设置了客户端在连接 Postfix 服务器发送邮件时，其描述自身时的信息的限制。

## `smtpd_client_restrictions`

此项设置了通过 SMTP 连接到 Postfix 服务器的哪些限制条件。我们在本章节讨论垃圾邮件时会讨论这些设置。

## `smtpd_helo_required`

此项指定了是否可以使用 HELO 或 EHLO 命令启动 SMTP 连接。这应该在尝试限制非标准服务器发送邮件或通过你的服务器发送邮件时使用。如果你想对 HELO/EHLO 强制执行严格的规则，请也使用 `smtpd_helo_restrictions`。

## HELO AND EHLO

HELO 是握手的第一部分（之所以这样命名是因为这是我们礼貌地开始对话的方式）。当 SMTP 服务器接收来自客户端的 HELO 时，它会返回 SMTP 服务器自身的能力作为响应。随着 SMTP 的发展，增加了更多功能。为了向后兼容，HELO 命令响应的是 SMTP 服务器可以做什么的标准响应。如果 SMTP 客户端可以理解扩展 SMTP 命令，它可以使用 EHLO（扩展 HELO）开始对话。作为响应，SMTP 服务器会告诉客户端它拥有哪些额外功能。EHLO 的主要用途之一是启动安全套层 (SSL) SMTP 连接。

### `smtpd_helo_restrictions`

如果设置了 HELO/EHLO 要求，你可以使用 HELO 限制来对连接机器的主机名执行严格检查。

### `strict_rfc821_envelopes`

如果你希望连接到 Postfix 的客户端严格使用 RFC 821 信封（完全限定并包含在括号内），则此选项将拒绝任何 `MAIL. FROM:` 和 `RCPT TO:` 非 RFC 地址。

> 设置此项可能是一个坏主意，因为有很多损坏的邮件服务器假设它们可以不带角括号运行，等等。

## `smtpd_recipient_restrictions`

此项处理 SMTP 传输（RCPT TO）中指定的接收者。你可以告诉 Postfix 检查接收者是否完全限定，或者接收者域名是否托管在 Postfix 安装主机上。

## `smtpd_sasl_auth_enable`

此项指定是否为连接的客户端启用 SMTP 认证。其本身允许用户对 Postfix 服务器进行认证，但你需要在 `smtpd_recipient_restrictions` 中添加 `permit_sasl_authenticated`，以便在用户成功认证后允许中继。你还需要正确设置 SASL（认证安全层）密码数据库以便进行查询。

### `smtpd_use_tls`

此项启用到 Postfix 服务器的传输安全层 (TLS) 加密连接。关于向你的邮件服务器提供加密链接的更多信息，请查看 www.aet.tu-de/personen/jaicke/postfix_tls/。

`smtp_tls_use`
此项启用 SMTP 请求。这将告诉 Postfix 创建 TLS 连接。要检查服务器是否接受 TLS 连接，请通过 Telnet 连接端口 25 `<your_host>`。如果服务器支持 TLS，它将向你返回扩展 HELO (EHLO) 响应。

`alias_maps`
别名的位置。这些可以存储在轻量级目录访问协议 (LDAP)、网络信息系统 (NIS) 或本地的别名文件中。

`mailbox_size_limit`
此项指定用户邮箱的最大大小。这仅适用于 mbox 格式。如果你使用 maildir 格式，它指的是单个文件的大小，而不是整体。

`message_size_limit`
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

要小心你放入 `mynetworks` 的内容，因为这是配置 Postfix 为开放中继最简单的方法。我们指出了第 17 章 – 邮件服务器 – Postfix, Sendmail 和 Cyrus 475

-   ♦ 允许来自以下机器的中继
-   ♦ 拒绝所有未经授权目的的中继

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_518_0.png)

# 第四部分 ♦ 在 SUSE Linux 中实现网络服务

# 向外部世界展示

始终建议让从你的网络发送的邮件尽可能符合互联网标准。为什么呢？如果你在笔记本电脑上运行 Postfix，你将使用系统的 `mail` 命令发送邮件，如果你没有配置地址重写，邮件将以 `username@fullname` 的形式发送。这并不美观，并且可能会给他人回复你的邮件带来困难。为了解决这些问题，你需要对邮件标头进行伪装（masquerade），以便它们在离开系统之前是整洁的。

`masquerade_domains` 参数通过在邮件离开 Postfix 之前重写其域名部分来控制这种行为。例如，如果你的机器名为 `foo.com`，而你的域名是 `bar.com`，你需要移除 "foo" 部分。`masquerade_domains` 参数可以将你的域名作为参数来解决这个问题。
