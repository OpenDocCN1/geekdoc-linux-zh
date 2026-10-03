
注意这些 U-Boot 符号的链接地址。它们是为位于此特定板内存映射最高部分的 Flash 设备链接的。此列表仅包含几个示例符号，用于讨论。中间列是符号类型。大写字母表示全局符号，小写字母表示本地符号。`B` 表示符号位于 `.bss` 段。`T` 表示符号位于 `.text` 段。

`D` 表示符号位于 `.data` 段。`A` 表示此地址是绝对的，不会在额外的链接阶段修改。此绝对符号指示了启动时 `.bss` 段的起始，正如 C 执行环境的要求的那样。

## 13.7 章节总结

- GNU 调试器 (GDB) 是一个复杂且强大的调试器，具有许多功能。我们介绍了基础知识以帮助你上手。
- GDB 的 DDD 图形化前端将源代码和数据显示与 GDB 命令接口强大的功能集成在一起。
- `cbrowser` 是理解大型项目的有用工具。它利用 `cscope` 数据库快速查找并显示 C 语言源码中的符号和其他元素。
- Linux 受到许多性能分析和跟踪分析工具的支持。我们介绍了其中几种工具，包括 `strace`、`ltrace`、`top` 和 `ps`，以及内存性能分析工具 `mtrace` 和 `dmalloc`。
- 嵌入式开发人员经常需要构建自定义镜像（如引导加载程序和固件镜像所需的镜像），因此对 `binutils` 的知识是必不可少的。我们介绍了 `binutils` 中的许多实用工具，如 `readelf`、`objdump`、`objcopy` 以及其他几个工具。

### 13.7.1 扩展阅读建议

- GDB: GNU 项目 调试器: www.gnu.org/software/gdb/gdb.html
- GDB 便查手册 (GDB Pocket Reference), Arnold Robbins, O'Reilly Media, 2005
- 数据显示调试器 (Data Display Debugger): www.gnu.org/software/ddd/
- `cbrowser` 首页: http://cbrowser.sourceforge.net/
- `cscope` 首页: http://cscope.sourceforge.net/index.html
- `dmalloc` Malloc 库: http://dmalloc.com/
- 工具接口标准 (TIS) 可执行与链接格式 (ELF) 规范, 版本 1.2, TIS 委员会，1995年5月
- 工具接口标准。

# 第 14 章 内核调试技术

### 本章内容

- 内核调试的挑战 第 352 页
- 使用 KGDB 进行内核调试 第 353 页
- 调试 Linux 内核 第 360 页
- 硬件辅助调试 第 385 页
- 无法启动 第 392 页
- 章节总结 第 397 页

实现开发进度的关键因素在于查找和修复 bug 的效率。在 Linux 内核内部进行调试可能非常有挑战性。无论你采用何种方法，内核调试始终是复杂的。本章将探讨其中的一些复杂性，并提出提高你在内核和设备驱动内部调试技能的想法和方法。

## 14.1 内核调试的挑战

调试现代操作系统涉及许多挑战。虚拟内存操作系统也有其独特的挑战。我们曾经可以使用在电路仿真器替换处理器的时代已经过去了。处理器已经变得极其复杂。此外，流水线架构掩盖了重要的代码执行细节，特别是因为总线上的内存访问可能与代码执行的顺序不同，特别是由于指令流的内部缓存。除非在非常粗的层面，否则无法将外部总线活动与处理器内部指令执行相关联。

在调试内核代码时你会遇到的一些挑战：

- Linux 内核代码在许多领域都针对执行速度进行了高度优化。
- 编译器使用的优化技术增加了 C 源码与实际机器指令流之间关联的复杂度。内联函数（`inline functions`）就是一个很好的例子。
- 对优化后的代码进行单步执行通常会产生异常和意外的结果。
- 虚拟内存将用户空间与内核内存隔离，使得各种调试场景变得特别困难。
- 某些代码无法用传统的调试器轻松调试。
- 启动代码由于其接近硬件且可用资源有限（例如，没有控制台、内存映射有限等）而可能难以调试。

Linux 内核已经成熟为一种高性能的操作系统，能够与最好的商业操作系统竞争。内核中的许多区域并不易于通过阅读源代码进行分析。为了理解特定区域的代码流，通常需要架构和详细设计的知识。市上有许多书籍详细地描述了内核设计。请参阅第 14.6.1 节“扩展阅读建议”获取推荐。

GCC 是一个优化编译器。默认情况下，Linux 内核使用 `-O2` 编译器标志编译。这开启了许多优化算法，这些算法可以改变你代码的基本结构和顺序。[^1] 例如，内核大量使用内联函数。内联函数是用 `inline` 关键字声明的小型函数，这导致函数被直接包含在执行线程中，而不是生成函数调用以及相关的开销。[^2] 内联函数需要至少的 `-O1` 优化级别。因此，你可以关闭优化，这有利于更易于调试。

[^1]: 详阅本章末第 14.6.1 节“扩展阅读建议”中引用的 GCC 手册有关优化级别的详细信息。
[^2]: 内联函数类似于宏，但具有编译时类型检查的优势。

在 Linux 内核的许多区域中，单步执行代码是困难或不可能的。最明显的例子是修改虚拟内存设置的代码路径。当应用程序发出导致进入内核的系统调用时，会导致进程看到的地址空间发生变化。事实上，任何涉及处理器异常的转换都会改变操作上下文，并且可能难以或无法进行单步执行。

## 14.2 使用 KGDB 进行内核调试

两种流行的方法可以在 Linux 内核中实现符号源级调试：

- 使用 KGDB 作为远程 gdb 代理
- 使用硬件 JTAG 探针控制处理器

我们在[第 14.4 节](#144-硬件辅助调试)“硬件辅助调试”介绍 KGDB 调试。

KGDB (内核 GDB) 是一组 Linux 内核补丁，它们通过其远程串口协议提供到 gdb 的接口。KGDB 实现了一个与在你主机开发工作站上运行的交叉 gdb 通信的 gdb。直到最近，KGDB 目标还需要开发主机的串口连接，尽管这相对较新。KGDB 的完整支持尚未进入主线内核。你需要将 KGDB 移植到你选择的目标，或者获取支持 KGDB 的嵌入式 Linux 发行版。今天大多数嵌入式 Linux 发行版都支持 KGDB。

### 图 14-1 KGDB 调试设置

![](img/501695be171f31bb1c32748cf0cd783_341_0.png)

串口用于 KGDB 与运行在开发系统上的 gdb 之间的连接，可选串口作为控制台。只有一个串口的系统使用 KGDB 会变得相当麻烦。

如图 14-1 所示，调试器（你的交叉版本 gdb）运行在开发主机系统上。KGDB 是运行在目标系统上的内核的一部分。KGDB 实现了与目标板建立接口所需的钩子，以启用设置断点、检查内存和启用单步执行程序等功能。

### 14.2.1 KGDB 内核配置

KGDB 是一个内核功能，必须在你的内核中启用。如图 14-2 所示，从内核破解（Kernel Hacking）菜单选择 KGDB。作为配置的一部分，你必须选择 KGDB 使用的串口。注意图 14-2，我们开启了带调试信息编译内核的选项。这在构建过程中添加了 `-g` 编译器标志以启用符号调试。

### 图 14-2 用于 KGDB 的内核配置

![](img/501695be171f31bb1c32748cf0cd783_342_0.png)

在内核中包含 kgdb 钩子，Linux 内核源级调试器。更多信息请参阅 <http://kgdb.sourceforge.net/>。除非你打算调试内核，否则在此选 N。

## 14.2.2 支持 KGDB 的目标启动

在带有 KGDB 支持构建好内核后，必须将其启用。遗憾的是，启用它的方法在所有架构和实现中并不统一。通常情况下，通过在内核命令行向内核传递命令行开关来启用 KGDB。如果 KGDB 支持已编译进内核但未通过命令行开关启用，则它将不起作用。当启用 KGDB 时，内核会在启动循环的极早阶段停止在启用 KGDB 的断点处，允许你使用 gdb 连接到目标机。图 14-3 显示了启用 KGDB 时生成初始断点的逻辑。

### 图 14-3 KGDB 逻辑

![](img/501695be171f31bb1c327487cf0cd783_343_0.png)

KGDB 需要一个串口来连接到主机。设置 KGDB 的第一步是在启动过程的极早期启用串口。在许多架构中，硬件 UART 在访问之前必须映射到内核内存。地址映射后，将初始化串口。随后安装调试陷获处理程序，以允许处理器异常捕获到调试器中。

> [^2] 尽管之前对通过以太网运行 KGDB 有注释。

### 列表 14-1 使用 U-Boot 启用 KGDB 启动

```
=> setenv bootargs console=ttyS1,115200 root=/dev/nfs rw ip=dhcp gdb
=> bootm 200000
## Booting at 00200000 ...
Image Name: Linux-2.6.13
Image Type: PowerPC Kernel Image (gzip compressed)
Data Size: 1064790 Bytes = 1 MB
Load address: 00000000
Entry Point: 00000000
Verifying Checksum ... OK
Uncompressing Kernel Image ... OK
$T0440:c00ae5c;01:c0205fa0#99 See text
```

大部分序列与我们在第 7 章“引导加载程序”中对 U-Boot 的介绍是相似的。该内核序列有两个独特之处：启用 KGDB 的命令行参数，以及内核解压后看起来奇怪的文本字符串。

回想第 7 章，内核命令行是由 `bootargs` 环境变量定义的。注意，我们添加了 `gdb` 参数，该参数指示内核强制提前断点，并让主机调试器（你的交叉 gdb）进行连接。

如图 14-3 详细所示，内核检测到 `gdb` 参数的存在，并尝试将控制权交给远程（基于主机的）调试器。这通过转到串口的 ASCII 字符序列得到了证明，它记录在本章末尾引用的 gdb 手册中。在此示例中，如果你对 `gdb` 远程协议感兴趣，可以在列表 14-1 中查看。KGDB 正在发送一个停止回复包（Stop Reply packet），向主机上的远程 gdb 会话报告断点陷获。两个 32 位参数表示程序和栈帧的位置。

现在内核已设置好并等待主机调试器，我们可以开始调试会话。从我们的主机开发工作站调用交叉 gdb，并通过 gdb 远程协议连接到目标机。在此示例中，我们正在共享串口，因此必须断开终端与目标机的连接，以便尝试用 gdb 连接。列表 14-2 强调了 gdb 连接过程。这假设我们已经退出了终端并释放了串口供 gdb 使用。

### 列表 14-2 连接到 KGDB

```
$ PPC_4xx-gdb --silent vmlinux
(gdb) target remote /dev/ttyS0
Remote debugging using /dev/ttyS0
breakinst () at arch/ppc/kernel/ppc-stub.c:825
825
}
(gdb) l
820
return;
821
822
823
asm(" .global breakinst \
824
breakinst: .long 0x7d821008");
825
}
826
827
#ifdef CONFIG_GDB_CONSOLE
/* Output string in GDB O-packet format if GDB has connected.
828 If nothing
829
    output, returns 0 (caller must then handle output). */
(gdb)
```

我们执行了这些操作：

- 调用 gdb，并将其传递给内核 `vmlinux`
- 在 gdb 内部使用 `target remote` 命令连接到目标机
- 发出 `list` 命令，使用其缩写形式显示我们在源代码中的位置

虽然说这些可能有些显而易见，但我们传递给 gdb 的 `vmlinux` 镜像必须来自生成目标内核的同一个内核。它还必须使用 `-g` 编译器标志编译以包含调试信息。

当我们执行 `target remote` 命令时，gdb 通过显示程序计数器（PC）的位置做出响应。在这种情况下，内核停在由 `arch/ppc/kernel/ppc-stub.c` 第 823 行内联汇编语句定义的断点处。

## 14.2.3 有用的断点

你发现自己在步进内核代码的常见原因之一是为了修改你特定板的代码。让我们看看如何使用 AMCC Yosemite 板进行操作。我们在平台特定的架构函数处放置断点，并继续直到遇到该断点。

### 列表 14-3 设置断点

```
(gdb) b panic
Breakpoint 1 at 0x16de8: file kernel/panic.c, line 74.
(gdb) b sys_sync
Breakpoint 2 at 0x5bd5c: file fs/buffer.c, line 296.
(gdb) info breakpoints
Num Type Disp Enb Address What
1 breakpoint keep y 0x0016de8 in panic at kernel/panic.c:74
2 breakpoint keep y 0x005bd5c in sys_sync at fs/buffer.c:296
(gdb)
```

### 列表 14-4 调试架构设置代码

```
(gdb) b yosemite_setup_arch
Breakpoint 3 at 00c2148: file arch/ppc/platforms/4xx/yosemite.c, line 308.
(gdb) c
Continuing.
Can't send signals to this remote system. SIGILL not sent.
Breakpoint 3, yosemite_setup_arch () at arch/ppc/platforms/4xx/yosemite.c:308
yosemite_set_emacada();
}
static void __init
yosemite_setup_arch(void)
{
yosemite_set_emacada();
ibm440q_get_clocks(&clocks, YOSEMITE_SYCLK, 6 * 1843200);
oc_sys_info.opb_bus_freq = clocks->obj;
```

### 14.2.4 gdb 远程串口协议

gdb 允许一个调试开关，使我们能够观察 gdb 在开发主机和目标机上使用的远程协议。这对于理解底层协议以及排除表现出异常或错误行为目标机的故障非常有用。要启用此调试模式，执行以下命令：

```
(gdb) set debug remote 1
```

在远程调试中，观察 `continue` 命令的执行过程以及 gdb 采取的步骤非常有启发性。列表 14-5 展示了在启用远程调试时使用 `continue` 命令。

### 列表 14-5 continue 远程协议示例

```
(gdb) c
Continuing.
Sending packet: $Mc0000000,4#80...Ack
Packet received: c022d20
Sending packet: $Mc0000000,4:7d82108#68...Ack
Packet received: OK
Sending packet: $Mc0016de8,4#f8...Ack
Packet received: 3860001
Sending packet: $Mc0016de8,4:7d82108#e0...Ack
Packet received: OK
Sending packet: $Mc005bd5c,4#23...Ack
Packet received: 3860001
Sending packet: $Mc005bd5c,4:7d82108#0b...Ack
Packet received: OK
Sending packet: $Mc021a488,4#c...Ack
Packet received: 4bffbad
Sending packet: $Mc021a488,4:7d82108#b0...Ack
Packet received: OK
Sending packet: $<#63...Ack
>>> program running, gdb waiting for event
```

虽然起初看起来很复杂，但这里发生的情况很容易理解。总而言之，gdb 正在恢复目标机上的断点。回想列表 14-3，我们设置了两个断点，一个在 `panic()`，另一个在 `sys_sync()`。稍后的列表 14-4 中，我们在 `yosemite_setup_arch()` 处添加了第三个断点。因此，有三个活跃的用户指定的断点可以使用 `gdb info breakpoints` 显示。像往常一样，我们使用了缩写版本。

```
(gdb) i b
Num Type Disp Address What
1 breakpoint keep y 0x0016de8 in panic at kernel/panic.c:74
2 breakpoint keep y 0x005bd5c in sys_sync at fs/buffer.c:296
3 breakpoint keep y 0x021a488 in yosemite_setup_arch at arch/ppc/platforms/4xx/yosemite.c:308 breakpoint already hit 1 time
(gdb)
```
