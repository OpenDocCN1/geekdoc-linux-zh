
Copyright (C) 1999-2006 Hewlett-Packard Co

Copyright (C) 2005, 2006 Fujitsu Limited

Copyright (C) 2006 VA Linux Systems Japan K.K.

Copyright (C) 2005 NBC Corporation

Copyright (C) 1999, 2002, 2007 Silicon Graphics, Inc.

Copyright (C) 1999, 2000, 2001 Mission Critical Linux, Inc.

This program is free software, covered by the GNU General Public License, and you are welcome to change it/or distribute copies of it under certain conditions. Enter `help copying` to see the conditions. This program has absolutely no warranty. Enter `help warranty` for details.

```
```

NOTE: stdin not a tty

`gdb` 6.1

Copyright 2004 Free Software Foundation, Inc.

GDB is free software, covered by the GNU General Public License, and you are free to change it/or distribute copies of it under certain conditions.\.

There is absolutely no warranty for GDB. Type `show warranty` for details. This GDB was configured as `x86_64-unknown-linux-gnu`...

`t`: cannot transition from exception stack to current process stack:

exception stack pointer: `fffff810107132bef20`

process stack pointer: `fffff81010712bef00`

current_stack_base: `fffff81010b509000`

```

<!-- no content -->

# 第 6 章 深入技术细节

```
--- <exception stack> ---
#3 [ffffffff80f3f9f0] `default_idle` at `ffffffff8006b301` *
#4 [ffffffff80f3f9f0] `cpu_idle` at `fffffffff8004943c`
```

Copyright ©Intel Corporation. 保留所有。

## 指令指针 (Instruction pointer)

第一行真正有趣的内容是这一行：

```
[exception RIP: default_idle+61]
```

Copyright ©Intel Corporation. 保留权利。

我们得到了 `exception RIP: default_idle + 61`。这意味着什么？让我们讨论一下 RIP。
三个字母的缩写代表返回指令指针（Return Instruction Pointer）；换句话说，它指向一个内存地址，指示程序在内存中的执行进度。在我们的情况下，你可以在括号异常行下方的行看到地址：

```
[exception RIP: default_idle+61]
RIP: fffffffff8006b301 RSP: fffffffff80f3f9f0 ...
```

Copyright ©Intel Corporation. 保留权利。

目前，地址本身并不重要。在 32 位架构上，指令指针被称为 `EIP`。
第二部分信息对我们来说有用得多。RIP 所在的内核函数名称是 `default_idle`：`61` 是该函数内部发生异常的十进制格式的偏移量。这是我们在分析中将使用的非常重要的部分。

### 代码段 (CS) 寄存器

从括号字符串到 --- <exception stack> 之间的内容是寄存器的转储。大多数对我们没用，但 CS 寄存器有用。

```
CS: 0010
```

Copyright ©Intel Corporation. 保留权利。

我们再次遇到了一个四位组合。为了解释这个概念，我们需要稍微挖掘并谈论特权级。

## 特权级 (Privilege levels)

特权级是保护 CPU 资源的概念。不同的执行线程可以拥有不同的权限级，授予对系统资源、内存区域、I/O 端口等的访问权限。共有四个级别，范围 0 到 3。

级别 0 权限最高，被称为内核模式（Kernel mode）。级别 3 权限最低，被称为用户模式（User mode）。

大多数现代操作系统（包括 Linux）忽略中间的两个级别，只使用 0 和 3。这些级别也被称为环（rings）。

## 当前特权级 (CPL)

代码段 (`CS`) 寄存器指向设置程序指令的段。该寄存器的两个低两个位指定了 CPU 的当前特权级 (`CPL`)：两个位意味着介于 0 到 3 之间的数字。

### 描述符特权级 (DPL) 和请求特权级 (RPL)

描述符特权级 (`DPL`) 定义为可以访问该资源的最高特权级。此值定义在段描述符中。请求特权级 (`RPL`) 定义在段选择器中，即最后两个位。从数学角度上说，`CPL` 不允许超过 `MAX(RPL,DPL)`，如果超过了，将导致通用保护故障（general protection fault）。现在，为什么这些对你很重要呢？

嗯，如果你遇到在 `CPL` 为 3 时系统崩溃的情况，那么这可能表明硬件故障，因为系统不应该因为用户模式下的问题而崩溃。或者，可能是某个有 Bug 的系统调用中存在问题。这些只是一些粗略的例子。现在，让我们继续分析我们的崩溃日志：

```
CS: 0010
```

正如我们所知，两个低位指定了 `CPL`。这意味着四个级别；级别 1 和 2 被忽略了。这给我们留下了 0 和 3，分别是内核模式和用户模式。转换成二进制格式，我们得到 00 和 11。

用于表示描述符数据的格式可能会让人困惑，但它非常简单。如果最后一个数字是偶数，那么我们就处于内核模式；如果最后一个数字是奇数，那么我们就处于用户模式。因此，看 `CPL` 是 0，因为导致崩溃的违规任务运行在内核模式下。了解这一点很重要。它能帮助我们理解问题的本质。仅供参考，这里有一个崩溃发生在用户模式的例子：

```
#20 [ffff880a77f9f90] mntput_no_expire at fffffffff811143
#21 [ffff880a77f9f94] filp_close at fffffffff81d0f9
#22 [ffff880a77f9f90] system_call_fastpath at fffffffff8102fb
RIP: 00002aaacd007 RSP: 00007ffffff6c8 RFLAGS: 00000202
RAX: 0000000000000057 RBX: fffffffff8102fb RCX: 00002aaa02960
```

| RDX | RSI | RDI |
| :--- | :--- | :--- |
| 000000000000041 | 0000aaaccdf650 | 000000001661238 |
| RBP | R8 | R9 |
| 00007ffff6cc0 | 736a2e73746753 | 0000000016615d0 |
| R10 | R11 | R12 |
| 0002aaaada82120 | 00000000000022 | 0000ffff00 |
| R13 | R14 | R15 |
| 00007ffff6d10 | 000000001661238 | fffff8810e5d50 |
| ORIG_RAX | CS | SS |
| 00000000000057 | 0033 | 002b |

回到示例，我们学习了很多重要的细节。我们知道了崩溃时指令指针所在的精确内存地址。我们知道了特权级。重要的是，我们知道了崩溃时的函数名称和偏移量。对于所有实际目的，我们只需要找到源并检查崩溃。由于各种原因，这可能并不总是可行的，但值得尝试。

所以，我们知道 `crash_callback` 函数是由 `do_nmi()` 调用的，而 `do_nmi()` 是由 `default_idle()` 调用的，导致了崩溃。我们可以检查这些函数并尝试理解更多。现在，让我们再次查看我们的 Fedora 示例。

```
Pid: 0, comm: swapper tainted 2.6.31.5-127.fc12 #1
```
