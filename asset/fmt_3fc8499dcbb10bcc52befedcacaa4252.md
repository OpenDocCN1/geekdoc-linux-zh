
注意，如果 IRQ 线是共享的，则 `IRQ_DISABLED` 标志仅对该 IRQ 上注册的第一个处理程序有效。

`irq` 结构如下：

```c
struct irq_action {
irq_handler_t handler;
unsigned long flags;
cpmask_t mask;
count_dev;
void *dev_id;
struct irq_action *next;
int irq;
struct proc_dir_entry *dir;
irq_handler_t thread_fn;
struct task_struct *thread;
unsigned long flags;
};
```

`name` 指向 `/proc/interrupts` 中的标识符。

`dev_id` 指向设备驱动程序（或内核子系统）地址空间中的唯一标识符。这对于确保在发出请求时，用于共享 IRQ 之间匹配的 Cookie（令牌）不被更改至关重要。驱动程序通常指向一个处理程序运行时可以访问的数据结构。如果 IRQ 不是共享的，可以使用 `NULL`。

`next` 指向共享相同 IRQ 的链中的 `irq_action` 结构。

`handler` 指向在中断发生时触发的中断服务例程（或处理程序）。

`flags` 是以下值之一：

#### 表 3: IRQ 处理程序标志

| 标志 | 含义 |
|---|---|
| `IRQ_DISABLED` | 中断在禁用中断的情况下运行；即它是一个快速处理程序。 |
| `IRQ_SHARED` | 如果所有设备都同意，则 IRQ 可以与其他设备共享。 |
| `IRQ_SAMPLE_RANDOM` | 该线路可能贡献熵池，我们用它来生成用于用途加密的随机数。对于在可预测时间发生的中断不应这样做。 |
| `IRQ_PROBE_SHARED` | 当预期发生不匹配时设置。 |
| `IRQ_TIMER` | 设置以表示这是一个定时器中断处理程序。 |
| `IRQ_NOBALANCING` | 设置将此排除在中断平衡之外。 |
| `IRQ_IRQPO` | 中断用于轮询（出于性能考虑，共享中断中第一个注册的中断才会被考虑） |

通常，驱动程序不会直接访问我们刚才描述的数据结构。相反，它们使用以下函数来安装和卸载中断处理程序：

```c
#include <irq.h>

int request_irq(unsigned int irq,
                irq_handler_t (handler)(unsigned int irq, void *dev_id),
                unsigned long flags,
                const char *dev_name,
                void *dev_id);
void synchronize_irq(unsigned int irq);
void free_irq(unsigned int irq, void *dev_id);
```

我们稍后会讨论这些参数。

`request_irq` 是用于为多个中断安装处理程序的函数。

`handler()` 是要安装的函数。

`flags` 是之前描述的选项位掩码；例如 `IRQ_DISABLED`。当 IRQ 已被注册为非共享时请求共享，可能会产生冗长但无害的消息。

`device` 是 `irqaction` 结构中相同的名称；它标识了 `/proc/interrupts` 中的标识符。

`handler()` 函数有两个参数：

- `irq`：如果只服务于一个 IRQ，则该参数很有用。

- `dev_id` 用于共享中断。

## 8.9. 实验

![](img/5f0cab84232061dba742ffc69894b1f1_61_0.png)

如果没有注册的处理程序为给定的 IRQ 处理 `IRQ_HANDLED`，则假设它已处理且会漏掉警告。注意，中断并没有被消耗；对于给定的 IRQ 线，所有处理程序仍然会被调用，即使其中一个或多个处理程序声称已处理了事件。

- 2.6.19 之前的内核引入了第三个参数，一种类型的数据结构，保存中断之前进程上下文的快。用于调试以及在处理中断后恢复寄存器状态。该结构的精度取决于 CPU；使用 `/usr/src/linux/x86/include/asm/ptrace.h`。

- `pt_irq` 参数在 2.6.19 内核中被移除，因为它在驱动程序中很少使用，且消除了所有栈空间的使用并稍微提升了性能。

- 如果需要访问此结构，可以调用内联函数 `struct irq_action *get_irq(irq)`。

### 实验 1：共享中断

编写一个与网卡共享 IRQ 的模块。你可以通过触发或 `ping` 生成一些网络中断。如果你在网络驱动方面遇到问题，尝试使用某些中断。在模块加载时检查 `/proc/interrupts`。让模块跟踪中断处理程序被调用的次数。

### 实验 2：共享所有中断

扩展之前的解决方案，构造一个与已安装的处理程序共享所有可能的中断的驱动。最大取决于你的内核和平台；查看 `/proc/interrupts` 以了解什么是必要的。调用 `request_irq` 时要特别小心，如果你不小心，很容易冻结你的系统。驱动程序可以是简单的；例如如果指定了 `open()` 和 `release()` 方法，默认是成功的。在设备上的 `read(2)` 应该返回处理中断的数量。`request_irq()` 可以在设备初始化之前或首次使用（`open`）时调用。在调用 `free_irq` 之前，应该调用 `synchronize_irq()` 以确保该 IRQ 的所有处理程序都已完成。中断处理程序返回 `irqreturn_t` 类型。三个可能的返回值为：

#### 表 8.5：IRQ 返回值

| 返回值 | 含义 |
|---|---|
| `IRQ_NONE` | 处理程序未识别事件；即由于某些共享，或者它是意外的 |
| `IRQ_HANDLED` | 处理程序识别了事件且是预期的 |
| `IRQ_RETVAL(x)` | 如果参数非零，则评估为 `IRQ_HANDLED`；否则为 `IRQ_NONE`。 |

# 第 9 章 模块 II：导出、许可与动态加载

![](img/5f0cab84232061dba742ffc69894b1f1_62.png)

我们将看到符号如何从内核导出到模块，从一个模块到另一个模块。我们讨论模块许可。我们将考虑模块的按需加载和卸载。我们将看到使驱动程序成为内核所需的更改，并讨论内核和模块构建的细节。

- 9.1 导出符号 .104
- 9.2 模块许可 .........104
- 9.3 模块的自动加载/卸载 ....106
- 9.4 构建驱动程序 ..............107
- 9.5 内核构建和 `Makefile` ....109
- 9.6 实验 .................110

## 9.1 导出符号

为了让模块可以使用内核代码中的符号，内核必须导出它。如果一个模块具有供之后加载的模块使用的符号，也要导出该符号。这通过使用 `EXPORT_SYMBOL()` 宏来实现：

```c
int my_variable;
int my_export_fun( int my_variable );
EXPORT_SYMBOL(my_variable);
EXPORT_SYMBOL(my_export_fun);
```

注意，如果符号被声明为 `static`，则不会被导出。也可以宏导出符号：

```c
EXPORT_SYMBOL_GPL();
```

这种方法如何使用以及它的影响已经过考虑。这这意味着该符号可以导出到符合 GPL 的模块，例如，它可以在二进制驱动程序中使用。然而，某些符号应该导出到内核内部使用的基本函数模块。还有其他导出符号的方法：

```c
EXPORT_PER_GPL();
EXPORT_GPL_CPU_GPL();
EXPORT_CPU_GPL_FUTURE();
EXPORT_KERNEL_GPL();
```

2.6 系列内核除非声明为 `static`，否则会在模块中导出全局符号；这就是内核中字面上使用 `static` 关键字的原因之一。

注意如果代码被编译为内置二进制，将符号声明为 `static` 仍然意义。通常的规则是除非需要，否则所有符号都应该声明为 `static`。

## 9.2 模块许可

模块可以使用 `MODULE_LICENSE()` 宏进行许可，例如：

```c
MODULE_DESCRIPTION("Does Everything")
MODULE_AUTHOR("Fandels with Handles")
MODULE_LICENSE("GPL v2");
```
