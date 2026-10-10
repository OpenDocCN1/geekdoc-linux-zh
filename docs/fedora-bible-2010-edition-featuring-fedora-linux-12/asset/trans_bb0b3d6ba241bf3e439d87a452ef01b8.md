

这些消息现在将被发送到运行在名为 loghost 的计算机上的 `rsyslogd` 上。loghost 这个名称并非随意选择。惯例是创建这样的主机名，并将其设置为实际充当 loghost 的系统的别名。这样，如果你需要将 loghost 的职责切换到另一台机器，你只需更改 loghost 别名即可，而无需重新编辑每台计算机上的 `rsyslog.conf` 文件。

> **注意：** 你可能需要编辑 loghost 上的 iptables 规则，以允许端口 514 的入站数据包，这是 `rsyslogd` 的默认端口号。

## 理解 messages 日志文件

由于许多程序和服务都会将信息记录到 messages 日志文件中，因此理解该文件的格式非常重要。经常检查该文件可以为你系统出现问题的早期迹象提供良好的预警。文件中的每一行都是由某个程序或服务记录的一条消息。以下是实际 messages 日志文件的一个片段：

```
Feb 25 11:04:32 toys network: Bringing up loopback interface: succeeded
Feb 25 11:04:35 toys network: Bringing up interface eth0: succeeded
Feb 25 13:01:14 toys vsftpd(pam_unix)[10565]: authentication failure;
	logname= uid=0 euid=0 tty= ruser= rhost=10.0.0.5 user=chris
Feb 25 14:44:24 toys su(pam_unix)[11439]: session opened for
user root by chris(uid=500)
```

如果你知道该看什么，这其实非常简单。每条消息分为五个主要部分。从左到右依次为：

- 消息记录时的日期和时间
- 消息来源计算机的名称
- 消息相关的程序或服务的名称
- 发送消息的程序的进程号（包含在方括号内）
- 实际的文本消息本身

让我们检查一下之前的文件片段。在前两行中，你可以看到我重启了网络。下一行显示我尝试以名为 chris 的用户身份登录，以从此系统的 FTP 服务器，从地址为 10.0.0.5 的计算机进行连接（我输入了错误的密码，身份验证失败）。最后一行显示我使用 `su` 命令切换为 root 用户。

通过偶尔检查 messages 文件和 secure 文件，可以在破解尝试成功之前发现它。如果你看到针对特定服务的连接尝试次数过多，特别是如果这些尝试来自互联网上的系统，你可能正在遭受攻击。

## 使用 logwatch 跟踪日志消息

另一种跟踪日志文件内容的方法是借助 logwatch 功能。Logwatch 标记可能反映系统问题的消息，并每天通过电子邮件消息将它们转发到系统的 root 用户。如果未安装 logwatch，请运行 `yum install logwatch` 命令。基于 logwatch 的 cron 文件（`/etc/cron.daily/01ogwatch`），logwatch 功能将执行以下操作：

- 每天早上 4:00 运行
- 根据配置文件 `/etc/logwatch/conf/logwatch.conf` 选择要扫描的日志文件以及发送电子邮件消息的位置。（默认值列在 `/usr/share/logwatch/default.conf` 中。）
- 基于日志文件的内容，向本地计算机的 root 用户发送电子邮件消息，报告系统中可能存在的可疑活动。
- 报告可能反映系统问题的管理活动。

logwatch 报告的信息类型包括已删除的用户和组、已安装或卸载的软件包以及消耗的磁盘空间。每日消息还显示了通过网络进行 SSH 的登录活动和文件传输活动。每个被扫描的日志文件的失败消息都会被标记并报告。

审查 `/usr/share/logwatch/default.conf/logwatch.conf` 文件以查看配置 logwatch 服务时可用的选项。若要更改任何选项，可以将它们添加到 `/etc/logwatch/conf/logwatch.conf` 文件中。以下是一些 logwatch 设置的示例：

```
LogDir = /var/log
TmpDir = /var/cache/logwatch
MailTo = root
MailFrom = Logwatch
Print = No
Service = "-zz-network" # Prevents execution of zz-network service, which
# prints useful network configuration info.
Service = "-zz-sys" # Prevents execution of zz-sys service, which
# prints useful system configuration info.
Service = "-eximstats" # Prevents execution of eximstats service, which
# is a wrapper for the eximstats program.
Range = yesterday
Detail = Low
Service = All
Mailer = "sendmail -t"
```

`LogDir` 将日志文件目录设置为 `/var/log`（因此列出的任何日志文件都显示为该目录的相对路径）。`/var/cache/logwatch` 目录用于保存临时文件。每日电子邮件报告发送到本地系统的 root 用户（你可以将 `MailTo` 更改为任何有效的电子邮件地址），发件人（`MailFrom`）显示为 `Logwatch`。你可以将 `Print` 值更改为 `Yes`，以便将报告发送到标准输出，而不是通过邮件发送给 `MailTo` 收件人。`Range` 设置为昨天，这会使 logwatch 仅搜索过去一天的日志文件。你可以将 `Range` 更改为 `All`，以搜索特定日志文件（如 `messages`、`messages.1`、`messages.2` 等）所有可用的过去文件。要增加详细信息量（默认为 Low），可以将 Detail 标识为 Medium 或 High（或 0 到 10 之间的数字）。

logwatch 发生的大部分操作基于 *Service* 条目的值。当 *Service* 设置为 *All* 时，*​/usr/share/logwatch/conf/services* 目录中的所有文件都用于生成 logwatch 报告。该目录中的每个文件都与 logwatch 检查的服务相关，并定义为该服务收集的信息类型。在你想禁用的任何服务名称前加一个破折号（-）。（默认情况下，*zz-network*、*zz-sys* 和 *eximstats* 是禁用的。）

## 使用 Secure Shell 软件包

Secure Shell 软件包（SSH）提供与其他远程执行、远程复制和远程登录命令（如旧的 UNIX *rsh*、*rcp* 和 *rlogin* 命令）类似的 shell 服务，但会对网络流量进行加密。它使用非对称加密，因此非常适合用于连接互联网的计算机。Fedora 发行版包含以下用于 SSH 的客户端和服务器软件包：*openssh*、*openssh-clients* 和 *openssh-server* 软件包。

### 启动 SSH 服务

如果你已安装 *openssh-server* 软件包，SSH 服务器会自动配置为启动。SSH 守护进程从 */etc/init.d/sshd* 启动脚本中启动。为确保该服务设置为自动启动，请以 root 用户身份输入以下内容：

```
$ chconfig --list sshd
sshd        0:off    1:off    2:on    3:on    4:on    5:on    6:off
```

这表明 *sshd* 服务被设置为在系统状态 2、3、4 和 5（正常启动状态）下运行，并在所有其他状态下设置为关闭。如果默认的运行状态下 SSH 服务处于关闭状态，你可以通过以 root 用户身份输入以下内容来开启它：

```
$ chconfig sshd on
```

这一行会在你进入运行级别 2、3、4 或 5 时开启 SSH 服务。若要立即启动该服务，请输入以下内容：

```
$ /etc/init.d/sshd start
```

> **提示：** 如果你无法从另一台计算机连接到 *sshd* 服务，请检查防火墙是否已在服务器上开放，以允许访问端口 22。这是 *sshd* 监听请求的默认端口。如果你更改 *sshd* 服务以监听非标准端口，然后在防火墙中打开该端口，安全性将会更高，因为攻击者会针对默认端口。

### 使用 ssh、sftp 和 scp 命令

你可以使用 SSH 服务的三个命令是 *ssh*、*sftp* 和 *scp*。远程用户使用 *ssh* 命令安全地登录到你的系统。*scp* 命令允许远程用户将文件复制到系统或从系统复制文件。*sftp* 命令提供了一种访问 FTP 站点的安全方式。

