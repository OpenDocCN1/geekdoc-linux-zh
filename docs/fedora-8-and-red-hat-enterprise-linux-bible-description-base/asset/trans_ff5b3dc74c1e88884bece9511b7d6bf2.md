
`syslogd` 守护进程甚至可以接受来自网络中其他计算机的消息。这特别有用，因为它允许你集中管理和审查网络上许多系统的日志文件。这种做法还具有重大的安全优势。如果网络中的某个系统遭到入侵，攻击者无法删除或修改日志文件，因为这些文件存储在一台单独的计算机上。

然而，务必记住的是，这些日志消息默认情况下并未加密。任何接入你局域网的人都可以窃听这些消息，因为它们在从一台机器传输到另一台机器时。此外，尽管攻击者可能无法更改旧的日志消息，但他可以影响系统，使得任何新的日志消息都不可信。

运行专用的日志主机（loghost）并不少见，这是一台除了记录网络中其他计算机的日志消息外没有其他用途的计算机。由于该系统不运行其他服务，因此被入侵的可能性较低。这使得攻击者几乎不可能抹去其痕迹。然而，这并不意味着在网络上的某台机器被入侵后，所有的日志消息都是准确的。

## 使用 syslogd 将日志重定向到日志主机

要将计算机的日志文件重定向到另一台计算机的 syslogd，你需要对本地 syslogd 的配置文件进行一些更改。你需要处理的文件是 /etc/syslog.conf。如果你还不是 root 用户，请先获取 root 权限，然后在文本编辑器（如 vi）中打开 /etc/syslog.conf 文件。你应该会看到类似以下内容的内容：

```
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
#kern.*                              /dev/console
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;news.none;authpriv.none;cron.none    /var/log/messages
# The authpriv file has restricted access.
authpriv.*                              /var/log/secure
# Log all the mail messages in one place.
mail.*                                  -/var/log/maillog
# Log cron stuff
cron.*                                  /var/log/cron
# Everybody gets emergency messages
*.emerg                                     * 
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

以 # 字符开头的行是注释。其他行包含两列信息，由空格或制表符分隔。左侧字段是分号分隔的消息类型和消息优先级列表。右侧字段是应写入这些消息的日志文件。

> **注意：** 注意 `/var/log/maillog` 文件前的短划线 (-)。通常，每个日志文件在每次记录后都会同步。如果日志文件完整路径前带有短划线，则表示该文件在每次记录后不会同步。虽然如果在日志写入前机器崩溃这可能会导致信息丢失，但如果你运行详细的日志记录，这可能会提高系统的性能。

要将消息发送到另一台计算机（日志主机）而不是文件，只需将日志文件名替换为 @ 字符后跟日志主机的名称即可。例如，要重定向通常发送到 `messages`、`secure` 和 `maillog` 日志文件的输出，请对上面的文件进行以下更改：

```
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;news.none;authpriv.none;cron.none @loghost

# The authpriv file has restricted access.
authpriv.* @loghost

# Log all the mail messages in one place.
mail.* @loghost
```

现在，消息将发送到名为 loghost 的计算机上运行的 `syslog`。名称 loghost 并非任意选择的。通常的做法是创建这样一个主机名，并将其设置为实际充当日志主机的系统的别名。这样，如果你将来需要切换日志主机职责到另一台机器，你只需更改 loghost 别名即可；无需在每台计算机上重新编辑 `syslog.conf` 文件。

## 理解 messages 日志文件

由于有许多程序和服务会向 messages 日志文件记录信息，理解该文件的格式非常重要。经常检查此文件通常能让你在系统出现问题之前获得良好的早期警告。文件中的每一行都是由某个程序或服务记录的单条消息。以下是实际 messages 日志文件的片段：

```
Feb 25 11:04:32 toys network: Bringing up loopback interface: succeeded
Feb 25 11:04:35 toys network: Bringing up interface eth0: succeeded
Feb 25 13:01:14 toys vafcpd(pam_unix)[10565]: authentication failure;
 logname=uid=0 euid=0 tty= ruser= rhost=10.0.0.5 user=chris
Feb 25 14:44:24 toys su(pam_unix)[11439]: session opened for user root by chris(uid=500)
```

当你知道要寻找什么时，这其实非常简单。每条消息分为五个主要部分。从左到右依次为：

- 记录消息的日期和时间
- 消息来源的计算机名称
- 消息相关的程序或服务名称
- 发送消息的程序的进程号（用方括号括起来）
- 实际的消息文本

让我们来看看上面的文件片段。在前两行中，你可以看到我重启了网络。下一行显示我尝试以名为 chris 的用户登录，从地址为 10.0.0.5 的计算机访问该系统的 FTP 服务器（我输入了错误的密码，认证失败）。最后一行显示我使用 su 命令变成了 root 用户。

通过偶尔审查 messages 文件和 secure 文件，可以在入侵尝试成功之前发现它。如果你看到针对特定服务的过多连接尝试，特别是如果它们来自互联网上的系统，你可能正在遭受攻击。

## 使用 logwatch 跟踪日志消息

跟踪日志文件内容的另一种方式是使用 logwatch 功能。Logwatch 会标记可能反映系统问题的消息，并每天通过电子邮件消息将它们转发给系统的 root 用户。安装 Fedora 或 RHEL 时，logwatch 软件包会安装并配置好以监视你的日志文件并向系统管理员报告可疑活动。基于 logwatch 的 cron 文件 (/etc/cron.daily/ilogwatch)，logwatch 功能将：

- 每天早晨 4:00 运行
- 根据配置文件 /etc/logwatch/conf/logwatch.conf 选择要扫描哪些日志文件以及电子邮件消息的发送位置。（默认值列在 /usr/share/logwatch/default.conf 中。）
- 向本地计算机的 root 用户发送电子邮件消息，报告基于日志文件内容可能存在的可疑活动。
- 报告可能反映系统问题的管理活动。

Logwatch 报告的信息类型包括已删除的用户和组、已安装或卸载的软件包以及消耗的磁盘空间。每日消息还显示通过 ssh 在网络上进行的登录活动以及文件传输活动。对于每个扫描的日志文件，失败消息都会被标记并报告。

审查 /usr/share/logwatch/default.conf/logwatch.conf 文件，以了解配置 logwatch 服务的选项。要更改任何选项，你可以将它们添加到 /etc/logwatch/conf/logwatch.conf 文件中。以下是一些 logwatch 设置的示例：

```
LogDir = /var/log
TmpDir = /var/cache/logwatch
MailTo = root
MailFrom = Logwatch
Print = No
Service = "-zz-network"       # Prevents execution of zz-network service, which
                              # prints useful network configuration info.
Service = "-zz-sys"           # Prevents execution of zz-sys service, which
                              # prints useful system configuration info.
Service = "-eximstats"        # Prevents execution of eximstats service, which
                              # is a wrapper for the eximstats program.
Range = yesterday
Detail = Low
Service = All
mailer = "sendmail -t"
```

LogDir 将日志文件目录设置为 /var/log（因此列出的任何日志文件都显示为相对于该目录）。/var/cache/logwatch 目录用于存储临时文件。每日电子邮件报告发送给本地系统的 root 用户（你可以将 MailTo 更改为任何有效的电子邮件地址），发件人 (MailFrom) 列为 Logwatch。你可以将 Print 值更改为 Yes，以便将报告发送到标准输出，而不是邮寄给 MailTo 收件人。Range 设置为 yesterday，这将使 logwatch 仅搜索过去一天的日志文件。你可以将 Range 更改为 All，以搜索特定日志文件的所有过去文件，例如 messages、messages.1、messages.2 等。为了增加详细信息量（默认设置为 Low），你可以将 Detail 标识为 Medium 或 High（或 0 到 10 之间的数字）。用于发送报告的邮件应用程序是 /bin/mail。

Logwatch 执行的大部分操作都基于 Service 条目的值。当 Service 设置为 All 时，/usr/share/logwatch/conf/services 目录中的所有文件都用于生成 logwatch 报告。此目录中的每个文件都与 logwatch 检查的服务相关，并定义了为该服务收集的信息类型。在你想要禁用的任何服务名称前加一个短划线 (-)。（默认情况下，zz-network、zz-sys 和 eximstats 被禁用。）

