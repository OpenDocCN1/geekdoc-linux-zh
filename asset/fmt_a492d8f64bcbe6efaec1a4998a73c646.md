
$ `opcontrol --start`

Profiler running.

$ `./summer-proj`

$ `opcontrol --dump`

$ `opgprof ./summer-proj`

$ `gprof --no-graph -l ./summer-proj | head`

Clear statistics. Run your code. Tell daemon to dump. Create `gmon.out` for `gprof`.

```
Flat profile:

| cumulative samples self total | | | |
| time samples calls T1/call T1/call name |
|---|---|---|---|---|---|
| 46.81 | 3496.00 | 3496.00 | | | summer-proj.c:19 @ 8 4844 |
| 20.10 | 4997.00 | 1501.00 | | | summer-proj.c:12 @ 8 4833 |
| 14.82 | 6140.00 | 1107.00 | | | summer-proj.c:19 @ 8 482c |
| 8.19 | 6716.00 | 612.00 | | | summer-proj.c:22 @ 8 4810 |
| 4.69 | 7066.00 | 350.00 | | | summer-proj.c:21 @ 8 483ea |
```

这产生了熟悉的逐行分析。再次，没有信息——只有样本计数。OProfile 通过 `opannotate` 提供带注释的源码使得 `gprof` 更好。这一步是：

```
$ opannotate --source ./summer-proj
```

输出到 stdout（如下）。

```
/*
* Command line: opannotate --source ./summer-proj
* Interpretation of command line:
* Output annotated source with samples
* Output all files
* CPU: P4 / Xeon, speed 1700 MHz (estimated)
* Counted Global_POWER_EVENTS (time during which processor is not stopped) with a unit mask of 0x01 (mandatory) count 100000
* Total samples for file: "/home/john/examples/07/prof/summer-proj.c"
* 7458 99.8527
*/
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <time.h>
#include <math.h>

volatile double x;
int main(int argc, char *argv[]) {
    /* main total: 7458 99.8527 */
    int i;
    for (i = 0; i < 1600000; i++) {
        x = 1000.0;
        /* 0 <= r < 16 */
        int r = i & 0xf;
        if (r <= 8) {
            x = pow(x, 1.23); /* called 9/16 of the time. */
        } else if (r <= 11) {
            x = sqrt(x); /* called 3/16 of the time. */
        } else {
            x = 1.0 / x; /* called 4/16 of the time. */
        }
    }
}
```

```
1554 20.8060
27 0.3615
6 0.0803
115 1.5297
4678 62.6322
350 4.6860
612 8.1939
116 1.5531
```

在这里，我们使用了 `gcov` 和 `gprof` 的优势。每行代码都标记了样本计数—— `profiled` 捕获执行该代码的次数。接下来，样本计数是花在代码行上的百分比。此百分比针对收集的文件进行了归一化，因此无论同时运行其他什么，数字总和都为 100%。

### 关于 OProfile 的结语

我仅仅触及 OProfile 功能的一角。特别是我没有检查 OProfile 能够监控的任何其他类型的。每个处理器的精确事件不同，你可以通过以下命令查看你的处理器的功能：

```
$ opcontrol --list-events
```

输出应该是很长的。默认事件适用于应用程序分析，但对于系统分析，你可能想要探索可用的其他事件。你可以在 OProfile 的主页找到更多信息。

## 9.4 多处理器性能

运行在多个 CPU 上的操作系统称为对称多处理（SMP），它已经存在多年。当使用 SMP 时，繁忙服务器的整体系统吞吐量会增加，因为调度器将进程分配到各个 CPU。另一方面，单个单线程应用程序在多处理器机器上运行得并不更快，因为它一次只能运行在一个处理器上。从 SMP 中获益最大的应用程序是多线程应用程序，它允许操作系统将线程分布到处理器上以更高的吞吐量。

最近，微处理器供应商一直在提供多核和多线程 CPU。这意味着许多桌面和笔记本电脑现在需要 SMP 操作系统来利用这些新处理器。以前，只有服务器和高端工作站使用 SMP 硬件。

### 9.4.1 SMP 硬件类型

SMP 有几种种类，新的种类正在路上。每种 SMP 方法都有优缺点。理解这些可以帮助你设计最充分利用多处理器硬件细节的代码。

在介绍 SMP 实现之前，你需要一些背景知识。如果你已经熟悉这些术语，可能想跳过以下章节。

#### 9.4.1.1 CPU 并行的一些背景

为了提高最快 CPU 的速度，制造商多年来采取了多种技巧。了解这些技巧有助于你理解为什么 SMP 和多核 CPU 是重要的。

##### RISC 与 CISC

很难想象，但曾经有一个时代人们不信任编译器。程序员直接用汇编编写代码，即使编译器可用。汇编语言被认为是效率最高的语言，而且大多数汇编语言程序员并不信任编译器能产生高效甚至正确的输出。

当今的大多数处理器都是 CISC（复杂指令集计算机），它们提供了丰富的指令集和多种寻址模式，使得汇编语言编程变得更容易。CISC 处理器的两个显著示例是摩托罗拉 68000 和 Intel 8086。摩托罗拉处理器是原始 Macintosh 计算机使用的处理器，而 8086 则是 IBM PC 使用的处理器。¹8086 指令集今天仍作为 IA32 架构的一个子集存在。

来自 IBM、斯坦福大学和伯克利大学的研究表明，通过创建更少的指令、限制的寻址模式和更低的指令延迟，他们可以更有效地利用 CPU 上的晶体。这就是创建精简指令集计算机（RISC）处理器的动机。通常情况下，RISC 指令对编译器更友好，而不是对用户友好。RISC 处理器的示例包括 PowerPC、SPARC 和 MIPS 处理器。

##### 流水线与执行并行

一种让 CISC 和 RISC 处理器运行更快的创新是使用流水线（pipelining）——这是计算机中类似于熟悉的流水线，亨利·福特在 20 世纪初利用它来加速汽车制造。当汽车的组装被分成几个步骤时，每个工人都可以专门负责一个组装步骤。由于所有工人都是专家，他们的工作效率比每个人都必须从头到尾组装汽车要高。

CPU 流水线不是组装汽车，而是一次执行一条指令。CPU 设计师将每条指令拆分为若干可以独立执行的离散步骤。每个步骤都配有在流水线中专门用于该步骤的专用硬件。这种专用硬件被称为执行单元（有时称为超标量单元）。流水线之于组装线，执行单元之于工人。

然而，与组装线的相似性仅此于此。不同的指令需要不同的阶段，某些指令的执行时间比其他指令长。指令流水线就像是一个在单条流水线上组装汽车、卡车、自行车和飞机的流水线。我们将一条指令穿过流水线所需的时间称为指令*延迟*（latency）。

> 16. 从技术上讲，它是 8088——8086 的 8 位版本。

流水线的每个阶段都在一个 CPU 时钟周期内完成，因此一个具有 2 阶段流水线的 CPU 可能需要最多 20 个时钟周期来完成单条指令。这看起来很多，但如果你考虑到 CPU 可以同时处理 20 条指令，那么净*吞吐量*（throughput）可以达到每个时钟周期一条指令。由于流水线*停顿*（stalls），这种理论最大吞吐量很少能实现。

流水线停顿通常是由条件分支指令引起的。当分支指令及其条件被解码时，流水线中后面可能已经有几条指令。这些指令可能会因为分支而被丢弃。在这种情况下，吞吐量会下降，因为 CPU 在重新执行指令之前必须填满流水线。流水线的深度决定了这种惩罚有多大，如图 9-3 所示。
