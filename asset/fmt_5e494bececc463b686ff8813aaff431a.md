
| :--- | :--- | :--- |

| `egroup` | `EGROUP` | 有效组 ID。如果可以获取且字段宽度允许，则显示文本形式的组 ID，否则显示十进制表示。（别名 `group`） |
| `eip` | `EIP` | 指令指针。 |
| `esp` | `ESP` | 栈指针。 |
| `eti` | `ELAPSED` | 自进程启动以来经过的时间，格式为 [[DD-]hh:]mm:ss。 |
| `etis` | `ELAPSED` | 自进程启动以来经过的时间，以秒为单位。 |
| `euid` | `EUID` | 有效用户 ID（别名 `uid`）。 |
| `euser` | `EUSER` | 有效用户名。如果可以获取且字段宽度允许，则显示文本形式的用户 ID，否则显示十进制表示。可以使用 `n` 选项强制显示十进制表示。（别名 `una`, `user`）。 |
| `f` | `F` | 与进程关联的标志，参见 `PROCESS FLAGS` 章节。（别名 `flag`, `flags`）。 |
| `fgroupid` | `FGROUP` | 文件系统访问组 ID。（别名 `fsuid`）。 |
|  |  | 文件系统访问组 ID。如果可以获取且字段宽度允许，则显示文本形式的组 ID，否则显示十进制表示。（别名 `fsgroup`）。 |
| `flag` | `F` | 参见 `f`。（别名 `f`, `flags`）。 |
| `flags` | `F` | 参见 `f`。（别名 `f`, `flag`）。 |
| `fna` | `COMMAND` | 进程可执行文件基名的前 8 个字节。此列中的输出可能包含空格。 |
| `fuid` | `FUID` | 文件系统访问用户 ID。（别名 `fsuid`）。 |
| `fuser` | `FUSER` | 文件系统访问用户 ID。如果可以获取且字段宽度允许，则显示文本形式的用户 ID，否则显示十进制表示。 |
| `gid` | `GID` | 参见 `egid`。（别名 `egid`）。 |
| `group` | `GROUP` | 参见 `egroup`。（别名 `egroup`）。 |
|  |  | 被忽略信号的掩码，参见 `(7)`。根据字段的宽度，将以十六进制格式显示 32 位或 64 位掩码。（别名 `sig_ignore`, `signoore`）。 |
| `ipcns` | `IPCNS` | 描述进程所属命名空间的唯一 inode 号。参见 `(7)`。 |
| `label` | `LABEL` | 安全标签，最常用于 SELinux 上下文数据。这是在高安全系统上发现的*强制访问控制*（"MAC"）。 |
| `lstart` | `STARTED` | 命令启动时间。另请参阅 `bsdstart`, `start`, `start_time` 和 `stime`。 |
| `lsession` | `SESSION` | 如果已包含 systemd 支持，则显示进程登录会话标识符。 |
| `ignored` | `IGNORED` |  |
| `label` | `LABEL` |  |

#### `lwp` LWP

可分派实体的轻量级进程（线程）ID（别名 `spid`, `tid`）。更多信息参见 `tid`。

#### `machine` MACHINE

如果已包含 systemd 支持，则显示分配给 VM 或容器的进程的机器名称。

#### `maj_flt` MAJFLT

与此进程相关的主要缺页中断次数。

#### `min_flt` MINFLT

与此进程相关的次要缺页中断次数。

#### `mntns` MNTNS

描述进程所属命名空间的唯一 inode 号。参见 `(7)`。

#### `netns` NETNS

描述进程所属命名空间的唯一 inode 号。参见 `(7)`。

#### `ni` NI

nice 值。范围从 19（最友好）到 -20（不友好），参见 `(1)`。（别名 `nice`）。

#### `nice` NI

参见 `ni`。（别名 `ni`）。

#### `nlwp` NLWP

进程中的 lwp（线程）数量。（别名 `thcount`）。

#### `nwchan` WCHAN

进程睡眠所在的内核函数地址（如果需要内核函数名，请使用 `wchan`）。正在运行的任务在此列中显示破折号（`-`）。

#### `ouid` OWNER

如果已包含 systemd 支持，则显示进程会话所有者的 Unix 用户标识符。

#### `pcpu` %CPU

参见 `%cpu`。（别名 `%cpu`）。

#### `pending` PENDING

待处理信号的掩码。参见 `(7)`。进程上的待处理信号与单个线程上的待处理信号不同。使用 `m` 选项或 `-m` 选项可以同时查看两者。根据字段的宽度，将以十六进制格式显示 32 位或 64 位掩码。（别名 `sig`）。

#### `pgid` PGID

进程组 ID，或者等效地，进程组领导者的进程 ID。（别名 `pgrp`）。

#### `pgrp` PGRP

参见 `pgid`。（别名 `pgid`）。

#### `pid` PID

表示进程 ID 的数字（别名 `tgid`）。

#### `pidns` PIDNS

描述进程所属命名空间的唯一 inode 号。参见 `(7)`。

#### `pm` %MEM

参见 `%m`。（别名 `%m`）。

#### `policy` POL

进程的调度类。（别名 `class`, `cls`）。可能的值为：

- 未报告 T
- SSCHED_OTHER F
- FSCHED_FIFO
- RRSCHED_RR B
- SCCHED_BATCH I
- OSCHED_ISO
- IDLSCHED_IDLE ?
- 未知值

| 字段 | 标签 | 描述 |
| :--- | :--- | :--- |
| `ppid` | PPID | 父进程 ID。 |
| `pri` | PRI | 进程的优先级。数字越大，优先级越低。 |
| `psr` | PSR | 当前分配给该进程的处理器。 |
| `rgid` | RGID | 真实组 ID。 |
| `rgroup` | RGROUP | 真实组名。如果可以获取且字段宽度允许，则显示文本形式的组 ID，否则显示十进制表示。 |
| `rss` | RSS | 常驻集大小，即任务使用的未交换物理内存（单位为千字节）。（别名 rssize,rsz）。 |
| `rssize` | RSS | 参见 rss。（别名 rss,rsz）。 |
| `rsz` | RSZ | 参见 rss。（别名 rss,rs size）。 |
| `rtprio` | RTPRIO | 实时优先级。 |
| `ruid` | RUID | 真实用户 ID。 |
| `ruser` | RUSER | 真实用户 ID。如果可以获取且字段宽度允许，则显示文本形式的用户 ID，否则显示十进制表示。 |
| `s` | S | 最小状态显示（单个字符）。不同值参见 PROCESS STATE CODES 章节。如果需要显示更多信息，另请参阅 stat。（别名 state）。 |
| `sched` | SCH | 进程的调度策略。策略 SCHED_OTHER (SCHED_NORMAL), SCHED_FIFO, SCHED_RR, SCHED_BATCH, SCHED_ISO 和 SCHED_IDLE 分别显示为 0, 1, 2, 3, 4 和 5。 |
| `seat` | SEAT | 如果已包含 systemd 支持，则显示与分配给特定工作场所的所有硬件设备关联的标识符。 |
| `sess` | SESS | 会话 ID，或者等效地，会话领导者的进程 ID。（别名 session,sid）。 |
| `sgi_p` | P | 当前正在执行该进程的处理器。如果进程当前未运行或不可运行，则显示“*”。 |
| `sgid` | SGID | 已保存的组 ID。（别名 sgid）。 |
| `sgroup` | SGROUP | 已保存的组名。如果可以获取且字段宽度允许，则显示文本形式的组 ID，否则显示十进制表示。 |
| `sid` | SID | 参见 sess。（别名 sess,session）。 |
| `sig` | PENDING | 参见 pending。（别名 pending,sig_pend）。 |
| `sigcatch` | CAUGHT | 参见 caught。（别名 caught,sig_catch）。 |

#### `signore`

参见 ignored。 (别名 ignored, sig_ignore)。

#### `sigmask`
