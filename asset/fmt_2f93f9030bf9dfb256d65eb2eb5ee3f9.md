
- 3. Use the `ls` command to display a list of the user’s home directory in the `/etc/passwd` file:

```
root@server ~ # grep project5 /etc/passwd

project5:x:1002:100::/home/project5:/bin/bash
```

- 4. Use the `ls -al /home/project5` to display the directory:

```
root@server ~ # ls -al /home/project5

total 28

drwxr-xr-x 4 project5 4096 Feb 7 14:13

drwxr-xr-x. 7 root 4096 Feb 7 14:13

-rw-r---- 1 project5 18 Jun 22 2020 .bash_logout

-rw-r---- 1 project5 176 Jun 22 2020 .bash_profile

-rw-r---- 1 project5 124 Jun 22 2020 .bashrc

drwxr-xr-x. 2 project5 4096 Sep 29 00:15 .gnome

drwxr-xr-x. 4 project5 4096 Jan 19 .gnome
```

# 第 5 章：命令行

## 135

## 列出进程：ps

`ps` 命令列出系统中的所有进程、其状态、大小、名称、所有者、CPU 时间、挂钟时间等。它有许多命令行参数可用；其中最常用的见表 5-4。

在与 `ps` 命令配合时最常用的参数组合是 `auxww`。这些参数显示所有进程（无论它们是否有控制终端）、每个进程的所有者以及所有进程的命令行参数。让我们查看执行 `ps auxww` 的某些输出。

```
$@server~$ ps auxww | head

USER PID %MEM VSZ RSS TTY STAT TIME COMMAND

root 1 0.0 0.3 19468 1528 ? S 10:06 0:02 /bin/systemd

root 2 0.0 0.0 0 ? S 10:06 0:00

root 3 0.0 0.0 0 ? S 10:06 0:00 [ksoftirqd/0]

root 4 0.0 0.0 0 ? S 10:06 0:00 [migration/0]

root 5 0.0 0.0 0 ? S 10:06 0:00 [watchdog/0]

OUTPUT TRUNCATED.

yang 1838 0.0 0.3 108476 1864 pts/1 S 10:35 0:00 -bash

yang 2365 0.0 0.2 108128 1084 pts/1 R+ 14:47 0:00 ps auxww
```

输出的第一行提供了列表的列头。列头的描述见表 5-5。

| 选项 | 描述 |
| :--- | :--- |
| -a | 显示所有带有控制终端的进程，而不是当前用户的进程 |
| -r | 仅显示运行中的进程（参见本节对进程状态的描述） |
| -x | 显示没有控制终端的进程 |
| -u | 显示进程所有者 |
| -f | 显示进程间的父/子关系 |
| -1 | 产生长格式的列表 |
| -w | 显示进程的命令行参数（最多达半行） |
| -ww | 显示进程的命令行参数（无限宽度模式） |

#### 表 5-4. 常用 ps 选项

Linux 管理：入门指南

| ps 列 | 描述 |
| :--- | :--- |
| USER | 进程的所有者。 |
| PID | 进程标识符。 |
| %CPU | 进程占用 CPU 的百分比。注意：对于具有多个处理器的系统，此列的百分比将超过 100%。 |
| %MEM | 进程占用内存的百分比。 |
| VSZ | 进程占用的虚拟内存量。 |
| RSS | 进程占用的实际（驻留）内存量。 |
| TTY | 进程的控制终端。此列中的问号意味着该进程不再连接到控制终端。 |
| STAT | 进程状态。这些是可能的状态：S 进程正在睡眠。所有准备好运行的进程（即多任务处理中，且 CPU 当前关注其他地方）都将处于睡眠状态。R 进程实际上正在 CPU 上运行。D 不可中断睡眠（通常与 I/O 相关）。T 进程正在被调试器跟踪或已停止。Z 进程已变为僵尸。这意味着该进程没有使用 `wait` 系统调用确认子进程的死亡，或者父进程被不当杀死，在父进程被完全杀死之前，init 进程（见第 8 章）无法杀死子进程本身。僵尸进程通常表明软件编写得不好。 |

此外此外，每个进程的 STAT 条目可以采取以下修饰符之一：

- - 内存中没有驻留页（已完全交换出）。
- 高优先级进程。
- 低优先级任务。
- 内存中的页面被锁定在位处（通常意味着需要实时功能）。

- 进程启动的日期。

- 进程在 CPU 上花费的时间。

- 进程的名称及其命令行参数。

#### 表 5-5. ps 输出字段

# 第 5 章：命令行

### 显示进程的交互列表：top

`top` 命令是 `ps` 的交互版本。它不是提供当前状况的静态视图，而是每 2-3 秒（用户可调）刷新一次进程列表。通过 `top`，你可以对它们进行优先级排序或杀死。图 5-1 显示了一个 `top` 屏幕。

`top` 程序的主要缺点是它是 CPU 大户。在拥堵的系统中，`top` 往往会使系统管理问题复杂化。用户开始运行 `top` 查看情况，发现其他人也在运行该程序，进一步减慢了整个系统的速度。

默认情况下，`top` 所有人都可以使用。根据环境，你可能发现将 `top` 的使用限制为 root 用户是明智的。要这样做，可以使用以下命令更改程序的参数：

```
[root@server ~]# chmod 0700 `which top`
```

运行命令后，非 root 用户将得到一个类似的错误：

```
[yang@server ~] top

bash: /top: Permission denied
```

图 5-1 显示了 `top` 屏幕。

Linux 管理：入门指南

### 向进程发送信号：kill

`kill` 命令用于向进程发送信号。虽然名字暗示它只杀死，但它实际上用于发送任何信号。最常用的信号是 SIGTERM `15`，它请求进程优雅地关闭。另一个是 SIGKILL `9`，它强制终止。

要使用 `kill`，你需要进程的 PID。可以使用之前讨论的 `ps` 命令找到 PID。

```bash
kill [PID]
```

要发送特定信号，使用：

```bash
kill [SIGNAL] [PID]
```

常用信号包括：

- SIGHUP `1`：挂断。
- SIGINT `2`：中断（键盘）。
- SIGKILL `9`：强制杀死。
- SIGSTOP `19`：停止。
- SIGTERM `15`：终止。
- SIGUSR1/2：自定义信号。

### kill 使用示例

你需要终止一个没有响应的进程：

```bash
kill 1234
```

如果进程没有停止，使用 SIGKILL：

```bash
kill -9 1234
```

发送 SIGHUP 信号以加载配置文件：

```bash
kill -HUP 1234
```

> 提示 获取所有可用信号及其数值对应的列表，请使用 `kill -l`。

# Linux 管理：初学者指南

`-s` 选项在这里看起来似乎被浪费了（毕竟，我们知道这是 Linux），但这个参数在几乎所有的类 Unix 操作系统上也证明是非常有用的。例如，在 Silicon Graphics, Inc. `SGI` 的工作站终端上，`uname -s` 会返回 SGI，而在 Sun 工作站上它会返回 SunOS。在异构环境中工作的人通常会编写根据不同操作系统而行为不同的脚本，而 `uname -s` 是确定这些信息的一种一致方法。

提示：另一个提供提供发行版特定信息的命令是 `lsb_release` 命令。具体来说，它可以显示与 Linux 标准基础（LSB）相关的信息，如发行版名称、发行版代号、发布或版本信息等。`lsb_release` 命令的一个常用选项是 `-a`。例如，`lsb_release -a`。

## 谁在线：who

在具有许多账户可以同时在本地或远程登录的多用户系统中，系统管理员可能需要知道谁正在在线。
使用以下命令可以生成一份显示所有在线用户以及其他有用统计数据的报告：

```
[yyang@server -]$ who

yyyang pts/0 2017-02-07 10:10 (192.168.2.12)

yyyang pts/1 2017-02-07 10:35 (10.1.122.1)
```
