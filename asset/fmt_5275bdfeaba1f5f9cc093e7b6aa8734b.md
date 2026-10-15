
禁用指定的报警器以防止其发生。可以使用 `cyg_alarm_initialize` 或 `cyg_alarm_enable` 函数重新启用报警器。

在列表 7.2 中，我们看到了一个结合内核时钟 API 和内核报警器 API 的示例。

```c
1 #include <kernel/kapi.h>
3 cyg_handle_t counter_hdl;
4 cyg_handle_t sys_clk;
5 cyg_handle_alarm_hdl;
6 cyg_tick_count_t ticks;
7 cyg_alarm_t_alarm_handler;
8 cyg_alarm_alarm_obj;
10 unsigned long index;
12 //
13 // 应用起始点。
15 void cyg_user_start( void )
17 sys_clk = cyg_real_time_clock();
19 cyg_clock_to_counter( sys_clk, &counter_hdl);
22 cyg_alarm_create( counter_hdl, alarm_handler, (cyg_addrd_t)&index, &alarm_hdl, &alarm_obj );
28 cyg_alarm_initialize( alarm_hdl,

30      cyg_current_time() + 100,
31      100);
32

33  //
34  // 报警处理程序。
35  //
36  30

36  void alarm_handler(
37      cyg_handle_t alarm_handle,
38      cyg_addrd_t data )
39  )
40      (unsigned long)data++;
41 )
```

# 代码列表 7.2 使用时钟和报警器的示例代码。

代码列表 7.2 是一个如何结合实时时钟使用报警器的示例。在第 15 行所示的 `cyg_user_start` 函数中，使用 `cyg_real_time_clock` 将实时时钟句柄存储在 `sys_clk` 中，如第 17 行所示。

接下来，我们在第 19 行获取对实时时钟附加计数器的访问。处理程序存储在变量 `counter_hdl` 中，如我们在第 20 行所示。我们使用实时时钟的句柄创建一个报警器。当报警触发时，会调用第 23 行所示的 `alarm_handler` 函数并传递 `index` 变量，在第 28 行创建报警。最后，通过 `cyg_alarm_initialize` 在第 30 行设置 `trigger`。如果在第 41 行设置 `interval` 参数，报警将在发生一次后禁用。

## 7.1.4 定时器

另一种定时功能是定时器。ECOS 支持两种辅助调试的机制：断言（asserts）和追踪（tracing）。断言是一种在运行时检查条件是否符合预期的代码。如果条件不符合，可以输出错误消息并停止程序。追踪则允许在执行的各个点输出文本。这允许你跟踪执行流或检查特定状态。

eCos 的断言支持与 ISO 基础中包含的断言头文件（`CYGLBD_ISO_ASSERT_HEADER`）配置选项互补。

断言和追踪都定义为宏。宏的第一个参数是一个布尔值，决定了消息是否预期。在发布镜像中启用断言和追踪代码会导致性能下降。使用宏可以在发布版本中移除这些开销。断言宏定义在基础包的 `cyg_ass.h` 文件中。该文件的顶部注释还包含了关于追踪宏及其使用的额外细节。

断言和追踪消息输出在通过诊断串口端口（`CYGNM_HAL_VIRTUAL_VECTOR_CONSOLE_CHANNEL`）选项配置的端口上。

eCos 支持四种不同的断言和追踪模式。这些模式决定了输出信息的格式。这四种模式为：

## 断言与跟踪 (Asserts and Tracing)

- 空 (Null)
- 简单 (Simple)
- 复杂 (Fancy)
- 缓冲 (Buffered)

缓冲跟踪模式在调用 `CYG_TRACE_PRINT` 之前不会输出消息。列表 7.7 描述了每种输出模式的输出消息。

还有一种使用 `CYG_TRACE_DUMP` 宏获取内核状态的机制，该宏也定义在 `cyg_trac.h` 文件中。eCOS 定义了五种类型的跟踪宏。这些宏为输出跟踪信息提供了标准机制。跟踪宏 `##` 中的 `#` 定义了传递给宏输出跟踪消息的参数个数（0到9），而 `%%` 定义了参数输出的格式。eCOS 定义的跟踪宏允许最多八个参数进行输出。表 7.1 显示了不同的跟踪宏及其描述。

## 表 7.1 跟踪宏

| 宏名称 | 描述 |
|---|---|
| `CYG_TRACE0` 到 `CYG_TRACE8` | 第一个参数是布尔值，决定是否输出跟踪消息。其他可能的参数使用 printf 风格的格式输出。 |
| `CYG_TRACE1X` 到 `CYG_TRACE8X` | 第一个参数是布尔值，决定是否输出跟踪消息。 |
| `CYG_TRACE1Y` 到 `CYG_TRACE8Y` | X—使用 `%0x` 格式输出参数。 |
| `CYG_TRACE1D` 到 `CYG_TRACE8D` | Y—使用 `%x` 格式输出参数。D—使用 `%d` 格式输出参数。 |
| `CYG_TRACE1XV` 到 `CYG_TRACE8XV` | 第一个参数是布尔值，决定是否输出跟踪消息。X、Y 和 D 与之前定义的格式相同。V 导致在跟踪消息中进行命名输出。例如：`CYG_TRACE1XV(var);` 将输出以下跟踪消息：TRACE:file.c[8]rout(): var=12 |

## 表 7.1 跟踪宏（续表）

| 宏名称 | 描述 |
| --- | --- |
| `CYG_TRACE1XB` 到 `CYG_TRACE8XB` | B 表示没有第一个布尔值参数；因此，使用此跟踪宏总是输出消息。X、Y 和 D 与之前定义的格式相同。 |
| `CYG_TRACE1YB` 到 `CYG_TRACE8YB` | B 表示没有第一个布尔值参数；因此，使用此跟踪宏总是输出消息。X、Y 和 D 与之前定义的格式相同。V 导致参数名出现在跟踪消息中。 |
| `CYG_TRACE1DB` 到 `CYG_TRACE8DB` | |

跟踪宏提供了一种定制应用程序内跟踪消息层级的方法。这允许在运行时控制输出消息的数量。跟踪级别可以通过传递给跟踪宏的第一个参数来控制。代码列表 7.3 展示了使用跟踪级别宏在调试期间控制输出消息的示例例。

```c
#include <cyg/infra/cyg_trace.h>
static int trace_level = 1;
#define TL1 ( 0 < trace_level )
#define TL2 ( 1 < trace_level )
void my_routine(
    unsigned long index)
{
    unsigned char v1, v2, v3;
    index++;
    // 使用本地变量 v1, v2 和 v3 进行处理。
    CYG_TRACE1( TL1, "Index: %d", index );
    CYG_TRACE3( TL2, "Locals: %d %d %d", v1, v2, v3 );
```

## 代码列表 7.3 跟踪输出运行时控制示例。

从代码列表 7.3 中可以看出，第 3 行所示变量 `trace_level` 控制输出哪些跟踪消息。第 5 行和第 6 行的不同 TLX 宏定义了消息的跟踪级别。

函数 `my_routine` 接收一个名为 `index` 的参数，该参数在第 13 行递增。本地变量如第 15 行所示用于某些处理中。第 17 行和第 19 行的两条跟踪消息允许根据跟踪级别的设置输出不同级别的信息。

在此示例中，第 17 行的 `CYG_TRACE1` 消息被输出，因为当 `trace_level` 设置为 1 时，`TL1` 宏（第 5 行）的值为 1。然而，第 19 行的 `CYG_TRACE3` 没有输出，因为当 `trace_level` 设置为 1 时，`TL2` 宏（第 6 行）的值为 0。

将 `trace_level` 的值改为 2（可以在运行时完成），允许在下次调用 `my_routine` 时输出 `CYG_TRACE3` Assert & Tracing (CYPKG_INFRA_DEBUG)。

位于 Infrastructure 包中的主配置决定了应用程序镜像中是否包含任何断言或跟踪消息。默认情况下，断言和跟踪是禁用的。参见列表 7.7 列出的 eCOS 系统中可用的断言和跟踪配置选项。

## 列表 7.7 断言与跟踪配置选项

- **选项名称：** 使用断言 (Use Asserts)
  CDL 名称：`CYDBG_USE_ASSERTS`
  描述: 启用断言代码检查和输出消息。
- **选项名称：** 使用跟踪 (Use Tracing)
  CDL 名称：`CYDBG_USE_TRACING`
  描述: 启用跟踪代码输出消息。
- **选项名称：** 空输出 (Null Output)
