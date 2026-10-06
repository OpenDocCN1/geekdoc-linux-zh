
| User | Block | soft | hard | timeleft | soft | hard | timeleft |
| --- | --- | --- | --- | --- | --- | --- | --- |
| bjl | 140 | 10000 | 12000 | 73 | 0 | 0 |  |
| vasili | 121 | 10000 | 12000 | 63 | 0 | 0 |  |
| ggu | 1025 | 10000 | 12000 | 140 | 0 | 0 |  |

| 姓名 | 列 1 | 列 2 | 列 3 | 列 4 | 列 5 | 列 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| park | 5 | 10000 | 12000 | 5 | 0 | 0 |
| dubey | 7836 | 20000 | 23000 | 790 | 0 | 0 |
| mdb | 77 | 10000 | 12000 | 13 | 0 | 0 |
| xut | 837 | 10000 | 12000 | 44 | 0 | 0 |
| aizin | 69 | 10000 | 12000 | 12 | 0 | 0 |

本报告指的是全新的 HP-UX 工作站，当时它只有少数活跃用户。

## 7.4 财务计费

UNIX 提供了多功能的计费功能。计费子系统记录系统中运行的每个进程的统计信息，它记录进程的 RUID（即启动进程的用户 UID）和系统资源使用情况。它的设计初衷主要是跟踪系统资源使用情况，以便对用户收取相应的费用。然而，记录的数据也可以高效地用于其他用途，例如某些类型的系统性能和安全监控。

两个主要平台（BSD 和 System V）上的计费子系统是不同的，但它们都基于相同的概念：对新的原始数据进行快速记录，并对记录的数据进行较慢的处理。此外，在第一部分，两个 UNIX 平台的数据记录方式是相似的，但数据处理和输出方法是不同的。在 BSD 平台上，计费是默认启用的；这意味着如果不需要计费，管理员必须防止其启动。在 System V 平台上，计费最初是禁用的，如果需要，必须由管理员设置。计费的启用和禁用通过系统 rc 初始化提供，尽管也可以从命令行完成。

一个特殊的系统实体（用户）`adm` 负责计费；所有与计费相关的资源（程序、目录和文件）都归 `adm` 所有。当启用计费时，内核会将原始数据记录到位于 `adm` 家目录下的二进制数据文件中：

对于 BSD 和 SunOS：

```
/usr/adm/acct and /var/adm/acct
```

对于 System V 和 AIX：

```
/var/adm/pacct and /usr/adm/pacct
```

记录的进程原始数据包括：

- 映像名称 (Image name)
- 使用的 CPU 时间
- 进程启动时间
- 关联 UID 和 GID
- 内存占用
- 读取和写入的字符数
- 读取和写入的磁盘 I/O 块数
- TTY
- 各种关联标志

额外的计费数据存储在文件中：

- `/etc/utmp`
  一个包含当前登录用户数据的二进制日志文件
- `/usr/adm/wtmp`
  一个记录每次登录和注销的二进制日志文件
- `/usr/adm/lastlog`
  包含每个用户上次登录日期和时间的数据库

列出的这三个文件源自计费子系统并是其组成部分；然而，它们已成为几乎任何 UNIX 变体的标准文件，包含了关于系统登录/注销活动的重要数据。某些 UNIX 命令依赖于这些数据。

### 7.4.1 BSD 计费

BSD 平台的计费默认启用；这意味着适当的启动命令包含在系统初始化 rc 脚本 `/etc/rc` 中：

```
[ -f /usr/adm/acct ]; then

  accton /usr/adm/acct; echo -n 'accounting' > /dev/console

fi
```

当指定计费文件（原始数据记录的目的地）作为参数时，`accton` 命令启用计费。如果没有参数，该命令将禁用计费。显然，启动计费的唯一条件是存在原始计费文件 `/usr/adm/acct`。

计费是对数据的连续记录，计费文件会稳定增长。为了控制计费文件 `/usr/adm/acct` 的增长，需要定期的文件处理和调整大小。为此工具是 `sa` 命令（程序）；`sa` 处理数据并将处理后的数据合并到标准摘要文件 `/usr/adm/savacct` 或基于用户的摘要文件 `/usr/adm/usracct`（选项 `-m`）。

以下是使用 `sa` 命令的示例：

```bash
accton # 临时禁用计费

cd /usr/adm # 到计费目录

mv acct acct.tmp # 重命名计费数据文件

touch acct # 重建零大小计费文件

accton acct # 重新启用计费

s -a -f acct.tmp > /dev/null # 将数据合并到标准摘要文件 "savacct"，丢弃生成的报告

rm -f acct.tmp # 删除计费文件
```

可以创建一个类似的脚本并通过 `cronset` (`cron`) 定期执行，这将在第 13 章中介绍。

计费数据应该在系统关机之前进行保存和处理。必须及时提供计费关机程序。然而，在系统崩溃的情况下，必须采取特殊步骤：在重启计费之前，必须手动关闭、保存并处理所有记录。该程序本质上包含了与上例相同的命令序列，但必须在系统达到多用户状态之前完成。实际上，这意味着在系统启动期间，计费启动必须在执行 `/etc/rc` 脚本之前完成。上述的 `sa` 命令具有多种选项；这是一个可以多种方式处理记录数据的程序。为了正确使用 `sa`，应查阅其手册。

另一个实用的工具是 `last` 命令，用于报告用户。

### 7.4.2 System V 计费

System V 计费比 BSD 更强大且功能更多。System V 使用了一系列命令：

- `/var/adm/pacct`
  记录磁盘使用情况的二进制日志文件
- `/usr/adm/wtmp`
  记录每次登录和注销的二进制日志文件
- `/usr/adm/lastlog`
  包含每个用户上次登录日期和时间的数据库

列出的三个文件源自计费子系统并是其组成部分；然而，它们已成为几乎任何 UNIX 变体的标准文件，包含了关于系统登录/注销活动的重要数据。某些 UNIX 命令依赖于这些数据。

启动/停止过程的主要部分是程序 `/usr/lib/acct/startup` 和 `/usr/lib/acct/shutacct`。这两个程序所示：

```
$ cat /usr/lib/acct/startup

#! /bin/sh

# Copyright (c) AT&T

# All Rights Reserved

# *startup - 每当系统启动时，应从 /etc/rc 调用

PATH=/usr/lib/acct:/var/bin/sbin

acctwwtmp acctg on /var/adm/wtmp

turnacct switch

# *clean 昨昨日的审计文件

rm -f /var/adm/acct/sum/wtmp

rm -f /var/adm/acct/sum/pacct

rm -f /var/adm/acct/nite*
```

Solaris 提供了 `turnacct` 命令来根据附加参数启动或停止审计。该命令取代了 BSD 的 `accton` 命令。

关闭审计的脚本是：

```
$ cat /usr/lib/acct/shutacct

#! /bin/sh

# Copyright (c) AT&T

# All Rights Reserved

# "shutacct [arg] 关闭审计，每当系统关机时，从 /usr/sbin/shutdown 调用"

# "Arg 添加到 /var/wtmp 以记录原因，默认值为 shutdown"

PATH=/usr/lib/acct:/usr/bin/sbin

_reason=$($1 -acctg off)

acctwwtmp "${_reason}" /var/adm/wtmp

turnacct off
```
