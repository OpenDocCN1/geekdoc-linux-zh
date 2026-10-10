
## 配置基本 Sendmail 设置 (`sendmail.mc`)

你的 Sendmail 服务器的大部分配置来自 `/etc/mail/sendmail.mc` 文件中的信息。由于该文件设置了 Sendmail 的默认值，这些值在大多数情况下都可以使用，因此你可能不需要对 `sendmail.mc` 做太多修改。然而，我建议逐步浏览本节，以便你理解你的邮件服务器是如何配置的。

你对 `sendmail.mc` 文件所做的更改不会立即生效。首先，你必须编译 `sendmail.mc` 设置以生成 `/etc/mail/sendmail.cf` 文件。我在“启动 Sendmail 并生成数据库文件”一节中描述了如何执行此操作。

生成的 `/etc/mail/sendmail.cf` 文件包含超过 1,800 行用于指导你的 `sendmail` 守护进程行为的设置和注释。你在 `sendmail.mc` 文件中使用的 `m4` 宏与 `sendmail.cf` 文件中的最终设置不同。

> **注意**：`m4` 实用程序可用于处理包含 IEEE 标准 1003.1-2001 格式宏的文本文件（第 12.2 节，“实用程序语法指南”）。该编译器对你是使用单引号还是反引号非常敏感，因此在编辑 `sendmail.mc` 时要小心。有关 `m4` 实用程序的详细信息，请输入 `info m4`。

要查找在 `sendmail.cf` 文件中找到的设置应使用哪些宏，请参阅 `/usr/share/doc/sendmail*/README.cf` 文件。

> **警告**：由于 CentOS 中 Sendmail 的配置方式，你不应该直接修改 `sendmail.cf` 文件。当 Sendmail 重启或 `sendmail.mc` 发生变更时，`sendmail.cf` 文件会自动重新生成。因此，任何直接对 `sendmail.cf` 所做的修改都将丢失。

以下代码示例来自随 CentOS 版本 Sendmail 附带的 `/etc/mail/sendmail.mc` 文件。

> **注意**：在 `sendmail.mc` 文件中以 `dnl`（“delete to new line”，即删除至行尾）开头的行是注释行。在大多数情况下，我在示例中省略了它们。此外，请注意 Sendmail 使用反引号作为开引号，使用直引号作为闭引号。

```
divert(-1)dnl
include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
VERSIONID(`setup for linux')dnl
OSTYPE(`linux')dnl
```

`sendmail.mc` 文件的前几行做一些事务性工作。`divert` 行在生成配置文件时移除了多余的输出。`include` 行引入了 `Sendmail` 所需的规则集。`VERSIONID` 行标识该配置文件是用于 Linux 系统的（如 `CentOS`）（尽管此设置不受检查，因此可以是任何你喜欢的值）。然而，`OSTYPE` 必须设置为 `linux` 才能获取 `Sendmail` 所需文件的正确位置。

```
dnl define(`confSMTP_LOGIN_MSG', '$j Sendmail; $b')dnl
dnl define(`SMART_HOST', `smtp.your.provider')
```

这里有两行你可以考虑取消注释（移除 `dnl` 字符串）。`confSMTP_LOGIN_MSG` 定义可用于隐藏你正在使用的邮件服务器（将 `Sendmail` 更改为任何你喜欢的内容）。至于第二行，默认情况下，`sendmail` 守护进程会尝试将你的出站电子邮件直接发送到其地址所属的邮件服务器。如果你希望所有电子邮件都通过特定的邮件服务器中继，你可以移除 `SMART_HOST` 行开头的注释（`dnl`，意为“delete to new line”）（保留行末尾的那个）。然后，将 `smtp.your.provider` 更改为你想要使用的邮件服务器的完全限定域名。当然，你需要确保你定义的 `SMART_HOST` 会接受来自你邮件服务器的中继。

```
define(`confDEF_USER_ID', `8:12')dnl
```

守护进程不以 `root` 用户身份运行，而是以 `mail` 用户（UID 8）和 `mail` 组（GID 12）身份运行，这是基于之前设置的 `confDEF_USER_ID` 行。这是一项良好的策略，因为它可以防止可能入侵你邮件服务器的人获得你机器的 root 访问权限。

```
dnl define(`confAUTO_REBUILD')dnl
define(`confIO_CONNECT', `1m')dnl
```

## 配置邮件服务器

如果你移除初始的 `dnl`，`DEFAULT_AUTO_REBUILD` 行将指示 Sendmail 在必要时自动重建别名数据库。`confIO_CONNECT` 行将 Sendmail 等待初始连接完成的时间设置为 1 分钟 (`1m`)。

```
#define('confTRY_NULL_MX_LIST', 'True')dnl
dnl define('confDONT_PROBE_INTERFACES', 'True')dnl
```

当 `confTRY_NULL_MX_LIST` 为 true 时，如果接收服务器是该主机最佳的邮件交换 (MX)，Sendmail 将尝试直接连接到该主机。如果 `confDONT_PROBE_INTERFACES` 为 true，sendmail 守护进程不会将本地网络接口插入到已知等效地址列表中。

```
#define('PROMAIL_MAILER_PATH', '/usr/bin/procmail')dnl
dnl define('ALIAS_FILE', '/etc/aliases')dnl
dnl define('STATUS_FILE', '/var/log/mail/statistics')dnl
```

接下来的三行（`PROMAIL_MAILER_PATH`、`ALIAS_FILE` 和 `STATUS_FILE`）分别设置分发传入邮件的程序（默认为 procmail）、邮件别名文件和邮件统计文件的位置。

```
#define('UUCP_MAILER_MAX', '2000000')dnl
dnl define('confUSERDB_SPEC', '/etc/mail/userdb.db')dnl
dnl define('confPRIVACY_FLAGS', 'authwarnings,novrfy,noexpn,restrictqun')dnl
dnl define('confAUTH_OPTIONS', 'A')dnl
```

`UUCP_MAILER_MAX` 行设置由 UUCP 邮件器接收的消息的最大大小（以字节为单位）。`confUSERDB_SPEC` 行设置用户数据库的位置（你可以在此覆盖特定用户的默认邮件服务器）。`confPRIVACY_FLAGS` 行使 Sendmail 坚持使用某些邮件协议。例如，`authwarnings` 会导致使用 `X-Authentication-Warning` 头并在日志文件中记录。`novrfy` 和 `noexpn` 设置防止请求这些服务。`restrictqun` 选项防止向 Sendmail 使用 `-q` 选项。

```
dnl define('confAUTH_OPTIONS', 'A p')dnl
dnl TRUST_AUTH_MECH$EXTERNAL_DIGEST$MD5 CRAM-MDS LOGIN PLAIN'dnl
dnl define('confAUTH_MECHANISMS', 'EXTERNAL GSSAPI DIGEST-MDS CRAM-MDS LOGIN PLAIN')dnl
```

```
dnl define('confCACERT_PATH', '/etc/pki/tls/certs')dnl
dnl define('confCACERT', '/etc/pki/tls/certs/ca-bundle.crt')dnl
dnl define('conCSERVER_CERT', '/etc/pki/tls/certs/sendmail.pem')dnl
dnl define('conSERVER_KEY', '/etc/pki/tls/certs/sendmail.pem')dnl
dnl define('confDONT_BLAME_SENDMAIL', 'groupreadablekeyfile')dnl
```

上面显示的一些以 `dnl` 开头的行组（因此它们被注释掉）可以取消注释（移除初始的 `dnl`）以提供某些功能。其他则是显式设置的。

## 第四部分 网络

`confAUTH_OPTIONS` 行可用于设置与 SMTP 身份验证一起使用的选项。此示例（使用 `A` 和 `p` 选项）将允许使用明文登录的经过身份验证的用户发送电子邮件。`TRUST_AUTH_MECH` 行将使 Sendmail 允许使用除纯密码以外的身份验证机制（如果移除了 `dnl`）。`confAUTH_MECHANISMS` 行可以配置可使用的身份验证机制类型（如果移除了 `dnl`）。接下来的几行将 Sendmail 的证书目录位置设置为 `/etc/pki/tls/certs`，然后识别该目录中持有身份验证所需的证书和密钥的不同文件。如果密钥文件需要能被 Sendmail 以外的应用程序读取，则应取消 `confDONT_BLAME_SENDMAIL` 行的注释。（通常，你不想让该文件对所有人可读。）

```
dnl define('confTO_QUEUEWARN', '4h')
dnl define('confTO_QUEUERETURN', '5d')
dnl define('confQUEUE_LA', '12')
dnl define('confREFUSE_LA', '1B')
dnl define('confTO_IDENT', '0')
```

上述被注释的行实际上显示了针对某些超时条件设置的默认值。你可以随心所欲地移除注释并更改这些值。`confTO_QUEUEWARN` 选项设置消息投递延迟后向发送者发送警告消息的时间间隔。默认值为 4 小时 (`4h`)。`confTO_QUEUERETURN` 选项设置不可投递消息被退回的时间间隔。`confQUEUE_LA` 和 `confREFUSE_LA` 选项分别设置接收邮件被排队或拒绝的系统平均负载级别。`confTO_IDENT` 选项设置等待收到对 IDENT 查询响应的超时时间（默认为 0，表示没有超时）。

```
FEATURE('no_default_msa', 'dn|')dnl
FEATURE('smrsh', '/usr/sbin/smrsh')dnl
FEATURE('mailertable', 'hash -o /etc/mail/mailertable.db')dnl
FEATURE('virtusertable', 'hash -o /etc/mail/virtusertable.db')dnl
FEATURE('redirect')dnl
FEATURE('always_add_domain')dnl
FEATURE('use_cw_file')dnl
FEATURE('use_ct_file')dnl
FEATURE('local_procmail', ':procmail -t -Y -a $h -d $u')dnl
FEATURE('access_db', 'hash T:IMPF; -o /etc/mail/access.db')dnl
FEATURE('blacklist_recipients')dnl
```

`FEATURE` 宏用于设置一些特殊的 Sendmail 功能。`no_default_msa` 功能告知 Sendmail 不要生成默认的 MSA 守护进程（通常设置为监听 587 端口）。`smrsh` 功能将 `/usr/sbin/smrsh` 定义为 Sendmail 用于接收命令的简单 shell。`mailertable` 和 `virtusertable` 选项设置 mailertable 和 virtusertable 数据库的位置。`redirect` 选项允许你拒绝为已迁移用户发送邮件并提供新地址。`always_add_domain` 选项会在所有投递的邮件中将本地域名添加到主机名中。`use_cw_file` 和 `use_ct_file` 选项分别告知 Sendmail 使用文件 `/etc/mail/local-host-names` 作为此邮件服务器的替代主机名，以及使用 `/etc/mail/trusted-users` 作为受信任的用户名。（受信任用户可以作为其他用户发送邮件而不会导致出现警告消息。）

`local_procmail` 选项设置用于投递本地邮件（procmail）的命令，以及该命令的选项（包括 `$h` 主机名和 `$u` 用户名）。`access_db` 选项设置访问数据库的位置，该数据库标识哪些主机和用户允许通过服务器中继邮件。`blacklist_recipients` 选项开启服务器阻止特定用户、主机或地址的传入邮件的能力。（`access_db` 和 `blacklist_recipients` 功能对于阻止垃圾邮件非常有用。）

```
EXPOSED_USER('root'dnl)
DAEMON_OPTIONS('Port=smtp,Addr=127.0.0.1, Name=MTA'dnl)
```

`EXPOSED_USER` 行允许显示 `root` 用户名而不是伪装名称。目前，`DAEMON_OPTIONS` 行只允许接受由本地主机创建的传入邮件。如果你想允许来自 Internet 或其他网络接口（如本地局域网）的传入邮件，请务必将此行注释掉。

```
FEATURE('accept_unresolvable_domains'dnl)
```

`accept_unresolvable_domains` 选项处于开启状态，使你接受来自没有可解析域名主机计算机的邮件。如果你有需要使用邮件服务器的客户端计算机（如拨号计算机），请保持此选项开启。然而，关闭它有助于消除垃圾邮件。

```
LOCAL_DOMAIN('localhost.localdomain'dnl)
MAILER(smtp)dnl)
MAILER(procmail)dnl)
```

此处的 `LOCAL_DOMAIN` 选项使 `localhost.localdomain` 名称被接受为你的本地计算机的名称。`sendmail.mc` 文件中的最后几行定义了服务器上使用的邮件器。`/usr/share/sendmail-c/` 邮件器目录包含 SMTP、procmail 和其他邮件器的定义。在你完成对 `sendmail.mc` 文件的更改后，可以按照“启动 Sendmail 并生成数据库文件”部分中所述重新生成 `sendmail.cf` 文件。

## 定义传出邮件访问权限

每次你的 Sendmail 服务器接收到打算作为传出邮件的电子邮件消息时，服务器需要决定是否接受或拒绝该消息的中继。过于严格的策略可能会阻止合法邮件发出。过于宽松的策略可能会使你的服务器暴露在垃圾邮件发送者面前。

鉴于如今电子邮件滥用的情况，你不应该运行开放中继（即你的服务器简单地将接收到的所有消息中继到请求的邮件服务器）。垃圾邮件发送者可以使用被称为爬虫的软件来寻找开放中继。如果你让你的邮件服务器保持开放，他们会找到你，并利用你的机器来转发他们的垃圾邮件。垃圾邮件发送者使用你的机器可能会产生以下后果：

- **你可能会被列入黑名单** — 一些电子邮件黑名单维护者会自行查找开放中继并加以阻止，甚至在滥用行为被报告之前就已经生效。使用这些黑名单的服务器将阻止来自你的所有邮件，即使是合法的电子邮件也不例外。

- **人们会讨厌你** — 你的邮件服务器会被识别为发送垃圾邮件的来源。因此，人们可能会对你的服务器进行报复，或者至少非常希望你停止向他们发送广告，帮助他们摆脱债务或以某种方式提升自我。

- **你可能面临罚款甚至入狱** — 越来越多的法律正在制定，以试图阻止垃圾邮件的传播。即使你没有主动发起垃圾邮件，你也可能因过失被判定有罪，或者你的机器被关闭或没收。

本节描述如何配置 Sendmail 访问文件（`/etc/mail/access`），以包含一组合理的规则，定义你的服务器为谁转发邮件。使用访问文件，Sendmail 可以根据发送者的主机/域名、IP 地址或电子邮件地址来决定是否转发某条消息。你可以通过检查与消息关联的 `Connect`、`From` 或 `To` 数据中的这些地址，进一步细化匹配。

此时，你可以让服务器在匹配时执行四种基本操作：

- **RELAY（转发）** — 你的邮件服务器可以直接将消息发送到邮件消息中请求的邮件服务器。

- **REJECT（拒绝）** — 消息被拒绝（不转发），并且发送者会被告知已被拒绝。

- **DISCARD（丢弃）** — 消息被静默丢弃，发送者不会收到任何通知。

- **ERROR: 你选择的文本** — 你可以在这里添加一些信息性文本，以便给发送者提供未发生转发的原因。

默认情况下，`/etc/mail/access` 文件仅从直接登录到邮件服务器（localhost）的用户处转发消息。如果没有明确允许，来自所有其他机器的用户都不被允许转发消息。以下是访问文件的默认设置：

```
Connect:localhost.localhost.localdomain      RELAY
Connect:localhost                             RELAY
Connect:127.0.0.1                             RELAY
```

在设置这些默认值后，只有从本地机器发送的邮件才会被转发。因此，如果你发送的唯一出站邮件是在你直接登录到服务器时发送的，那么你就无需更改此文件。以下示例说明了你可以如何选择性地转发或拒绝你的 Sendmail 服务器收到的邮件：
