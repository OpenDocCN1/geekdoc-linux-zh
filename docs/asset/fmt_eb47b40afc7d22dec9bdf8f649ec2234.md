
28 Reading symbols from `/home/chris/sandbox/linux-2.6.27/drivers/block/loop.ko`...done.

29 (gdb)

## 14.3 printk 调试

使用 `printk` 进行内核调试是一种流行的技术，因为 `printk` 已经变成了内核熟悉的 `printf()` 函数。`printk` 定义在 `printk.c` 中。`printk` 允许添加一个字符串来标识消息的严重程度。`kernel.h` 定义了八个级别：

```
#define KERN_EMERG "<0>" /* 系统不可用 */
#define KERN_ALERT "<1>" /* 必须立即采取行动 */
#define KERN_CRIT "<2>"  /* 严重情况 */
#define KERN_ERR "<3>"   /* 错误情况 */
#define KERN_WARNING "<4>" /* 警告情况 */
#define KERN_NOTICE "<5>" /* 正常但重要的情况 */
#define KERN_INFO "<6>"  /* 信息性 */
#define KERN_DEBUG "<7>" /* 调试级消息 */
```

一个简单的 `printk` 消息可能如下：

```
printk("foo() entered with %s\n", arg);
```

如果省略了级别（如下所示），内核会分配一个级别，这定义在 `printk.c` 中。在最近的内核中，它被设置为级别 4，`KERN_WARNING`。带有级别的 `printk`（首选方法）可能如下：

```
printk(KERN_CRIT "vmalloc failed in foo()");
```

不，这种不寻常的 C 语法并不是错别字。`KERN_CRIT` 本身就是一个字符串，因此不需要逗号来分隔参数。事实上，如果包含了逗号，将无法产生预期结果。编译器会自动将字符串连接成一个字符串。默认情况下，所有低于预定义日志级别的 `printk` 消息都会显示在系统控制台设备上。默认控制台级别定义在 `printk.c` 中。在最近的内核中，它的值为 7。这意味着任何重要性大于 `KERN_DEBUG` 的 `printk` 消息。

你可以通过多种方式设置默认内核日志级别。在启动时，你可以通过向内核传递适当的内核命令行参数在目标板上指定级别。在 `main.c` 中定义的三个内核命令行选项影响默认日志级别：

- `debug` 将控制台级别设置为 10。
- `quiet` 将控制台级别设置为 4。
- `loglevel` 将控制台级别设置为你选择的值。

使用调试日志级别可以有效地显示所有的 `printk` 消息。使用 `quiet` 则显示所有严重性为 `KERN_ERR` 或更高的 `printk` 消息。

`printk` 消息可以记录到目标机文件或通过网络发送。使用 `klog`（内核日志）和 `syslog`（系统日志）可以控制 `printk` 消息的日志行为。这些常用工具在 Linux 手册页（man pages）中已有描述，因此在此不再详述。

## 14.3 魔术请求键

Magic SysReq 键是一种非常有用的调试工具，通过一系列预定义的快捷键直接向内核发送消息。对于许多目标架构和板卡，你使用串口端口上的终端仿真器作为控制台。对于这些架构，Magic SysReq 键被定义为一个中断字符后跟一个命令字符。许多 Linux 开发者使用 `minicom` 终端。对于 `minicom`，通过按下 `Ctrl-A F` 发送中断。如果你使用 `screen`，按下 `Ctrl-A C` 发送中断。发送中断字符后，你有 5 秒的时间在命令字符超时前输入。

这个实用的工具对于开发和调试非常有帮助，但也可能导致系统损坏。事实上，执行 `b` 命令会立即重启你的系统，而无需任何通知。文件没有关闭，磁盘没有卸载。当发布 `reboot` 命令时，控制权立即传递给架构的复位向量。使用此强大工具时需谨慎！

该功能在 Linux 内核子目录下的 `sysreq` 文件中有详细文档。你可以在那里找到许多架构细节以及可用命令的描述。

设置内核日志级别的另一种方法是使用 Magic SysReq 键。该命令是一个 0 到 9 之间的数字，结果是将默认日志级别设置为该数字。在 `minicom` 中，按下 `Ctrl-A F` 后跟一个数字，例如 9。在发送中断序列后，终端上显示如下：

```
$ SysRq : Changing Loglevel
LogLevel set to 9
```

命令可以转储寄存器、关闭系统、重启系统、转储进程列表、将当前内存信息转储到控制台等。详情请参阅任何 Linux 内核文档。

此功能最常用于系统死锁的情况。通常情况下，Magic SysReq 键提供了一种从死机系统中获取某些信息的方法。

## 14.4 硬件辅助调试

到此时，你可能已经意识到无法使用 GDB 调试极早的启动代码。这是因为在大多数底层硬件初始化代码执行之前，GDB 还没有初始化。此外，如果你被分配了启动新板卡并移植引导程序和 Linux 内核的任务，拥有硬件调试探针无疑是调试这些早期阶段问题的有效方法。

你可以选择多种硬件调试探针。对于本节的示例，我们使用由 Abatron 制造的 BDI-2000 设备（见 www.abatron.ch）。这些设备通常被称为 JTAG 探针，因为它们使用最初由联合测试动作小组（JTAG）用于集成电路边界扫描的底层通信方法。Abatron 随后发布了更新的 BDI-3000，它具有更快的 100MB 以太网接口。

JTAG 探针包含一个用于连接目标板的小连接器。它通常是一个小型方形引脚插头和排线。大多数现代高性能 CPU 都包含一个 JTAG 接口，用于提供这种软件调试能力。JTAG 探针连接到此 CPU 的 JTAG 接口。JTAG 探针的另一侧通过以太网、USB 或并行端口连接到你的开发系统。图 14-6 详细说明了 Abatron 设备的设置。

![](img/75da989fc023923ea1a768dd5ab686d4_445_0.png)

图 14-6 硬件 JTAG 探针调试

JTAG 探针的设置可能非常复杂。这是由于其连接的 CPU 复杂性导致的。当目标板上电且 CPU 跳出复位状态时，几乎没有任何东西初始化。事实上，许多处理器在执行任何操作之前至少需要少量的初始化。有许多方法可以将此配置导入 CPU。某些 CPU 读取硬件配置字或特定引脚的初始值来获取其上电配置。另一些则取决于 Flash 等简单易失性存储设备中的默认位置。在使用 JTAG 探针时（特别是启动新板卡设计时），在进行任何其他操作之前必须执行最小级别的 CPU 和板卡初始化。许多 JTAG 探针依赖配置文件进行初始化。

Abatron 单元使用配置文件来初始化其连接的目标硬件，并定义调试器的其他运行参数。该配置文件包含了初始化 CPU、内存系统和其他必要的板卡级硬件的指令。开发者有责任根据自己的板卡使用正确的指令自定义此配置文件。配置命令语法的细节可以在 JTAG 探针文档中找到。然而，只有嵌入式开发者才能为特定的板卡设计创建唯一的配置文件。这需要对 CPU 和板卡级设计特征有深入了解。就像为新板创建自定义 Linux 移植一样，这项任务没有捷径或替代方案。

附录 F，“示例 BDI-2000 配置文件”包含一个 MPC5200 嵌入式控制器的示例 Abatron 配置文件。在该附录中，你可以看到该 Abatron 设备的设置。

`prog` 命令显示了它的三个可选参数。这些参数指定了新镜像加载到内存中的位置以及镜像文件的名称——在本例中，这是一个二进制文件。你可以在 BDI-2000 配置文件中指定这些参数。在这种情况下，该命令简化为不带任何参数的 `prog`。

此示例仅触及了这两个 BDI-2000 命令的皮毛。它支持更多用法和功能组合。每个硬件 JTAG 探针都有其指定 Flash 擦除和编程能力的方法。具体细节请参阅您特定设备的文档。

### 14.4.2 使用 JTAG 探针进行调试

与其通过用户界面直接与 JTAG 探针交互，许多 JTAG 探针可以与你的源码级调试器接口。目前硬件探针支持的 Linux 最流行的调试器是 GDB 调试器。在这种用法场景下，指示 GDB 通过以太网连接与目标外部连接开始调试会话。调试器不是通过用户界面与 JTAG 探针直接通信，而是自身与 JTAG 探针来回传递命令。在这种模型中，JTAG 探针使用 GDB 远程协议代表调试器控制硬件。连接细节请参考图 14-6。

JTAG 探针对于 bootloader 和早期启动代码的源码级调试特别有用。在本示例中，我们演示了如何使用 GDB 和 Abatron BDI-2000 对 Power Architecture 目标上的 U-Boot bootloader 部分进行调试。

许多处理器包含调试寄存器，具有设置传统地址断点（处理器到达某个地址时停止）和数据断点（对指定内存地址进行条件访问时停止）的能力。当调试代码存储在只读内存 Flash 中时，这是设置断点的唯一方法。然而，这些寄存器通常是有限的。许多处理器仅包含一两个这样的寄存器。在使用硬件断点之前，你必须理解这一限制。接下来的示例演示了这一点。

使用如图 14-6 所示的设置，假设你的目标板将 U-Boot 存储在 Flash 中。我们在第 7 章介绍引导加载程序时，你了解到 U-Boot 和其他引导加载程序会在启动后尽快自复制到 RAM 中。这是因为 RAM 的硬件读取（和写入）周期比 Flash 等典型的只读存储设备快几个数量级。这带来了两个具体的调试挑战。首先，我们无法修改只读内存的内容（以插入软件断点），我们必须依赖处理器支持的断点寄存器来实现此目的。

第二个挑战在于，执行上下文（Flash 或 RAM）中只有一个能被 GDB 读取其符号调试信息的 ELF 可执行文件所表示。在 U-Boot 中，它被链接到其初始启动的 Flash 环境。早期代码会进行重定位并执行任何必要的地址调整。这意味着我们需要在这两个执行上下文中使用 GDB 进行工作。列表 14-25 显示了此类调试会话的示例。

#### 列表 14-25 使用 JTAG 探针调试 U-Boot

```
$ pp-linux-gdb -q u-boot
(gdb) target remote bdi:201
Remote debugging using bdi:201
_start () at /home/chris/sandbox/u-boot-1.1.4/cpu/mpc55xxx/start.S:91
91      l1 r21, BOOTFLAG_COLD /* Power-On */
Current language: auto; currently asm
```

```
<< Debug a flash resident code snippet >>
(gdb) mon break
(gdb) b board_init_f
Breakpoint 1 at 0xffff0457c: file board, line 366.
(gdb) c
Continuing.
```

```
Breakpoint 1, board_init_f (bootflag=0x7fc3afc) at board.c:366
366      gd = (gd_t *) (CFG_INIT_RAM_ADDR + CFG_GBL_DATA_OFFSET)
Current language: auto; currently c
(gdb) bt
#0 board_init_f (bootflag=0x1) at board.c:366
#1 0xff0456c in board_init_f (bootflag=0x1) at board.c:353
(gdb) i frame
Stack level 0, frame at 0xff000bf50:
pc = 0xff0457c in board_init_f (board.c:366); saved pc 0xff0456c
called by frame at 0xff000bf78
source language c
Arglist at 0xff000bf50, args: bootflag=0x1
Locals at 0xff000bf50, Previous frame's sp is 0x0
```

#### 列表 14-25 续

```
<< Debug a memory resident code snippet after relocation >>
(gdb) del 1
(gdb) symbol-file
Discard symbol table from /home/chris/sandbox/u-boot-1.1.4-powerdna/u-boot'?
(y or n) y
No symbol file now.
(gdb) add-symbol-file u-boot 0x7fa8
(gdb) add-symbol-file u-boot 0x7fa8
Reading symbol table from /home/chris/sandbox/u-boot-1.1.4-powerdna/u-boot...
(gdb) b board_init_f
Breakpoint 2 at 0xffff0457c: file board, line 366.
(gdb) c
Continuing.
Breakpoint 1, board_init_f (bootflag=0x7fc3afc) at board.c:366
366      gd = (gd_t *) (CFG_INIT_RAM_ADDR + CFG_GBL_DATA_OFFSET)
Current language: auto; currently c
(gdb) bt
#0 board_init_f (bootflag=0x1) at board.c:366
#1 0xff0456c in board_init_f (bootflag=0x1) at board.c:353
(gdb) i frame
Stack level 0, frame at 0xff000bf50:
pc = 0xff0457c in board_init_f (board.c:366); saved pc 0xff0456c
called by frame at 0xff000bf78
source language c
Arglist at 0xff000bf50, args: bootflag=0x1
Locals at 0xff000bf50, Previous frame's sp is 0x0
```

由于我们正在进行远程调试，在尝试在进入额外的断点后恢复执行之前，我们并不知道存在资源限制的。这是由于 GDB 处理断点的方式导致的。当命中断点时，GDB 会使用该特定内存位置的原始操作码（opcodes）恢复所有断点。当它恢复执行时，它会在指定的位置上重新恢复断点操作码。你可以通过启用 GDB 的远程调试模式来观察这一行为，正如我们之前看到的那样：

```
(gdb) set debug remote 1
```

## 14.5 当无法启动时

在服务嵌入式 Linux 的各种邮件列表中，经常被问到的问题之一如下：

> 我正尝试在我的板子上启动 Linux，但在控制台打印出这条消息后就卡住了：
> "Uncompressing Kernel Image . . . OK.",

这标志着嵌入式 Linux 那段漫长且有时令人沮丧的学习曲线的开始！许多可能出错的地方都会导致这种常见的失败。通过一些知识和 JTAG 调试器，有方法可以确定哪里出了什么问题。

### 14.5.1 早期串口调试输出

我们在书中第一版中介绍过的 `CONFIG_SERIAL_TEXT_DEBUG` 在最近的内核中已被弃用。内核源码已删除了对该配置参数的引用。

然而，`CONFIG_EARLY_PRINTK` 在大多数架构上都是可用的。该功能在大多数内核配置中默认开启的。开启后，它允许比串口驱动注册早得多的控制台输出。在大多数 Linux 端口上，不需要任何操作即可启用它；它是默认的。

### 14.5.2 转储 printk 日志缓冲区

我们在第 14.3.6 节讨论 `printk` 调试时，指出了这种方法的某些局限性。`printk` 本身是一个非常非常健壮的实现。它的缺陷之一是，在启动序列的后续阶段（即控制台设备初始化之前），你看不到任何 `printk` 消息。通常，当你的板子在启动时挂起，会有很多消息阻塞在 `printk` 缓冲区中。如果你知道在哪里找到它们，就可以轻松地定位导致启动挂起的精确问题。事实上，很多时候你会发现内核遇到了错误并导致了对 `panic()` 的调用。`panic()` 的输出可能已经转储到打印缓冲区中，你可以轻松地定位到产生问题的代码的确切行。

使用 JTAG 调试器完成此操作最好，但仍然可以使用 bootloader 及其内存转储能力在重置后显示打印缓冲区的内容。重置可能会导致内存内容的某些损坏，但日志缓冲区文本通常是可读的。

`printk` 存储消息文本的实际缓冲区在打印源文件 `.../kernel/printk.c` 中声明。

我们可以从 Linux map 文件 `System.map` 中轻松地确定该缓冲区的链接位置。

```
$ grep _log_buf System.map
c022e5a4 b __log_buf
```

如果系统在启动时发生挂起，请重启并使用 bootloader 检查缓冲区。由于内核虚拟内存和物理内存之间的关系在给定架构上是固定且恒定的，我们可以进行简单的转换。`__log_buf` 的地址是一个内核虚拟地址；我们必须将其转换为物理地址。在这个特定的 Power Architecture 处理器上，转换只是简单的减去常量 `KERNELBASE`（`0xc000000`）。这就是我们在内存中探测并读取打印日志缓冲区内容（如果有的话）的地方。

列表 14-26 是 U-Boot 内存转储命令显示的列表示例。

#### 列表 14-26 原始 printk 日志缓冲区转储

```
= md 22e55a4
```
