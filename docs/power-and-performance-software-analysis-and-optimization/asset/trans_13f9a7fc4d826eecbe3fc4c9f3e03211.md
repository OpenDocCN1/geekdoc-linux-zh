

# 162 第 8 章 Perf 

采样事件 'cycles:ppu' 计数计数（约）：61722942801 

```
+ 40.38% grip grip [.] longest_match
+ 14.51% grip grip [.] deflate
+ 8.37% grip grip [.] updrc
+ 5.73% grip grip [.] fill_window
+ 3.47% grip grip [.] compress_block
+ 3.00% grip grip [.] send_tally
+ 0.61% grip [kernel.kallsyms] [k] sys_check
+ 0.16% grip lib-2.18.0 [.] upwakeup
+ 0.05% grip grip [.] memcpy_sse2_unnaligned
+ 0.04% grip [kernel.kallsyms] [.] build_tree
+ 0.02% grip grip [.] scan_tree
+ 0.02% grip grip [.] bi_reverse
+ 0.01% grip grip [.] gen_code
+ 0.01% grip grip [.] init_block
+ 0.00% grip grip [.] copy_block
+ 0.00% grip grip [.] readfplit
+ 0.00% grip lib-2.18.0 [.] libc_read
+ 0.00% grip grip [.] read_buffer
```

按 'h' 查看按键绑定帮助

图 8.2

Perf 报告 TUI。

| 最长匹配 /home/~j/tk/pmbuild/BUILD/gzip-1.6/gzip | |
|---|---|
| do | Assert(cur_match strstart, "no future"); |
| | match = window + cur_match; |
| 0.74 4028a0 mov | len = (MAX_MATCH - 1) - (int)(strend-scan); |
| | scan = strend - (MAX_MATCH-1); |
| #else /* UNALIGNED OR # */ | if (match[best len]) = scan end || |
| 5.53 4028a2 movslq leak_thr,rxi |
| 31.73 4028a5: movslq 0x650020($krxi,krxi,1),r8 |
| | Assert(strstart < window_size-MIN_LOOKAHEAD,"insufficient |
| do | Assert(cur_match strstart, "no future"); |
| | match = window + cur_match; |
| 0.21 4028ae lea | 0x650020($krxi),r15 |
| | len = (MAX_MATCH - 1) - (int)(strend-scan); |
| | scan = strend - (MAX_MATCH-1); |

按 'h' 查看按键绑定帮助

图 8.3

Perf 报告 TUI。

## 8.2 Perf 工具 163

最高百分比。按 Tab 键将按采样递减顺序循环遍历指令。

在解释注释时，请考虑偏移（skid）。例如，1 的恒定偏移意味着报告的是所标记指令之前的指令样本。

### 8.2.4 PER TIMEART

Perf timechart 是一种图形化描述系统交互的工具。交互包括进程、内核和睡眠状态之间的交互。Timechart 命令通过 `perf timechart` 命令复用。首先，使用 `record` 命令收集事件，该命令接收要运行的命令，类似于 `perf record`。接下来，不带任何参数运行 `perf timechart`。这将生成一个名为 output.svg 的系统事件 SVG 时间轴。即

```
$ perf timechart record <command>
$ perf timechart
```

例如，在 gzip 压缩负载上运行 perf timechart：

```
$ perf timechart gzip -c -6 /dev/shm/linux-31.5.tar /dev/null
[ perf record: Woken up 3 times to write data ]
[ perf record: Captured and wrote 0.883 MB perf.data (-38600 samples) ]
$ perfchart
```

已向 output.svg 写入 16.2 秒的跟踪数据。

此示例的输出见图 8.4。

使用矢量图像格式的优势在于能够提供可缩放的细节。以不同尺寸查看图表（即放大和缩小）可以显示不同级别的细节。例如，缩放 CPU 条形可以显示代表 CPU 状态转换的不同颜色条，如空闲状态。要正确利用可缩放的细节，请确保在 SVG 编辑器或查看器（如 inkscape）中查看 SVG，而不是将矢量图像转换为位图查看的工具。

可缩放细节的缺点是文件和时间轴的大小。为了保持结果可控，作者建议避免在运行中的进程上使用 timechart。

时间轴突出了各个进程之间的交互。图表顶部是一系列代表 CPU 状态的条形。在高细节级别，这些条形显示了 CPU 在该特定时刻正在做什么。这些包括运行（Running）、空闲（Idle）、深层空闲（Deeper Idle）、深度睡眠（Deep Sleep）、等待 CPU（Waiting for CPU）和被 IO 阻塞（Blocked on IO）。增加细节级别（即放大图像）会显示更多关于状态的信息。如图 8.5 所示。CPU 状态下方是代表系统上进程的条形。与 CPU 条形类似，这些条形以相同的颜色分类显示单个进程状态。

![img/33fadfa149d4f0cdd5ff256970ab181_0] 图8.4 timechart 输出。

![img/33fadfa149d4f0cdd5ff256970ab182_0] 图8.5 缩放 timechart。

### 参考文献

- Weiner, T., Molnar, I., 2014, 05. perf_event.h. ${LINUX_SRC}/include/uapi/linux/perf_event.h.
- Howells, D., 2012, 11. hw_breakpoint.h. ${LINUX_SRC}/include/uapi/linux/hw_breakpoint.h.
- Intel Corporation, 2013. Intel 64 and IA-32 Architectures Software Developer's Manual.
- Kleen, A., S., Molnar, I., Zijlstra, P., 2014, 02. perf_event_intel.c. ${LINUX_SRC}/arch/x86/kernel/cpu/perf_event_intel.c.
- Molnar, I., Zijlstra, P., Weiner, T., 2014, 06. core. ${LINUX_SRC}/kernel/events/core.
- Tovral, L., et al., 2014, 06. fault.c. ${LINUX_SRC}/arch/x86/mm/fault.c.
- Weaver, V., 2013. 07. perf_event_open manual page.
- Zijlstra, P., Molnar, I., Howells, D., et al., 2014, 01. parse_events.c. ${LINUX_SRC}/tools/util/parse-events.c.

# Ftrace 9

目录
9.1 DebugFS ........................................................ 168
  9.1.1 Tracers ....................................................... 169
    Available tracers.............................................................. 170
    function and function_graph............................................... 170
    blk ................................................................... 173
    Nop ................................................................... 176
  9.2 Kernel Shark ................................................................ 176
  References ............................................................ 178

Ftrace 是 Linux 内核中的一种调试基础设施，暴露内核的内部行为。这些数据允许分析人员洞察正在执行的路径，并帮助隔离导致性能问题的内核条件。虽然 Ftrace 是“function tracer”的缩写，但它监控的不只是函数调用。Ftrace 还可以监控内核内的静态和动态跟踪点，称为事件。静态跟踪点是由各个子系统创建的定义事件。通过跟踪这些事件，开发者可以更好地理解他们的代码如何与内核以及硬件交互。

例如，在本文编写时，Intel® i915 图形驱动程序暴露了三十个静态跟踪器。大多数关注 i915 GEM内存对象的操作，如 i915_gem_object_create、i915_gem_object_evict 和 i915_gem_object_destroy。其他 i915 跟踪器专注于记录驱动更新寄存器 i915_reg_rw，或重要的渲染事件，如 i915_flip_request 和 i915_flip_complete。

除了这些静态跟踪点外，ftrace 还支持动态跟踪点。动态跟踪点允许在运行时几乎任何地方插入自定义跟踪点。为了实现这一点，跟踪点没有被定义为高级事件，而是定义为导出内核符号的内存偏移。此外，通过指定跟踪点位置相关数据的寄存器列表、内存标签和栈偏移，可以记录每个动态跟踪点的状态。由于由于，利用动态跟踪点至少需要对被跟踪代码的基础知识。

与第 7 章和第 8 章讨论的性能工具（Intel® VTune Amplifier 和 perf）使用统计采样将事件归类到相关的热点中，而跟踪工具则在事件发生时记录相关信息。Linux 内核跟踪基础设施经过优化，使得跟踪点即使被编译进内核，在运行时禁用的情况下开销也极低（通常只是一个分支）。这极大地增强了 ftrace 的用性，因为这种低开销鼓励 Linux 跟踪在他们的默认内核配置中启用跟踪点。否则，禁用跟踪点时的巨大开销将迫使他们仅使用调试内核。

在本文编写时，Android、Fedora 和 Red Hat Enterprise Linux 等常见 Linux 发行版在其默认内核配置中启用了跟踪基础设施。其主要的内核配置是 CONFIG_TRACE。其他配置选项提供了对可用跟踪功能的细粒控制。选项包括 CONFIG_FUNCTION_TRACER、CONFIG_FUNCTION_GRAPH_TRACER、CONFIG_STACK_TRACER、CONFIG_FTRACE_SYSCALLS 等。例如，检查 Fedora 20 上 x86_64 的默认内核配置：

```
$ grep CONFIG_TRACE /boot/config-uname -r'
CONFIG_TRACE=y
CONFIG_FTRACE_SYSCALLS=y
CONFIG_FTRACE_COUNT_RECORD=y
# CONFIG_FTRACE_STARTUP_TEST is not set
$ grep CONFIG_FUNCTION /boot/config-uname -r'
CONFIG_FUNCTION_TRACER=y
CONFIG_FUNCTION_GRAPH_TRACER=y
CONFIG_FUNCTION_PROFILER=y
```

## 9.1 debugfs

ftrace API 通过 debugfs 内存备份文件系统暴露。因此，与书中讨论的其他性能工具不同，ftrace 的所有功能都可以无需专用工具进行访问。相反，所有操作（例如选择报告的数据、开始和停止数据收集以及查看结果）都可以通过基础实用程序（如 cat(1) 和 echo(1)）完成。

