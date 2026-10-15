
刚刚展示的“树”示例说明了显示进程层次结构的不同方法。输出经过截取，以便比较几个具有不同输出的相同进程。请注意，`PPID`（父进程 ID）是启动子进程的进程 ID。`sshd` 显示了一个正在运行的 Shell 守护进程，该用户正通过网络登录，导致启动了 `bash` shell（最终启动了 `vim` 编辑器）。`httpd` 守护进程代表 Apache Web 服务器，该进程由 `root` 用户启动，而子进程则以 `apache` 用户身份启动。最后一个示例显示了 `ptree` 命令，它专门用于显示进程树。

如果您更喜欢对 `ps` 输出进行个性化视图，可以使用 `-o` 选项精确选择要显示哪些列数据。然后，您可以使用 `--sort` 选项根据这些任何一个数据对输出进行排序。表 9-1 显示了可用的列输出以及添加到 `-o` 的选项，以便用 `ps` 打印每一列。

## 表 9-1：选择和查看 ps 列输出

| 选项 | 列标题 | 说明 |
|---|---|---|
| %cpu | %CPU | 进程在生命周期内的 CPU 占用率，格式为 00.0 |
| %mem | %MEM | 进程占用物理内存的百分比（驻留集大小） |
| args | COMMAND | 带有所有参数的命令 |
| bsdstart | START | 启动命令的时间：HH:MM 或 月 日 |
| bsdtime | TIME | 总（用户和系统）CPU 时间 |
| comm | COMMAND | 仅命令名（不显示参数） |
| cp | CP | 以百分比十分为单位的 CPU 占用率 |
| cputime | TIME | 格式为 [DD-]HH:MM:SS 的总 CPU 时间 |
| egid | EGID | 进程的有效组 ID（整数） |
| egroup | EGROUP | 进程的有效组 ID（名称形式） |
| etime | ELAPSED | 自进程启动以来的时间，格式为 [[DD-]HH]:MM:SS |
| euid | EUID | 进程的有效用户 ID（整数） |
| euser | EUSER | 进程的有效用户 ID（名称形式） |

# 第 9 章：检查和管理运行中的进程

## 表 9-1：选择和查看 ps 列输出（继续）

| 选项 | 列标题 | 说明 |
|---|---|---|
| fgid | FGID | 文件系统访问组 ID（数字形式） |
| fgroup | FGROUP | 文件系统访问组 ID（名称形式） |
| fname | COMMAND | 命令名的前八个字符 |
| fuid | FUID | 文件系统访问用户 ID（数字形式） |
| fuser | FUSER | 文件系统访问用户 ID（名称形式） |
| l1start | STARTED | 命令启动的日期和时间 |
| nice | NI | Nice 值，从 19（最低）到 -20（CPU  者） |
| pgid | PGID | 进程组 ID |
| pid | PID | 进程 ID 号 |
| ppid | PPID | 进程的父进程 ID |
| psr | PSR | 进程分配的处理器（第一个 CPU 是 0） |
| rgid | RGID | 真实组 ID（数字形式） |
| rgroup | RGROUP | 真实组（名称形式） |
| rss | RSS | 非交换物理内存（驻留集大小），单位 KB |
| rprio | RTRIO | 实时优先级 |
| ruid | RUID | 真实用户 ID（数字形式） |
| ruser | RUSER | 真实用户（名称形式） |
| s | S | 单字符状态显示（D:睡眠，不可中断；R:运行中；S:睡眠，可中断；T:停止；W:分页；X:死亡；Z:僵尸） |
| sess | SESS | 会话领导者的会话 ID |
| sgi_p | P | 当前运行的处理器 |
| size | SZ | 如果进程被交换出，所需的近似交换空间 |
| start | STARTED | 命令启动时间：HH:MM:SS 或 月 日 |

## 表 9-1：选择和查看 ps 列输出（继续）

| 选项 | 列标题 | 说明 |
|---|---|---|
| start_time | START | 启动时间：HH:MM 或 月 日 |
| stat | STAT | 多字符状态：单字符 "s" 加上其他字符（<:高优先级；N:低优先级；L:内存中锁定页面；s:会话领导者；I:多线程；+:在前台进程组） |
| sz | SZ | 进程核心的大小（物理页） |
| tname | TTY | 控制的ty（终端） |
| user | USER | 进程的有效用户 ID（名称形式） |
| vsize | VSZ | 进程的虚拟内存（1024 字节为单位） |

注意，某些本应打印用户名的值如果名称太长无法适应给定的空间，仍可能打印数字（UID）。

通过使用逗号分隔的列选项列表，您可以生成自定义输出。以下是运行中进程自定义视图的示例：

这里是 `ps` 命令的其他几个示例：

```
$ ps -C httpd 显示正在运行的 httpd 进程

PID TTY TIME CMD

1493 ? 00:00:00 httpd

1495 ? 00:00:00 httpd
```

注意，您需要安装 HTTP 服务器（如 Apache）来运行 `httpd` 进程。

```
$ ps -p 5413 -o pid,ppid,bdstime,args 显示 PID 5413 的信息

PID PPID TIME COMMAND

5413 1 0:08 -m /dev/input/mice
```

```
$ ps -U chris,francois -o pid,user,tty 显示 2 个用户的信息

  PID USER TT STAT

1010 chris pts/0 S

5951 francois pts/1 SS+ /bash
```

## 使用 top 查看活动进程

如果您想持续查看运行的进程，可以使用 `top` 命令。`top` 命令运行一个持续更新的屏幕定向视图。如果不带选项启动 `top` 命令，它将显示系统运行时间、任务、CPU 使用率和内存占用，随后是按 CPU 使用率排序的运行进程列表。例如下：

```
top - 10:24:01 up 1 day,  1:20,  1 user, load average: 0.00, 0.01, 0.05

Tasks: 150 total,   1 running, 149 sleeping,   0 stopped,   0 idle,   0 wait

Cpu(s):  0.3%us,  0.0%sy,  99.7% id,  0.0% ni,  0.0% si,  0.0%wa

Mem usage:  8192.0 total,   7000.0 free,  1100.0 used,   100.0 buff

Swap:   2048.0 total,   2048.0 free,     0.0 used

  PID    USER      PR  NI    VIRT    RES    SHR  S S COMMAND

 1234 root      20    0  500000   50000  20000 S   0:00 httpd

 5678 chris     20    0  200000   10000    5000 S   0:00 -bash
```

# 第9章：检查和管理运行进程

你也可以搜索与特定用户相关的进程：

```bash
$ pgrep -lu chris    列出用户 chris 拥的所有进程
2551 sshd
2552 bash
2803 vim
```

使用 `pgrep` 最有用的方法是找到运行进程的进程 ID (`PID`)，并将这些 PID 管道传输到另一个命令以生成输出。以下是一些示例（如果 `metacity` 或 `firefox` 正在运行，请查找其他命令）：

```bash
$ ps -p 'pgrep metacity'    搜索 metacity 并运行 ps (短格式)
PID TTY                 TIME
2778 ?                 00:05:00 metacity
$ ps -fp $(pgrep xinit)      搜索 xinit 并运行 ps (全格式)
UID PID PPID Aug4 TIME CMD
chris 2689 2678 tty1 00:00 /etc/X11/xinit/xinitrc
# renice -5 $(pgrep firefox)  搜索 firefox，提高其优先级
20522: old priority 0, new priority -5
20557: old priority 0, new priority -5
```
