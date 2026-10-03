
要在目标机器上安装 `dmalloc` 库，请将其放在你喜欢的位置（可能是 `/usr/local/lib`）。你可能需要让系统找到该库。我们将 `/usr/local/lib` 添加到 `/etc/so.conf` 并运行 `ldconfig` 更新缓存。

最后一步是设置 `dmalloc` 库使用的环境变量。它可能如下：

```
DMALLOC_OPTIONS=debug=0xfed0,inter=100,log=dmalloc.log
```

在这里，`debug` 是调试掩码，`inter` 设置了 `dmalloc` 执行自身检查的间隔。`dmalloc` 库将其跟踪写入 `log` 指定的文件。

`dmalloc` 软件包带有一个工具可以根据传递给它的标志生成 `DMALLOC_OPTIONS`。软件包中的文档详细说明了这一点，我们这里不再重复。上面的示例是用以下 `dmalloc` 调用生成的：

```
$ dmalloc -p check-fence dmalloc.log -i 100
```

完成这些步骤后，你应该可以使用 `dmalloc` 库运行你的应用程序。

`dmalloc` 会产生详细的输出。列表 13-13 显示了故意产生内存泄漏的示例 `dmalloc` 输出。

## 列表 13-13 dmalloc 输出

```
2592: 4002: dmalloc version '5.4.2' from 'http://dmalloc.com/'
2592: 4002: flags = 0x4fe53, logfile 'dmalloc.log'
2592: 4002: interval = 100, addr = 0, seen = 0
2592: 4002: starting time = 2592
2592: 4002: process pid = 442
2592: 4002: Dumping Chunk Statistics:
2592: 4002: basic-block 4096 bytes, alignment 8 bytes
2592: 4002: heap address range: 0x30015000 to 0x3004f000, 237568 bytes
2592: 4002: user blocks: 18 blocks, 73652 bytes (38%)
2592: 4002: admin blocks: 29 blocks, 118784 bytes (61%)
2592: 4002: total blocks: 47 blocks, 192512 bytes
2592: 4002: heap checked 41
```

# 352 页 第13章 开发工具

列表 13-13 续

```
2592: 4002: alloc calls: malloc 2003, calloc 0, realloc 0, free 1999
2592: 4002: alloc calls: recalloc 0, memalign 0, valloc 0
2592: 4002: alloc calls: new 0, delete 0
2592: 4002: current memory in use: 52 bytes (4 pnts)
2592: 4002: total memory allocated: 27546 bytes (2003 pnts)
2592: 4002: max in use of time: 27546 bytes (2003 pnts)
2592: 4002: max allocated with 1 call: 376 bytes
2592: 4002: max unused memory space: 37542 bytes (57%)
2592: 4002: top 10 allocations:
2592: 4002: total-size in-use count source
2592: 4002: 1600 1000 32 mtest_ex.c:36
2592: 4002: 10880 1000 20 mtest_ex.c:74
2592: 4002: 256 1 0 mtest_ex.c:154
2592: 4002: 27146 0 52 4 Total of 3
2592: 4002: Dumping Not-Free leaks Changed Start:
2592: 4002: not free: '0x300204e8s1' (10 bytes) from mtest_ex.c:74
2592: 4002: not free: '0x300205d8s1' (16 bytes) from mtest_ex.c:36
2592: 4002: not free: '0x300206e8s1' (16 bytes) from mtest_ex.c:36
2592: 4002: not free: '0x300208a8s1' (10 bytes) from mtest_ex.c:74
2592: 4002: total-size count source
2592: 4002: 32 2 mtest_ex.c:36
2592: 4002: 20 2 mtest_ex.c:74
2592: 4002: 52 4 Total of 2
2592: 4002: ending time = 2592, elapsed since start = 0:00:00
```

值得注意的是，此日志是在程序退出时生成的（`dmalloc` 有许多选项和运行模式；可以配置 `dmalloc` 在检测到错误时打印信息）。

输出日志的前半部分报告了关于堆和应用程序整体内存使用的高级统计数据。对于每个 `malloc` 库调用（如 `malloc()`、`free()` 和 `realloc()`），都会生成总数。有趣的是，此默认日志报告了前十次分配以及它们发生的源代码位置。这对于系统级别的性能分析非常有帮助。

在日志的末尾，我们看到了应用程序中存在内存泄漏的证据。你可以看到 `dmalloc` 库检测到了四个已分配但从未释放的内存实例。我们包含了 `dmalloc.h` 并使用调试符号进行编译，`dmalloc` 将分配内存的源代码位置记录在了日志中。

与我们在本章中介绍的其他工具一样，由于空间限制，这里对这个非常强大的调试工具进行简要介绍。`dmalloc` 可以检测许多其他情况和限制。例如，`dmalloc` 可以检测已释放的指针是否被写入。它可以判断指针是否被用于访问其边界之外但在应用程序允许的地址范围内的数据。事实上，`dmalloc` 可以配置为通过 `malloc` 调用链记录几乎任何内存事务。`dmalloc` 是一个需要投入数倍努力才能精通的工具。

## 13.4.8 Kernel Oops

虽然内核 oops 严格来说不是一种工具，但它包含了许多有助于排除故障原因的有用信息。内核 oops 源于各种内核错误，从进程产生的简单内存错误（大多数情况下可以完全恢复）到内核恐慌。最近的 Linux 内核支持显示原始十六进制值之外的符号信息。列表 13-14 显示了一个来自 Power Architecture 目标的内核 oops。

### 列表 13-14 Kernel Oops 显示

```
$ kernel access of bad area, sig: 11 [#]
IP: C00D058 LR: C08B560 SP: C7787E80 REGS: c7787dd0 TRAP: 0300 Not tainted
MSR: 00009032 EE: PR 1 FP: 0 ME: 1/DR: 11
DAR: 00000000, DISR: 220000
TASK = c7d8tb0[32] 'modprobe' THREAD: c778600
Last syscall: 128
PR00: 000000C6 C7787E80 C7D1B80 00000000 C7D2C5 FFFFFFFF 00000000 808080
PR08: 00000001 C03A4D30 C0D2C30 C1A4D30 C0335A80 101E23C0 00000000 00000000
PR16: 00000000 0000000 10001000 0D1E30 C9040000 C09D3F80 C0000000
PR24: 00000000 C9040000 C0040000 00000940 C778A400 C7CD25C0 C0CD25C0
IP [c008560] register+0x10/*xf0
LR [c008560] register_link:0exc/xf0
Call trace:
[c00e7c0] add_stack+0x58/0x74
[c90061e0] loop_init+0x1e/0x30 [loop]
[c002fc90] sys_init_module+0x1f4/0x20
[c0004a0] ret_from_syscall+0x0/0x44
```

注意寄存器转储包含了相应的符号信息。你的内核必须启用 `KALLSYMS` 以获取符号信息。图 13–4 显示了通用设置下的选项。

| 文件 | 选项 | 帮助 | | |
|---|---|---|---|---|
| Back | Load | Save | Split | Expand |
| Options | EMBEDDED | | | |
| ☑ Configure standard kernel features (small systems) KALLSYMS | | | |
| ☑ Load all symbols for debugging/kallsyms KSYMS_ALL | | | | |
| ☐ Include all symbols in kallsyms KSYMS_EXTRA | | | | |
| ☐ Do an error kallsyms pass | | | | |

13–4 oops符号支持

内核 oops 消息中的大部分信息与进程直接相关。完全理解 oops 消息需要具备底层架构知识。分析列表 13-14 中的 oops，我们立即看到 oops 是由于“kernel access of bad area, sig: 11”产生的。从之前的架构示例已经知道信号 11 是段错误。

第一部分是摘要，显示了 oops 的原因、几个重要的指针以及出错的任务。在列表 13-14 中，`NIP` 是下一条指令指针，在 oops 消息中后解码指向了 oops。`LR` 是 Power Architecture 寄存器，通常指示当前执行的子程序的返回地址。`SP` 是栈指针。`REGS` 表示寄存器转储数据的内核地址。`TRAP` 指明此消息相关的异常类型。参考第 7 章“引导加载程序”末提到的 PowerPC 架构手册，我们看到 `TRAP 0300` 是数据存储中断，由内存访问错误触发。

在 oops 消息的第三行，我们看到了额外的 Power Architecture 寄存器，如 `MSR`（状态寄存器）及其位解码。在下一行，我们看到了 `DAR`（数据访问寄存器），它通常包含出错的内存地址。`ISR` 寄存器的内容可以结合 PowerPC 架构引用来发现异常的具体原因。

oops 消息还包含任务指针和解码后的任务名称，有助于快速确定 oops 发生时正在运行的任务或线程。我们也看到了详细的处理器寄存器转储，可以作为额外的线索。同样，我们需要架构和编译器寄存器使用的知识来理解寄存器值的线索。例如，PowerPC 架构使用 `r3` 寄存器作为 C 函数返回值。

如果内核启用了符号，oops 消息的最后提供了带符号的回溯。使用这些信息，我们可以构建导致故障状况的事件序列。

在这个简单的示例中，我们从这个 oops 消息中学了大量信息。我们知道它是 Power Architecture 数据异常，是由数据内存访问错误（而不是指令取内存访问错误）引起的。`DAR` 寄存器告诉我们产生此异常的数据地址是 `0x0000_0000`。我们通过 `modprobe` 和 `NIP`（下一条指令指针）知道它是在 `strcpy()` 的调用中，这可以直接追溯到发生异常时的 `loop_init()` 函数。在 `loop.ko` 模块中，`modprobe` 在发生异常时正尝试插入。给定这些信息，追踪此空指针解引的源应该是应该是的。

## 13.5 二进制工具

二进制工具（或 `binutils`）是任何工具链的关键组件。事实上，要构建编译器，你必须首先构建 `binutils`。本节简要介绍了嵌入式开发者需要了解的有用工具。与本章中的大多数工具一样，这些是交叉工具，必须构建为在你的开发主机上运行，同时处理针对所选架构的二进制文件。或者，你可以编译或获取这些工具的版本运行在目标上，但我们假设示例使用的是交叉开发环境。

### 13.5.1 readelf

`readelf` 工具检查你的目标 ELF 二进制文件的组成。这对于构建需要显式控制布局的 ROM 或 Flash 内存镜像特别有用。它也是学习你的工具链如何构建镜像以及理解 ELF 文件格式的绝佳工具。

例如，要显示 ELF 镜像中的符号表，使用以下命令：

```
readelf -s <elf-image>
```

要发现并显示镜像中的所有节，请使用此命令：

```
$ readelf -e <elf-image>
```

使用 `-s` 标志列出 ELF 映像中的节头部。你可能会惊讶地发现，即使是一个简单的七行“Hello World”程序也包含 38 个独立的节。其中一些对你来说很熟悉，例如 `.text` 和 `.data` 节。列表 13-15 包含了来自我们的“Hello World”示例的部分的节列表。为了简单起见，我们只列出了嵌入式开发人员可能熟悉或相关的节。

### 列表 13-15 readelf 节头部

```
$ ppc82xx-readelf -S hello-ex
There are 38 section headers, starting at offset 0x32f4:
```

节头部：

| Nr | Name | Type | Addr | Off | Size | ES Flg | Lk Inf | Al |
|---|---|---|---|---|---|---|---|---|
| [11] | .text | PROBITS | 100002f0 | 0002f0 | 000568 | AX | 0 | 0 | 4 |
| [13] | .rodata | PROBITS | 10000878 | 000878 | 000068 | A | 0 | 0 | 4 |
| [15] | .data | PROBITS | 100108e0 | 0008e0 | 00000c | WA | 0 | 0 | 4 |
| [22] | .sdata | PROBITS | 100109e0 | 0009e0 | 00011c | WA | 0 | 0 | 4 |
| [23] | .sbss | NOBITS | 100109cf | 0009fc | 000000 | WA | 0 | 0 | 1 |
| [25] | .bss | NOBITS | 10010a74 | 0009fc | 00011c | WA | 0 | 0 | 4 |

`.text` 节包含可执行的程序代码。`.data` 节通常包含 C 库序言代码使用的初始化全局数据，并可以包含来自你应用程序的大型初始化数据项。`.sdata` 节用于较小的初始化全局数据项，且仅于某些架构上。当内存区域的属性已知时，处理器架构将利用优化的数据访问。`.data` 和 `.bss` 节实现了这些优化。`.bss` 节包含程序中的未初始化数据。这些节在程序映像中不占用空间。它们的内存空间由 C 库序言代码在程序启动时被分配并初始化为 0。

我们可以转储这些节中的任何一个并显示其内容。给定你 C 程序中在任何函数之外声明的这一行代码，我们可以检查它是如何放置在 `.rodata` 节中的：

```
char *hello_rodata = "This is a read-only data string\n";
```

执行 `readelf` 命令，并从列表 13-15 中指定我们想要转储的节：

```
$ ppc_82xx-readelf -x 13 hello-ex
dump of section '.rodata':
0x01000878 00181920 10000488 1000050c 1000058c
0x01000888 00020001 54686974 20697320 61207265 ...This is a read-
0x01000898 61642d6f 6e6c7920 64617461 20737472 only data string
0x010008a8 69a6e7a0 00000000 54686974 20697320 ...This is
0x010008b8 73741674 69630264 61741610 00000000 static data...
0x010008c8 4856c5c6 62f02453 6564a0a0 Hello Embedded...
0x010008d8 25730a00 25780a00                               %s..%x.
```

我们看到声明的初始化变量表示在 `.rodata` 节中，其中包含了程序定义的所有常量字符串。

## 13.5.2 使用 readelf 检查调试信息

`readelf` 更有用的功能之一是显示 ELF 文件包含的调试信息。当在编译期间发出 `-g` 编译器标志时，编译器会在生成的 ELF 文件中的一系列节中生成调试信息。我们可以使用 `readelf` 头部显示这些节：
