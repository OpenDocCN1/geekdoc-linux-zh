
```c
void
cyg_counter_set_value(
cyg_handle_t counter, cyg_tick_count_t new_value
);
```

上下文：`Init/Thread/DSR`

参数：`counter`—指向计数器的句柄，`new_value`—要设置的计数器值（以滴答为单位）。

描述：将计数器设置为由 `new_value` 指定的滴值。

代码列表 7.1 显示了一个导致报警触发的计数器示例。在本章中，我们将取消报警器。

```c
#include <cyg/kernel/kapi.h>

cyg_counter counter_obj;
cyg_handle_t counter_hdl;

cyg_handle_t alarm_hdl;
cyg_alarm alarm_obj;

// 报警处理函数，以便可以
// 传递报警初始化函数。
cyg_alarm_t alarm_handler;

unsigned long index = 0;

// 计数器线程。
void counter_thread(cyg_addrword_t index )
{
    // 无限运行。
    while ( 1 )
    {
        // 延迟 10 个滴答。
        cyg_thread_delay( 10 );

        // 增加计数器。
        cyg_counter_tick( counter_hdl );
    }
}

// 应用的主入口。
void cyg_user_start( void )
{
    // 创建计数器。
    cyg_counter_create( &counter_hdl,
    counter_obj );

    // 创建报警。
    cyg_alarm_create( counter_hdl,
    alarm_handler,
    (cyg_addword_t)index,
    &alarm_obj );

    // 初始化报警。
    cyg_alarm_initialize( alarm_hdl,
    12,
    6 );

    // 创建运行计数器线程。
}

// 报警处理器。
void alarm_handler(
cyg_handle_t alarm_handle, cyg_addword_t data )
{
    (void)data;
}
```

# 代码列表 7.1 使用计数器和报警

在 7.1 中，创建一个计数器。接下来，使用之前创建的句柄创建报警。报警触发时传递处理器。现在初始化创建的报警。当 `counter_thread` 运行时，它延迟 10 个滴答，然后使用 `cyg_counter_tick` 函数增加计数器。当 `counter_hdl` 达到 12 时，会调用 `alarm_handler`。在这种情况下，`alarm_handler` 仅增加 `data`。

## 7.1.2 时钟

时钟带有关联分辨率的计数器，由代表时间周期的定期滴答源驱动。操作系统内核实现了一个默认系统时钟 `RTC`，用于跟踪时间。项目列表 7.5 列出了控制时钟的内核 API 函数。代码列表 7.2 显示了使用内核 API 函数的示例。

## 项目列表 7.5 内核时钟 API 函数

语法：
```c
cyg_clock_create(
cyg_resolution_t resolution,
cyg_handle_t *handle,
cyg_clock *clock
);
```

上下文：

`Init/Thread`

参数：

`resolution`--每滴答的纳秒分子和分母。

`handle`--指向新时钟句柄的指针。

`clock`--指向新时钟对象的指针。

描述：使用指定的分辨率构造一个新的时钟。

删除指定的时钟。

语法：
```c
cyg_clock_delete(
cyg_handle_t clock
);
```

上下文：

`Init/Thread`

参数：

`clock`--指向时钟的句柄。

描述：

语法：
```c
cyg_clock_to_counter(
cyg_handle_t clock,
cyg_handle_t *counter
);
```

上下文：

`Init/Thread/DSR`

参数：

`counter`--指向新计数器的指针。

`clock`--指向时钟的句柄。

描述：将时钟转换为计数器处理器，允许使用内核计数器 API 函数。这提供了访问时钟挂载的计数器的权限。

语法：
```c
cyg_clock_set_resolution(
cyg_handle_t clock,
cyg_resolution_t
);
```

上下文：`clock`—时钟句柄。

参数：`resolution`—每滴答（tick）对应的纳秒的分子和分母值。

描述：更改指定时钟对象的分辨率。此函数实际上不会改变驱动时钟硬件的行为。相反，`cyg_clock_set_resolution` 同步内核时钟对象以匹配提供滴答的底层硬件时钟的分辨率。

```c
cyg_resolution_t
cyg_clock_get_resolution(
  cyg_handle_t clock
);
```

上下文：`Init/Thread/DSR`

参数：`clock`—时钟句柄。

描述：返回指定时钟的当前分辨率。

```c
cyg_handle_t
cyg_real_time_clock(
  void
);
```

上下文：`Init/Thread/DSR`

参数：无

描述：返回系统实时时钟的句柄。

```c
cyg_tick_count_t
cyg_current_time(
  void
);
```

上下文：`Init/Thread/DSR`

参数：无

描述：返回以滴答为单位的实时时钟计数器值。

## 7.1.3 报警器

另一个 ECOS定时功能是报警器。报警器附加到计数器上，提供了一种根据计数器值生成事件的方法。该事件可以配置为定期触发或触发一次。

当配置报警器时，将使用处理函数来执行处理事件所需的必要处理。报警器处理程序必须遵循与其他 ISR 函数相同的指南，这些指南在第 3 章“异常与中断”以及“中断与调度器同步”中有详细说明。

列表 7.6 列出了内核报警器 API 函数。提供了一个 `simple-alarm.c` 文件中的示例，展示了如何使用实时时钟实现报警器。eCos 示例作为安装过程的一部分提供，并在第 12 章“使用 eCos 的示例应用程序”中进一步讨论。

## 列表 7.6 内核报警器 API 函数

语法：
```c
void
cyg_alarm_create(
  cyg_handle_t counter,
  cyg_alarm_t *alarm_fn,
  cyg_addrd_t data,
  cyg_handle_t *handle,
  cyg_alarm *alarm
);
```

上下文：

参数：

- `counter`--报警器附加的计数器句柄。
- `alarm_fn`--报警器处理函数的指针。
- `data`--传递给报警处理器的参数。
- `handle`--新报警句柄的指针。
- `alarm`--新报警对象的指针；

描述：构造一个附加到指定计数器的报警对象。当报警触发时，会调用报警处理程序，并在增加计数器的函数环境中执行。在调用 `cyg_alarm_initialize` 之前，计数器不会运行。

语法：
```c
void
cyg_alarm_delete(
  cyg_handle_t alarm
);
```

上下文：

参数：

- `alarm`--报警器的句柄。

描述：禁用报警器并将其从计数器上分离。

语法：
```c
void
cyg_alarm_initialize(
  cyg_handle_t alarm,
  cyg_tick_count_t trigger,
  cyg_tick_count_t interval
);
```

上下文：

参数：

- `alarm`--报警器的句柄。
- `trigger`--导致报警发生的滴答值。
- `interval`--导致报警再次发生的滴答值。将此参数设置为零则在报警发生一次后禁用。

描述：初始化报警器，当滴答值等于 `trigger` 参数时触发。如果 `interval` 参数设置为零，报警在发生一次后禁用。否则，报警根据 `interval` 参数的设置递归。

语法：
```c
void
cyg_alarm_enable(
  cyg_handle_t alarm
);
```

# 第 7 章 • 其他 eCos 架构组件

上下文：

`Init/Thread/DSR`

参数：

- `alarm`—报警器的句柄。

描述：

启用指定的报警器，允许其按照 `cyg_alarm_initialize` 函数的原始设置发生。

语法：
```c
void
cyg_alarm_disable(
  cyg_handle_t alarm
);
```

上下文：

`Init/Thread/DSR`

描述：
