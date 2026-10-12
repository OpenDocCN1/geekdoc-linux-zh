
DAEMON=yes

QUEUE=1h

`DAEMON=yes` 条目设置 sendmail 监听 TCP/IP 端口 25 消息，该端口与 SMTP 关联。`QUEUE=1h` 条目告诉 sendmail 每小时递送一次队列中的邮件。

## SENDMAIL 别名 (ALIASES)

`/etc/aliases` 文件也很简单。它指定了应该真正接收邮件的用户。例如，如果你尝试向 `ftp@localhost` 等服务发送 sendmail，以下条目会将该邮件重定向到 `root@localhost`：

```
ftp:    root
```

或者，你可以将邮件从前员工重定向到现员工。

```
byelts: vputin
```

## 配置 SENDMAIL (CONFIGURING SENDMAIL)

## SENDMAIL/ETC/MAIL 配置文件

`/etc/mail` 中有许多文件，你可以用它们来配置 sendmail 或设置数据库以规范 sendmail 的工作。如果你想启用这些配置文件，通常需要在 `sendmail.mc` 宏文件中有一个条目。如果存在 db 文件，在大多数情况下，你可以使用 `makemap` 命令转换如 `access.db` 之类的文本文件（该命令在用 `-c /etc/mail` 命令处理此目录下的配置文件时也会运行）。

- **access.db**: 配置域名或电子邮件地址；来自这些源的邮件可以被丢弃 (DISCARD)、带错误消息的拒绝 (REJECT) 或发送到特定地址 (RELAY)。你可以通过丢弃或拒绝来自特定域名或电子邮件的邮件来减少不必要的邮件。请查看 `/etc/mail/access` 文件获取示例。
- **domainable 和 domainable.db**: 映射两个不同的域名。如果你更改了域名，而其他人仍在向用户的旧邮件地址发送邮件，这些文件就会有用。如果你将域名从 `dictatorsrus.com` 更改为 `demracysisus.com`，你可以在 domainable 文件中添加以下行：

```
dictatorsrus.com democracysisus.com
```

- **helpfile**: 为 sendmail 提示符可用命令提供帮助。你可以通过 `telnet localhost 25` 命令进入 sendmail 提示符。
- **local-host-names**: 包含你的 sendmail 服务器的别名或其他主机名。只需在该文件中逐行为 sendmail 服务器计算机输入其他名称即可。
- **mailtable and mailtert.db**: 允许为特定地址指定不常用的邮件服务器类型；很少使用。
- **Makefile**: 允许编译不同的选项；它允许 `make -C /etc/mail` 命令处理 `/etc/mail` 目录中的所有文件。
- **sendmail.cf and sendmail.mc**: 允许你配置 sendmail。`sendmail.cf` 是配置文件；`sendmail.mc` 是一个可以处理成配置文件的宏文件。在本章稍后部分将提供有关这些文件的更多信息。
- **spamassassin**: 支持配置 SpamAssassin 垃圾邮件还原器 (www.spamassassin.org)。你可以通过向 `/etc/procmailrc` 配置文件（你可能需要创建）添加以下行为所有用户启用 SpamAssassin：

```
INCLUDESRC=/etc/mail/spamassassin/spamassassin-default.rc
```

- **statistics**: 包含 sendmail 使用统计数据。运行 `mailstats` 命令读取此文件。

## 第 21 章 邮件服务 (MAIL SERVICES)

- **submit.cf and submit.mc**: 允许将 sendmail 使用限制在特定组。默认 `submit.mc` 文件中的语法与 `sendmail.mc` 。关于 `submit.mc` 的更多信息在本章稍后部分提供。
- **trusted-users**: 允许列出代表其他用户发送邮件的用户。很少使用。
- **virtualuserable and virtualusertable.db**: 支持虚拟用户。

（注：原文后续部分存在大量重复和 OCR 错误，译文已按要求清理并保留核心内容。）

# 邮件与演进

尽管 Outlook Express 和其他 MUAs（邮件用户代理）使用了 LOGIN，但如果连接无法保证安全，则应使用其他机制。

```
TRUST_AUTH_MECH(`EXTERNAL DIGEST-MODS CRAM-MOD LOGIN PLAIN`)

define(`CONFAUTH_MECHANISMS`, `EXTERNAL GSSAPI DIGEST-MODS CRAM-MOD LOGIN PLAIN`)
```

以下命令允许你在使用 sendmail 时使用系统上的任何 SSL 证书。有关 SSL 证书的更多信息，请参阅第 25 章。你在该章中为 Apache 创建的证书也适用于此处。

### 关于为 sendmail TLS 创建证书的基础性信息：

```bash
make -C /usr/share/ssl1/certs usage
```

```
define(`CONFCACERT_PATH`, `/usr/share/ssl1/certs/`)

define(`CONFCACERT`, `/usr/share/ssl1/certs/ca-bundle.crt`)

define(`SERVER_CERT`, `/usr/share/ssl1/certs/sendmail.pem`)

define(`CONSERVER_KEY`, `/usr/share/ssl1/certs/sendmail.pem`)
```

以下 `define` 命令支持与轻量级目录访问协议（LDAP）集成，该协议提供详细的用户信息，并可以替换 `/etc/aliases` 和 `/etc/mail/virtertable.db` 文件的内容。sendmail 和 LDAP 的集成是一个复杂的课题，超出了本书的范围。

```
# 这允许 sendmail 使用一个与 OpenLDAP 的 slapd 共享的密钥文件，
# 这要求该文件对 ldap 组可读
define(`CONDFONT_BLAME_SENDMAIL`, `grouppreadablekeyfile`)
```

以下命令指定了与无法找到目的地的邮件相关的操作。例如，如果你的邮件难以送达至收件者的邮件服务器，你将在四（4）小时后收到警告消息，并在五天后收到一条无法投递的消息（`CONTO_QUEUEERTURN`）。

```
define(`CONTO_QUEUEWARN`, `4h`)

define(`CONTO_QUEERTURN`, `5d`)

define(`CONQUEUE_LA`, `12d`)

define(`CONREFUSE_LA`, `18d`)

define(`CONTO_IDENT`, `0d`)

FEATURE(`delay_checks`)

FEATURE(`no_default_msa`, `dnl`)
```

此 `feature` 命令设置了默认 sendmail 辅助程序 `smrsh`。`mailtert.db` 关联了不同的名称。

```
FEATURE(`smrush`, `/usr/sbin/smrsh`)
```

```
FEATURE('mailertable', 'hash -o/etc/mail/mailertable.db')

FEATURE('virtusertable', 'hash -o/etc/mail/virtusertable.db')

FEATURE(redirect)

FEATURE(always_add_domain)

FEATURE(use_cw_file)

FEATURE(use_ct_file)

# 如果例如用户超过了配额，-t 选项将重试投递。
FEATURE(local_db, 'procmail -t -Y -a $h -d $u)

FEATURE('access_db', 'hash -tTMP -o/etc/mail/access.db')

FEATURE(blacklist_recipients)
```

如果 `root` 用户尝试登录，`EXPOSED_USER` 命令需要电子邮件地址。

```
EXPOSED_USER('root')
```
