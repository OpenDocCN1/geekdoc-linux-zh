
### 强制屏障

为了在全系统层级强制内存一致性，你可以使用强制屏障（mandatory barriers）。这在与外部内存映射外设通信时最常见。内核强制屏障保证至少能扩展为通用屏障，而这与目标架构无关。

Linux 内核有三种强制 CPU 屏障：

- **GENERAL `mb()`**: 一个全系统屏障。指令流中 `mb()` 之前的所有内存操作将在 `mb()` 之后的任何操作之前提交。这种排序对系统中的所有总线主都是可见的。它还将确保来自单个处理器的访问到达从设备的顺序。
- **WRITE `wmb()`**: 类似于 `mb()`，但只保证读访问之间的排序：`rmb()` 之前的所有读操作将在 `rmb()` 之后的任何操作之前提交。
- **READ `rmb()`**: 类似于 `mb()`，但只保证写访问之间的排序：`wmb()` 之前的所有写操作将在 `wmb()` 之后的任何操作之前提交。[6]。

对于 Arm Arch64 架构，这些屏障在 `arm64/include/asm/barrier.h` 中实现，与其在 `arm/include/asm/barrier.h` 中实现的 `dsb()` 宏如下：

Listing 7.3.10: Arm 实现的内核内存屏障 (1)

```
1 #define mb() dsb(sy)
2 #define rmb() dsb(ld)
3 #define wmb() dsb(st)
```

而在 `arm/include/asm/barrier.h` 中实现的 `dsb()` 宏如下：

Listing 7.3.11: Arm 实现的内核内存屏障 (2)

```
1 #define isb(option) asm__volatile__("isb" #option : : "memory")

2 #define dsb(option) asm__volatile__("dsb" #option : : "memory")

3 #define dmb(option) asm__volatile__("dmb" #option : : "memory")
```

`DMB`、`DSB` 和 `ISB` 分别是数据内存屏障（Data Memory Barrier）、数据同步屏障（Data Synchronization Barrier）和指令同步屏障（Instruction Synchronization Barrier）[7]。特别是 `DSB`，充当了一种特殊的内存屏障。程序顺序中在该指令之后的任何指令在在该指令完成之前都不会执行。当在该指令之前的所有显内存访问都完成（并且在该指令之前的所有缓存、分支预测器和 TLB 维护操作都完成）时，`DSB` 指令完成。

参数 `SY` 表示全系统 `DSB` 操作；`LD` 是仅等待加载完成的 `DSB` 操作，`ST` 是等待存储完成的 `DSB` 操作。

### SMP 条件屏障

SMP 条件屏障用于确保缓存一致 SMP 系统内不同核心之间的内存视图。在编译未定义 `CONFIG_SMP` 的内核时，SMP 屏障被转换为普通屏障。

内核有三种 SMP 条件 CPU 内存屏障：

- **GENERAL `mb()`**: 类似于 `mb()`，但只保证 SMP 系统内不同核心之间的排序。`mb()` 之前的所有内存操作对于 SMP 系统内 `mb()` 之后的任何操作都是可见的。
- **WRITE `wmb()`**: 类似于 `mb()`，但只保证读访问之间的排序。
- **READ `rmb()`**: 类似于 `mb()`，但只保证写访问之间的排序。

SMP 屏障在 `include/asm-generic/barrier.h` 中实现如下：

Listing 7.13.12: Linux 内核 屏障

```
1 #ifdef CONFIG_SMP

2 #ifndef smp_mb

3 #define smp_mb() __smp_mb()

4 #endif

5 #ifndef smp_rmb

6 #define smp_rmb() __smp_rmb()

7 #endif

8 #ifndef smp_wmb

9 #define smp_wmb() __smp_wmb()

10 #endif

11 #endif
```

## 树莓派上的 Linux 操作系统基础

对于 Arm A64 架构，SMP 屏障在 `arm64/include/asm/barrier.h` 中实现如下：

Listing 7.13.13: Arm 实现的内核 SMP 屏障

```c
1 #define __smp_mb() dmb(ish)
2 #define __smp_rmb() dmb(ishld)
3 #define __smp_wmb() dmb(ish)
```

使用上述定义的 `dmb()` 内存。`DMB` 是数据内存屏障。它确保程序顺序之前的显式内存访问在 `RMB` 指令之后的显式内存访问之前被观察。它不影响处理器上执行的其他指令的排序。

参数 `ISH` 将 `SMB` 操作限制在内部共享域；`ISHLD` 是仅等待加载完成的 `RMB` 操作，并限制在内部共享域；`ISHST` 是等待存储完成的 `DMB` 操作，并限制在内部共享域。回想，“内部共享域”在实践中硬件内存空间（由 Linux 内核控制的 SMP 系统）。

### 隐式屏障

除了显式屏障，可以使用内核中的锁定构造作为隐式 SMP 屏障（类似于用户空间的 `pthread` 同步操作，见第 7.3.6 节）。由于实际上大量的设备驱动程序没有使用所需的屏障，Arm 架构的内核 I/O 访问器（`readb()`, `iowrite32()` 等）在内核带有 `CONFIG_ARM_DMA_MEM_BUFFERABLE` 时作为显式内存屏障，例如在 `arm/include/asm/io.h` 中：

Listing 7.13.14: 作为显式内存屏障的 Arm 内核 I/O 访问器

```c
1 #ifdef CONFIG_ARM_DMA_MEM_BUFFERABLE

2 #include <barrier.h>

3 #define __iormb() rmb()

4 #define __iowmb() wmb()

5 #else

6 #define __iormb() do {} while (0)

7 #define __iowmb() do {} while (0)

8 #endif
```

（Linux 内核代码使用 `do { } while (0)` 作为架构无关的空操作）。

# 第 7 章 | 并发与并行

## 自旋锁 (Spin locks)

自旋锁是最简单的锁形式。本质上，尝试获取锁的任务会进入循环并什么都不做，直到获取锁为止，其伪代码如下：

Listing 7.3.15 自旋锁伪代码

```
while (! has_lock ) {
  // 尝试获取锁
}
```

自旋锁有一个明显的缺点是在等待期间会占用 CPU。如果等待时间很长，另一个尝试获取锁的任务应该进入睡眠。然而，对于不希望让任务睡眠的情况，或者用户知道等待时间很短时，内核提供了自旋锁，也称为忙等锁（`kernel/locking/spin.c`）。

SMP 系统的自旋锁功能通过一个宏实现，该宏为给定的操作（读或写）创建一个锁。本质上，该实现是一个带有条件退出的无限循环。首先，禁用抢占，然后函数尝试原子性地获取锁，如果成功则退出；否则，重新启用抢占并调用与架构相关的 `relax` 函数，这实际上是执行空操作（no-op）的高效方式），然后执行循环的下一次迭代并重试。

Listing 7.3.16: Linux SMP 锁构建宏

```
#define BUILD_LOCK_OPS(op, locktype)
void __lockfunc__raw_op##_lock(locktype)_t *lock)
for ();
  preempt_disable();
  if (likely(do_raw__op##_trylock(lock))
    break;
  preempt_enable();
  arch__op##_relax(lock->raw_lock);
}
```

对于单处理器系统（`include/linux/spin_lock_api.h`），自旋锁要简单得多：

Listing 7.3.17: Linux 内核单处理器自旋锁

```
#define LOCK(lock) \
do { __acquire(lock); (void)(lock); } while (0)
#define LOCK(lock) \
do { preempt_disable(); __LOCK(lock); } while (0)
//...
#define raw_spin_lock(lock) __LOCK(lock)
```

换句话说，代码只禁用了抢占；并没有实际的自旋锁。对锁变量的引用仅是为了抑制编译器警告。

## Futex

如第 7.3.3 节所讨论的那样，互斥锁（`mutex`）是一个二值信号量。`Futex` 是一种“快速用户空间互斥锁”，是 Linux 特有的互斥锁实现，在没有资源争用的情况下对性能进行了优化。
