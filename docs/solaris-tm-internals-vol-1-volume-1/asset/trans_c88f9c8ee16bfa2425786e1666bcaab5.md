
如果线程没有请求内核优先级，`ts_sleep()` 代码会将 `ts_dispwait` 值（线程在调度队列上等待的时间）与调度表中的 `ts_maxwait` 值进行比较，`ts_maxwait` 由 `ts_umdpri` 索引，该索引与上次设置全局优先级时用于获取全局优先级的行相同。代码大致如下。

```c
if (kthread->tsproc.ts_dispwait > ts_dptbl[ts_umdpri].ts_maxwait)
```

- 如前所述，优先级会被重新计算，但有一个显著区别。`ts_umdpri` 值从 TS/IA 调度表中的 `ts_slpret`（睡眠返回优先级）列获取，而不是像前一个示例那样从 `ts_tqexp` 列获取。`ts_slpret` 优先级赋予线程较高的优先级，因此它们会比调度队列上的大多数其他 TS/IA 线程更早获得调度。

- 如果线程没有请求内核优先级，并且线程等待时间没有超过 `ts_maxwait`（即刚刚描述的前两种场景），则进入 `ts_sleep()` 代码中的最后一种场景。

如果这两个条件不成立，并且线程已经处于 SYS 优先级，那么线程的优先级会被设回 TS/IA 类优先级，使用 `ts_umdpri` 作为 TS/IA 调度表的索引，并将 `t_pri` 设置为相应的全局优先级。

如果三个条件都不成立——这意味着线程不处于 SYS 优先级，不需要被赋予 SYS 优先级，并且没有等待过长的时间——那么 `ts_sleep()` 代码实际上什么也不做，只是返回到调用者，而不改变线程的任何调度器属性。该线程将在唤醒代码中再次获得调整优先级的机会。

- 唤醒函数将线程放入调度队列，并且仅当前面描述的线程等待测试为真时才调整线程优先级；也就是说，线程的 `ts_dispwait` 值大于 `ts_maxwait`，再次使用 `ts_umdpri` 从调度表中获取 `ts_maxwait` 值。唤醒代码在调整线程优先级之后、调用调度器队列函数进行队列插入之前，还会将 `ts_dispwait` 值重置为 0。实际的优先级调整是通过使用 `ts_slpret` 调度表值来设置 `ts_cpupri` 完成的，这与 `ts_sleep()` 代码中对长时间等待线程的处理方式相同。

`ts_timeleft` 被设置为 `ts_quantum`，在完成用户优先级计算后，`t_pri` 被赋予一个调度优先级，`ts_umdpri` 值决定从调度表的哪一行获取全局优先级，如图 9.8 中的序列所示。

![](img/220ae4af07df2fe8e5be69d27f885d1b_425_0.png)

图 9.8 *使用* `ts_slpret` *进行优先级调整*

- 内核通过 callout 机制每秒运行一次 `ts_update()` 例程。`ts_update()` 遍历内核线程的链表，并更新 TS/IA 类线程的 `ts_dispwait` 值（RT 和 SYS 类线程不会被更新）。

  更新代码会轮流遍历 `tsproc` 结构的多个链表（参见第 371 页的图 9.4），从 `ts_listhead` 开始，一次遍历一个链表。如果线程更新后的 `ts_dispwait` 大于 `ts_maxwait`，则使用已描述的方法提升线程优先级，但会使用调度表中的不同列来重置 `ts_cpupri`。

  从调度表的索引行获取 `ts_lwait` 来设置新的 `ts_cpupri` 值，计算用户模式优先级，并将 `ts_dispwait` 重置为 0。

  `ts_update()` 函数调用 `ts_change_pri()`，后者会为更新过程做一些额外的工作。

- 如果线程当前正在处理器上运行（线程状态为 `ONPROC`），则会在 `t_pri` 中设置新的全局优先级：在 `ts_update()` 函数中推导出的新 `ts_umdpri` 值会从调度表中获取全局优先级。

- 如果线程的新优先级大于处理器调度队列上最高优先级线程的优先级（使用调度器结构 `disp_maxrunpri` 进行测试，该结构在每次将线程放入调度队列时都会更新），则该线程的 `ts_timeleft` 参数会从 `ts_quantum`（在调度表中）重置，并继续运行。

- 如果调度队列上有一个更高优先级的线程，则该线程被迫让出处理器。

- `ts_change_pri()` 中的另一种可能情况是线程没有在处理器上运行，此时会调用 `thread_change_pri()` 来设置新优先级。处于 SLEEP 状态（位于睡眠队列上）的线程将由同步对象特定函数来更改其优先级。

  例如，如果线程正在互斥锁上睡眠，则会调用 `mutex_change_pri()` 代码来更改优先级，并在必要时在线程睡眠队列上重新定位（更多内容请参见第 404 页的“内核睡眠/唤醒设施”）。否则，线程必定位于调度队列上。设置优先级，并调用一个调度器队列插入函数来设置线程在调度队列上的位置。

下面的伪代码展示了整个过程。

```text
ts_update()
        set list from ts_plisthead[] /* lists of tsproc structures */
        ts_update_list()
                while (not at the end of the current list)
                        if (thread is not in TS or IA class)
                                bail out
                        if (thread has preemption control turned on)
                                bail out
                        if (thread is not sitting on dispatch queue)
                                set thread flags for post trap processing
                                bail out
                        kthread->tsproc.ts_cpupri = ts_dtbl[ts_cpupri].ts_lwait
                        calculate new user mode priority (ts_umdpri)
                        kthread->tsproc.ts_dispwait = 0
                        if (the thread's priority will change based on new ts_umdpri)
                                ts_change_priority()
                end while loop

ts_change_priority()
        if (thread is running on a processor) /* state is ONPROC */
                kthread->t_pri = ts_dtbl[ts_umdpri].ts_glopri
                if (thread's priority > max runnable priority on dispatch queue)
                        kthread->tsproc.ts_timeleft = ts_dtbl[ts_umdpri].ts_quantum
                else
                        set flag for back of dispatch queue
                        surrender cpu
        else /* thread is not running */
                set front dispatch queue flag if IA class thread
                thread_change_pri()
                if (thread was on a run queue)
                        kthread->tsproc.ts_timeleft = ts_dtbl[ts_umdpri].ts_quantum
                else
                        set dispatch back queue flag

thread_change_pri()
        if (thread is not on a sleeper queue or run queue)
                set new priority and return
        if (thread is on a sleep queue)
                call synchronization object specific priority change code
        else
                take the thread off the dispatch queue
                set the new priority
                call a dispatcher queue insertion function /* put it back on a queue */
```

在考察了两个按固定间隔发生的 TS/IA 特定函数——`ts_tick()` 和 `ts_update()`，它们都由时钟中断处理程序驱动——之后，我们需要确保每个函数的预期用途之间的区别是清晰的。`ts_tick()` 旨在处理*正在*处理器上运行的线程。`ts_update()` 旨在处理*未在*处理器上运行、而是位于调度队列或睡眠队列上的线程。如果你在前面的讨论细节中迷失了方向，我们认为有必要把这个要点讲清楚。

正如我们之前指出的，IA 类线程在很大程度上由刚才描述的 TS 类函数处理。为 IA 类定义的类特定函数包括初始化 IA 类的代码、获取类特定信息的代码，以及用于发送和获取类参数的支持代码。`ia_init()` 代码非常少，因为 IA 类的大部分工作都在 TS 类代码中完成。`ia_init()` 设置其调度类、指向其类函数表的指针以及其最大全局优先级（与 TS 一样是 59）。用户模式优先级支持函数 `ia_parms()`、`ia_getparms()` 和 `ia_parmsget()` 在流程和功能上跟踪等价的 TS 支持代码。

进程由 IA 类特定例程 `ia_set_process_group()` 放入 IA 类，该例程在 TTY 被新的进程组接管时从 STREAMS ioctl()（`strioctl()`）调用——ioctl 是 I/O 控制调用，受所有字符设备驱动程序支持。它源于内核中基于 STREAMS 的终端驱动程序代码。如果你启动 Solaris 桌面系统但不启动窗口系统，那么不会有任何 IA 进程在运行（只有 TS 和 SYS 类 Solaris 守护进程）。当窗口系统启动时，它会接管“终端”的控制权，在桌面环境中，这个终端就是键盘、鼠标以及显卡到显示器的接口。

接管操作会生成 set-process-group ioctl 调用，该调用最终调用 `CL_SET_PROCESS_GROUP` 宏。由于调用者是交互式进程（窗口系统软件确保了这一点），这个宏会解析为 IA 类特定函数 `ia_set_process_group()`。与窗口系统关联的所有进程都被放入 IA 类。由于进程和线程都是从父进程继承调度类，因此新创建的进程（终端窗口、应用程序）也被放入 IA 类。IA 类线程会获得一个值为 10 的优先级提升量，该提升量在线程的用户模式优先级计算时被计入，也就是说，每次调整线程优先级时都会计入。回想一下，用户优先级是 `ts_cpupri`、`ts_upri` 和 `ts_boost` 之和。（对于 IA 类线程，`ts_boost` 的固定值为 10。）

处理 RT 类线程要简单得多：由于 RT 优先级是固定的，在线程执行生命周期内既不会变高也不会变低。RT 类线程优先级发生变化的唯一方式是，通过 `priocntl()` 命令或系统调用显式更改。当线程进入 RT 调度类（通过 `priocntl()` 调用 `rt_enterclass()`）时，除非指定了优先级，否则线程的 RT 类优先级（`rtproc` 结构中的 `rt_pri`）被设置为默认值 0；也就是说，`rt_pri` 将反映所请求的优先级（前提是它在类的有效范围内）。`rt_pquantum`（也在 `rtproc` 中）被设置为调度表中与优先级索引的对应行号相对应的 `rt_quantum` 值。例如，默认的 RT 类优先级

