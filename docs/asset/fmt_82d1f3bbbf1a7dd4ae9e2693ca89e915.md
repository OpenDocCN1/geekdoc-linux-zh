
GCC 是一个优化编译器。默认情况下，Linux 内核使用 `-O2` 编译器标志编译。这启用了许多优化算法，这些算法可以改变代码的基本结构和顺序。例如，Linux 内核大量使用内联函数。内联函数是用 `inline` 关键字声明的小型函数，结果是函数被直接包含在执行线程中，而不是生成带有相关开销的函数调用²。内联函数至少需要 `-O1` 优化级别。因此，你无法关闭优化，而关闭优化对于便于调试是理想的。

在 Linux 内核的某些区域，单步执行代码是困难或不可能的。显而易见的例子是修改虚拟内存设置的代码路径。当你的应用程序调用系统并进入内核时，这会导致进程地址空间的变化。事实上，任何涉及处理器异常的转换都会改变操作上下文，并且可能很难或无法进行单步。

## 14.2 使用 KGDB 进行内核调试

两种流行的方法可以在 Linux 内核中实现源码级调试：

- 使用 KGDB 作为远程 GDB 代理
- 使用硬件 JTAG 探针控制处理器

JTAG 调试见第 14.4 节“硬件辅助调试”。KGDB（内核 GDB）是一组 Linux 内核补丁，通过其远程串口协议³为 GDB 提供接口。KGDB 实现了一个 GDB stub，与运行在你的主机开发工作站上的交叉 GDB 通信。直到最近，目标机上的 KGDB 还需要串口连接到开发主机。

> ^1 详见本章末尾引用的 GCC 手册有关优化级别的细节。
>
> ^2 内联函数类似于宏，但具有编译时类型检查的优势。
>
> ^3 KGDB 的简化版本已合并到 Linux 2.6.26 主线中，但不支持某些功能，包括通过以太网 KGDB 以及其他功能。

如图 14-1 所示，调试器（你的交叉版本 GDB）运行在你的开发主机系统上。KGDB 是运行在你目标系统上的内核的一部分。KGDB 实现了将 GDB 与你的目标板接口所需的钩子，以启用设置断点、检查内存和启用单步程序执行等功能。

### 14.2.1 KGDB 内核配置

如所述，不同架构和平台在 KGDB 支持方面存在差异。以下示例基于 Freescale Semiconductor 在 CDS 平台上的 Power Architecture MPC8548 CPU，使用了商业 MontVista Linux 发行版，该版本增加了此 KGDB 支持。示例中的某些功能在主线内核源码中不可用，包括内核中的 KGDB 支持长期以来一直不被推荐，直到最近（Linux 2.6.26）才开始以通用形式出现。

KGDB 是内核特性，必须在你的内核中启用。KGDB 从 Kernel hacking 菜单中选择，如图 14-2 所示。（为了使该图适应页面，Kernel hacking 菜单中删除了许多项。你的菜单将会有更多。）

如图 14-1 所示，调试器（你的交叉版本 GDB）运行在你的开发主机系统上。KGDB 是运行在你目标系统上的内核的一部分。KGDB 实现了将 GDB 与你的目标板接口所需的钩子，以启用设置断点、检查内存和启用单步程序执行等功能。

# 列表 14-1 继续

```
Memory CAM mapping: CAM0=256Mb, CAM1=0Mb, CAM2=0Mb residual: 0Mb
Linux version 2.6.27.28.freescale-8548cds.0980109010 (chris@pluto) (gcc version
4.3.3 (MontaVista Linux Sourcery G++ 4.3-217) #1 PREEMPT Mon Mar 29 11:09:48 EDT
2010
```

```
console [dbg0] enabled
setup_arch: bootmem
mp85xx_cds_arch()
<.. many messages deleted ..>
serial: 8250/1650 driver 4 ports, IRQ sharing enabled
serial8250.0: ttyS0 at MMIO 0xe000450 (irq = 42) is 16550A
serial8250.0: ttyS1 at MMIO 0xe000460 (irq = 42) is 16550A
console handler: boot [dbg0] -> real [ttyS1]
kgdb: Registered I/O driver kgdb8250.
kgdb: Waiting for connection from remote gdb...
```

启动序列的大部分内容在我们第 7 章“引导加载程序”的介绍中已经熟悉了。回想第 7 章，内核命令行是由 U-Boot `bootargs` 环境变量定义的。注意，我们添加了 `kgdbwait` 变量，它指示内核强制执行早断点并等待主机调试器（你的 `console-db`）连接。

请注意，启动序列并没有完成。由于我们在命令行中放置了 `kgdbwait`，内核一直完成初始化，直到串口驱动程序加载，然后命中了预定义的断点。在此时，它会无限期地等待外部调试器的连接。

你还应该注意第二个内核命令行参数。这种特定的架构（Power）和平台（8548CDS）使用 8250 串口驱动程序以及由 `../drivers/serial/8250_kgdb.c` 实现的特殊 8250 基础 KGDB。你必须使用类似于描述控制设备的语法，告诉 KGDB 使用哪个串口进行调试。

现在内核已经设置好并正在等待主机调试器，我们可以开始调试会话了。我们从主机开发工作站调用交叉编译的 GDB 的远程协议，并通过它连接到目标机。在这个示例中，我们与控制台共享串口，因此在尝试用 GDB 连接之前，我们必须断开终端模拟器与远程的连接。列表 14-2 强调了 GDB 连接过程。这假设我们已经退出了终端模拟器，并释放了串口供 GDB 使用。

## 14.2.2 连接到 KGDB

### 列表 14-2 连接到 KGDB

在这里我们执行了三个操作：

- 调用了交叉 GDB，并向其传递了内核 ELF 文件 `vmlinux`
- 使用 `target remote` 命令连接到目标
- 发布了 `list` 命令（使用其缩写 `l`）来显示我们在源代码中的位置

虽然说这有些显而易见，但我们传递给 GDB 的 `vmlinux` 镜像必须与运行在你的目标板上的内核是同一个内核构建版本。它还必须使用 `-g` 编译器标志进行编译，以包含调试信息。回想第 13 章“开发工具”第 13.5.2 节，你可以使用交叉 `readelf` 来验证你的 `vmlinux` 镜像是否已编译了调试符号。使用类似的命令来验证你的 ELF 文件中是否包含调试段：

```
$ ppc_85xx-readelf -S vmlinux | grep debug
```

当我们发布 `target remote` 命令时，GDB 通过显示程序计数器（PC）的位置做出响应。在这个示例中，内核停止在 `../kernel/kgdb.c` 文件第 1802 行的 `kgdb_breakpoint()` 函数中。当我们发布 `continue (c)` 命令时，执行将从该点恢复。

### 14.2.3 有用的内核断点

我们现在已经与目标板上的内核建立了调试连接。当我们发布 GDB 连接 `(c)` 命令时，内核继续启动，如果没有发生任何问题，启动过程将完成。在这一阶段，你可能想要放置一些断点来建立你特定的调试会话。列表 14-3 中列出了最常见的断点。

### 列表 14-3 常见的内核断点

```
(gdb) b panic
Breakpoint 1 at 0xc02d1a84: file arch/powerpc/include/asm/thread_info.h, line 87.
(gdb) b sys_sync
Breakpoint 2 at 0xc00bae4: file fs/sync.c, line 41.
(gdb) c
Continuing.
```

使用 GDB 断点命令（再次使用其缩写版本），我们进入了两个断点。一个是 `panic()`，另一个是在系统调用进入 `sys_sync()` 时。前者允许在稍后的事件产生 `panic` 时调用调试器。这使得能够检查 `panic` 发生时的系统状态。后者是停止内核并从用户空间陷入调试器的一种很有用方法。

我们现在准备好继续调试会话了。我们的目标机上运行了一个启用了 KGDB 的内核，并暂停在 KGDB 定义的断点处。我们通过主机的交叉调试器（在本例中调用了 `ppc_85xx-gdb`）与目标建立了连接，并启用了一对有用的断点。我们现在可以将调试活动直接指向当前任务。

有一个例外：根据定义，在 `breakpoint()` 用于建立启用了 KGDB 的内核与交叉调试器连接之前，无法使用 KGDB 单步代码。这一主题将在 14.4 节“硬件辅助调试”中介绍。

一旦设置了断点并发布了 `continue` 命令，你可以随时通过向交叉调试器发送 `Ctrl-C` 来停止执行。列表 14-4 显示了其样子。

### 列表 14-4 正在进行的调试会话

```
(gdb) c
Continuing.

<<< User signal Ctrl-C >>>
Program received SIGINT, Trace/trap.
0xc058048 in kgdb_breakpoint () at kernel/kgdb.c:1802
1802
wmb(); /* Sync point before breakpoint */
(gdb) bt
#0 0xc058048 in kgdb_breakpoint () at kernel/kgdb.c:1802
#1 0xc019bcdc in kgdb_8250_interrupt (irq=<optimized out>, dev_id=<optimized out>) at drivers/serial/8250_kgdb.c:145
#2 0xc05a4f0 in handle_IRQ_event (irq=42, action=0xc8faf20) at kernel/irq.c:140
#3 0xc05c19c in handle_irq (irq=42, desc=0xc39a950) at kernel/irq/chip.c:42
#4 0xc0004b0 in do_IRQ (irq=<optimized out>) at include/linux/irq.h:289
#5 0xc00f310 in ret_from_exception ()
#6 0xc0008144 in cpu_idle () at arch/powerpc/kernel/idle.c:59
#7 0xc02d022c in rest_init () at init/main.c:481
#8 0xc0336e75c in start_kernel () at init/main.c:691
#9 0xc0003d0 in setup()
(gdb)
```

你可以在列表 14-4 中看到编译器优化的影响。这将在 14.3 节进一步讨论。

### 14.2.4 与 KGDB 共享控制台端口

虽然可以使用单个串口作为系统控制台以及通过串口运行 KGDB，但这并不是理想的。KGDB 以不同的完整程度存在，取决于你的架构和平台。一旦你离开 x86 架构，情况就会变得不确定。KGDB 有许多连接选项，包括使用串口、以太网端口甚至某些平台上的 USB。可以确定，并不是所有平台都提供了这些组合。

书中其他地方提到过：如果你认为你将使用 KGDB 进行内核调试，那么额外串口的成本是完全合理的，特别是如果为了满足成本需要在生产环境中移除它。节省的麻烦（开发者时间）将弥回增加的开发成本。

要在控制台和 KGDB 之间共享串口，你需要两个命令行参数。使用内核命令行参数 `kgdboc` 来指定使用哪个串口，并使用 `kgdbcon` 指定你与控制台共享该端口。类似于在内核命令行上描述控制设备的方式指定 `kgdboc` 参数：

```
kgdbcon kgdboc=ttyS1,115200
```

当你启动并连接到 KGDB 时，任何控制台消息由你的交叉 GDB 显示。列表 14-5 显示了这种情况。我们首先使用上述内核命令行参数启动目标。目标启动到登录提示符。我们必须使用 Sysrq 功能启用 KGDB。从控制台串口执行此操作简单的方法是使用 `/proc/sysrq-trigger`。

```
root@8548:~# echo g > /proc/sysrq-trigger
SysRq : GDB
Entering KGDB
```

现在我们断开控制台串口终端，将其释放给 KGDB 使用。然后我们启动交叉 GDB，会话如列表 14-5 所示。

### 列表 14-5 与 KGDB 共享串口控制台

```
$ ppc_85xx-gdb -q /dev/ttyS0
(gdb) target remote /dev/ttyS0
Remote debugging using /dev/ttyS0
0xc058098 in sysrq_handle_gdb (key=0x11, tty=0xc8dd) at kernel/kgdb.c:1802
1802
wmb(); /* Sync point before breakpoint */
(gdb) bt
#0 0xc058048 in kgdb_breakpoint () at kernel/kgdb.c:1802
#1 0xc019bcdc in kgdb_8250_interrupt (irq=<optimized out>, dev_id=<optimized out>) at drivers/serial/8250_kgdb.c:145
#2 0xc05a4f0 in handle_IRQ_event (irq=42, action=0xc8faf20) at kernel/irq.c:140
#3 0xc05c19c in handle_irq (irq=42, desc=0xc39a950) at kernel/irq/chip.c:42
#4 0xc0004b0 in do_IRQ (irq=<optimized out>) at include/linux/irq.h:289
#5 0xc00f310 in ret_from_exception ()
#6 0xc0008144 in cpu_idle () at arch/powerpc/kernel/idle.c:59
#7 0xc02d022c in rest_init () at init/main.c:481
#8 0xc0336e75c in start_kernel () at init/main.c:691
#9 0xc0003d0 in setup()
```

# 列表 14-5 继续

```
[New Thread 1665]
NET: Registered protocol family 10
lo: Disabled Privacy Extensions
ADDCONF(NETDEV_UP): eth0: link is not ready
tun0: Disabled Privacy Extensions
```

如列表 14-5 所示，我们设置了断点并继续，允许内核再次运行，且此时我们的断点已经设置好。在主机的另一个单独终端窗口中，我们通过 ssh 登录该终端并加载一个模块。在这种情况下，模块是 `ipv6.ko`。使用哪种模块并不重要。我们的目标是生成一些内核 `printk` 消息，以验证它们确实到达了 GDB 终端窗口。你可以看到这些以 [New Thread 1665] 行开头的消息。这些是路由到系统控制台的内核 `printk` 消息，并通过 KGDB 的 GDB 远程协议路由到 GDB 控制台。这确实非常酷。

### 14.2.5 调试极早期内核代码

上述技术无法在内核初始化期间调试极早期的内核代码。事实上，你能做的最好是在串口驱动程序被调用并注册后调试初始化代码。在某些架构和平台上，这种能力通过两个内核命令行参数提供：`kgdbwait` 和 `kgdb8250`。

对早期内核的支持需要一个支持早期内核调试的 KGDB I/O 驱动程序。使用 KGDB 进行早期内核调试最常见（侵入性最小）的 I/O 方法是串口驱动程序。一个例子就是之前提到的 `kgdb8250` 驱动。显而易见，该驱动需要编译到内核中才能供早期内核调试使用。

正如我们在列表 14-1 中看到的，`kgdb8250` 用于告诉 KGDB 使用哪个串口。然而，通过使用另一种语法，我们可以调用一个早期初始化程序，该程序将进行非常早的内核调试。通过使用 `kgdbwait`，我们可以指示内核在初始化序列的极早期停止，等待用户的命令。将这些内容添加到内核命令行以启用使用 KGDB 进行早期内核调试：

```
kgdb8250=ttyS1,115200 kgdbwait
```

> ⁵这种早期调试支持是由 MontaVista 在其针对 MPC8548 平台的商业嵌入式 Linux 中提供的。目前在主内核源码中不可用。你的内核需要通过这些补丁来复制该功能。

重要的是意识到这些内核命令行参数的顺序至关重要。你必须先提供 KGDB I/O 驱动程序（在我们的示例中是 `kgdb8250`），以便它在遇到 `kgdbwait` 之前完成初始化。由于 `kgdbwait` 基本上会导致调试断点，因此在发布断点之前，必须有基础设施可以与调试器进行通信。

另一个需要记住的点是，这种支持通常是特定平台的。也就是说，你的内核和平台必须支持某种早期内核调试 I/O 驱动程序，该功能才能可用。你的平台可能为此提供不同的硬件，这取决于你（或你的嵌入式 Linux 供应商）提供早期内核调试 I/O 驱动程序。

对于 `kgdb8250` I/O 驱动程序，你还可以提供一个完整的规范，传递适用于你特定板卡的驱动程序详细信息。这可以包括访问此驱动程序所需的 I/O 类型、其基地址，以及可选的寄存器偏移 IRQ 和波特率。在这种情况下，它看起来如下：

```
kgdb8250=cio|mmio|base,<address>[/<regshift>,<baud rate>,<irq>]
```

### 14.2.6 主内核中的 KGDB 支持
