
| 文件 | 函数 | 行号 |
| --- | --- | --- |
| `process.c` | `<global>` | 170 `void (*cm_idle)(void) = default_idle;` |
| `system.h` | `<global>` | 97 `void default_idle(void);` |
| `process.c` | `<global>` | 90 `extern void default_idle(void);` |
| `process.c` | `<global>` | 71 `(*default_idle)(void) = default_idle;` |
| `system.h` | `<global>` | 194 `void (*default_idle)(void);` |
| `process_m.c` | `<global>` | 62 `void default_idle(void) = default_idle;` |
| `system.h` | `<global>` | 80 `void default_idle(void);` |
| `system.h` | `<global>` | 142 `void default_idle(void);` |

- dos 行，按空格键显示更多 **
- 查找此符号：
- 查找此全局定义：
- 查找调用此函数的函数：
- 查找此文本字符串：
- 修改此文本：
- 查找此模式：
- 查找此文件：
- 查找包含此文件的文件：

图 6-4 Cscope 搜索

Copyright ©Intel Corporation. All rights reserved.

# 190 页 第 6 章 深入研究极客技术

`kernel/watchdog.o`: file format elf64-x86-64

```
Disassembly of section .text:

0000000000000000 <touch_softlock_watchdog>:

    __this_cpu_write(watchdog_touch_ts, get_timestamp(this_cpu));

}

void touch_softlock_watchdog(void)

{

    __this_cpu_write(watchdog_touch_ts, 0);

0:    68 48 67 04 25 00 00  movq $0x0,%gs:0x0

7:    00 00 00 00 00 00      retq

d:    c3              66 90        xchg ax,%ax

0000000000000010 <touch_softlock_watchdog_sync>:

#endif

watchdog lines 1-23/1681 0%
```

图 6.6 反汇编后的内核对象文件

所有权利由 Intel特公司所有。

最后，反汇编后的对象文件如图 6.6 所示。

## 我们现在要做什么？

嗯，你寻找异常 RIP 中列出的函数并标记起始地址。然后将此偏移量加到该数字上，并翻译为指定的行。剩下的工作就是尝试理解到底发生了什么。你将看到列出的一条汇编指令，可能还有一些 C 代码，告诉我们哪里可能出了问题。

这并不容易。事实上，这非常困难。但它是令人兴奋的，而且你可能仍然成功在操作系统中找到 Bug。还有比这更有趣的吗？在上面我们学习了编译和反汇编过程，但并没有真正进行过任何具体的操作。既然我们已经知道了如何编译内核对象并将其剖析成小块，让我们来做一些实际工作吧。

## 中级示例

我们现在将尝试一些更严肃的东西。获取一个会导致内核崩溃的原理证明（PoC）代码，编译它，检查崩溃报告，寻找正确的源文件，执行我们上面提到的整个过程，并尝试阅读后期的中间汇编和 C 代码。当然，我们会胜，因为我们知道在寻找什么，但尽管如此，这是一个很好的练习。

最非平凡的例子是创建一个可以触发 panic（崩溃）的内核模块。在我们让内核 panic 之前，让我们简要概述一下内核模块编程的基础。

## 崩溃分析 (crash) 191 页

## 创建问题内核模块

这个练习迫使我们偏离崩溃分析流程，从内核的角度简要观察 C 语言。我们想要让内核崩溃，所以我们需要内核代码。虽然我们将使用 C 语言，它与日常内容有些不同。内核有它自己的规则。

我们将对内核模块编程进行采样。我们将编写自己的模块和 Makefile，编译该模块并将其插入内核。由于我们的模块写得很糟糕，它会导致内核崩溃。然后，我们将分析崩溃报告。利用报告中获得的信息，我们将尝试弄清楚源代码哪里有问题。

## 第 1 步：内核模块

我们首先编写一些 C 代码。让我们从一个简单且无害的 `hello.c` 开始。在不涉及过多技术的情况下，这里是最基本的模块，包含了 `init` 和 `cleanup` 函数。该模块除了向内核日志设施打印消息外，没有做任何特殊操作。

```
/*
* hello.c - 最简单的内核模块。
*/
#include <linux/module.h>    /* 所有模块都需要 */
#include <linux/kernel.h>    /* KERN_INFO 需要 */
int init_module(void)
{
    printk(KERN_INFO "Hello world.\n");
    /*
    * 非 0 返回值意味着 init_module 失败；无法加载模块。
    */
    return 0;
}
void cleanup_module(void)
{
    printk(KERN_INFO "Goodbye world.\n");
}
```

版权所有 ©Intel Corporation. 所有权利保留。

我们需要编译这个模块，所以我们需要一个 Makefile —— 同样是最基本的示例

```
obj-m += hello.o

all:
    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

版权所有 ©Intel Corporation. 所有权利保留。

现在，运行 `make` 命令

```
make
make -C /lib/modules/3.0.51-0.7.9-default/build M=/usr/src/linux/test modules
make[1]: Entering directory "/usr/src/linux-3.0.51-0.7.9-obj/x86_64/default/"
make -C ../../linux-3.0.51-0.7.9 O=/usr/src/linux-3.0.51-0.7.9-
obj/x86_64/default/.
modules
Building modules, stage 2.
MODPOST 1 modules
make[1]: Leaving directory "/tmp/src/linux-3.0.51-0.7.9-obj/x86_64/default/
```

版权所有 ©Intel Corporation. 所有权利保留。

我们的模块已经编译完成。将其插入内核。这是使用 `insmod` 完成的。然而，在我们这样做之前，可以检查我们的模块并查看它的作用。也许，我们可能会在模块中找到一些信息。使用 `modinfo` 命令：

```
/sbin/modinfo hello.ko
filename: hello.ko
version: 7AC965BA10A1C8B
vermagic: 3.0.51-0.7.9 SMP
```

版权所有 ©Intel Corporation. 所有权利保留。

## 崩溃分析 (crash) 193 页

在这种情况下，没什么特别的。现在，插入它：

```
/sbin/insmod hello.ko
```

如果模块正确加载到内核，你将能够通过 `lsmod` 命令看到它

```
/sbin/lsmod | grep hello
```

注意我们模块的使用计数为 0。这意味着我们可以从内核中卸载它而不会引起问题。通常，内核模块用于各种用途，例如与设备通信。最后，使用 `rmmod` 命令移除模块：

```
/sbin/rmmod hello
```

如果你查看 `/var/log/messages`，你会注意到 Hello 和 Goodbye 消息，它们属于 `init` 和 `cleanup` 函数：

```
Dec 22 14:47 test: [8264] Hello
Dec 22 14:47 test: [8264] Goodbye
Dec 22 14:47 test: [8264] oops: kernel
Dec 22 14:47 test: [8264] taints kernel
Dec 22 14:47 test: [8264] Call
```
