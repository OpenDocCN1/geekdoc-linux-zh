
# Linux 内核破解不靠谱指南

作者 Paul Rusty Russell

## 第 1 章 引言

亲爱的读者，欢迎阅读 Rusty 的《Linux 内核破解不靠谱指南》。本文描述了内核代码的常见例程和通用要求：它的目标是为经验 C 语言程序员提供 Linux 内核开发的入门。我避开了实现细节：那是代码要做的，我忽略了整大部分有用的例程。

在阅读之前，请理解我从未想过写这份文档，因为我的资质远远不够，但我一直想读，而这是唯一的办法。我希望它能成为最佳实践、常见起点和随机信息的汇编。

## 第 2 章 参与者

在任何时刻，系统中的每个 CPU 都可能处于以下状态：

- 未与任何进程关联，正在处理硬件中断；
- 未与任何进程关联，正在处理 softirq、tasklet 或 bh（下半部）；
- 在内核空间运行，与某个进程关联；
- 在用户空间运行一个进程。

这些状态之间存在严格的顺序：除了最后一类（用户空间）外，每一种状态只能被上面的状态抢占。例如，当一个 softirq 在 CPU 上运行时，没有其他 softirq 会抢占它，但硬件中断可以。然而，系统中的任何其他 CPU 都是独立执行的。

我们将看到用户上下文阻塞中断的方法，从而变得真正的不可抢占。

### 2.1 用户上下文

用户上下文是你通过系统调用或其他陷阱（trap）进入时：你可以睡眠，并且你拥有 CPU（中断外），直到你调用 `schedule()`。换句话说，用户上下文（与用户空间不同）是不可抢占的。

> **注意**：在模块加载、卸载以及对块设备层进行操作时，你始终处于用户上下文。

### 2.2 硬件中断（硬中断）

时钟滴答、网卡和键盘是随时可能产生中断的真实硬件示例。内核运行处理程序来服务硬件。内核保证该处理程序绝不会重入：如果另一个中断到达，它会被排队（或丢弃）。因为它禁用了中断，所以这个处理程序必须非常快：它通常只是确认中断，标记一个待执行的“软件中断”并退出。

你可以判断自己是否正处于硬件中断中，因为 `in_irq()` 返回 `true`。

> **警告**：注意，如果你禁用了中断或下半部（见下文），`in_interrupt()` 将返回虚假真值。

> **警告**：注意，如果禁用了中断（见下文），这将返回虚假真值。

### 2.3 软件中断上下文：下半部、Tasklets、softirqs

每当系统调用即将返回用户空间，或者硬件中断处理程序退出时，任何被标记为等待（通常由硬件中断引起）的“软件中断”都会运行（内核/softirq）。

许多真实的中断处理工作在这里完成。在向 SMP（对称多处理）过渡的早期，只有“下半部”（BHs），它们无法利用多个 CPU。

在我们切换到由火柴和绳结制成的发条式计算机后不久，我们放弃了这种限制。

```
include/linux/interrupt.h 列出了不同的 BH（下半部）。无论你有多少个 CPU，没有两个 BH 会同时运行。这使得向 SMP 的过渡变得更简单，但对于可扩展性能来说非常困难。一个非常重要的下半部是定时器 BH (include/linux/timer.h)；你可以注册它以便在给定的时间内为你执行所有函数。
```

2.33 版本引入了 softirqs（软中断），并在底层重新实现了底座的（现已废弃的）BH。Softirqs 是 BH 的全 SMP 版本：它们可以根据需要同时在任意数量的 CPU 上运行。这意味着需要使用自己的锁来处理共享数据中的竞态。使用位掩码（bitmask）来跟踪哪些已启用，因此 32 个可用的 softirqs 不应轻率使用。（是的，人们会注意到的）。

tasklets (include/linux/interrupt.h) 类似于 softirqs，区别在于它们是动态分配的（意味着你可以创建任意数量的），而且它们还保证任何 tasklet 在任何时间只会运行在一个 CPU 上，尽管不同的 tasklet 可以同时运行（与不同的 BH 不同）。

> **注意事项**：'tasklet' 这个名字具有误导性：它们与 'tasks'（任务）毫无关系，可能更多与 Alexey Kuznetsov 当时喝的某些廉价伏特酒有关。

你可以通过使用 `in_softirq()` 宏 (include/asm/softirq.h) 来判断你是否处于 softirq（或下半部、或 tasklet）中。

> **注意事项**：注意，如果持有 bh 锁（见下文），这将将返回一个假阳性结果。

## 第 3 章 一些基本规则

### 无内存保护

如果你损坏了内存，无论是在用户上下文中还是中断上下文中，整个机器都会崩溃。你确定不能在用户空间中完成你想做的事情吗？

### 无浮点运算或 MMX

FPU 上文不会被保存；即使在用户上下文中，FPU 状态可能也不会与当前进程对应：你会破坏某些用户进程的 FPU 状态。如果你真的想这样做，你必须显式地保存/恢复完整的 FPU 状态（避免上下文切换）。这通常是一个坏主意；先使用定点算术。

### 严格的栈空间限制

内核栈在 2.2 版本中约为 6K（对于大多数架构：在 Alpha 上约为 14K），并与中断共享，因此你不能全部使用它。避免在栈上使用深度递归和巨大的局部数组（改用动态分配分配它们）。

### Linux 内核是可移植的

让我们保持现状。你的代码应该是 64 位纯净的，并且与字节序无关。你还应该减少 CPU 特有的内容，例如，内联汇编应该被干净地封装并最小化以便于移植。通常它应该被限制在内核树中依赖架构的部分。

## 第 4 章 iols：不要编写新的系统调用

系统调用通常看起来如下：

```
asmlinkage int sys_mycall(int arg)
{
    return 0;
}
```

首先，在大多数情况下，你不想创建一个新的系统调用。你可以创建一个字符设备并为它实现相应的 ioctl。这比系统调用灵活得多，系统调用不需要在每个架构的 `include/asm/unistd.h` 和 `arch/kernel/entry.S` 文件中进入，并且更容易被 Linux 接受。

如果你所有的常规工作只是读取或写入某些参数，考虑实现一个 sysctl 接口。

在 ioctl 内部，你处于一个进程的用户上下文中。当发生错误时，你返回一个负的 errno（见 include/linux/errno.h），否则返回 0。

在你睡眠后，你应该检查是否发生了信号：Unix/Linux 处理信号的方法是带上 `-RESTARTSYS` 错误临时退出系统调用。系统调用入口代码将切换到用户上下文中，执行信号处理程序，然后你的系统调用将重启（除非用户禁用了它）。因此，你应该准备好重启工作，例如，如果你正在操作某些数据结构的中间。

```
if (signal_pending())
    return -ERESTARTSYS;
```

如果你在进行较长时间的计算：先考虑用户空间。如果你真的想在内核中执行，你应该定期检查是否需要放弃 CPU（记住每个 CPU 都有协作式多任务）。惯用法是：

```
if (current->need_resched)
    schedule(); /* 将睡眠 */
```

关于接口设计的简短说明：Unix 系统调用的格言是“提供机制而非策略”。

## 第 5 章 死锁配方

你不能调用任何可能睡眠的程序，除非：

- 你处于用户上下文中。
- 你没有持有任何旋锁（spinlock）。
- 你启用了中断（实际上，Andi Kleen 说调度代码会为你启用它们，但那可能不是你想要的）。

注意某些函数可能会隐式睡眠：常见的有用户空间访问函数（*_user）和没有带 `GFP_ATOMIC` 的内存分配函数。

如果你违反这些规则，最终会导致你的机器死机。

真的。

## 第 6 章 常用程序

### 6.1 printk() include/linux/kernel.h

`printk()` 将内核消息传递到控制台、dmesg 和 syslog 守护进程。对于调试和报告错误很有用，可以在中断上下文中使用，但要谨慎使用：控制台被 printk 消息淹没的机器是无法使用的。它使用主要与 ANSI C 兼容的格式字符串，并使用 C 字符串拼接来提供第一个“优先级”参数：

```
printk(KERN_INFO "i = %u\n", i);
```

include/linux/kernel.h；用于其他 KERN_ 值；这些值被 syslog 解释为级别。特殊情况：打印 IP 地址时使用

```
__u32 ipaddress;
printk(KERN_INFO "my ip: %d.%d.%d.%d\n", NIPQUAD(ipaddress));
```

`printk()` 内部使用 1K 缓冲区且不捕获溢出。确保你的缓冲区足够。

> **注意**：当你开始在用户程序中将 printf 写为 printk 时，你就知道自己是一个真正的内核黑客了 :)

> **注意**：另一个旁题外话：原始 Unix 第 6 版源代码在其 printf 函数顶部有一条注释：“Printf 不应用于闲聊”。你应该遵循那条建议。

### 6.2 copy_[to/from]_user() / get_user() / put_user() include/asm/uaccess.h

[睡眠]

`put_user()` 和 `get_user()` 用于从用户空间获取放入单个值（如 int、char 或 long）。指向用户空间的指针绝不应简单解引用；数据应该使用这些程序进行拷贝。两者都返回 -EFAULT 或 0。

`copy_to_user()` 和 `copy_from_user()` 更通用：它们在用户空间与之间拷贝任意数量的数据。

> **注意**：与 `put_user()` 和 `get_user()` 不同，它们返回未拷贝的数据量（即 0 仍意味着成功）。

是的，愚蠢接口让我作呕。请提交一个补丁并成为我的英雄。

这些函数可能会隐式睡眠。这不应在用户上下文之外、禁用中断或持有旋锁时调用。

### 6.3 kmalloc()/kfree() include/linux/slab.h

[可能会睡眠]：见下文

这些程序用于动态分配对齐的内存块，用户空间的 malloc 和 free，但 `kmalloc()` 取一个额外的标志字。重要值：

- `GFP_KERNEL`：可能会睡眠并交换内存。仅允许在用户环境中，但它是分配内存最可靠的方法。
- `GFP_ATOMIC`：不睡眠。比 `GFP_KERNEL` 不可靠，但可以在中断环境中调用。你应该有一个良好的内存错误处理策略。
- `GFP_DMA`：分配低于 16MB 的 ISA。如果你不知道那是什么，就不需要它。非常不可靠。

如果你看到 `kmmem_grow`；从 int 非原子地调用内存分配函数 `GFP_atomic` 警告。你应该修复它。运行，不要走。

如果你分配至少 `PAGE_SIZE` (include/asm/page.h) 字节，考虑使用 `get_free_pages()` (include/linux/mm.h)。它接受一个阶数参数（0 代表页，1 双页，2 四页等）和相同的内存优先级标志。

如果你分配超过一页的字节可以使用 `valloc()`。它会在内核映射中分配虚拟内存。此块在物理内存中是不连续的，通过 MMU 让它看起来是连续的（所以它对 CPU 是连续的，但对外部设备驱动不是）。如果你确实为某些特殊设备需要巨大的物理连续内存，你就有问题了：Linux 对此支持良好，因为运行内核中的某些碎片化很难。最好的方法是在启动早期通过 `alloc_bootmem()` 分配该块。

在使用 slab cache 发明你自己的经常使用对象的缓存之前。

### 6.4 current include/asm/current.h

这个全局变量（实际上是一个宏）包含指向当前任务实例的指针，因此仅在用户上下文中有效。例如，当进程执行系统调用时，它将指向调用进程的任务结构。在中断上下文中它不是 NULL。

### 6.5 udelay()/mdelay() include/asm/delay.h

include/linux/delay.h

`udelay()` 函数用于短时间暂停。不要对 `mdelay()` 使用大值，否则会有溢出风险——在这里辅助函数 `mdelay()` 很有用，甚至可以考虑 `schedule_timeout()`。

### 6.6 local_irq_save()/local_irq_restore() include/asm/system.h

这些例程在本地 CPU 上禁用硬中断并恢复它们。它们是重入的；通过其唯一的 `unsigned long` 类型的标志参数保存之前的状态。如果你知道中断已开启，可以简单使用 `local_irq_disable()` 和 `local_irq_enable()`。

### 6.7 local_bh_disable()/local_bh_enable() include/asm/softirq

这些例程在本地 CPU 上禁用软中断并恢复它们。它们是重入的；如果之前禁用了软中断，那么在调用这一对函数后它们仍然将处于禁用状态。它们防止软中断、tasklets 和下半部（bottom halves）在当前 CPU 上运行。

### 6.8 smp_processor_id()/cpu_[number/logical]_map() include/asm/smp.h

`smp_processor_id()` 返回当前的处理器编号，介于 0 到 `NR_CPUS`（Linux 支持的最大 CPU 数量，为 32）。这些值并不一定连续的：要获取于 0 到 `smp_num_cpus()`（该机器上实际处理器的数量）之间的数字，使用 `cpu_number_map()` 函数将处理器 ID 映射到逻辑数字。`cpu_logical_map()` 执行相反操作。

### 6.9 __init/__exit/__initdata include/linux/init.h

启动后，内核会释放一个特殊区域；标记为 `__init` 的函数和标记为 `__initdata` 的数据结构在启动完成后会被丢弃（在模块内部，该指令目前被忽略）。`__exit` 用于声明一个仅在退出时需要的函数：如果此文件没有被编译为模块，则该函数会被丢弃。用法请参见头文件。注意，将标记为 `__init` 的函数通过 `EXPORT_SYMBOL()` 导出到模块是没有意义的——这会破坏程序。

标记为 `__initdata` 的静态数据结构必须初始化（与在 BSS 段中清零普通静态数据相反）。

### 6.10 __initcall()/module_init include/linux/init.h

内核许多部分作为模块（内核的动态加载部分）运行得很好。使用 `module_init()` 和 `module_exit()` 宏，可以很容易编写不带 `#ifdef` 的代码，这些代码可以作为模块运行，也可以编译到内核中。

`module_init()` 宏定义了在模块插入时（如果文件被编译为模块）或在启动时调用的函数：如果文件没有被编译为模块，`module_init()` 宏等同于 `__initcall()`，后者通过链接器的“魔法”确保函数在启动时被调用。

该函数可以返回一个负错误以导致模块加载失败（遗憾的是，如果模块被编译进内核，则没有影响）。对于模块来说，这在用户上下文中使用的，此时中断已开启且持有了内核，因此它可以睡眠。

### 6.11 module_exit() include/linux/init.h

此宏定义了在模块移除时调用的函数（如果文件被编译进内核，则永远不会调用）。只有当模块的使用计数达到零时，才会被调用。此函数也可以睡眠，但不能失败：在返回之前，一切都必须清理完毕。

### 6.12 MOD_INC_USE_COUNT/MOD_DEC_USE_COUNT include/linux/module.h

这些操作处理模块的使用计数，以防止移除（如果另一个模块使用了它导出的符号，该模块也无法被移除：见下文）。用户上下文对模块的每次引用都应该在函数睡眠之前反映在该计数器中（例如对于每个数据结构或套字）。引用 Tim Waugh 的：

```c
/* 这是糟糕的做法 */
foo_open (...)
{
	stuff.
	if (fail)
		return -EBUSY;
	sleep.. (可能在此处被卸载)
	stuff.
	MOD_INC_USE_COUNT;

	return 0;
}
```

```c
/* 这是良好的做法 */
foo_open(...)
{
  MOD_INC_USE_COUNT;
  stuff.
  if (fail) {
    MOD_DEC_USE_COUNT;
    return -EBUSY;
  }
  sleep.. (现在安全了)
  stuff..
  return 0;
}
```

你通常可以通过使用 `file_operations` 结构体的 `owner` 字段来避免处理这些问题。将此字段置为宏 `THIS_MODULE`。

对于更复杂的模块卸载锁需求，你可以将 `can_unload` 函数指针设置为你自己的例程，如果模块可以卸载，则返回 0，否则返回 `-EBUSY`。

## 第 7 章 等待队列

### 7.1 声明

你使用 `DECLARE_WAIT_QUEUE_HEAD()` 宏，或者在初始化代码中使用 `init_waitqueue_head()` 例程来声明 `wait_queue_head_t`。

### 7.2 入队

将自己放入等待队列相当复杂，因为你必须在检查条件之前把自己放入队列。有一个宏可以做到：`wait_event_interruptible()` include/linux/sched.h。第一个参数是等待队列头，第二个参数是要求值的表达式；当表达式为真时宏返回 0，如果接收到信号则返回 `-RESTARTSYS`。`wait_event()` 版本忽略信号。



不要使用`sleep_on()`函数——很容易意外引入竞态；几乎确定可以使用`wait_event()`系列中的某一个，或者围绕`schedule_timeout()`使用循环。如果你选择围绕`schedule_timeout()`使用循环，记住你必须在每次迭代中设置任务状态（使用`set_current_state()`）以避免忙轮。

## 7.3. 唤醒队列中的任务

调用`wake_up()` `include/linux/sched.h`，它将唤醒队列中的每个进程。异常是如果设置了`TASK_EXCLUSIVE`，在这种情况下队列的剩余部分不会被唤醒。

## 第 8 章 原子操作

某些操作在所有平台上都保证原子性。第一类操作作用于`atomic_t` `include/asm/atomic.h`；它包含一个带符号整数（至少 24 位），你必须使用这些函数来操作或读取`atomic_t`变量。`atomic_read()`和`atomic_set()`获取和设置计数器，`atomic_add()`、`atomic_sub()`、`atomic_inc()`、`atomic_dec()`以及`atomic_dec_and_test()`（减到零时返回真）。

是的。如果原子变量为零，它返回真（i != 0）。

注意这些函数比普通算术慢，不应不必要使用。在某些平台上它们慢得多，例如 32 位的 Sparc 上使用自旋锁。

第二类原子操作是对`long`的原子操作，定义在`include/asm/bitops.h`中。这些操作通常接受位模式的指针和一个位索引：0 是最低位。`set_bit()`、`clear_bit()`和`change_bit()`分别设置、清除和翻转给定的位。`test_and_set_bit()`、`test_and_clear_bit()`和`test_and_change_bit()`执行相同的操作，只是如果位之前被设置过则返回真；这些对于简单的锁非常有用。

可以使用大于`BITS_PER_LONG`的位调用这些操作。但在大端序平台上，结果行为很奇怪，因此最好不要这样做。

注意位顺序取决于架构，特别是传递给这些操作的位域必须至少与`long`一大。

## 第 9 章 符号

在内核内部，适用标准的链接规则（即：除非符号使用`static`关键字声明为文件作用域，否则可以在内核任何地方使用）。然而，对于模块，有一个特殊的导出符号表限制了进入内核的入口点。模块也可以导出符号。

## 9.1. EXPORT_SYMBOL() include/linux/module.h

这是导出符号的经典方法，适用于模块和非模块。在内核中，所有这些声明通常封装在一个文件中以帮助`gensyms`（它搜索源文件的这些声明）。见下文关于`gensyms`和 Makefile 的注释。

## 9.2. EXPORT_SYMTAB

为了方便，模块通常导出所有非文件作用域的符号（即所有未声明为`static`的符号）。如果在包含`include/linux/module.h`之前定义此宏，则只有显式通过`EXPORT_SYMBOL()`导出的符号会被导出。

# 第 10 章. 例程与约定

## 10.1. 双向链表 include/linux/list.h

内核头文件中有三组链表例程，但这一组似乎占了优势（Linux 一直在使用它）。如果你对单向链表没有特定的迫切需求，这是一个很好的选择。事实上，我不在乎它是否是一个好选择，直接用它就好，这样我们就可以删掉其他的。

## 10.2. 返回约定

对于在用户上下文中调用的代码，违反 C 语言惯例是非常常见的：返回 0 表示成功，返回一个负错误码（例如失败时返回`-EFFAULT`）。这在初看起来可能不符合直觉，但在网络代码中非常广泛。例如，文件系统代码使用`ERR_PTR()`（`include/linux/fs.h`）将负错误码编码为指针，并使用`IS_ERR()`和`PTR_ERR()`将其提取出来：避免了为错误码单独设置一个指针参数。虽然很别扭，但这种做法很有好处。

## 10.3. 破坏编译

Linux 和其他开发者有时会在开发内核中更改函数或结构体的名称；这并不是为了让大家保持警惕：它反映了根本性的变化（例如：不能在中断开启时调用，或者进行了额外的检查，或者不再进行以前捕的检查）。通常这会伴随着向 linux-kernel 邮件列表发送的相当完整的说明；请搜索存档。简单对文件进行全局替换通常会让情况变得更糟。

## 10.4. 初始化结构体成员

初始化结构体的优方法是使用 gcc 的标签元素扩展，例如：

```c
static struct block_device_operations opt_fops = {
    open:               opt_open,
    release:            opt_release,
    ioctl:              opt_ioctl,
    check_media_change:  opt_media_change,
};
```

这使得 grep 搜索变得容易，并且清楚了是哪些结构体字段被设置了。我们应该因为它看起来酷就这样做吗？

## 10.5. GNU 扩展

Linux 内核明确允许使用 GNU 扩展。注意，由于缺乏通用性，某些较复杂的扩展支持并不良好，但以下内容被认为是标准的（详情请参见 GCC info 页的“C Extensions”部分——是的，真的，是 info 页，man 手页只是 info 中内容的简短摘要）：

- 内联函数 (Inline functions)
- 语句表达式（即`({`和`})`结构）
- 声明函数 / 变量 / 类型的属性(`__attribute__`)
- 标签元素 (Labeled elements)
- typedef
- 零长度数组
- 宏可变参数 (Macro varargs)
- 对 void 指针进行算术运算
- 非常量初始化（不在 arch/ 和 include/asm/ 之外）
- 汇编指令作为字符串的函数名(`__FUNCTION__`)
- `__builtin_constant_p()`

在内核中使用`long`时要小心，gcc 为其生成的代码非常糟糕，甚至更糟：在 i386 上除法和乘法无法工作，因为内核环境中缺少了它的 GCC 运行时函数。

## 10.6. C++

在内核中使用 C++ 通常是一个坏主意，因为内核没有提供必要的运行时环境，且头文件没有针对它进行过测试。虽然这仍然可行，但并不推荐。如果你真的想这样做，至少忘记异常（exceptions）吧。

## 10.7. #if

通常认为在头文件（或 .c 文件的顶部）使用宏来抽象函数，比在整个源代码中使用 ‘#if’ 预处理器语句更简洁。

# 第 11 章. 将你的代码放入内核

为了让你的代码达到正式纳入的标准，甚至仅仅是为了制作一个整洁的补丁，你有很多行政工作需要完成：

- 搞清楚你是在谁的地头上“撒尿”。查看源文件顶部、`MAINTAINERS` 文件内部，最后是 `CREDITS` 文件。你应该与此人协调，确保你没有在重复造劳动，或者在尝试某些已经被拒绝的东西。

- 确保在你创建或进行大幅修改的任何文件顶部写上你的名字和电子邮箱地址。当人们发现 bug 或想要进行更改时，这是他们会查看第一个地方。

- 通常你为你的内核 hack 使用一个配置选项。在相应的目录中编辑 `Config.in`（在 `arch/` 下被称为 `config.in`）。Config 语言不是 bash，尽管它看起来像 bash；安全的做法是只使用你已经在 `Config.in` 文件中看到的结构（至少运行一次 "xconfig" 来测试(因为它是唯一带有静态解析器的工具)）。

可以使用 Y 或 N 的变量后面跟着一个标签和 config 定义名称（必须以 CONFIG_ 开头）。三态函数（tristate function）相同，但如果 `CONFIG_MODULES` 被启用，它允许答案 M（这会在你的源码中定义 `CONFIG_foo_MODULE`，而不是 `CONFIG_FOO`）。

你完全可以让你的 CONFIG 选项仅在 `CONFIG_EXPERIMENTAL` 启用时可见：这可以作为对用户的警告。你还可以做很多其他酷事：参考各种 `Config.in` 文件获取灵感。

- 编辑 Makefile：`CONFIG` 变量在这里导出，因此你可以使用 'ifeq' 进行条件编译。如果你的文件符号添加了名称，请将它们加入到 `MX_OBJS` 而不是 `OX_OBJS`、`M_OBJS` 或 `O_OBJS`，这样 `genmake` 就能找到它们。

- 在 `Documentation/Configure.help` 中记录你的选项。在这里提到不兼容性和问题。务必在你的描述末尾加上“如果没疑问，请说 N”（或者，偶尔说 'Y'）；这是给那些完全不知道你在说什么的人准备的。

- 如果你做了一些值得注意的事，将自己放入 `CREDITS` 中，通常不止一个文件（你的名字本该就在源文件顶部）。`MAINTAINERS` 意味着当对子系统进行更改时，你希望被咨询并听到 bug 信息；它意味着对某些代码部分有着超常的投入。

- 最后，不要忘记阅读 `Documentation/SubmittingPatches` 以及可能的 `Documentation/SubmittingDrivers`。

# 第 12 章. 内核口诀

从浏览源码时发现的一些心爱。欢迎随时添加到此列表。

```c
include/linux/brlock.h:

extern inline void br_read_lock (enum brlock_indices idx)
{
    /*
     * 如果使用了无效索引，
     * 这会导致链接时产生错误消息：
     */
    if (idx >= __BR_END)
        _brlock_usage_bug();

    read_lock(&brlock_array[smp_processor_id()][idx]);
```

include/linux/fs.h:

```c
/*
* 内核指针包含冗余信息，所以我们可以使用一种方案，
* 我们可以返回错误码或 dentry 指针
* 它们具有相同的返回值。
*
* 这应该是针对架构的，以允许不同的
* 错误和指针决策。
*/
#define ERR_PTR(err)    ((void*)((long)(err))
#define PTR_ERR(ptr)    ((long) (ptr))
#define IS_ERR(ptr)     ((unsigned long) (ptr) > (unsigned-long)1000))
```

include/asm-i386/uaccess.h:

```c
#define copy_to_user(to,from,n)
```

```c
(__builtin_constant_p(n) ? \
  __constant_copy_to_user((to), (from), (n)) : \
  __generic_copy_to_user((to), (from), (n)))
```

arch/sparc/kernel/head.S:

```c
/*
* Sun 的人不会写单词。确实是 "compatability"。
* 至少我们*知道*自己不会写，并且使用了拼写检查器。
*/
```

```c
/*
* 呃，实际上不会写的是我 Linus。
* 太多的 Sparc 汇编会让你变成这样。
*/
```

```c
C_LABEL(cputypvar):
  .ascii "compatability"
```

```c
/* 在 SS-5, SS-10 上测试过。可能是 Sun 的某人用了拼写检查器。 */
  .align 4
```

```c
C_LABEL(cputypvar_sun4m):
  .ascii "compatible"
```

arch/sparc/lib/checksum.S:

```c
/* Sun，你真的赢不了我，你真的赢不了。停止尝试，
  * 放弃吧。我是认真的，我要把你活生生地
  * 踢出去，游戏结束，灯光熄灭。
  */
```

# 第 13 章. 感谢

感谢 Andi Kleen 提供灵感、回答我的问题、纠正我的错误、填充内容等。感谢 Philipp Rumpf 修复更多拼写和清晰度问题，并提供了一些优秀的非显而易见的观点。感谢 Werner Almesberger 给了我关于 `disable_irq()` 的精彩总结，Jes Sorensen 和 Andrea Arcangeli 补充了警告。感谢 Michael Elizabeth Chastain 检查并完善了 Configure 部分。感谢 Telsa Gwyne 教我 DocBook。
