
传统上，Linux 内核会“滴答”（tick），也就是说，它通过硬件计时器以给定的频率产生中断，代表一次滴答。这些中断每次都会导致内核暂停当前的用户空间程序，进行一些计数，然后选择下一个要运行的进程。这会在通过 `CONFIG_HZ` `Kconfig` 选项选择的间隔内发生。x86 的可能配置选项为 1000、350、250 和 100 Hz。例如，配置为 `HZ=1000` 的内核每秒会接收 1000 次滴答中断，将计时器的分辨率限制为 1 ms。

选择此频率是在产生的中断数量（这会不断唤醒处理器从而降低效率）之间的权衡。

## 5.3 定时

深度睡眠状态，以及快速响应交互式任务的能力，这是由于调度程序更小的时间片（quantum）。每次滴答（tick）都会增加 `jiffies` 内核变量。由于一次 tick 对应于精确的时间，即一个 jiffy 的值等于……秒，因此 `jiffies` 的数量可以作为时钟。

如今，能够更好地优化功耗的用户会将 Linux 内核配置为无滴答（tickless），即无滴答内核，中断仅在需要时发生，而不是固定间隔。这防止了 tick 频繁地唤醒深层睡眠状态，从而节省电源。

可以通过读取 `/sys/bus/clocksource/devices/clocksource0/` 中的 `available_clocksource` 和 `current_clocksource` 来查询系统可用的时源。例如：

```bash
$ /sys/bus/clocksource/devices/clocksource0/available_clocksource tsc acpipm
$ /sys/bus/clocksource/devices/clocksource0/current_clocksource
```

Linux 内核的默认时钟现在是第 5.3.1 节描述的 `TSC` 寄存器。内核使用一个缩放因子将周期转换为纳秒（`$(KERNEL_SRC)/arch/x86/kernel/tsc.c` 中的 `cycles_ns()` 函数）。在 `TSC` 不具有不变性或被认为不可靠的情况下，将使用高精度定时器 (`HPET`)。

时钟通过一系列时间调用暴露给用户空间，包括 `time(2)` 和 `clock_gettime(2)`。

`system(2)` 返回 UNIX 时间，即表示自 UNIX 纪（1970 年 1 月 1 日午夜）以来秒数的整数。由于 UNIX 时间是一个单一整数，因此很容易处理。遗憾的是，它计算秒，因此分辨率为 1 秒，这使其对于精确测量并不实用。

`clock_gettime(2)` 系统调用提供了对多个不同时钟的访问，每个时钟的测量行为略有不同。可以使用 `clock_getres(2)` 测量每个可用时钟的解析。以下是时钟：

- `CLOCK_REALTIME`: 测量时间。受系统时间改变的影响。
- `CLOCK_REALTIME_COARSE`: 与 `CLOCK_REALTIME` 类似，但为了更好的性能牺牲了精度。
- `CLOCK_MONOTONIC`: 测量系统的运行时间。不受手动更改时钟的影响，但受通过 `adjtime(3)` 和 NTP 更新的影响。不包含睡眠状态的时间。
- `CLOCK_MONOTONIC_COARSE`: 与 `CLOCK_MONOTONIC` 类似，但为了更好的性能牺牲了精度。
- `CLOCK_MONOTONIC_RAW`: 与 `CLOCK_MONOTONIC` 类似，但不受系统时间改变的影响。
- `CLOCK_BOOTTIME`: 与 `CLOCK_MONOTONIC` 类似，但包含睡眠状态。
- `CLOCK_PROCESS_CPUTIME_ID`: 进程 CPU 定时器。
- `CLOCK_THREAD_CPUTIME_ID`: 线程 CPU 定时器。

`gettimeofday(2)` 系统调用与使用 `CLOCK_REALTIME` 的 `clock_gettime(2)` 本质上相同。时区参数已废弃，应设置为 NULL。

```c
#include <stdio.h>
#include <math.h>
#include <sys/time.h>

static inline double time_diff_ms(const struct timeval *const s, const struct timeval *const e)
{
    double s_ms, e_ms;

    s_ms = ((s)->tv_sec * 1000) + ((s)->tv_usec / 1000);
    e_ms = ((e)->tv_sec * 1000) + ((e)->tv_usec / 1000);
    return e_ms - s_ms;
}

static void run_bench(double *avg, double *std_dev)
{
    size_t i;

    *avg = 0.0;
    *std_dev = 0.0;
    for (i = 0; i < NUM_RUNS; i++) {
        double measure, t;
        struct timeval s, e;

        gettimeofday(&s, NULL);
        /* do benchmarked code */
        gettimeofday(&e, NULL);

        measure = time_diff_ms(&s, &e);
        *avg += measure / (i + 1);
        *std_dev += (t * (measure - *avg));
    }
    *std_dev = sqrt(*std_dev) / (NUM_RUNS - 1));
}
```

列表 5.3：测量毫秒的函数。

## 第 5 章 设计实验

### 5.4 PHORONIX TEST SUITE

除了运营最流行的专注于 Linux 性能新闻的网站 `http://www.phoronix.com` 之外，Phoronix Media 还制作了一个专门为基准测试设计的框架。该框架被称为 Phoronix Test Suite，提供了一个灵活的架构，可以通过自定义模块和基准测试轻松扩展。虽然 Phoronix 通常关注 Linux 性能，但 Phoronix Test Suite 是跨平台的。

与编写自定义基准测试管理器相比，利用 Phoronix Test Suite 有许多优势：其中一个优势是具有高级的基准测试功能，例如自动重新运行高方差测试的能力，或者利用 Git bisection 的。另一个优势是能够生成高质量的图表，图表可以放在网站上或作为邮件附件。例如，图 5.1–5.3 展示了不同的配置，其中一个突出了性能退化的来源。如果合并来自不同配置的两个结果，系统配置将突出显示这两个配置之间的差异。

Phoronix Test Suite 的另一个有用功能是自动化能力，包括一种无需任何人工干预即可运行预配置基准测试的“批处理（'batch'）模式。这允许将其集成到现有的性能框架中，或者在用自定义实现处理其他方面时，仅利用部分高级功能。

`phoronix-test-suite` 脚本。通过不带任何参数运行该脚本可以获取完整的命令列表。

Phorix Test Suite 中的每个基准测试都由相应的测试配置（test profile）表示。该配置负责定义基准测试如何安装、如何运行、如何解析结果，以及描述结果含义的元数据。多个测试配置可以组合成一个测试套件（test suite）。

该框架包含了许多预定义的测试和测试套件，提供了对热门基准测试的访问。表 5.1 显示了可用基准测试示例及其描述。注意在列表中列表中，存在相似的测试，“GZIP Compression”和“System GZIP Compression”。缺少“System”标识符的 Phorix 测试旨在保持软件不变并测试硬件之间的差异。为了实现这一点，这些测试会下载并编译它们自己版本的软件，而不是测试由 Linux 发行版安装的版本。在根据测试做出决策时，请务必双重检查正在测量的内容。

#### 表 5.1 可用 Phorix 基准测试示例

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| Apache Benchmark | System | 测量给定系统每秒可以维持多少 Apache 请求 |
| BlogBench | Disk | 模拟真实世界中繁忙的文件服务器负载，使用多个线程进行随机读取、写入和重写 |
| Timed Linux Kernel Compilation | Processor | 测量构建 Linux 内核所需的时间 |
| C-Ray | Processor | 通过 C-Ray 光线追踪器测量浮点性能 |
| Cairo Performance Demos | Graphics | 测量 Cairo 绘图性能 |
| Gzip Compression | Processor | 测量使用下载的 gzip 压缩文件所需的时间 |
