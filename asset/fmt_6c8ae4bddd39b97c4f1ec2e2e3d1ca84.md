
## 增强您的 iptables 防火墙

您可以通过多种方式修改或扩展本章中给出的 iptables 示例。`iptables` 具有极大的灵活性。

当您实际创建自己的 `iptables` 防火墙时，您应参考 `iptables` 手册页（输入 `man iptables`）以获取选项、匹配方式、输入地址方式和其他细节的详细描述。我还推荐 Oskar Andreason 的优秀 `iptables` 教程（http://iptables-tutorial.frozentux.net）。

以下是使用 `iptables` 功能的几个提示：

- **减少规则** — 尝试通过减少规则数量来提高性能。使用子链可以防止数据包看到不适用于它的规则。
- **处理分片** — 使用 `-f` 选项来引用被拆分为分片的数据包的第二个及后续数据包。通常，对于没有第一个数据包分片的第二个和第三个分片，安全地不丢弃它们，因为它们不会被重新组装。如果您使用 NAT，分片在过滤之前会被组装，因此您不应该出现未过滤分片被发送通过的问题。
- **相反** — 要使规则与其相反，请使用感叹号（`!`）。
- **所有接口** — 要匹配某类接口的所有接口，请使用加号（`+`），如 `eth+`。
- **阻止连接** — 使用 `--syn` 选项阻止 SYN 数据包（即请求连接的那些数据包）。此选项仅适用于 TCP 数据包。
- **限制** — 使用 `--limit` 选项限制导致日志消息的匹配的速率。此选项允许匹配每秒仅产生有限次数的消息（默认每小时三次，突发五次）。
- **DOS 攻击** — 您可以使用 `--limit` 选项来减少 DOS 攻击的影响，但它并不能完全阻止它们。只要流量指向您的服务器，您的网络带宽就会被耗尽，并且机器仍会利用资源来忽略数据。
- **表类型** — 默认表类型是 *过滤*。其他类型的表是 *nat*（用于 IP 伪装）和 *mangle*（用于修改数据包）。要使用 *过滤* 以外的表，您必须添加 `-t table_type` 选项，其中 *table_type* 为 *nat* 或 *mangle*。

## 从日志文件检测入侵

为系统准备抵御黑客攻击只是战斗的一部分。您还必须在攻击发生时识别出黑客攻击。了解 Red Hat Linux 记录重要事件的各种日志文件对于实现这一目标至关重要。Red Hat Linux 系统的日志文件可以在 `/var/log` 目录中找到。

Red Hat Linux 附带一个系统日志窗口（`redhat-logview` 命令），您可以使用它从 GUI 查看和搜索关键系统日志文件。要打开系统日志窗口，请从主桌面菜单中单击 系统工具 → 系统日志。图 14-3 显示了系统日志窗口的示例。

要查看特定日志文件，请单击左侧列中的日志名称。如果您正在查找特定消息或问题，请在“筛选条件”框中输入关键字，然后单击筛选。仅显示包含该词的行。大写字母有区别，因此使用筛选器搜索“Mem”时找不到“mem”。单击重置以再次显示整个文件。

表 14-6 包含在系统日志窗口中显示的日志文件列表，以及 `/var/log` 目录中可能引起您兴趣的其他文件。（* 表示不在系统日志窗口中的日志文件。请直接从 `/var/log` 访问这些文件。）

![](img/27a85d56d393921ced6412ae6e8336bf_546_0.png)

图 14-3：在系统日志窗口中显示系统日志文件。

## 表 14-6：/var/log 目录中的日志文件

| 系统日志名称 | 文件名 | 描述 |
|---|---|---|
| 启动日志 | boot.log | 包含指示哪些系统服务已成功启动和关闭以及哪些（如有）启动或停止失败的消息。 |
| Cron 日志 | cron | 包含来自 crond 的状态消息，crond 是一个定期运行计划作业（如备份和日志文件轮转）的守护进程。 |
| 内核启动日志 | dmesg | 系统启动时内核打印的消息记录。 |
| FTP 日志 | xferlog | 使用 wu-ftp FTP 服务传输的文件信息。 |
| Apache 访问日志 | httpd/access_log | 记录来自您的 Apache Web 服务器的信息请求。 |
| Apache 错误日志 | httpd/error_log | 记录客户端尝试访问您的 Apache Web 服务器数据时遇到的错误。 |

| 系统日志名称 | 文件名 | 描述 |
| :--- | :--- | :--- |
| 邮件日志 | maillog | 包含电子邮件发送到的地址和发出的地址信息。用于检测垃圾邮件。 |
| MySQL 服务器日志 | mysqld.log | 包含与 MySQL 数据库服务器 (mysqld) 活动相关的信息。 |
| 新闻日志 | spooler | 如果您正在运行 Usenet 新闻服务器，则包含该服务器消息日志的目录。 |
| RPM 包 | rpmpkgs | 包含系统中已安装的 RPM 包列表。 |
| 安全日志 | secure | 记录登录尝试和会话的日期、时间以及持续时间。 |
| 系统日志 | messages | 一个通用日志文件，许多程序都会向其记录消息。 |
| 更新代理日志 | up2date | 包含 Red Hat 更新代理操作产生的信息。 |
| XFree86 日志 | XFree86.0.log | 包含 Xfree86 服务器输出的消息。 |
| * | gdm/:0.log | 保存与登录屏幕（GNOME 显示管理器）相关的消息。 |
| * | samba/log.smbd | 来自 Samba SMB 文件服务守护进程的消息。 |
| * | squid/access.log | 包含与 squid 代理/缓存服务器相关的消息。 |
| * | vsftpd.log | 包含使用 vsFTPd 守护进程（FTP 服务器）进行传输相关的消息。 |
| * | sendmail | 由 sendmail 守护进程记录的错误消息。 |
| * | uucp | 来自 Unix 到 Unix 复制协议守护进程的状态消息。 |

## syslogd 的作用

`/var/log` 目录中的大多数文件由 `syslogd` 服务维护。`syslogd` 守护进程是系统日志守护进程。它接受来自各种其他程序的日志消息并将其写入适当的日志文件。这比让每个程序直接写入自己的日志文件更好，因为它允许您集中管理日志文件的处理方式。可以配置 `syslogd` 在日志文件中记录不同详细程度的信息。可以让它忽略除最关键消息之外的所有内容，也可以记录每一个细节。

`syslogd` 守护进程甚至可以接受来自网络上其他计算机的消息。这特别方便，因为它使您能够集中管理和审查网络上许多系统的日志文件。这种做法还有一个重大的安全优势。如果网络上的系统被入侵，黑客无法删除或修改日志文件，因为这些文件存储在另一台计算机上。不过，需要记住的是，这些日志消息默认情况下未加密。任何人只要接入本地网络，就能够在这些消息从一台机器传递到另一台机器时窃听。此外，尽管黑客可能无法更改旧的日志消息，但他能够影响系统，使得任何新的日志消息都不可信。

运行专用日志主机并不罕见，这是一台计算机，其唯一用途是记录网络上其他计算机的日志消息。因为该系统不运行其他服务，所以不太可能被入侵。这使得黑客几乎不可能抹去自己的痕迹。然而，这并不意味着在黑客入侵网络上的机器后，所有日志消息都是准确的。

### 使用 syslogd 将日志重定向到日志主机

要将计算机的日志文件重定向到另一台计算机的 `syslogd`，必须对本地 `syslogd` 的配置文件进行一些更改。您需要处理的文件是 `/etc/syslog.conf`。使用 `su` 命令成为 root，然后在文本编辑器（如 `vi`）中加载 `/etc/syslog.conf` 文件。您应该会看到类似以下内容：

```
# Log all kernel messages to the console.

# Logging much else clutters up the screen.

#kern.*		/dev/console

# Log anything (except mail) of level info or higher.

# Don't log private authentication messages!

*.info;mail.none;news.none;authpriv.none;cron.none	/var/log/messages

# The authpriv file has restricted access.

authpriv.*			/var/log/secure

# Log all the mail messages in one place.

mail.*			/var/log/maillog

# Log cron stuff

cron.*			/var/log/cron

# Everybody gets emergency messages

*.emerg			*
```

```
# Save news errors of level crit and higher in a special file.
```
