
> 虽然 `Telnet` 作为一个配合 `xinetd` 的便捷示例，但由于安全顾虑，你不应该运行 `Telnet` 服务。请改为启用 `ssh` 进行远程登录。有关 `ssh` 的更多信息，请参阅后面关于使用 `secure shell` 包的章节。

如果 `Jukebox` 使用 `CUPS-lpd` 协议连接到你的机器呢？在这种情况下，它不匹配 `hosts.allow` 中的任何规则；唯一提到 `lpd` 守护进程的那一行并未提到 `199.170.177` 子网或 `linuxtoys.net` 域名。`xinetd` 继续检查 `hosts.deny` 文件。条目 `ALL: ALL` 匹配任何内容，因此 `tcpd` 拒绝该连接。

`hosts.allow` 文件中也使用了 `ALL` 通配符。在这种情况下，我们告诉 `xinetd` 允许绝对任何主机连接到 Linux 机器上的 `FTP` 服务。这对于运行任何人（互联网上的任何人）都可以访问的匿名 `FTP` 服务器来说是合适的。如果你没有运行匿名 `FTP` 站点，可能不应该使用 `ALL` 标志。

一条好的经验法则是让 `hosts.allow` 和 `hosts.deny` 文件尽可能具有限制性，然后仅显式启用你真正需要的服务。此外，仅向确实需要访问权限的系统授予访问权限。使用 `ALL` 标志来授予对特定服务的通用访问权限。

配置服务可能比输入长长的子网或域名列表更简单，但在网络安全措施上花几分钟总比花数小时恢复入侵后损失要强。

> 你可以使用 `/etc/xinetd.conf` 文件中的各种选项进一步限制对服务的访问，甚至可以将对特定服务的访问限制在一天中的特定时间段。在命令提示符下输入 `man xinetd` 阅读 `xinetd` 的手册页，以了解有关这些选项的更多信息。

###### 检查日志文件

为你的系统应对黑客攻击做好预防工作只是战斗的一部分。你还必须在攻击发生时识别它。理解 `CentOS` 记录重要事件的各个日志文件对于实现这一目标至关重要。你的 `CentOS` 系统的日志文件可以在 `/var/log` 目录中找到。

由于系统日志是纯文本文件，你可以使用任何文本编辑器或分页命令（如 `less` 或 `more`）直接查看日志内容。`CentOS` 自带的 `logwatch` 设施会通过电子邮件向 `root` 用户发送日志文件的每日摘要。你还可以添加诸如 `logsentry` 等软件包来监控你的日志文件。

###### 替换 `syslogd` 软件包

`CentOS` 的默认日志服务是 `syslogd`。然而，较新的 `rsyslogd` 比其前身更灵活、更强大。建议你安装并使用 `rsyslogd`，并卸载 `syslogd`。你可以以 `root` 用户身份在终端窗口中执行此操作。

```bash
# yum install rsyslog && yum remove syslogd
```

`&&` 非常重要，因为如果没有 `syslog` 替代品而移除 `syslogd` 软件包，将移除你的大部分系统！

在使用 `yum` 安装 `rsyslog` 软件包后，你需要使用 `chkconfig` 启用它并启动该服务。

```bash
# service rsyslog start
# chkconfig rsyslog on
```

###### 理解 `rsyslogd` 服务

`/var/log` 目录中的大多数文件由 `rsyslogd` 服务维护。`rsyslogd` 守护进程是系统日志守护进程，充当先前名为 `syslogd` 的日志系统的扩展。它接受来自各种其他程序的日志消息，并将其写入适当的日志文件。这比让每个程序直接写入其自己的日志文件要好，因为它允许你集中管理日志文件的处理方式。可以配置 `rsyslogd` 在日志文件中记录不同详细程度。可以指示它忽略除最关键消息以外的所有内容，或者记录每一个细节。

`rsyslogd` 守护进程甚至可以接受来自网络中其他计算机的消息。这特别有用，因为它使你可以集中管理和审查网络上许多系统的日志文件。这种做法还有重大的安全益处。如果网络中的某个系统遭到入侵，黑客无法删除或修改日志文件，因为这些文件存储在另一台计算机上。

但是，重要的是要记住，这些日志消息默认情况下是未加密的。任何嗅探你局域网的人都能窃听这些消息在机器间传输的过程。此外，虽然黑客可能无法更改旧的日志消息，但她可以影响系统，使得任何新的日志消息都不应被信任。

运行专用的日志主机（`loghost`）并不少见，这是一种除了记录网络上其他计算机的日志消息外没有其他用途的计算机。由于该系统不运行其他服务，它被入侵的可能性较小。这使得黑客几乎不可能抹去她的痕迹。然而，这并不意味着在黑客入侵网络中的机器后，所有日志消息都是准确的。

###### 使用 `rsyslogd` 将日志重定向到日志主机

要将计算机的日志文件重定向到另一台计算机的 `rsyslogd`，你必须对本地 `rsyslogd` 的配置文件进行一些更改。你需要处理的文件是 `/etc/rsyslog.conf`。如果你还不是 `root`，请成为 `root`，然后在文本编辑器（如 `vi`）中打开 `/etc/rsyslog.conf` 文件。你应该看到类似以下内容：

```text
# Log all kernel messages to the console. # Logging much else clutters up the screen. #kern.* /dev/console
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none;cron.none /var/log/messages
# The authpriv file has restricted access.
authpriv.* /var/log/secure
# Log all the mail messages in one place.
mail.* -/var/log/maillog
# Log cron stuff
cron.* /var/log/cron
# Everybody gets emergency messages
*.emerg *
# Save news errors of level crit and higher in a special file.
uucp,news.crit		/var/log/spooler
# Save boot messages also to boot.log
local7.*			/var/log/boot.log
```

以 `#` 字符开头的行是注释。其他行包含两列信息，由空格或制表符分隔。左侧字段是用分号分隔的消息类型和消息优先级列表。右侧字段是应写入这些消息的日志文件。

> **注意** 注意 `/var/log/maillog` 文件前的破折号（`-`）。通常，每次记录后每个日志文件都会同步。日志文件完整路径前的破折号表示文件在每次记录后不同步。如果你的机器在日志写入前崩溃，这可能导致信息丢失，但如果你运行详细日志记录，它可以提高系统的性能。

要将消息发送到另一台计算机（日志主机）而不是文件，只需将日志文件名替换为 `@` 字符后跟日志主机的名称。例如，要将通常发送到 `messages`、`secure` 和 `maillog` 日志文件的输出重定向，请对之前的文件进行以下更改：

```text
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none:cron.none		@loghost

# The authpriv file has restricted access.
authpriv.*			@loghost

# Log all the mail messages in one place.
mail.*			@loghost
```

现在消息将发送到名为 `loghost` 的计算机上运行的 `rsyslogd`。`loghost` 的名称并非随意选择。通常的做法是创建这样一个主机名，并将其设置为实际充当日志主机的系统的别名。这样，如果你以后需要将日志主机职责切换到另一台机器，你只需更改 `loghost` 别名；无需重新编辑每台计算机上的 `rsyslog.conf` 文件。

###### 理解 `messages` 日志文件

由于许多程序和服务将信息记录到 `messages` 日志文件中，理解该文件的格式非常重要。检查此文件通常能为你提供系统正在出现问题的好早期预警。文件中的每一行都是某个程序或服务记录的一条消息。以下是实际 `messages` 日志文件的片段：

```text
Feb 25 11:04:32 toys network: Bringing up loopback interface: succeeded
Feb 25 11:04:35 toys network: Bringing up interface eth0: succeeded
Feb 25 13:01:14 toys vsftpd[pam_unix] [10565]: authentication failure;
logname= uid=0 euid=0 tty= user= root= 10.0.0.5 user=chris
Feb 25 14:44:24 toys su(pam_unix) [11439]: session opened for user root by chris (uid= 500)
```

当你知道要找什么时，这真的非常简单。每条消息分为五个主要部分。从左到右它们是：

- 消息记录时的日期和时间
- 消息来源计算机的名称
- 消息所属的程序或服务名称
- 发送消息的程序的进程号（用方括号括起来）
- 实际的文本消息本身

让我们查看前面的文件片段。在前两行中，你可以看到我重启了网络。下一行显示我尝试以 `chris` 用户身份从地址为 `10.0.0.5` 的计算机登录此系统上的 `FTP` 服务器。（我输入了错误的密码，认证失败。）最后一行显示我使用 `su` 命令变成了 `root` 用户。

通过偶尔审查 `messages` 文件和 `secure` 文件，可以在破解尝试成功之前捕获它。如果你看到对特定服务的连接尝试数量过多，尤其是如果它们来自 Internet 上的系统，你可能正受到攻击。

###### 使用 `logwatch` 跟踪日志消息

跟踪日志文件内容的另一种方法是使用 `logwatch` 设施。`logwatch` 标记可能反映系统问题的消息，并每天通过电子邮件消息将它们转发给你系统的 `root` 用户。安装 `CentOS` 时，`logwatch` 软件包已安装并配置为监视你的日志文件并向系统管理员报告可疑活动。基于 `logwatch` 的 `cron` 文件（`/etc/cron.daily/ilogwatch`），`logwatch` 设施将：

- 每天早上 4:00 运行。
- 根据配置文件 `/etc/logwatch/conf/logwatch.conf` 选择要扫描哪些日志文件以及将电子邮件消息发送到哪里。（默认值列在 `/usr/share/logwatch/default.conf` 中）
- 向本地计算机的 `root` 用户发送电子邮件消息，基于日志文件内容报告系统上可能存在的可疑活动。
- 报告可能反映系统问题的管理活动。

`logwatch` 报告的信息类型包括已删除的用户和组、已安装或卸载的软件包以及消耗的磁盘空间。每日消息还显示通过 `ssh` 的网络登录活动和文件传输活动。每个扫描的日志文件都会标记并报告失败消息。

###### 第三部分 管理

查看 `/usr/share/logwatch/default.conf/logwatch.conf` 文件以了解配置 `logwatch` 服务的选项。若要更改任何选项，可以将它们添加到 `/etc/logwatch/conf/logwatch.conf` 文件中。以下是一些 `logwatch` 设置示例。

```text
LogDir = /var/log
TmpDir = /var/cache/logwatch
MailTo = root
MailFrom = Logwatch
Print = No
Service = "-zz-network" # Prevents execution of zz-network service, which
###### prints useful network configuration info.
Service = "-zz-sys" # Prevents execution of zz-sys service, which
###### prints useful system configuration info.
Service = "-eximstats" # Prevents execution of eximstats service, which
###### is a wrapper for the eximstats program.
Range = yesterday
Detail = Low
Service = All
mailer = "sendmail -t"
```

`LogDir` 将日志文件目录设置为 `/var/log`（因此，列出的任何日志文件都相对于该目录显示）。`/var/cache/logwatch` 目录用于存储临时文件。每日电子邮件报告发送给本地系统的 `root` 用户（你可以将 `MailTo` 更改为任何有效的电子邮件地址），发件人（`MailFrom`）显示为 `Logwatch`。你可以将 `Print` 值更改为 `Yes`，以便将报告发送到标准输出，而不是通过电子邮件发送给 `MailTo` 收件人。`Range` 设置为 `yesterday`（昨天），这将导致 `logwatch` 仅搜索过去一天的日志文件。你可以将 `Range` 更改为 `All`（全部），以搜索特定日志文件的所有可用历史文件，例如 `messages`、`messages.1`、`messages.2` 等。要增加详情程度（默认设置为 `Low`），可以将 `Detail` 标识为 `Medium`（中）或 `High`（高）（或 0 到 10 之间的数字）。用于发送报告的邮件应用程序是 `sendmail`。

`logwatch` 执行的大多数操作都基于 `Service` 条目的值。当 `Service` 设置为 `All` 时，`/usr/share/logwatch/conf/services` 目录中的所有文件都用于生成 `logwatch` 报告。该目录中的每个文件都与 `logwatch` 检查的服务相关联，并定义了为该服务收集的信息类型。在你想要禁用的任何服务名称前加一个连字符（`-`）。（默认情况下，`zz-network`、`zz-sys` 和 `eximstats` 被禁用。）

###### 使用 `Secure Shell` 软件包

`Secure Shell` 软件包（`SSH`）提供与其他远程执行、远程复制和远程登录命令（如旧式 `UNIX` `rsh`、`rcp` 和 `rlogin` 命令）相似的 shell 服务，但会对网络流量进行加密。它使用私钥密码学，因此非常适合用于连接互联网的计算设备。`CentOS` 包含用于 `SSH` 的以下客户端和服务器软件包：`openssh`、`openssh-clients` 和 `openssh-server`。

###### 启动 `SSH` 服务

如果你已安装 `openssh-server` 软件包，`SSH` 服务器会自动配置为启动。`SSH` 守护程序由启动脚本 `/etc/init.d/sshd` 启动。要确保设置为自动启动服务，请以 `root` 用户身份输入以下内容：

```bash
# chkconfig --list sshd
sshd          0:off   1:off   2:on    3:on    4:on    5:on    6:off
```

这显示 `sshd` 服务被设置为在系统状态 2、3、4 和 5（正常引导状态）中运行，并在所有其他状态下关闭。如果你的默认运行状态下 `SSH` 服务是关闭的，你以 `root` 用户身份输入以下内容即可将其打开：

```bash
# chkconfig sshd on
```

这行命令在你进入运行级别 2、3、4 或 5 时开启 `SSH` 服务。若要立即启动服务，请输入以下内容：

```bash
# /etc/init.d/sshd start
```

> **注意** 如果你无法从另一台计算机连接到 `sshd` 服务，请检查防火墙是否已开放以允许访问 `tcp` 端口 22。这是 `sshd` 监听请求的默认端口。

###### 使用 `ssh`、`sftp` 和 `scp` 命令

你可以使用 `SSH` 服务的三个命令是 `ssh`、`sftp` 和 `scp`。远程用户使用 `ssh` 命令安全地登录到你的系统。`scp` 命令允许远程用户在系统之间复制文件。`sftp` 命令提供了访问安全 `SFTP` 站点的安全方式。

与普通的远程 shell 服务一样，`secure shell` 会在 `/etc/hosts` equiv 文件和用户的 `.rhost` 文件中查找，以确定是否允许连接。它还会在 `SSH` 专用文件 `/etc/hosts.equiv` 和 `.shosts` 中查找。使用 `shosts.equiv` 和 `.shosts` 文件更可取，因为它避免了对非加密远程 shell 服务的访问权限。`/etc/ssh/shosts.equiv` 和 `.shosts` 文件在功能上与传统 `hosts.equiv` 和 `.rhosts` 文件等效，因此相同的说明和规则适用。（输入 `man hosts.equiv` 以获取更多信息。）

现在你已准备好测试 `SSH` 服务。从另一台已安装 `SSH` 的计算机（或者如果另一台计算机不可用，甚至可以从同一台计算机）输入 `ssh` 命令，后跟一个空格和你要连接的系统名称。例如，若要连接到系统 `ratbert.glaci.com`，请输入：

```bash
$ ssh ratbert.glaci.com
```
