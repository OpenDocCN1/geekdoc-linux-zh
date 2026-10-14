
将诊断信息发送到 logs.example.com 上的 syslogd，第三条将所有 syslog 消息发送到文件 /var/log/messages，最后一条将紧急消息写入 root 的屏幕，前提是 root 恰好已登录。

kern.warn 的条目表示消息的设施名称为 kern，优先级为 warn。Linux 2.2 的有效设施名称为 auth、authpriv、cron、daemon、kern、lpr、mail、news、syslog、user、uucp 以及 local0 到 local7。优先级为 alert、crit、debug、emerg、err、info、notice 和 warning。还有一些已过时的优先级（请查看 /usr/include/sys/syslog.h 获取列表）。

随着系统运行，消息会不断堆积在 /var/log 中。如果系统对此不采取任何措施，包含 /var 的磁盘分区最终会填满，使得系统难以使用。大多数发行版意识到了这一点，并运行 cron 作业来清理日志目录，以防止这种情况发生。

如果您拥有一个庞大的网络，最好设置一个日志主机，让其他机器可以将日志消息发送到该主机。将整个网络的日志集中保存在一处，可以使检测和调试问题变得更快、更轻松。您可能还希望保留本地日志——您可以用很少的磁盘空间和系统时间换取这里那里节省几分钟的时间。

> **注意**：某些发行版不会将所有消息设施都放在 /etc/syslog.conf 中（尤其是本地设施）。如果 /etc/syslog.conf 中未提及某个设施，则任何程序向该设施输出的内容都将被丢弃。使用 logger 命令来调试您的配置。

相关手册页：syslog.conf (5)、syslog (1)、logger (1)

## cron

cron 是一个周期性事件调度程序，是一个有用的系统守护进程。它读取名为 crontabs 的文件，这些文件指定了时间、间隔以及在每个间隔结束时运行的命令。这些文件通常位于 /var/spool/cron，用户使用 crontab 命令创建、访问、修改并将其放置到位。以下是简短的 crontab 参考：

- `crontab file`  使用 file 作为 crontab
- `crontab -e`  编辑 crontab（使用环境变量 VISUAL 或 EDITOR 指定的编辑器）
- `crontab -l`  显示 crontab
- `crontab -r`  删除 crontab

下面是一个 crontab 示例（对于登录名为 jamie 的用户）：

```
SHELL=/bin/sh
PATH=/usr/bin:/usr/sbin:/usr/local/sbin:/usr/local/bin:/sbin:/bin
MAILTO=jamie
53 6,20 * * * /home/jamie/bin/clean-junk > /dev/null 2>&1
```

SHELL、PATH 和 MAILTO 被设置为您所期望的值：用于命令的 shell 和路径，以及如果有任何命令产生输出时发送邮件的用户。在第四行，前五个字段指定时间和间隔；从第一个到第五个，它们分别是分钟、小时、月份中的日期、月份和星期几。它们以数字或星号 (*) 指定，星号表示全部——例如，星期几字段中的 * 与 0,1,2,3,4,5,6 相同。上面 jamie 的 crontab 中的最后一行匹配每一天（月份中的日期和星期几）和每个月，当分钟为 53 且小时为 6 或 20 时（即上午 6:53 和晚上 8:53）。

当时间与五个字段中指定的内容匹配时，字段后的操作将被执行。如果您想在每个 13 号星期五烦扰一个名为 bob 的用户，您可以写：

```
* * 13 * 5 /bin/mail -s "Beware, Bob" bob
```

分钟和小时的 * 条目使得这对 bob 来说尤其令人讨厌：可怜的 bob 在每个 13 号星期五的每一分钟都会收到您的一条消息。如果您只想在每个 13 号星期五中午给 bob 发送一条消息，可以使用以下内容：

```
00 12 13 * 5 /bin/mail -s "Beware, Bob" bob
```

> （我们可不是说这种折磨 bob 的行为是个好主意。）

crontab 文件的另一个版本，/etc/crontab，是一个系统 crontab，并在时间规范后多了一个字段：运行作业的用户。在以下两个条目中，运行任务的用户是 root 和 backup。

```
15 4 * * * root /usr/local/sbin/sysclean > /dev/null 2>&1
25 23 * * * backup /usr/local/sbin/do-backups
```

随 Linux 一起提供的 cron 版本（Vixie Cron）与其它 Unix 变体上的版本相比相当灵活；请查看手册页以获取更多信息。

相关手册页：crontab (5)、crontab (1)、cron (8)

## The passwd File

Unix 下的主要用户数据库是 /etc/passwd。修改它的方法有多种。用户可用的 passwd 命令也是系统管理员的维护工具。

