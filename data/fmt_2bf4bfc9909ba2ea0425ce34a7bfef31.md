
## 访问控制

邮件服务器应仅代表受信任的客户端转发邮件。如果邮件服务器将未知客户端的邮件转发到其他服务器，那么它就是所谓的开放中继（`open relay`）。幸运的是，Postfix 默认不作为开放中继。

最重要的参数是 `smtpd_recipient_restrictions`，因为当收件地址已知时执行访问控制最为容易。表 20.23 显示了参数。

### 表 20.23 SMTP访问参数

| 参数 | 应用 |
| :--- | :--- |
| `smtpd_client_restrictions` | 连接 |
| `smtpd_helo_restrictions` | HELO/EHLO 命令（会话开始） |
| `smtpd_sender_restrictions` | MAIL 命令（发送者规范） |
| `smtpd_recipient_restrictions` | RCPT 命令（收件者规范） |
| `smtpd_data_restrictions` | DATA 命令（邮件主体） |
| `smtpd_etrn_restrictions` | ETRN 命令 |

对指定的每个进行测试，直到得出确定决定。下一页的表 20.24 显示常见的限制。

### 表 20.24 常见限制

| 限制 | 功能 |
| :--- | :--- |
| `check_client_access` | 使用查找表检查客户端地址 |
| `check_recipient_access` | 使用查找表检查收件地址 |
| `permit_mynetworks` | 允许 `mynetworks` 列出的地址访问 |
| `reject_unauth_destination` | 拒绝非本地收件者的邮件 |

所有内容都可以在这些限制中进行测试，而不只是 `smtpd_sender_restrictions` 中的发送者地址。因此，为了简单起见，你可能想将所有限制放在一个参数下，该参数应该是 `smtpd_recipient_restrictions`，因为它是唯一可以测试所有内容的（DATA 部分除）。

访问表

每个限制返回表 20.25 所示的操作。访问表用于 `check_client_access` 和 `check_recipient_access` 等限制，以分别根据客户端地址或收件地址选择动作。

### 表 20.25 访问表的动作

| 动作 | 含义 |
| :--- | :--- |
| `4nn text` | 返回临时错误代码 4nn 和文本 |
| `5nn text` | 返回永久性错误代码 5nn 和文本 |
| `DEFER_IF_PERMIT` | 如果结果为 PERMIT，则将其变为临时错误 |
| `DEFER_IF_REJECT` | 如果结果为 REJECT，则将其变为临时错误 |
| `DISCARD` | 接受消息但静默丢弃 |
| `DUNNO` | 假装未找到键；测试后续限制 |
| `FILTER:transport:dest` | 通过过滤器 `transport:dest` 传递邮件 |
| `HOLD` | 在队列中阻塞邮件 |
| `OK` | 接受邮件 |
| `PREPEND header` | 为消息添加头头 |
| `REDI addr` | 将此邮件转发到指定地址 |
| `REJECT` | 拒绝邮件 |
| `WARN message` | 在日志中输入给定的警告信息 |

## 客户端认证与加密

向内部邮件列表 `newsletter@cs.colorado.edu` 发送。你可以在 `main.cf` 中以下几行来实现这些策略：

```
smtpd_recipient_restrictions =
  permit_mynetworks
  check_client_access hash=/etc/postfix/relaying_access
  reject_unauth_destination
  check_recipient_access hash=/etc/postfix/restricted_recipients
```

请注意，当指定参数的值列表时，注释是可选的。在 `/etc/postfix/relaying_access` 中：

```
.cs.colorado.edu OK
```

在 `/etc/postfix/restricted_recipients` 中：

```
newsletter@cs.colorado.edu REJECT Internal list
```

`REJECT` 之后的文本是一个可选字符串，它会随错误代码一起发送给客户端。它会告诉发送者为什么邮件被拒绝了。

## 客户端认证与加密

对于从家里发送邮件的用户，通常最简单的方法是将出站邮件通过家庭 ISP 的邮件服务器路由，无论邮件上显示的发件人地址是什么。大多数 ISP 都信任其直接客户端并允许中继。如果无法进行配置，或者你正在使用 Sender ID 或 SPF 等系统，请确保网络外的移动用户已授权向你的 `smtppd` 提交消息。

该问题的解决方案是使用 SMTP AUTH 机制直接在 SMTP 级别进行认证。Postfix 必须编译时包含对 SASL 库的支持才能实现此功能。然后你可以这样配置该功能：

```
smtpd_sasl_auth_enable = yes
smtpd_recipient_restrictions =
  permit_mynetworks
  permit_sasl_authenticated
```

你还需要支持加密连接，以避免以明文发送密码。在 `main.cf` 中添加类似下方的行：

```
smtpd_tls_security_level = may
smtpd_tls_auth_only = yes
smtpd_tls_joggle = 1
smtpd_tls_received_header = yes
smtpd_tls_cert_file = /etc/certs/smtp_pem
smtpd_tls_key_file = $smtpd_tls_cert_file
smtpd_tls_protocols = !SSLv2
```

## 第 20 章 电子邮箱

你需要在 `/etc/certs/smtp.pem` 中准备一个经过正确签名的证书。开启出站 SMTP 连接的加密也是一个好主意：

```
smtp_tls_security_level = may
smtp_tls_loglevel = 1
```

## 防范垃圾邮件和病毒

Postfix 拥有许多可以帮助拦截可疑邮件的功能。

一类保护功能要求严格执行 SMTP 协议。合法的邮件服务器应该遵守协议，但垃圾邮件和病毒发送者往往对其百不一顾，从而暴露自己。目前仍有处理合法邮件的完备处理器在运行，因此这种技术并不是万无一失的。请仔细选择限制条件，并监控日志文件。

以下是该类别中的一些主要功能：

- `reject_non_fqdn_` - 拒绝不包含完全限定发送人域名（`sender`）、收件人域名（`recipient`）或 HELO/EHLO 主机名（`hostname`）的消息。
- `reject_unknown_pipelining` - 如果客户端在继续操作之前等待命令状态，则中止会话。
- `reject_unknown_sender_domain` - 拒绝无法解析的发送人域名的邮件。Postfix 返回一个临时错误消息，因为该问题可能由瞬时 DNS 故障引起。
- `reject_unknown_reverse_client_hostname` - 拒绝来自没有 DNS 记录的主机的邮件。
- `smtpd_helo_required` - 要求在对话开始时进行 HELO/EHLO（`yes` 或 `no`）。
- `strict_rfc821_envelopes` - 要求 MAIL FROM 和 RCPT TO 命令中的邮件地址具有正确的语法（`yes` 或 `no`）。

未标记为参数的项目是限制条件。你通过将它们的名称包含在 `smtpd_hello_restrictions`（针对 `reject_non_fqdn_`）或 `smtpd_client_restrictions`（针对其他）中来调用它们。在将其投入生产环境之前测试限制条件（这始终是个好主意），在限制条件前面插入 `warn_if_reject`，以将效果从出站拒绝转换为警告日志消息。

## 黑名单

你可以让 Postfix 根据基于 DNS 的黑名单检查入站邮件；更多详情请参阅第 392 页的用户或站点黑名单。要启用此功能，请使用 `reject_rbl_client` 限制，并指定要查询的 DNS 服务器地址。类似的功能是 `reject_rhsbl_sender`，它检查发件人地址的域名而非客户端的主机名。

## 策略守护进程

垃圾邮件斗争示例

以下示例代表了 `main.cf` 文件中相对完整的垃圾邮件斗争配置：

```
strict_rfc8221_envelopes = yes
smtpd_helo_required = yes
smtpd_recipient_restrictions = =
reject_unknown_sender_domain
reject_non_fqdn_sender
reject_non_fqdn_recipient
permit_mynetworks
permit_sasl_authenticated
check_client_access hash: /etc/postfix/relaying_access
reject_unauth_destination
reject_unauth_pipelining
reject_unknown_reverse_client_hostname
reject_rbl_client zen.spamhaus.org
permit
```

注意，我们在 `permit_mynetworks` 之前放置了一些限制条件。

## SpamAssassin 和 procmail

以下示例代表了 `main.cf` 文件中相对完整的垃圾邮件斗争配置：

```
strict_rfc8221_envelopes = yes
smtpd_helo_required = yes
smtpd_recipient_restrictions = =
reject_unknown_sender_domain
reject_non_fqdn_sender
reject_non_fqdn_recipient
permit_mynetworks
permit_sasl_authenticated
check_client_access hash: /etc/postfix/relaying_access
reject_unauth_destination
reject_unauth_pipelining
reject_unknown_reverse_client_hostname
reject_rbl_client zen.spamhaus.
```

注意，我们在 `permit_mynetworks` 之前放置了一些限制条件。
