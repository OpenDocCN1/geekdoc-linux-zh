

| cron 文件和目录 | 描述 |
|---|---|
| /etc/crontab | 系统 crontab 文件，仅 root 用户可访问 |
| /etc/cron.d | 包含多个 crontab 文件的目录，仅 root 用户可访问 |
| /etc/cron.hourly | 每小时执行的任务目录 |
| /etc/cron.daily | 每天执行的任务目录 |
| /etc/cron.weekly | 每周执行的任务目录 |
| /etc/cron.monthly | 每月执行的任务目录 |
| /etc/cron.yearly | 每年执行的任务目录 |
| /etc/cron.hourly | 每小时执行的任务目录 |
| /etc/cron.allow | 允许提交 cron 任务的用户 |
| /etc/cron.deny | 被拒绝访问 cron 的用户 |

## 表 27-2 Cron 文件和目录

## 运行 cron 目录脚本

每个目录都包含在同一时间运行的脚本。每个组的调度由 /etc/crontab 文件中的一个条目确定。脚本的实际执行由 /usr/bin/run-parts 执行，它运行给定目录中的所有脚本和程序。给定目录中所有任务的调度由 /etc/crontab 文件中的条目处理。Red Hat 提供了指定时间的条目，您可以根据自己的需要更改它们。默认的 Red Hat crontab 文件如下所示，其中包含在不同 cron 目录中运行脚本的时间。可以看出，大多数脚本都在大约凌晨 4 点运行，每天（4:02）、每周日（4:22）或每月第一天（4:42）。每小时的脚本在整点后一分钟运行。

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/
# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

> 提示 cron 目录中的脚本按字母顺序运行。如果需要某个脚本在其他脚本之前运行，您可能需要更改其名称。一种方法是为名称添加前缀数字。例如，在 /cron.weekly 目录中，anacron 脚本命名为 0anacron，以便它在其他脚本之前运行。

请记住，这些只是包含可执行文件的目录。实际调度由 /etc/crontab 文件中的条目执行。例如，如果将 cron.weekly crontab 条目中的每周字段从 0 改为 1，并将每月字段改为 1（22 4 1 * * 而不是 22 4 * * 0），则 cron.weekly 文件中的任务最终将按月而不是按周运行。

## cron 目录名称

这些目录使用的名称只是约定。对 cron 守护进程没有任何特殊意义。实际上，您可以创建自己的目录，将脚本放在其中，并安排 run-parts 在给定时间运行这些脚本。在下一个示例中，放在 /etc/cron.mydocs 目录中的脚本将在每周三中午 12 点运行。

```
* 12 * * 3 root run-parts /etc/cron.mydocs
```

## Anacron

对于可能在 cron 可能会运行的时间段内正常关机的系统，您可能希望用 anacron 来补充 cron。anacron 仅在需要执行计划任务时才激活。例如，如果系统在周末关机，而 cron 作业已安排在此时运行，则作业将不会执行。但是，anacron 会在系统再次打开时检查需要执行的作业，然后运行它们。它仅设计用于每天或每周运行的作业。

对于 anacron 作业，您将 crontab 条目放在 /etc/anacrontab 文件中。对于每个计划任务，您指定执行时间隔的天数（7 为每周，30 为每月）、运行的当天时间（以分钟为单位编号）、任务描述以及要执行的命令。对于备份，命令将是 tar 操作。您可以使用 redhat-config-services 打开 anacron 服务或使其在启动时自动启动。

## 系统运行级别：telinit、initab 和 shutdown

Linux 系统可以根据您想要赋予它的功能在不同的级别运行。例如，您可以在管理级别运行系统，锁定用户访问。正常完全操作只需在一定的操作能力级别运行系统即可激活，例如支持多用户访问或图形界面。这些级别（也称为状态或模式）称为运行级别，即您运行系统的支持级别。

## 运行级别

