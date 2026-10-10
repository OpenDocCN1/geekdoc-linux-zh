
Breakpoint 1, `main__omp_fn()` at `omp_test.c:15`

`15			place++;`

```
注意在跳过 `#pragma` 行后，GDB 显示程序创建了三个新的工作线程。默认情况下，调试会话留在主线程中。程序员可以使用 `info threads` 命令查看活动线程列表，并将调试会话切换到另一个线程，例如使用 `thread 1` 命令切换到线程 1。
另外注意当前函数是 `main__omp_fn()`。由于调试会话不再 `main` 函数中，用户无法访问局部变量。
遗憾的是，GCC 没有为并行区域内的局部生成调试信息。在本章稍后的部分，你可能需要使用 `info registers`。
```

### 2.4.6 The OpenMP parallel for pragma

内核通常由包含嵌套循环的 `for` 循环组成。OpenMP 提供了一种简单的方法，使用 `for` 指令将 `for` 循环的迭代自动分配到多个线程。该指令可以写为：

```c
#pragma omp parallel
#pragma omp for
for (...)
```

或者作为简写形式：

```c
#pragma omp parallel for
for (...)
```

`parallel for` 指令要求终止条件必须是与循环变量的单个小于、小于等于、大于或大于等于比较，增量操作不能依赖于循环体中的代码，且循环体内不允许使用 `break`、`goto` 或 `throw` 语句。

默认情况下，循环变量被处理为私有。这很重要，因为每个线程将同时处理一组不同的循环迭代，因此每个线程的 `i` 变量值在同一时刻会有不同的值。

考虑以下示例：

```c
#pragma omp parallel for
for (i=0;i<12;i++) {
    printf("iteration %d, thread %d\n",
    i,omp_get_thread_num());
}
```

执行时，新代码将产生以下输出：

+   iteration 0, thread 0
iteration 1, thread 0
iteration 2, thread 0
iteration 9, thread 3
iteration 10, thread 3
iteration 11, thread 3

# 第 2 章 多核与数据级优化：OpenMP 与 SIMD

iteration 6, thread 2

iteration 7, thread 2

iteration 8, thread 2

iteration 3, thread 1

iteration 4, thread 1

iteration 5, thread 1

主线程已完成

如我们的输出所示，每个线程被分配了三次迭代。由于线程正在并行执行，所有线程的打印语句在控制台中是交替显示的。由于并行区域后存在屏障（barrier），主线程在并行区域后的打印消息始终出现在控制台输出的末尾。

OpenMP 支持多种分配迭代的线程策略。默认情况下，分配是静态的（static），这意味着每个线程执行大约相同数量的循环迭代。由于所有线程在程序离开循环之前必须完成分配的迭代集，因此分配的任务完成得比其他线程快的线程将经历比其他线程更长的等待时间。

为了避免这个问题，OpenMP 支持动态调度（dynamic scheduling），将较小的一批循环迭代（称为块，chunk）分配给每个线程。当某个线程完成上一个块时，会轮分配一个新的块。这允许负载均衡，并且当迭代之间的执行时间变化时效果最好。

通常情况下，调度适用于 `parallel for` 指令，并可以使用 `parallel` 指令的 `schedule` 选项进行指定。默认情况下，并行循环采用静态调度。指令选项可以指定动态调度。例如，`#pragma parallel (dynamic)` 开启自动块大小的动态调度；`#pragma parallel for schedule(dynamic,chunksize)` 允许程序员指定 `chunksize`。

### 2.4.7 结合性能计数器的 OpenMP

`Perf_event` 仅在主线程中记录事件，因此程序员在计算包含未由性能计数器报告的指标（例如浮点操作次数）时需要考虑到这一点。例如，`cnts_dump()` 函数仅统计主线程执行的指令数。要计算每个浮点运算（flop）的指令数，请将指令数乘以 `NUM_THREADS` 或将浮点操作次数除以 `NUM_THREADS`。

### 2.4.8 OpenMP 对 Horner 核的支持

Horner 核的最外层循环不包含跨迭代的依赖，这意味着每次迭代都与后续迭代无关。通过这种方式，程序员可以将最外层循环的工作负载分布到所有可用核心上。OpenMP 头文件以及一个设置线程数的定义（该值应设置为您特定处理器的核心数）：

```c
#include <comp.h>
```

```c
#define NUM_THREADS 4
```

在代码的初始化部分指定线程数：

```c
omp_set_num_threads(NUM_THREADS);
```

最后，告诉 OpenMP 运行时对外层循环进行并行化：

```c
#pragma omp parallel for
for (i=0;i<N/4;i++) {
    d[1]=coeff[0];
    for (j=1;j<8;j++) {
        d[1]*=x[i];
        d[1]+=coeff[j];
    }
}
```

## 2.5 性能边界

处理器的理论峰值性能至少为 $2 \times cores \times frequency \times n$，其中 $n$ 是处理器每个周期可以执行的浮点操作次数，且该处理器支持乘加运算。对于单精度浮点数，ARM11 处理器的 $n=1$，Cortex 处理器的 $n=4$。这使得树莓派上的 ARM11 处理器峰值容量达到 1.4 Gflops，Xilinx Zedboard 上的 Cortex-A9 处理器达到 2.7 Gflops，而 NVIDIA Jetson 上的 Cortex-A15 处理器达到 17.8 Gflops。

在实践中，任何处理器达到其峰值浮点性能几乎是不可能的，因为这需要供应商每个周期都向所有浮点单元提供输入，并消除所有延迟。延迟的一个重要来源是平均内存访问时间，这意味着浮点单元在访问计算所需数据的整个时间内都处于忙状态。由于浮点单元的吞吐量远高于片外内存，它们的有效性能取决于内核在执行过程中重用数据的程度。这种重用率通常通过测量的算术强度（arithmetic intensity）来表示，即每字节数据的平均浮点操作次数。

每个 CPU 都有一个理论算术强度阈值，在该阈值之下，内核性能受内存带宽限制；之上则受浮点吞吐量限制。这是一种过于简化，因为它没有考虑决定缓存性能的内存局部性或其他延迟源（如数据依赖引起的延迟）。

算术强度提供了一个比峰值浮点性能更紧密的性能上界。其计算方式为：

```
Upper bound = min \frac{2 \times cores \times frequency \times n}{intensity \times peak memory b/w} 浮点操作每字节
```
