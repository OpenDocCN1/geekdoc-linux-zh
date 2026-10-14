

Table 10-19 shows some other commonly used commands and options for `at`.

| Command | Description |
|---|---|
| `atq` | 显示已定义的作业（包括作业编号，删除作业时需要）。 |
| `atrm job_number` | 删除一个作业（使用作业编号）。 |

**Table 10-19**

![](img/9129877170834ca9d5fdac5319bf5f12_373_0.png)

## Exercise 10-4: Schedule Jobs with at and cron

在本练习中，使用 at 和 cron 安排作业。

首先，将 finger 的输出重定向到当前时间三分钟后的 `/var/log/messages`。然后，将同一作业安排在明天中午运行。然后，安排一个程序在明天下午 2:00 运行，之后删除该作业。

练习的第二部分，创建一个普通用户 cron 作业，每分钟将 finger 的输出记录到 `~/users/log`。

## Detailed Steps to Complete This Exercise

- Part I: Schedule Jobs with at
- Part II: Schedule Jobs with cron

## Part I: Schedule Jobs with at

要使用 at 安排作业，请执行以下操作：

1. 在 GNOME 桌面上的终端窗口中，切换到 root 用户（`su -`，密码 `n0v3ll`）。

2. 通过输入以下命令验证 at 服务是否正在运行
```
rcatd status
```

3. （条件）如果 at 服务未运行，通过输入以下命令启动服务
```
rcatd start
```

4. 通过输入以下命令显示当前日期和时间
```
date
```

5. 从现在起三分钟后，将登录用户记录到 `/var/log/messages` 中，输入
```
at hh:mm
/usr/bin/finger >> /var/log/messages
```

上述命令将 finger 的输出重定向到 `/var/log/messages`。确保你有两个 `>` 字符；如果只有一个 `>` 字符，`/var/log/messages` 中的现有条目将被删除。

6. 通过按以下键退出 `at` 编辑器
`Ctrl+d`

7. 通过输入以下命令查看已安排的 `at` 作业
`atq`（或 `at -l`）

注意列出的作业编号。

8. 等待 3 分钟过去；然后通过输入以下命令检查 `/var/log/messages` 文件中的 finger 信息

```
tail /var/log/messages
```

geeko 的登录信息列在文件末尾。

9. 通过输入以下命令安排同一作业在明天中午运行
`at noon tomorrow`

在 at 提示符下，输入

```
/usr/bin/finger >> /var/log/messages Ctrl+d
```

10. 通过输入以下命令安排在明天下午 2:00 将日期记录到 `/var/log/messages` 文件中
`at 14:00 tomorrow`

在 at 提示符下，输入

```
/bin/date >> /var/log/messages Ctrl+d
```

11. 通过输入以下命令查看已安排的 `at` 作业
`atq`（或 `at -l`）

注意两个作业都已列出，每个作业都有单独的作业编号。

12. 通过输入以下命令删除安排在明天下午 2:00 的作业
`atrm job number`

13. 通过输入以下命令查看已安排的 `at` 作业
`atq`（或 `at -l`）

只有安排在 12:00 的作业仍然列出。

## Part II: Schedule Jobs with cron

要使用 cron 安排作业，请执行以下操作：

1. 打开一个终端窗口。

2. 通过执行以下操作以 geeko 身份安排 cron 作业：
   a. 输入 `crontab -e`。
   vi 编辑器会显示一个 cron 表文件（如 `/tmp/crontab.11743`）。
   按 `i` 进入插入模式。

   b. 安排一个作业每分钟运行，使用 `finger` 记录当前登录的用户。让 `finger` 将其输出写入 `~/users.log` 文件，输入

   ```bash
   * * * * * /usr/bin/finger >> ~/users.log
   ```

   c. 按 Esc。

   d. 通过输入以下内容保存文件并退出 vi 编辑器

   ```bash
   :wq
   ```

   e. 观察 users.log 文件几分钟。为验证其正在更新，输入

   ```bash
   tail -f ~/users.log
   ```

   f. 当你完成观察文件更新时，按

   ```text
   Ctrl+c
   ```

3. 通过输入以下命令查看 geeko 的 crontab 文件

```bash
crontab -l
```

4. 通过输入以下命令删除 geeko 的 crontab 文件

```bash
crontab -r
```

5. 通过输入以下命令验证 crontab 文件不再存在

```bash
crontab -l
```

6. 通过输入以下命令验证你在第 2 步中定义的 cron 作业不再处于活动状态

```bash
tail -f ~/users.log
```

注意 users.log 不再添加条目。

7. 按 Ctrl+c。

## Summary

- 要监控启动过程，可以使用 YaST，查看 `dmesg` 命令的输出，以及查看 `/var/log/boot.msg` 文件的内容。

- 大多数硬件信息可在 `/proc` 目录下的文本文件中获得。或者，你也可以使用 `hwinfo`、`hwparm`、`fdisk`、`lspci` 和 `sig` 命令查看系统硬件信息。

- 可以使用 `uptime`、`netstat` 和 `uname` 命令获得通用系统信息。

- 可以使用 `df` 命令、`du` 命令和 GNOME 系统监视器实用程序来监控磁盘使用情况。

- 大多数日志文件存储在 `/var/log` 目录中，并由 Syslog 守护进程（syslog-ng）通过其配置文件中的条目创建。文本日志文件可以使用 `tail` 等文本程序查看。

- `logrotate` 程序每天运行，使用 `/etc/logrotate.conf` 文件中的条目和 `/etc/logrotate.d` 目录中的应用程序特定信息来归档日志文件。

- 你可以使用多种不同的命令行实用程序监控登录活动，例如 `who`、`w`、`finger`、`last` 和 `lastlog`。

- 进程是系统上正在执行的程序。用户进程在终端中运行并由用户执行，而守护进程是系统服务，不在终端上运行。

- 每个进程都有一个 PID、一个 PPID，并且可能启动无限数量的子进程。

- 除了 PID 外，后台进程还有一个作业 ID，可用于控制其执行。你可以通过在程序命令后附加 `&` 字符来在后台启动任何程序。然后可以使用 `jobs` 命令查看该程序，或使用 `fg` 和 `bg` 命令进行操作。

- 你可以在桌面环境中使用 GNOME 系统监视器，或在命令行提示符下使用 `ps`、`pstree` 和 `top` 命令查看进程。

- GNOME 系统监视器以及 `kill`、`killall` 和 `top` 命令可用于通过发送信号来停止进程。尽管有许多可用信号，但这些命令使用的默认信号是 SIGTERM。

- 你可以通过更改其 nice 值来影响进程的优先级。所有进程都以 0 nice 值启动，可以降低到 -20（高优先级）或增加到 +19（低优先级）。只有 root 用户可以提高进程的优先级。

- 要更改程序的 nice 值，可以使用 `nice` 命令。要更改进程的 nice 值，必须使用 `renice` 命令。

- 守护进程名称通常以 d 结尾，并且在 ps 命令输出的 TTY 列中包含一个 ?。信号控制的守护进程在特定事件发生时执行，而间隔控制的守护进程会定期在系统上运行。

- 你可以通过在 `/etc/init.d` 目录中运行适当的脚本并使用 `start` 参数，或使用 `rcdaemonname start` 命令来启动守护进程。

- 可以使用 `at` 守护进程安排命令在以后某个时间运行。

- 要安排任务在未来重复发生，必须使用 cron 守护进程并创建 crontab（cron 表）。系统任务使用 `/etc/crontab` 文件安排运行。用户任务可以使用 `crontab` 命令安排，并存储在 `/var/spool/cron/tabs` 目录中。

## Key Terms

- **&** — 用于在后台启动程序的特殊字符。
- **/etc/at.allow** — 列出可以使用 at 命令的用户的文件。
- **/etc/at.deny** — 列出不能使用 at 命令的用户的文件。
- **/etc/cron.d** — 包含其他系统 cron 表的目录。
- **/etc/crontab** — 系统 cron 表。
- **/etc/logrotate.conf** — `logrotate` 命令的配置文件。它通常使用 `/etc/logrotate.d` 目录中列出的每个日志文件的参数。
- **/etc/logrotate.d** — 存储供 `logrotate` 命令使用的日志文件特定信息的目录。
- **/etc/sysconfig/cron** — 包含 cron 守护进程参数的文件。
- **/etc/sysconfig/syslog** — 包含 Syslog 守护进程配置参数的文件。
- **/etc/syslog-ng/syslog-ng.conf** — 定义 Syslog 守护进程如何记录系统进程信息的配置文件。
- **/etc/syslog-ng/syslog-ng.conf.in** — 用于创建 `/etc/syslog-ng/syslog-ng.conf` 文件的模板。
- **/proc** — 包含 Linux 系统上硬件、软件和进程信息的目录。
- **/var/log** — 包含 Linux 系统上大多数日志文件的目录。
- **/var/log/audit/audit.log** — AppArmor 的日志文件。
- **/var/log/boot.log** — 包含启动过程中写入的所有消息的文件。
- **/var/log/firewall** — 存储防火墙相关消息的日志文件。
- **/var/log/messages** — 包含大多数系统消息的日志文件。
- **/var/spool/cron/lastrun** — 用于存储过去运行的系统 cron 作业信息的目录。
- **/var/spool/cron/tabs** — 包含用户 cron 表的目录。
- **at command** — 用于安排命令在未来某个时间运行并操作 at 作业的命令。
- **atq command** — 用于查看已安排 at 作业的命令。
- **atrm command** — 用于删除已安排 at 作业的命令。
- **background process** — 在终端中无声运行且不干扰命令行界面的进程。
- **bg command** — 用于在后台启动进程的命令。
- **child process** — 由另一个进程启动的进程。
- **cron** — 根据 crontabs 中的信息重复执行命令的系统服务。
- **crontab (cron table)** — 指定 cron 守护进程要运行的命令以及运行时间表的<|message|>。
- **crontab command** — 用于查看和编辑用户 cron 表的命令。
- **daemon** — 参见 daemon process。
- **daemon process** — 与终端无关的系统进程。它代表 Disk and Execution Monitor。
- **df command** — 显示按文件系统划分的磁盘使用情况的命令。

