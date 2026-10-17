
$ActionDefaultTemplate RSYSLOGFormat

# 文件同步默认禁用。

`$ActionFileEnable on`

#### RULES ####

# 将内核日志到控制台。

`/kern.* /dev/console`

# 记录任何（邮件之外的）info 或更高级别的信息。

`*.info;mail.none;authpriv.none;cron.none /var/log/messages`

# authpriv 文件有限制的访问。

`authpriv.* /var/log/secure`

# 将所有邮件消息放在一个地方。

`mail.* -/var/log/mail`

# 记录 cron 任务

`cron.* /var/log/cron`

# 所有人接收紧急消息

`*.emerg *`

# 将 crit 级及以上的严重错误保存在特殊文件中。

`news.crit /var/log/news`

# 将启动消息也保存到 boot.log

`local7.* /var/log/boot`

### begin forwarding ###

# begin ... end 之间的语句定义了一个单一的转发

# 规则。它们是一个整体，不要拆分。如果你创建了多个

# 规则，请复制！

# 远程日志（使用 TCP 用于可靠交付）

#创建一个磁盘队列。如果远程主机

# 宕，消息将缓冲到 /syslog并在恢复后发送。

#WorkDirectory /var/syslog # 缓冲文件的位置

#ActionQueueFileName frulet # 缓冲文件的唯一前缀

#ActionQueueMaxFileSize 0列表（尽可能使用）

#ActionQueueSaveShutdown on 关机时保存消息到磁盘

#ActionQueueType LinkedList # 异步运行

#ActionResumeRetryCount -1 宕机时无限重试

# 远程主机是：端口，例如 192.168.0.1:514，端口选项

#.* @remote-host:514

### end of the forwarding rule ###

以 `#` 字符开头的行是注释。其他行包含列，用空格或制表符分隔。左字段是用分号分隔的消息类型和优先级列表。右字段是应写入这些消息的日志文件。

最有趣的部分从 RULES 部分开始。

> 注意：注意 `/var/log/mail` 前的横杠（）。通常，每个日志文件在每次记录后都会同步。日志路径前的横杠表示文件在每次记录后不同步。虽然这在机器在写入日志之前崩溃可能会导致信息丢失，但在运行详细日志时可以提高系统的性能。

## 第三部分：管理 Fedora 和 RHEL

要将消息发送到另一台计算机（loghost）而不是文件，只需将日志文件名替换为 `@` 符号，后跟 loghost 的名称即可。例如，要重定向通常发送到 messages、`secure、`mailog` 日志的输出，请对之前的文件进行以下更改：

```
# 记录级别为 info 或更高的任何内容（邮件外）。
# 不要记录私有的认证消息：
*.info.mail:node;news.node:authpriv.node;cron.none @loghost

# authpriv 文件有访问限制。
authpriv.* @loghost

# 将所有邮件消息记录在某处。
mail.* @loghost
```

现在，消息将发送到在名为 loghost 的计算机上的 rsyslog。loghost 这个名字并不是随机选择的。通常会创建一个主机名并使其充当 loghost 的别名。这样，如果你需要将 loghost 职责切换到不同的机器，只需更改 loghost 别名；而无需在每台计算机上重新编辑 `rsyslog.conf` 文件。

## 检查 messages 日志文件

由于有许多程序和服务向 messages 日志记录信息，因此理解此文件的格式至关重要。此示例通常能让你尽早发现系统中正在出现的问题。日志中的每一行都是某些程序或服务记录的一条消息。以下是实际 messages 日志文件的片段：

```
Feb 25 11:04:32 toys: Bringing up loopback interface: succeeded

Feb 25 11:04:35 toys: Bringing up interface eth0: succeeded

Feb 25 13:01:14 toys: vsftpd(pam_unix) [10565]: authentication failure:

Feb 25 14:44:24 toys: su(pam_unix) [11439]: session opened for

user root by uid=0 tty=0 host=10.0.0.5 user-chris
```

只要知道要看什么，这其实非常简单。每条消息被分为五个主要部分。从左到右它们是：

- 记录消息的日期和时间
- 消息来源计算机的名称
- 消息所属程序或服务名称
- 发送消息程序的进程号（位于方括号内）
- 实际文本本身

让我们检查之前的片段。在前两行中，你可以看到我重启了网络。下一行显示我尝试以用户 chris 的身份登录，从地址为 10.0.0.5 的计算机访问该系统的 FTP 服务器（我输入了错误的密码且认证失败）。最后一行显示我使用了 `su` 命令切换到 root 用户。

偶尔检查 `messages` 文件和 `secure` 文件，可能在攻击成功之前捕获破解尝试。如果你发现某个特定服务有大量的连接尝试，特别是当这些尝试来自网络上的其他系统时，你可能正受到攻击。

## 使用 logwatch 跟踪日志消息

跟踪日志文件内容的另一种方法是使用 logwatchset。logwatch 会标记可能反映系统问题的标志，并每天通过电子邮件发送给系统的 root 用户。当你安装 Fedora 或 RHEL 时，系统会安装并配置 logwatch 包，以监控你的日志并向管理员报告可疑活动。根据 logwatch cron 文件 (`/etc/cron.daily/0logwatch`)，logwatchset：

- 每天早上 4:00 运行。
- 根据配置文件 `/etc/logwatch/conf/logwatch.conf` 选择扫描哪些日志文件并发送电子邮件（默认值列在 `/usr/share/logwatch/default.conf` 中）。
- 根据你日志文件的内容，向本地计算机的 root 用户发送电子邮件，报告你系统中潜在的可疑活动。
- 报告可能反映系统问题的管理活动。

logwatch 报告的信息类型包括被删除的用户和用户组、安装或卸载的包以及消耗的磁盘空间。每日消息还显示通过 ssh 网络和文件传输进行的日志活动。每个日志文件的失败消息都会被标记并报告。

检查 `/usr/share/logwatch/default.conf` 日志文件以查看配置 logwatch 服务的选项。要更改任何选项，可以将其添加到 `/etc/logwatch/conf/logwatch.conf` 文件中。以下是日志设置的示例：

| LogDir = /var/log |
| TmpDir = /var/cache/logwatch |
| MailTo = root |
| MailFrom = Logwatch |
| Print = No |
| Service = "-zz-network" # 防止执行 zz-network 服务，该服务会打印常用的网络配置信息。 |
| Service = "-zz-sys" # 防止执行 zz-sys 服务，该服务会打印常用的系统配置信息。 |
| Service = "-eximstats" # 防止执行 eximstats 服务，该服务会打印常用的系统配置信息。 |

（注：此处由于原文开始出现大量重复和乱码，以下内容已根据逻辑进行处理）

## 使用 Secure Shell 包

Secure Shell (SSH) 提供了类似于远程执行、远程复制和远程登录的服务（类似于旧的 UNIX rsh、scp 和 login 命令），它会加密网络流量。它使用私钥加密，因此非常适合连接互联网的计算机。Fedora 和 RHEL 发行版包含以下 SSH 客户端和服务包：`openssh`、`openssh-clients` 和 `openssh-server`。

## 启动 SSH 服务

如果你安装了 `openssh-server` 包，SSH 服务将自动配置为启动。SSH 守护进程从 `/etc/init.d/sshd` 脚本启动。要确保服务自动启动，请执行以下命令（作为 root 用户）：

```
# chkconfig --list ssh

sshd 0:off 1:off 2:on 3:on 4:on 5:off 6:off
```

这显示 sshd 服务设置为在状态 2、3、4 下运行。如果 SSH 服务已关闭，可以通过以下命令开启它：

```bash
# chkconfig on
```
