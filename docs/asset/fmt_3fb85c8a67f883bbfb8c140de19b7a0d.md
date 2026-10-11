
| task: `softirq-timer/0-3` (`uid:0 nice:0 policy:1 rt_prio:1`)

-----------------------------------------------------------------

         --> `CPU#`

          |____--> `irqs-off`

          |        |____--> `need-resched`

          |        |       | `hardirq/softirq`

          |        |       |  |____--> `preempt-depth`

          |        |       |  |      |

          |        |       |  |    `delay`

`cmd`       `pid`        `time`     | `caller`

                                |

`cat-6637`  `0D..`   `00us` : `common_interrupt` (`01`)

`cat-6637`  `0D.h.`   `2us` : `do_IRQ` (`c013491c 0 0`)

`cat-6637`  `0D.hi`   `3us+` : `mask_and_ack_8259A` (`_do_IRQ`)

`cat-6637`  `0D.h.`   `10us` : `redirect_hardirq` (`_do_IRQ`)

`cat-6637`  `0D.h.`   `12us` : `handle_IRQ_event` (`_do_IRQ`)

`cat-6637`  `0D.h.`   `13us` : `timer_interrupt` (`handle_IRQ_event`)

`cat-6637`  `0D.h.`   `15us` : `handle_tick_update` (`timer_interrupt`)

`cat-6637`  `0D.h`    `16us` : `do_timer` (`handle_tick_update`)

...      `<we're in the timer interrupt function>`

`cat-6637`  `0D.h.`    `22us` : `run_local_timers` (`update_process_times`)

`cat-6637`  `0D.h.`    `22us` : `raise_softirq` (`run_local_timers`)

`cat-6637`  `0D.h`     `23us` : `wakeup_softirqd` (`raise_softirq`)

...      `<softirq work pending - need to preempt if signaled>`

`cat-6637`  `0Dmh.`    `34us` : `wake_up_process` (`wakeup_softirqd`)

`cat-6637`  `0Dmh.`    `35us` : `rcu_pending` (`update_process_times`)

`cat-6637`  `0Dmh`     `39us` : `scheduler_tick` (`update_process_times`)

`cat-6637`  `0Dmh`     `39us` : `sched_clock` (`scheduler_tick`)

`cat-6637`  `0Dmh`     `41us` : `task_timeslice` (`scheduler_tick`)

`cat-6637`  `0Dmh`     `42us+` : `preempt_schedule` (`scheduler_tick`)

`cat-6637`  `0Dmh`     `45us` : `note_interrupt` (`_do_IRQ`)

`cat-6637`  `0Dmh`     `45us` : `enable_8259A_irq` (`_do_IRQ`)

`cat-6637`  `0Dmh`     `47us` : `preempt_schedule` (`enable_8259A_irq`)

`cat-6637`  `0Dmh`     `48us` : `preempt_schedule` (`_do_IRQ`)

`cat-6637`  `0Dmh`     `48us` : `irq_exit` (`_do_IRQ`)

`cat-6637`  `0Dm.`     `49us` : `preempt_schedule_irq` (`need_resched`)

`cat-6637`  `0Dm.`     `50us` : `_schedule` (`preempt_schedule_irq`)

...      `<here is the context_switch to softirq-timer thread>`

`<...>3`       `0D..2`  `74us+` : `__switch_to` (`_schedule`)

`<...>3`       `0D..3`  `76us` : `__switch_to` (`cat-6637`) (`74 62`)

`<...>3`       `0D..2`  `77us` : `_schedule` (`schedule`)

`<...>3`       `0D..2`  `78us` : `trace_irqs_on` (`_schedule`)

...      `<output truncated here for brevity>`

为了清晰起见，我们大幅精简了此清单，但此跟踪的关键要素显而易见。此跟踪源自定时器中断。在硬中断线程中，除了为稍后的软中断上下文排队一些工作外，几乎什么都没做。这在 23 微秒处的 `wakeup_softirqd()` 函数中可以看到，这是中断处理的典型情况。这会触发 `need_resched` 标志，如跟踪中第二个字段第三列的 `n` 所示。在 49 微秒时，经过定时器软中断的一些处理后，调度器被调用于抢占。在 74 微秒时，控制权传递给实际运行在此特定内核中的 PID 为 3 的 `softirqd-timer/0` 线程。（进程名称被截断以适合字段宽度，显示为 `<...>`。）

清单 17-7 中的大多数字段含义显而易见。`irqsoff` 字段在中断关闭的代码段中包含一个 `D`。由于此延迟跟踪是中断关闭跟踪，我们看到整个跟踪中都有此指示。`need_resched` 字段反映内核 `need_resched` 标志的状态。`n` 表示应在最早的机会运行调度器，而句点 (`.`) 表示此标志未激活。`hardirq/softirq` 字段指示在硬中断上下文中执行的线程用 `h` 表示，在软中断上下文中执行的线程用 `s` 表示。`preempt-depth` 字段指示内核 `preempt_count` 变量的值，这是内核内锁嵌套层级的指示器。只有当此变量为零时，才可以发生抢占。

### 17.4.8 调试死锁状况

`DEBUG_DEADLOCKS` 内核配置选项启用检测并报告与内核中信号量和自旋锁相关的死锁状况。启用后，潜在的死锁状况将以类似于以下的方式报告：

```text
BUG: lock recursion deadlock detected!
.
.
.
```
