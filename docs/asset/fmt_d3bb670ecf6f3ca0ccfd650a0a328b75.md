
https://www.kernel.org/doc/latest/core-api.html

# 内核中的锁

假设有两个内核线程（kthreads），它们读取共享计数器的值并对其进行递增。可能会发生的情况：其中一个内核线程（我们称之为 kthread1）正在运行，读取共享计数器的值并将其存储在局部变量中，在递增之前，kthread1 被另一个内核线程（我们称之为 kthread2）抢占，kthread2 读取共享计数器的相同值并存储在另一个局部变量中。现在，kthread1 抢占 kthread2 并将其局部变量的值加1，更新计数器值。最后，kthread2 抢占 kthread1，递增共享计数器的值。结果是计数器的值在两个内核线程递增后仅增加了一个单位。这种结果取决于多个任务相对执行时间的重叠被称为**竞态条件**。包含并发问题的代码段被称为**临界区**。特别是 Linux 开始在 SMP 多处理器机器上运行以来，这成为内核设计和实现中的主要问题之一。解决方案是识别这些并发访问发生的情况，并使用锁来确保任何时刻只有一个实例进入临界区。

锁有两种。基本类型是**自旋锁**（在内核源码树的 `include/asm/spinlock.h` 中声明）；它是一种简单的单持有者锁：如果你无法获取自旋锁，请继续尝试（旋转）直到获取为止（这会禁用运行内核的抢占）。自旋锁非常小且快速，可以用于任何地方。

第二类型是**互斥锁**（在内核树的 `include/linux/mutex.h` 中声明）；它类似于自旋锁，但在持有互斥锁时可能会阻塞。如果你无法锁定互斥锁，你的任务将挂起并在互斥锁释放时被唤醒。这意味着在你等待时 CPU 可以执行其他事情。

# 第7章

## 锁与多处理器 CONFIG

对于没有编译 `CONFIG_SMP` 且没有编译 `CONFIG_PREEMPT` 的内核，自旋锁完全不存在。这是一个极佳的设计决策：当没有程序可以同时运行时，没有理由使用锁。

如果内核在没有编译 `CONFIG_SMP` 的情况下但设置了 `CONFIG_PREEMPT`，那么自旋锁只需禁用抢占，这足以防止任何竞态。

## 在中断上下文和进程上下文之间共享自旋锁

进程可能会睡眠，但你必须遵守一些规则才能安全地睡眠。这些规则中的第一条是：永远不要在原子上下运行时睡眠。如果你禁用了中断，也不能睡眠。在持有信号量时睡眠是合法的，但在唤醒时，你应该检查执行该操作的代码。如果代码在持有信号量时睡眠，任何等待它的线程也会睡眠。关于睡眠的另一个要点是，当你唤醒时，你永远不知道你的进程离开了 CPU 多久，或者在此期间发生了什么变化。你也不知道另一个进程是否可能由于同一个事件睡眠。另一个相关点是，除非确保有人唤醒你，否则进程无法睡眠。执行唤醒的代码也必须找到你的进程。这是通过一个名为等待队列的数据结构实现的。等待队列是等待特定事件的进程列表。在 Linux 中，等待队列用于等待当特定条件为真时有人唤醒你。你需要一个类型为 `wait_queue_head_t` 的结构。你可以静态地定义并初始化等待队列：

```
DECLARE_WAIT_QUEUE_HEAD(name);
```

或者动态地：

```c
wait_queue_head_t my_queue;
init_wait_queue(&my_queue);
```

`wait_event(wq, condition)` 宏（若干变体）会将进程睡眠（`TASK_UNINTERRUPTIBLE`），直到条件为真。每当队列被唤醒时，都会检查条件。以下是 `wait_event` 宏的不同变体：

```c
wait_event(queue, condition);
wait_event_interruptible(queue, condition);
wait_event_timeout(queue, condition, timeout);
wait_event_interruptible_timeout(queue, condition, timeout);
```

之前的所有函数都共享 `queue` 参数。`condition` 参数将在睡眠前后由宏进行求值；除非条件求值结果为真值，否则进程将继续睡眠。如果你使用 `wait_event`，你的进程将进入不可中断睡眠。首选的替代方案是 `wait_event_interruptible`，它可以被信号中断。超时版本（`wait_event_timeout` 和 `wait_event_interruptible_timeout`）会等待有限的时间；在该时间段（以 `jiffies` 为单位）过期后，无论条件求值结果如何，宏都将返回零。

另一个不同的进程或中断处理程序将唤醒处于睡眠的进程。`wake_up()` 函数会唤醒使用相同条件变量进入睡眠的进程。此函数不会阻塞，并且可以从中断处理程序中调用。你可以看到下面它的两种形式之一：

```
void wake_up(wait_queue_head_t *queue); /* wake_up 唤醒所有等待给定队列的进程 */
```

```
void wake_up_interruptible(wait_queue_head_t *queue); /* 仅限制执行不可中断睡眠的进程 */
```

## LAB 7.2: "sleeping device"模块

在 LAB 7.2 中，你将开发一个内核模块，该模块会导致进程睡眠，并通过中断唤醒它。你可以从下面的图中看到驱动程序的行为。当用户应用程序尝试从设备读取（系统调用）时，进程将进入睡眠。每当你按下或释放按钮时，生成的中断都会唤醒该进程，驱动的 read 回调函数将向用户空间发送设置的中断类型（按下 Press 或释放 Release）。一旦你退出用户应用程序，你就可以从文件中读取所有生成的中断。

![](img/eebd1e8dc8b2bd72a2e142ef70e7c33_231_0.png)

你将保持与之前的 LAB 7.1 相同的硬件硬件配置。

## LAB 7.2 设备树描述

### 设备驱动程序中的中断处理（等待，检查结构）

GPIO23 引脚将在 DT 中复用为 GPIO 输入，并启用内部拉低。将产生两个中断：第一个在按下按钮时产生，第二个在释放时产生。你必须在中断属性中设置 `IRQ_TYPE_EDGE_BOTH`。

### 设备驱动程序中的中断处理

打开并修改 `bcm2710-rpi-3-b.dts` 设备树文件，添加以下加粗代码：

```
&gpio {
    spi0_pins: spi0_pins {
        brcm,pins = <9 10 11>;
        brcm,function = <4>; /* alt0 */
    };
};
[...]
```

```
key_pin: key_pin {
    brcm,pins = <23>;
    brcm,function = <0>; /* Input */
    brcm,puil = <1>; /* Pull down */
};
;
```

```
&soc {
    virtgpio: virtgpio {
        compatible = "brcm,bcm2835-virtgpio";
        gpio-controller {
            #gpio-cells = <2>;
            firmware = <&firmware>;
            status = "okay";
        }
    };
[...]
```

```
int_key_wait {
    compatible = "arrow,intkeywait";
    pinctrl-names = "default";
    pinctrl-0 = <&key_pin>;
    pios = <&gpio 23 0>;
    interrupts = <23 IRQ_TYPE_EDGE_BOTH>;
    interrupt-parent = <&gpio>;
};
;
```

## LAB 7.2 "sleeping device"模块代码描述

现在将描述驱动程序的主要代码部分：

1. 包含函数头：

```c
#include <linux/module.h>
#include <linux/fs.h>
#include <linux/platform_device.h>
#include <linux/of_gpio.h>
#include <linux/of_irq.h>
#include <linux/uaccess.h>
#include <linux/interrupt.h>
#include <linux/misdevice.h>
```
