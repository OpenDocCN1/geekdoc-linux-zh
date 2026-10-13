
```
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
9 S 0 8200 4100 0 84 20 f0274e38 193 ? 0:00 largejob
```

发出以下命令以提高 `PID` `8200` 的优先级：

```
renice -n -4 -p 8200
```

再次发出 `ps -el` 命令显示该进程具有更高的优先级：

```
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
9 S 0 8200 4100 0 60 12 f0274e38 193 ? 0:00 largejob
```

### 使用 `priocntl` 更改进程的调度优先级

作为对实时进程的支持，Solaris 下的标准优先级方案已得到改进。实时进程设计用于需要几乎立即响应事件的应用领域。这些进程在运行时几乎可以完全访问所有系统资源。Solaris 使用范围从 `-20` 到 `20` 的分时优先级数字。Solaris 使用 `priocntl` 命令（旨在改进 `nice` 命令）来修改进程优先级。要使用 `priocntl` 更改进程的优先级，请输入

```
priocntl -s -p <new-priority> -i pid <process-id>
```

其中 `new-priority` 是进程的新优先级，`process-id` 是你要更改的进程的 `PID`。以下示例将进程 `8200` 的优先级级别设置为 `-5`：

```
priocntl -s -p -5 -i pid 8200
```

以下示例用于为给定父进程创建的每个进程设置优先级（`nice` 值）：

```
priocntl -s -p -5 -I ppid 8200
```

执行此命令后，从进程 `8200` 分叉的所有进程的优先级都将为 `-5`。

有关 `priocntl` 命令的更多信息，请参阅在线手册页。

## Solaris 批处理设施

在繁忙的系统上划分进程的一种方式是安排作业在不同时间运行。例如，一个大型作业可以安排在凌晨2点运行，此时系统通常处于空闲状态。Solaris 支持两种批处理方法——`crontab` 和 `at` 命令。`crontab` 命令按固定间隔安排多个系统事件，而 `at` 命令安排单个系统事件。

### `crontab`

`cron` 守护进程根据每个 `crontab` 文件中包含的命令安排系统事件。`crontab` 文件由按固定间隔执行的命令组成，每行一条。每行的开头包含五个日期和时间字段，告诉 `cron` 守护进程何时执行命令。第六个字段是要运行的程序的完整路径名。这些字段在表 10-7 中有描述，由空格分隔。

表 10-7 `crontab` 文件

| 字段 | 描述 | 值 |
|---|---|---|
| 1 | 分钟 | 0-59 此字段中的 `*` 表示每分钟。 |
| 2 | 小时 | 0-23 此字段中的 `*` 表示每小时。 |
| 3 | 月中的日期 | 1-31 此字段中的 `*` 表示每月的每一天。 |
| 4 | 月份 | 1-12 此字段中的 `*` 表示每个月。 |
| 5 | 星期几 | 0-6（0=星期日）此字段中的 `*` 表示每周每一天。 |
| 6 | 命令 |  |

在 `crontab` 中添加条目时请遵循以下准则：

- 用空格分隔字段。
- 用逗号分隔时间字段中的多个值。
- 使用连字符指定时间字段中的值范围。
- 使用星号作为通配符以包含时间字段中的所有可能值。例如，星号 `*` 可用于时间字段中表示所有合法值。
- 在行开头使用注释标记 `#` 表示注释或空行。
- `crontab` 文件中的每个命令必须占一行，即使非常长，因为 `crontab` 不识别额外的回车符。

以下示例 `crontab` 命令条目会在每个月的 1 日和 15 日下午 5 点在用户控制台窗口中显示提醒。

```
0 17 1,15 * * echo Handing Timesheet > /dev/console
```

`crontab` 文件位于 `/var/spool/cron/crontabs` 目录中。除了 `root` 之外，SunOS 软件安装期间还提供了多个 `crontab` 文件，也位于此目录中。其他 `crontab` 文件以创建它们的账户命名，例如 `bill`、`glenda`、`miguel` 或 `nicole`。它们也位于 `/var/spool/cron/crontabs` 目录中。例如，名为 `root` 的 `crontab` 文件在软件安装期间提供。其内容包括以下命令行：

```
10 3 * * 0,4 /etc/cron.d/logchecker
10 3 * * 0 /usr/lib/newsyslog
15 3 * * /usr/lib/fs/nfs/nfssfind
1 2 * * * [ -x /usr/sbin/rtc ] && /usr/sbin/rtc -c > /dev/null 2>&1
```

第一行命令指示系统在星期日和星期四晚上 3:10 运行 `logchecker`。第二行命令安排系统在每个星期日早上 3:10 运行 `newsyslog`。第三行命令指示系统每天早上 3:15 执行 `nfssfind`。第四行命令指示系统检查夏令时并在必要时进行修正。如果没有 `RTC` 时区或没有 `/etc/rtc_config` 文件，此条目将不执行任何操作。

`cron` 守护进程处理 `crontab` 命令的自动调度。其功能是每 15 分钟检查一次 `/var/spool/cron/crontabs` 目录是否存在 `crontab` 文件。它检查新的 `crontab` 文件或现有文件的更改，读取文件中的执行时间，并在适当的时间提交命令执行。

### 如何创建或编辑 `crontab` 文件

在 `crontab` 文件中创建条目与使用您喜欢的编辑器编辑文本文件一样简单。步骤如下：

1. （可选）要创建或编辑属于 `root` 或其他用户的 `crontab` 文件，请成为超级用户。
2. 通过输入创建新的 `crontab` 文件或编辑现有文件

   `crontab -e`
3. 按照表 10-7 中描述的语法向文件添加命令行。
4. 保存更改并退出文件。`crontab` 文件放置在 `/var/spool/cron/crontabs` 中。
5. 通过输入验证 `crontab` 文件

   `crontab -l`

系统会通过列出 `crontab` 文件的内容做出响应。

### 控制对 `crontab` 的访问

您可以通过修改 `/etc/cron.d` 目录中的两个文件来控制对 `crontab` 的访问：`cron.deny` 和 `cron.allow`。这些文件仅允许指定用户执行 `crontab` 任务，例如创建、编辑、显示或删除自己的 `crontab` 文件。`cron.deny` 和 `cron.allow` 文件由用户名列表组成，每行一个。这些访问控制文件按以下方式协同工作：

- 如果存在 `cron.allow`，则只有列在此文件中的用户可以创建、编辑、显示或删除 `crontab` 文件。
- 如果不存在 `cron.allow`，则所有用户都可以提交 `crontab` 文件，除 `cron.deny` 中列出的用户外。
- 如果 `cron.allow` 和 `cron.deny` 都不存在，则需要超级用户权限才能运行 `crontab`。

编辑或创建 `cron.deny` 和 `cron.allow` 需要超级用户权限。

在 Solaris 软件安装期间，会提供默认的 `/etc/cron.d/cron.deny` 文件，其中包含以下条目：

- `daemon`
- `bin`
- `smtp`
- `nuucp`
- `listen`
- `nobody`
- `noaccess`

`cron.deny` 文件中列出的用户均无法访问 `crontab` 命令。系统管理员可以编辑此文件以添加将被拒绝访问 `crontab` 命令的其他用户。未提供默认的 `cron.allow` 文件。这意味着在 Solaris 软件安装后，所有用户（除默认 `cron.deny` 文件中列出的用户外）都可以访问 `crontab`。如果您创建 `cron.allow` 文件，则只有这些用户可以访问 `crontab` 命令。

### 安排单个系统事件（`at`）

`at` 命令用于安排作业在稍后时间执行。与按固定间隔安排作业的 `crontab` 不同，使用 `at` 提交的作业将在指定时间执行一次。

要提交 `at` 作业，输入 `at`。然后指定执行时间和要运行的程序，如以下示例所示：

```
at 07:45am today
at> who > /tmp/log
at> <Press Control-d>
job 912687240.a at Thu Dec 3 07:14:00 1998
```

当您提交 `at` 作业时，会分配一个作业标识号，连同 `.a` 扩展名一起成为其文件名。该文件存储在 `/var/spool/cron/atjobs` 目录中。`cron` 守护进程以与调度 `crontab` 作业类似的方式控制 `at` 文件的调度。

`at` 命令语法列在表 10-8 中。

### 表 10-8 `at` 命令语法

|  |  |
|---|---|
| `at -m <time> <date>` |  |
| `-m` | 作业完成后向您发送邮件。 |
