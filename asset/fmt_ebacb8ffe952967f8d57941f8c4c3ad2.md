
Feb 25 11:04:35 toys network: Bringing up interface eth0: succeeded

Feb 25 11:03:14 toys vsftpd(pam_unix) [10565]: authentication failure;
logname= uid=0 eid=0 rhost=10.0.0.5 user=chris

Feb 25 14:44:22 toys su(pam_unix) [11439]: session opened for
user root by chris (uid=500)

当你知道要看什么时，这其实非常简单。每条消息分为五个主要部分。从左到右它们分别是：

- 记录消息的日期和时间
- 消息来源的名称
- 消息所属程序或服务名称
- 发送消息的程序的进程号（括号内）
- 消息文本本身

通过偶尔查看 `messages` 文件和 `secure` 文件，有可能在破解尝试成功之前将其发现。如果你看到某个服务的连接尝试过多，特别是当这些尝试来自互联网上的系统时，你可能正受到攻击。

## 使用 logwatch 跟踪日志消息

跟踪日志文件内容的另一种方法是使用 `logwatch` 设施。`logwatch` 会标记可能反映系统问题的消息，并每天通过电子邮件转发给你系统的 `root` 用户。当你安装 Fedora 或 RHEL 时，会安装并配置 `logwatch` 包，以监控你的日志文件并向你的系统管理员报告可疑活动。根据 `logwatch` cron 文件 `/etc/cron.daily/logwatch`，`logwatch` 设施将：

- 每天早晨 4:00 运行。
- 根据配置文件 `/etc/logwatch/conf/logwatch.conf` 选择保存哪些日志文件以及将电子邮件发送到哪里。（默认值在 `/usr/share/logwatch/default.conf` 中。）
- 根据日志文件的内容，向本地计算机的 `root` 用户发送电子邮件消息，报告你系统中潜在的可疑活动。
- 报告可能反映系统问题的管理活动。

`logwatch` 报告的信息类型包括已删除的用户和组、安装或卸载的包以及占用的磁盘空间。每日消息还显示了通过网络进行 `ssh` 连接和文件传输的日志活动。对于扫描的每个日志文件，失败消息都会被标记并报告。

查看 `/usr/share/logwatch/default.conf/logwatch.conf` 文件以查看配置 `logwatch` 选项。要更改选项，你可以将它们添加到 `/etc/logwatch/conf/logwatch.conf` 文件中。以下是 `logwatch` 设置示例：

```
LogDir = /var/log
TmpDir = /var/tmp/logwatch
MailTo = root
Print = Yes
```

## 第三部分：管理 Fedora RHEL

```
uucp,news.crit /var/log/spooler
```

```
# 将启动消息也保存到 boot.log
local7.* /var/log/boot.log
#
# INN
#
news=.crit /var/log/news/news.crit
news=.err /var/log/news/news.err
news=.notice /var/log/news/news.notice
```

以 `#` 字符开头的行是注释。其他行包含两列信息，用空格或制表符分隔。左侧字段是用分号分隔的消息类型和优先级列表。右侧字段是应将这些消息写入的日志文件。

> 注意：注意 `/var/log/mayillog` 文件前的横杠 `-`。通常情况下，每个日志文件在每次记录后都会同步。位于日志文件完整路径前的横杠表示该文件在每次记录后不会进行同步。如果你的机器在写入日志之前崩溃，这可能会导致信息丢失；但如果你运行详细日志，这可以获得更好的性能。

若要将消息发送到另一台计算机（日志主机 `loghost`）而不是文件，只需将日志文件名替换为 `@` 符号后跟日志主机的名称。例如，重定向通常发送到 `messages`、`secure` 和 `mayillog` 日志文件的输出，请对前面的文件进行更改：

- `# 记录级别为 info 或更高的任何内容（邮件除外）。`
- `# 不要记录私有的身份验证消息！`
`*.info;mail.none;news.none;authpriv.none;cron.none @loghost`

- `# authpriv 文件受限制访问。`
`authpriv.* @loghost`

- `# 将所有邮件消息记录在一个处。`
`mail.* @loghost`

现在，消息将发送到在名为 `loghost` 的计算机上运行的 `syslog`。`loghost` 并不是随机选择。惯例是创建一个这样的主机名，并创建一个指向作为日志主机的实际系统的别名。这样，如果你需要将日志主机职责切换到另一台机器，你只需要更改 `loghost` 别名；不需要在每台计算机上重新编辑 `syslog.conf` 文件。

## 理解消息日志文件

由于有许多程序和服务都会向 `messages` 日志文件记录信息，因此理解此文件的格式非常重要。检查此文件通常可以让你对系统中正在出现的问题提供良好的早期警报。文件中的每行都是某个程序或服务记录的消息。以下是实际 `messages` 日志文件的一个片段：

```
Feb 25 11:04:32 toys network: Bringing up loopback interface: succeeded
Feb 25 11:04:35 toys network: Bringing up interface eth0: succeeded
Feb 25 11:03:14 toys vsftpd(pam_unix) [10565]: authentication failure;
logname= uid=0 eid=0 rhost=10.0.0.5 user=chris
Feb 25 14:44:22 toys su(pam_unix) [11439]: session opened for
user root by chris (uid=500)
```

当你知道要看什么时，这其实非常简单。每条消息分为五个主要部分。从左到右它们分别是：

- 记录消息的日期和时间
- 消息来源的名称
- 消息所属程序或服务名称
- 发送消息的程序的进程号（括号内）
- 消息文本本身

通过偶尔查看 `messages` 文件和 `secure` 文件，有可能在破解尝试成功之前将其发现。如果你看到某个服务的连接尝试过多，特别是当这些尝试来自互联网上的系统时，你可能正受到攻击。

## 使用 logwatch 跟踪日志消息

跟踪日志文件内容的另一种方法是使用 `logwatch` 设施。`logwatch` 会标记可能反映系统问题的消息，并每天通过电子邮件转发给你系统的 `root` 用户。当你安装 Fedora 或 RHEL 时，会安装并配置 `logwatch` 包，以监控你的日志文件并向你的系统管理员报告可疑活动。根据 `logwatch` cron 文件 `/etc/cron.daily/logwatch`，`logwatch` 设施将：

- 每天早晨 4:00 运行。
- 根据配置文件 `/etc/logwatch/conf/logwatch.conf` 选择保存哪些日志文件以及将电子邮件发送到哪里。（默认值在 `/usr/share/logwatch/default.conf` 中。）
- 根据日志文件的内容，向本地计算机的 `root` 用户发送电子邮件消息，报告你系统中潜在的可疑活动。
- 报告可能反映系统问题的管理活动。

`logwatch` 报告的信息类型包括已删除的用户和组、安装或卸载的包以及占用的磁盘空间。每日消息还显示了通过网络进行 `ssh` 连接和文件传输的日志活动。对于扫描的每个日志文件，失败消息都会被标记并报告。

查看 `/usr/share/logwatch/default.conf/logwatch.conf` 文件以查看配置 `logwatch` 选项。要更改选项，你可以将它们添加到 `/etc/logwatch/conf/logwatch.conf` 文件中。以下是 `logwatch` 设置示例：

```
LogDir = /var/log
TmpDir = /var/tmp/logwatch
MailTo = root
Print = Yes
```

## 第三部分：管理 Fedora RHEL

在后面输入一个空格和你要连接的系统名称。例如，要连接到系统 `rabtert.glaci.com`，请输入：

```
$ ssh rabtert.glaci.com
```

如果你是第一次使用 `ssh` 命令登录到该系统，它会要求你确认是否要连接。当出现以下提示时，输入 `yes` 并按回车：
