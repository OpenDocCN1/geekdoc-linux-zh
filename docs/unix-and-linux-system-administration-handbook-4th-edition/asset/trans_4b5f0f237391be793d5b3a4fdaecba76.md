

## 表 20.24 常见的 Postfix 后缀访问限制

| 限制 | 功能 |
|---|---|
| check_client_access | 使用查找表检查客户端主机地址 |
| check_recipient_access | 使用查找表检查收件人邮件地址 |
| permit_mynetworks | 允许列在 mynetworks 中的地址访问 |
| reject_unauth_destination | 拒绝发往非本地收件人的邮件；不允许中继 |

所有这些限制都可以进行测试，而不仅仅是像 smtpd_sender_restrictions 中的发件人地址这样的特定信息。因此，为了简化，你可能希望将所有限制放在单个参数下，这个参数应该是 smtpd_recipient_restrictions，因为它是唯一可以测试所有内容的参数（除了 DATA 部分）。

smtpd_recipient_restriction 也是测试邮件中继的地方。你应该保留 reject_unauth_destination 限制，并在其之前仔细选择 "permit" 限制。

## 访问表

每个限制返回表 20.25 中显示的操作之一。访问表用于诸如 check_client_access 和 check_recipient_access 等限制中，分别根据客户端主机地址或收件人地址选择一个操作。

## 表 20.25 访问表的操作

| 操作 | 含义 |
|---|---|
| 4nn text | 返回临时错误代码 4nn 和消息文本 |
| 5nn text | 返回永久错误代码 5nn 和消息文本 |
| DEFER_IF_PERMIT | 如果限制结果为 PERMIT，则将其更改为临时错误 |
| DEFER_IF_REJECT | 如果限制结果为 REJECT，则将其更改为临时错误 |
| DISCARD | 接受邮件但静默丢弃它 |
| DUNNO | 假装未找到该键；测试进一步的限制 |
| FILTER transport:dest | 将邮件通过 filter transport:dest* 传递 |
| HOLD | 将邮件阻塞在队列中 |
| OK | 接受邮件 |
| PREPEND header | 向消息添加一个头部 |
| REDIRECT addr | 将此邮件转发到指定地址 |
| REJECT | 拒绝邮件 |
| WARN message | 在日志中输入给定的警告消息 |

a. 请参阅从第 840 页开始的关于 Postfix 中垃圾邮件和病毒处理的章节。

例如，假设你希望允许 cs.colorado.edu 域内所有机器进行中继，并且你只希望受信任的客户端能够向内部邮件列表 newsletter@cs.colorado.edu 发布。你可以在 main.cf 中用以下行实现这些策略：

```
smtpd_recipient_restrictions =
    permit_mynetworks
    check_client_access hash:/etc/postfix/relaying_access
    reject_unauth_destination
    check_recipient_access hash:/etc/postfix/restricted_recipients
```

请注意，当为参数指定值列表时，逗号是可选的。

在 /etc/postfix/relaying_access 中：

```
.cs.colorado.edu    OK
```

在 /etc/postfix/restricted_recipients 中：

```
newsletter@cs.colorado.edu    REJECT Internal list
```

REJECT 后的文本是一个可选字符串，连同错误代码一起发送给客户端。它告诉发件人邮件被拒绝的原因。

## 客户端认证和加密

对于从家中发送邮件的用户，通常最简单的方法是通过家庭 ISP 的邮件服务器路由外出邮件，而不管该邮件上显示的发件人地址是什么。大多数 ISP 信任其直接客户端并允许中继。如果此配置不可行，或者你正在使用 Sender ID 或 SPF 等系统，请确保网络外的移动用户能够被授权向你的 smtpd 提交消息。

解决此问题的方案是使用 SMTP AUTH 机制在 SMTP 级别直接进行身份验证。Postfix 必须编译为支持 SASL 库才能使其工作。然后你可以像这样配置该功能：

```
smtpd_sasl_auth_enable = yes
smtpd_recipient_restrictions =
    permit_mynetworks
    permit_sasl_authenticated
    ...
```

你还需要支持加密连接以避免以明文发送密码。将以下类似的行添加到 main.cf 中：

```
smtpd_tls_security_level = may
smtpd_tls_auth_only = yes
smtpd_tls_loglevel = 1
smtpd_tls_received_header = yes
smtpd_tls_cert_file = /etc/certs/smtpd.pem
smtpd_tls_key_file = $smtpd_tls_cert_file
smtpd_tls_protocols = !SSLv2
```

