
## 清单 12-4 /etc/syslog.conf 文件

```
/etc/syslog.conf
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
#kern.*								/dev/console

# Log anything (except mail) of level
# info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none	/var/log/messages

# The authpriv file has restricted access.
authpriv.*					/var/log/secure

# Log all the mail messages in one place.
mail.*						/var/log/maillog

# Everybody gets emergency messages,
# plus log them on another machine.
*.emerg						*

# Save mail and news errors of level
# err and higher in a special file.
uucp,news.crit				/var/log/spooler

# Save boot messages also to boot.log
local7.*						/var/log/boot.log
```

在本清单中，有两行（就 Apache 而言）很重要。它们是：

```
*.info;mail.none;authpriv.none	/var/log/messages
*.emerg						*
```

第一行告诉 syslog 将所有 info 类型的消息（除邮件和私有认证外）写入 /var/log/messages 文件，第二行说明所有紧急消息应写入所有日志文件。使用 LogLevel 指令，你可以指定 Apache 应向 syslog 发送的消息类型。例如：

```
ErrorLog syslog
LogLevel debug
```

这里，Apache 被指示将调试消息发送到 syslog。如果想通过 syslog 将调试消息存储到不同的文件，则需要修改 /etc/syslog.conf。例如：

```
*.debug          /var/log/debug
```

在 /etc/syslog.conf 中添加此行并重启 syslogd（kill -HUP syslogd_PID）和 Apache，即可将所有 Apache 调试消息存储到 /var/log/debug 文件。以下是几个日志级别设置：

- Emerg — 紧急消息
- Alert — 警告消息
- Crit — 严重消息
- Error — 错误消息
- Warn — 警告
- Notice — 通知消息
- Info — 信息消息
- Debug — 在调试级别记录的消息还将包含消息生成的源文件和行号，以帮助调试和代码开发。

如果你想在日志发生时查看 syslog 或其他日志文件的更新，可以使用 tail 工具。例如，如果你想在发生时查看名为 /var/log/messages 的日志的更新，请使用以下命令：

```
tail -f /var/log/messages
```

## 日志维护

通过启用日志记录，你可能能够节省大量工作。然而，日志本身也会增加你的额外工作：它们需要维护。在访问率高或拥有多个虚拟域的 Apache 站点上，日志文件可能在很短时间内变得巨大，这很容易导致磁盘空间危机。当日志文件变得非常大时，你应该轮转它们。

你有两种轮转日志的选项：你可以使用 Apache 自带的名为 rotatelog 的工具；或者你可以使用 logrotate，这是一个在大多数 Linux 系统上都可用的设施。

## 使用 rotatelog 轮转日志文件

Apache 附带了一个名为 rotatelog 的支持工具，可让你轮转日志文件。你可以按如下方式使用此程序：

```
TransferLog "| path_to_rotatelogs logfile rotation_time_in_seconds"
```

例如，如果你想每 86,400 秒（即 24 小时）轮转一次访问日志，请使用以下行：

```
TransferLog "| /path/to/rotatelogs /var/logs/httpd 86400"
```

你将每天的访问日志信息存储在名为 /var/logs/httpd.nnnn 的文件中，其中 nnnn 代表一个长数字。

## 使用 logrotate 轮转日志文件

logrotate 工具会轮转、压缩和邮件发送日志文件。它旨在简化日志文件的系统管理，并能够按每日、每周或每月，或按大小基准自动轮转、压缩、删除和邮件发送日志文件。通常，logrotate 作为每日 cron 作业运行。阅读 logrotate 的 man 手册以了解更多信息。

你应该创建一个名为 /etc/logrotate.d/apache 的脚本，如清单 12-5 所示，以自动轮转 Apache 日志。

## 清单 12-5 /etc/logrotate.d/apache 文件

```
# Note that this script assumes the following:
#
# a. You have installed Apache in /usr/local/apache
# b. Your log path is /usr/local/apache/logs
# c. Your access log is called access_log (default in Apache)
# d. Your error log is called error_log (default in Apache)
```

### 清单 12-5 继续

```
# e. The PID file, httpd.pid, for Apache is stored in the log
#   directory (default in Apache)
#
# If any of the above assumptions are wrong, please change
# the path or filename accordingly.
#
/usr/local/apache/logs/access_log {
    missingok

    compress
    rotate 5
    mail webmaster@yourdomain.com
    errors webmaster@yourdomain.com
    size=10240K

    postrotate
        /bin/kill -HUP \
        `cat /usr/local/apache/logs/httpd.pid 2>/dev/null` \
        2> /dev/null || true
    endscript
}

/usr/local/apache/logs/error_log {
    missingok

    compress
    rotate 5
    mail webmaster@yourdomain.com
    errors webmaster@yourdomain.com
    size=10240K

postrotate
    /bin/kill -HUP \
    `cat /usr/local/apache/logs/httpd.pid 2>/dev/null` \
    2> /dev/null || true
endscript
}
```

此配置指定 Apache 的访问日志和错误日志文件将在每个文件增长超过 10MB（10240K）大小时进行轮转，并且旧日志文件在经过五次轮转后会被压缩并邮件发送给 webmaster@yourdomain.com，而不是被删除。处理日志文件时发生的任何错误都会被邮件发送给 root@yourdomain.com。

## 使用 logresolve 将 IP 地址解析为主机名

出于性能原因，你应该通过将 HostNameLookups 指令设置为 Off 来禁用主机名查找。这意味着你的日志条目显示远程客户端的 IP 地址而不是主机名。在分析日志时，拥有主机名有助于更轻松地确定谁来自何处。例如，以下是我的 /usr/local/apache/logs/access_log 文件中的几个示例日志条目：

```
207.183.233.19 - - [15/Mar/2001:13:05:01 -0800] "GET /book/images/back.gif
HTTP/1.1" 304 0

207.183.233.20 - - [15/Mar/2001:14:45:02 -0800] "GET /book/images/forward.gif
HTTP/1.1" 304 0

207.183.233.21 - - [15/Mar/2001:15:30:03 -0800] "GET /book/images/top.gif
HTTP/1.1" 304 0
```

如果你打开了 HostNameLookups，Apache 将把客户端 IP 地址 207.183.233.19、207.183.233.20 和 207.183.233.21 解析为适当的主机名。当 HostNameLookups 设置为 On 且默认 LogFormat 指令设置为如下所示时

```
LogFormat "%h %l %u %t \"%r\" %>s %b" common
```

并且你使用 CustomLog logs/access_log common 使用通用格式进行日志记录时，这些示例日志条目将如下所示：

```
nano.evoknow.com - - [15/Mar/2001:13:05:01 -0800] "GET /book/images/back.
gif HTTP/1.1" 304 0

rhat.evoknow.com - - [15/Mar/2001:14:45:02 -0800] "GET /book/images/forward.gif
HTTP/1.1" 304 0

r2d2.evoknow.com - - [15/Mar/2001:15:30:03 -0800] "GET /book/images/top.
gif HTTP/1.1" 304 0
```

由于打开 DNS 查找会导致 Apache 服务器在完成响应时花费更多时间，因此广泛建议应单独使用名为 logresolve 的工具执行主机名查找，该工具可在你的 Apache bin 目录（/usr/local/apache/bin）中找到。log_resolver.sh 脚本，如清单 12-6 所示，使用 logresolve 工具执行主机名查找。

## 清单 12-6 一个示例 log_resolver.sh 文件

```sh
#!/bin/sh

#
# Make sure you change the pathnames according to
# your Apache installation
#

# Fully qualified path name (FQPN) of the
# log resolver utility
LOGRESOLVER=/usr/local/apache/bin/logresolve

# Statistic file generated by the utility
STATFILE=/tmp/log_stats.txt

# Your Apache Log file
LOGFILE=/usr/local/apache/logs/access_log

# New log file that has IP addressed resolved
OUTFILE=/usr/local/apache/logs/access_log.resolved
```
