
```
# cd /
# find -depth cpio -o8 > /dev/st0
```

（注：原文中的 `find -depth cpio -o8` 看起来像是 `find -depth . -print -o8` 或类似命令，但根据要求不翻译代码块，故保持原样。）

```
# cd /
# find -depth cpio -o8 > /dev/st0
```

下一个命令从之前的备份中恢复 `/home` 目录中的文件。这些选项从归包中提取文件 `-x`，使用详细模式 `-v`，修改复制时间 `-m`，并根据需要创建目录 `-d`。星号（前面带有反斜杠）是这样 `shell` 不会扩展它，而是将其传递给 `cp`。

```
# cd /
# cpio -ivmd /home/* < /dev/st0
```

尽管所有程序对于简单备份都运行良好，但像 `amanda`（第 607 页）这样的实用工具提供了更复杂的备份和恢复系统。例如，要确定一个文件是否在归包中，你必须读取整个归包。如果归包跨越多个磁带，这个过程将变得格外繁琐。更复杂的工具（包括 `amanda`）在多个方面提供帮助，包括备份中文件的目录（或索引）。

## 从备份中排除目录

在实践中，你可能希望从备份过程中排除某些目录。例如，不备份 `/home` 或 `/var/tmp`（或其链接）可以节省归包空间。此外，不要备份 `proc` 中的文件。因为 `/proc` 不是真正的磁盘文件系统，而是 Linux 内核提供操作系统和内存信息的一种，你不需要备份从其他系统挂载的文件系统。

`dump` 实用工具（`dump` 包）首次出现在 UNIX 版本 6 中。它可以备份整个文件系统、目录层次结构或单个文件。`restore` 工具随后可以恢复之后更改的文件。调度某些任务自动运行是一个良好的习惯。例如，你可能想每周删除一次旧文件，每月汇总会计数据，并每月轮换系统日志。

## cron 为一个停止

`cron` 守护进程假设系统始终在运行。类似的实用工具 `anacron` 不做该假设，非常适合经常关闭的便携式计算机。`anacron` 工具使用来自 `/etc/anontab` 文件的指令，除非另有规定（注：此处原文 `/etc/anontab` 疑为 `/etc/anontab`）。`anacron` 工具使用来自 `/etc/anontab` 文件的指令，除非另有规定。

## cron 为一个停止

`cron` 守护进程假设系统始终在运行。类似的实用工具 `anacron` 不做该假设，非常适合经常关闭的便携式计算机。`anacron` 工具使用来自 `/etc/anontab` 文件的指令，除非另有规定。

`anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `ontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `anontab` `ontab`（此处原文存在大量重复，跳过翻译）。

## cron 为一个停止

`cron` 守护进程假设系统始终在运行。类似的实用工具 `anacron` 不做该假设，非常适合经常关闭的便携式计算机。`anacron` 工具使用来自 `/etc/anontab` 文件的指令，除非另有规定。

## cron 为一个停止

`cron` 守护进程假设系统始终在运行。

`cron` 守护进程读取。这五个字段让 `cron` 守护进程执行命令。要获取更多信息，请查看 `cron` 手册第 5 节。

### CRONTAB 文件

`cron` 守护进程读取 `/etc/crontab` 中的命令。`/etc/crontab` 中描述任务的行具有以下格式：

```
minute hour day-of-month month-of-week user command
```

前五个字段指示了 `cron` 何时执行命令。分钟是小时开始后的分钟数，小时是基于 24 小时制的，月份是 1 到 31 的数字，星期是 0 到 7 的数字（其中 0 和 7 表示星期日）。星号 `*` 代表字段中的任何值。用户是运行该任务的用户名或用户 ID。命令应指定绝对路径以确保 `cron` 执行的是正确的命令。

在 `/etc/crontab` 文件中，以下是某些示例：

```
20 1 * * root /usr/local/bin/checkit
25 19 * * root /usr/local/bin/monthly.check
40 23 * * root /usr/local/bin/sunday.check
10/* * * * root /usr/local/bin/tenmin.check
```

所有行都以 `root` 权限运行。第一行每月 7 号凌晨 1:20 执行 `check`。第二行在周日的上午 9:25 执行 `monthly.check`。第三行在每周日日的晚上 23:40 执行 `sunday.check`。第四行使用语法每十分分钟运行 `tenmin.check`；`10/*` 等同于 `0,10,20,30,40,50`。要获取更多信息，请查看 `cron` 手册第 5。

用户 `crontab` 文件的格式与系统 `crontab` 文件相同，但它不包含用户字段，因为它始终作为运行它的用户运行。用户可以通过给出 `cron` 命令并带有选项来操作自己的 `crontab` 文件：`-l` 列出文件，`-r` 删除文件，`-e` 编辑文件。`e` 选项默认使用 `vi` 编辑器；如果你有偏好，可以导出并使用 `VISUAL` 或 `EDITOR` 环境变量指定你选择的文本编辑器。查看 `cron` 手册可以获取更多信息。

`/etc/crontab` `cron` 守护进程锁定 `/etc/crontab` 和 `/etc/cron.d` 目录下的 `crontab` 文件。默认是 `/etc/crontab` 文件，它不运行任何任务：

```
$ /etc/crontab
SHELL=/bin/bash
PATH=/bin:/sbin:/usr/bin
MAILTO="
```

# 任务调度 613

`/etc/cron.d/0Hourly` 按照安装情况，`/etc/cron.d` 目录包含两个 `crontab` 文件：`smolt`（用于跟踪硬件）和 `0Hourly`。以下是默认的 `/etc/cron.d/0Hourly` `crontab` 文件：

```
$ cat /etc/cron.d/0Hourly
SHELL=/bin/bash
PATH=/bin:/bin:/usr/sbin:/usr/bin
MAILTO=root
01 * * * * run-parts /etc/cron.hourly
```

`run-parts` 在设置某些变量后，该脚本以 `root` 权限执行 `run-parts`。行开头的 `01 * * * *` 导致 `cron` 在每小时开始一分钟后运行该作业。`run-parts` 工具运行其参数所指定目录（`/etc/cron.hourly`）中的可执行文件。这些文件执行的输出将通过 `MAILTO` 发送用户。

`/etc/cron.hourly/` 按照安装情况，`/etc/cron.hourly/` 中有一个文件：`0anacron`。以下是默认的 `0anacron` `/etc/cron.hourly/0anacron` 壳脚本：

```
$ cat /etc/cron.hourly/0anacron
!/bin/bash
# 以防文件不存在
if test -r /var/spool/anacron/cron.daily; then
  day=$(cat /var/spool/anacron/cron.daily)
fi
if [ `date +%Y%m%d` = "$day" ]; then
  exit 0
fi
```

```
# 如果 anacron 已经在运行，
# 将会有日志（守护进程不会运行两次）。
if test -x /usr/bin/on_ac_power; then
  /usr/bin/on_ac_power & > /dev/null
if test $? -eq 1; then
  exit 0
fi
```

```
/usr/sbin/anacron -s
```
