
#include <asm/ir>

#include <linux/interrupt.h>

```c
void disable_irq(int irq);

void disable_irq_nosync(int irq);

void enable_irq(int irq);
```

这些操作在调用时对 CPU 有效；其他处理器继续处理中断。因为内核在调用之前会禁用中断，所以当调用它们时，中断是禁用的。由于内核在调用之前会禁用中断，当调用它们时，中断是禁用的。第一种形式在处理程序中是安全的，第二种形式（`disable_irq_nosync`）。在处理程序执行时，第一种形式是安全的。在资源被持有时禁用/启用中断是重要的。为了保护临界区，应使用这些函数：

```c
unsigned long flags;

spinlock_t lock;

spin_lock_irqsave(&lock, flags);

/* 临界区 */

spin_unlock_irqrestore(&lock, flags);
```

这些函数会导致阻塞。

### 8.4. MSI

PCIe 快速中断是基于线的，被认为是遗留技术。PCIe 通过模拟这种行为来保持向后兼容性，但仅限于四条线。PCI 2.2 标准引入了新机制 MSI（消息中断），并在 PCI 3.0 标准中进一步增强为 MSI-X，与 MSI 兼容。

MSI 设备通过向内存地址写入消息来发送中断。消息值通过总线（FSB）传递中断。该机制不需要确认，且不会产生边触发中断。MSI 每个设备最多可使用 32 个地址和 2048 个独立消息。MSI-X 使用不同的地址和值（与 MSI 不同）。使用消息中断有重要优点：首先，设备不再竞争有限的 IRQ 线；不需要共享。中断延迟也因此减少，并使得行为更具可预测性。

### 8.6. 中断期间不能做的事情

中断不在进程上下文中运行。你无法访问 `task_struct` 的字段，因为这些字段都是未定义的。通常，你访问的是中断服务程序执行时正在运行的内容，这与当前进程没有连接。

任何操作都可能导致内核崩溃，至少阻塞的处理器是这样。特别是你不能直接或间接地使用任何这些函数。如果在尝试分配内存时非法是有害的，因为 GFP 标志不是当前的。如果你必须使用 `GFP_ATOMIC`，它会返回。

你不能由于任何原因调用 `schedule()`，或任何调用调度程序的器的调用，因为所有的睡眠函数都会阻塞。

你不能对信号量执行 `sleep()`，因为它在等待资源时可能会阻塞。但是，你可以执行 `up()` 或任何类型的 `wake_up()`。

你不能使用互斥锁请求锁 `request_lock()`。

你不能在进程地址空间之间传输数据；即 `get_user()`、`put_user()`、`copy_from_user()` 函数有进入睡眠的潜力。此外，因为没有真实的用户上下文。

# 第 8 章：中断与异常

## 8.8. 安装中断处理程序

`lock` 用于防止竞态条件。

如果 IRQ 线是共享的，则 `IRQ_DISABLED` 标志仅对注册到该 IRQ 线的第一个处理程序有效。
`mask` 表示在运行期间哪些中断被阻塞；
指向 `/proc/` 中的中断驱动程序（或内核子系统）。
`dev_id` 指向已注册 IRQ 的设备驱动地址空间中的唯一标识符。这对于确保在发出请求时 cookie（用于共享 IRQ）有效至关重要。设备驱动程序通常指向处理程序可以访问的数据结构。如果 IRQ 不共享，可以使用 `NULL`。
`next` 指向链中共享相同 IRQ 的 `irq` 结构。

`irq` 结构体所示：

```c
2.63.01  03 struct irq {
2.63.01  94     irq_handler_t handler;
2.63.01  96     unsigned long flags;
2.63.01  97     const char *name;
2.63.01  98     void *dev_id;
2.63.01 100     struct irq *next;
2.63.01 101     int irq;
2.63.01 102     struct proc_dir_entry *dir;
2.63.01 103     struct task_struct *thread;
2.63.01 104     struct task_struct *task;
2.63.01 105     unsigned long thread_flags;
```

## 8.8 安装中断处理程序

`handler` 指向由中断触发的中断服务程序（或处理程序）。
我们稍后会解释这些参数。

通常，设备驱动程序不会直接访问我们描述的数据结构。相反，它们必须使用以下函数来安装和卸载中断处理程序：

`flags` 是以下值之一：

```c
#include <linux/interrupt.h>

int request_irq(unsigned int irq, irq_handler_t handler, void *dev,
               unsigned long flags,
               const char *name,
               void *dev_id);

void synchronize_irq(unsigned int irq);

void free_irq(unsigned int irq, void *dev_id);
```
