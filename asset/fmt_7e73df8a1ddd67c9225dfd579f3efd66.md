
还包含了几个目录，例如 `network-scripts`，它列出了多个网络连接的启动脚本——例如启动 PPP 连接的 `ifup-ppp`。

## 系统日志：/var/log 和 syslogd

在系统上执行的任务所保留的各种日志都保存在 `/var/log` 目录中。在这里，你可以找到邮件、新闻以及所有其他系统操作的日志。`/var/log/messages` 是未被其他日志涵盖的所有系统任务的日志。这通常包括启动任务，例如加载驱动程序和挂载文件系统。如果某个卡的驱动程序在启动时安装失败，你可以在这里找到错误信息。日志也会记录在文件中，显示谁尝试登录哪个账户。`/var/log/maillog` 文件记录消息传输和新闻传输。

日志由 `syslog` 守护进程管理。该守护进程将管理系统上的日志，并与网络上其他系统的日志操作协调。`syslogd` 的配置保存在 `/etc/syslog.conf` 文件中。该文件包含系统文件的名称和位置。在这里你有 `/var/log/messages` 和 `/var/log/maillog` 的条目。每个条目由两个字段组成：选择器（selector）和动作（action）。选择器是要记录的服务类型，而动作是日志存放的地方。动作通常是一个日志文件，也可以是远程主机或到另一个程序的管道。服务的类型被称为设施（facility）；syslog 使用若干个术语来指定某些服务类型（见表 28-7）。设施可以由优先级（priority）进一步限定。优先级指定由设施生成的消息类型；syslog 使用多个指定的术语来指示不同的优先级。选择器由设施和优先级组成，用点隔开。

### 表 28-7：Syslog 设施、优先级和操作符

| Facility | Priority | Description |
| :--- | :--- | :--- |
| auth | 7 | Security (private) |
| cron | 5 | Clock |
| daemon | 3 | Daemon |
| kernel | 0 | Kernel |
| lpr | 4 | Printer |
| mail | 4 | Mail |
| news | 5 | News |
| syslog | 6 | Syslog |
| user | 8 | User |
| uucp | 7 | UUCP |
| local0... | | Local |
| debug | 7 | Debug |
| info | 6 | Informational |
| notice | 5 | Notice |
| warning | 4 | Warning |
| err | 3 | Error |
| crit | 2 | Critical |
| alert | 1 | Alert |
| emerg | 0 | Emergency |

### 表 28-8：Syslog 优先级和描述

| Priority | Description |
| :--- | :--- |
| 0 | Emergency |
| 1 | Alert |
| 2 | Critical |
| 3 | Error |
| 4 | Warning |
| 5 | Notice |
| 6 | Informational |
| 7 | Debug |
| 8 | Local |

```
uucp,news.crit /var/log/spooler
```

# Save boot messages also to boot.log

```
local7.* /var/log/boot.log
```

```
#
# INN
#
news.crit /var/log/news/news.crit
news.err /var/log/news/news.err
news.notice /var/log/news/news.notice
```

## 性能分析工具与进程

Linux 将你在系统上执行的每个任务都视为一个进程，并为其分配一个数字。你可以检查这些进程并停止它们。从命令行，你可以使用 `ps` 命令列出进程。通过 `-aux` 命令，你可以列出所有进程。将输出通过管道交给 `grep` 并匹配模式可以让你搜索特定的进程。以下命令列出了所有系统进程：

```
ps -aux | grep 'X'
```
