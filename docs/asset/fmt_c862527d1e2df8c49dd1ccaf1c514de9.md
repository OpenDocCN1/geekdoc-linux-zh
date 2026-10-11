
"F" 选项列出更多信息。"x" 选项显示 CPU 和内存的使用情况。

## 按 'F' 键调出窗口，允许按列进行排序

当前排序字段：对于窗口 3:Mem
- PID: 进程 ID u: nFLT
- b PID: 父进程 ID v: nDRT 脏页计数 (Dirty Pages count)
- c RUSER: 真实用户名 w: S 进程状态
- d UID: 用户 ID x: COMMAND 命令/命令行
- e USER: 用户 ID y: WCHAN 睡眠所在的函数
- f GROUP: 组名 g: Flags 任务标志 `<sched.h>`
- g TTY: 控制终端 TTY
- h PR: 优先级
- i J: Nice 值
- k CPU CPU: 上次使用的 CPU 副本 (CPU)
- l TIME: CPU 时间
- m M: n MEM: 已用内存 (RES)
- o VIRT: 虚拟内存 (kb)
- p SWAP: 交换大小 (kb)
- q RES: 驻留大小 (kb)
- s DATA: 数据+大小 (kb)
- t SHR: 共享内存大小 (kb)

如果选定的字段无法在屏幕上显示或不在字段范围内，则 '<' 和 '>' 键将不可用，直到选择了 `xrange` 范围内的字段。

注意 2：
字段排序使用内部值，而非列显示值。因此，TTY 和 WCHAN 字段将产生严格的排序（如果选择了 WCHAN 也是如此）。

启动 `top` 的不同方式：
- `top -u <username>`: 显示特定用户的进程
- `top -p 1208, 1425` - 使用 'batch' 模式输出到文件或管道（文本格式而非二进制）`-n 14` 迭代 14 次
- `top -n 1 -b -top-output` - 使用 'batch' 模式输出到文件
- `top -i` 仅显示活动进程（忽略空进程）

请注意 `top` 有多个版本，其选项和用法方法略有不同。检查你的 `top` 版本并使用 `-o` 选项。
例如，如果 HTOP 用起来更方便，但消耗的系统资源是 5 倍。

在读取 `top` 中的 `/i` 驻留内存列时，请记住它显示的是“页”（pages）——内存页默认约为 40kb，因此你需要将结果乘以 4 才能获得实际内存大小（resident 是物理内存）。
请记住部分 RAM 可供应用程序使用，同时也用于磁盘缓冲区（buffer/cache）。

## 内存到底有多少空闲？（磁盘缓冲区/缓存）

| | 总计 (total) | 已用 (used) | 空闲 (free) | 共享 (shared) | 缓冲区 (buffers) | 缓存 (cached) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Mem | 1504 | 1491 | 13 | 0 | 76 | |
| +buffers/cache | | | | 635 | 869 | |
| Swap | 2047 | 0 | | | | |

如果你不理解这些数字，`top` 可能会显示 RAM 空闲率为 99%，但实际上只有 42% (635MB)。此外，635+869-13=1493 为 "used"，而 91+764-13=~869 为 "free"。

这里使用了 735MB。
735+1098-76=1757 被称为 "used"（缓冲区/缓存中的空闲 减去内存中的空闲 = 报告的已用）。
Shared 是共享库。Buffer 是数据需要提交（commit）时的情况。
Cache 是因为移动到空闲资源的大文件被尽可能地保留在 RAM 中（优化）。当需要重新分配资源时，缓存会释放。
此外考虑 1757 "used" 减去 1021 缓存是真实的 735。（735+1098 是报告的总数 1834）。这里我们实际上有 1098 可用。

- `/buffers/cache` 的数字是真实的。

## sysstat 套件与 sar

`sysstat` 包含这些程序：CPU、I/O 统计，`mstat`（CPU 统计）、`pidstat`（进程统计）、`nfiostat`（NFS 相关统计）以及 `cifsat`（CIFS 统计）。该套件的核心是 `sar` 收集和报告套件，此外它们还有各自的扩展。

**`sadc` - 系统活动收集器。** 将二进制数据写入 `/var/log/`，命名为 "sa-dd"（d 是每月日期）。
**`sa1` -** 用于通过 cron 或系统运行 `sadc` 的查询程序。收集并将数据存储在系统活动每日数据文件中。
**`sar` - 系统活动报告器。** 从 `sadc` 文件生成报告。将 ascii 文件写入 `/var/log/`，命名为 "sa-dd"。
**`sa2` -** 用于通过 cron 或系统运行的查询程序。写入一份摘要的每日活动报告。
**`sadf`** 以 CSV、XML、JSON 等格式输出报告，以便你可以将其输出到其他程序。还支持 SVG 图表。

安装方法：

- 如果从源码安装：运行 `/configure --enable-install-cron`，然后执行 `make install`。
- `--enable-install-cron` 选项会确保为你创建 `/etc/rc.d/` 。
- 使用 `/usr/local/bin` 安装可执行文件。
- （旧问题？）运行 `echo alias sar=LANG=C >> ~/.bashrc` 以确保 `sar` 使用 24 小时制。

确保 cron 已设置：

- 如果你的 `sysstat` 版本没有自动设置，请在 `/etc/cron.d` 目录下创建一个包含历史数据的文件。
- `vi /etc/cron.d/sysstat`
- `*/10 * * * root /usr/local/lib/sa/sa1 1`
- `53 23 * root /usr/local/lib/sa/sa2 -A`

- 如果是从源码安装的，`sadc` 和 `sa2` 可能位于 `/usr/local/lib/sa` 和 `/usr/lib/sa/sa2`。
- 如果是用包管理器安装的，它们可能位于 `/usr/lib/sa/sa1` 和 `/usr/lib/sa/sa2`。
- 上述运行 `sa1` 每 10 分钟收集一次数据，并在午夜通过 `sa2` 完成数据收集。
- 使用 "1 f" 运行 `sar -` 每每隔 1 秒运行一次。

日志管理：

生成的日志仅保留有限时间（通常为约 28 天）。一种方案是在删除前运行脚本进行备份；配置文件 `/etc/sysconfig/sysstat` 有一个 `HISTORY` 参数，用于指定你想保留日志文件的天数。最大为 28 天，但如果设置为某个值，日志将按月目录存储。此时，日志将指向名为 `YYYYMMDD` 的符号链接。

- `sar -U ALL 1` - 每 1 秒报告一次 CPU 使用率（百分比 %），持续 3 分钟；`ALL` 选项提供扩展信息。
- `sar -f /var/log/sa/10` - 报告特定日的统计；这里是本月的 10 号（在文件 `sa10` 中）。
- `sar -P 1` - 仅显示活动进程（忽略空进程）。

## iostat - 设备和分区的 CPU 及 I/O 统计

`iostat [option] [count]`
每次报告之间的间隔时间（秒），以及在退出前生成的报告数量。
`iostat 2 -5` - 表示间隔为 2 秒，执行 5 次迭代。如果你不指定迭代次数，它将将持续运行。
首次运行时，第一份报告包含自系统启动以来的信息，而随后的每份报告都涵盖自上份报告生成以后的时间段，你可能需要忽略第一份。

普通输出的第一部分涵盖 CPU 占用率，对于 Top 等其他工具来说，这部分是不言自明的。前两列显示了带有待处理 I/O 请求（等待活动延迟）和无待处理 I/O 请求的 %CPU 空闲时间。如果你只想获取报告中的这部分，请运行 `iostat -c`。

| Linux 2.6.31-17-generic (dt-laptop) | 03/24 | i686_0 (1 CPU) |
|---|---|---|
| avg-cpu: %user | %nice | %sys | %iowait | %rdq | %soft | %steal | %guest | %idle |
| 25.99 | 0.08 | 7.43 | 12.77 | 53.03 | | | | | | |

| Device: %util | Blk/s | Blk/wrt | Blk_read | Blk_wrt |
|---|---|---|---|---|
| sda | | 27.40 | 797.19 | 201.27 | 802208 |
| sdb | 0.03 | 1.24 | | 0 | 1248 |

设备报告每秒报告数、每秒块数、每秒写入块数、总读取块数和总写入块数。当你使用 `-k`（KB）或 `-m`（MB）将唯一设备报告中的四列转换为人类可读的术语（而不是扇区）时，请运行 `iostat -k`。
`iostat -x` 给出扩展报告的统计数据。
使用冒号语法添加设备标识符将报告限制为指定的设备。
在其中它将显示有关分区的数据，`-N` 给出 LVM 名称和统计数据。
对于 NFS 使用，`iostat -n` `iostat -j` 激活空闲设备。
像任何操作一样，将输出重定向到文件，或使用 `awk` 提取你需要的列。
使用 `/proc/stat`, `/proc/partitions`, `/proc/diskstats`, `/proc/self/mounts`

## mpstat - 多处理器统计

如果不指定 CPU，CPU 将显示所有 CPU 的全局平均值。使用 `-P` 并输入 `ALL` 来获取所有 CPU 的统计数据。
`mpstat -P ALL`

| CPU | %user | %nice | %sys | %iowait | %rdq | %soft | %steal | %guest | %idle |
|---|---|---|---|---|---|---|---|---|---|---|
| 1:03:26 | all | 37.33 | 0.01 | 4.57 | 2.58 | 0.00 | 0.07 | 0.00 | 0.00 | 55.44 |
| 1:03:26 | all | 37.90 | 0.01 | 4.96 | 2.62 | 0.00 | 0.03 | 0.00 | 0.00 | 54.48 |

`mpstat -P 2 -5` - 带有间隔和次数用法。`-P` 选项显示每个处理器的报告，如果使用了其他选项，`-u` 显示 CPU 统计数据。
最简单的是：`mpstat -A` 是 `mpstat -u ALL` 的快速简单示例。

`pidstat 2 -5` 每隔两秒为系统中的每个活动任务提供五份 CPU 统计报告。
`pidstat -r -` 侧重于内存统计中的缺页错误：

| Time | UID | PID | minit | maxjit | VSZ | %MEM | Command |
|---|---|---|---|---|---|---|---|---|
| 1409816695 | 1000 | 3958 | 3378.22 | 0.0 | 707240 | 215972 | 5 | cinnamon |

`pidstat -d` 用于磁盘 I/O 统计
`pidstat -k 1643` 用于 PID 1643 的所有进程
输入字符串来匹配进程名（如 `-http`），使用 `pidstat -e <command>` 启动并监控可执行文件。
`pidstat -T CHILD-1643` 用于 PID 1643 的子进程。只显示非零统计值的进程。`-T ALL` 意味着所有子进程和孙进程。
不带选项的 `pidstat` 评估所有。
实时统计使用 `-R` 选项，或使用 `-h` 输出一行输出以便于用 `awk` 等轻松解析。

# Linux 性能观测性工具

![](img/4541d1f2c9832b9303a6df6c929f86f6_21_0.png)

强烈推荐：Brendan Reggg 的工作：http://www.breandreggg.com/linuxperf.html

## Linux 性能观测性：sar

![](img/4541d1f2c9832b9303a6df6c929f86f6_21_1.png)

## 命令等效项 - SysUnit 和 systemd

| 操作 | SysUnit | systemd |
|---|---|---|
| 启动/重启/重载/状态/服务 | `service nptd [ start | stop | etc... ]` | `systemctl [ start | stop etc... ] nptd.service` |
| 如果服务已运行则重启服务 | `service nptd restart` | `systemctl restart httpd.service` |
| 在启动时启用或禁用服务 | `chconfig nptd [ off | on ]` | `systemctl [ enable | disable ] nptd.service` |
| 服务是否在启动时启用（运行级别?） | `chconfig nptd` | `systemctl is-enabled nptd.service` |
| 列出可以启动或停止的服务 | `ls /etc/rc.d/init/` | `systemctl OR | systemctl list-units --type=service AND` |
| 用于列出所有服务和其他单元 | | `ls /etc/systemd/system/ | systemctl list-units` |

## SysVinit - 目录结构

通常，你会在 `/etc/` 目录下找到指向实际位于 `/etc/rc/` 目录内容的符号链接。这可能会导致困惑，因为为了兼容不再支持 Upstart 的系统，我们还有其他用于兼容的链接。本文将忽略所有这些内容，专注于 CentOS 5。

`/etc/init.d` 是指向 `/etc/rc/init.d` 目录的符号链接，`/etc/rc.d` 也是如此，它指向 `/etc/rc#.d`。同样的，脚本 `rc`、`rc.local` 和 `rc.sysinit` 链接，其实际位置也在 `/etc/rc/` 目录中。尽管你在 `/etc` 中能看到它们，但它们的实际位置如下：

- `/etc/rc.d/init.d/`
- `/etc/rc.d/rc0/`
- `/etc/rc.d/rc1/`
- `/etc/rc.d/rc5/`
- `/etc/rc.d/rc6/`
- `/etc/rc.d/rc.local`
- `/etc/rc.d/rc.sysinit`

……此类推……

服务的脚本位于 `/etc/rc.d/`。Systeminit 需要 `/etc/rc.d/` 下的脚本：
- `/etc/rc.d/<servicename>` 脚本中每个受管理的服务的前几行如下：

```bash
