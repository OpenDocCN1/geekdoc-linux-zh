
图 16.25 Tasklet 锁宏

这些是针对 SMP 情况的。

`test_and_set_bit()`函数用于设置指定`tasklet_struct`状态字段中的`TASKLET_STATE_RUN`位，该函数在第 5.1.4.1 节描述过。如果该位之前已设置，则返回 FALSE（我们未获取锁）。如果该位之前是清除的，则返回 TRUE（我们获取了锁）。因此，如果该位之前已设置（tasklet 正在运行），`tasklet_trylock()`函数返回 TRUE；否则返回 FALSE。在某些情况下，该位是由此函数设置。

此宏是`barrier()`指令的别名，它保证所有 CPU 都有内存的一致视图。

这清除了指定`tasklet_struct`状态字段中的`TASKLET_STATE_RUN`位（见第 5.1.2 节的`clear_bit()`函数）。

此函数等待直到该位被清除。

关于`test_bit()`函数，请参见第 5.1.3 节。

150–152 这是单处理器情况。状态字段中的任何位都没有进行实际的设置或测试，因为同一时间只能有一个 tasklet 在运行。

150 此宏始终求值为 TRUE，因为任何时间只能有一个 tasklet，当它想要锁时就能拥有。

151 它不等待，因为没有可以等待的。

152 它不执行任何操作，因为没有锁。

## 16.3 下半部 (Bottom halves)

下半部是 Linux 中软件中断的最早实现。当中断处理程序结束时，只要没有其他挂起的硬件中断，内核就会扫描下半部表。中的每个条目都可以标记为激活或非激活。如果是激活状态，则执行一次并标记为非激活。

### 16.3.1 数据结构

Linux 2.4 版本支持所有的下半部。本节将检查当前下半部实现的基础数据结构。

#### 16.3.1.1 下半部数组

下半部通过`bh_base[]`进行跟踪，它包含指向下半部处理程序的指针；见来自`kernel/softirq.c`的图 16.26。

```c
static void (*bh_base[32])(void);
```

```c
spinlock_t global_bh_lock = SPIN_LOCK_UNLOCKED;
```

> 图 16.26 下半部数据结构

232 数组从不初始化，但插入和删除通过`init_bh()`和`remove_bh()`完成（见第 16.3.1.3 节）。

287 通过在运行下半部时取出`global_bh_lock`自旋锁来保证互斥。

#### 16.3.1.2 预下半部

前 15 个左右的下半部分配了固定的数字。来自`<linux/interrupt.h>`的枚举决定了“谁”进入`bh_base[]`。最经常发生的事情排在前面的似乎是合理的。我们会再次遇到的只有`TIMER_BH`(0)、`TQUEUE_BH`(1)和`IMMEDIATE_BH`(9)。

```c
enum {
  TIMER_BH = 0,
  TQUEUE_BH,
  DIGI_BH,
  SERIAL_BH,
  RISCOM8_BH,
  SPECIALIX_BH,
  AURORA_BH,
  ESP_BH,
  SCSI_BH,
  IMMEDIATE_BH,
  CYCLADES_BH,
  CM206_BH,
  JS_BH,
  MACSERIAL_BH,
  ISICOM_BH
};
```

图 16.27 某些预下半部

#### 16.3.1.3 插入和删除下半部

下半部处理程序通过将处理程序指针插入`bh_base[]`数组的相应元素来安装。图 16.28 显示的两个函数来自`kernel/softirq.c`。

```c
void init_bh(int nr, void (*routine)(void))
  bh_base[nr] = routine;
  mb();
}
void remove_bh(int nr)
  tasklet_kill(bh_task_vec[nr]);
  bh_base[nr] = NULL;
}
```

图 16.28 插入和删除下半部

- 312–316 此函数设置下半部处理程序。它仅将提供的指针插入`bh_base[]`数组的指定元素中。`mb()`要求在返回之前更新已写入内存。
- 318–322 此函数从数组中移除下半部。
- 320 下节将解释下半部实际上使用 tasklet 机制执行的。因此，首先我们检查对应的 tasklet 是否正在运行或已调度运行（见第 16.5 节的`tasklet_kill()`函数）。
- 321 然后在`bh_base[]`数组的相应元素中放入 NULL。

### 16.3.2 执行下半部

预计下半部最终消失并被 tasklet 取替。即使在 Linux 2.4 中，下半部仍通过自己的数组注册，正如我们所看到的，它们使用 tasklet 机制执行。这是通过建立 tasklet 和下半部之间的一一对应关系来实现。正如第 16.2.1 节所示，tasklet 数组`bh_task_vec[]`的默认初始化是每个元素指向同一个函数`bh_action()`，来自`kernel/softirq.c`的图 16.29。此函数在`bh_base[]`数组的正确位置运行下半部处理程序。

```c
static void bh_action(unsigned long nr)
{
    int cpu = smp_processor_id();

    if (!spin_trylock(&bh_lock))
        goto resched;

    if (!hardirq_trylock(cpu))
        goto resched_unlock;

    if (bh_base[nr])
        bh_base[nr]();

    hardirq_unlock(cpu);
    spin_unlock(&global_bh_lock);
    return;

resched_unlock:
    spin_unlock(&global_bh_lock);
resched:
    mark_bh(nr);
}
```

图 16.29 默认 tasklet 处理程序

- 289 参数`nr`是要运行的下半部编号。
- 291 找到我们正在运行的 CPU ID（见第 7.2.1.4 节）。如果获取锁返回 TRUE，否则返回 FALSE。它不等待。如果全局下半部（定义在 16.3.1.1）闲，意味着另一个下半部正在运行，因此我们跳转到第 308 行，仅标记该下半部在稍后处理。
- `hardirq_trylock()`在第 16.5.3.1 节（单处理器情况）中定义为宏，在第 16.5.3.2 节（多处理器情况）中定义为函数。如果没有硬件中断处理程序运行，它求值为 TRUE，否则为 FALSE。它不等待。如果我们获取了全局下半部锁，但 hardirq 不闲，我们跳转到第 306 行。这释放全局下半部锁，标记该下半部稍后处理并返回。
- 如果`bh_base[]`数组中对应提供的数字的有效指针，则调用该函数；否则什么都不做。
- 在每种，我们都释放两个锁并返回。`hardirq_unlock()`宏在第 16.5.3.1 节。`spin_unlock()`宏来自第 5.3.1 节。
- 此函数调度下半部执行。在第 16.3.3 节中处理。

### 16.3.3 标记下半部执行

图 16.30 来自`<interrupt.h>`显示了尽快标记下半部执行的函数。等效地，它将旧的`mark_bh()`转换为带有转换参数的`tasklet_hi_schedule()`调用。它调度该下半部对应的 tasklet 在当前 CPU 的高优先级 tasklet 队列上执行（第 16.2.4.1 节）。

```c
static inline void mark_bh(int nr)
{
    tasklet_hi_schedule(bh_task_vec+nr);
}
```
