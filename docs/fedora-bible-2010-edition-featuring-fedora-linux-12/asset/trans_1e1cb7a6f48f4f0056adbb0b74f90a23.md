

可以被 sendmail 使用。如果服务器已在运行，您可以简单地重新编译配置文件，使新的设置生效而无需重启服务器。

以下小节将详细介绍这些步骤。

## 获取域名

为了让人们能够向您的邮件服务器上的用户发送邮件，您必须拥有自己的域名。第 24 章介绍了如何获取自己的域名以及设置 DNS 服务器。特别是，您需要确保 DNS 服务器上您的域名的 MX 记录指向您邮件服务器的主机名。

> **注意：** 您的 ISP 可能不允许您在家庭互联网账户上运行私有邮件服务器。为了执行这一规定，ISP 可能会阻止发往 25 端口的数据包。您可能需要联系他们以开放该端口，然后才能在该连接上设置邮件服务器。由于许多垃圾邮件以及其他恶意（或至少控制不严）的电子邮件服务器试图隐藏在动态 IP 地址之后，许多 ISP 既不允许来自动态 IP 地址的电子邮件地址，也不接受从这些服务器发送的电子邮件。

## 配置基本的 sendmail 设置 (sendmail.mc)

您的 sendmail 服务器的大部分配置来自 `/etc/mail/sendmail.mc` 文件中的信息。由于此文件设置了在大多数情况下均可使用的 sendmail 默认值，因此您可能不需要对 `sendmail.mc` 做太多修改。不过，我建议您可以逐步阅读本章节，以便了解您的邮件服务器是如何配置的。此外，要使 sendmail 作为公共服务器运行（默认情况下它仅监听本地端口），您必须编辑此文件。

您对 `sendmail.mc` 文件所做的更改不会立即生效。首先，您必须编译 `sendmail.mc` 设置以生成 `/etc/mail/sendmail.cf` 文件。我在“启动 sendmail 和生成数据库文件”一节中描述了如何进行此操作。

生成的 `/etc/mail/sendmail.cf` 文件包含超过 1,800 行的设置和注释，用于指导 sendmail 守护进程的行为。您在 `sendmail.mc` 文件中使用的 `m4` 宏与 `sendmail.cf` 文件中生成的设置是不同的。

> **注意：** 可以使用 `m4` 实用程序来处理包含 IEEE 标准 1003.1-2001 格式（第 12.2 节，实用程序语法指南）中宏的文本文件。该编译器对使用单引号和反引号的方式非常严格，因此编辑 `sendmail.mc` 时请务必小心。有关 `m4` 实用程序的详细信息，请输入 `info m4`。

要查找在 `sendmail.cf` 文件中找到的设置所使用的宏，请参阅 `/usr/share/doc/sendmail*/README.cf` 文件。

> **警告：** 由于 Fedora 中 sendmail 的配置方式，您不应直接修改 `sendmail.cf` 文件。如果您安装了 `sendmail-cf` 软件包，当 `sendmail.mc` 发生变化时，sendmail 重启时会自动重新生成 `sendmail.cf` 文件。因此，直接对 `sendmail.cf` 所做的任何修改都将丢失。

以下代码示例来自随 Fedora 版 sendmail 附带的 `/etc/mail/sendmail.mc` 文件。

> **注意：** `sendmail.mc` 文件中以 `dnl`（删除至行尾）开头的行是注释行。在大多数情况下，我在示例中省略了这些行。另外，请注意 sendmail 使用反引号作为开始引号，使用直引号作为结束引号。

```
divert(1)dnl
include('/usr/share/sendmail-cf/m4/cf.m4')dnl
VERSIONID('setup for linux')dnl
OSTYPE('linux')dnl
```

`sendmail.mc` 文件的前几行执行一些基础工作。`divert` 行在生成配置文件时删除多余输出。`include` 行包含 sendmail 所需的规则集。`VERSIONID` 行标识配置文件是用于 Linux 系统的（例如 Fedora，尽管该设置不会进行检查，因此可以是您喜欢的任何值）。然而，必须将 `OSTYPE` 设置为 `linux` 才能获得 sendmail 所需文件的正确位置。您可以选择取消注释（删除 `dnl` 字符串）以下两行：

```
dnl define('confSMTP_LOGIN_MSG', '$3 Sendmail $b')dnl
dnl define('SMART_HOST', 'smtp.your.provider')dnl
```

可以使用 `confSMTP_LOGIN_MSG` 定义来伪装您正在使用的邮件服务器（将 `Sendmail` 更改为任意内容）。至于第二行，默认情况下，sendmail 守护进程尝试直接将您发出的电子邮件发送到目标邮件服务器。如果您希望所有电子邮件通过特定的邮件服务器进行中继，您可以删除上述 `SMART_HOST` 行开头的注释（`dnl`，代表“删除至行尾”，保留末尾的 `dnl`）。然后，将 `smtp.your.provider` 更改为您要使用的邮件服务器的完全限定域名。当然，您需要确保您定义的 `SMART_HOST` 接受来自您邮件服务器的中继。

```
define('confDEF_USER_ID', 812')dnl
```

守护进程并非以 root 用户运行，而是基于先前设置的 `confDEF_USER_ID` 行，以 mail 用户（UID 8）和 mail 组（GID 12）运行。这是一个很好的策略，因为它可以防止可能入侵您邮件服务器的人获得您机器的 root 权限。

```
dnl define('confAUTO_REBUILD')dnl
define('confTO_CONNECT', '4m')dnl
```

如果您删除初始的 `dnl,`，`confAUTO_REBUILD` 行将指示 sendmail 在必要时自动重新生成别名数据库。`confTO_CONNECT` 行将 sendmail 等待初始连接完成的时间设置为一分钟（1m）。

```
dnl
define(`confTRY_NULL_MX_LIST', `True')dnl
define(`confDONT_PROBE_INTERFACES', `True')dnl
```

当 `confTRY_NULL_MX_LIST` 为 true 时，如果查找结果没有为主机返回邮件交换（MX），sendmail 将尝试直接连接到该主机。如果 `confDONT_PROBE_INTERFACES` 为 true，sendmail 守护进程不会将本地网络接口插入已知等效地址列表中。

```
dnl
define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail')dnl
define(`ALIAS_FILE', `/etc/aliases')dnl
dnl define(`STATUS_FILE', `/var/log/mail/statistics')dnl
```

前几行（`PROCMAIL_MAILER_PATH`、`ALIAS_FILE` 和 `STATUS_FILE`）分别设置了分发传入邮件的程序（默认为 procmail）、邮件别名文件和邮件统计文件的位置。以下几行与最大消息大小、用户数据库文件以及邮件协议有关：

```
dnl
define(`UUCP_MAILER_MAX', `200000')dnl
define(`confUSERDB_SPEC', `/etc/mail/userdb.db')dnl
define(`confPRIVACY_FLAGS', `authwarnings,noverify,noexpn,restrictqrun')dnl
define(`confAUTH_OPTIONS', `A')dnl
```

`UUCP_MAILER_MAX` 行设置了 UUCP mailer 接收消息的最大大小（以字节为单位）。`confUSERDB_SPEC` 行设置了用户数据库的位置（您可以在这里为特定用户覆盖默认邮件服务器）。`confPRIVACY_FLAGS` 行促使 sendmail 强制使用某些邮件协议。例如，`authwarnings` 导致使用 X-Authentication-Warning 标头并在日志文件中注明。`noverify` 和 `noexpn` 设置禁止请求这些服务。`restrictqrun` 选项禁止使用 sendmail 的 `-q` 选项。以下是几行您可以考虑取消注释的内容：

```
dnl
dnl define(`confAUTH_OPTIONS', `A p')dnl
dnl TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
dnl define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5\nLOGIN PLAIN')dnl

dnl define(`confCACERT_PATH', `/etc/pki/tls/certs/')dnl
dnl define(`confCACERT', `/etc/pki/tls/certs/ca-bundle.crt')dnl
dnl define(`confSERVER_CERT', `/etc/pki/tls/certs/sendmail.pem')dnl
dnl define(`confSERVER_KEY', `/etc/pki/tls/private/sendmail.pem')dnl
dnl define(`confDONT_BLAME_SENDMAIL', `groupreadablekeyfile')dnl
```

刚刚显示的一组以 `dnl` 开头的行（即它们是被注释掉的）中的一些可以通过取消注释（删除初始的 `dnl`）来提供某些功能。其他则被显式设置。`confAUTH_OPTIONS` 行可用于设置与 SMTP 身份验证一起使用的选项。此示例（使用 `A` 和 `p` 选项）将允许使用明文登录的经过身份验证的用户

