
当消息的接收者实际上是一个程序（例如下一节中描述的 *majordomo*）时，使用 `Mprog` 邮件器定义。为了将消息导向程序，`sendmail` 使用一个名为 `smrsh`（SendMail Restricted Shell）的程序。从安全角度来看，允许邮件直接通过管道传入程序并不是一个好主意，但 `smrsh` 使这个过程变得稍微安全一些。为了使程序成功执行，必须在 `/etc/smrsh` 目录中存在指向该程序的链接。此限制确保只有管理员安装的程序可以直接接收邮件，而其他随机可执行程序会被拒绝。

## 使用 m4 宏预处理器

虽然使用 m4 预处理器宏文件不会让配置 `sendmail` 变得简单，但至少会直观得多。例如，本章中描述的晦涩难懂的 `sendmail.cf` 文件是由以下文本文件（`/etc/mail/sendmail.mc` 文件）生成的：

```
divert(-1)
dnl This is the sendmail macro config file. If you make changes to this
dnl file, you need the sendmail-cf rpm installed and then have to
dnl generate a new /etc/sendmail.cf by running the following command:
dnl 
dnl     m4 /etc/mail/sendmail.mc > /etc/sendmail.cf
dnl
include(`/usr/lib/sendmail-cf/m4/cf.m4')
VERSIONID('linux setup for Red Hat Linux')
dnl
OSTYPE('linux')
dnl Uncomment and edit the following line if your mail needs to be sent
dnl out through an external mail server:
dnl define('SMART_HOST', 'smtp.your.provider')
define('confDEF_USER_ID', '8:12')
dnl
undefined('UUCP_RELAY')
dnl
undefined('BITNET_RELAY')
dnl
define('confAUTO_REBUILD')
dnl
define('confTO_CONNECT', '1m')
dnl
define('confTRY_NULL_MX_LIST',true)
dnl
define('confDONT_PROBE_INTERFACES',true)
dnl
define('PROCMAIL_MAILER_PATH', '/usr/bin/procmail')
dnl
define('ALIAS_FILE', '/etc/aliases')
dnl
define('STATUS_FILE', '/var/log/sendmail.st')
dnl
define('UUCP_MAILER_MAX', '200000')
dnl
define('confUSERDB_SPEC', '/etc/mail/userdb.db')
dnl
define('confPRIVACY_FLAGS',
    'authwarnings,novrfy,noexpn,restrictqrun')
dnl
define('confAUTH_OPTIONS', 'A')
dnl

dnl TRUST_AUTH_MECH('DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')
dnl
dnl define('confAUTH_MECHANISMS', 'DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')
dnl
dnl define('confTO_QUEUEWARN', '4h')
dnl
dnl define('confTO_QUEUERETURN', '5d')
dnl
dnl define('confQUEUE_LA', '12')
dnl
dnl define('confREFUSE_LA', '18')
dnl
FEATURE(delay_checks)
dnl
FEATURE('no_default_msa', 'dnl')
dnl
FEATURE('smrsh', '/usr/sbin/smrsh')
dnl
FEATURE('mailertable', 'hash -o /etc/mail/mailertable')
dnl
FEATURE('virtusertable', 'hash -o /etc/mail/virtualusertable')
dnl
FEATURE(redirect)
dnl
FEATURE(always_add_domain)
dnl
FEATURE(use_cw_file)
dnl
FEATURE(use_ct_file)
dnl

dnl The '-t' option will retry delivery if e.g. user runs over quota.
dnl
FEATURE(local_procmail, '', 'procmail -t -Y -a $h -d $u')
dnl
FEATURE('access_db', 'hash -o /etc/mail/access.db')
dnl
FEATURE('blacklist_recipients')
dnl
EXPOSED_USER('root')
dnl

dnl This changes sendmail to only listen on the loopback device
dnl 127.0.0.1and not on any other network devices. Comment this out if
dnl you want to accept email over the network.
DAEMON_OPTIONS('Port=smtp,Addr=127.0.0.1, Name=MTA')
dnl NOTE: binding both IPv4 and IPv6 daemon to the same port requires
dnl     a kernel patch
dnl DAEMON_OPTIONS('port=smtp,Addr=::1, Name=MTA-v6, Family=inet6')
dnl We strongly recommend to comment this one out if you want to
dnl protect yourself from spam. However, the laptop and users on
dnl computers that do not have 24x7 DNS do need this.
FEATURE('accept_unresolvable_domains')dnl
dnl FEATURE('relay_based_on_MX')dnl
MAILER (smtp)dnl
MAILER(procmail)dnl
Cwdlocalhost.localhostdomain
```

与 `sendmail.cf` 文件相比，它几乎看起来可读。通过一系列 `include`、`define`、`undefined` 和 `feature` 操作，该文件将模板化的 m4 宏文件组合起来，形成 `sendmail.cf` 文件。

`dnl` 命令用于注释条目，但技术定义是“删除直到新行（Delete through New Line）”。请注意，`dnl` 命令也用于终止命令。`include` 命令使用 `cf.m4` 文件作为原型，而 `OSTYPE` 命令设置 Red Hat Linux 特有的配置选项。`define` 命令执行与在 `sendmail.cf` 文件中设置类似选项相同的任务。例如，从 `confAUTO_REBUILD` 开始，与上述 `define` 命令等效的选项和宏依次为 `AutoRebuildAliases`、`Timeout.connect`、`TryNullMXList`、`DontProbeInterfaces` 以及 `Procmail` 邮件器规范。

最后，通过以下命令将这个 `sendmail.mc` 文件转换为 `sendmail.cf` 文件：

```
m4 /etc/mail/sendmail.mc > /etc/sendmail.cf
```

有关通过 m4 宏预处理器可用的配置选项的详细信息，可以在 `www.sendmail.org/m4/tweakingoptions.html` 找到。

## .forward 文件

用户重定向自己邮件的一种方式是通过使用 `.forward` 文件，如之前列出的 `sendmail.cf` 文件中所述。纯文本 `.forward` 文件的格式是逗号分隔的邮件接收者列表。`.forward` 文件的常见用途包括：

- 将邮件通过管道传输到程序以筛选邮箱内容：

  `"| /usr/bin/procmail"`
