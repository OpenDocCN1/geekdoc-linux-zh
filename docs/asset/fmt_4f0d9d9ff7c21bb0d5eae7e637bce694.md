
| Solaris | 0 to 39 | -incr or -n incr | +incr or -incr | incr or -n incr |
| HP-UX | 0 to 39 | -prio or -n prio | +incr or -incr | -n prio* |
| AIX | -20 to 19 | -incr or -n incr | +incr or -incr | -n incr |

a. 使用绝对优先级，但会在你指定的值上加上 20。

现代世界中最常见的 `niced` 进程是 `ntpd`，即时钟同步守护进程。由于及时性对其任务至关重要，它通常以比默认值低约 12 的 `nice` 值运行（即优先级高于正常）。

如果问题导致系统负载平均值达到 65，你可能需要使用 `nice` 启动一个高优先级 `shell`，然后才能运行命令调查问题。否则，你可能难以运行甚至简单的命令。

## 5.7 PS：监控进程

`ps` 是系统管理员监控进程的主要工具。虽然 `ps` 的版本在参数和显示上有所不同，但它们都提供本质上相同的信息。`ps` 版本之间巨大差异的一部分可以追溯到 UNIX 开发历史的差异。然而，`ps` 也是供应商倾向于出于其他原因定制的命令。它与内核对进程的处理紧密相关，因此往往反映了供应商所有底层内核更改。

`ps` 可以显示进程的 PID、UID、优先级和控制终端。它还提供有关进程使用多少内存、已消耗多少 CPU 时间以及其当前状态（运行、停止、睡眠等）的信息。僵尸进程在 `ps` 列表中显示为 `<exiting>` 或 `<defunct>`。

过去十年中，`ps` 的实现变得极其复杂。一些厂商已经放弃了定义有意义显示的尝试，并使他们的 `ps` 完全可配置。只要做一点定制工作，就几乎可以产生任何期望的输出。举例来说，Linux 使用的 `ps` 是一个三性同体且雌雄同体的版本，它理解多个选项集，并使用环境变量来告诉它所处的宇宙。

不要被所有这些复杂性吓到：它主要为开发者准备，而不是为系统管理员准备。虽然你会经常使用 `ps`，但你只需要知道几种特定的咒语。

![](img/14d78e3cecac4581d37024baf1e94cca_179_0.png)

在 Linux 和 AIX 上，你可以用 `ps aux` 获得系统中所有进程的有用概览。`a` 选项表示显示所有进程，`x` 表示显示甚至没有控制终端的进程，`u` 选择“用户导向”的输出格式。以下是 Red Hat 机器上 `ps aux` 输出的示例（AIX 上同一命令的输出略有不同）：

```
redhat$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY   STAT TIME COMMAND
root         1  0.1  0.2  3356   560 ?    S    0:00 init [5]
root         2  0    0      0     0 ?    SN   0:00 [ksoftirqd/0]
root         3  0    0      0     0 ?    S<   0:00 [events/0]
root         4  0    0      0     0 ?    S<   0:00 [khelper]
root         5  0    0      0     0 ?    S<   0:00 [kacpid]
root        18  0    0      0     0 ?    S<   0:00 [kblockd/0]
root        28  0    0      0     0 ?    S    0:00 [pdfflush]
...
root       196  0    0      0     0 ?    S    0:00 [kjournald]
root      1050  0    0.1 2652   448 ?    Ss   0:00 udevd
root      1472  0    0.3 3048  1008 ?    Ss<  0:00 /sbin/dhclient -1
root      1646  0    0.3 3012  1012 ?    Ss<  0:00 /sbin/dhclient -1
root      1733  0    0      0     0 ?    S    0:00 [kjournald]
root      2124  0    0.3 3004  1008 ?    Ss   0:00 /sbin/dhclient -1
root      2182  0    0.2 2264   596 ?    Ss   0:00 syslogd -m 0
root      2186  0    0.1 2952   484 ?    Ss   0:00 klogd -x
rpc       2207  0    0.2 2824   580 ?    Ss   0:00 portmap
rpcuser   2227  0    0.2 2110   760 ?    Ss   0:00 rpc.statd
root      2260  0    0.4 5668  1084 ?    Ss   0:00 rpc.idmapd
root      2336  0    0.2 3268   556 ?    Ss   0:00 /usr/sbin/acpid
root      2348  0    0.8 9100  2108 ?    Ss   0:00 cupsd
root      2384  0    0.6 4080  1660 ?    Ss   0:00 /usr/sbin/sshd
root      2399  0    0.3 2780   828 ?    Ss   0:00 xinetd -stayalive
root      2419  0    1.1 7776  3004 ?    Ss   0:00 sendmail: accept
...
```

方括号中的命令名实际上根本不是命令，而是作为进程调度的内核线程。每个字段的含义在下一页的表 5.4 中显示。

Linux 和 AIX 上另一组有用的参数是 `lax`，它提供更技术性的信息。`a` 和 `x` 选项与上述相同（显示每个进程），并且

### 表 5.4 ps aux 输出说明

| Field | Contents |
|-------|----------|
| USER | 进程所有者的用户名 |
| PID | 进程 ID |
| %CPU | 该进程使用的 CPU 百分比 |
| %MEM | 该进程使用的实际内存百分比 |
| VSZ | 进程的虚拟大小 |
| RSS | 常驻集大小（内存中的页数） |
| TTY | 控制终端 ID |
| STAT | 当前进程状态：<br>R = 可运行        D = 在不可中断睡眠中<br>S = 睡眠（< 20 秒） T = 被跟踪或停止<br>Z = 僵尸<br>附加标志：<br>W = 进程已被换出<br>< = 进程具有高于正常的优先级<br>N = 进程具有低于正常的优先级<br>L = 部分页面被锁定在内存中<br>s = 进程是会话领导者 |
| TIME | 进程已消耗的 CPU 时间 |
| COMMAND | 命令名和参数* |

a. 程序可以修改此信息，因此它不一定准确代表实际命令行。

`l` 选择“长”输出格式。`ps lax` 运行起来也比 `ps aux` 稍快，因为它不必将每个 UID 翻译成用户名——如果系统已经不堪重负，效率可能很重要。

如下所示的简略示例中，`ps lax` 包含父进程 ID（PPID）、`nice` 值（NI）以及进程正在等待的资源类型（WCHAN）等字段。
