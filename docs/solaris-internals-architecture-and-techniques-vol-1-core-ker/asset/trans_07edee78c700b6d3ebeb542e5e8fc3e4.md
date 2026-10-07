

# 表 8-4 使用字段（续）

| 字段 | 描述 |
|---|---|
| nswap | LWP 被交换出的次数。在 LWP 的 `swapout()` 代码中增加。 |
| inblock | 输入块数量。在内核块 I/O 子系统（`bio.c`）中，针对设备读取时增加。 |
| outblock | 输出块数量。与上所述，在 `bio.c` 中，针对设备写入时增加。 |
| msgsnd | 发出的 STREAMS 消息数。在 STREAMS 通用代码的 `putmsg()` 中增加。 |
| msgrcv | 接收到的 STREAMS 消息数。在 STREAMS 通用代码的 `getmsg()` 中增加。 |
| nsignals | 接收到的信号数。在内核 `psig()` 代码中增加，该处 LWP 被设定为运行信号处理程序。 |
| nvcw | 自愿上下文切换次数。当 LWP 发生阻塞（进入睡眠状态）等待 I/O 或同步原语时增加。 |
| nivscw | 非自愿上下文切换次数。当 LWP 用完分配的时间片或被高优先级内核线程（kthread）抢占导致上下文切换时增加。 |
| sysc | 系统调用次数。在系统调用中断处理程序中增加。 |
| ioch | 读写字符数。在读/写系统调用代码中增加。 |

资源利用计数器不需要对进程或 LWP 微状态统计（microstate accounting）。可以通过 `procs` 维护的用法结构进行访问，其中 `/proc/<PID>/usage` 代表进程级使用，`/proc/<PID>/lwp/<LWP_ID>/lwusage` 代表每个 LWP 的使用数据。参见附录 C，“示例 Procs 工具”代码。

在进程内部，操作系统维护了一个高分辨率时间戳，标记进程的开始和结束时间。`p_start` 字段（开始时间）在进程创建时于内核 `fork()` 中设置，而进程结束时间 `p_term` 在内核 `exit()` 代码中设置。在启用了微状态统计的 LWP 中也维护了开始和结束时间。相关的进程 `p_real` 字段包含了 LWP 从开始到结束的经过时间总和。

 系统使用内部例程 `gethrtime()`，即 `get_high_resolution_time`（有一个相应的 `gethrtime(3)` API）。当调用 `get_high_resolution_time` 时，它返回一个以纳秒表示的 64 位值。该值与当前时间无关，因此与后续调用 `gethrime()` 结合使用非常有用。在情况下，

# 316 Solaris 多线程进程架构

第一次调用和第二次调用返回值之差就产生了以纳秒为单位的经过时间的高分辨率测量。这正是在启用微状态统计时的使用方式。例如，在进程创建期间设置的 `p_mstart` 值与进程结束时设置的 `p_mterm` 值之间的差，即为进程的经过时间。同样地，`p_mlreal` 是进程所有 LWP 的总经过时间。这些细粒度的纳秒级值源于处理器中的一个硬件寄存器，该寄存器维护着 CPU 时钟周数的计数（在 UltraSPARC 处理器上，它是 `TICK` 寄存器）。特定处理器的程序根据时钟频率将寄存器值转换为纳秒。

### 8.6.3 微状态统计

微状态统计是在典型 LWP 生命周期内对时间值进行细粒度的检索。时间戳维护在 LWP 和进程层级的数组中。与资源利用的情况一样，LWP 微状态在执行期间被记录，并在 LWP 终止时更新进程中的数组。进程和 LWP 的微状态统计（以及资源使用结构）如下所示。

层级用法和微状态统计（来自 /usr/include/sys/proc.h）：

```
/*
 * 微状态统计、资源使用和实时性能分析
hrtime_t p_mstart;              /* 高精度进程开始时间 */
hrtime_t p_mterm;               /* 高精度进程结束时间 */
hrtime_t p_mlreal;              /* 已失效 lwp 的经过时间总和 */
hrtime_t p_acct[NMSTATES];      /* 已失效 lwp 的微状态总和 */
struct lusage lwp_ru;          /* 已失效 lwp 的使用总和 */

层级用法和微状态统计数据（来自 /usr/include/sys/lwp.h）：
struct mstate {
    int mprev;                  /* 上一个运行的 mstate */
    nhrtime_t m_start;          /* lwp 创建时间 */
    nhrtime_t m_term;           /* lwp 终止时间 */
    nhrtime_t m_state_start;    /* 此 mstate 的开始时间 */
    nhrtime_t m_acct[NMSTATES]; /* 每个 mstate 的统计 */
} lwp_mstate;
/*
 * 每个 lwp 的资源使用。
 struct lusage lwp_ru;
```

# Procs - 进程文件系统

默认情况下禁用微状态统计以将开销降至最低。开启微状态统计必须通过 `/proc` 编程实现。必须打开控制文件 `/proc/<pid>/ctl` 并以 `write(2)` 的形式向控制文件发送控制消息，这需要一个操作符（PCSET）和一个操作数（PR_MSACCT）。以下是如何在进程中启用微状态统计的部分代码示例。

```
int control[2];
/* 启用微状态统计 */
control[0] = PCSET;
control[1] = PR_MSACCT;
fd = open("/proc/self/ctl", O_WRONLY);
write(fd, control, sizeof(control));
```

一旦启用了微状态统计，内核在进程状态切换时记录 LWP 的微状态。这反映了 LWP 状态。

