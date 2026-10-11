
```bash
[root@server1]# useradd -u 502 sue
[root@server1]# ls -la /home/bobg
total 52
drwx-------- 4 sue root 4096 Jul 17 15:37 .
drwx-xr-x 5 root 4096 Jul 17 15:37 .
-rw-r--r-- 1 sue root 24 Jul 17 15:37 .bash_logout
-rw-r--r-- 1 sue root 191 Jul 17 15:37 .bash_profile
-rw-r--r-- 1 sue root 124 Jul 17 15:37 .bashrc
-rw-r--r-- 1 sue root 5542 Jul 17 15:37 .canna
-rw-r--r-- 1 sue root 820 Jul 17 15:37 .emacs
-rw-r--r-- 1 sue root 118 Jul 17 15:37 .gtstrc
-rw-r--r-- 1 sue root 4096 Jul 17 15:37 .kde
drwx-xr-x 2 root 502 Jul 17 15:37 .xemas
-rw-r--r-- 1 root 3511 Jul 17 15:37 .zsh
```

## 管理用户与组

### 常用任务

| 选项 | 描述 |
| :--- | :--- |
| `-c "description"` | 在 `/etc/passwd` 的 GECOS 字段中为用户指定新描述 |
| `-d homirectory` | 指定新主目录的绝对路径 |
| `-e expiredate` | 指定禁用账户登录的日期 |
| `-f days` | 指定密码过期的账户被禁用的前等待天数 |
| `-g group` | 为用户账户指定新的主组 |
| `-G group1,group2, etc.` | 为用户账户指定所有其他组组成 |
| `-l name` | 指定新的登录名 |
| `-s shell` | 指定用于用户账户的新 `shell` 绝对路径 |
| `-u UID` | 为用户账户指定新的 `UID` |

**表 10-7** `usermod` 命令的常用选项

`usermod` 命令无法修改的账户信息是存储在 `/etc/shadow` 中的密码过期信息（之前讨论过的 `min`, `max`, `warn`）。要更改这些信息，可以使用 `chage` 命令配合相应的选项。例如，要指定用户在收到新密码后必须等待两天才能更改密码，并指定密码在 50 天后过期且提前 7 天发出警告，可以使用 `chage` 命令的以下选项：

```bash
[root@server1-#] chage -m 2 -M 50 -W 7 bobg
[root@server1-#]
```

有时有必要锁定账户——即防止用户登录。要锁定账户，可以在命令行提示符下使用 `usermod -L username`。这会在 `/etc/shadow` 的过期密码字段开头放置一个 `!` 字符。要解锁账户，只需在命令行提示符下输入 `usermod -U username`，这将移除 `/etc/shadow` 文件中密码字段的 `!` 字符。或者，你可以使用 `passwd -l username` 锁定账户，使用 `passwd -u username` 解锁账户。这些命令分别在 `/etc/shadow` 文件的过期字段开头放置或移除 `!` 字符。

另一种常用的锁定账户方法是将 `/etc/shadow` 中的账户 `shell` 字段更改为无效 `shell`（如 `/bin/false`）。如果没有有效的 `shell`，用户将无法使用系统。要锁定账户，可以编辑 `/etc/shadow` 文件、使用 `usermod` 命令的 `-s` 选项或使用 `chsh` 命令。以下示例使用 `chsh` 命令将 `bobg` 的 `shell` 更改为 `/bin/false`：

```bash
[root@server1-#] chsh -s /bin/false bobg
Changing shell for bobg.
Warning: "/bin/false is not listed in /etc/shells
Shell changed.
[root@server1]#
```

## 管理组

（注：原文后续部分为大量重复的乱码，已根据上述逻辑完成核心翻译）

## 章节总结

- 打印任务在打印到打印机之前会被轮空到打印队列中。
- 你可以使用 `cupsaccept`、`cupsreject`、`cupsenable` 和 `cupsdisable` 命令配置打印机的轮空或打印。
- 使用 `lp` 命令创建打印任务，使用 `lpq` 在打印队列中查看任务，并使用 `cancel` 命令从队列中移除任务。
- 你可以使用“打印机配置”工具或修改 `/etc/cups/printers.conf` 文件来创建本地和远程打印机。
- Linux 系统上的大多数日志文件存储在 `/var/log` 目录下。
- 系统事件通常由系统日志守护进程（System Log Daemon）记录到文件中。
- 日志文件可以清除或轮转以节省磁盘空间；可以使用 `logrotate` 工具轮转日志文件。
- 用户和组信息通常存储在 `/etc/passwd`、`/etc/shadow` 和 `/etc/group` 文件中。
- 你可以使用 `useradd` 命令创建用户，使用 `groupadd` 命令创建组。
- 所有用户在登录 Linux 系统之前必须有一个有效的密码。
- 用户可以使用 `usermod`、`chage`、`chfn`、`cush` 和 `passwd` 命令进行修改，组可以使用 `groupmod` 命令进行修改。
- `userdel` 和 `groupdel` 命令分别用于从系统中删除用户和组。

## 关键术语

- `/etc/cups/cupsd.conf` 存储 `cups` 守护进程配置的文件。
- `/etc/cups/printers.conf` 存储 `cups` 守护进程打印机配置的文件。
- `/etc/default/useradd` 包含用户创建时默认值的文件。
- `/etc/group` 包含组定义和成员关系的文件。
- `/etc/login.defs` 包含用户创建时默认值的文件。
- `/etc/logrotate.conf` `logrotate` 工具用于指定日志文件轮转参数的文件。
- `/etc/passwd` 包含用户账户信息的文件。
- `/etc/shadow` 包含加密后的密码以及每个用户账户的密码过期和账户过期时间参数的文件。
- `/etc/skeleton` 包含会被复制到所有用户主目录文件的目录。
- `/etc/syslog.conf` 指定系统日志守护进程监听哪些事件以及保存到哪些日志文件的文件。
- `/var/log` 包含 Linux 系统上大多数日志文件的目录。

## 关键术语

- **接受打印机 (accepting printer)** 接受打印任务进入打印队列的打印机。
- **认证 (authentication)** 通过将用户名和密码与系统数据库（`/etc/passwd` 和 `/etc/shadow`）对比来验证用户身份的行为。
- **`cancel` 命令 (cancel command)** 用于从 CUPS 打印队列中移除打印任务的命令。
- **`chage` 命令 (chage command)** 用于修改用户账户过期信息的命令。
- **`chfn` 命令 (chfn command)** 用于更改用户 GECOS 的命令。
- **`charm` 命令 (charm command)** 将有效 `shell` 改为无效 `shell` 的命令。
- **通用 Unix 打印系统 (CUPS)** Linux 常用的打印系统。
- **`cupsaccept` 命令 (cupsaccept command)** 允许打印机接受任务进入打印队列的命令。
- **`cups` 守护进程 (cupsd)** 负责 CUPS 打印系统中打印任务的守护进程。
- **`cupsdisable` 命令 (cupsdisable command)** 防止打印任务离开队列的命令。
- **`cupsenable` 命令 (cupsenable command)** 允许打印任务离开队列的命令。
- **`cupsreject` 命令 (cupsreject command)** 拒绝打印任务进入队列的命令。
- **已禁用打印机 (disabled printer)** 不将打印任务从打印队列发送到打印机的打印机。
- **已启用打印机 (enabled printer)** 将打印任务从打印队列发送到打印机的打印机。
- **设施 (facility)** 记录事件时收集信息的系统区域。
- **通用综合信息 (GECOS)** `/etc/passwd` 文件中包含用户账户描述信息的字段。
- **`groupadd` 命令 (groupadd command)** 用于向系统添加组的命令。
