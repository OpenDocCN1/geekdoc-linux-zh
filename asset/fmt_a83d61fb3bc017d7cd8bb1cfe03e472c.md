
* 文件的 `inode`，以便我们能够操作

* 权限、所有权等。 */

};

```c
/* 初始化模块 - 注册 proc 文件 */

int init_module()
{
    /* 将任务放入 tq_timer 任务队列，这样它
    * 将在下次定时器中断时执行 */
    queue_task(&Task, &tq_timer);
    /* 如果 proc_register_dynamic 成功，则成功，
    * 否则失败 */
#if LINUX_VERSION_CODE > KERNEL_VERSION(2,2,0)
    return proc_register(&proc_root, &Out_Proc_File);
#else
    return proc_register_dynamic(&proc_root, &Our_Proc_File);
#endif
}
```

```c
/* 清理 */
void cleanup_module()
{
    /* 注销我们的 /proc 文件 */
    proc_unregister(&proc_root, &Our_Proc_File.low_inode);
    /* 睡眠直到 interrupt_routine 被最后一次
    * 调用。这是必要的，因为否则我们将
    * 释放持有 interrupt_routine 和
    * Task 的内存，而此时 tq_timer 仍在引用它们。
    * 注意，在这里我们不允许信号
    * 中断我们。
    * 既然 WaitQ 现在不为空，这会自动
    * 告诉中断处理程序是时候该退出了。 */
    sleep_on(&WaitQ);
}
```

# 第 11 章

## 中断处理程序

除了最后一章，我们到目前为止在内核中所做的一切工作都是为了响应进程请求而进行的，无论是通过处理特殊文件、发送 `irq` 或发出系统调用。但内核的工作不仅仅是响应进程请求。另一项同样重要的工作是与连接到机器的硬件进行通信。

`CPU` 和硬件之间有两种类型的交互。第一类型是硬件告诉 `CPU` 某些信息。第二类型是 `CPU` 告诉硬件某些信息。

在 `Linux` 中，中断有两种类型：短中断和长。短中断是指执行时间很短的中断，期间其他中断会被阻塞。长中断是指执行时间较长的中断，期间可能会发生其他中断。

实现长中断要困难得多，因为早期的 `Linux` 版本只有一个底半数组，其中一个（`BH_IMMEDIATE`）用于那些没有分配底半的驱动程序。

当 `CPU` 接收到中断时，它会停止当前操作，在栈上保存状态，并调用中断处理程序。只有当该 `IRQ` 上没有处理器或者你愿意共享时，该函数才会成功。

标志可以通过 `SA_SHIRQ` 表示你愿意共享 `IRQ`（通常是因为多个设备位于同一个 `IRQ`），以及 `SA_INTERRUPT` 表示这是一个快速中断。

## Intel 架构上的键盘

警告：本章的剩余部分是 `Intel` 特有的。如果你不是在 `Intel` 平台上运行，它将无法工作。不要尝试编译这些代码。

我在编写本章的示例代码时遇到了一个问题。一方面，为了让示例有用，它必须在每个人的计算机上运行并产生有意义的结果。另一方面，内核已经包含了所有常用设备的驱动程序，这些驱动程序无法与我要编写的内容共存。我找到的解决方案是为键盘中断编写一些，并禁用常规键盘中断处理程序。由于它是作为内核源文件（具体为 `drivers/char/keyboard.c`）中的静态符号定义的，因此可以在另一个终端执行 `sleep 120 ; reboot` 如果你重视你的文件系统。

```c
ex intprpt.c

/* intprpt.c - 一个中断处理程序。 */
/* Copyright (C) 1998 Ori Pomeranz * */

/* 必要的头文件 */
/* 内核模块中的标准 *
#include <linux/kernel.h>  /** 我们正在内核工作 *
#include <linux/module.h>  /** 具体来说，一个模块 *

/* 处理 CONFIG_MODVERSIONS */
#if CONFIG_MODVERSIONS==1
#define MODVERSIONS
#include <linux/modversions.h>
#endif

#include <linux/sched.h>
#include <linux/tqueue.h>

/* 我们想要一个中断 *
#include <linux/interrupt.h>
#include <asm/io.h>

/* 在 2.2.3 中 /usr/include/linux/version.h 包含了
* 此宏，但 2.0.35 没有 - 所以如果需要，我就
*在这里添加它。 *
#ifndef KERNEL_VERSION
#define KERNEL_VERSION(a,b,c) ((a)*65536+(b)*256+(c))
#endif

/* 下半部 (Bottom Half) - 当内核认为
* 安全可以正常执行内核模块允许的所有操作
* 时就会调用它。 */
static void got_char(void *scancode)
{
    printk("Scan Code %x %s.\n",
        (int)((char *)scancode) & 0x7F,
        ((char *)scancode) & 0x80 ? "Released" : "Pressed");
}
```

# 300 Linux 内核模块编程指南：第 11 章

```c
/* 此函数处理键盘中断。它从键盘读取
* 相关信息，然后在内核
* 认为安全时调度下半部进行运行。 */
void irq_handler(int irq,
    void *irq_id,
    struct pt_regs *regs)
```

```c
/* 这些变量是静态的，因为它们需要被
* （通过指针）供下半部
* 例程访问。 */
static unsigned char scancode;
static struct tq_struct task =
    (NULL, 0, got_char, &scancode);
unsigned char status;
```

```c
/* 读取键盘状态 */
status = inb(0x64);
scancode = inb(0x60);
```

```c
/* 调度下半部运行 */
#if LINUX_VERSION_CODE > KERNEL_VERSION(2,2,0)
queue_task(&task, &tq_immediate);
#else
queue_task_irq(&task, &tq_immediate);
#endif
mark_bh(IMMEDIATE_BH);
```

```c
/* 初始化模块 - 注册 IRQ 处理程序 */
int init_module()
{
    /* 由于键盘处理器不会与其他
    * 处理程序（如我们的）共存，我们必须在做任何事之前
    * 禁用它（释放它的 IRQ）。由于我们
    * 不知道它在哪里，没有办法在以后
    * 恢复它 - 所以在我们完成后
    * 必须重启电脑。 */
    free_irq(irq, NULL);
    /* 请求 IRQ 1（键盘 IRQ），将其发送到我们的
    * irq_handler。 */
    return request_irq(
        1,  /* PC 上的键盘 IRQ 编号 */
        irq_handler,   /* 我们的处理器 */
        SA_SHIRQ;
    /* SA_SHIRQ 意味着我们愿意在该 IRQ 上有
    * 其他处理程序。
    *
    * SA_INTERRUPT 可用于将处理器
    * 变成中断。
    */
        "test_keyboard_irq_handler", NULL);
}
```

```c
/* 清理 */
void cleanup_module()
{
    /* 这仅仅是为了完整性。它完全
    * 无关，因为我们没有办法恢复
    * 正常的键盘中断，所以电脑
    * 完全没用且必须重启。 */
    free_irq(1, NULL);
}
```
