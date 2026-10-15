
# 8.6.3 微状态会计

内核也支持微状态会计的概念，即在显式启用微状态会计时，对低级处理进行计时。附录 C，“示例 Procs 工具”包含一个简单程序的源代码，该程序对进程运行微状态会计，并转储微状态会计时间和资源使用计数器（如上）。

微状态会计是在典型 LWP 生命周期内发生的几次状态变化之一期间所花费时间的细粒度取值。时间戳维护在 LWP 和进程级的数组中。与资源利用的情况类似，LWP 的微状态在执行期间被记录，LWP 终止时更新数组。进程和 LWP 的微状态会计（以及资源使用结构）如下所示。

```c
/* 微状态会计、资源使用和实时分析 */
hrtime_t p_mstart;               /* 高分辨率进程开始时间 */
hrtime_t p_mterm;               /* 高分辨率结束时间 * */
hrtime_t p_mreal;               /* 已结束 LWP 的时间总和 */
hrtime_t p_acct[NMSTATES];      /* 已结束 LWP 的微状态 * */
struct lusage_ru;               /* 已结束 LWP 的 lusage * */
```

```c
struct mstate {
    int m_prev;                     /* * 上一个 mstate * */
    nhrtime_t m_start;              /* * lwp 创建时间 * */
    nhrtime_t m_term;               /* * lwp 终止时间 * */
    time_t m__start;          /* 启用微状态会计的进程开始时间 */
    time_t m_acct[NMSTATES];      /* 启用微状态会计的 LWP 状态 * */
    /* 处理处理器的微状态 */
};
/* 进程级 资源使用 */
struct lusage_ru;
```

内核支持在显式启用微状态会计时，对低级处理进行计时。

## Procs —进程文件

### 表 8-4 使用字段（续）

| 字段 | 描述 |
| --- | --- |
| `nswap` | LWP 被换出的次数。在 LWP `swapout()` 代码中增加。 |
| `inblock` | 输入块数。在块设备 I/O 子系统（`bio.c`）的块读取时增加。 |
| `outblock` | 输出块数。同上，在 `bio.c` 的块设备写入时增加。 |
| `msgsnd` | 发出的 STREAMS 消息。在 `putmsg()` 的 STREAMS Common代码中增加。 |
| `msgrcv` | 接收到的 STREAMS 消息。在 `getmsg()` 的 STREAMS Common代码中增加。 |
| `nsignals` | 接收到的信号数。在 `psig()` 代码中增加，当 LWP 被设置为运行信号处理程序时。 |
| `nvscw` | 自愿上下文切换次数。当 LWP 阻塞（进入睡眠）、等待 I/O 或同步原语时增加。 |
| `nicsw` | 非自愿上下文切换次数。当 LWP 使用完分配的时间片或被高优先级线程抢占时增加。 |
| `sysc` | 系统调用数。在系统调用中断处理程序（`trap`）中增加。 |
| `ioch` | 读取和写入的字符数。在读/写系统调用代码中增加。 |

资源利用计数器不需要进程或 LWP 的微状态会计。它们可以通过 `procs` 维护的状态访问，其中 `/proc/<PID>/usage` 代表进程级的使用，而 `/proc/<PID>/<LWP_ID>/lwusage` 代表每个 LWP 的。参见附录 C，“示例 Procs 工具”。

在进程内部，操作系统维护一个高分辨率时间戳来标记进程的开始和结束时间。进程开始时间 `p_start` 字段在进程创建时于内核 `fork()` 代码中设置，进程结束时间 `p_term` 在内核 `exit()` 代码中设置。在启用微状态会计的 LWP 中，也会维护开始和结束时间。相关的 `p_mlreal` 字段包含了根据开始和结束时间得出的 LWP 经过时间。

系统使用内部 `gettime()` 例程 `get_high_resolution_time`（等同于 `gettimeof(3)` API）。调用 `get_high_resolution_time` 时，它返回一个用纳秒表示的 64 位值。该值与当前时间无关，只有在与后续 `gettime()` 使用时才有用。在这种情况下，第一次调用和第二次调用返回值差异提供了纳秒级经过时间的高分辨率测量。这正是启用微状态会计时的使用方法。例如，进程创建期间设置的 `p_mstart` 值与进程终止时设置的 `p_mterm` 值之间的差异产生了进程的经过时间。`p_mreal` 是进程所有 LWP 经过时间的总和，采用类似的方式。细粒度的纳秒级值来自处理器中的硬件寄存器，在 UltraSPARC 处理器上维护 CPU 时钟周期计数，即 `TICK` 寄存器。特定处理器的转换例程根据处理器时钟周期将寄存器值转换为纳秒。
