
**代码列表 7.2** 使用时和定时器的示例代码。

代码列表 7.2 是一个如何使用系统实时时钟配合定时器的示例。在第 15 行所示 `cyg_user_start` 函数中，使用 `cyg_real_time_clock` 函数将实时时钟句柄存储在 `sys_clk` 中，如第 17 行所示。

接下来，我们在第 19 行获取与实时时钟关联的计数器。句柄存储在变量 `counter_hdl` 中，如第 20 行所示。在第 22 行，我们使用系统实时时钟句柄来创建一个定时器。当定时器触发时，会调用第 23 行传递的函数 `alarm_handler`，并向该函数传递第 24 行所示的变量 `index`。定时器对象通过第 25 行传递的参数 `alarm_hdl` 返回。定时器对象存储在第 26 行传递的参数 `alarm_obj` 中。

最后，我们在第 28 行使用我们创建的定时器处理函数初始化定时器。在 `cyg_alarm_initialize` 函数调用中，我们在第 29 行设置了定时器的初始触发时间。在这种情况下，我们使用了 `cyg_current_time` 函数调用，它返回实时时钟计数器值，并在 tick 值上加上 100。这会导致定时器在当前时间 100 个 tick 后触发。第 30 行的参数决定了初始触发后触发定时器的间隔。在这种情况下，每隔 100 个实时时钟 tick 会调用一次 `alarm_handler` 函数。

`alarm_handler` 函数位于第 36 行至 41 行，它简单地增加了传递给函数的 `data` 参数，并在第 24 行创建定时器时增加了 `index` 变量。

## 7.1 定器 (Timers)

定时器是附加到时钟的闹器。内核定义了一个定时器对象。然而，Cores 没有为定时器对象提供正式实现或内核 API。

Cores 系统中的定时器用于 POSIX 兼容层。POSIX 包使用附加到实时时钟的定时器对象来实现计时功能。

## 7.2 断言 (Asserts) 和跟踪 (Tracing)

Cores 支持两种调试机制：断言和跟踪。断言是一段在运行时检查条件是否符合预期的代码。如果条件符合预期，可能会输出错误消息并停止操作。跟踪允许在应用程序执行的各个点输出文本消息，以便在特定事件发生时跟踪程序的流程。

Cores 断言支持与 C 标准功能（位于 `ISO_ASSERT_HEADER` 配置选项下）互补。

断言和跟踪都定义为宏。宏的第一个参数是一个布尔值，决定是否输出消息。在发布镜像中启用断言和跟踪代码会导致性能下降。这些内容在发布镜像中可以被移除。断言宏定义在 `cyg_assert.h` 中。跟踪宏定义在基础包的 `cyg_trac.h` 中，该文件还包含了跟踪宏的额外详细信息。

在特定架构 HAL 的 `CYG_HAL_VIRTUAL_CONSOLE_CHANNEL` 选项输出断言和跟踪消息。

Cores 定义了三个断言宏，可以在应用程序启用断言时使用：
- `CYG_FAIL`——不接受条件作为第一个参数。相反，该宏无论条件是否满足都会输出标准消息以及用户定义的消息。
- `CYG_ASSERT`——接受条件作为第一个参数。根据条件的值，该宏输出标准消息以及用户定义的消息。
- `CYG_ASSERT`——断言的紧凑版本，根据第一个参数的值输出标准消息。

Cores 支持四种断言和跟踪输出模式。这些模式决定了输出信息的格式：
- Null（空）
- Simple（简单）
- Fancy（花哨）
- Buffered（缓冲）

缓冲模式在调用 `CYG_TRACE_PRINT` 之前不会输出消息。使用 `CYG_TRACE_DUMP` 宏获取内核状态。

Cores 定义了五类跟踪宏。各种宏提供了输出不同消息的标准机制。跟踪宏的形式为 `CYG_TRACENF`，其中 `N` 定义了输出跟踪消息的参数个数（0 到九），`F` 定义了参数输出的格式。Cores 定义了允许最多八个参数的跟踪宏。表 7.1 显示了不同的跟踪宏。

### 表 7.1 跟踪宏

| 宏名称 | 描述 |
| :--- | :--- |
| `CYG_TRACE0` 到 `CYG_TRACE8` | 第一个参数是布尔值，决定是否输出跟踪消息。其他参数使用 `printf` 格式输出。 |
| `CYG_TRACE1X` 到 `CYG_TRACE8X` | 第一个参数是布尔值，决定是否输出跟踪消息。X 使用 `%x` 格式输出。 |
| `CYG_TRACE1Y` 到 `CYG_TRACE8Y` | 第一个参数是布尔值，决定是否输出跟踪消息。Y 使用 `%p` 格式输出。 |
| `CYG_TRACE1D` 到 `CYG_TRACE8D` | D 使用 `%d` 格式输出。 |
| `CYG_TRACE1XV` 到 `CYG_TRACE8V` | 第一个参数是布尔值，决定是否输出跟踪消息。X、Y 和 D 与之前定义的格式相同。V 在跟踪消息中输出参数名。例如：`CYG_TRACE1XV(var);` 将输出以下跟踪消息：`TRACE:file.c(): var=12` |

### 表 7.1 跟踪宏（续）

| 宏名称 | 描述 |
| :--- | :--- |
| `CYG_TRACE1XB` 到 `CYG_TRACE8XB` | B 表示没有第一个参数布尔值；因此使用此宏总是输出消息。X、Y 和 D 与之前定义的格式相同。 |
| `CYG_TRACE1YB` 到 `CYG_TRACE8YB` | |
| `CYG_TRACE1DB` 到 `CYG_TRACE8DB` | |
| `CYG_TRACE1XVB` 到 `CYG_TRACE8XVB` | B 表示没有第一个参数布尔值；因此使用此宏总是输出消息。X、Y 和 D 与之前定义的格式相同。V 在跟踪消息中输出参数名。 |
| `CYG_TRACE1YVB` 到 `CYG_TRACE8YVB` | |
| `CYG_TRACE1DB` 到 `CYG_TRACE8DB` | |

跟踪宏提供了一种调整应用程序内部跟踪消息级别的方法。这允许在运行时控制输出消息。跟踪级别可以通过传递给跟踪宏的第一个参数来控制。代码列表 7.3 展示了使用跟踪级别宏控制调试期间输出消息的示例。

```c
#include <cyg/infra/cyg_trac.h>

static int trace_level = 1;

#define TL1 ( 0 < trace_level )

#define TL2 ( 1 < trace_level )

void my_routine(

    unsigned long index;

    unsigned char v1, v2, v3;

    index++;

    // 使用局部变量 v1, v2, v3 进行处理;

    CYG_TRACE1 ( TL1, "Index: %d", index );

    CYG_TRACE3 ( TL2, "Locals: %d %d", v1, v2, v3 );

}
```
