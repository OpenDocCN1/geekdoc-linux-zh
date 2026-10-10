

## `xinetd` 连接处理
1. **`xinetd`** 接收连接请求。
2. **`xinetd`** 开始将 `jukebox.linuxtoys.net` 的地址和名称与 `/etc/hosts.allow` 中列出的规则进行比较。它从文件顶部开始，依次向下查找，直到找到匹配项。守护进程（处理您 Fedora 机器上网络服务的程序）和连接客户端的 IP 地址或名称都必须与 `hosts.allow` 文件中的信息匹配。在这种情况下，遇到的第一条规则匹配了该请求：

```
cups-lpd : 199.170.177.* . . linuxtoys.net
```

3. Jukebox 不在 `199.170.177` 子网中，但它在 `linuxtoys.net` 域中。`xinetd` 一找到此匹配项就停止搜索该文件。

如果 Jukebox 使用另一种协议连接到您的机器呢？在这种情况下，它不匹配 `hosts.allow` 中的任何规则，`xinetd` 继续处理 `hosts.deny` 文件。条目 `ALL: ALL` 匹配任何内容，因此 `tcpd` 拒绝连接。

`ALL` 通配符也用在 `hosts.allow` 文件中。在这种情况下，我们是告诉 `xinetd` 允许任何主机连接到 Linux 机器上的 FTP 服务。这对于运行任何人都可访问的匿名 FTP 服务器是合适的。如果您没有运行匿名 FTP 站点，您最好不要使用 `ALL` 标志。

一条很好的经验法则是使您的 `hosts.allow` 和 `hosts.deny` 文件尽可能严格，然后仅显式启用您真正需要的服务。相反，仅授予真正需要访问权限的系统访问权。使用 `ALL` 标志授予特定服务的通用访问权限可能比输入长长的子网或域列表更容易，但花几分钟时间实施正确的安全措施，总比花很多时间恢复入侵后的损失要好。

> **提示：** 您可以使用 `/etc/xinetd.conf` 文件中的各种选项进一步限制对服务的访问，甚至可以限制某些服务仅在一天中的特定时间访问。阅读 `xinetd` 的手册页（通过在命令提示符下键入 **man xinetd**）以了解有关这些选项的更多信息。

## 检查日志文件

为应对黑客攻击准备您的系统只是战斗的一部分。您还必须在黑客攻击发生时识别出它。理解 Fedora 记录重要事件的各类日志文件对实现这一目标至关重要。您的 Fedora 系统的日志文件可以在 `/var/log` 目录中找到。

由于系统日志是纯文本文件，您可以使用任何文本编辑器或分页命令（如 `less` 或 `more`）直接查看日志内容。logwatch 设施（随 Fedora 附带）会通过电子邮件将日志文件的每日重点发送给 root 用户。您还可以添加诸如 `logsentry` 之类的包来监控您的日志文件。

### 了解 rsyslogd 服务

`/var/log` 目录中的大多数文件由 rsyslogd 服务维护。rsyslogd 守护进程是系统日志守护进程，作为先前称为 syslog 的日志系统的扩展。它接受来自各种其他程序的日志消息，并将其写入适当的日志文件。这比每个程序直接写入其自己的日志文件更好，因为它允许您集中管理日志文件的处理方式。可以配置 rsyslogd 在日志文件中记录不同级别的详细信息。它可以被指示忽略除最关键的消息以外的所有内容，或者记录每个细节。

rsyslogd 守护进程甚至可以从网络上的其他计算机接收消息。这特别有用，因为它使您可以集中管理和审查网络上多个系统的日志文件。这种做法还有重大的安全利益。如果您的网络中的某个系统被入侵，黑客无法删除或修改日志文件，因为这些文件存储在一台单独的计算机上。

然而，重要的是要记住，这些日志消息默认情况下是未加密的。任何侦听您本地网络的人都可能在这些消息从一台机器传输到另一台机器时窃听这些消息。此外，虽然黑客可能无法更改旧的日志消息，但他能够影响系统，使得任何新的日志消息都不应被信任。

运行专用的日志主机（loghost）并不少见，即一台除了记录网络中其他计算机的日志消息外没有其它用途的计算机。由于该系统不运行其他服务，因此被入侵的可能性较小。这使得黑客几乎不可能擦除其痕迹。然而，这并不意味着在黑客人侵了您网络中的一台机器后，所有的日志消息都是准确的。

### 使用 rsyslogd 将日志重定向到日志主机

要将您计算机的日志文件重定向到另一台计算机的 rsyslogd，您必须对本地 rsyslogd 的配置文件进行一些更改。您需要处理的文件是 `/etc/rsyslog.conf`。如果您还不是 root，请先成为 root，然后使用文本编辑器（如 `vi`）打开 `/etc/rsyslog.conf` 文件。您应该会看到类似以下内容：

```
#rsyslog v3 config file

# if you experience problems, check
# http://www.rsyslog.com/troubleshoot for assistance

#### MODULES ####

$ModLoad imuxsock.so # provides support for local system logging (e.g. via logger command)
$ModLoad imklog.so # provides kernel logging support (previously done by rklogd)
#ModLoad immark.so # provides --MARK-- message capability

# Provides UDP syslog reception
##ModLoad imudp.so
##UDPServerRun 514

# Provides TCP syslog reception
##ModLoad imtcp.so
##InputTCPServerRun 514


### GLOBAL DIRECTIVES ###

# Use default timestamp format
$ActionFileDefaultTemplate RSYSLOG TraditionalFileFormat

# File syncing capability is disabled by default.
# This feature is usually not required,
# not useful and an extreme performance hit
#$ActionFileEnableSync on

### RULES ###

# Log all kernel messages to the console.
# Logging much else clutters up the screen.
#Kern.*						/dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none;cron.none		/var/log/messages

# The authpriv file has restricted access.
authpriv.*					/var/log/secure

# Log all the mail messages in one place.
mail.*						-/var/log/maillog

# Log cron stuff
cron.*						/var/log/cron

# Everybody gets emergency messages
*.emerg						*

# Save news errors of level crit and higher in a special file.
ucp,news.crit					/var/log/spooler

# Save boot messages also to boot.log
local7.*						/var/log/boot.log

# ### begin forwarding rule ###
# The statement between the begin ... end define a SINGLE forwarding
# rule. They belong together, do NOT split them. If you create multiple
# forwarding rules, duplicate the whole block!
# Remote Logging (we use TCP for reliable delivery)
#
# An on-disk queue is created for this action. If the remote host is
# down, messages are spooled to disk and sent when it is up again.
#\$WorkDirectory /var/\$pgpl/relaylog # where to place spool files
#\$ActionQueueSaveName fwdRule1 # unique name prefix for spool files
#\$ActionQueueMaxDiskSpace 1g # 1gb space limit (use as much as possible)
#\$ActionQueueSaveOnShutdown on # save messages to disk on shutdown
#\$ActionQueueType LinkedList # run asynchronously
#\$ActionResendRetryCount -1 # infinite retries if host is down
# remote host is: name/sp-port, e.g. 192.168.0.1:514, port optional
\*.* \@remote-host:514
# ### end of the forwarding rule ###
```

以 `#` 字符开头的行是注释。其他行包含两列信息，由空格或制表符分隔。左侧字段是分号分隔的消息类型和消息优先级列表。右侧字段是这些消息应写入的日志文件。

最有趣的部分以名为 RULES 的章节开始。

> **注意：** 注意 `/var/log/maillog` 文件前面的破折号（`-`）。通常，每次记录后都会同步每个日志文件。在日志文件的完整路径前加上破折号表示在每次记录后不会同步该文件。虽然这可能会导致如果您的机器在日志写入前崩溃而丢失信息，但如果您运行详细日志记录，这可以提高系统的性能。

要将消息发送到另一台计算机（日志主机）而不是文件，只需将日志文件名替换为 `@` 字符后跟日志主机的名称。例如，要重定向通常发送到 messages、secure 和 maillog 日志文件的输出，请对前面的文件进行以下更改：

```
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;news.none;authpriv.none;cron.none @loghost

# The authpriv file has restricted access.
authpriv.* @loghost

# Log all the mail messages in one place.
mail.* @loghost
```

