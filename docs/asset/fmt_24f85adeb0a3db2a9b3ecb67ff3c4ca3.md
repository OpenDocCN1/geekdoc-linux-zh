
内核中的位置被称为 `system_call`。该位置的入口检查调用号，调用号告诉内核进程请求的服务。然后，它查看系统调用表（`sys_call_table`）以查看其地址。然后它调用函数，并在返回后进行几次系统检查，然后返回进程（如果进程运行结束，则返回另一个进程）。如果你想读取这段代码，它是 `arch/<architecture>/kernel/entry.S` 文件中 `ENTRY(system_call)` 行之后。

所以，如果我们想更改某个系统调用，我们需要做的是编写我们的函数来实现它（通常通过添加我们自己的代码然后调用原始函数），然后将 `sys_call_table` 的指针指向我们的函数。因为我们可能会被移除，并且我们不想让系统处于不稳定状态，所以 `cleanup_module` 将表恢复到原始状态是非常关重要的。

源代码是此类内核模块的示例。我们想要“监控”某些用户，并在该用户打开文件时打印消息。为此，我们用我们自己的函数 `our_sys_open` 替换打开文件的系统调用。此函数检查当前进程的 `uid`（用户 ID），如果它等于我们监控的 `uid`，它会调用 `print` 显示要打开的文件名。然后，它用相同的参数调用原始的 `open` 函数，以实际打开它。

`init_module` 函数替换了 `sys_call_table` 中适当的位置，并将原始指针保存在变量中。`cleanup_module` 函数使用变量将一切恢复正常。

将 `B` 从循环中切除。然后，当 `B` 被移除时，它会将系统调用恢复到它认为的原始 `Aopen`，而该函数已不再位于内存中。乍一看，我们似乎可以通过检查系统调用是否等于我们的 `open` 函数，并且如果不相等则完全修改（这样 `B` 在被移除时就不会更改系统调用）来解决这个特定问题，但这会导致一个更严重的问题。当 `A` 被移除时，它看到系统调用已被更改为 `Bopen`，因此它不再指向 `Aopen`，所以在它从内存中移除之前，不会将其恢复为 `sysopen`。遗憾的是，`Bopen` 仍然尝试调用已不在[那里]的 `Aopen`，因此即使不移除 `B`，系统也会崩溃。

我想到了两种防止这种问题的方法。第一是将调用恢复到原始值，`sysopen` 并不是 `/proc/ksym` 中内核系统表的一部分，因此我们无法访问它。另一种解决方案是使用引用计数来防止 `root` 在模块加载后通过 `rmmod` 卸载。这对于生产模块是好的，但对于教学示例来说糟糕——这就是为什么我在这里没有这样做。

### syscall.c

```c
/* syscall.c
 *
 * 系统调用“劫持”示例
 */

/* Copyright (C) 1998-99 by Ori Pomerantz */

/* 必要的头文件 */

/* 内核模块中的标准头 */
#include <linux/kernel.h> /* 我们正在进行内核工作 */
#include <linux/module.h> /* 具体来说，一个模块 */

/* 处理 CONFIG_MODVERSIONS */
#if CONFIG_MODVERSIONS=1
#define MODVERSIONS
#include <linux/modversions.h>
#endif

#include <sys/syscall.h> /* 系统调用列表 */

/* 对于当前（进程）结构，我们需要
* 使用此来知道当前用户是谁。 */
#include <linux/sched.h>

/* * 在 2.2.3 的 /usr/include/linux/version.h 中包含
* 用于此的宏，但 2.0.35 没有 - 所以如果有必要
* 我在这里在这里添加它。 */
#ifndef KERNEL_VERSION
#define KERNEL_VERSION(a,b,c) ((a)*65536+(b)*256+(c))
#endif

#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
#include <asm/uaccess.h>
#endif

/* * 系统调用表（函数数组）。我们
* 只将其定义为外部，内核会在
* 被 insmod 时为我们填充它 */
extern void sys_call_table[];

/* * UID - 我们想要监视的 UID - 将从
* 命令行中填充 */
int uid;

#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
MODULE_PARM(uid, "i");
#endif

/* * 指向原始系统调用的指针。我们保留

* 它而不是调用原始函数

* (sys_open)，是因为可能可能在我们

* 之前已经替换了系统调用。注意这

* 并不是 100% 安全的，因为如果另一个模块

* 在在我们之前替换了 sys_open，那么当我们

* 插入时，我们将调用该模块中的函数 - 而

* 它可能会在我们之前被移除。

*

* 另一个原因是我们无法获取 sys_open。

* 它是一个静态变量，所以它没有被导出。 */

asmlinkage int (*original_call)(const char *, int, int);

/* * 出于某些原因，在 2.2.3 中 current->uid 给了我

* 零，而不是真实的用户 ID。我尝试寻找

* 哪里错了，但没短时间内完成，

* 我很懒 - 所以我会使用系统调用来

* 获取 uid，就像那样。

* 出于某些原因，重新编译后

* 问题消失了。 */

asmlinkage int (*getuid_call)();

/* * 我们将替换 sys_open（当调用

* 系统调用时的函数）的函数。

* 精确的原型、参数的数量和

* 类型，原始函数

* (它在 fs/open.c 中)。

* 在理论上，这意味着我们与内核的

* 版本绑定。在实践中，系统

* 调用从不改变（这会破坏

* 并需要重新编译程序，因为

* 调用是内核和

* 之间的接口）。 */

asmlinkage int our_sys_open(const char *filename,
 int flags,
 int mode)
{
    int i = 0;
    char ch;
    /* 检查是否是我们监视的用户 */
    if (uid == getuid_call()) {
        /* getuid_call 是系统调用，
        * 它提供了调用我们的进程 uid。
        /* 调用原始 sys_open - 否则我们会失去
        * 打开文件的能力 */
        return original_call(filename, flags, mode);
    }
    /* 保留原始函数的指针
* original_call，然后将表中的
* 系统调用替换为 our_sys_open */
    original_call = sys_call_table[__NR_open];
    sys_call_table[__NR_open] = our_sys_open;
    /* 为了获取函数的地址，
* 跳转到 sys_call_table[__NR_open]。 */
    printk("Spying on UID:%d\n", uid);
    /* 获取 getuid 的系统调用 */
    getuid_call = sys_call_table[__NR_getuid];
    return 0;
}

/* 清理 - 从 /proc 取消适当的文件 */
void cleanup_module() {
    /* 将系统调用还原为 */
    if (sys_call_table[__NR_open] != our_sys_open) {
        printk("Somebody else played with the");
        printk("open call\n");
        printk("system may be left in");
        printk("an unstable state.\n");
    }
    sys_call_table[__NR_open] = original_call;
}
```

## 第8章

### 阻塞进程
