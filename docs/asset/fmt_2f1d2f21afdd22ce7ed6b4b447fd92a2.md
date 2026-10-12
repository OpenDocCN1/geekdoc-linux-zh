
From: `400c52` : predicted

From: `400c4c` : mispredicted

From: `400c62` : predicted

From: `400c52` : predicted

From: `400c62` : predicted

From: `400c4c` : mispredicted

From: `400c62` : predicted

From: `400c52` : predicted

From: `400c62` : predicted

From: `400c4c` : mispredicted

From: `400c62` : predicted

From: `400c52` : predicted

From: `400c62` : predicted

From: `ffffffff172f407` : predicted

From: `400c4c` : mispredicted

From: `400c62` : predicted

From: `400c52` : predicted

## 8.1 事件基础设施 157

SAMPLE `0x400c4c`
16 Branches in Stack
From: `400c4c` : mispredicted
From: `400c62` : predicted
From: `400c52` : predicted
From: `400c62` : predicted
From: `400c4c` : predicted
From: `400c62` : predicted
From: `400c52` : predicted
From: `400c62` : predicted
From: `400c4c` : mispredicted
From: `400c62` : predicted
From: `400c52` : predicted
From: `400c62` : predicted
From: `400c4c` : mispredicted
From: `400c62` : predicted
From: `400c52` : predicted
From: `400c62` : predicted

SAMPLE `0x400710`
16 Branches in Stack
From: `400710` : mispredicted
From: `400c78` : predicted
From: `400c52` : predicted
From: `400c62` : predicted
From: `400c4c` : predicted
From: `400c62` : predicted
From: `400c52` : predicted
From: `400c62` : predicted
From: `400c4c` : predicted
From: `400c62` : predicted
From: `400c52` : predicted
From: `400c62` : predicted
From: `400c4c` : predicted
From: `400c62` : predicted
From: `400c52` : predicted
From: `400c62` : predicted

查看这些结果，突出了几个不同的分支。结果似乎证实了早的假设，即分支预测器擅长处理微基准测试工作负载。指令指针在 `0x400000` 左右的分支显然是用户应用程序的分支，而像 `0xffffff812e` 这样的地址显然是内核代码分支。注意在列表 8.3 的第 97 行，`perf_attr.exclude_kernel` 被设置了。因此，即使某个内核分支被预测错误，它也不会出现在采样数据中。在当时，LBR 记录所有分支，这就是为什么用户空间和内核空间的地址都出现在分支栈中。

虽然此示例打印的是原始结果，但更复杂的应用程序可以对结果进行某些自动分析。例如，性能文件中会出现分支（branches），可以保留一个与指令指针关联的运行计数器。在负载完成后，可以使用此计数器来汇总结果，列出最热的分支。

此外，应用程序还可以通过解析证明文件（如如 `/proc/self/maps`）中的 maps 文件，为生成的报告查找与这些指令指针相关的源代码。这将虚拟内存地址与特定的映射文件（包括可执行文件和共享库）关联起来。然后，使用调试信息，可以将从文件基地址的偏移量转换为源代码和行号。为了简单起见，这些信息也可以在示例应用程序中获取：

```
$ addr2line -e map 0x400c4c

/home/jtk/map.c:126

$ addr2line -e map 400c62

/home/jtk/map.c:125

$ addr2line -e map 400c52

/home/jtk/map.c:127
```

## 8.2 PERF 工具

`perf` 工具利用内核性能事件基础设施的功能进行剖析（profiling）。换句话说，`perf` 提供了对计数和采样事件的访问，处理结果及相关调试信息的解析，并生成突出显示代码中热点的报告。

数据收集可以针对特定进程进行（通过通过 `perf` 启动新进程或挂载到现有进程），也可以针对系统上的每个进程。要监控新进程，只需将命令和相关参数作为最后的参数传递给 `perf` 即可。例如，`perf stat` 会导致 `perf` 创建新进程。要挂载到现有进程，使用 `-p` 参数。例如，`perf record -p 12345` 会导致 `perf` 挂载到 PID 为 `12345` 的现有进程，然后进行测量。最后，可以使用 `perf -a` 选项监控所有进程。

### 8.2.1 表达事件

使用 `-e` 命令参数选择事件。可以通过为每个事件重复该参数来指定多个事件，或者通过提供用逗号分隔的事件列表来指定。通过将逗号分隔的事件列表括在括号中可以创建事件组，例如 `perf stat -e "cycles,instructions"`。对于大多数工具，如果没有指定事件，则选择 CPU 周期。

第 8.2.1 节描述的事件（排除 `PERF_TYPE_RAW`）属于“已处理的”（cooked）事件类别。可以通过 `perf list` 获取这些事件的完整列表以及它们在命令行上的表达方式。

未包含在该列表中事件（即“原始”raw事件）可以使用格式 `r<config number>`。其中 `config number` 是第 6.1 节描述的 MSR 寄存器的十六进制表示。在大多数情况下，这仅仅是 `r<umask value><event value>`。例如，考虑到未停止核心周期（Unhalted Core Cycles）的架构事件，其“已处理”周期的事件编号为 `0x3C`，Umask 值为 `0:00`：

```
$ perf stat -e cycles -e r03c ls > /dev/null
```

'ls' 的性能计数器统计：

| 3,165,711 cycles | 0.000 GHz |
| 3,165,705 r03c | |

0.002415953 times elapsed

这些通常是唯一需要的字段，因为事件修饰符有特殊的语法。它们通过在所修饰的事件末尾添加冒号，然后跟上修饰符列表来实现。表 8.7 列出了可用的修饰符。修饰符可以应用于“已处理的”或“原始”事件。考虑：

```
$ perf stat -e cycles:u -e cycles:k -e r03c:uk ls > /dev/null
```
