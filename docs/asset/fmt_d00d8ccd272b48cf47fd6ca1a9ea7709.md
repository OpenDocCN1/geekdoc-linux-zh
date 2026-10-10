
注意：ISP 可能不允许你在家庭账户上拥有私有邮件服务器。要执行这一点，在设置邮件服务器之前你可能需要联系他们。

### 配置基础 sendmail 设置 (`sendmail.mc`)

你邮件服务器的大部分配置来自 `/etc/mail/sendmail.mc` 中的信息。由于该文件设置了大多数情况下可使用的 sendmail 默认值，你可能不需要对其进行任何操作。然而，`sendmail.mc` 的更改不会立即生效。你必须编译 `sendmail.mc` 设置以生成 `/etc/mail/sendmail.cf` 文件。我在“启动 sendmail 并生成数据库文件”部分描述了如何进行操作。生成的 `/etc/mail/sendmail.cf` 文件包含 1800 行设置和注释，用于引导你的 sendmail 进程的行为。`sendmail.mc` 文件中的 m4 宏与 `sendmail.cf` 文件中生成的设置不同。

注意：`m4` 工具可用于处理 IEEE 标准 1003.1 格式包含宏的文本文件。要了解 `sendmail.cf` 文件中的设置，请参考 `/usr/share/doc/sendmail/README.cf`。如果你对 `sendmail.cf` 文件的内容感兴趣，Fedora 6 和 Red Hat Enterprise Linux 网站包含了 `sendmail.cf` 的详尽描述。

警告：由于 Fedora 中配置 sendmail 的方式，你不应直接修改 `sendmail.cf` 文件。当 sendmail 重启或 `sendmail.mc` 变化时，`sendmail.cf` 文件会自动重新生成。因此，直接对 `sendmail.cf` 进行的修改将丢失。

以下代码示例来自 Fedora 版本 sendmail 的 `/etc/mail/sendmail.mc` 文件。

注意：`sendmail.mc` 文件中带有 `dnl`（删除行）的行是注释行。在大多数情况下，我在所示的示例中省略了它们。

```
divert(-dnl)
include('/usr/share/sendmail-cf/m4/cf.m4') dnl
VERSIONID('setup for Red Hat Linux') dnl
OSTYPE('linux') dnl
```

`sendmail.mc` 文件的前几行执行清理工作。`diver` 行在生成配置时移除多余输出。`include` 行包含了 sendmail 需要的规则。`VERSIONID` 行标识配置文件适用于 Red Hat Linux 系统（如 Fedora，尽管没有检查此设置，但它可以是任何内容）。`OSTYPE` 必须设置以获取 sendmail 需要的文件正确位置。

```
dnl define('SMART_HOST', 'smtp.provider') dnl
```

默认情况下，sendmail 进程直接向其地址所在的邮件服务器发送电子邮件。如果你想将所有电子邮件中继到特定的邮件服务器实例，可以移除 `SMART_HOST` 行开头的注释（`dnl`，代表“删除行”），但在末尾保留一个。然后，将 `smtp.provider` 更改为你想要使用的邮件服务器的完全限定域名。当然，请确保你定义的 SMART HOST 会接受来自你邮件服务器的中继。

```
dnl define('CONFDEF_USER_ID', '8:12') dnl
```

根据之前的 `CONFDEF_USER_ID` 行，进程不是以 root 运行，而是以邮件用户 (`UID 8`) 和邮件组 (`GID 12`) 运行。这是一个良好的策略，因为它防止了可能破坏你邮件服务器的人获得你机器的 root 权限。

```
dnl define('AUTO_REBUILD') dnl
define('confTO_CONNECT','1m') dnl
```

如果你删除了初始的 `dnl`，`AUTO_REBUILD` 行必须设置为在必要时自动重建别名数据库。`confTO_CONNECT` 行设置邮件服务器等待初始连接完成的时间为一分钟（`1m`）。

```
define('confTRY_NULL_MX_LIST',true) dnl
define('confCNT_PROBE_INTERFACES',true) dnl
```

使用 `confTRY_NULL_MX_LIST`，如果接收服务器是该主机的最佳邮件交换 (`MX`)，sendmail 将尝试直接连接该主机。如果

## 第19 章：设置邮件服务器

如果 `CONFDONTONT_PROBE_INTERFACES` 为 true，sendmail 守护进程将不会将本地插入已知等效地址列表中。

```
define(`PROMAIL_MAILER_PATH`, `/usr/bin/procmail`)`dnl
define(`ALIAS_FILE`, `/etc/aliases`)`dnl
dnl define(`STATUS_FILE`, `/var/log/mail/statistics`)`dnl
```

接下来的三行（`PROC_MAILER_PATH`、`ALIAS_FILE` 和 `STATUS_FILE`）分别设置了传入邮件（默认为 `procmail`）的程序、邮件别名文件以及邮件统计文件的位置。

```
define(`UCCP_MAILER_MAX`, `2000000`)`dnl
define(`USERDB_SPEC`, `/etc/mail/userdb.db`)`dnl
define(`CONFPRIVACY_FLAGS`, `authwarnings, novrry, noexceptrestrict`)`dnl
define(`CONFAUTH_OPTIONS`, `A`)`dnl
```

`UQCP_MAIL` 行设置了 UQCP 邮件接收消息的最大大小（以字节计）。`confUSERDB_SPEC` 行设置了用户数据库的位置（你可以在那里为特定用户覆盖默认邮件服务器）。`confPRIVACY_FLAGS` 标志会导致 sendmail 在控制邮件上注入身份验证。例如，`authwarnings` `Authentication-Warning` 头部用于通知登录，而 `noexcept` 设置防止这些服务被请求。`restrict` 选项为 sendmail 提供了 `-q` 选项。

```
dnl define(`CONFAUTH_OPTIONS`, `A p`)`dnl
dnl TRUE_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN`)`dnl
dnl define(`CONFAUTH_MECHANISMS`, `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN`, `/usr/share/ssl/*`)
dnl define(`CONFACERT_PATH`, `/usr/share/ssl/certs/*`)`dnl
dnl define(`CONFACERT`, `/usr/share/ssl/certs/ca-bundle.crt`)`dnl
dnl define(`CONFSERVER_CERT`, `/usr/share/ssl/certs/sendmail.pem`)`dnl
dnl define(`CONFSERVER_KEY`, `/usr/share/ssl/certs/sendmail.pem`)`dnl
dnl define(`CONFDONT_BLAME_SENDMAIL`, `groupablekeyfile`)`dnl
```

你刚刚展示的一些行以 `dnl` 开头（因此它们被注释掉了），可以通过取消注释（删除初始的 `dnl`）提供某些功能。其他行则是显式设置的。`CONFAUTH_OPTIONS` 行可用于设置 SMTP 身份验证的选项。此示例（带有 `A` 和 `p` 选项）将允许使用明文登录的身份验证用户发送邮件。`TRUE_AUTH_MECH` 行（如果删除了 `dnl`）会导致 sendmail 允许密码以外的身份验证机制。`CONFAUTH_MECHANISMS` 行可以配置所需的身份验证机制类型（如果删除了 `dnl`）。接下来的列表是 sendmail 证书目录 `/usr/share/ssl/certs` 之前的几行：

```
dnl define(`CONTO_QUEUEWARN`, `4h`)dnl
dnl define(`CONTO_QUEUETURN`, `5d`)dnl
dnl define(`CONQUEUE_LA`, `12m`)dnl
dnl define(`CONREFUSE_LA`, `18d`)dnl
define(`CONTO_IDENT`, `0s`)
```

你可以根据需要更改这些值。`CONTO_QUEUEWARN` 选项设置了邮件投递延迟多久后向发送者发送警告消息。`CONTO_QUEUETURN` 选项设置了无法投递的邮件返回之前的时间。`CONQUEUE_LA` 选项设置了接收邮件进入队列或拒绝的系统负载平均值。`CONTO_IDENT` 选项设置了等待 ID 查询响应的时间（默认是 0，意味着无超时）。
