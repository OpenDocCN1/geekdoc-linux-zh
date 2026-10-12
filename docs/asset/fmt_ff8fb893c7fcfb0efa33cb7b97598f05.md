
这些事件中的每一个在 `/sys/devices` 中都有对应的目录。在其中某些目录中包含一个 `events` 子目录。在 `events` 目录内，每个预定义事件都有一个文件。这些预定义文件包含了对该事件所需的信息。例如：

```bash
$ ls /sys/devices/cpu/events
Branch-instructions cache-misses instructions
Ref-cycles branch-misses cache-references
Mem-loads stalled-backend bus-cycles
cpu-cycles mem-stores stalled-cycles-frontend
$ cat /sys/devices/cpu/events/cpu-cycles
event=0x3c
$ cat /sys/devices/cpu/events/ref-cycles
event=0x03
$ ls /sys/devices/power/events
```

energy-cores energy-gpu energy-pkg

energy-cores.scale energy-gpu.scale energy-pkg.scale

energy-cores.unit energy-gpu.unit energy-pkg.unit

注意在上面的示例中，有一个名为“power”的事件类型是可以用的；但这种事件类型并未出现在 ABI 事件类型的列表中。这是因为在本文编写时，ABI 头文件在 `perf_type_id` 中没有该类型的对应条目。“power”事件类型引入不到一年前，它添加了利用第 3.2.4 节描述的 RAPL 接口的事件，以提供功耗信息。这说明了基础设施是如何演变的。Andi Kleen 写了一个名为 `libevents` 的库来解析其中列出的事件。它可以在 https://github.com/andikleen/pmu-tools/ 获取。

`perf_event_open(2)` 函数遵循打开文件描述符函数的标准惯例，即返回新的文件描述符或 -1 并设置 `errno`。

## 8.1 事件基础设施

需要填充一个结构体 `perf_event_attr`。该结构体描述了要收集的事件、应如何进行测量以及如何报告结果。系统调用返回一个文件描述符，用于访问所收集的数据。换句话说，每个需要监控的事件都会调用此系统调用。

在本文编写时，glibc 中尚不存在该系统调用的封装器，需要手动（例如使用 `SYSCALL` 指令）进行调用。函数原型可以在列表 8.1 中找到。

```c
int perf_event_open(struct perf_event_attr *attr, pid_t pid,
               int group_fd, unsigned long flags);
```

列表 8.1

`perf_event_open(2)` 函数原型。

如上所述，`attr` 参数负责传递事件配置。

`pid` 指定了要监控的进程。`pid` 为 0 时测量系统上的所有进程，正数 `pid` 则测量给定 `pid` 的进程。

`cpu` 参数指定了要监控的逻辑处理器。`cpu` 值为 -1 时监控所有逻辑处理器，正值或零值则将收集限制在指定的处理器上。

`group_fd` 参数是组组的文件描述符。这允许将多个事件分组在一起。只有当所有成员都准备好测量时，事件组才会被调度进行收集。因此，所有将要计算或比较的事件都应该是同一组的成员，以确保每个指标都是基于简单的代码执行计算的。第一个事件（领导者）在创建时 `group_fd` 为 -1。领导者返回的文件描述符随后会在创建组内所有其他事件时作为 `group_fd` 的值传递。

最后，`flags` 参数允许指定任何行为修饰符。目前，作者认为唯一有用的标志是 `PER_FLAG_PID_CGROUP`，它允许对控制组（cgroup）进行全系统级监控。

`perf_event_open(2)` 函数遵循打开文件描述符的标准惯例，即返回新的文件描述符或 -1 并设置 `errno`。

### 8.1.2 选择事件

通过填充 `perf_event_attr` 结构体并将其传递给内核来选择事件。该数据结构按照内核 ABI 的预期定义在 `/usr/include/linux/perf_event.h` 中。此头文件还包含了各种事件的枚举以及任何其他 ABI 定义。

由于接口的灵活性，事件属性结构相当复杂。确定填充该结构体中的哪些字段取决于所需的信息。

第一步是选择事件和事件类型，分别对应 `perf_event_attr.config` 和 `perf_event_attr.type` 字段。在本文编写时，`perf_event.h` 头文件中列出了以下预定义的事件类型：

```
PERF_TYPE_HARDWARE Hardware Event
PERF_TYPE_SOFTWARE Software Event
PERF_TYPE_TRACEPOINT Tracing Event
PERF_TYPE_HW_CACHE Hardware Cache Event
PERF_TYPE_RAW Hardware Event
PERF_TYPE_BREAKPOINT Hardware Breakpoint
```

此外，可以通过 `sysfs` 列举受支持的事件和事件类型。事件类型可以通过 `sysfs` 中的 `event_source` 基目录进行迭代。`/sys/bus/event_source/devices/` 下的每个目录都代表一种事件类型。要选择该事件，使用 `perf_event_attr.type` 字段在对应目录的 `type` 文件中查找值。注意，`sysfs` 导出的值与预定义值对应。例如：

```bash
$ ls /sys/bus/event_source/devices/
breakpoint@ cpu@ power@ software@ tracepoint
$ cat /sys/bus/event_source/devices/software/type
1
$ grep PERF_TYPE_SOFTWARE /usr/include/linux/perf_event.h
```

```bash
PERF_TYPE_SOFTWARE = 1.
$ cat /sys/bus/event_source/devices/power/type
6
```

这些事件中的每一个在 `/sys/devices` 中都有对应的目录。在其中某些目录中包含一个 `events` 子目录。在 `events` 目录内，每个预定义事件都有一个文件。这些预定义文件包含了对该事件所需的信息。例如：

```bash
$ ls /sys/devices/cpu/events
Branch-instructions cache-misses instructions
Ref-cycles branch-misses cache-references
Mem-loads stalled-backend bus-cycles
cpu-cycles mem-stores stalled-cycles-frontend
$ cat /sys/devices/cpu/events/cpu-cycles
event=0x3c
$ cat /sys/devices/cpu/events/ref-cycles
event=0x03
$ ls /sys/devices/power/events
```

energy-cores energy-gpu energy-pkg

energy-cores.scale energy-gpu.scale energy-pkg.scale

energy-cores.unit energy-gpu.unit energy-pkg.unit

注意在上面的示例中，有一个名为“power”的事件类型是可以用的；但这种事件类型并未出现在 ABI 事件类型的列表中。这是因为在本文编写时，ABI 头文件在 `perf_type_id` 中没有该类型的对应条目。“power”事件类型引入不到一年前，它添加了利用第 3.2.4 节描述的 RAPL 接口的事件，以提供功耗信息。这说明了基础设施是如何演变的。Andi Kleen 写了一个名为 `libevents` 的库来解析其中列出的事件。它可以在 https://github.com/andikleen/pmu-tools/ 获取。

## 8.1 事件

`perf_event_open(2)` 函数遵循打开文件描述符函数的标准惯例，即返回新的文件描述符或 -1 并设置 `errno`。

`perf_event_open(2)` 函数遵循打开文件描述符函数的标准惯例，即返回新的文件描述符或 -1 并设置 `errno`。

`perf_event_open(2)` 函数遵循打开文件描述符函数的标准惯例，即返回新的文件描述符或 -1 并设置 `errno`。

`perf_event_open(2)` 函数遵循打开文件描述符函数的标准惯例， 1。
