

要将来自 news 设施的所有消息（从 info 到 crit，但不包括 alert 或 emerg）记录到 newsboy 用户的控制台中，您应使用如下所示的命令：

```bash
news.lalert newsboy
```

![](img/49f4f38f3aec011238fa50f89e643db3_356_0.png)

> 以下行将所有消息（除 debug 级别外）发送到 **tty12** 控制台，可以通过按 Alt+F12 或 Ctrl+Alt+F12 切换到由 /dev/tty12 定义的控制台：
> `*: : /dev/tty12`
>
> 为了使此更改生效，必须向 **syslogd** 守护进程发送 HUP 信号或重启该守护进程。

## 自定义日志条目

logger 命令通常用于脚本中，以便在需要时将条目放入系统日志设施中。它具有生成系统可接受的几乎任何日志文件条目的能力，包括不同的严重级别。

一个典型的 logger 命令用于写入特定事件已完成的记录，例如：

```bash
logger Backup succeeded on host snuffy
```

logger 命令还可以用于提交匹配特定设施且具有不同严重级别的日志条目。要向 user 设施提交一条关于备份失败且严重级别为 crit 的日志条目，请使用以下命令：

```bash
logger -p user.crit Backup failed on host snuffy
```

对 `/var/log/messages` 文件使用 `tail -n 5` 命令将显示类似以下内容的内容：

```text
Mar 19 18:06:52 localhost network:
Bringing up Loopback interface:
Mar 19 18:07:05 localhost network:
Bringing up interface eth0: succeeded
Mar 19 18:07:31 localhost sshd[pan_unix](3838):
session opened for user root by (uid=0)
Mar 19 20:38:39 localhost sshd[pan_unix](4556):
session opened for user root by (uid=0)
Mar 19 20:53:39 localhost root:
backup failed on host snuffy
```

## 安全日志文件

多个日志文件会影响系统安全性，特别是使用 who、last、lastlog 和 w 命令进行查询的能力。

| 日志文件 | 用途 | 相关命令 |
|---|---|---|
| /var/log/wtmp | 用户登录时间和持续时间 | last, w, **up**d**w**tmp |
| /var/run/utmp | 当前用户登录信息 | **f**inger, **w**ho, **l**ogin |
| /var/log/lastlog | 用户登录日期、时间和持续时间 | **last**log |

如果 `/var/log/wtmp` 和 `/var/log/btmp` 文件存在，`last` 命令将使用这些文件来显示最近登录用户的信息。默认情况下，它会显示一屏混合的用户条目，或者您可以将其限制为特定用户：`last`

这会生成类似的输出：

```text
rbunson  tty1     Thu Mar 18 14:13  - 21:49  (07:36)
rbunson  tty1     Tue Mar 16 16:10  - 16:23  (00:12)
rbunson  tty1     Tue Mar 16 15:59  - 16:10  (00:11)
rbunson  pts/2    Tue Mar 15 15:47  - 15:10  (00:23)
```

`w` 和 `who` 命令通常用于确定哪些用户正在系统中，它们分别引用 `/var/log/wtmp` 和 `/var/run/utmp` 文件。通过比较输出可以看到这两个程序输出的主要区别。

`w` 命令的输出看起来像这样：

```text
 3:38pm  up  1 day, 10:53,  2 users,  load average:: 0.00, 0.00, 0.00
USER     TTY      FROM                 LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0   192.168.1.100         20Mar04  34:53m  0.41s  0.01s man xconsole
root     pts/1   192.168.1.100         3:30pm   0.00s   0.19s  0.01s w
```

`who` 命令的输出看起来像这样：

```text
root      pts/0    Mar 20 17:46 (192.168.1.100)
root      pts/1    Apr 1 15:30  (192.168.1.100)
```

如您所见，`w` 命令输出大量信息，但包含两行标题行，因此在使用 `wc` 命令统计系统中的用户时，本质上不够准确。

> **警报** 通过从 `/var/run/utmp` 日志文件中移除其他用户可读权限位，可以禁用普通用户从 `w` 和 `who` 命令获取信息的能力。`w` 和 `who` 命令仍然可以运行，但如果执行命令的用户是普通用户，它们将不显示任何数据。

`lastlog` 命令是更有用的日志命令之一，因为它显示 `lastlog` 日志文件的内容，并按用户 ID 对输出进行排序。不过，如果用户从未登录，它会打印 **从未登录** (Never logged in) 而不是端口和时间信息。

**lastlog** 命令显示 `/var/log/lastlog` 日志文件，这是一个 Unicode 文件，包含大量二进制代码和信息，应主要使用 **lastlog** 命令来查看它。如果使用 **cat** 命令查看此文件而导致终端格式混乱，请使用 **reset** 命令重置终端。

要显示已登录用户的列表，特别是为了检查系统账户是否已被破解并登录到系统，请使用以下命令：

```bash
lastlog | grep -iv "never logged in"
```

这会生成与以下内容类似的输出：

| 用户名 | 端口 | 来源 | 最新时间 |
|---|---|---|---|
| root | pts/1 | 192.168.1.100 | Thu Apr 1 15:30:52 -0500 |
| rbrunson | tty1 | | Thu Mar 18 14:13:36 -0500 |

使用 **grep** 命令的 **-v** 选项会导致所有匹配搜索术语的行不被显示，从而留下一个自系统安装以来已登录该系统的用户列表。

您还可以使用 **-u** 用户名选项将 **lastlog** 条目的显示限制为特定的用户名：

```bash
lastlog -u rbrunson
```

这返回以下输出：

| 用户名 | 端口 | 来源 | 最新时间 |
|---|---|---|---|
| rbrunson | tty1 | | Thu Mar 18 14:13:36 -0500 |

您也可以显示比某个天数值更新的条目，例如过去 5 天内发生的条目：

```bash
lastlog -t 5
```

这返回以下输出：

| 用户名 | 端口 | 来源 | 最新时间 |
|---|---|---|---|
| root | pts/1 | 192.168.1.100 | Thu Apr 1 15:30:52 -0500 |
| rbrunson | tty1 | | Thu Mar 30 14:13:36 -0500 |

归档日志文件可以通过手动操作或使用 **logrotate** 命令来完成。当正确配置并定期运行 **logrotate** 命令时，它会按照配置归档、压缩、删除并发送邮件日志文件到中心主机（如果需要的话）。

logrotate 命令使用 `/etc/logrotate.conf` 作为其配置文件，文件中的条目允许您设置依赖日期或日志大小的日志轮换参数，以启动归档、压缩以及将日志文件通过电子邮件发送到中心主机（如果需要）。

> **警报** logrotate 命令和 /etc/logrotate.conf 文件的存在和功能在考试中会被测试，但它们的实际使用超出了考试目标范围，不在我们的讨论范围之内。

## 调度和运行任务

有三个主要实用工具在 Linux 系统上调度的任务，它们各有优缺点。任何忙碌的系统管理员都会认识到需要一种调度工具，以便重复性任务能够按时且足够频繁地实际执行。

### at 命令

at 命令旨在在特定时间运行一次任务。at 命令的任务或作业被排队在 /var/spool/at 目录中，每个作业由一个单一文件表示。

典型的 at 作业旨在处理一次性的或非常不频繁的作业，这些作业在奇怪的时间发生。例如，许多系统管理员使用 at 来提醒自己参加会议或执行某些任务：

```text
at 2pm today
at> echo "take a break"
at> <EOI>
job 1 at 2004-04-02 14:00
```

您在命令行输入前一个代码块的第一行（`at 2pm today`），这会使 `at>` 提示符出现。然后输入您想要执行的命令，按 Enter 键，再按 Ctrl+D 结束任务。结束任务会显示 `<EOI>` 通知，随后是一行回显作业调度信息的内容。

at 命令使用各种时间限定符，有些非常复杂，有些非常简单：

- **midnight**（午夜）——在当天 00:00 运行任务。
- **noon**（中午）——在当天 12:00 运行任务。
- **teatime**（下午茶时间）——在 16:00 运行任务（可以看出 at 的英国根源）。
- **time-of-day**（一天中的时间）——例如 `2 p.m.` 或 `5 a.m.`。
- **date**（日期）——您可以指定特定日期上的时间，例如 `2pm jul 23` 或 `4am 121504`。
- **now + time**（当前时间 + 时间）——您可以指定从当前时间起的任意分钟、小时、天或周数，例如 `now + 30 minutes`。

### 与 at 相关的命令和文件

`at` 命令仅启动作业。一些命令可以帮助您管理系统中的 `at` 作业，包括以下命令：

- `atq`——显示 `at` 队列中的作业，包括作业编号、日期和时间以及执行用户（这也可以通过 `at -l` 查看）。
- `atrm`——通过作业编号删除 `at` 作业，该编号通过上一个命令确定，语法为 `atrm #`（其中 `#` 是作业编号）。

`at` 拥有一组安全文件——`/etc/at.allow` 和 `/etc/at.deny`——允许用户或阻止用户排队 at 作业。如果存在 `at.allow` 文件且包含用户名，则只有这些用户可以使用 `at`。如果存在 `at.deny` 文件且包含用户名，则这些用户被拒绝，而所有其他用户被允许。如果两个文件都不存在，则只有 `root` 用户允许提交 `at` 作业。

### batch 命令

使用 `batch` 命令相对简单；它是 `at` 命令的某种扩展，并共享相同的手册页。`batch` 命令用于在特定系统利用率阈值时运行任务或作业，而不是在特定时间。正如您可以想象的，有些系统相当繁忙，您需要确定哪些作业如果具有时间敏感性，可能需要使用另一种调度实用工具来运行。

默认情况下，`batch` 在未来某个时间运行作业，当机器系统利用率小于或等于 0.8 的平均负载时。这可以通过使用 `atrun` 命令指定所需的利用率平均值来配置，例如：

```bash
atrun -l 20
```

这将 `batch` 监测的阈值设置为系统利用率的平均负载的 20%，如果系统利用率降至该平均值以下，则会运行 `batch` 作业。

