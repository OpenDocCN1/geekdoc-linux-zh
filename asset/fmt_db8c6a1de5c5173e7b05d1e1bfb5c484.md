
| 6968 | 6968 | 8264 | root | xyz005 |

| 6968 | 6968 | 8520 | root | xyz006 |

```
# kill -6 -6968 # 6968 来自 PGID 列
```

一个常见的问题是，在登录 shell 的命令行中以后台方式或作为守护进程启动命令，结果发现当你注销时命令退出了。这是因为当你的终端连接断开时，会向进程发送挂起 (`HUP`) 信号。你可以使用 `nohup` 命令指定这些命令要忽略 `HUP` 信号。

- `nohup <command> &` 忽略挂起的后台进程

## /proc 文件系统

AIX 5L 新增了对 `/proc` 文件系统的支持。`/proc` 文件系统是一个伪文件系统，用于将进程和内核数据结构映射到进程文件。在 AIX 5L 之前，这类信息是被隐藏的，但现在它开放出来供窥探，因此在任何时候都必须极度谨慎！这里永远不是存储信息或尝试修复任何问题的地方。

你可以使用 `df` 命令或 `mount` 命令查看 `/proc` 伪文件系统的统计信息。

```
# df -k
Filesystem   1024-blocks  Free 6used  Iused 6Iused Mounted on
/dev/hd4       32768  3972  8% 1783  13% /
/dev/hd2      1212416 37544 97% 97689  13% /usr
/dev/hd9var    53248 25328 53% 596  5% /var
/dev/hd3       106496  99768  7% 168  1% /tmp
/dev/hd1        4096  3904  5% 42  5% /home
/dev/hd10opt   638976  22388 97% 15603  10% /opt
/proc           -     -     -     -     - /proc

# mount
node       mounted     mounted over   vfs    date      options
---------------------------------------------
/dev/hd4        /                     jfs     Feb 04 10:55 rw log=/dev/hd8
/dev/hd2        /usr                  jfs     Feb 04 10:55 rw log=/dev/hd8
/dev/hd9var     /var                  jfs     Feb 04 10:55 rw log=/dev/hd8
/dev/hd3        /tmp                  jfs     Feb 04 10:55 rw log=/dev/hd8
/dev/hd1        /home                 jfs     Feb 04 10:56 rw log=/dev/hd8
/dev/hd10opt    /opt                  jfs     Feb 04 10:56 rw log=/dev/hd8
/proc                     /proc      Feb 04 10:56 rw
```

请注意，在 `df` 和 `mount` 中，`/proc` 文件系统实际上没有统计信息。这个伪文件系统没有大小、使用百分比或 `inode`。在 `mount` 命令输出中，`/proc` 的文件系统类型是 `procs`，而不是 `jfs` 文件系统。`/etc/vfs` 文件中关于 `procs` 的条目如下所示：

```
# lsvfs procs
procs       6           none     none
```

系统中的每个进程都在 `/proc` 中分配了一个目录，名称等于该进程的 `PID`。在这些进程目录下的每个目录中都有多个文件和子目录，它们与进程的相应内部控制数据结构相关联。其中大多数（但并非全部）文件是只读的，但有些可供进程控制使用并可以写入。用于操作这些文件的工具是标准 C 语言子例程 `open()`、`read()`、`write()` 和 `close()`。可以在 `/usr/include/sys/procs.h` 文件中找到每个数据结构的描述。`/proc` 中的所有文件都属于 `PID` 所有者，这一事实允许普通用户仅访问他们拥有的进程。

为了展示 `/proc` 文件系统的结构，让我们看看我机器上的一个特定进程。我当前正在运行 `docsearch`。我机器上 `docsearch` 命令的 `PID` 是 `19898`。使用 `ls -l` 命令显示目录的内容。

```
# ls -l /proc/19898
```

total 0

```
-rw------- 1 root system 0 Feb 16 14:42 as

-rw------- 1 root system 128 Feb 16 14:42 cred

-rw------- 1 root system 0 Feb 16 14:42 cti

dr-xr-xr-x 1 root system 0 Feb 16 14:42 lwp

-rw------- 1 root system 0 Feb 16 14:42 map

dr-x------ 1 root system 0 Feb 16 14:42 object

-rw-r--r-- 1 root system 448 Feb 16 14:42 psinfo

-rw------- 1 root system 1024 Feb 16 14:42 sigact

-rw------- 1 root system 1520 Feb 16 14:42 status

-r--r--r-- 1 root system 0 Feb 16 14:42 systm
```

随着该进程的执行，有很多进程信息在不断变化。如表 21-2 所示，这些伪文件中的每一个都有特定的功能。`object` 目录包含与进程地址空间中映射的文件相对应的文件。深入查看 `/proc` 结构，`ls -l /proc/19898/object` 命令输出如下：

```
# ls -l /proc/19898/object
```

total 14504

```
-r-xr-xr-x 4 bin bin 240404 Apr 08 2001 a.out

-r-r-xr-xr-x 2 bin bin 6411106 Jul 30 2001 jfs:10.5.2071

-r-r-r-r-r-- 1 bin bin 118685 Apr 08 2001 jfs:10.5.2179

-r-r-xr-xr-x 4 bin bin 240404 Apr 08 2001 jfs:10.5.4207

-r-r-xr-xr-x 1 bin bin 11059 Apr 08 2001 jfs:10.5.4372

-r-r-r-r-r-- 1 bin bin 377654 Apr 08 2001 jfs:10.5.4438

-r-rw-f-r-- 1 bin bin 14342 Apr 08 2001 jfs:10.5.8459
```

`a.out` 文件是 C 语言可执行二进制文件，代表进程源自的程序。`lwp` 目录包含进程中正在运行的每个内核线程的子目录。IBM 使用术语 “lwp” 来表示轻量级进程；它的含义与 AIX 文档中使用的术语 “线程”相同。每个 `lwp` 子目录的名称都是与该进程关联的线程 ID (`TID`)。我的 `docsearch` 进程

| 伪文件 | 功能 |
| :--- | :--- |
| `as` | 允许访问进程的地址空间。你可以读取和写入属于该进程的内存 |
| `cred` | 显示与进程关联的凭据 |
| `cti` | 允许你控制进程，例如停止和恢复进程 |
| `lwp` (directory) | 包含进程的内核线程信息 |
| `map` | 允许访问进程的虚拟地址映射 |
| `object` (directory) | 包含映射文件名 |
| `psinfo` | 包含由 `ps` 命令提供的相同信息 |
| `sigact` | 显示与该进程相关的所有信号的当前状态 |
| `status` | 包含进程状态信息，如地址和堆大小 |
| `systm` | 显示可供该进程使用的系统调用 |

**表 21-2.** `/proc/<PID>` 中伪文件的功能

只有一个线程 ID `29059`，可以通过以下命令在进程表中看到：

```
# ps -mo THREAD -p 19898

USER PID PPID TID ST CFPRI SC WCHAN F TT RND COMMAND
root 19898 15518 - A 0 76 1 - 200001 pt8/2 0 /usr/bin/docssearch
- - 29059 S 0 76 1 - 10400 - - 0 -
```

在 `/proc/19898/lwp/29059` 目录中，我们有以下三个文件：

```
# ls -l /proc/19898/lwp/29059

total 0
-rw------- 1 root system 0 Feb 16 16:08 lwpctl
-r-x-r-r-r- 1 root system 120 Feb 16 16:08 lwpinfo
-r------- 1 root system 1200 Feb 16 16:08 lwpstatus
```

`lwpctl`、`lwpinfo` 和 `lwpstatus` 文件包含控制线程所需的所有线程特定信息。它们的内容类似于我们在示例中 `/proc/19898` 目录中的文件中找到的信息。使用凭据信息，我们可以提供一个从这些文件中检索数据的更好示例。我们使用 `od`（八进制转储）命令显示 `/proc/19898/cred` 文件的内容，如下所示：

```
# ls -l /proc/19898/cred

-rw------- 1 root system 128 Feb 16 16:29 /proc/19898/cred
```

现在对 `/proc/19898/cred` 文件执行八进制转储：

```
# od -x /proc/19898/cred

0000000 0000 0000 0000 0000 0000 0000 0000

0000160 0000 0000 0000 0007 0000 0000 0000 0000

0000200 0000 0000 0000 0002 0000 0000 0000 0003

0000220 0000 0000 0000 0007 0000 0000 0000 0000

0000240 0000 0000 0000 000a 0000 0000 0000 000b

0000260
```

在最左侧列中，显示了文件的八进制字节偏移量。其他所有信息均为文件内容的十六进制表示。

如需了解 `/proc` 文件系统的更多信息，请参阅 IBM Redbook `sg245765`《AIX 5L Differences Guide Version 5.1 Edition》。所有 `pSeries` 和 `UNIX` Redbook 的索引都可以在以下网址找到：`http://publib-b.boulder.ibm.com/Redbooks.nsf/Portals/UNIXRedbooks`。

《AIX 5L Differences Guide Version 5.1 Edition》Redbook 位于以下网址：`http://www.redbooks.ibm.com/pubs/pdf/redbooks/sg245765.pdf`。

## 计划任务（CRON）

UNIX `cron` 实用程序提供了一种基本手段，用于安排任务在一天中的特定时间或定期执行。`cron` 任务可用于执行常规的系统清理任务，如同步磁盘写入、清理 `/tmp` 以及运行计费程序。这类周期性任务可以通过使用 `crontab` 进行定制。`crontab` 是一份包含指定运行时间的命令和脚本列表，将由 `cron` 以所有者的 `EUID` 身份调用。在命令执行后，`cron` 任务会通过电子邮件向拥有者报告任何错误或输出信息。此外，`cron` 会将错误记录到日志文件 `/var/adm/cron/log` 中，如果启用了 AIX 审计功能，还会生成审计记录。

### crontab

要创建一个 `crontab`，请使用您喜欢的编辑器创建一个具有以下格式的表格：

- 分钟
- 小时
- 日期
- 月份
- 星期几
- 命令

表 21-3 列出了每个条目有效值。

每个与时间相关的字段都可以表示为逗号分隔列表、连字符 (`-`) 分隔的范围，或者星号 (`*`)，可用于表示所有可能的时间。例如，如果我想每半小时在系统控制台上显示运行时间统计信息，我将向我的 `crontab` 文件添加以下行。

```
0,30 * * * * /bin/uptime > /dev/console 2>&1
```

| 字段 | 有效值 | 备注 |
| :--- | :--- | :--- |
| 分钟 | 0-59 | 0 = 整点 |
| 小时 | 0-23 | 0 = 午夜 |
| 日期 | 1-31 | |
| 月份 | 1-12 | |
| 星期几 | 0-6 | 周日 = 0，周六 = 6 |
| 命令 | 要执行文件的完整路径名 | |

**表 21-3.** 有效的 Crontab 值

一旦您按照喜好定制了 `crontab` 文件，请通过调用 `crontab` 命令将其交给 `cron` 守护进程。

```
# crontab <YourCrontabFile>
# crontab -e # 作为 cron 表拥有者
```

所有 `crontab` 都存储在 `/var/spool/cron/crontabs` 目录下，以拥有者用户名命名。下列列表来自 `adm` 用户的 `crontab`，该用户 `crontab` 用于收集系统统计信息：

```
#====================================================================
# SYSTEM ACTIVITY REPORTS
# 8am-5pm activity reports every 20 mins during weekdays.
# activity reports every an hour on Saturday and Sunday.
# 6am-7am activity reports every an hour during weekdays.
# Daily summary prepared at 18:05.
#====================================================================
0 8-17 * * 1-5 /usr/lib/sa/sa1 1200 3 &
0 * * * 0,6 /usr/lib/sa/sa1 &
0 18-7 * * 1-5 /usr/lib/sa/sa1 &
5 18 * * 1-5 /usr/lib/sa/sa2 -B 8:00 -e 18:01 -i 3600 -ubwcyagm &
#====================================================================
# PROCESS ACCOUNTING:
# runacct at 11:10 every night
# dodisk at 11:00 every night
# ckpackt every hour on the hour
# monthly accounting 4:15 the first of every month
#====================================================================
#10 23 * * 0-6 /usr/lib/sacct/runacct 2>/usr/adm/sacct/nite/saccterr > /dev/null
#0 23 * * 0-6 /usr/lib/sacct/dodisk > /dev/null 2>&1
#0 * * * * /usr/lib/sacct/ckpackt > /dev/null 2>&1
#15 4 1 * * /usr/lib/sacct/monacct > /dev/null 2>&1
#====================================================================
```

除非系统管理员通过在 `/usr/adm/cron/cron.allow` 和 `/usr/adm/cron/cron.deny` 文件中逐行列出用户名来强制限制可以使用 `cron` 服务的用户，否则任何用户都可以创建 `crontab` 文件。每当用户尝试创建或编辑 `cron` 表时，`cron` 守护进程在调用用户的 `crontab` 文件之前会检查这些文件的授权。默认情况下允许所有用户访问。

请注意！如果您创建了 `/var/adm/cron/cron.deny` 文件，则该文件的优先级高于 `cron.allow` 文件。此外，如果存在 `cron.allow` 文件但未为 `root` 用户创建条目，则即使是 `root` 也无法编辑 `cron` 表！

### 临时任务

假设您想在非工作时间运行任务，但不想为此创建 `crontab` 条目。这可能是一次性的运行。您可以使用 `at` 和 `batch` 命令来实现。请注意，`batch` 只是一个调用 `at` 的脚本。执行 `at` 并指定时间和命令输入流。作业流会被复制到 `/usr/spool/cron/at/jobs` 目录。当时间到来时，`cron` 将在指定时间执行作业流。

使用 `at` 运行任务的授权由 `/usr/adm/cron/at.allow` 和 `/usr/adm/cron/at.deny` 文件中的用户名列出进行控制，这与 `crontab` 的情况类似。默认情况下允许所有用户访问。
