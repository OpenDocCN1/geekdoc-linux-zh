
# 16.1. at

```
root@laika:-# at 22:01

at> date

at> <EOT>

job 1 at Wed Aug 22:01:00 2007

root@laika:-# at 22:03

at> sleep 10

at> <EOT>

job 2 at Wed Aug 22:03:00 2007

root@laika:-#
```

在现实生活中，我们希望你调度的是更有用的的命令 :-)

## 16.1.2. atq

可以使用 `atq` 或 `at -l` 命令轻松检查任务的调度时间。

```
root@laika:-# atq

1 Wed Aug 22:01:00 2007 a root

2 Wed Aug 22:03:00 2007 a root

root@laika:-# at -l

1 Wed Aug 22:01:00 2007 a root

2 Wed Aug 22:03:00 2007 a root

root@laika:-#
```

`at` 命令可以理解英文单词，如 `tomorrow` 和 `bedtime`，用它们在明天或下午四点调度命令。

```
root@laika:-# at 10:05 tomorrow

at> sleep 100

at> <EOT>

job 5 at Thu Aug 22 10:05:00 2007

root@laika:-# bedtime

at> date

at> <EOT>

job 6 at Thu Aug 22 16:00:00 2007

root@laika:-# atq

6 Thu Aug 22 16:00:00 2007 a root

5 Thu Aug 22 10:05:00 2007 a root

root@laika:-#
```

## 16.1.3. atrm

laika: 队列中的任务可以使用 `atrm` 删除。

```
root@laika:-# atq

6 Thu Aug 22 16:00:00 2007 a root

5 Thu Aug 22 10:05:00 2007 a root

root@laika:-# atrm 5

root@laika:-# atq

6 Thu Aug 22 16:00:00 2007 a root

root@laika:-#
```

## 16.1.4. at.allow 和 at.deny

你还可以使用 `/etc/at.allow` 和 `/etc/at.deny` 文件来管理谁可以使用 `at` 调度。

`/etc/at.allow` 文件可以包含允许调度 `at` 任务的用户列表。当 `/etc/at.allow` 不存在时，除非用户名列在 `/etc/at.deny` 中，否则所有人都可以使用 `at`。

如果这些文件都不存在，所有人都可以使用 `at`。

# 16.2. cron

## 16.2.1. crontab 文件

可以使用 `crontab` 命令维护 `crontab` 文件。每个用户都可以拥有自己的 `crontab` 文件在特定时间调度任务。该时间可以通过五个字段指定：分钟、小时、日期、月份和星期。如果某个字段包含星号 (`*`)，则表示该字段的所有值。

以下示例表示：在每月的每个周日的 14 点运行 `script`。

```
8 14 * * * script
```

每月第一日的午夜 25 分运行 `script`。

```
25 0 * * * script
```

周日每两分钟运行一次 `script`（`0` 和 `7` 都指周日）。

```
*/2 * * * 0
```

除了这五个字段外，你还可以输入以下之一：`@reboot`、`@yearly`（或 `@annually`）、`@monthly`、`@weekly`、`@daily`（或 `@midnight`）以及 `@hourly`。

## 16.2.2. crontab 命令

用户不应直接编辑 `crontab` 文件，而应该输入 `crontab -e`，这将使用 `EDITOR` 或 `VISUAL` 环境变量定义的编辑器。用户可以使用 `crontab -l` 显示他们的 cron 表。

## 16.2.3. cron.allow 和 cron.deny

cron 进程读取 cron 表时会考虑 `/etc/cron.allow` 和 `/etc/cron.deny` 文件。

这些文件的工作方式与 `at.allow` 和 `at.deny` 。当 `cron.allow` 文件存在时，你的用户名必须在其中，否则你无法使用 `cron`。当 `cron.allow` 文件不存在时，如果你想使用 `cron`，你的用户名不能出现在 `cron.deny` 文件中。

## 16.2.4. /etc/crontab

`/etc/crontab` 文件包含了运行小时/每日/每月任务的条目。它看起来像这样：

```
SHELL=/bin/sh

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin

20 3 * * * root      run-parts /etc/cron.daily

40 3 * * 7 root      run-parts /etc/cron.weekly

55 3 1 * * root      run-parts /etc/cron.monthly
```

## 16.2.5. /etc/cron.*

接下来显示的目录包含了在 `/etc/crontab` 指定时间运行的任务。`/etc/cron.d` 目录用于特殊情况，调度比小时/每日/每月需要更精细控制的任务。

```
paul@laika:~$ ls -ld /etc/cron.*

drwxr-xr-x 2 root root 4096-Aug 11 09:14 /etc/cron.d

drwxr-xr-x 2 root root 4096-Aug 11 15:04 /etc/cron.daily

drwxr-xr-x 2 root root 4096-Aug 11 09:14 /etc/cron.hourly

drwxr-xr-x 2 root root 4096-Aug 11 09:14 /etc/cron.monthly

drwxr-xr-x 2 root root 4096-Aug 11 09:14 /etc/cron.weekly
```

## 16.2.6. /etc/cron.*

注意 Red Hat 使用 `anacron` 来调度每日、每周和每月任务。

```
root@rhel6:~ cat anacontab

# /etc/anacontab: anacron 配置文件

# 详情见 anacron (8) 和 anacontab (5)。

SHELL=/bin/sh

PATH=/bin/usr/sbin:/bin

MAILTO=root

# 基础任务的最大延迟

RANDOM_DELAY=45

# 任务将在以下小时内启动

START_HOURS_RANGE=3-22

@period in days      delay in minutes    job-identifier      command

1               5               cron.daily         run-parts /etc/cron.daily

7               25              cron.weekly        run-parts /etc/cron.weekly

@monthly        45              cron.monthly        run-parts /etc/cron.monthly

root@rhel6:/etc#
```

# 16.3. 练习：调度

1. 使用 `at` 调度两个任务，显示队列并删除任务。
2. 作为普通用户，使用 `crontab -e` 调度一个每四分钟运行一次脚本。
3. 作为 root，显示普通用户的 `crontab` 文件。
4. 再次作为普通用户，删除你的 `crontab` 文件。
5. 查看 `/etc` 中的 cron 文件和目录并理解它们。`run-parts` 是做什么的？

# 16.4. 解答：调度

1. 使用 `at` 调度两个任务，显示队列并删除任务。

```
root@rhel5 ~# at 9 today

at> echo go to bed >> /root/todo.txt

at> <EOT>

job 1 at 2010-11-14 21:00

root@rhel5 ~# at 17:31 today

at> echo go to lunch >> /root/todo.txt

at> <EOT>

job 2 at 2010-11-14 17:31

root@rhel5 ~# rm 1

root@rhel5 ~# at

2 2010-11-14 17:31 a root

root@rhel5 ~# date

Sun Nov 14 17:31 CET 2010
```
