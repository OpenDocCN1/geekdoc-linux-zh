
`email` 指令设置 FTP 管理员的电子邮件。两个 `readme` 指令使 `ftppd` 在用户登录以及每次更改到匿名 FTP 目录树的基础目录（红帽 Linux 中的 `./var/ftp`）时，显示任何以 `README*` 开头的文件的名称和最后修改日期，以便匿名 FTP 用户看到它们。例如，给出指令 `readme README.NOW login`，则 `README.NOW` 必须位于 `/var/ftp` 中。

第一个指令在用户登录后显示 `welcome.msg` 的内容，而第二个指令显示 `.message` 文件的内容。`shutdown` 指令指向 `/etc/shutmsg`，作为服务器关闭信息的文件。

![](img/d1fbff32ec66d002a5e63f7293)

“维护服务器”章节详细地讨论了 `shutdown` 指令。为了提高服务器安全性，在 `/etc/ftaccess` 中添加以下指令：

- `greeting terse`
- `signoff terse`
- `stat terse`

这些添加的理论是防止显示黑客可能用来破解系统的服务器信息。`greeting terse` 在用户登录时显示 FTP server ready，而默认是显示主机名和版本号。`signoff terse` 在用户断开时显示 Goodbye（默认是显示传输统计和主机名）。默认情况下，`stat` 指令提供主机名、版本号、传输统计和配额信息。而 `stat terse` 则仅显示连接状态。或者，你可以分别使用 `greeting text message`、`signoff text message` 和 `stat message` 指令提供自己的欢迎、注销和状态消息（见表 13-3）。

# 配置 WU-FTPD 日志

表 13-4 中的指令组定义了 `ftpd` 的日志策略。虽然大多数管理员将日志用于故障排查（这是正确的），但良好的日志也是监控系统性能和安全性以及执行安全审计的宝贵资源。

红帽 Linux 默认 `ftpd` 日志配置是不足够的，它仅记录了所有用户的入站和出站传输（上传和下载）。`/etc/ftpaccess` 中的相关指令是：

```
log transfers anonymous,guest,real inbound,outbound
```

为了增强审计追踪并提高您监控使用情况和安全问题的能力，请在 `/etc/ftppass` 中应用以下指令：

- `log commands anonymous,guest,real`
- `log security anonymous,guest,real`
- `log syslog+xferlog`
- `logfile /var/log/xferlog`

第一条指令记录所有允许访问 FTP 服务器的用户执行的所有命令。第二条指令记录所有违反安全规则的行为。`syslog+xferlog` 将所有传输信息同时记录在系统日志和传输日志中。重复这些信息的理由是为了利用 syslog 的功能之一：syslog 是系统日志守护进程（与 `ftppd` 无关），它支持远程日志。可以配置 syslog 志在远程主机上维护系统日志。如果 FTP 服务器被攻破，导致传输日志损坏或被篡改，传输信息仍保存在系统日志中。此外，如果系统日志位于另一个系统上，它被损坏或丢失的概率更小。最后一条指令专门定义了传输日志的名称和路径（使用默认值 `/var/log/xferlog`）。

# 配置 WU-FTPD 特性

表 13-5 显示的最后一组 `ftpd` 配置指令用于启用或禁用 FTP 服务器的各种特性。

表 13-5 WU-FTPD 特性配置指令

| 指令 | 说明 |
|--- | --- |
| `alias string dir` | 定义字符串作为 `dir` 的别名（仅对 `cd` 命令有效） |
| `compress [yes|no] [class]` | 为所有用户类或 `class` 中指定的一个或多个类启用或禁用即时文件压缩（默认为 `yes`） |
| `incmail emailaddr` | 定义一个或多个电子邮件地址以发送文件上传通知（默认不发送通知） |
| `lslong command [options]` | 定义响应匿名 FTP 用户发出的 `LIST (ls)` 命令时生成列表的命令（如果指定了选项则包含选项） |

# 第 13 章：配置 FTP 服务

| 指令 | 说明 |
| --- | --- |
| `lsplain command [options]` | 定义响应 `NLST (list)` 命令时生成列表的命令（如果指定了选项则包含选项） |
| `lsshort [options]` | 定义响应除匿名 FTP 用户外所有用户发出的 `LIST (ls)` 命令时生成列表的命令（如果指定了选项则包含选项） |
| `mailfrom emailaddr` | 定义用于发送匿名 FTP 文件上传电子邮件通知的发者名称（默认为 `wu ftppd`） |
| `mailserver hostname` | 指定主机作为一个或多个邮件服务器，用于传递所有上传电子邮件通知（默认为 `localhost`） |
| `tar [yes|no] [class]` | 为所有用户类或 `class` 中指定的一个或多个类启用或禁用即时 tar 使用（默认为 `yes`） |

Red Hat Linux 配置中的相关指令是：

- `compress yes all`
- `tar yes all`

这些语句允许所有用户使用即时压缩和 tar 功能。用于这些功能的实际命令定义在 `/etc/ftp-conversions` 中。如果您打算执行上传，特别是针对匿名 FTP 账户，请向 `/etc/ftp-access` 中添加以下指令：

- `incmail root@localhost`
- `mailfrom anupload`
- `mailserver primary.mail.server backup.mail.server`

`incmail` 指令向 `root@localhost` 发送文件上传通知。您可能想使用不同的地址。`mailfrom` 语句指定了 `ftpd` 在发送关于匿名 FTP 用户上传的电子邮件通知时使用的名称。使用一个独特的名称（如 `anupload`）易于过滤和选择此类方法。最后一条指令标识用于发送上传通知的邮件服务器。默认服务器是 `localhost`，但使用 `mailserver` 允许您在服务器上的邮件服务无法正常工作时列出一个或多个备用邮件服务器。`ftppd` 会按顺序尝试每个列出的服务器，直到接受消息为止。

# 增强型 /etc/ftpaccess 文件

列表 13-4 显示了应用在本节讨论的更改和添加后经过仔细注释的 `/etc/ftpaccess` 文件。它在本章随附的光盘源码目录中以 `ftpaccess.better` 提供。

列表 13-4: 更好的 ftppd 配置文件

```
# 拒绝系统和特殊账户

deny-uid %-99 %65534-

deny-gid %-99 %65534-
```

```
# 允许 ftp 用户

allow-uid ftp

allow-gid ftp
```

```
# 为了方便起见，定义名为 all 的类

class all real,guest,anonymous *
```

```
# 允许登录 5 次

loginfails 5
```

```
# 不让匿名用户执行任何危险操作

chmod no guest,anonymous

delete no anonymous

overwrite no anonymous

rename no anonymous

umask no anonymous
```

```
# 强制匿名用户提供符合有效电子邮件地址格式的密码

passwd-check rfc8222 enforce
```

```
# 来自远程主机的连接必须运行一个配置正确的名称服务器

deny nameserver no-dns.msg

dns refuse_match dns-match.msg

dns refuse_no_reverse dns-no-reverse.msg
```

```
# 不要让系统过载

limit all 10 Any too-many-users.msg
```
