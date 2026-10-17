
`MASQUERADE_AS('mydomain.com')` 伪装不仅针对头部，还针对信封

`@mydomainalias.com`

`@mydomain.com`

# 468 第三部分：网络化 Linux

```bash
grep "\etc/mail\" /etc/mail/sendmail.cf
w /etc/mail/local-host-names
relay -o /etc/mail/relay-domains
mailertail hash -o /etc/mail/mailertail.db
virtuser hash -o /etc/mail/virtertail.db
access hash -TTMPF -o /etc/mail/access.db
# ErrorHeader=/etc/mail/error-header
# Helpfile=/etc/mail/helpfile
# UserDatabaseSpec=/etc/mail/userdb.db
# ServiceSwitchfile=/etc/mail/service.switch
# DefaultAuthInfo=/etc/mail/default-auth-info
f /etc/mail/trusted-users
```

你可以忽略以哈希符号或井号符号（`#`）开头的行；`send-mail` 将这些行视为注释。其他行是 `sendmail` 控制项，引用了 `/etc/mail` 目录中的其他文件。

以下是 `sendmail` 配置文件中引用的 `/etc/mail` 目录中文件的简要描述（请注意，这些文件并不都会出现在你的 `/etc/mail` 目录中，如果存在，该文件可能可能是）：

- `/etc/mail/access`：用于防止垃圾邮件（不想要的邮件）的访问列表
- `/etc/mail/helpfile`：SMTP 命令信息
- `/etc/mail/local-host-names`：此主机的备名列表（列表通常是该 `sendmail` 服务器接受邮件的域名列表）
- `/etc/mail/mailertail`：指定特定域名邮件路由（中继-）的表格
- `/etc/mail/relay-domains`：`sendmail` 允许外部中继的域名（中继是指使用你的 `sendmail` 服务器作为中介向他人发送邮件的过程）
- `/etc/mail/userdb.db`：用户数据库文件，指定用户如何接收入站邮件
- `/etc/mail/virtertail`：接收用户数据库

`/etc/mail` 目录包含一些其他文件 — `/etc/mail/certs` 以及带有 `.pem` 扩展名的文件 —— 这些用于在 `sendmail` 中通过 SMTP 的 STARTTLS 扩展支持增强型邮件（PEM）。STARTTLS 扩展使用 TLS（更通被称为 SSL – 安全套接层）对邮件进行身份验证和加密。RFC 2487 描述了 STARTTLS。（此 RFC 可以在 `http://ietf.org/rfc/rfc2487.txt` 在线获取）。

后续章节简要描述 `/etc/mail` 目录中的这些 `sendmail` 配置文件。

## 准备用户数据库

用户数据库在没有集中邮件服务器时帮助投递邮件。例如，假设发送到 `jdoe@someplace.net` 的邮件实际上应该发送到 `jd@home.someplace.net`。这涉及到识别用户邮件投递点——用户接收邮件的位置——以进行发送。你可以通过创建用户数据库来完成此任务。
