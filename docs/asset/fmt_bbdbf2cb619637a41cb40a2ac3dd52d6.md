
Cyg 包含两个条件变量的配置选项。这些选项位于 Cos Kernel 程序包中的同步优先级（Synchronization Priorities）中。第一个配置选项是条件变量定时等待（`CYGMFN_KERNEL_SYNCH_CONVDAR_TIMED_WAIT`），它允许应用程序使用 `cyg_cond_timed_wait` 内核 API 函数。该选项默认启用。

第二个配置选项是条件变量显式互斥锁等待支持（`CYGMFN_KERNEL_SYNCH_CONVAR_WAIT_MUTEX`），它允许线程在调用等待函数时提供不同的互斥锁。默认情况下，条件变量是用静态关联的互斥锁创建的。该选项默认启用。

## 项目列表 6.6 条件变量 API 函数

语法：

```
cyg_cond_init {
    cyg_cond_t *cond,
    cyg_mutex_t *mutex
}
```

上下文：

初始化/线程

参数：

`cond`—指向条件变量对象的指针。

描述：初始化条件变量并将其附加到指定的互斥锁上。

语法：

```
cyg_cond_destroy {
    cyg_cond_t *cond
}
```

上下文：

初始化/线程

参数：

`cond`—指向条件变量对象的指针。

描述：销毁一个条件变量。重要的是，不要对未使用的条件变量调用此函数。

语法：

```
cyg_bool_t
cyg_cond_wait {
    cyg_cond_t *cond
}
```

上下文：

线程

参数：

`cond`—指向条件变量对象的指针。

描述：导致线程等待指定的条件变量，并同时解锁附加到条件变量的互斥锁。成功返回 `TRUE`，如果线程被强制唤醒则返回 `FALSE`。这必须在线程持有附加到条件变量的互斥锁时进行。条件信号或广播会唤醒调用此等待函数的线程。当线程唤醒时，互斥锁由该程序获取。由于线程必须等待互斥锁，因此应在循环内调用此等待函数，因为等待期间条件可能会变为 `FALSE`。

语法：

```
cyg_bool_t
cyg_cond_timed_wait {
    cyg_cond_t *cond,
    cyg_tick_count_t abstime
}
```

上下文：

线程

参数：

`cond`—指向条件变量对象的指针。

`abstime`—等待条件变量的绝对时间。

描述：导致线程按绝对时间段等待指定的条件变量。此函数仅在启用“条件变量定时等待支持”选项时可用。如果接收到条件变量信号或广播，此函数返回 `TRUE`。如果在条件变量信号 `FALSE` 之前发生超时，则返回 `FALSE`。参数 `abstime` 是以 ticks 计算的绝对时间。以下显示了如何使用相对等待时间：

```
cyg_cond_timed_wait(
    &cond,
    cyg_current_time() + 100);
```

在此示例中，线程将从当前时间起等待条件变量 100 ticks。

语法：

```
cyg_cond_signal(
    cyg_cond_t *cond
);
```

上下文：

参数：

`cond`—指向条件变量对象的指针。

描述：唤醒每个等待条件变量的线程，使该线程成为互斥锁的所有者。需要理解的是，如果有多个线程在等待条件变量，可能会出现竞态。这就是为什么等待线程……非常重要。

## 6.2.4 标志（Flags）

标志是用 32 位字表示的同步机制。标志中的每个位都代表一个条件，允许线程等待单个条件或多个条件的组合。等待的线程可以指定在唤醒前是满足所有条件还是满足组合条件。信号线程可以根据特定条件设置或重置置位，以便执行适当的线程。用于创建和控制标志的内核 API 函数详见条目列表 6.7。

- 条目列表 6.7 内核标志 API 函数

```
Syntax:
void
cyg_flag_init(
cyg_flag_t *flag
);
Context:
/Thread
Parameters:
--指向标志对象的指针。
Description:
初始化标志变量。
```

```
Syntax:
void
cyg_flag_destroy(
cyg_flag_t *flag
);
Context:
/Thread
Parameters:
--指向标志对象的指针。
Description:
销毁指定的标志变量。正在被等待的标志变量不能被销毁。
```

```
Syntax:
void
cyg_flag_setbits(
cyg_flag_t *flag,
cyg_flag_value_t value
);
Context:
Thread/DSR
Parameters:
--指向标志对象的指针。
value--此参数中被设置为 1 的位将与标志中的当前位一起被设置。
Description:
设置标志值中在 value 参数中被设置为 1 的位。所有等待该标志且条件满足的线程都将被唤醒。
```

```
Syntax:
void
cyg_flag_maskbits(
cyg_flag_t *flag,
cyg_flag_value_t value
);
Context:
Thread/DSR
Parameters: flag--指向标志对象的指针。
value--此参数中被设置为 0 的位将在标志中清除。

Description: 清除标志值中在 value 参数中被设置为 0 的位。此调用不会唤醒任何线程。
```

```
cyg_flag_value_t
cyg_flag_wait(
cyg_flag_t *flag,
cyg_flag_value_t pattern,
cyg_flag_mode_t mode
);
Thread
```

Parameters: `flag`--指向标志对象的指针。

`mode`--指定导致调用线程被唤醒的条件。

Description: 如果 `mode` 参数设置为 `AND`（与），该函数将等待 `pattern` 参数中的所有位在标志值中被设置。如果 `mode` 参数设置为 `OR`（或），该函数将等待 `pattern` 参数中的任何位被设置。当此条件满足时，调用返回标志值。如果线程被强制唤醒或通过 `cyg_thread_exit` 强制退出，则返回 0。`mode` 参数可以有以下可能值：

- `CY_FLAG_WAITMODE_AND`--掩码中的所有位都在标志中被设置。
- `CY_FLAG_WAITMODE_OR`--如果掩码中的任何位在标志中被设置，则唤醒。
- `CY_FLAG_WAITMODE_CLR`--当条件满足时清除标志中的所有位。通常，只有 `pattern` 中设置的位会被清除。此标志与 `AND` 或 `OR` 模式标志进行位运算组合。

```
cyg_flag_value_t
cyg_flag_timed_wait(
cyg_flag_t *flag,
cyg_flag_value_t pattern,
cyg_flag_mode_t mode,
cyg_tick_count_t abstime
);Thread
```

Parameters: `flag`--指向标志对象的指针。
`pattern`--导致调用线程被唤醒的设置位。
`mode`--修改唤醒的条件。

Description: 等待 `pattern` 和 `mode` 参数要求的条件，或 `abstime` 参数指定的超时时间。如果在条件满足之前发生超时，则返回 0；否则，返回标志值。此函数仅在启用了 `Allow-Per-Timers` 配置选项时可用。

```
cyg_flag_value_t
cyg_flag_poll(
cyg_flag_t *flag,
cyg_flag_value_t pattern,
cyg_flag_mode_t mode
);
```

Context:
Thread/DSR
`flag`--指向标志对象的指针。
`pattern`--导致线程被唤醒的位设置。
`mode`--修改返回标志值的条件。

如果满足 `pattern` 和 `mode` 参数要求的条件，则返回标志值。如果条件不满足，则返回 0；否则，返回标志值。在 `mode` 参数中指定 `CYG_FLAG_WAITMODE_CLR` 将标志值清零为 0。

```
cyg_flag_value_t
cyg_flag_peek(
cyg_flag_t *flag
);
```

Context:
Thread/DSR
`flag`--指向标志对象的指针。
返回指定标志的当前值。

```
cyg_bool_t
cyg_flag_waiting(
cyg_flag_t *flag
);
```
