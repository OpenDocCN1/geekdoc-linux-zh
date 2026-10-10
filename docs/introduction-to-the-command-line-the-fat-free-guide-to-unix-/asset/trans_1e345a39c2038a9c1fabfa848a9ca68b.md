
## ulimit

用途：显示/设置系统资源限制。

用法语法：`ulimit [OPTIONS] [LIMIT]`

```
$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority           (-r) 20
file size               (blocks, -f) unlimited
pending signals             (-i) 16384
max locked memory       (kbytes, -l) 64
max memory size         (kbytes, -m) unlimited
open files                  (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority            (-r) 0
stack size              (kbytes, -s) 8192
cpu time                (seconds, -t) unlimited
max user processes          (-u) unlimited
virtual memory          (kbytes, -v) unlimited
file locks                (-x) unlimited
```

使用 ulimit 命令显示已定义的资源限制

`ulimit` 命令用于显示和设置系统资源限制。这些限制控制了可供程序使用的最大系统资源量。它可以用于控制由用户启动的每个程序可用的最大内存量、CPU 时间以及文件大小。

> 提示：Ulimit 配置通常存储在大多数系统的 `/etc/limits.conf` 或 `/etc/security/limits.conf` 中。

常见用法示例：

- `ulimit -a`：显示所有已定义的资源限制
- `ulimit [OPTION] [LIMIT]`：设置 ulimit 值

## 第 6 节：进程控制与调度

### 概述

在 Unix、Linux 和 BSD 系统上运行的每个程序都被视为一个进程。进程被分配了一个唯一标识符，用于监控和控制该进程。此进程标识符 (PID) 可用于使用本节中讨论的命令行实用程序来控制进程。

本节涵盖的命令：

| 命令 | 用途 |
| :--- | :--- |
| ps | 显示正在运行的进程。 |
| pgrep | 按名称查找进程。 |
| pstree | 以树状视图显示所有正在运行的进程。 |
| kill | 终止一个进程。 |
| killall | 终止所有具有指定名称的进程。 |
| nice | 以指定的 CPU 优先级级别执行程序。 |
| renice | 更改正在运行的进程的优先级。 |
| & | 在后台启动进程。 |
| bg / fg | 将进程移至后台/前台。 |
| jobs | 显示后台和暂停的任务。 |
| nohup | 运行对挂断信号具有免疫能力的进程。 |
| batch | 计划在低 CPU 负载期间运行程序。 |
| at | 计划在指定时间运行程序。 |
| atq | 显示队列中的 at 任务。 |
| atrm | 从队列中移除已调度的 at 任务。 |
| crontab | 计划在指定时间运行程序。 |

### 本节使用的术语表：

| 术语 | 描述 |
| :--- | :--- |
| **Cron** | 一种用于在特定时间间隔执行程序的计划系统。 |
| **任务 (Job)** | 使用 **at** 或 **batch** 计划程序进行计划、暂停或当前正在运行的程序。 |
| **Nice 值** | 分配给进程的数值指示器，用于指示和控制其 CPU 调度优先级。 |
| **PID** | (**P**rocess **I**Dentifier，进程标识符) 分配给系统中每个已执行进程的唯 一数值。 |
| **PPID** | (**P**arent **P**rocess **I**Dentifier，父进程标识符) 启动子进程的父进程的 PID。 |
| **优先级** | *Nice 值*的同义词。 |
| **进程** | 任何已执行的程序。 |

## ps

**用途：** 显示正在运行的进程。

**用法语法：** `ps [OPTIONS]`

```
$ ps
  PID TTY          TIME CMD
4958 pts/0    00:00:00 bash
9596 pts/0    00:00:00 ps
```

*ps* 命令的示例输出

**ps** 命令显示系统上正在运行的进程。不带选项执行 **ps** 命令将显示当前用户拥有的所有进程，如上述示例所示。要获取完整的进程列表，请如下一个示例所示使用 **-e** 选项。

```
$ ps -e
  PID TTY          TIME CMD
  1 ?        00:00:01 init
  2 ?        00:00:00 kthreadd
  3 ?        00:00:00 migration/0
  4 ?        00:00:00 ksoftirqd/0
  5 ?        00:00:00 watchdog/0
...
```

使用 *ps* 命令配合 *-e* 选项

可以使用 **-ef** 选项来显示系统中所有进程的详细信息。这包括用户 ID、进程 ID、父进程 ID 以及其他有用信息，如下一个示例所示。

```
$ ps -ef
UID          PID    PPID C STIME TTY          TIME CMD
root           1       0 0 Jun24 ?        00:00:02 /sbin/init
root           2       0 0 Jun24 ?        00:00:00 [kthreadd]
root           3       2 0 Jun24 ?        00:00:00 [migration/0]
root           4       2 0 Jun24 ?        00:00:00 [ksoftirqd/0]
root           5       2 0 Jun24 ?        00:00:00 [watchdog/0]
...
```

*-ef* 命令的输出

**常见用法示例：**

- `ps`：显示当前用户的进程
- `ps -e`：显示系统上运行的所有进程
- `ps -ef`：显示正在运行的进程的详细信息
- `ps -u [USER]`：显示由指定用户拥有的进程

## pgrep

**用途：** 按名称查找进程。

**用法语法：** `pgrep [OPTIONS] [NAME]`

```
$ pgrep apache
3952
4075
4076
4077
4078
4079
```

使用 pgrep 命令显示名为 apache 的 PID

**pgrep** 命令显示所有匹配指定名称的进程。在上面的示例中，显示了 *apache* Web 服务器的 PID。这等同于输入 `ps -el | grep apache`，并作为产生相同结果的快捷方式提供。

可以使用 `-l` 选项与 **pgrep** 一起，如下一个示例所示，以显示每个 PID 的完整进程名称。

```
$ pgrep -l apache
3952 apache2
4075 apache2
4076 apache2
4077 apache2
4078 apache2
4079 apache2
```

使用 pgrep 配合 -l 选项显示每个进程的完整名称

> **注意**
>
> 某些系统可能使用 *pidof* 命令来替代 **pgrep** 命令。

**常见用法示例：**

- **pgrep [NAME]**：显示匹配指定名称的 PID
- **pgrep -l [NAME]**：除 PID 外还显示进程名称
- **pgrep -P [PPID]**：显示指定 PPID 的所有子进程
- **pgrep -c [NAME]**：显示匹配进程的总数

## pstree

用途：以树状视图显示所有正在运行的进程。

用法语法：`pstree [OPTIONS]`

```
$ pstree
init
├──NetworkManager──┬──dhclient
│                  └──{NetworkManager}
├──acpid
├──apache2──5* {apache2}
├──atd
├──cron
├──cupsd
├──dbus-launch
├──dd
├──fast-user-switc
├──gconfd-2
├──6* {getty}
├──gnome-keyring-d
├──gnome-power-man──{gnome-power-man}
├──gnome-screensav
├──gnome-settings──┬──{gnome-settings}
├──gnome-terminal─bash──pstree
│                  ├──gnome-pty-helpe
│                  └──{gnome-terminal}
├──gvfsd
└──gvfsd-burn
... 
```

![Process tree example](img/8f33496304c637dbf51ff6ddc3c7ff29_109_0.png)

`pstree` 命令会为当前在系统上运行的所有进程绘制进程树，如上述示例所示。`pstree` 的输出使查看父进程和子进程之间的关系变得容易。

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `pstree` | 显示基本的进程树列表 |
| `pstree -p` | 在树列表中包括 PID 编号 |
| `pstree -a` | 包括每个进程的命令行选项 |
| `pstree [USER]` | 显示由指定用户拥有的进程 |
| `pstree [PID]` | 显示指定 PID 的子进程 |

## kill

**用途：** 终止一个进程。

**用法语法：** `kill [OPTIONS] [PID]`

```
# pgrep -l mysqld
5540 mysqld
# kill 5540
```

使用 kill 命令终止一个进程

`kill` 命令终止指定的 PID。在上面的示例中，使用 `kill` 终止了 PID 为 5540 的 `mysqld` 进程。

`kill` 命令的默认行为是请求进程正常退出。如果进程未能正常终止，可以发送可选的 kill 信号以强制进程结束。在此情况下，最常用的 kill 信号是 `-9`，它会强制终止指定的 PID，如下一个示例所示。

```
# pgrep -l mysqld
5545 mysqld
# kill -9 5545
```

使用 -9 选项杀死卡住的进程

> 注意：建议在极少数情况下才使用 `kill -9` 命令，即当卡住的进程拒绝正常退出时。`-9` 信号仅在这些极端情况下使用，因为它可能导致不良结果，如系统不稳定和“僵尸”子进程。

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `kill [PID]` | 终止指定的进程 |
| `kill -9 [PID]` | 强制无响应的进程终止 |

