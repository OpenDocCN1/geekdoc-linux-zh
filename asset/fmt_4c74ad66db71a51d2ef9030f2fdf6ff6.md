
## 独占监控器（Exclusive monitors）

独占监控器是一个简单的状态机，它必须实现两组监控器：本地和全局（图 7.3）。为了支持处理器之间的同步，系统必须实现本地和全局监控器。独占加载（Load-Exclusive）操作会将监控器的状态更新为独占状态。独占存储（Store-Exclusive）操作会访问监控器，以确定其是否能成功完成。如果所有访问的独占监控器都处于独占状态，则独占存储操作可以成功。

![](img/17ca5177da1b1e15b2169f9c7932e5b6_189_0.png)

图 7.3：多核系统中的本地和全局监控器（来自 [3]）。

`LDREX` 和 `STREX` 指令被 Arm 特定 Linux 内核代码用于实现内核特定的同步原语，这些原语转而用于 POSIX 同步原语。例如，`include/asm/spin_lock.h` 为 Arm 架构实现了自旋锁功能，并被用于 `include/linux/spin_lock.h` 中的非架构特定实现。

## 共享域（Shareability domains）

在缓存一致性对称多处理体系（SMP）的上下文中，Arm 系统架构使用了共享域的概念 [4]，它们是内部共享（Inner Shareable）、外部共享（Outer Shareable）、系统共享（System）或非共享（Non-shareable），如图 7.4 所示。这些域主要用于限制内存屏障的范围，如第 7.3.5 节所述的。

![](img/17ca5177da1b1e15b2169f9c7932e5b6_189_1.png)

图 7.4：基于 [5] 的多核系统中的共享域。

# 第 7 章 | 并发与并行

这些域的架构定义允许我们定义一组观察者，使得共享性使数据访问是透明的。内部域共享代码和数据，在实践中，运行操作系统实例的多核系统将处于内部域；外部域共享数据但不共享代码，并且如图所示，例如包含 GPU、DSP 或 DMA 引擎。将内存区域标记为非共享意味着本地代理（核心）完全不共享该区域。这在 SMP 系统中通常不使用。如果域设置为系统，则对该域的操作将影响系统中的所有代理。例如，UART 接口通常位于共享域，因此其域将是整个系统。

## 3.7.5 Linux 内核同步原语

Linux 内核实现了大量的同步原语；我们在这里只讨论其中一部分。

### 原子原语（Atomic primitives）

Linux 内核实现了一组作为读-修改-写（RMW）操作的原子操作。这些操作是从内存位置读取值、修改然后写回，并保证在读和写之间不会有其他写入操作发生在该位置（因此命名为原子的）。

Linux 中的大多数 RMW 操作属于两类之一：对特殊的 `atomic_t` 或 `atomic64_t` 数据类型进行的操作，以及对位图的操作（位图可能存储在 `unsigned long` 中或 `unsigned long` 数组中）。

为每个架构单独实现的这些 RMW 操作集被称为“原子原语”。作为内核开发者，你将使用这些来编写与架构无关的代码，例如文件系统或设备驱动程序。

由于这些原语作用于原子类型或位图上，让我们先来看看这些。原子类型定义在 `types.h` 中，它们实际上是封装在结构体（struct）中的简单整数：

列表 7.3.1：Linux 内核原子类型

```c
typedef struct {
    int counter;
} atomic_t;

#ifdef CONFIG_64BIT
typedef struct {
    long counter;
} atomic64_t;
#endif
```

之所以这样做是因为原子类型应该定义为有符号整数，但同时也必须是不透明的，这样将其强制转换为普通的 C 整数类型将会失败。

# 在树莓派上运行 Linux 的 Linux 基础

最简单的原子操作是初始化、读取和写入，在 `include/asm/atomic.h` 中为 arm64 架构定义：

### 列表 7.3.2：Linux 内核原子操作

```c
1 #define ATOMIC_INIT(i)    { i }
2 #define atomic_read(v)     READ_ONCE((v)->counter)
3 #define atomic_set(v, i)   WRITE_ONCE((v)->counter, (i))
```

`READ_ONCE` 和 `WRITE_ONCE` 宏定义在 `include/linux/compiler.h` 中，并非特定架构。它们的目的是防止编译器合并或重新获取读取，或重排这些语句。我们在这里展示它们是为了说明要让 C 编译器停止优化是多么困难。

### 列表 7.3.3：Linux 内核原子类型操作

```c
1 #include <asm/barrier.h>
2 #define READ_ONCE(x, check)
3 {
4  union { typeof(x) __val; char __c[1]; } __u;
5  if (check)
6    read_once(&__u.__val, __u.__c, sizeof(__u));
7  else
8    read_once_nocheck(&__u.__val, __u.__c, sizeof(__u));
9  smp_barrier_depend(&__u.__val); /* 强制来自 x 的依赖关系 */
10 return __u.__val;
11 }
12 #define READ_ONCE(x)
```

*(注：此处原文列表 7.3.3 似乎存在截断或重复错误，已根据上下文逻辑翻译并保持结构)*

由于原文提供的文本中列表 7.3.3 存在大量重复和逻辑混乱，此处已根据 Markdown 格式要求进行了结构性翻译。

# 第 7 章 | 并发与并行

### 内存操作排序

在对称多处理（SMP）系统上，来自不同 CPU 的内存访问在原则上是不排序的。我们称这种内存操作排序是松弛的（relaxed）。通常情况下，需要某种程度的排序。Linux 内核的默认做法是通过所谓的内存屏障（memory barrier）来施加严格的全局顺序。严格来说，内存屏障对屏障两侧的内存操作施加了部分排序。引用 Linux 内核文档（memory_barriers.txt）：

这种增强是关重要的，因为系统中的 CPU 和其他设备可以使用多种技巧来提高性能，如内存操作的重排序、延迟和组合；推测加载；分支预测以及各种类型的缓存。内存屏障用于覆盖或抑制（suppress）这些技巧，允许代码能够安全地控制多个 CPU 和/或设备之间的相互作用。

内核提供了内存屏障 `smp_mb_before_atomic()`，在实践中，严格的操作是由一个屏障之前的松弛操作和一个紧随其后的屏障松弛操作组成的，例如：

# 列表 7.3: 通过屏障实现的 Linux 内核原子操作

```
1 atomic_fetch_add();
2 // 等同于：
3 smp_mb before_atomic();
4 atomic_fetch_add_relaxed();
5 smp_mb after_atomic();
```

在松弛和严格排序之间还有两种其他可能的语义，称为获取（acquire）和释放（release）。

获取语义适用于 RMW（读-修改-写）操作和从共享内存读取的加载操作（read-acquire），它防止 read-acquire 操作与程序顺序中随其后的任何读或写操作发生内存重排序。

释放语义适用于 RMW 操作和写入共享内存的存储操作（write-release），它防止 write-release 操作与程序顺序中在随其之前的任何读或写操作发生内存重排序。

表 7.1 提供了所有可能情况的总结。

| 操作类型 | 排序 |
|---|---|
| 非 RMW 操作 | 无序 |
| RMW 操作 | |
| RMW 操作 | 无返回值的 无序 |
| | 有返回值的 | 完全排序 |
| | 具有显式排序 | |
| | [操作名称]_relaxed | 无序 |
| | [操作名称]_acquire | RMW 读取是 ACQUIRE |
| | [操作名称]_release | RMW 写入是 RELEASE |

表 7.1: 内存操作排序语义。

## 树莓派上的 Linux 操作系统基础

### 内存屏障

内存屏障 `smp_mb<before,after>atomic()`并不是 Linux 内核提供的唯一屏障类型。我们可以区分以下类型 [6]：

### 通用屏障

来自 `include/linux/compiler.h` 的通用屏障（barrier）在运行时没有作用；它只作为一种编译器的指令，防止内存访问从语句的一侧移动到另一侧（重排序）。对于 gcc 编译器，它在内核代码中实现为：

```
Listing 7.3.9: Linux 内核通用屏障
```

```
1 #define barrier() asm__volatile__(":": "memory")
```
