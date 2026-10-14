
在考察了两个按固定间隔发生的 TS/IA 特定函数——`ts_tick()` 和 `ts_update()`，它们都由时钟中断处理程序驱动——之后，我们需要确保每个函数的预期用途之间的区别是清晰的。`ts_tick()` 旨在处理*正在*处理器上运行的线程。`ts_update()` 旨在处理*未在*处理器上运行、而是位于调度队列或睡眠队列上的线程。如果你在前面的讨论细节中迷失了方向，我们认为有必要把这个要点讲清楚。

正如我们之前指出的，IA 类线程在很大程度上由刚才描述的 TS 类函数处理。为 IA 类定义的类特定函数包括初始化 IA 类的代码、获取类特定信息的代码，以及用于发送和获取类参数的支持代码。`ia_init()` 代码非常少，因为 IA 类的大部分工作都在 TS 类代码中完成。`ia_init()` 设置其调度类、指向其类函数表的指针以及其最大全局优先级（与 TS 一样是 59）。用户模式优先级支持函数 `ia_parms()`、`ia_getparms()` 和 `ia_parmsget()` 在流程和功能上跟踪等价的 TS 支持代码。

进程由 IA 类特定例程 `ia_set_process_group()` 放入 IA 类，该例程在 TTY 被新的进程组接管时从 STREAMS `ioctl()`（`strioctl()`）调用——`ioctl` 是 I/O 控制调用，受所有字符设备驱动程序支持。它源于内核中基于 STREAMS 的终端驱动程序代码。如果你启动 Solaris 桌面系统但不启动窗口系统，那么不会有任何 IA 进程在运行（只有 TS 和 SYS 类 Solaris 守护进程）。当窗口系统启动时，它会接管“终端”的控制权，在桌面环境中，这个终端就是键盘、鼠标以及显卡到显示器的接口。

接管操作会生成 set-process-group `ioctl` 调用，该调用最终调用 `CL_SET_PROCESS_GROUP` 宏。由于调用者是交互式进程（窗口系统软件确保了这一点），这个宏会解析为 IA 类特定函数 `ia_set_process_group()`。与窗口系统关联的所有进程都被放入 IA 类。由于进程和线程都是从父进程继承调度类，因此新创建的进程（终端窗口、应用程序）也被放入 IA 类。IA 类线程会获得一个值为 10 的优先级提升量，该提升量在线程的用户模式优先级计算时被计入，也就是说，每次调整线程优先级时都会计入。回想一下，用户优先级是 `ts_cpupri`、`ts_upri` 和 `ts_boost` 之和。（对于 IA 类线程，`ts_boost` 的固定值为 10。）

处理 RT 类线程要简单得多：由于 RT 优先级是固定的，在线程执行生命周期内既不会变高也不会变低。RT 类线程优先级发生变化的唯一方式是，通过 `priocntl()` 命令或系统调用显式更改。当线程进入 RT 调度类（通过 `priocntl()` 调用 `rt_enterclass()`）时，除非指定了优先级，否则线程的 RT 类优先级（`rtproc` 结构中的 `rt_pri`）被设置为默认值 0；也就是说，`rt_pri` 将反映所请求的优先级（前提是它在类的有效范围内）。`rt_pquantum`（也在 `rtproc` 中）被设置为调度表中与优先级索引的对应行号相对应的 `rt_quantum` 值。例如，默认的 RT 类优先级

值为 0 时，时间片为 1000，即 1000 毫秒，或 100 个时钟滴答（参见第 362 页“分派表”中关于 RES 的描述）。

如果线程当前正在某个处理器上运行，则线程的全局优先级会被设置到 `t_pri` 中，代码会查看分派队列，以确定当前线程的优先级是否高于位于某个分派队列上的最高优先级线程。如果是，则将 `rt_timeleft` 设置为 `rt_pquantum`，并允许线程继续运行；否则，强制线程交出处理器。如果线程当前未在运行，则会调用 `thread_change_pri()` 代码（与 TS/TA 示例中描述的函数相同），并将线程放到相应的分派队列上。下面的伪代码说明了这一系列事件。

```text
rt_enterclass()
    if (not superuser)
        return /* must be root to use RT class */
    if (no user-supplied priority)
        rtproc->rt_pri = 0
        rtproc->rt_pquantum = rt_dtbl[0].rt_quantum;
    else
        rtproc->rt_pri = user-supplied priority;
        if (user-supplied time quantum) /* -t flag in priocntl */
            rtproc->rt_pquantum = user-supplied time quantum
        else
            rtproc->rt_pquantum = rt_dtbl[1].rt_quantum;
    if (thread is running)
        kthread->t_pri = rt_dtbl[rt_pri].rt_globpri;
        if (thread priority > highest-priority thread on a queue)
            rtproc->rt_timeleft = rt_pquantum;
        else
            surrender the processor
    else /* thread is not running */
        thread_change_pri(new-priority)
```

其他一些例行工作——初始化 `rtproc` 的其他成员，以及设置 `rtproc` 和 `kthread` 结构中的指针——是在 `rt_enterclass()` 中完成的，但上面的代码中并未显示。

如果线程是从另一个 RT 线程 `fork` 出来的，它也会进入 RT 类，因为子线程会从父线程继承其调度类。在 `rt_fork()` 代码中，子线程继承父线程的优先级和时间片。RT 类中父线程和子线程的执行顺序与 TS/IA 类线程不同。当 `fork` 一个 TS/IA 类线程时，按照设计，子线程会先执行（在使用 `vfork()` 时尤其如此，如上一章所述）。RT 子线程最终会进入分派队列，而父线程继续运行，当然，除非应用程序代码明确写成不这样做。

`rt_tick()` 代码由 RT 类线程的时钟滴答处理程序调用，用于判断线程的时间片是否已到期。如果已到期，则强制线程交出处理器；否则继续运行。RT 类线程会递减 `rtproc` 结构中的一个时间计数器 `rt_timeleft`，以跟踪处理器时间滴答（与 TS 线程的情况相同）。`rt_timeleft` 为零表示时间片已经用完。可以为 RT 类线程设置无限时间片。

RT 分派表中 `rt_quantum` 的值为 −2 时，内核将其解释为无限时间片。在这种情况下，RT 类线程会持续运行，除非它因睡眠（例如发出阻塞系统调用）而主动交出处理器。

RT 代码不会在每次需要测试时都通过索引 RT 分派表来获取 `rt_quantum` 数据。一旦 RT 线程建立，RT 表中的 RT 时间片就会被存储到线程 `rtproc` 结构中的 `rt_quantum` 中。后续测试使用 `rt_quantum` 进行；如果对线程使用 `priocntl()` 为其指定新的优先级和时间片，`rt_quantum` 将会获得新值。一旦 RT 线程初始化并开始执行，除非使用 `priocntl()` 显式修改，否则优先级永远不会改变。

### 9.2.3 调度器函数

调度器的主要功能是决定下一个执行哪个可运行线程，管理线程在处理器上的上下文切换，以及提供一种机制，将变为可运行状态的内核线程插入到分派队列中。调度器子系统内还定义了用于初始化过程（加载调度类、设置分派队列等）的支持代码，以及对 `dispadmin(1M)` 和 `priocntl(1)` 命令的支持。

调度器的核心是 `disp()` 函数，它选择下一个要执行的线程。`disp()` 主要从上下文切换函数 `swtch()` 调用，而 `swtch()` 是进入调度器的主要入口点，并且被内核中的许多地方调用。队列插入由 `setfrontdq()` 和 `setbackdq()` 代码处理，它们根据线程的优先级将内核线程放到分派队列上。内核线程是被放到队列的前端还是后端，是在调用队列插入函数之前确定的；我们将在后续函数描述中了解这个决定是如何做出的。

### 9.2.3.1 调度器队列插入
