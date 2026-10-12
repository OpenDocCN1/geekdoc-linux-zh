

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

/var/log 目录中的大多数文件由 syslogd 服务维护。syslogd 守护进程是系统日志守护进程。它接受来自各种其他程序的日志消息并将其写入适当的日志文件。这比让每个程序直接写入自己的日志文件更好，因为它允许您集中管理日志文件的处理方式。可以配置 syslogd 在日志文件中记录不同详细程度的信息。可以让它忽略除最关键消息之外的所有内容，也可以记录每一个细节。

syslogd 守护进程甚至可以接受来自网络上其他计算机的消息。这特别方便，因为它使您能够集中管理和审查网络上许多系统的日志文件。这种做法还有一个重大的安全优势。如果网络上的系统被入侵，黑客无法删除或修改日志文件，因为这些文件存储在另一台计算机上。不过，需要记住的是，这些日志消息默认情况下未加密。任何人只要接入本地网络，就能够在这些消息从一台机器传递到另一台机器时窃听。此外，尽管黑客可能无法更改旧的日志消息，但他能够影响系统，使得任何新的日志消息都不可信。

运行专用日志主机并不罕见，这是一台计算机，其唯一用途是记录网络上其他计算机的日志消息。因为该系统不运行其他服务，所以不太可能被入侵。这使得黑客几乎不可能抹去自己的痕迹。然而，这并不意味着在黑客入侵网络上的机器后，所有日志消息都是准确的。

### 使用 syslogd 将日志重定向到日志主机

要将计算机的日志文件重定向到另一台计算机的 syslogd，必须对本地 syslogd 的配置文件进行一些更改。您需要处理的文件是 /etc/syslog.conf。使用 su 命令成为 root，然后在文本编辑器（如 vi）中加载 /etc/syslog.conf 文件。您应该会看到类似以下内容：

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
uucp,news.crit /var/log/spooler
# Save boot messages also to boot.log
local7.* /var/log/boot.log
#
# INN
#
news.=crit /var/log/news/news.crit
news.=err /var/log/news/news.err
news.notice /var/log/news/news.notice
```

以 # 字符开头的行是注释。其他行包含两列信息，由冒号分隔（空格无效）。左字段是以分号分隔的消息类型和消息优先级列表。右字段是要写入这些消息的日志文件。要将消息发送到另一台计算机（日志主机）而不是文件，只需将日志文件名替换为 @ 字符，后跟日志主机的名称。例如，要重定向通常发送到 messages、secure 和 maillog 日志文件的输出，请对上述文件进行以下更改：

```
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;news.none;authpriv.none;cron.none @loghost
# The authpriv file has restricted access.
authpriv.* @loghost
# Log all the mail messages in one place.
mail.* @loghost
```

消息现在将发送到名为 loghost 的计算机上运行的 syslogd。名称 loghost 并非随意选择。通常会创建这样的主机名，并将其设为作为日志主机实际系统的别名。这样，如果您需要将日志主机职责切换到另一台机器，只需更改 loghost 别名；无需在每台计算机上重新编辑 syslog.conf 文件。

## 了解 messages 日志文件

由于许多程序和服务都会向 messages 日志文件记录信息，因此了解此文件的格式非常重要。检查此文件通常会为您提供系统出现问题的早期预警。文件中的每一行都是某个程序或服务记录的单条消息。以下是实际 messages 日志文件的一个片段：

```
Feb 25 11:04:32 toys network: Bringing up loopback interface: succeeded
Feb 25 11:04:35 toys network: Bringing up interface eth0: succeeded
Feb 25 13:01:14 toys vsftpd(pam_unix)[10565]: authentication failure;
loginme= uid=0 euid=0 tty= ruser= rhost=10.0.0.5 user=chris
```

```
Feb 25 14:44:24 toys su(pam_unix): [11439]: session opened for user root by chris(uid=500)
```

当您知道该寻找什么时，这其实非常简单。每条消息分为五个主要部分，从左到右依次为：

- 记录该消息的日期和时间
- 消息来源的计算机名称
- 消息所涉及的程序或服务名称
- 发送消息的程序的进程号（用方括号括起来）
- 消息的实际文本内容

让我们检查上面的文件片段。在前两行中，您可以看到我重新启动了网络。下一行显示我尝试从地址为 10.0.0.5 的计算机登录到此系统上的 FTP 服务器，使用名为 chris 的用户（我输入了错误的密码，身份验证失败）。最后一行显示我使用 su 命令成为 root 用户。

通过偶尔检查 messages 文件和 secure 文件，可以在破解尝试成功之前将其发现。如果您看到针对特定服务的连接尝试次数过多，尤其是来自互联网上的系统，您可能正遭受攻击。

> **CROSS REFERENCE:** 日志哨兵包提供了一种更简单的方式来管理日志文件并不会错过关键消息。请参阅本章后面的“使用 LogSentry 监控日志文件”。

## 使用 LogSentry 监控日志文件

Red Hat Linux 具有监控和记录计算机上几乎每项活动的的能力。在繁忙的系统上，会产生大量信息和错误消息并放置在日志文件中。对于管理员来说，监控日志文件的困难之处不在于检测或记录安全问题；困难之处在于记住检查日志文件并从所有被记录的内容中筛选出构成威胁的消息。本节描述如何使用 LogSentry 包监控日志文件。

LogSentry 包（以前称为 LogCheck）是一个方便的工具，可用于轻松管理系统日志文件。因为您更有可能浏览电子邮件而不是记住检查日志文件，所以 LogSentry 会将可能被忽视的信息呈现在您面前。

LogSentry 检查由标准 Linux syslog 设施产生的日志文件，尝试过滤掉不构成安全威胁的消息，然后对可能构成威胁的消息进行分类并通过电子邮件发送给系统管理员。默认情况下，LogSentry 会检查 /var/log 目录中 messages、secure 和 mail 日志文件中的消息。通过更改 LogSentry 配置文件，您可以更改 which

