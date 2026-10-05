

## 任务调度 605

为 '.?' 设置所有者/模式 [yn]

当您恢复整个文件系统或意外删除的文件时，请在此提示符处回答 `y`。这将为正在恢复的文件和目录恢复适当的权限。如果您将转储（dump）恢复到转储目录以外的其他目录，请回答 `n`。此时，所有者将设置为执行恢复的用户（通常是 root）。

可以使用多种设备名称访问 `/dev/st0`。每个名称访问一个不同的设备号，这些设备号控制磁带驱动器使用的的某些方面。在完成使用 `/dev/st0` 的转储后，磁带驱动器会自动回带。使用非回带 SCSI 磁带设备 (`/dev/nst0`) 可以在完成后保持磁带不回带。此功能允许您将多个文件系统备份到同一个卷。

以下是一个备份系统的示例，其中 `/home`、`/usr` 和 `/var` 目录位于不同的文件系统：

```
$ dump -ouf /dev/nst0 /home
$ dump -ouf /dev/nst0 /usr
$ dump -ouf /dev/st0 /var
```

上述示例对前两个转储使用了非回带设备。如果您使用回带设备，磁带会在每次转储后回带，导致磁带上只剩下最后一次转储。

您可以使用 cio 包中的 `mt`（磁带工具）来操作多变量转储磁带上的文件。以下 `mt` 命令为磁带定位（`fsf 2` 指令 `mt` 跳过两个文件，磁带位于第三个文件的开头）。`restore` 命令恢复上例中的 `/var` 文件系统：

```
$ mt -f /dev/st0 fsf 2
$ dump restore rf /dev/st0
```

## 任务调度

将某些任务设置为自动运行是一个良好的习惯。例如，您可能希望每周删除一次旧的核心文件，每天汇总会计数据，每月轮系统日志文件。

## cron 与 anacron：调度常规任务

cron 守护进程定期执行计划的命令。在始终运行的系统上，此守护进程可以在特定时间执行命令。`anacron` 工具在被调用时执行计划的命令。它在笔记本和其他并非一直开启的系统中运行良好。调用 `anacron` 的 `anacron` 初始化脚本在系统使用电池运行（即未接交流电）时将不会执行命令。

## CRONTAB 文件

cron 守护进程通过读取 `/var/spool/cron/crontab` 中的个人 crontab 文件来执行任务。用户可以使用 `crontab` 工具设置个人 cron 文件，这些文件被保存在 `/etc/cron` 目录和 `/etc/crontab` 文件中。`crontab` 一词有三个含义：它指的是特定格式的文件 [a crontab]，它也是一个文件 [/etc/crontab] 的名称。

默认情况下，Ubuntu 设置对 cron 以该格式运行命令没有任何限制。请查看第 491 页的 `cron.allow` 和 `cron.deny` 以了解限制此类访问的方法。

系统 crontab 文件指定了 cron 运行命令的频率。在系统 crontab 文件（如 `/etc/crontab`）中，具有如下格式：

分钟 日期 月 星期几 用户 命令

前五个字段表示 cron 何时执行该命令。分钟是整点开始后的分钟数，小时是基于 24 小时制的小时，日期是 1 到 31 的数字，星期几是 0 到 7 的数字（其中 7 表示星期日）。星号 (*) 表示字段中的任何值。用户是运行该命令的用户名或 ID。以下是一些示例：

```
* 20 1 * * root /usr/local/bin/check
25 9 17 * * /usr/local/bin/monthly.check
40 23 * * 7 root /usr/local/bin/sunday.check
```

三行都以 root 权限运行命令。第一行每天凌晨 1:20 运行 `check`。第二行在每月 17 号上午 9:25 运行 `monthly.check`。第三行在晚上 23:40 运行 `sunday.check`。给出 `man crontab` 命令获取更多关于 crontab 文件的信息。

用户 crontab 文件：系统文件不包含用户字段，因为它始终作为创建它的用户运行。用户可以使用 `crontab` 命令处理自己的 crontab 文件：`-l` 列出文件，`-r` 文件，`-e` 编辑文件。此命令使用 nano 编辑器；如果您习惯，可以使用 `export`（第 992 页）并使用 `EDITOR` 环境变量指定您的文本编辑器。更多信息请参 `crontab man`。

/etc/crontab：以下是 `/etc/crontab` 文件。注释以井号 (#) 开头。文件设置了 `SHELL` 和 `PATH`（第 319 页）环境变量。

```
$ /etc/crontab
# /etc/crontab: 系统 crontab
# 与其他 crontab 不同，你不需要运行 'crontab'
# 命令来安装编辑此文件以及 /etc/cron.d 中的文件。
# 这些文件也有像其他 crontabs 那样的用户名字段。
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin
```

## 任务调度 607

```
# dom dow user command
17 * * * root cd /run-parts --report /etc/cron.hourly
25 6 * * root test -x /usr/sbin/anacron (cd /run-parts --report /etc/cron.daily)
47 6 * * root test -x /usr/sbin/anacron (cd /run-parts --report /etc/cron.weekly)
52 1 * * root test -x /usr/sbin/anacron (cd /run-parts --report /etc/cron.monthly)
```

run-parts：`run-parts` 工具运行作为参数的目录中的可执行文件。`--report` 影响产生输出的命令。它将命令名称发送标准输出或错误输出——取决于哪个先输出。守护进程每小时 17 分运行以 17 开头的行。逻辑运算符 `&&` 然后执行 `run-parts`，它执行 `/etc/cron.hourly` 目录中的所有文件。下一行测试 `/usr/sbin/anacron` 是否执行。如果文件可执行，逻辑运算符 `||` 导致 shell 忽略行的剩余。然后，如果 anacron 已安装且可执行，此文件仅执行行以及 `cron.hourly` 目录中的文件。如果 anacron 未安装或不可执行，这三行中的每一行都会 `cd` 到 `/root` 并执行指定目录中的文件。

/etc/cron.d/anacron：除了 crontab 文件外，cron 还读取 `/etc/cron.d` 中的文件来执行命令。以下情况每天上午 7:30 运行一次 anacron。此脚本在系统运行且未使用电池时运行 anacron：

```
$ /etc/cron.d/anacron
# anontab: anacron 的 crontab 条目
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin
# 30 7 * * root test -x /usr/sbin/invoke-rc.d anacron start >/dev/null
30 7 * * root start -q anacron
```

运行 SysInit 脚本的行被注释掉，并替换为在 `/etc/init/anacron` 中运行 anacron 守护进程的行，由 Upstart（第 432 页）触发。当 anacron 运行时，它从 `anontab` 文件读取要执行的命令。`anacron` 工具跟踪每个任务最后调用的时间，它可以告知应运行哪些任务。此文件在运行 anacron 的系统上执行 `cron.daily`、`cron.weekly` 和 `cron.monthly` 目录中的文件。

```
$ /etc/anontab
# anontab: anacron 的配置文件
# anontab 中的 cron.daily 任务在 anacron 启动 5 分钟后每天执行可执行文件。如果系统在上午7:30 运行，/etc/cron.d/anacron 调用 anacron 初始化脚本，此任务在上午 7:35 运行。当 Ubuntu 启动时，rc 脚本调用 anacron 初始化脚本。如果系统在上午 7:30 未运行，cron.daily 任务至少一天未运行，且权限已更改为非电池运行，该任务将在系统启动 5 分钟后运行。

## 在正确的时间运行任务

按照安装情况，如果 `/usr/bin/anacron` 文件存在且可执行，cron 将使用 anacron 尽快运行每日、每周和每月任务。请参阅第 607 页的“run-parts”和关于 `/etc/anontab` 的章节。一种简单的方法是更改权限使其不可执行：

```
$ sudo chmod 644 /usr/bin/anacron
```

