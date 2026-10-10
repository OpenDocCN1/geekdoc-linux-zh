
`define(`CONFDONT_PROBE_INTERFACES', `True')` dnl

当 `CONFTRY_NULL_MX_LIST` 为 true 时，如果接收服务器是某个主机的邮件交换（MX），sendmail 将尝试直接连接到该主机。

## 第 19 章：设置邮件服务器

如果 `DONT_PROBE_INTERFACES` 为 true，sendmail 守护进程将不会将本地接口插入已知等效地址列表中。

```
define(`PROMAIL_MAILER_PATH', `/usr/bin/procmail')
define(`ALIAS_FILE', `/etc/aliases')
dnl define(`STATUS_FILE', `/var/log/mail/statistics')
dnl
```

上述三行（`PROMAIL_MAILER_PATH`、`ALIAS_FILE` 和 `STATUS_FILE`）分别设置分发传入邮件（默认为 `procmail`）的程序、邮件别名文件以及邮件统计文件的位置。

```
define(`UUCP_MAILER_MAX')
```

`UUCP_mailer-max` 行设置了 UUCP 邮件传输器接收的邮件最大长度（字节）。`userdbspec` 行设置了用户数据库的位置（你可以在此处为特定用户覆盖默认邮件服务器）。隐私标志行会导致 sendmail 插入某些邮件。例如，`authwarnings` 会导致使用并记录 X-Authentication 头部到日志文件中。`novrpy` 和 `noexpn` 设置防止对这些服务的请求。sendmail 的 `restrictgrun -q` 选项。

```
define(`CONFAUTH_OPTIONS')
```

```
define(`CONFCACERT_PATH', `/etc/pki/tls/certs/ca-bundle.cert')
define(`CONFCACERT', `/etc/pki/tls/certs')
define(`CONFSERVER_CERT', `/etc/pki/tls/certs/sendmail.pem')
define(`CONFSERVER_KEY', `/etc/pki/tls/certs/sendmail.pem')
define(`CONFBLAME_SENDMAIL', `groupreadablekeyfile')
```

上述显示的某些行以 `dnl` 开头（因此它们被注释掉了），可以取消注释（删除初始句首的 `dnl`）来提供某些功能。其他行是显式的。`confAUTH_OPTIONS` 行可用于设置带有 SMTP 认证的选项。此带有 `TRUST_AUTH_MECH` 行的示例将允许认证登录发送邮件。`TRUST_AUTH_MECH` 行会让 sendmail 允许除纯密码以外的认证机制（如果该行可以配置可使用的认证机制类型（如果删除了 `dnl`）。上面的几行将证书目录的位置设置为 `/etc/pki/tls/certs`，这识别出该目录中的不同文件持有认证所需的证书和密钥。如果密钥文件需要被（通常）以外的应用程序读取，则应取消 `DONT_SENDMAIL` 行的注释。（通常情况下，你不希望该文件被所有人读取。）

## 806 第 4 部分：Fedora RHEL 网络和服务器设置

```
dnl define(`CONFTO_QUEUEWARN', `4h')dnl
dnl define(`CONFTO_QUEUETURN', `5d')dnl
dnl define(`CONFQUEUE_LA', `12d')dnl
dnl define(`CONFREFUSE_LA', `18d') // 根据上下文从 CONFUSE_LA 修正
define(`CONFTO_IDENT', `0d')dnl
```

上述注释的行实际上显示了为某些超时条件设置的默认值。你可以根据需要删除注释并更改这些值。`CONFTO_QUEUEWARN` 选项设置了邮件投递延迟到向发送者发送警告消息的时间。四小时（4h）是默认值。`CONFTO_QUEUETURN` 选项设置了无法投递的邮件返回之前。`CONFQUEUE_LA` 和 `CONFUSE_LA` 选项设置了邮件队列或被拒绝的系统负载级别。`CONFTO_IDENT` 选项设置了等待接收 ID 查询响应的超时时间（默认为 0，意味着无超时）。

```
FEATURE('no default_msa', '')dnl
FEATURE('smsh', '/usr/sbin/smsh')dnl
FEATURE('mailertable', 'hash -o /etc/mail/mailertable.db')dnl
FEATURE('virtuosable', 'hash -o /etc/mail/virtuosable.db')dnl
FEATURE(redirect)dnl
FEATURE(always_add_domain)dnl
FEATURE(use_cw_file)dnl
FEATURE(use_ct_file)dnl
FEATURE('access_db', 'hash -T:TMPDB -o /etc/mail/access.db')dnl
FEATURE('blacklist_recipients')dnl
```

`FEATURE` 用于设置某些特殊的 sendmail 特性。`no_default_msa` 特性告诉 sendmail 不要生成默认 MSA 守护进程（通常设置为监听端口 587）。`smsh` 特性将 `/usr/bin/smsh` 定义为 sendmail 用于接收命令的简单 shell。`mailertable` 和 `virtuosable` 选项设置了 mailertable 和 virtuosable 数据库的位置。`redirect` 选项允许拒绝已移动用户的邮件并提供新地址。`always_add_domain` 选项使用本地域名将其添加到所有投递邮件的主机名中。`use_cw_file` 和 `use_ct_file` 选项分别告诉 sendmail 使用 `/etc/mail/local-host-name` 作为此邮件服务器的备用主机名，使用 `/etc/mail/trusted-users` 作为信任用户。（信任用户可以以另一个用户的身份发送邮件而不会产生警告消息）

`local_procmail` 选项设置了用于投递本地邮件（procmail）的命令（格式为如 de $h 主机名和 $u 用户名）。`access_db` 选项设置了访问数据库的位置，该数据库识别哪些主机和用户允许中继邮件。`blacklist_recipients` 选项设置

# 第 19 章：设置邮件服务器

允许中继。第三行代表一个你知的垃圾邮件中继域名，因此我们拒绝来自该域的邮件。

接下来的三行指示了根据与邮件相关的发件人（From）和收件人（To）名称如何处理接收用于中继的邮件。如你所见，第一个示例允许中继来自 chris@linuxutoys.net 的任何邮件。在最后一个示例中，转发到特定个人（former-user@linuxutoys.net）的邮件将被拒绝，并向发送者发送自定义错误（在此例中为“用户不再在此工作”）。

> 注意：在根据用户电子邮件地址创建中继规则时要倍小心。因为这些值是由用户本身报告的，它们容易受到伪造攻击。

一旦你根据需要调整了此文件，就必须重新构建访问数据库（access.db 文件）以使更改生效。有关此主题的信息，请参阅“启动 sendmail 并生成数据库文件”。

## 配置虚拟服务器

如果你为一个域名设置了邮件服务器，那么很可能某一天你将希望从同一台计算机上服务多个域名。要在同一台计算机上创建虚拟服务器，你必须将每个正在服务的域名名称添加到 `/etc/mail/local-host-names` 文件中。

例如，如果你的邮件服务器处理 linuxutoys.net、example.com 和 example.net 的电子邮件帐户，local-host-names 文件将显示如下：

```
# local-host-names - 在此处包含你机器的所有别名。
linuxutoys.net
example.com
example.net
```

即使你的邮件服务器只服务一个域名，在该文件中标识该域名也是一个好主意。当发往此处列出的域名的邮件到达服务器时，sendmail 知道在本地投递这些邮件。sendmail 将未列在此处的域名的邮件解释为中继。

> 注意：如果你想卸载当前定向到你的邮件服务器的特定域名的邮件处理，可以使用 `/etc/mail/mailertable` 文件。在为该域名设置 DNS MX 记录指向你的邮件服务器后，并在 mailertable 文件中列出该域名，你可以指定另一台计算机，sendmail 将将该域的所有流量转发到该计算机。例如：

```
example.com	smt:mx1.linuxutoys.net
```
