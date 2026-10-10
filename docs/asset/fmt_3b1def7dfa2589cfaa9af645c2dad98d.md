
`/etc/cron.daily` 目录中的所有文件都会每天凌晨 4:02 以 `root` 用户身份执行。

上述 `/etc/crontab` 文件的其余行将在周日凌晨 4:22 运行 `cron` 目录中的文件，并在每月第一天的凌晨 4:42 运行 `/etc/cron.monthly` 目录中的所有文件（此处原文为 `/etc/crontab`）。

由于 `/etc/crontab` 按日、每周和每月组织任务，你可以将脚本文件复制到相应的目录，使其按照系统 `cron` 表确定的计划运行。要每天运行一个名为 `myscript` 的脚本，请将文件复制到 `/etc/cron.daily` 目录。

## 管理系统进程

你也可以在 `/etc/cron.d` 目录中放置具有相同信息的 `cron` 表。在此目录下发现的任何与 `/etc/crontab` 格式相同的 `cron` 表都会由系统运行。如果某个任务需要按小时、每天、每周或每月间隔运行，则需要此操作。例如，如下所示，`cron` 守护进程通过 `/etc/cron.d/sysstat` 文件每 10 分钟以 `root` 用户身份运行 `sal` 命令。

```
[root@localhost]# cat /etc/cron.d/sysstat
# 每 10 分钟运行系统活动统计工具
*/10 * * * root /usr/lib/sa/sal 1
[root@localhost]# _
```

注意上述输出，第一列使用了特殊符号 `*/10`，用于表示每隔 10 分钟间隔的所有分钟。相反，你也可以使用 `0-59/10` 来指定从第 0 分到第 59 分每隔 10 分钟运行一次 `sal` 命令。

## 10-36 CompTIA Linux+ 认证， 2004 目标

执行吧！

## C-2: 使用 at 和 crontab 调度进程

| 如下所示 | 理由如下 |
| :--- | :--- |
| 1. 按 `CTRL + ALT + F2` | 为了切换到命令行终端 (`tty2`)。 |
| 2. 以 `root` 身份登录 | 为了调度进程在一分钟后运行。 |
| 3. 输入 `at -n + 1 minute` | 当 `at>` 提示符出现时。 |
| 4. 输入日期 | 当第二个 `at>` 提示符出现时。 |
| 5. 输入用户 | (当第三个 `at>` 出现时。) 以完成调度并观察输出。 |
| 6. 按 `CTRL + d` | 为了检查你的邮件。 |
| 7. 一分钟后，输入 `mail` | 在屏幕顶部。 |
| 注意消息数量 | 你应该看到主题为 "Output from your job." 的提示。 |
| 输入该数字 | |
| 观察输出 | |
| 8. 按 `q` | 完成后，在 `at>` 提示符。 |
| 按回车键 | 退出邮件。 |
| 9. 输入 `crontab -l` | 为了尝试列出你的 `cron` 表。 |
| 10. 输入 `crontab -e` | 为 `root` 用户编辑新的 `cron` 表。 |
| 11. 添加以下行： | |
| `30 20 * * * /bin/false` | |
| 12. 更新文件并退出 | 为了列出你的 `cron` 表。 |
| 13. 输入 `crontab -l` | 从 `cron` 目录列出你的 `cron` 表。 |
| 14. 输入以下命令： | |
| `cat /var/spool/cron/root` | |
| 15. 输入 `crontab -r` | 删除你的 `cron` 表。 |
| 16. 输入 `crontab -l` | 观察输出。 |
| 17. 输入 `exit` | 退出 `shell`。 |

## 单元总结：管理进程

**主题 A**

在此主题中，你学习了进程是程序的执行实例。你学习了用户进程运行在相同的终端中。你学习了（此处原文逻辑略有缺失，根据上下文推断为关于 `cron` 表的配置）。

**主题 B**

在此主题中，你学习了（关于在 `/etc/cron.d` 目录下放置 `cron` 表）。

**主题 C**

在此主题中，你学习了（关于任务调度和优先级控制）。

## cron 表的格式

- 题目

1. 格式：

`* * * * * /etc/cron.hourly`

`/etc/cron.hourly` 目录中的所有文件都会每天每小时的整点后一分钟以 `root` 用户身份执行。

同样地：

`* * * * * /etc/cron.daily`

`/etc/cron.daily` 目录中的所有文件都会每天凌晨 4:02 以 `root` 用户身份执行。

上述 `/etc/crontab` 文件的其余行将在周日凌晨 4:22 运行 `cron` 目录中的文件，并在每月第一天的凌晨 4:42 运行 `/etc/cron.monthly` 目录中的所有文件。

由于 `/etc/crontab` 按日、每周和每月组织任务，你可以将脚本文件复制到相应的目录，使其按照系统 `cron` 表确定的计划运行。要每天运行一个名为 `myscript` 的脚本，请将文件复制到 `/etc/cron.daily` 目录。

要启用或禁用 `cron`，请使用如下所示的 `-option` 参数：

`service cron enable` / `service cron deactivate`

你可以使用 `-u` 选项编辑任何用户的 `crontab` 以指定用户名；例如，要编辑用户 `mary` 的 `cron` 表，请使用 `-u mary`。要列出和删除 `mary` 的 `cron` 表，分别使用 `crontab -l mary` 和 `crontab -r mary`。

### crontab 格式

每个 `crontab` 文件都用于调度在不同时间运行的维护任务、备份（或）程序。这些命令中的大多数都是由 `crontab` 文件调度的，该文件可以由 `root` 用户编辑。下面的输出显示了一个 `crontab` 文件示例：

```
crontab -u root -e

crontab=
```

`* * * * * /etc/cron.hourly`
`* * * * * /etc/cron.daily`
`* * * * * /etc/cron.weekly`
`* * * * * /etc/cron.monthly`

行的第一部分指定了执行命令的环境；行的其余部分遵循用户 `cron` 表的格式。字段指定了运行命令的时间，而字段指定了由谁运行命令（上述提到的用户）。其余字段代表命令和参数，用于执行作为参数列出的命令目录中的文件。

### 行格式

`* * * * * /etc/cron.hourly`

`/etc/cron.hourly` 目录中的所有文件都会每天每小时的整点后一分钟以 `root` 用户身份执行。

同样地：

`* * * * * /etc/cron.daily`

`/etc/cron.daily` 目录中的所有文件都会每天凌晨 4:02 以 `root` 用户身份执行。

上述 `/etc/crontab` 文件的其余行将在周日凌晨 4:22 运行 `cron` 目录中的文件，并在每月第一天的凌晨 4:42 运行 `/etc/cron.monthly` 目录中的所有文件。

由于 `/etc/crontab` 按日、每周和每月组织任务，你可以将脚本文件复制到相应的目录，使其按照系统 `cron` 表确定的计划运行。要每天运行一个名为 `myscript` 的脚本，请将文件复制到 `/etc/cron.daily` 目录。
