
## 模块: rtai

```
#include "rtai.h"
```

### 中断管理

```
void rt_global_cli (void);
void rt_global_sti (void);
```

`rt_global_cli` 强制禁用请求 cpu 上的中断 (`cli`) 并获取调用 cpu 的全局自旋锁，以便任何通过此方法同步的其他 cpu 都被阻塞。

`rt_global_sti` 强制启用调用 cpu 中断 (`sti`) 并释放全局锁。

```
void rt_global_save_flags (unsigned long *flags);
int rt_global_save_flags_and_cli (void);
void rt_global_save_restore_flags (unsigned long flags);
```

`rt_global_save_flags` 将 CPU 中断标志 (`IF`) 和全局锁标志保存到 `flags` 的第 9 位和第 0 位。

### 用于嵌入式和实时应用的 Linux

`rt_global_save_flags_and_cli` 强制禁用请求 CPU 上的中断并返回 CPU 中断标志 (`IF`) 和全局锁标志的旧状态，位于第 9 位和第 0 位。

`rt_global_restore_flags` 根据 `flags` 恢复 CPU 硬中断标志 (`IF`) 和全局锁标志，根据全局位的状态释放或获取全局锁。

```
void send_ipsi_shorthand (unsigned int shorthand, int irq);
void send_ipsi_logical (unsigned long dest, int irq);
```

- `send_ipsi_shorthand` 向以下对象发送 `irq` 处理器间消息：

  * 如果 `shorthand` 等于 `APIC_DEST_ALLINC`，则发送给所有 CPUs

  * 如果 `shorthand` 等于 `APIC_DEST_ALLBUT`，则发送给除自身外的所有 CPUs

  * 如果 `shorthand` 等于 `APIC_DEST_SELF`，则发送给自身。

`send_ipsi_logical` 向 `dest` 定义的所有 CPUs 发送 `irq` 处理器间消息。`dest` 由一个 `unsigned long` 给出，对应于要发送的 CPUs 的位掩码。它用于扁平逻辑模式下的本地 APIC 程序，因此允许的 CPU 最大数量为 8，这个约束适用于 RTAI 的所有函数和数据。在安装 RTAI 时通过调用 `rt_mount_rtai` 设置扁平逻辑模式。

```
int rt_assign_irq_to_cpu(int irq, int cpu);
rt_reset_irq_to_sym_mode(int irq);
```

`rt_assign_irq_to_cpu` 强制将外部中断 `irq` 分配给 `cpu`。

`rt_reset_irq_to_sym_mode` 将中断 `irq` 重置为对称模式。对称模式将 IRQs 分布到所有 CPUs。注意：这些函数适用于多系统。

返回值：如果系统中只有一个 CPU，返回值为 1。如果有两个或更多 CPU，则返回 0 表示成功。如果 `cpu` 指向不存在的 CPU，返回 `-EINVAL`。

### RTAI 应用程序接口 (API)

```
int rt_request_global_irq (unsigned int irq, void (*handler)(void));
int rt_free_global_irq (unsigned int irq);
int rt_request_RTirq (unsigned int irq, void (*handler)(void));
int rt_free_RTirq (unsigned int irq);
```

`rt_request_global_irq` 安装 `handler` 作为 IRQ 级中断服务程序，每当发生中断 `irq` 时就会调用。安装的 `handler` 必须通过调用 `rt_pend_linux_irq` 来激活任何 Linux handler。

`rt_free_global_irq` 卸载中断服务程序。`request_RTirq` 和 `free_RTirq` 是 `rtai.h` 中定义的宏，仅支持与 RT_linux 2.0.35 。它们与另外两个函数完全等效。

返回值：

- 0 - 成功

- `-EINVAL` - `irq` 无效或 `handler` 为 NULL

- `-EBUSY` - 已存在该中断的 `handler`

```
int rt_request_linux_irq (unsigned int irq, void (*handler)(int irq, void *dev_id, struct pt_regs *regs), char *handler, void *dev_id);
int rt_free_linux_irq (unsigned int irq, void *dev_id);
```

`rt_request_linux_irq` 安装 `handler` 作为 IRQ 级服务程序，强制 Linux 与其他 handler 共享 IRQ。`handler` 被附加到相同 IRQ 的现有 Linux handler 并作为 Linux IRQ 运行。通过这种方式，实时应用程序可以监控 Linux 中断。`handler` 出现在 `/proc/interrupts` 中；`handler_id` 是 `/proc/interrupts` 中的名称。`dev_id` 以标准 Linux IRQ 请求的方式传递给中断 handler。中断服务程序可以使用 `rt_free_linux_irq` 卸载。

返回值：

- 0 - 成功

- `-EINVAL` - `irq` 无效或 `handler` 为 NULL

- `-EBUSY` - 已存在该中断的 `handler`

```
void rt_pend_linux_irq (unsigned int irq);
```

以 Linux IRQ 模式（即完全启用中断）挂起 Linux 中断 `irq`。

```
int rt_request_srq (unsigned int label, void (*rtai_handler)(void), long long (*user_srq)(unsigned int));
int rt_free_srq (unsigned int srq);
```

`rt_request_srq`。未提供描述。

`rt_free_srq` 卸载由 `srq` 标识的系统调用。

返回值：

- 0 - 成功

- `-EINVAL` - `rtai_handler` 为 NULL 或 `srq` 无效

- `-EBUSY` - 无可用的 `srq` 槽

```
void rt_pend_linux_srq (unsigned int srq);
```

挂起系统调用 `srq` 作为 Linux 内核的服务请求。`srq` 是 `rt_request_srq` 返回的值

## RTAI 应用程序接口 (API)

### 定器管理

```
void rt_request_timer (void (*handler)(void), int tick, int apic);
void rt_free_timer (void);
```

`rt_request_timer` 请求一个周期为 `tick` 的定时器，并将 `handler` 安装为定时器的中断服务程序。将 `tick` 设置为 0 用于单次模式（oneshot）。如果 `apic` 有非零值，则使用本地 APIC 定器。否则基于 8254。

`rt_free_timer` 卸载之前由 `rt_request_timer` 设置的定时器。

### 初始化

```
void rt_mount_rtai (void);
void rt_umount_rtai (void);
```

`rt_mount_rtai` 初始化实时应用程序接口，即获取由实时硬件抽象层（`struct rt_hal *hal`）指向的任何硬件、数据或服务。

`rt_umount_rtai` 卸载实时应用程序接口，将 Linux 重置为正常状态。

### 诊断

```
int rt_printk (const char *format, ...);
```

`printf()` 的 RTAI 安全版本。

返回值：

- 打印的字符数

## 模块: rtai_sched

`rtai_sched` 是三个可能的调度器之一（`up_sched`, `smp_sched` 或 `mups_sched`）的逻辑链接。除另说明外，三个调度器都支持相同的 API。

### 用于嵌入式和实时应用的 Linux

```
#include rtai_sched.h
```

### 任务函数
