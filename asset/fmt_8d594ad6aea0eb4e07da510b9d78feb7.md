
第 46–50 行
`preempt_enable()` 调用 `preempt_enable_no_resched()`，该函数将当前任务的 `preempt_count` 减 1，然后调用 `preempt_check_resched()`：

```c
include/linux/preempt.h

40 #define preempt_check_resched() \
41 do \
42     if (unlikely(test_thread_flag(TIF_NEED_RESCHED))) \
43         preempt_schedule(); \
44 ) while (0)
```

第 40–44 行
`preempt_check_resched()` 检查当前任务是否标记为需要调度；如果是，它会调用 `preempt_schedule()`。

```c
kernel/sched.c

2328 asmlinkage void __sched_preempt_schedule(void)
2329 (
2330   struct thread_info *ti = current_thread_info();
/*
 * 如果 preempt_count 不为 0 或中断被禁用，
 * 我们不希望抢占当前任务。直接返回。
 *
  if (unlikely(ti->preempt_count || irqs_disabled()))
    return;

  need_resched:
    ti->preempt_count = PREEMPT_ACTIVE;
    schedule();
    ti->preempt_count = 0;

  /* 我们可能在 schedule 和现在之间错过一次抢占机会 */
    barrier();
    if (unlikely(test_thread_flag(TIF_NEED_RESCHED)))
    goto need_resched;
```

第 2336–2347 行

如果当前任务仍然具有正数的 `preempt_count`（可能是由于嵌套了 `preempt_disable()` 命令），或者当前任务禁用了中断，则将处理器控制权返回给当前任务。

第 2340–2347 行

当前任务没有锁，因为 `preempt_count` 为 0 且中断已启用。因此，我们将当前任务的 `preempt_count` 标记为正在进行抢占，并调用 `schedule()`，它会选择另一个任务。

如果从代码块出来的任务需要重新调度，内核需要确保从当前任务让处理器是安全的。内核检查任务的 `preempt_count` 值。如果 `preempt_count` 为 0（即当前任务未持有锁），则调用 `schedule()` 并选择一个新任务执行。如果 `preempt_count` 不为 0，则将控制交给另一个任务是不安全的，控制权将返回给当前任务，直到它释放所有锁。当当前任务释放锁时，会检查该任务是否需要重新调度。

## 7.3 自旋锁和信号量

当当前任务释放最后一个锁且 `preempt_count` 变为 0 时，会发生调度。

当两个或多个进程需要对共享资源进行专用访问时，它们可能需要强制执行条件，即它们是操作特定代码段的唯一进程。Linux 内核中锁的基本形式是自旋锁（spinlock）。

自旋锁之所以取这个名字，是因为它们会不断循环（或自旋）等待获取锁。由于自旋锁以这种方式运行，因此不能让任何代码段中的自旋锁尝试两次获取锁，这会导致死锁。

在操作自旋锁之前，必须初始化 `spin_lock_t` 结构。这是通过调用 `spin_lock_init()` 实现的：

```c
include/linux/spinlock.h

63 #define spin_lock_init(x) \
64 do { \
65 (x)->magic = SPINLOCK_MAGIC; \
66 (x)->lock = 0; \
67 (x)->babble = 5; \
68 (x)->module = _FILE_; \
69 (x)->owner = NULL; \
70 (x)->lock = 0; \
71 } while (0)
```

这段代码在第 70 行将锁设置为“未锁定”，并初始化其他变量。

自旋锁初始化后，可以通过调用 `spin_lock()` 和 `spin_lock_unlock()` 来获取。

要释放自旋锁，进程应该调用 `spin_lock_unlock()`。这确保了锁被释放。

# 第 7 章 • 调度与内核同步

时钟是施加处理器的一个周期性信号，使其能够在时间域内运行。处理器依赖于时钟信号来判断何时可以执行下一个功能，例如将两个整数相加或从内存中提取数据。这种时钟信号的速度（1.4GHz、2GHz 等）在历史上一直被用来比较本地电子产品商店里不同系统的处理速度。

在任何给定时刻，你的系统都有几个时钟/定时器在运行。简单的例子包括屏幕右下角显示的日期（也称为时间）、杂乱桌面上闪烁的光标，或者由于长时间处于空闲状态而接管屏幕的笔记本电脑屏保护程序。更复杂的计时示例包括音频和视频播放、按键重复（长按不放）、通信运行速度，以及如之前讨论过的，任务可以运行多久。

## 7.4.1 实时时钟：现在几点？

Linux 挂钟（wall clock）的接口是通过 `/dev/rtc` 设备驱动的 `ioctl()` 函数实现的。该设备被称为实时时钟（RTC）。RTC 提供了一个带有小型 114 字节用户非易失性随机访问存储器（NVRAM）的计时功能。该设备的输入是一个 32.768KHz 振荡器和一个备份电池接口。某些特定的 RTC 型号内置了振荡器和电池，而其他 RTC 现在被内置在处理器芯片组的外设总控制器（例如南桥）中。RTC 不仅报告当天，还是一个能够中断系统的可编程定时器。中断频率从 2Hz 到 8,192Hz 不等。RTC 还可以像闹钟一样每天中断一次。在这里，我们探索 RTC 的代码：

```c
/include/linux/rtc.h
/* 如果启用了任何 RTC 驱动程序，则允许对 /dev/rtc 接口进行 ioctl 调度。 */
70 #define RTC_AIR_ON  _IO('p', 0x01) /* 闹钟中断，开启 */
71 #define RTC_AIR_OFF  _IO('p', 0x02) /* ... 关闭 */
72 #define RTC_UTC_ON  _IO('p', 0x03) /* 更新中断，开启 */
73 #define RTC_UTC_OFF _IO('p', 0x04) /* ... 关闭 */
74 #define RTC_PIE_ON  _IO('p', 0x05) /* 周期性中断，开启 */
```

> 由多个供应商制造，最著名的是摩托罗拉（Motorola）的 mc146818。（此 RTC 已不再生产。现在使用 Dallas DS12885 或同等设备。）

## 7.4 系统时钟：关于时间与定时器

```c
75 #define RTC_PIE_OFF      _IO('p', 0x06) /* ... 关闭 */
76 #define RTC_WIE_ON       _IO('p', 0x0f) /* 看门狗中断，开启 */
77 #define RTC_WIE_OFF      _IO('p', 0x10) /* ... 关闭 */
78 #define RTC_ALM_SET      _IOR('p', 0x07, struct rtc_time) /* 设置闹钟时间 *
79 #define RTC_RD_TIME      _IOR('p', 0x08, struct rtc_time) /* 读取闹钟时间*
80 #define RTC_RD_TIME      _IOR('p', 0x09, struct rtc_time) /* 读取 RTC 时间 *
81 #define RTC_SET_TIME     _IOR('p', 0x0a, struct rtc_time) /* 设置 RTC 时间 *
82 #define RTC_IRQ_READ     _IOR('p', 0x0b, unsigned long) /* 读取 IRQ 速率 *
83 #define RTC_IRQ_SET      _IOR('p', 0x0c, unsigned long) /* 设置 IRQ 速率 */
84 #define RTC_EPOCH_READ   _IOR('p', 0x0d, unsigned long) /* 读取 epoch */
85 #define RTC_EPOCH_SET    _IOR('p', 0x0e, unsigned long) /* 设置 epoch */
```
