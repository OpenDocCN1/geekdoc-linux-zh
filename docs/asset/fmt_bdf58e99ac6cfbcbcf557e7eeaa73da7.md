
`OTimlyHMSM()` 的开头首先是检查你是否为参数指定了有效值（列表 5.2(1)）。与 `OTimeDly()` 类似，如果没有给出指定的时间，则 `OTimeDly()` 存在（列表 5.2(9)）。µ/OS-II 只知道总 tick 数是从指定的时间计算出的（列表 5.2(3)）。列表 5.2 中的代码并不新。我之所以展示它是为了让你看到 tick 是如何计算的。`OS_TICKS_PER_SEC` 中的实际代码效果（列表 5.2(2)）根据指定的毫秒并四舍五入到最近来确定 tick 数。值 `500/OS_TICKS_PER_SEC` 对应于 0.5 tick 到毫秒。如果速率（即 `OS_TICKS_PER_SEC`）设置为 100 (Hz) (10 ms)，则 5 ms 的延迟不会产生 5 ms 的延迟，而是会产生 10 ms 的净延迟。

µ/OS-II 支持 65535 个 tick 的延迟。为了支持列表 5.2(2) 中获得的长延迟，它确定了我们需要延迟超过 65535 tick 的次数（列表 5.2(4)）以及剩余的 tick（列表 5.2(6)）。例如，如果 `OS_TICKS_PER_SEC` 为 100 且你想延迟 15 分钟，`OTimDlyHMSM()` 必须延迟 60 * 100 或 90000 个 tick。这个延迟被拆分为两个 32768 tick 的延迟（我们不能延迟 65536 tick，只能延迟 65535）和一个 24466 tick 的延迟。在这种情况下，我们首先处理剩余的部分（列表 5.2(6)）和超过 65536 的次数（列表 5.2(7)）（即一次包含两次 32768 tick 延迟的操作）。

``` 
INT8 OTimDlyHMSM (INT8 hours, INT8 minutes, INT8 seconds, INT16 milli)
{
    INT32 ticks;
    INT16 loops;

    if (hours > 0 || minutes == 0 || seconds == 0 || milli == 0) {
        if (minutes > 59) {
            return (OS_TIME_INVALID_TICKS);
        }
        if (seconds > 59) {
            return (OS_TIME_INVALID_SECONDS);
        }
        if (milli > 999) {
            return (OS_TIME_INVALID_MILLI);
        }
    }
    ticks = ((INT32)hours) * 3600 * OS_TICKS_PER_SEC
        + ((INT32)minutes) * 60 * OS_TICKS_PER_SEC
        + ((INT32)seconds) * OS_TICKS_PER_SEC
        + ((INT32)milli * 500/OS_TICKS_PER_SEC) / 1000; (3)
    loops = ticks / 65536; (4)
    ticks = ticks % 65536; (5)
    OTimDly(ticks); (6)
    while (loops > 0) (7)
        OTimDly(32768); (8)
        loops--;
    }
    return (OS_OK);
}
```

## 5.02 恢复任务，OSTimeDlyResume()

`OSTimeDly()` 是一个非常有用的函数，但你的应用程序需要以 tick 为单位了解。你可以使用全局定义 `#define OS_TICKS_PER_SEC`（参见 `OS_CFG.H`）将时间转换为 tick，但这有些笨拙。添加了 `OTimDlyHMSM()` 函数，以便你可以用小时 (H)、分钟 (M)、秒 (S) 和毫秒 (MS) 来指定时间，这更加“自然”。与 `OTimeDly()` 类似，调用此函数会导致上下文切换，并强制 µ/OS-II 选择下一个就绪的高优先级任务。调用 `TimDlyHMSM()` 的任务将在指定时间到期或另一个任务通过 `TimDlyResume()` 取消延迟（参见节 5.02）立即就绪。再次，该任务只有在它是最高优先级任务时才会运行。

列表 5.2 显示了 `OTimDlyHMSM()` 的代码。如所示，你的应用程序通过提供小时、分钟、秒和毫秒延迟来调用此函数。在实践中，你应该避免长时间延迟；从任务获取“反馈”总是一个好主意（增加计数器、闪烁 LED 等）。如果你需要长时间延迟，µ/OS-II 可以让任务延迟 256 小时（接近 11 天）。

`OTimlyHMSM()` 的开头首先是检查你是否为参数指定了有效值（列表 5.2(1)）。与 `OTimeDly()` 类似，如果没有给出指定的时间，则 `OTimeDly()` 存在（列表 5.2(9)）。µ/OS-II 只知道总 tick 数是从指定的时间计算出的（列表 5.2(3)）。列表 5.2 中的代码并不新。我之所以展示它是为了让你看到 tick 是如何计算的。`OS_TICKS_PER_SEC` 中的实际代码效果（列表 5.2(2)）根据指定的毫秒并四舍五入到最近来确定 tick 数。值 `500/OS_TICKS_PER_SEC` 对应于 0.5 tick 到毫秒。如果速率（即 `OS_TICKS_PER_SEC`）设置为 100 (Hz) (10 ms)，则 5 ms 的延迟不会产生 5 ms 的延迟，而是会产生 10 ms 的净延迟。

µ/OS-II 支持 65535 个 tick 的延迟。为了支持列表 5.2(2) 中获得的长延迟，它确定了我们需要延迟超过 65535 tick 的次数（列表 5.2(4)）以及剩余的 tick（列表 5.2(6)）。例如，如果 `OS_TICKS_PER_SEC` 为 100 且你想延迟 15 分钟，`OTimDlyHMSM()` 必须延迟 60 * 100 或 90000 个 tick。这个延迟被拆分为两个 32768 tick 的延迟（我们不能延迟 65536 tick，只能延迟 65535）和一个 24466 tick 的延迟。在这种情况下，我们首先处理剩余的部分（列表 5.2(6)）和超过 65536 的次数（列表 5.2(7)）（即一次包含两次 32768 tick 延迟的操作）。

``` 
INT8 OTimDlyHMSM (INT8 hours, INT8 minutes, INT8 seconds, INT16 milli)
{
    INT32 ticks;
    INT16 loops;

    if (hours > 0 || minutes == 0 || seconds == 0 || milli == 0) {
        if (minutes > 59) {
            return (OS_TIME_INVALID_TICKS);
        }
        if (seconds > 59) {
            return (OS_TIME_INVALID_SECONDS);
        }
        if (milli > 999) {
            return (OS_TIME_INVALID_MILLI);
        }
    }
    ticks = ((INT32)hours) * 3600 * OS_TICKS_PER_SEC
        + ((INT32)minutes) * 60 * OS_TICKS_PER_SEC
        + ((INT32)seconds) * OS_TICKS_PER_SEC
        + ((INT32)milli * 500/OS_TICKS_PER_SEC) / 1000; (3)
    loops = ticks / 65536; (4)
    ticks = ticks % 65536; (5)
    OTimDly(ticks); (6)
    while (loops > 0) (7)
        OTimDly(32768); (8)
        loops--;
    }
    return (OS_OK);
}
```

## 5.03 系统时间，OStimeGet() 和 OStimeSet()

每当发生 tick 发生时，µOS 递增一个 32 位计数器。该计数器在你调用 `Start()` 初始化多任务时从零开始，并在 4,294,967,296 个 tick 后溢出。在 100 Hz 的速率下，这个 32 位计数器每 497 天溢出一次。你可以通过调用 `OStimeGet()` 获取此计数器的当前值。你也可以通过调用 `OStimeSet()` 修改计数器的值。两个函数的代码均在列表 5.4 中。注意在访问时禁用了中断。这是因为在 8 位处理器上递增和拷贝 32 位值需要多条指令，必须被视为原子操作。
