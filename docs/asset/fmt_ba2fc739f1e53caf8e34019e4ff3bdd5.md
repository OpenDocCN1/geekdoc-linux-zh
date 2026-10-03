
| 793 | dla | 1032K | 844K | cpu0 | 58 | 0 | 0:00.00 | 0.1% | prstat/1 |
| 789 | dla | 2960K | 2132K | sleep | 58 | 0 | 0:00.00 | 0.1% | xterm/1 |
| 217 | root | 1908K | 1100K | sleep | 53 | 0 | 0:00.00 | 0.1% | nscd/7 |
| 312 | root | 1936K | 660K | sleep | 48 | 0 | 0:00.00 | 0.1% | mibisa/12 |
| 397 | root | 64M | 47M | sleep | 59 | 0 | 0:00.07 | 0.0% | perfmeter/1 |
| 790 | dla | 808K | 628K | sleep | 41 | 0 | 0:00.00 | 0.0% | sh/1 |
| 177 | root | 1576K | Ok | sleep | 30 | 0 | 0:00.00 | 0.0% | lockd/1 |
| 229 | root | 2692K | Ok | sleep | 48 | 0 | 0:00.00 | 0.0% | lpscheed/1 |
| 165 | root | 1940K | 696K | sleep | 58 | 0 | 0:00.00 | 0.0% | in.named/1 |
| 250 | root | 804K | 480K | sleep | 58 | 0 | 0:00.00 | 0.0% | utmpd/1 |
| 188 | root | 2720K | 664K | sleep | 58 | 0 | 0:00.00 | 0.0% | automountd/5 |
| 143 | root | 2144K | 672K | sleep | 58 | 0 | 0:00.00 | 0.0% | rpcbind/1 |
| 129 | root | 1552K | 300K | sleep | 59 | 0 | 0:00.00 | 0.0% | in.ndpd/1 |
| 122 | root | 1304K | 220K | sleep | 58 | 0 | 0:00.00 | 0.0% | in.routed/1 |
Total: 64 processes, 负载平均: 0.11, 0.04, 0.05
$

`prstat` 命令参数允许你通过 PID、所有者的 UID、正在使用的 CPU 等选择要监控的进程。表 7.2 列出了 `prstat` 命令的参数。

### 表 7.2：prstat 命令行参数

| 参数 | 描述 |
| :--- | :--- |
| -a | 显示进程和用户的单独报告。 |
| -c | 打印新报告而不是覆盖初始报告。 |
| -C sets | 仅报告绑定到指定处理器集的进程。 |
| -L | 报告每个 LWP（轻量级进程）。 |
| -m | 报告微状态信息。 |
| -n number | 将报告限制在窗口或终端中的 `number` 行。默认使用整个显示区域。 |
| -p pids | 仅报告 PID 在 `pids` 列表中列出的进程。 |
| -P cpus | 仅报告在 `cpus` 列出的 CPU 上执行的进程。 |
| -R | 在实时模式下执行 `prstat`。 |
| -s key | 根据键（cpu, time, size, rss, 或 pri）降序排序报告。 |
| -S key | 根据键升序排序报告。 |
| -t | 报告每个用户的总使用摘要。 |
| -u euids | 仅报告有效 UID 在 `euids` 列表中列出的进程。 |
| -U u | 仅报告实际 UID 在 `uids` 列表中列出的进程。 |
| -v | 使用详细模式报告，包括在用户模式和系统模式下的时间百分比。 |

以下示例使用 `prstat` 命令列出具有 `dla` 用户账户的进程：

```
$ prstat -c u dla

PID USER SIZE STATE NICE TIME CPU PROCESS/NLWP

9830 812K 696K cpu 48 0 00:00.00 0.2% prstat/1

9789 230 2906K sleep 59 0 00:00.00 0.1% xterm/1

9790 808K 628K sleep 48 0 00:00.00 0.0% sh/1

Total: 3 processes, 3 leafs, load averages: 0.00, 0.01
```

> **注意**
>
> 请理解 `ps` 和 `prstat` 提供有关活动进程的信息。`ps` 命令提供更多面向用户的信息（如父进程 PID、TTY、启动日期等），而 `prstat` 命令提供更多面向系统的信息（如进程大小、优先级、CPU 利用率等）。

## kill 命令

`kill(1)` 命令通过向进程发送信号使其退出。许多不同类型的信号。用于终止进程的信号见表 7.3，完整的信号列表可以在 `signal(3)` 中找到。

### 表 7.3：用于终止进程的信号

| 符号名称 | 值 | 描述 |
| :--- | :--- | :--- |
| SIGHUP | 1 | 挂起 |
| SIGINT | 2 | 中断 |
| SIGKILL | 9 | 杀死 |
| SIGTERM | 15 | 终止（默认） |

### 表 7.4：常用的 pgrep 和 pkill 命令行参数

| 参数 | 描述 |
| :--- | :--- |
| -g Process ID | 匹配指定组 ID 的进程 |
| -G Real Group ID | 匹配指定组 ID 的进程 |
| -n | 仅匹配符合指定的最新进程 |
| -P Process ID | 匹配指定父 ID 的进程 |
| -s Session ID | 匹配指定会话 ID 的进程 |
| -t Terminal Device | 匹配指定设备路径进程 |
| -u Effective User ID | 匹配指定用户 ID 的进程 |
| -U Real User ID | 匹配指定用户 ID 的进程 |
| -v | 匹配所有不符合条件的进程 |
| -x | 精确匹配模式的进程 |

`pattern` 是根据程序名选择进程的正则表达式。以下行显示了使用 `ps(1)` 命令与 `pgrep` 命令获取进程 PID 的区别：

```
$ ps -eaf | grep root

root 2898 1096 0 pts/0 0:02 root

$ pgrep root
```

当你指定 `-f` 命令行参数配合 `pattern` 时，`pattern` 会与参数而非程序名进行比较。此外，如果你指定 `-x` 命令行参数，`pattern` 的正则表达式解释将被禁用，且必须精确匹配程序名。

所有类型的命令行参数都接受多个 ID（用逗号分隔）。在实际和有效用户 ID 以及实际组 ID (`-G`) 的情况下可以指定数字 ID 或账户名。

`pgrep` 命令支持额外的命令行参数。`-d` 命令行参数指定分隔符，当指定的 `pgrep` 标准匹配多个 PID 时使用。默认，该分隔符是换行符。以下列表显示使用 `pgrep` 命令列出 `dla` 账户拥有的进程以及指定空格作为分隔符的效果：

```
$ pgrep -u dla -d ' '
```

## 调度进程

有两个命令用于调度进程的自动执行：`cron(1)` 和 `at(1)`。

## cron 命令

`cron` 是系统启动时启动的一个守护进程。它负责在未来时间以及可能的定期计划执行命令。要执行的命令以标准的表格格式指定，并存储在称为 *crontab 文件* 的文件中。这些文件位于 `/var/spool/cron/crontabs` 目录下。

通过放在 crontab 文件中自动执行的命令被称为 **cron 任务**。在未来时间只执行一次的命令可以使用 `at` 命令提交，而不是修改 crontab。`at` 命令在下一节描述。

两类主要的 crontab 是系统 crontab（由 root、lp 等系统账户所有）和用户 crontab（由非管理员用户账户创建和维护）。

### 默认 cron 设置

与其他工具一样，你可以设置参数来控制 `cron` 命令的行为。这些设置列在 `/etc/default/cron` 文件中。如果 `/etc/default/cron` 文件包含以下条目，`cron` 命令将将其活动记录在 `/var/cron/log` 中：
`CRLOG=YES`

这是默认设置。要禁用日志，将 `YES` 改为 `NO` 并重启系统或使用 `/etc/init.d/cron rc` 脚本重启 cron。

### Crontab 文件

`/var/spool/cron/crontabs` 目录包含了系统和用户的 crontab 文件。这些文件的文件名与所有者的账户名相同。例如，`guest` 用户账户的 crontab 文件名为 `guest`。

crontab 文件包含多个条目，指定了要执行的命令以及执行的时间和频率。命令可以在一天的任何时间每天、每周或每月执行。

一个 crontab 条目由空格或制表符分隔的六个字段组成。星号 (`*`) 用作未使用的字段的占位符。表 7.5 列出了 crontab 条目的各个字段。

### 表 7.5：crontab 条目的字段

| 字段 | 取值 | 描述 |
| --- | --- | --- |
| minute | 0 到 59 | 小时内的分钟 |
| hour | 0 到 23 | 天中的小时 |
| day | 1 到 31 | 月的几号 |
| month | 1 到 12 | 年份 |
| weekday | 0 到 6 | 星期（0 = 周日） |
| command | 无 | 要执行的命令 |

以下列出了典型的 root crontab 文件内容：

```
10 3 * * 4 /etc/cron.d/logchecker
10 3 * * 0 /usr/lib/newsyslog
15 3 * * 0 /usr/lib/fs/nfs/nfsfind
1 2 * * * [ -x /usr/sbin/rtc ] && /usr/sbin/rtc -c
30 3 * * * [ -x /usr/lib/clean ] && /usr/lib/clean
```

注意，你可以通过逗号分隔来为某个字段指定多个值，如 `logchecker` crontab 条目中的 `weekday` 字段所示。在此示例中，`logchecker` 将在每周日和周四的早晨 3:10 执行。

> **考试警示**
>
> 系统管理员的一项关键技能是理解并使用 crontabs 来调度日志维护、系统备份和其他例行维护。

### 操作 Crontabs

你可以使用 `crontab(1)` 命令来创建、列出、编辑和删除 crontabs。`crontab` 命令的一项功能（编辑其他用户的 crontab 的能力）仅对超级用户可用。

当执行 `crontab` 而不带命令行参数时，它读取标准输入（通常是键盘）。当通过 `Ctrl+D` 终止命令时，输入的数据将用于为执行该 crontab 的用户账户创建（或覆盖现有的）crontab。当通过命令行参数指定文件名时，则将使用指定文件的内容来创建/覆盖该用户的 crontab。

当你使用带有 `-e` 命令行参数执行 `crontab` 时，将调用环境变量 `EDITOR` 指定的编辑器对用户 crontab 进行编辑。如果未设置 `EDITOR` 参数，则将使用 `ed(1)` 文本编辑器。这种机制允许编辑与调用用户账户相关的 crontab。

`crontab -l` 命令显示用户 crontab 的内容，而 `crontab -r` 则删除用户的 crontab。

> **考试警示**
>
> 当 cron 守护进程启动时，它会读取所有现有的 crontabs。因为它不直接读取 crontab 文件，除非使用 `crontab` 命令创建了更改，否则它不会感知到任何更改。`crontab` 命令会通知 cron 守护进程 crontab 已更改或添加。随后 cron 守护进程会更新其信息。

超级用户可以指定用户账户名来控制另一个用户账户的 crontab。该账户可以配合 `-l` 或 `-r` 命令行参数来列出或删除另一个用户的 crontab；但不要在使用 `-e` 命令行参数时指定账户名。

> **考试警示**
>
> 如果超级用户尝试通过使用 `crontab -e` 命令并指定账户名来修改另一个用户的 crontab，结果将是不可预测的。相反，请使用 `su(1)` 命令切换到另一个用户账户，然后使用 `crontab -e`。

### 访问控制

对 crontab 的访问由两个文件控制：`cron.allow` 和 `cron.deny`，这两个文件都位于 `/etc/cron.d` 目录下。这些文本文件包含了用户账户名列表（每行一个），允许或拒绝对命令的访问。

如果用户的账户名列在 `/etc/cron.d/cron.allow` 文件中，则允许该用户访问 crontab。如果 `cron.allow` 文件不存在，只要用户的账户名未列在 `/etc/cron.d/cron.deny` 文件中，就允许该用户访问。此外，如果两个文件都不存在，用户将被拒绝访问。

如果存在 `cron.allow` 或 `cron.deny` 之一，这些规则也适用于 root 账户。默认情况下，`/etc/cron.d/cron.deny` 文件会被创建并包含所有非管理用户账户。如果两个文件都不存在，只有超级用户可以提交作业。

注意，`/usr/lib/cron` 目录是 `/etc/cron.d` 目录符号链接。因此，可以使用任何路径访问 crontab 控制文件。即 `/etc/cron.d/cron.allow` 或 `/usr/lib/cron/cron.allow` 以及 `/etc/cron.d/cron.deny`。

## at 命令

在稍后时间执行命令的一种简单方法是使用 `at` 命令。`at` 命令的语法为：

```
at [time] command
```

`[time]` 参数指定执行命令的时间。你可以使用多种格式的时间：

- 一天中的（例如 `10:30 pm`, `22:30`）
- 相对时间（例如 `now`, `in 10 minutes`, `in 2 hours`）
- 日期（例如 `tomorrow`, `next Tuesday`, `2023-12-25`）

`command` 参数是将在指定时间执行的命令。该命令将被放入队列中，并在时间到达时执行。

你可以使用 `atq` 命令查看调度作业队列。要从队列中删除作业，使用 `atrm` 命令后跟作业号：

```
atrm [job_number]
```
