

+   27. 通过输入以下命令杀死 xeyes 程序

```
killall xeyes
```

## Part II: 修改进程优先级

要修改进程优先级，请执行以下操作：

+   1. 通过输入以下命令在后台启动 xeyes 程序
+      ```
+      xeyes&
+      ```
+   2. 记录 xeyes 的 PID（在终端窗口中显示）：
+   3. 通过输入以下命令查看正在运行的进程
+      ```
+      ps lf
+      ```
+      注意 nice 值（NI）目前为 0。
+   4. 通过输入以下命令将进程的优先级提高到 nice 值为 -5
+      ```
+      renice -5 -p xeyes PID
+      ```
+      注意普通用户无法将 nice 值更改到 0 以下，只能为 0–20。
+   5. 切换到用户 root（su -，密码 noV3ll）。
+   6. 通过输入以下命令再次尝试将 nice 值设置为 -5
+      ```
+      renice -5 -p xeyes PID
+      ```
+   7. 通过输入以下命令检查设置是否生效
+      ```
+      ps lf (lowercase L)
+      ```
+      注意进程未显示，因为 ps lf 仅显示当前用户启动的进程。xeyes 程序是由 geeko 启动的（不是 root）。
+   8. 通过输入以下命令查看所有进程
+      ```
+      ps alf
+      ```
+      xeyes 进程现在显示出来了。
+   9. 通过输入以下命令将 xeyes 进程的 nice 值更改为更高优先级
+      ```
+      renice -10 -p xeyes PID
+      ```
+   10. 通过输入以下命令验证 xeyes 进程的 nice 值是否设置为 -10
+       ```
+       ps alf (lowercase L)
+       ```
+   11. 通过输入以下命令退出以 root 身份运行的 shell
+       ```
+       exit
+       ```
+       你现在应该再次成为用户 geeko。
+   12. 通过输入以下命令以 nice 值为 +10 在后台启动 xeyes 程序
+       ```
+       nice xeyes&
+       ```

+   13. 通过输入以下命令验证此新的 xeyes 进程的 nice 值是否设置为 +10

```
ps -lf (lowercase L)
```

+   14. 通过输入以下命令杀死 xeyes 进程

```
killall xeyes
```

## Objective 5—调度作业

大多数 SUSE Linux Enterprise Desktop 管理员和用户发现他们需要在运行的系统上定期执行某些任务（例如更新数据库或备份数据）。你可以通过以下方式在 Linux 中自动化这些作业：

- Schedule a Job (cron)
- Run a Job One Time Only (at)

### Schedule a Job (cron)

你可以使用 cron 服务（/usr/sbin/cron）按计划安排作业。默认情况下，cron 在 SUSE Linux Enterprise Desktop 10 上已激活。

该服务作为守护进程运行，每分钟检查一次是否已为当前时间定义了作业。

包含作业列表的文件称为 crontab。系统存在一个 crontab，以及为系统上定义的每个用户存在一个 crontab。

/etc/sysconfig/cron 文件包含 cron 启动的一些脚本的配置变量。

cron 可以定义两种类型的作业：

- System Jobs
- User Jobs

**System Jobs** 你使用 /etc/crontab 文件控制系统作业。安装后，该文件中只定义了一个作业，该作业在表 10-16 中所示目录中的脚本按所示间隔运行。

| Directory | Interval |
|---|---|
| /etc/cron.hourly | Jobs are run on an hourly basis. |
| /etc/cron.daily | Jobs are run on a daily basis. |
| /etc/cron.weekly | Jobs are run on a weekly basis. |
| /etc/cron.monthly | Jobs are run on a monthly basis. |

Table 10-16

你可以向 /etc/crontab 添加行，但不应删除安装时添加的行。

![](img/9129877170834ca9d5fdac5319bf5f12_370_0.png)

要获取 /etc/crontab 语法的详细描述，请输入 `man 5 crontab`。

从 /etc/crontab 文件调用的脚本不仅确保脚本在规定间隔运行（由 /usr/lib/cron/run-crons 脚本处理），而且如果无法在指定时间运行作业，则作业会在稍后运行。

例如，如果由于计算机已关闭而无法在指定时间运行脚本，则脚本会使用 /etc/crontab 中的设置自动稍后运行。

这仅适用于在 cron.hourly、cron.daily、cron.weekly 或 cron.monthly 中脚本中定义的作业。

上次运行作业的信息保存在 /var/spool/cron/lastrun/ 目录中的文件中，例如 cron.daily。文件的时间戳由 /usr/lib/cron/run-crons 脚本评估，以确定是否需要运行脚本。

在标准安装中，只有 /etc/cron.daily/ 目录包含脚本，如下所示：

```
da10:~ # ls -l /etc/cron*
-rw------- 1 root root   11 2006-05-08 20:47 /etc/cron.deny
-rw-r--r-- 1 root root  255 2006-05-08 20:47 /etc/crontab

/etc/cron.d:
total 0

/etc/cron.daily:
total 32
-rwxr-xr-x 1 root root  393 ... logrotate
-rwxr-xr-x 1 root root  948 ... suse-clean_catman
-rwxr-xr-x 1 root root 1875 ... suse.de-backup-rc.config
-rwxr-xr-x 1 root root 2059 ... suse.de-backup-rpmdb
-rwxr-xr-x 1 root root  566 ... suse.de-check-battery
-rwxr-xr-x 1 root root 1320 ... suse.de-clean-tmp
-rwxr-xr-x 1 root root  371 ... suse.de-cron-local
-rwxr-xr-x 1 root root 1196 ... suse.do-manbd

/etc/cron.hourly:
total 0

/etc/cron.monthly:
total 0

/etc/cron.weekly:
total 0
```

这些 shell 脚本在你更新系统时会覆盖。更新这些文件时，你对这些文件所做的任何修改都会丢失。

因此，建议将你自己的添加和修改写入 /root/bin/cron.daily.local（参见 /etc/cron.daily/suse.de-cron-local），因为在更新系统时不会覆盖此脚本。

其他系统作业文件可以存储在 /etc/cron.d/ 目录中。这些文件必须与 /etc/crontab 具有相同的格式。/etc/cron.d 中定义的作业不会在稍后自动运行。

### User Jobs

各个用户的作业存储在 /var/spool/cron/tabs/ 目录中，与用户名匹配的文件中。这些文件始终属于用户 root。用户使用 crontab 命令创建自己的作业。

表 10-17 显示了 crontab 命令的选项。

| Option | Description |
|---|---|
| `crontab -e` | Creates or edits jobs. The vi editor is used. |
| `crontab file` | The specified file contains a list of jobs in the proper format and replaces any existing crontab file for that user. |
| `crontab -l` | Displays current jobs. |
| `crontab -r` | Deletes all jobs. |

# Table 10-17

文件中每一行定义一个作业。行中有六个字段。

前五个字段定义时间；最后一个字段包含要运行的命令。这可以是任何类型的命令或 shell 脚本。但是，命令或 shell 脚本运行时没有用户交互。

表 10-18 中显示的前五个字段具有以下格式：

| Field | Range |
|---|---|
| Minutes | 0–59 |
| Hours | 0–23 |
| Day of the Month | 1–31 |
| Month | 1–12 |
| Weekday | 0–7 |

# Table 10-18

配置这些字段的指导原则如下：

- 如果你希望作业每分钟（每小时、每天、每月）运行，请在相应字段中输入星号 (*)。
- 你可以在字段中包含多个条目，用逗号分隔。
- 你可以使用连字符分隔的开始和结束值指定范围。
- 你可以使用 `/n` 配置时间步长（其中 `n` 代表步长大小）。
- 你可以通过其前三个字母指定月份和星期几（不区分大小写）。但是，使用字母时，不能使用范围或列表。
- 代表星期几的数字从星期日的 0 开始，依次运行整个星期，7 再次代表星期日。例如，3 是星期三，6 是星期六。

cron 作业条目的示例如下：

```
*/10 8-17 * * 1-5 /usr/bin/fetchmail mailserver
```

在此示例中，每 10 分钟（*/10）在 8.00 至 17.00（8-17）之间，从星期一到星期五（1-5）运行 `fetchmail` 命令，以从计算机 mailserver 获取传入电子邮件。

对于系统作业，必须在 /etc/crontab 文件中指定具有运行命令权限的用户，通过在时间详细信息（前五个字段）与命令名称（现在成为第七个字段）之间输入用户名。

### Run a Job One Time Only (at)

如果你只想运行一次作业（而不是使用 cron 定期安排），可以使用 `at` 命令。要使用 `at`，你必须确保 `atd` 服务已启动（`rcatd start`）。

两个文件决定哪些用户可以运行此命令：

- `/etc/at.allow`—在此处输入的用户可以定义作业。
- `/etc/at.deny`—未在此文件中列出的用户可以定义作业。

这些文件是你可以修改或创建的文本文件。
默认情况下，/etc/at.deny 文件已存在，其条目如下所示：

```
dalo:~ # cat /etc/at.deny
alias
backup
bin
daemon
ftp
games
...
```

如果 /etc/at.allow 文件存在，则仅评估此文件。如果这两个文件都不存在，则只有用户 root 可以使用 at 定义作业。

你可以通过在命令提示符下输入以下命令来定义作业
at *launch_time*（其中 *launch_time* 是你希望作业开始的时间，例如 12:34）。

此时，你将被置于一个特殊环境中，在其中逐行输入命令。完成输入命令后，通过按 Ctrl+d 保存作业。

以下是使用 at 命令创建作业的示例：

```
geeko@da10:~> at 21:00
warning: commands will be executed using /bin/sh
at> /home/geeko/bin/doit
at> mail -s "Results file of geeko" geeko@da10 < /home/geeko/results
at> <EOT>
job 4 at 2004-08-27 21:00
```

如果要执行的命令包含在文本文件中，则需要输入 `at --file launch_time`（其中 *file* 是文件的路径名）。

