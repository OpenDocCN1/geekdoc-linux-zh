
- 处理此时间变量的函数包含在`/usr/src/linux/include/linux/ktime.h`中，不需要过多解释：

# 10.8 实验

```c
static int __init_my_init(void) {
    data = kmalloc(sizeof(*data), GFP_KERNEL);
    data->period = ktime_set(1, 0);    /* short period, 1 second */
    hrtimer_init(&data->timer, CLOCK_REALTIME, HRTIMER_MODE_REL);
    data->timer.function = ktfunun;
    hrtimer_start(&data->timer, data->period, HRTIMER_MODE_REL);

    return 0;
}
```

```c
static void __exit_my_exit(void) {
    hrtimer_cancel(&data->timer);
    kfree(data);
}
```

```c
module_init(my_init);
module_exit(my_exit);
MODULE_LICENSE("GPL v2");
```

## 10.8 实验

### 实验 1：字符驱动中的内核定时器

- 编写驱动程序，每当对设备进行`write()`操作时，启动一个内核定时器。
- 向驱动程序传递一些数据并将其打印出来。
- 在定时器函数被调度时打印`current->pid`字段，然后在函数执行时再次打印。

### 实验 2：多个内核定时器

- 将第一个实验中的周期设置得足够长，以便在定时器函数运行之前可以执行多次写操作。提示：你可能想在运行此实验之前保存好你的数据。
- 该函数运行了多少次？
- 修复解决方案使多个定时器能够正常工作。

### 实验 3：周期性内核定时器

- 编写一个模块，启动一个周期性的内核定时器函数；即它应该重新安装自己。

### 实验 4：多个周期性内核定时器

- 编写一个模块，启动两个周期性的内核定时器函数；即它们应该重新安装自己。
- 一个周期序列应该小于 256 个 ticks，因此落在`tv1`向量中，另一个应该小于 16 K ticks，因此落在`tv2`向量中。
- 每当定时器函数执行时，打印自模块加载以来的总经过时间，以 jiffies 为单位。

### 实验 5：高分辨率定时器

- 执行与上一个练习相同的任务，设置两个周期性定时器，但这次使用`hrtimer`接口。

### 实验 6：使用 kprobes 获取统计数据

- 使用 kprobes 找出内核定时器在运行之前被删除的频率。
- 检查内核源码发现，定时器是通过`add_timer()`或`mod_timer()`的。
- 你可以通过监控`del_timer()`和`del_timer_sync()`来查看定时器删除的频率；然而在单处理器系统上，`del_timer_sync()`未定义。
- 定时器非常频繁，你可能不想在每次调度或删除时都打印，例如每 100 次打印一次加上最后的统计。
- 定时器的删除可能比调度更频繁吗？

# 第 11 章 竞态条件与同步方法

![](img/134c18b05ee9bbbe93ba3f4335720ac1_120_0.png)

我们将考虑内核用于同步和避免竞态条件的一些方法。我们将讨论原子函数和位操作、自旋锁、互斥锁、信号量以及完成函数的使用。最后我们将查看内核如何维护引用计数。

- 11.1 并发与同步方法 105
- 11.2 原子操作 107
- 11.3 位操作 108
- 11.4 自旋锁 109
- 11.5 大内核锁 110
- 11.6 互斥锁 111
- 11.17 信号量 113
- 11.8 完成函数 116
- 11.9 引用计数 116
- 11.10 实验 117

## 11.1 并发与同步方法

内核执行是异步且不可预测的；中断会随时发生，系统调用可能会被抢占。这可能导致竞态条件，即多个执行线程同时访问相同数据，从而产生不可预测的结果。

竞态条件发生在两个或多个执行线程并发访问共享数据时，且最终结果取决于访问的顺序。

为了避免竞态条件，内核使用了多种同步方法：

- 原子操作：这些操作保证在单个不可分割的步骤中完成。
- 自旋锁：一种锁，线程会在循环中“自旋”直到锁可用。
- 互斥锁：类似于自旋锁，但如果锁被占用，线程将进入睡眠。
- 信号量：用于控制多个线程或进程对资源的访问的同步机制。
- 完成函数：用于向线程通知事件已发生。

## 11.2 原子操作

```
int atomic_inc_return(int i, atomic_t *);
int atomic_dec_return(int i, atomic_t *);
```

- 注意`ATOMIC_INIT()`、`atomic_read()`和`atomic_set()`宏是自动原子的，因为它们只是读取和写入一个值。
- 在 64 位平台上，还有一种 64 位的原子类型和相关函数，例如`void atomic64_inc(atomic64_t *v)`。详情请参阅相应的头文件。

### 11.3 位操作

- 为了检查和修改各种标志位和锁变量中的单个位，内核提供了许多原子操作函数。
- 这些操作通过单条机器指令完成，因此非常快；在大多数平台上，这可以在不中断的情况下完成。
- 理出所料，这些函数根据架构而有所不同。它们定义在`/usr/src/linux/x86/include/asm/bitops.h`中。

```c
#include <asm/bitops.h>
```

```c
void set_bit(int nr, volatile unsigned long *addr);
void clear_bit(int nr, volatile unsigned long *addr);
void change_bit(int nr, volatile unsigned long *addr);
```

```c
int test_bit(int nr, volatile unsigned long *addr);
int test_and_set_bit(int nr, volatile unsigned long *addr);
int test_and_clear_bit(int nr, volatile unsigned long *addr);
int test_and_change_bit(int nr, volatile unsigned long *addr);
```

```c
long find_first_zero_bit(const unsigned long *addr, unsigned long size);
long find_next_zero_bit(const unsigned long *addr, unsigned long size, unsigned long offset);
long find_first_bit(const unsigned long *addr, unsigned long size);
```

```c
unsigned long fff(unsigned long word);
unsigned long ffs(int x);
unsigned long fls(int x);
```

- 在这些函数中，`nr`的类型取决于架构；对于 32 位 x86 和 ARM，它只是一个整数，而`alpha`是`unsigned long`。第二个参数是指要检查或修改的位的变量。其类型随架构而异，通常为`volatile long`。
- 这些函数返回之前的位值作为返回值。
- 注意，`ff()`、`ffs()`和`fls()`分别查找字字整数中的第一个 0 位、第一个置位和最后一个置位，而`find_first_zero_bit()`、`find_next_zero_bit()`和`find_first_bit()`函数在变变长度的掩码上工作。
- 还存在一组非原子位，它们与上述位不同之处在于带有`__set_bit()`前缀。它们可以在锁已获取并确保完整性时使用，且速度比原子版本快得多。

### 11.4 自旋锁

- 自旋锁是一种保护代码临界区的机制。在等待资源可用时它会自旋等待，而不是进入睡眠状态。
- 人可以防止同一代码段在多个 CPU 上执行，但更广泛地说，它还保护了对同一资源的并发访问，这些资源可能被不同的代码路径访问，并且可能在进程上下文中内部或之外。
- 在引入内核抢占之前，自旋锁仅在多处理器系统中是重要的。这是因为 SMP CPU 可以同时访问代码的临界区。因此，在内核抢占被纳入 2.6 内核之前，在单处理器系统上，自旋锁被定义为空操作 no-ops。然而，在可抢占、超线程或多核系统中，自旋锁始终会工作。
