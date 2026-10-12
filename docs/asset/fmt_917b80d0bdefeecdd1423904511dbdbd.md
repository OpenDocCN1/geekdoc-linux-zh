
## 第 21 章 邮件服务

### 邮件与演进

尽管 Outlook Express 和其他 MU邮件使用 LOGIN。但如果连接无法保证安全，则应使用其他机制。

```
TRUST_AUTH_MECH(`EXTERNAL DIGEST-MODS CRAM-MOD LOGIN PLAIN`)

define(`CONFAUTH_MECHANISMS`, `EXTERNAL GSSAPI DIGEST-MODS CRAM-MOD LOGIN PLAIN`)
```

以下命令允许你在使用 sendmail 时使用系统上的任何 SSL 证书。有关 SSL 证书的更多信息，请参阅第 25 章。你在该章中为 Apache 创建的证书也适用于此处。

### 关于为 sendmail TLS 创建证书的基础性信息

```
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

以下命令导致 sendmail 仅在 IPv4 回环地址 `127.0.0.1` 上监听。默认情况下，sendmail 监听 `127.0.0.1`，且如果你希望 sendmail 能够处理其他网络，请删除回环地址限制。

如果你有可靠的 DNS 访问和高速互联网连接，请注释掉下一行。这可以防止 sendmail 检查与入站邮件地址相关的域名。你可以通过在行首加一个 `#` 来注释掉该行；当重启 sendmail 服务时，sendmail 将自动开始检查域名。

```
FEATURE(`accept_unresolvable_domains`) #
```

### 理解并修改 submit.mc

`submit.mc` 文件是用于创建 `submit.cf` 的宏，`submit.cf` 是用于发送电子邮件的 sendmail 配置文件。它的处理方式与 `sendmail.mc` 相同；幸运的是，它要更简单。通常情况下，你不需要对此文件进行任何更改——但理解这一点有助于知道还需要配置哪些其他文件。

前几个命令本质上与 `sendmail.mc` 中的前几个命令相同，并在本章的本节中进行了解释。

```
divert(-1) #

include(`usr/share/sendmail-cf/m4/cf.m4')

VERSIONID(`linux setup for Red Hat Linux`) #
```
