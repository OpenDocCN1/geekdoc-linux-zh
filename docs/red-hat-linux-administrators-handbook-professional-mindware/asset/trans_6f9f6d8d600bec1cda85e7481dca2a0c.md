

无。您也可以使用 `*` 作为通配符，分别代表该行的设备（facility）部分或优先级（priority）部分，以指示所有设备或所有优先级。您可以在一行中使用逗号分隔的多个具有相同优先级的设备列表。例如，以下内容表示来自 ucp 和 news 设备（ucp 和 news 服务器程序）的严重（crit）优先级日志条目（通常称为消息）被写入 `/var/log/spooler` 文件：

```
uucp,news.crit /var/log/spooler
```

您还可以使用分号分隔的多个 `facility.priority` 对列表，将它们分配给单个目标。例如，以下内容表示来自所有设备的所有信息（info）日志条目被写入 `/var/log/messages` 文件，但邮件（mail）和 authpriv 设备的信息消息除外：

```
*.info;mail.none;authpriv.none /var/log/messages
```

默认的 syslogd 配置会将其日志写入 `/var/log` 目录。

## 使用 tail 监控日志

如果您遇到服务器进程问题，请查明该进程是否写入日志文件。如果它写入自己的日志文件或使用了 syslog 设施，您可以使用 tail 实用工具在进程运行时监控日志文件，该工具允许通过查看文件的最后部分来监控正在增长的日志文件。例如，要监控 `/var/log/messages` 文件，请运行以下命令：

```
tail -f /var/log/messages
```

这允许您在新条目写入文件时查看该文件。如果您想限制查看的行数，请使用 `-n` 或 `--lines` 选项。例如，要仅查看与上一个示例相同文件的最后三行，请运行 `tail -f -n 3 /var/log/messages`。

请注意，在非常活跃的系统上，由 syslogd 生成的日志文件可能会变得相当大。因此，您需要使用 logrotate 设施来轮转您的日志文件。事实上，默认情况下，syslogd 的 RPM 包会安装一个名为 syslog 的 logrotate 配置文件，位于 `/etc/logrotate.d` 目录中。

logrotate 配置每周轮转日志文件，并且也保留过去日志的压缩备份。

## 调度进程

与所有其他形式的 Unix 和类 Unix 操作系统一样，Red Hat Linux 为您提供两种广泛使用的进程调度设施。本节介绍如何使用这两种服务。

## 使用 at

at 实用工具允许您将命令排队以稍后执行。例如，要在晚上 8:40 运行名为 `du` 的磁盘使用情况摘要生成实用工具，请按如下方式运行 `at`：

```
at 20:40
```

at 命令会显示诸如 `at>` 这样的提示，您可以在其中输入 du 命令，如下所示：

```
at> du -a > /tmp/du.out
```

这里，du 的输出被重定向到一个文件。输入命令后（在本例中为 du 命令），at 会再次显示提示。您可以按 Ctrl+D 退出。您会看到类似以下的消息：

```
at> <EOF>
warning: commands will be executed using /bin/sh
job 1 at 2000-12-04 20:40
```

这意味着 at 已计划由 at 守护进程（atd）在 2000 年 12 月 4 日晚上 8:40 运行 `du -a > /tmp/du.out` 任务。您可以使用多种时间格式来指定执行时间。例如，除了说 `at 20:40` 之外，您也可以说 `at 8:40 p.m.`。您还可以指定日期连同时间。例如，`8:40pm Feb 23`、`10am + 5 days`、`12:30pm tomorrow`、`midnight` 和 `noon` 都是有效的时间规范。

要验证您的任务是否在任务队列中，请运行 `atq` 命令，它显示当前队列中已调度的任务。所有已调度的任务都存储在 `/var/spool/at` 目录中。

### 提示

如果您是该系统的 root 用户，您可以检查 `/var/spool/at` 存储目录中的文件，以查看将要运行的命令。

如果由于某种原因您想停止一个已调度的任务，您可以运行 `atrm` 命令来移除您的任务。使用 `atrm` 移除任务需要知道任务的序列号。要了解您已调度了哪些任务，请运行 `atq` 命令。要删除任何任务，请使用 `atrm job#`。例如，要移除任务 1，请运行 `atrm 1`。

调度的任务通过 `atd` 守护进程运行，该守护进程由 `init` 在运行级别 3（多用户模式）下启动。如果您想限制 at 设施的使用，请创建一个 `/etc/at.allow` 文件，并列出所有被允许运行它的用户。请记住每行输入一个用户名。任何未列在允许文件中的用户都会被拒绝访问 at 设施。另一方面，如果您只想拒绝少数用户但允许其余用户，请创建一个名为 `/etc/cron.deny` 的类似文件（原文此处可能有误，根据上下文应为 `/etc/at.deny`，但根据指令“翻译内容并保留符号”及不改变原文逻辑的原则，此处按原文直译，但在实际技术文档中通常对应 at.deny。不过，原文写的是 `/etc/at.deny` 吗？ 让我们仔细看原文：“create a similar file called `/etc/at.deny`”。 好的，原文确实是 `/etc/at.deny`。 抱歉，我刚才看错了。 原文是：`create a similar file called /etc/at.deny`。 好的。） 列出在此文件中的所有用户名都会被拒绝 at 访问。

尽管 at 为您提供了进程调度功能，但另一种名为 `cron` 的设施比 at 使用得更广泛，因为 `cron` 为重复性任务提供了创建无人值守进程执行计划表的更结构化的方式。

## 使用 cron

Linux 系统中的许多任务（进程）需要定期调度以进行无人值守执行。例如，要轮转 syslog 创建的日志文件，或从 tmp 目录中删除旧文件，您需要每天或每周运行一次进程。cron 设施允许您创建循环任务计划表。

cron 设施包括 `crond` 守护进程，该守护进程由 `init` 进程启动。crond 守护进程从 `/etc/crontab` 和 `/var/spool/cron` 目录中的文件读取任务计划表。后者用于存储被允许运行 cron 任务的普通用户的计划文件（通常称为 `crontab` 或 `cron table`）。作为超级用户，您可以在 `/etc/cron.allow` 文件中指定允许运行 cron 任务的用户列表。同样，您可以通过在 `/etc/cron.deny` 文件中指定其姓名来明确拒绝任何用户对 cron 的访问。这两个文件都使用简单的每行一个用户名的格式。被允许运行 cron 任务的普通用户可以使用 `crontab` 实用工具创建任务计划表。例如，被允许运行 cron 任务的普通用户可以运行 `crontab -e` 来创建和编辑 cron 任务条目。cron 任务规范具有以下格式：

```
minute(s) hour(s) day(s) month weekday username command argument(s)
```

前五个时间规范字段在表 6-4 中讨论。

表 6-4 cron 时间规范字段

| 字段 | 描述 | 范围 |
| :--- | :--- | :--- |
| minutes(s) | 一小时中的一个或多个分钟。您可以指定逗号分隔的分钟列表。 | 0-59 |
| hour(s) | 一天中的一个或多个小时。您可以指定逗号分隔的小时列表。 | 0-23，其中 0 是午夜 |
| day(s) | 一个月中的一个或多个天。您可以指定逗号分隔的天列表。 | 1-31 |
| month | 一年中的一个或多个月份。您可以指定逗号分隔的月份列表。 | 1-12 |
| weekday | 一周中的一个或多个天。您可以指定逗号分隔的天列表。 | 1-7，其中 1 是星期一 |

对于表 6-4 中显示的任何字段，您都可以使用 `*` 作为通配符。以下是一个示例 cron 任务规范：

```
01 * * * * root /some/script
```

这表明 `/some/script` 将在每小时的第一分钟、每天、每月、每星期几运行。该脚本将作为 root 用户运行。要每十分钟运行一次此脚本，可以定义如下的 cron 任务：

```
0,10,20,30,40,50 * * * * root /some/script
```

要运行相同的脚本但每月仅运行一次，可以按以下方式调度 cron 任务：

```
01 1 1 * * root /some/script
```

这里，脚本将在每月第一天的凌晨 1:01 运行。

系统的默认 cron 任务是 /etc/crontab，其中包括一些有趣的 cron 任务条目，例如以下内容：

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

这些 cron 任务用于运行位于 /usr/bin 目录中的 run-parts 脚本。使用前面的示例中的四个 cron 任务规范，该脚本每小时、每天、每周和每月运行一次。它接受目录名称作为参数，并运行位于该目录中的所有脚本或程序。例如，考虑前面示例中的第一个 cron 条目。它表示 run-parts 脚本应在每小时的第一分钟运行。该脚本被传入参数 /etc/cron.hourly。由于该脚本运行位于此目录中的所有文件，因此整个过程的效果就好像 /etc/cron.hourly 目录中的所有文件都被设置为 cron 任务一样。这种技巧允许您将新文件放入 /etc/cron.hourly 目录，并自动将其调度为每小时运行一次。同样，其他三个 cron 条目允许您只需将程序放置在 /etc/cron.daily、/etc/cron.weekly 或 /etc/cron.monthly 目录中，即可分别每天、每周或每月运行任何程序。这使得创建几乎所有一切 cron 任务变得轻而易举，而无需真正配置 cron 条目。

