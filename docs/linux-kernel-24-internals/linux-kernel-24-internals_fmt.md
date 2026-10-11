
# Linux 内核 2.4 深入剖析

**Tigran Aivazian** `tigran@veritas.com`

Linux 2.4 内核入门。本文档的最新副本始终可以从以下地址下载：[http://www.moses.uklinux.net/patches/klc.sgm](http://www.moses.uklinux.net/patches/klc.sgm)。本指南现在是 Linux 文档项目的一部分，也可以从以下地址下载各种格式的版本：[http://www.linuxdoc.org/guides.html](http://www.linuxdoc.org/guides.html) 或在线阅读（最新版本）：[http://www.moses.uklinux.net/patches/klc.html](http://www.moses.uklinux.net/patches/klc.html)。

本文档是自由软件；你可以按照自由软件基金会发布的 GNU 通用公共许可协议的条款重新分发和/或修改它；要么是许可证的第 2 版，或者（按你的选择）任何后续版本。

作者目前在 `VERITAS Software Ltd` 担任高级 Linux 内核工程师，并撰写了这本书，目的是支持他在 `VERITAS` 内部就这一主题所做的短期培训/讲座。

感谢以下人员提供的各种更正和建议：`Juan J. QuinTELA` (`quintela@fi.udc.es`), `Francis Galiegue` (`fg@mandrakesoft.com`), `Hakjun Mun` (`juniofm@orgio.net`), `Matt Kraai` (`kraai@alumni.carnegiemellon.edu`), `Nicholas Dronen` (`mdronen@froi.com`), `Samuel S Chessman` (`chessman@tux.org`), `Nadeem Hasan` (`nhasan@nadm.com`)。

Linux 页面缓存章节由 `Christoph Hellwig` (`ch@exacer.de`) 撰写。IPC 机制章节由 `Russel Weight` (`weight@rs.ibm.com`) 和 `Mingming Cao` (`mcao@us.ibm.com`) 撰写。

## 1. 引导

- [1.1 构建 Linux 内核镜像](#1.1-building-the-linux-kernel-image)
- [1.2 引导：概览](#1.2-booting-overview)
- [1.3 引导：BIOS POST](#1.3-booting-bios-post)
- [1.4 引导：引导扇区与设置](#1.4-booting-bootsector-and-setup)
- [1.5 使用 LILO 作为引导加载程序](#1.5-using-lilo-as-a-bootloader)
- [1.6 高级初始化](#1.6-high-level-initialisation)
- [1.7 x86 架构下的 SMP 启动](#1.7-smp-bootup-on-x86)
- [1.8 释放初始化数据和代码](#1.8-freeing-initialisation-data-and-code)
- [1.9 处理内核命令行](#1.9-processing-kernel-command-line)

## 2. 进程与中断管理

- [2.1 任务结构与进程表](#2.1-task-structure-and-process-table)
- [2.2 任务与内核线程的创建与终止](#2.2-creation-and-termination-of-tasks-and-kernel-threads)
- [2.3 Linux 调度器](#2.3-linux-scheduler)
- [2.4 Linux 链表实现](#2.4-linux-linked-list-implementation)
- [2.5 等待队列](#2.5-wait-queues)
- [2.6 内核定时器](#2.6-kernel-timers)
- [2.7 下半部 (Bottom Halves)](#2.7-bottom-halves)
- [2.8 任务队列](#2.8-task-queues)
- [2.9 任务片 (Tasklets)](#2.9-tasklets)
- [2.10 软中断 (Softirqs)](#2.10-softirqs)
- [2.11 系统调用在 i386 架构中是如何实现的？](#2.11-how-system-calls-are-implemented-on-i386-architecture)

### 1.1 构建 Linux 内核映像

本节说明了编译 Linux 内核期间执行的步骤以及每个阶段产生的输出。构建过程取决于体系结构，因此我想强调我们只考虑构建 Linux/x86 内核。

当用户输入 `make zImage` 或 `make bzImage` 时，生成的可引导内核映像分别存储为 `arch/i386/boot/zImage` 或 `arch/i386/boot/bzImage`。映像的构建方式如下：

1. `C` 和汇编源文件被编译为 `ELF` 可重定位对象格式（`.o`），其中一些使用 `ar(1)` 在逻辑上分组为归档（`.a`）。

2. 使用 `ld(1)`，将上述 `.o` 和 `.a` 链接为 `vmlinux`，这是一个静态链接、未剥离的 `ELF` 32 位 `LSB` 80386 可执行文件。

3. 通过 `nm vmlinux` 生成 `System.map`，并使用 `grep` 过滤掉无关或无趣的符号。

4. 进入目录 `arch/i386/boot`。

5. 引导扇区汇编代码 `bootsect.S` 根据目标是 `bzImage` 还是 `zImage`，分别使用或不使用 `–D__BIG_KERNEL__` 进行预处理，生成 `bootsect.s` 或 `bootsect.s`。

6. `bbootsect.s` 被汇编，然后转换为称为 `bbootsect` 的“原始二进制”形式（对于 `zImage`，则是 `bootsect.s` 汇编并原始转换为 `bootsect`）。

7. 设置代码 `setup.S`（`setup.S` 包含 `video.S`）被预处理为 `bZImage` 的 `bsetup.s` 或 `zImage` 的 `setup.s`。与引导扇区代码一样，`bZImage` 中存在 `-D_BIG_KERNEL_` 标记来标示差异。结果随后转换为称为 `bsetup` 的“原始二进制”形式。

8. 进入目录 `arch/i386/boot/compressed`，将 `/usr/src/linux/vmlinux` 转换为原始二进制格式的 `$tmpiggy`（临时文件名），并移除 `.note` 和 `.comment` `ELF` 段。

9. `gzip -9 < $tmpiggy > $tmpiggy.gz`

10. 将 `$tmpiggy.gz` 链接为 `ELF` 可重定位文件（`ld -r`）`piggy.o`。

11. 将压缩例程 `head.S` 和 `misc.c`（仍在 `arch/i386/boot/compressed` 目录中）编译为 `ELF` 对象 `head.o` 和 `misc.o`。

12. 将 `head.o`、`misc.o` 和 `piggy.o` 一起链接为 `bvmlinux`（对于 `zImage` 则为 `vmlinux`，请勿将此与 `/usr/src/linux/vmlinux` 混淆！）。注意用于 `vmlinux` 的 `-Ttext 0x1000` 与用于 `bvmlinux` 的 `-Ttext 0x10000` 之间的区别，即 `bZImage` 的压缩加载器被高加载。

13. 将 `bvmlinux` 转换为“原始二进制” `bvmlinux.out`，移除 `.note` 和 `.comment` `ELF` 段。

14. 返回 `arch/i386/boot` 目录，使用程序 `tools/build`，将 `bbootsect`、`bsetup` 和 `compressed/bvmlinux.out` 拼接为 `bZImage`（对于 `zImage`，删除上述多余的 `b`）。这会在引导扇区末尾写入诸如 `setup_sects` 和 `root_dev` 等重要变量。

引导扇区的大小始终为 512 字节。设置的大小必须大于 4 个扇区，但上限约为 12K – 规则如下：

`0x4000 bytes >= 512 + setup_sects * 512 + room for stack while running bootsector/setup`

我们稍后将看到这一限制从何而来。

此步骤产生的 `bZImage` 大小上限约为 2.5M（使用 `LILO` 引导时），或使用原始映像引导（例如从软盘或 `CD-ROM`（`El-Torito` 模拟模式）引导时为 `0xFFFF` 段（`0xFFFF0 = 1048560` 字节））。

请注意，虽然 `tools/build` 会验证引导扇区、内核映像的大小以及设置大小的下限，但它不会检查上述设置大小的*上限*。因此，只需在 `setup.S` 末尾添加一些大的 `.space`，就很容易构建出一个损坏的内核。

### 1.2 引导：概述



引导过程的细节取决于体系结构，因此我们将重点关注 IBM PC/IA32 体系结构。由于旧设计和向后兼容性，PC 固件以一种老式的方式引导操作系统。此过程可以分为以下六个逻辑阶段：

1. `BIOS` 选择引导设备。
2. `BIOS` 从引导设备加载引导扇区。
3. 引导扇区加载 `setup`、解压缩例程和压缩的内核映像。
4. 内核在保护模式下解压缩。
5. 汇编代码执行底层初始化。
6. 高级 C 初始化。

### 1.3 引导：BIOS POST

1. 电源启动时钟发生器，并在总线上断言 `#POWERGOOD` 信号。
2. 断言 `CPU #RESET` 线（CPU 现在处于真实的 `8086` 模式）。
3. `%ds=%es=%fs=%gs=%ss=0, %cs=0xFFFF0000, %ip = 0x0000FFF0`（ROM BIOS POST 代码）。
4. 所有 POST 检查均在中断禁用的情况下执行。
5. 中断向量表（`IVT`）在地址 `0` 处初始化。
6. 通过 `int 0x19` 调用 `BIOS` 引导加载器功能，`%dl` 包含引导设备的“驱动器号”。这在物理地址 `0x7C00`（`0x07C:0000`）处加载 `0` 磁道、`1` 扇区。

### 1.4 引导：bootsector 和 setup

用于引导 Linux 内核的 `bootsector` 可以是：

- Linux `bootsector`（`arch/i386/boot/bootsect.S`），
- `LILO`（或其他启动加载器的）`bootsector`，或者
- 没有 `bootsector`（如 `loadlin` 等）

在这里，我们详细讨论 Linux `bootsector`。前两行初始化了用于段值的便利宏：

```
29 SETUPSECS = 4 /* default nr of setup-sectors */
30 BOOTSEG = 0x07C0 /* original address of boot-sector */
31 INITSEG = DEF_INITSEG /* we move boot here – out of the way */
32 SETUPSEG = DEF_SETUPSEG /* setup starts here */
33 SYSSEG = DEF_SYSSEG /* system loaded at 0x10000 (65536) */
34 SYSSIZE = DEF_SYSSIZE /* system size: # of 16-byte clicks */
```

（左侧的数字是 `bootsect.S` 文件的行号）`DEF_INITSEG`、`DEF_SETUPSEG`、`DEF_SYSSEG` 和 `DEF_SYSSIZE` 的值取自 `include/asm/boot.h`：

```
/* Don't touch these, unless you really know what you're doing. */
#define DEF_INITSEG 0x9000
#define DEF_SYSSEG 0x1000
#define DEF_SETUPSEG 0x9020
#define DEF_SYSSIZE 0x7F00
```

现在，让我们看看 `bootsect.S` 的实际代码：

```
54 movw $BOOTSEG, %ax
55 movw %ax, %ds
56 movw $INITSEG, %ax
57 movw %ax, %es
58 movw $256, %cx
59 subw %si, %si
60 subw %di, %di
61 cltd
62 rep
63 movsw   $go
64 ljmp    $INITSEG,

65 # bde - changed 0xff00 to 0x4000 to use debugger at 0x6400 up (bde). We
66 # wouldn't have to worry about this if we checked the top of memory. Also
67 # my BIOS can be configured to put the wfi drive tables in high memory
68 # instead of in the vector table. The old stack might have clobbered the
69 # drive table.

70 go:
        movw    $0x4000-12, %di        # 0x4000 is an arbitrary value >=
                                       # length of bootsect + length of
72                                       # setup + room for stack;
73                                       # 12 is disk parm size.
74                movw    %ax, %ds
75                movw    %ax, %ss
76                movw    %di, %sp      # put_stack at INITSEG:0x4000-12.
```

第 54–63 行将 `bootsector` 代码从地址 `0x7C00` 移动到 `0x9000`。这是通过以下步骤实现的：

1. 将 `%ds:%si` 设置为 `$BOOTSEG:0`（`0x7C0:0 = 0x7C00`）
2. 将 `%es:%di` 设置为 `$INITSEG:0`（`0x9000:0 = 0x90000`）
3. 将 16 位字的数量设置在 `%cx` 中（`256` 字 = `512` 字节 = `1` 扇区）
4. 清除 `EFLAGS` 中的 `DF`（方向）标志以自动递增地址（`cld`）
5. 执行 `512` 字节的复制（`rep movsw`）

这段代码有意不使用 `rep movsd`（提示 – `.code16`）。

第 64 行跳转到新制作的 `bootsector` 副本中的标签 `go:`，即在段（`0x9000`）中。这条指令及接下来的三条指令（第 64–76 行）在 `$INITSEG:0x4000–0xC` 处准备堆栈，即 `%ss = $INITSEG (0x9000)` 且 `%sp = 0x3FF4 (0x4000–0xC)`。这就是我们前面提到的设置大小限制的来源（参见《构建 Linux 内核映像》）。

第 77–103 行修补第一个磁盘的磁盘参数表，以允许多扇区读取：

```
77 # Many BIOS's default disk parameter tables will not recognise
78 # multi-sector reads beyond the maximum sector number specified
79 # in the default diskette parameter tables - this may mean 7
80 # sectors in some cases.
81 #
82 # Since single sector reads are slow and out of the question,
83 # we must take care of this by creating new parameter tables
84 # (for the first disk) in RAM. We will set the maximum sector
85 # count to 36 - the most we will encounter on an ED 2.88.
86 #
87 # High doesn't hurt. Low does.
88 #
89 # Segments are as follows: ds = es = ss = cs - INITSEG, fs = 0,
90 # and gs is unused.

91                movw    %cx, %fs        # set fs to 0
92                movw    $0x78, %bx      # fs:bx is parameter table address
93                pushw   %ds
94                ldsq    fga:(%bx), %si # ds:si is source
95                movb    $6, %cl         # copy 12 bytes
```

## Linux 内核 2.4 内部机制

```
96     pushw    $di                   # di = 0x4000-12.

97     rep                     # 不需要 clid -> 已在第 66 行完成

98     movsw

99     popw    $di
```



```
100    popw    $ds

101    movb    $36, 0x4($di)           # 修补扇区计数

102    movw    $di, $fs:($bx)

103    movw    %es, $fs:2($bx)
```

软盘控制器通过使用 `BIOS` 服务 `int 0x13` 功能 `0`（重置 `FDC`）进行重置，而设置扇区（`setup` `sectors`）则在引导扇区加载后立即被加载，即位于物理地址 `0x90200`（`INTSEG:0x200`），再次使用 `BIOS` 服务 `int 0x13`，功能 `2`（读取扇区）。这发生在第 107-124 行：

```
107 load_setup:

108    xor b    % ah, % ah           # 重置 FDC

109    xor b    % dl, % dl

110    int      0x13

111    movw    0x00, % dx           # 驱动器 0，磁头 0

112    movb    0x02, % cl           # 扇区 2，磁道 0

113    movw    0x0200, % bx           # 地址 = 512，位于 INTSEG 中

114    movb    0x02, % ah           # 服务 2，“读取扇区”

115    movb    setup_sects, % al     # （假设全部在磁头 0，磁道 0 上）

116    int      0x13                # 读取它

117    jnc     ok_load_setup           # 成功 - 继续

118    pushw    % ax                   # 转储错误代码

119    call    print_n 1

120    movw    % sp, % bp

121    call    print_hex

122    popw    % ax

123    jmp     load_setup

124 ok_load_setup:
```

如果由于某种原因（软盘损坏或在操作过程中有人取出了软盘）导致加载失败，我们将转储错误代码并在无限循环中重试。唯一的退出方法是重启机器，除非重试成功，但通常不会成功（如果出了问题，情况只会变得更糟）。

如果成功加载了 `setup_sects` 个扇区的设置代码，则跳转到标签 `ok_load_setup`。

然后我们继续加载位于物理地址 `0x10000` 的压缩内核镜像。这样做是为了保留低内存（`0-64k`）中的固件数据区域。内核加载完成后，我们跳转到 `SETUPSEG:0`（`arch/i386/boot/setup.S`）。一旦不再需要这些数据（例如，不再调用 `BIOS`），通过将从 `0x10000` 移动到 `0x1000` 的整个（压缩的）内核镜像来覆盖它们（物理地址，当然是）。这是由 `setup.S` 完成的，它设置了保护模式并跳转到 `0x1000`，即压缩内核的头部，也就是 `arch/i386/boot/compressed/head.S, misc.c`）。这会设置堆栈并调用 `decompress_kernel()`，该函数将内核解压到地址 `0x100000` 并跳转到该地址。

请注意，旧的加载器（旧版本的 `LILO`）只能加载 `setup` 的前 4 个扇区，这就是为什么如果需要在 `setup` 中有代码来加载其余部分的原因。此外，`setup` 中的代码必须处理加载器类型/版本与 `zImage/bzImage` 的各种组合，因此非常复杂。

让我们看看引导扇区代码中允许加载大型内核（也称为 `"bzImage"`）的怪招（`kludge`）。设置扇区通常加载在 `0x90200`，但内核使用特殊辅助例程一次加载 `64K` 块，该例程调用 `BIOS` 将数据从低内存移到高内存。该辅助例程在 `bootsect.S` 中称为 `bootsect_kludge`，在 `setup.S` 中定义为 `bootsect_helper`。`setup.S` 中的 `bootsect_kludge` 标签包含 `setup` 段的值以及其中 `bootsect_helper` 代码的偏移量，以便引导扇区可以使用 `lcall` 指令跳转到它（跨段跳转）。它位于 `setup.S` 中的原因 simply 是因为 `bootsect.S` 中没有更多空间了（严格来说这不正确 – `bootsect.S` 中大约有 4 个备用字节和至少 1 个备用字节，但这显然不够）。此例程使用 `BIOS` 服务 `int 0x15`（`ax=0x8700`）将数据移动到高级内存，并将 `%es` 重置为始终指向 `0x10000`。这确保了 `bootsect.S` 中的代码在从磁盘复制数据时不会用尽低内存。

### 1.5 使用 LILO 作为引导加载器

使用专用引导加载器（`LILO`）相比于简单的 `Linux` 引导扇区有几个优点：

- 能够在多个 `Linux` 内核甚至多个操作系统之间选择。
- 能够传递内核命令行参数（有一个名为 `BCP` 的补丁为简单的引导扇区+`setup` 增加了此功能）。
- 能够加载大得多的 `bzImage` 内核 – 高达 `2.5M` 对比 `1M`。
    - 旧版本的 `LILO`（`v17` 及更早版本）无法加载 `bzImage` 内核。较新的版本（几年前或更早）使用与 `bootsect+setup` 相同的技术，通过 `BIOS` 服务将数据从低内存移到高级内存。有些人（特别是 `Peter` `Anvin`）认为应该移除对 `zImage` 的支持。

据 `Alan` `Cox` 称，保留它的主要原因是，显然存在一些损坏的 `BIOS`，使得无法引导 `bzImage` 内核，而 `zImage` 内核可以正常引导。

`LILO` 做的最后一件事是跳转到 `setup.S`，然后事情按正常流程进行。

### 1.6 高层初始化

所谓“高层初始化”，我们指的是与引导（`bootstrap`）不直接相关的任何内容，尽管执行此操作的部分代码是用汇编编写的，即 `arch/i386/kernel/head.S`，它是未压缩内核的头部。执行以下步骤：

- 初始化段值（`%ds = %es = %fs = %gs = __KERNEL_DS = 0x18`）。
- 初始化页表。
- 通过设置 `%cr0` 中的 `PG` 位来启用分页。
- 清零 `BSS`（在 `SMP` 上，只有第一个 `CPU` 执行此操作）。
- 复制前 `2k` 的启动参数（内核命令行）。
- 使用 `EFLAGS` 检查 `CPU` 类型，如果可能，使用 `cpuid`，能够检测 `386` 及更高级别的 `CPU`。
- 第一个 `CPU` 调用 `start_kernel()`，如果 `ready=1`，其他所有 `CPU` 调用 `arch/i386/kernel/smpboot.c:initialize_secondary()`，该函数仅重新加载 `esp/eip` 并且不返回。

`init/main.c:start_kernel()` 是用 `C` 编写的，执行以下操作：

- 获取全局内核锁（需要它以确保只有一个 `CPU` 通过初始化过程）。
- 执行架构特定的设置（内存布局分析，再次复制启动命令行等）。
- 将包含版本、用于构建的编译器等信息的 `Linux` 内核“横幅”打印到内核消息环形缓冲区。这取自定义在 `init/version.c` 中的变量 `linux_banner`。
- 初始化陷阱（`traps`）。
- 初始化中断请求（`irqs`）。
- 初始化调度器所需的数据。
- 初始化时间记录数据。
- 初始化软中断（`softirq`）子系统。
- 解析启动命令行选项。
- 初始化控制台。
- 如果模块支持被编译进内核，初始化动态模块加载设施。
- 如果提供了 `"profile="` 命令行，初始化性能剖析缓冲区。
- `kmem_cache_init()`，初始化大部分 `slab` 分配器。
- 启用中断。
- 计算此 `CPU` 的 `BogoMips` 值。
- 调用 `mem_init()`，它计算 `max_mapnr`、`totalram_pages` 和 `high_memory` 并打印 `"Memory: ..."` 行。
- `kmem_cache_sizes_init()`，完成 `slab` 分配器的初始化。
- 初始化用于进程的数据结构。
- `fork_init()`，创建 `uid_cache`，基于可用内存量初始化 `max_threads`，并将 `init_task` 的 `RLIMIT_NPROC` 配置为 `max_threads/2`。
- 创建 `VFS`、`VM`、缓冲区缓存等所需的多个 `slab` 缓存。
- 如果编译了 `System` `V` `IPC` 支持，初始化 `IPC` 子系统。注意，对于 `System` `V` `shm`，这包括挂载一个内部的（内核中）`shmfs` 文件系统实例。
- 如果编译了配额（`quota`）支持，为其创建并初始化一个特殊的 `slab` 缓存。
- 执行架构特定的“缺陷检查”，并尽可能激活处理器/总线/其他缺陷的工作变通方法。比较各种架构发现“`ia64` 没有缺陷”而“`ia32` 有相当多的缺陷”，一个好例子是 “`f00f` `bug`”，它仅在针对少于 `686` 编译的内核中进行检查，并相应地进行变通处理。



- 设置一个标志，指示应在“下一个机会”调用调度，并创建一个内核线程 `init()`，如果通过 `"init="` 启动参数提供了 `execute_command`，则执行它；否则，依次尝试执行 `/sbin/init`、`/etc/init`、`/bin/init`、`/bin/sh`；如果所有这些失败，则引发 `panic`，并给出使用 `"init="` 参数的“建议”。

- 进入空闲循环，这是一个 `pid=0` 的空闲线程。

这里要注意的重要事情是，`init()` 内核线程调用 `do_basic_setup()`，进而调用 `do_initcalls()`，该函数遍历通过 `__initcall` 或 `module_init()` 宏注册的函数列表并调用它们。这些函数要么相互独立，要么它们的依赖关系已通过 `Makefile` 中的链接顺序手动修复。这意味着，根据目录在树中的位置以及 `Makefile` 的结构，初始化函数的调用顺序可能会改变。有时，这很重要，因为你可以想象两个子系统 `A` 和 `B`，其中 `B` 依赖于 `A` 完成的某些初始化。如果 `A` 是静态编译的，`B` 是一个模块，则 `B` 的入口点保证在 `A` 准备好所有必要环境后调用。如果 `A` 是一个模块，则 `B` 也必然是模块，因此没有问题。但如果 `A` 和 `B` 都静态链接到内核中怎么办？它们被调用的顺序取决于内核镜像中 `.initcall_init` ELF 段中的相对入口点偏移量。`Roger Wolfow` 提议引入一个分层“优先级”基础设施，使模块能够告知链接器它们应该以何种（相对）顺序链接，但目前还没有可用补丁以足够优雅的方式实现这一功能并被内核接受。因此，请确保你的链接顺序是正确的。如果在上述示例中，`A` 和 `B` 在静态编译时能正常工作，那么只要它们在同一个 `Makefile` 中顺序列出，它们将始终正常工作。如果它们不能正常工作，请更改其目标文件列出的顺序。

另一件值得注意的事情是，Linux 能够通过传递 `"init="` 引导命令行参数来执行一个“替代的 init 程序”。这在意外覆盖了 `/sbin/init` 时进行恢复，或者手动调试初始化 (rc) 脚本和 `/etc/inittab`（逐个执行它们）时非常有用。

## 1.7 x86 上的 SMP 引导

在 SMP（对称多处理）系统中，BP（引导处理器）会经历常规的启动扇区、`setup` 等序列，直到它到达 `start_kernel()`，然后进入 `smp_init()`，特别是 `src/i386/kernel/smpboot.c` 中的 `smp_boot_cpus()`。`smp_boot_cpus()` 会对每个 `apicd`（直到 `NR_CPUS`）进行循环，并调用 `do_boot_cpu()`。`do_boot_cpu()` 的作用是为目标 CPU 创建一个（即手动 `fork`）空闲任务，并在 Intel MP 规范定义的知名位置（`0x467`/`0x469`）写入 `trampoline.S` 中找到的跳板代码的 `EIP`。然后它向目标 CPU 生成 `STARTUP IPI`，使该 AP（应用程序处理器）执行 `trampoline.S` 中的代码。

引导 CPU 在低内存中为每个 CPU 创建跳板代码的一个副本。AP 代码在其自己的数据字中写入一个魔术数字，BP 会验证这个数字以确保 AP 正在执行跳板代码。Intel MP 规范强制要求跳板代码必须位于低内存中。

跳板代码只是将 `%bx` 寄存器设置为 1，进入保护模式，然后跳转到 `startup_32`，这是 `arch/i386/kernel/head.S` 的主入口点。

此时，AP 开始执行 `head.S`，并发现它不是 BP，于是跳过清除 `BSS` 的代码，然后进入 `initialize_secondary()`（它只是进入该 CPU 的空闲任务 – 回想一下，`init_tasks[cpu]` 已经由执行 `do_boot_cpu(cpu)` 的 BP 初始化了）。

请注意，`init_task` 可以共享，但每个空闲线程必须拥有自己的 `TSS`。这就是为什么 `init_tss[NR_CPUS]` 是一个数组的原因。

## 1.8 释放初始化数据和代码

当操作系统初始化自身时，大多数代码和数据结构之后再也不需要了。大多数操作系统（`BSD`、`FreeBSD` 等）无法处置这些不再需要的信息，从而浪费了宝贵的物理内核内存。它们使用的借口（参见 `McKusick` 的 `4.4BSD` 书籍）是“相关代码散布在各个子系统中，因此无法释放”。当然，Linux 不能使用这种借口，因为在 Linux 下“如果某事原则上是可能的，那么它要么已经实现，要么有人正在处理它”。

所以，正如我之前所说，Linux 内核只能编译为 `ELF` 二进制文件，现在我们找到了原因（或者原因之一）。与丢弃初始化代码/数据相关的原因是，Linux 提供了两个可供使用的宏：

- `__init` – 用于初始化代码
- `__initdata` – 用于数据

这些宏在 `include/linux/init.h` 中定义为 `gcc` 属性说明符（也被称为“`gcc` 魔法”）：

```c
#ifndef MODULE
#define __init    __attribute__ (( ".text.init" ))
#define __initdata __attribute__ (".data.init")
#else
#define __init
#define __initdata
#endif
```

这意味着，如果代码被静态编译到内核中（即 `MODULE` 未定义），那么它将被放置在特殊的 ELF 段 `.text.init` 中，该段在 `arch/i386/vmlinux.lds` 的链接器映射中被声明。否则（即如果是模块），这些宏将无效（不评估为任何内容）。

引导期间发生的事情是，“init”内核线程（函数 `init/main.c:init()`）调用特定于架构的函数 `free_initmem()`，该函数释放位于地址 `__init_begin` 和 `__init_end` 之间的所有页面。

在典型的系统（我的工作站）上，这会导致释放约 `260K` 的内存。

通过 `module_init()` 注册的函数被放置在 `.initcall.init` 中，在静态情况下也会被释放。当前 Linux 在设计和规划子系（不一定是模块）时的趋势是，在设计初期提供 init/exit 入口点，以便将来如果需要可以将相关子系模块化。一个例子是 pipe，参见 `fs/pipe.c`。即使给定的子系永远不会成为模块，例如 bdflush（参见 `fs/buffer.c`），只要函数的调用时机不重要，使用 `module_init()` 宏来处理其初始化函数仍然是一种整洁的做法。

还有两个工作方式类似的宏，称为 `__exit` 和 `__exitdata`，但它们与模块支持更直接相关，因此将在后面的章节中解释。

## 1.9 处理内核命令行

让我们回顾一下在引导期间传递给内核的命令行会发生什么：

1. `LILO`（或 `BCP`）使用 `BIOS` 键盘服务接受命令行，并将其存储在物理内存中的知名位置，同时也存储了一个签名，表明那里有一个有效的命令行。
2. `arch/i386/kernel/head.S` 将其前 `2k` 字节复制到 `zeropage`。注意，当前版本的 `LILO`（`21` 版本）将命令行截断为 `79` 字节。这是 `LILO` 的一个非平凡的 bug（当启用了大型 `EBDA` 支持时），`Werner` 承诺不久会修复它。如果你真的需要传递超过 `79` 字节的命令行，你可以使用 `BCP` 或者在 `arch/i386/kernel/setup.c:parse_mem_cmdline()` 函数中硬编码你的命令行。
3. `arch/i386/kernel/setup.c:parse_mem_cmdline()`（由 `setup_arch()` 调用，而 `setup_arch()` 本身由 `start_kernel()` 调用）将 `256` 字节从 `zeropage` 复制到 `saved_command_line`，该变量由 `/proc/cmdline` 显示。同一例程还处理 `"mem="` 选项（如果存在），并对 `VM` 参数进行适当调整。
4. 我们在 `parse_options()`（由 `start_kernel()` 调用）中返回到命令行，它处理一些“内核内部”参数（目前是 `"init="` 以及 init 的环境/参数），并将每个单词传递给 `checksetup()`。
5. `checksetup()` 遍历 ELF 段 `.setup.init` 中的代码并调用每个函数，如果匹配则传递该单词。注意，通过利用通过 `__setup()` 注册的函数返回值为 `0` 的特性，可以将同一个 `"variable=value"` 传递给多个函数，其中 `"value"` 对一个函数无效但对另一个有效。`Jeff Garzik` 评论道：“那样做的黑客会被揍的 :)"

为什么？因为这显然是依赖于链接顺序的，即按照一种顺序链接的内核会有 `functionA` 在 `functionB` 之前被调用，而另一种顺序则相反，结果取决于顺序。



那么，我们如何编写处理引导命令行的代码？我们使用在 `include/linux/init.h` 中定义的 `__setup()` 宏：

```c
/*
 * Used for kernel command line parameter setup
 */
struct kernel_param {
    const char *str;
    int (*setup_func)(char *);
};

extern struct kernel_param __setup_start, __setup_end;

#ifdef MODULE
#define __setup(str, fn) \
    static char __setup_str_##fn[] __initdata = str; \
    static struct kernel_param __setup_##fn __initsetup = \
        { __setup_str_##fn, fn }
#else
#define __setup(str,func) /* nothing */
#endif
```

因此，你通常在代码中这样使用它（取自真实驱动程序 BusLogic HBA `drivers/scsi/BusLogic.c` 的代码）：

```c
static int __init
BusLogic_Setup(char *str)
{
    int ints[3];

    (void)get_options(str, ARRAY_SIZE(ints), ints);

    if (ints[0] != 0)
        BusLogic_Error("BusLogic: Obsolete Command Line Entry "
                        "Format Ignored\n", NULL);
        return 0;

    if (str == NULL || *str == '\0')
        return 0;
    return BusLogic_ParseDriverOptions(str);
}

__setup("BusLogic=", BusLogic_Setup);
```

请注意，`__setup()` 对模块不起作用，因此希望处理引导命令行的代码如果是模块或静态链接的，必须在模块初始化例程中手动调用其解析函数。这也意味着，可以编写在编译为模块时处理参数但在静态编译时不处理（或反之）的代码。

## 2. 进程和中断管理

### 2.1 任务结构和进程表

Linux 下的每个进程都动态分配一个 `struct task_struct` 结构。在 Linux 上可以创建的最大进程数仅受现有物理内存量的限制，且等于（参见 `kernel/fork.c:fork_init()`：）

```c
/*
 *  The default maximum number of threads is set to a safe
 *  value: the thread structures can take up at most half
 *  of memory.
 */
max_threads = nr_pages / (THREAD_SIZE/PAGE_SIZE) / 2;
```

这基本上在 IA32 架构上意味着 `num_physpages/4`。举个例子，在 512M 的机器上，你可以创建 32k 个线程。这比旧内核（2.2 及更早版本）的 4k-epsilon 限制有了相当大的改进。此外，这可以使用 `KERN_MAX_THREADS` `sysctl(2)` 在运行时更改，或者简单地使用 `kernel` 可调整参数中的 `procs` 接口：

```bash
# cat /proc/sys/kernel/threads-max
32764
# echo 100000 > /proc/sys/kernel/threads-max
# cat /proc/sys/kernel/threads-max
100000
# gdb -q vmlinux /proc/kcore
Core was generated by `BOOT_IMAGE=240ac18 ro root=306 video=matrox:vsa:0x118'.
#0  0x0 in ?? ()
(gdb) p max_threads
$1 = 100000
```

Linux 系统上的进程集合由一组 `struct task_struct` 结构表示，它们以两种方式链接：

1. 作为散列表，通过 `pid` 进行散列，并且
2. 作为使用 `p->next_task` 和 `p->prev_task` 指针的环形双向链表。

散列表称为 `pid_hash[]`，定义在 `include/linux/sched.h` 中：

```c
/* PID hashing. (shouldnt this be dynamic?) */
#define PIDHASH_SZ (4096 >> 2)
extern struct task_struct *pid_hash[PIDHASH_SZ];

#define pid_hashfn(x)  (((x) >> 8) ^ (x)) & (PIDHASH_SZ - 1))
```

任务根据其 `pid` 值进行哈希，上述哈希函数旨在将这些元素均匀地分布在其定义域（0 到 `PID_MAX-1`）中。该哈希表用于通过给定的 `pid` 快速查找任务，使用来自 `include/linux/sched.h` 的内联函数 `find_task_pid()`：

```c
static inline struct task_struct *find_task_by_pid(int pid)
{
  struct task_struct *p, **htable = &pidhash[pid_hashfn(pid)];
  for (p = *htable; p && p->pid != pid; p = p->pidhash_next)
    ;
  return p;
}
```

每个哈希链（即哈希到相同值的任务）上的任务通过 `p->pidhash_next/pidhash_prev` 链接起来，它们由 `hash_pid()` 和 `unhash_pid()` 用于将给定进程插入或删除哈希表。这些操作在称为 `tasklist_lock` 的读写自旋锁保护下进行，该锁以写（WRITE）模式获取。

使用 `p->next_task/prev_task` 的循环双向链表得以维护，以便轻松遍历系统中的所有任务。这是通过 `include/linux/sched.h` 中的 `for_each_task()` 宏实现的：

```c
#define for_each_task(p) \
  for (p = &init_task ; (p = p->next_task) != &init_task ; )
```

使用 `for_each_task()` 的用户需要以读（READ）模式获取 `tasklist_lock`。请注意，`for_each_task()` 使用 `init_task` 来标记列表的开始（也是结束）——这是安全的，因为空闲任务（`pid` 0）永远不会退出。

修改进程哈希表或/和进程表链接的元素，特别是 `fork()`、`exit()` 和 `ptrace()`，必须以写（WRITE）模式获取 `tasklist_lock`。更有趣的是，写者还必须禁用本地 CPU 上的中断。这背后的原因并不简单：`send_sigio()` 函数遍历任务列表，因此以读（READ）模式获取 `tasklist_lock`，并且它是从中断上下文中由 `kill_fasync()` 调用的。这就是为什么写者在持有锁时必须禁用中断，而读者则不需要的原因。

既然我们理解了 `task_struct` 结构是如何链接在一起的，让我们来检查一下 `task_struct` 的成员。它们大致对应于 UNIX 中 `struct proc` 和 `struct user` 合并后的成员。

其他版本的 UNIX 将任务状态信息分离为两部分：一部分需要始终保持在内存中（称为 `proc` 结构，包含进程状态、调度信息等），另一部分仅在进程运行时才需要（称为 `u area`，包含文件描述符表、磁盘配额信息等）。这种丑陋设计的唯一原因是内存曾经是非常稀缺的资源。现代操作系统（好吧，目前只有 Linux，但其他操作系统，例如 FreeBSD 似乎也在朝 Linux 的方向改进）不需要这种分离，因此始终在内核内存驻留的数据结构中维护进程状态。

`task_struct` 结构在 `include/linux/sched.h` 中声明，当前大小为 1680 字节。

`state` 字段声明如下：



```c
volatile long state;    /* -1 unrunnable, 0 runnable, >0 stopped */

#define TASK_RUNNING           0
#define TASK_INTERRUPTIBLE     1
#define TASK_UNINTERRUPTIBLE   2
#define TASK_ZOMBIE            4
#define TASK_STOPPED           8
#define TASK_EXCLUSIVE         32
```

为什么 `TASK_EXCLUSIVE` 定义为 32 而不是 16？因为 16 被 `TASK_SWAPPING` 占用了，而我移除所有对 `TASK_SWAPPING` 的引用时（在 2.3.x 某个版本中）忘记将 `TASK_EXCLUSIVE` 向上移位。

`p->state` 声明中的 `volatile` 意味着它可以被异步修改（来自中断处理程序）：

- `TASK_RUNNING`：表示任务“应该”在运行队列上。它可能尚未进入运行队列的原因是将任务标记为 `TASK_RUNNING` 并将其放入运行队列这两个操作不是原子的。你需要以读模式持有 `runqueue_lock` 读写自旋锁才能查看运行队列。如果你这样做，你会看到运行队列上的每个任务都处于 `TASK_RUNNING` 状态。然而，由于上述原因，反之并不成立。同样，驱动程序可以将自身（或者更准确地说，它们运行的进程上下文）标记为 `TASK_INTERRUPTIBLE`（或 `TASK_UNINTERRUPTIBLE`），然后调用 `schedule()`，这会将其从运行队列中移除（除非有挂起的信号，如果是这种情况，它会保留在运行队列中）。

- `TASK_INTERRUPTIBLE`：表示任务正在睡眠，但可以被信号或定时器到期唤醒。

- `TASK_UNINTERRUPTIBLE`：与 `TASK_INTERRUPTIBLE` 相同，但不能被唤醒。

- `TASK_ZOMBIE`：任务已终止，但其状态尚未被父进程（自然父进程或通过收养的父进程）收集（即 `wait(1)`）。

- `TASK_STOPPED`：任务已被停止，原因是作业控制信号或 `ptrace(2)`。

- `TASK_EXCLUSIVE`：这不是一个独立的状态，但可以按位或（OR）到 `TASK_INTERRUPTIBLE` 或 `TASK_UNINTERRUPTIBLE` 中的任意一个。这意味着当此任务在一个有许多其他任务的等待队列上睡眠时，它将单独被唤醒，而不是通过唤醒所有等待者导致“惊群效应”问题。

任务标志包含有关进程状态的信息，这些状态不是互斥的：

```c
unsigned long flags;    /* per process flags, defined below */
/*
 * Per process flags
 */
#define PF_ALIGNWARN       0x00000001      /* Print alignment warning msgs */
                                     /* Not implemented yet, only for 486*/
#define PF_STARTING        0x00000002    /* being created */
#define PF_EXITING         0x00000004    /* getting shut down */
#define PF_FORKNOEXEC      0x00000040    /* forked but didn't exec */
#define PF_SUPERPRIV       0x00000100    /* used super-user privileges */
#define PF_DUMPCORE        0x00000200    /* dumped core */
#define PF_SIGNALED        0x00000400    /* killed by a signal */
#define PF_MEMALLOC        0x00000800    /* Allocating memory */
#define PF_VWORK           0x00001000    /* Wake up parent in mm_release */
#define PF_USEDPU          0x00100000    /* task used PFU this quantum (SMP) */
```

字段 `p->has_cpu`、`p->processor`、`p->counter`、`p->priority`、`p->policy` 和 `p->rt_priority` 与调度器相关，将在后面讨论。

字段 `p->mm` 和 `p->active_mm` 分别指向由 `mm_struct` 结构描述的进程地址空间，以及如果进程没有真实地址空间（例如内核线程）时的活动地址空间。这有助于在任务被调度出去时最小化切换地址空间时的 TLB 刷新。因此，如果我们正在调度入一个内核线程（没有 `p->mm`），那么它的 `next->active_mm` 将被设置为被调度出的任务的 `prev->active_mm`，如果 `prev->mm != NULL`，这将等同于 `prev->mm`。如果 `clone(2)` 系统调用传递了 `CLONE_VM` 标志，或者通过 `vfork(2)` 系统调用，地址空间可以在线程之间共享。

字段 `p->exec_domain` 和 `p->personality` 与任务的“个性”有关，即某些系统调用的行为方式，以模拟外部 UNIX 变体的“个性”。

字段 `p->fs` 包含文件系统信息，在 Linux 下意味着三个信息片段：

- 根目录的 `dentry` 和挂载点，

- 备用根目录的 `dentry` 和挂载点，

- 当前工作目录的 `dentry` 和挂载点。

该结构还包含一个引用计数，因为当 `clone(2)` 系统调用传递了 `CLONE_FS` 标志时，它可以在克隆任务之间共享。

字段 `p->files` 包含文件描述符表。如果 `clone(2)` 系统调用指定了 `CLONE_FILES`，这也可以在任务之间共享。

字段 `p->sig` 包含信号处理程序，并可以通过 `CLONE_SIGHAND` 在克隆任务之间共享。

### 2.2 任务和内核线程的创建与终止

不同的操作系统书籍对“进程”有不同的定义，从“正在执行的程序实例”开始，到“由 `clone(2)` 或 `fork(2)` 系统调用所产生的事物”结束。在 Linux 下，有三种类型的进程：

- 空闲线程，

- 内核线程，

- 用户任务。

空闲线程是为第一个 CPU 在编译时创建的；然后通过 `arch/i386/kernel/smpboot.c` 中特定的架构相关函数 `fork_by_hand()` 为每个 CPU“手动”创建，该函数展开

手动调用 `fork(2)` 系统调用（在某些架构上）。空闲任务共享同一个 `init_task` 结构，但拥有私有的 `TSS` 结构，位于每 CPU 数组 `init_tss` 中。所有空闲任务的 `pid` 均为 0，且没有其他任务可以共享 `pid`，即不能通过 `clone(2)` 使用 `CLONE_PID` 标志。

内核线程使用 `kernel_thread()` 函数创建，该函数在内核模式下调用 `clone(2)` 系统调用。内核线程通常没有用户地址空间，即 `p->mm = NULL`，因为它们显式调用了 `exit_mm()`（例如通过 `daemonize()` 函数）。内核线程始终可以直接访问内核地址空间。它们被分配低范围的 `pid` 号。运行在进程的环 0（即 x86 架构下）意味着内核线程享有所有 I/O 特权，并且不能被调度器抢占。

用户任务通过 `clone(2)` 或 `fork(2)` 系统调用创建，两者在内部都调用了 `kernel/sched.c::do_fork()`。

让我们理解当用户进程发出 `fork(2)` 系统调用时发生了什么。尽管 `fork(2)` 因传递用户栈和寄存器的方式不同而具有架构依赖性，但实际执行操作的底层函数 `do_fork()` 是可移植的，位于 `kernel/fork.c` 中。

执行以下步骤：

1. 局部变量 `retval` 被设置为 `-ENOMEM`，因为这是 `fork(2)` 在无法分配新的任务结构时 `errno` 应设置的值。

2. 如果 `clone_flags` 中设置了 `CLONE_PID`，则返回错误（`-EPERM`），除非调用者是空闲线程（仅在启动期间）。因此，普通用户线程不能向 `clone(2)` 传递 `CLONE_PID` 并期望成功。对于 `fork(2)`，这无关紧要，因为 `clone_flags` 被设置为 `SIFCHLD` – 这仅在 `do_fork()` 由 `sys_clone()` 调用时相关，此时会传递来自用户空间请求的 `clone_flags` 值。



3. 初始化 `current->vfork_sem`，因为它稍后会在子进程中清除。这被 `sys_vfork()`（`vfork(2)` 系统调用，对应于 `clone_flags = CLONE_VFORK | CLONE_VM | SIGCHLD`）用于让父进程睡眠，直到子进程执行 `mm_release()`，例如作为 `exec(1)`（另一个程序）或退出（即执行 `exit(2)` 系统调用）的结果。

4. 使用依赖于架构的 `alloc_task_struct()` 宏分配一个新的任务结构。在 x86 上，这只是在 `GFP_KERNEL` 优先级下的 `gfp`。这是 `fork(2)` 系统调用可能睡眠的第一个原因。如果此分配失败，我们返回 -ENOMEM。

5. 使用结构赋值 `*p = *current` 将当前进程任务结构中的所有值复制到新结构中。也许这应该被 `memset()` 替换？随后，不应被子进程继承的字段被设置为正确的值。

6. 获取大内核锁，因为剩余代码否则会不可重入。

7. 如果父进程拥有用户资源（UID 的概念，Linux 足够灵活，使其成为一个问题而非事实），则验证该用户是否超出了 `RLIMIT_NPROC` 软限制 – 如果是，则以 -EAGAIN 失败；如果不是，则按给定 uid 增加进程计数 `p->user->count`。

8. 如果全系统的任务数超过可调参数 `max_threads` 的值，则以 -EAGAIN 失败。

9. 如果正在执行的二进制文件属于模块化执行域，则增加相应模块的引用计数。

10. 如果正在执行的二进制文件属于模块化二进制格式，则增加相应模块的引用计数。

11. 子进程被标记为“未执行 exec”（`p->did_exec = 0`）

12. 子进程被标记为“不可交换”（`p->swappable = 0`）

13. 子进程进入“不可中断睡眠”状态，即 `p->state = TASK_UNINTERRUPTIBLE`（TODO: 为什么要这样做？我认为这是不必要的 – 去掉它，Linus 确认这是不必要的）

14. 子进程的 `p->flags` 根据 `clone_flags` 的值进行设置；对于纯 `fork(2)`，这将设置为 `p->flags = PF_FORKNOEXEC`。

15. 子进程的 `pid` `p->pid` 使用 `kernel/fork.c:get_pid()` 中的快速算法进行设置（TODO: `get_pid()` 总是在大内核锁下从 `do_fork()` 调用，因此 `lastpid` 锁可以冗余，同时也移除 `get_pid()` 的 `flags` 参数，补丁已于 2000/06/20 发送给 Alan – 后续跟进）。

16. `do_fork()` 中的其余代码初始化子进程任务结构的其余部分。在最后，子进程的任务结构被哈希到 `pidhash` 哈希表中，并且子进程被唤醒（TODO: `wake_up_process(p)` 设置 `p->state = TASK_RUNNING` 并将进程添加到运行队列，因此我们之前可能不需要在 `do_fork()` 中将 `p->state` 设置为 `TASK_RUNNING`）。有趣的部分是将 `p->exit_signal` 设置为 `clone_flags & CSIGNAL`，对于 `fork(2)` 这意味着只是 `SIGCHLD`，并将 `p->pdeath_signal` 设置为 0。当进程“忘记”原始父进程（通过死亡）时使用 `pdeath_signal`，可以通过 `prctl(2)` 系统调用的 `PR_GET/SET_PDEATHSIG` 命令设置/获取（你可能会争辩说，`prctl(2)` 通过用户空间指针参数返回 `pdeath_signal` 值的方式有点傻 – 我的错，在 Andries Brouwer 更新 man 页之后，已经太晚了无法修复 ;)

因此任务被创建。任务终止有几种方式：

1. 通过发出 `exit(2)` 系统调用；
2. 通过接收默认处置为终止的信号；
3. 在某些异常情况下被迫终止；
4. 通过调用 `bdflush(2)` 且 `func == 1`（这是 Linux 特定的，为了兼容仍然在 `/etc/inittab` 中有 'update' 行的旧发行版 – 如今 update 的工作由内核线程 `kupdated` 完成。

在 Linux 下实现系统调用的函数以 `sys_` 为前缀，但它们通常只关注参数检查或架构特定的信息传递方式，实际工作由 `do_` 函数完成。`sys_exit()` 就是这样，它调用 `do_exit()` 来做工作。尽管，内核的其他部分有时会调用 `sys_exit()`，而它们真正应该调用的是 `do_exit()`。

函数 `do_exit()` 位于 `kernel/exit.c`。关于 `do_exit()` 需要注意的要点：

- 使用全局内核锁（加锁但不解锁）。
- 在结尾调用 `schedule()`，它永不返回。
- 将任务状态设置为 `TASK_ZOMBIE`。
- 如果 `current->pdeath_signal` 不为 0，则通知任何子进程。
- 使用通常等于 SIGCHLD 的 `current->exit_signal` 通知父进程。
- 释放由 fork 分配的资源，关闭打开的文件等。
- 在使用懒惰 FPU 切换的架构上（ia64, mips, mips64）（TODO: 移除 `sparc, sparc64` 的 'flags' 参数，做硬件所需的操作以将 FPU 所有权（如果属于当前进程）传递给“无”）。

### 2.2 任务和内核线程的创建与终止

## 2.3 Linux 调度器

调度器的任务是在多个进程之间协调对当前 CPU 的访问。调度器在“内核主文件” `kernel/sched.c` 中实现。相应的头文件 `include/linux/sched.h` 被几乎所有内核源文件包含（显式或隐式）。

与调度器相关的任务结构字段包括：

- `p->need_resched`：如果应在“下一个机会”调用 `schedule()`，则设置此字段。
- `p->counter`：在此调度切片中剩余的时钟滴答数，由定时器递减。当此字段小于或等于零时，它被重置为 0，并设置 `p->need_resched`。这也有时被称为进程的“动态优先级”，因为它可以自行变化。
- `p->priority`：进程的静态优先级，仅通过像 `nice(2)`、POSIX.1b `sched_setparam(2)` 或 4.4BSDSVR4 `setpriority(2)` 这样众所周知的系统调用更改。
- `p->rt_priority`：实时优先级
- `p->policy`：调度策略，指定任务属于哪个调度类。任务可以使用 `sched_setscheduler(2)` 系统调用更改其调度类。有效值为 `SCHED_OTHER`（传统 UNIX 进程）、`SCHED_FIFO`（POSIX.1b FIFO 实时进程）和 `SCHED_RR`（POSIX 轮转实时进程）。也可以将 `SCHED_YIELD` 与这些值中的任意一个进行 OR 运算，表示进程决定让出 CPU，例如通过调用 `sched_yield(2)` 系统调用。FIFO 实时进程将运行直到 a) 它在 I/O 上阻塞，b) 它显式让出 CPU，或 c) 它被具有更高 `p->rt_priority` 值的另一个实时进程抢占。`SCHED_RR` 与 `SCHED_FIFO` 相同，除了当其时间片到期时，它会回到运行队列的末尾。

调度器的算法很简单，尽管 `schedule()` 函数表面上的复杂性很大。该函数复杂，因为它在一个函数中实现了三种调度算法，同时也由于微妙的 SMP 特性。

`schedule()` 中看似“无用”的 gotos 是有目的的 – 为了生成优化得最好（针对 i386）的代码。另外，请注意，调度器（像内核的大部分一样）在 2.4 中完全重写，因此下面的讨论不适用于 2.2 或更早的内核。

让我们详细查看该函数：

1. 如果 `current->active_mm == NULL`，则有问题。当前进程，即使是内核线程（`current->mm == NULL`），必须在所有时刻都拥有有效的 `p->active_mm`。
2. 如果 `tq_scheduler` 任务队列中有任务需要处理，现在就处理它。任务队列提供了一种内核机制，以便稍后安排函数的执行。我们将在其他地方详细研究它。
3. 将局部变量 `prev` 和 `this_cpu` 分别初始化为当前任务和当前 CPU。
4. 检查 `schedule()` 是否从中断处理程序中调用（由于 bug），如果是则引发 panic。
5. 释放全局内核锁。
6. 如果通过软中断机制有一些工作需要执行，现在就执行。



7. 将局部指针`struct schedule_data *sched_data`初始化为指向每 CPU（缓存行对齐以防止缓存行乒乓效应）的调度数据区域，该区域包含`last_schedule`的 TSC 值以及最后调度的任务结构指针（TODO: `sched_data` 仅在 SMP 上使用，为什么`init_idle()`在 UP 上也初始化它？）。

8. 获取`runqueue_lock`自旋锁。注意，我们使用`spin_lock_irq()`，因为在`schedule()`中我们保证中断是使能的。因此，当我们解锁`runqueue_lock`时，我们可以直接重新使能中断，而不是保存/恢复 eflags（`spin_lock_irqsave/restore`变体）。

9. 任务状态机：如果任务处于`TASK_RUNNING`状态，则保持不变；如果它处于`TASK_INTERRUPTIBLE`状态且有信号挂起，则将其移动到`TASK_RUNNING`状态。在所有其他情况下，从运行队列中删除它。

10. `next`（最佳调度候选者）被设置为此 cpu 的空闲任务。然而，此候选者的 goodness 值被设置为非常低的值（-1000），希望有人比它更好。

### 2.3 调度器

11. 如果上一个（当前）任务处于`TASK_RUNNING`状态，则当前的 goodness（优劣度）被设置为该任务的 goodness，并且它被标记为比空闲任务更优的调度候选者。

12. 现在检查运行队列，并将每个可以在此 CPU 上调度的进程的 goodness 与当前值进行比较；goodness 最高的进程胜出。现在必须澄清“可以在此 CPU 上调度”这一概念：在 UP（单处理器）系统中，运行队列上的每个进程都有资格被调度；在 SMP（对称多处理）系统中，只有在其他 CPU 上尚未运行的进程才有资格在此 CPU 上被调度。Goodness 由一个名为`goodness()`的函数计算，该函数通过使实时进程的 goodness 非常高`1000 + p->rt_priority`来处理实时进程，大于 1000 的值保证没有`SCHED_OTHER`类型的进程能胜出；因此，它们只与其他可能具有更大`p->rt_priority`的实时进程竞争。如果进程的时间片（`p->counter`）用尽，goodness 函数返回 0。对于非实时进程，goodness 的初始值设置为`p->counter` – 这样，如果进程已经占用 CPU 一段时间，它获得 CPU 的可能性就更小，即交互型进程比 CPU 密集型（number crunchers）进程更受青睐。架构特定的常量`PROC_CHANGE_PENALTY`试图实现“CPU 亲和性”（即给位于同一 CPU 上的进程优势）。它还稍微偏向于 mm 指向当前`active_mm`的进程或没有（用户）地址空间的进程，即内核线程。

13. 如果当前的 goodness 值为 0，则检查整个进程列表（不仅仅是运行队列上的！），并使用简单算法重新计算它们的动态优先级：

```c
recalculate:
(
        struct task_struct *p;
        spin_unlock_irq(&runqueue_lock);
        read_lock(&tasklist_lock);
        for_each_task(p)
                p->counter = (p->counter >> 1) + p->priority;
        read_unlock(&tasklist_lock);
        spin_lock_irq(&runqueue_lock);
)
```

注意我们在重新计算之前释放了`runqueue_lock`。原因是我们遍历了所有进程集合；这可能花费很长时间，在此期间，`schedule()`可能在另一个 CPU 上被调用并选择一个 goodness 足够用于该 CPU 的进程，而我们在当前 CPU 上被迫进行重新计算。好吧，承认这在某种程度上是不一致的，因为当我们（在当前 CPU 上）选择具有最佳 goodness 的进程时，在另一个 CPU 上运行的`schedule()`可能正在重新计算动态优先级。

14. 从这一点开始，可以确定`next`指向要调度的任务，因此我们将`next->has_cpu`初始化为 1，将`next->processor`初始化为`this_cpu`。现在可以解锁`runqueue_lock`。

15. 如果我们切换回同一个任务（`next == prev`），那么我们可以简单地重新获取全局内核锁并返回，即跳过所有硬件级（寄存器、栈等）和 VM 相关（切换页目录、重新计算`active_mm`等）的工作。

16. 宏`switch_to()`是架构相关的，在 i386 上，它涉及 a) FPU 处理，b) LDT 处理，c) 重新加载段寄存器，d) TSS 处理以及 e) 重新加载调试寄存器。

## 2.4 Linux 双向链表实现

在我们继续研究等待队列的实现之前，我们必须熟悉 Linux 标准的双向链表实现。等待队列（以及 Linux 中的其他所有内容）大量使用它们，因为它们被称为行话中的“list.h 实现”，因为最相关的文件是`list.h`。

`include/linux/list.h`。

这里的基本数据结构是`struct list_head`：

```c
struct list_head {
    struct list_head *next, *prev;
};

#define LIST_HEAD_INIT(name) { &(name), &(name) }

#define LIST_HEAD(name) \
    struct list_head name = LIST_HEAD_INIT(name)

#define INIT_LIST_HEAD(ptr) do { \
    (ptr)->next = (ptr); (ptr)->prev = (ptr); \
} while (0)

#define list_entry(ptr, type, member) \
    ((type *)((char *)(ptr)-(unsigned long)(&(type *)0)->member)))

#define list_for_each(pos, head) \
    for (pos = (head)->next; pos != (head); pos = pos->next)
```

前三个宏用于通过让`next`和`prev`指针都指向自身来初始化空列表。从 C 语法限制中可以明显看出在哪里应该使用哪一个 – 例如，`LIST_HEAD_INIT()`可用于声明中的结构体元素初始化，第二个可用于静态变量初始化声明，第三个可用于函数内部。

宏`list_entry()`用于访问单个链表元素，例如（来自`fs/file_table.c:fs_may_remount_ro()`）：

```c
struct super_block {
    ...
    struct list_head s_files;
    ...
} *sb = &some_super_block;

struct file {
    ...
    struct list_head f_list;
    ...
} *file;

struct list_head *p;
for (p = sb->s_files.next; p != &sb->s_files; p = p->next) {
    struct file *file = list_entry(p, struct file, f_list);
    do something to 'file'
}
```

使用`list_for_each()`宏的一个很好的例子是在调度器中，我们遍历运行队列寻找具有最高 goodness 的进程：

```c
static LIST_HEAD(runqueue_head);
struct list_head *tmp;
struct task_struct *p;
list_for_each(tmp, &runqueue_head) {
    p = list_entry(tmp, struct task_struct, run_list);
    if (can_schedule(p)) {
        int weight = goodness(p, this_cpu, prev->active_mm);
        if (weight > c)
            c = weight, next = p;
    }
}
```



在这里，`p->run_list` 在 `task_struct` 结构体内声明为 `struct list_head run_list`，并作为列表的锚点。从列表中删除元素和添加（到列表的头或尾）是通过 `list_del()` / `list_add()` / `list_add_tail()` 宏完成的。下面的示例是将任务添加和从运行队列中移除：

```c
static inline void del_from_runqueue(struct task_struct * p)
{
    nr_running--;
    list_del(&p->run_list);
    p->run_list.next = NULL;
}

static inline void add_to_runqueue(struct task_struct * p)
{
    list_add(&p->run_list, &runqueue_head);
    nr_running++;
}

static inline void move_last_runqueue(struct task_struct * p)
{
    list_del(&p->run_list);
    list_add_tail(&p->run_list, &runqueue_head);
}

static inline void move_first_runqueue(struct task_struct * p)
{
    list_del(&p->run_list);
    list_add(&p->run_list, &runqueue_head);
}
```

## 2.5 等待队列

当进程请求内核做当前不可能但稍后可能变得可能的某件事时，进程会被挂起（睡眠），并在请求更有可能得到满足时被唤醒。用于此目的的内核机制之一是称为“等待队列”。

Linux 实现允许使用 `TASK_EXCLUSIVE` 标志进行唤醒语义。使用等待队列时，你可以使用一个众所周知的队列，然后简单地使用 `sleep_on` / `sleep_on_timeout` / `interruptible_sleep_on` / `interruptible_sleep_on_timeout`，或者你可以定义自己的等待队列，并使用 `add_wait_queue` / `remove_wait_queue` 将自己添加或移除，并在需要时使用 `wake_up()` / `wake_up_interruptible()` 进行唤醒。

等待队列第一种用法的示例是页分配器（在 `mm/page_alloc.c` 中；`__alloc_pages()`）和 `kswapd` 内核守护进程（在 `mm/vmscan.c` 中；`kswapd()`）之间的交互，通过等待队列 `kswapd_wait` 实现，该队列在 `mm/vmscan.c` 中声明；`kswapd` 守护进程在此队列上睡眠，每当页分配器需要释放一些页面时，它会被唤醒。

自主等待队列用法的示例是通过 `read(2)` 系统调用请求数据的用户进程和在中断上下文中运行以提供数据的内核之间的交互。中断处理程序可能如下所示（简化的 `drivers/char/rtc_interrupt()`）：

```c
static DECLARE_WAIT_QUEUE_HEAD(rtc_wait);
void rtc_interrupt(int irq, void *dev_id, struct pt_regs *regs)
{
    spin_lock(&rtc_lock);
    rtc_irq_data = CMOS_READ(RTC_INTR_FLAGS);
    spin_unlock(&rtc_lock);
    wake_up_interruptible(&rtc_wait);
}
```

因此，中断处理程序通过从某个设备特定的 I/O 端口读取数据（`CMOS_READ()` 宏转化为几对 `outb` / `inb`）来获取数据，然后唤醒在 `rtc_wait` 等待队列上睡眠的人。

现在，`read(2)` 系统调用可以这样实现：

```c
ssize_t rtc_read(struct file file, char *buf, size_t count, off_t *ppos)
{
    DECLARE_WAITQUEUE(wait, current);
    unsigned long data;
    ssize_t retval;
    add_wait_queue(&rtc_wait, &wait);
    current->state = TASK_INTERRUPTIBLE;
    do {
        spin_lock_irq(&rtc_lock);
        data = rtc_irq_data;
        rtc_irq_data = 0;
        spin_unlock_irq(&rtc_lock);

        if (data != 0)
            break;

        if (file->f_flags & O_NONBLOCK) {
            retval = -EAGAIN;
            goto out;
        }
        if (signal_pending(current)) {
            retval = -ERESTARTSYS;
            goto out;
        }
        schedule();
    } while(1);

    retval = put_user(data, (unsigned long *)buf);

    if (!retval)
        retval = sizeof(unsigned long);

out:
    current->state = TASK_RUNNING;
    remove_wait_queue(&rtc_wait, &wait);
    return retval;
}
```

`rtc_read()` 中发生的事情如下：

1. 我们声明一个等待队列元素，指向当前进程上下文。
2. 我们将该元素添加到 `rtc_wait` 等待队列中。
3. 我们将当前上下文标记为 `TASK_INTERRUPTIBLE`，这意味着在下一次休眠后它不会被重新调度。
4. 我们检查是否有数据可用；如果有，我们跳出循环，将数据复制到用户缓冲区，将自身标记为 `TASK_RUNNING`，从等待队列中移除自身并返回。
5. 如果尚未有数据，我们检查用户是否指定了非阻塞 I/O；如果是，则以 `EAGAIN`（等同于 `EWOULDBLOCK`）失败。
6. 我们还检查是否有挂起的信号；如果有，则通知“上层”在必要时重启系统调用。这里“必要时”指的是 `sigaction(2)` 系统调用中指定的信号处置细节。
7. 然后我们“切换出去”，即进入睡眠状态，直到被中断处理程序唤醒。如果我们没有将自身标记为 `TASK_INTERRUPTIBLE`，调度器可能会在数据可用之前更早地调度我们，从而导致不必要的处理。

值得指出的是，使用等待队列，实现 `poll(2)` 系统调用非常容易：

```c
static unsigned int rtc_poll(struct file *file, poll_table *wait)
{
    unsigned long l;

    poll_wait(file, &rtc_wait, wait);

    spin_lock_irq(&rtc_lock);
    l = rtc_irq_data;
    spin_unlock_irq(&rtc_lock);

    if (l != 0)
        return POLLIN | POLLRDNORM;
    return 0;
}
```

所有工作都是由与设备无关的函数 `poll_wait()` 完成的，该函数执行必要的等待队列操作：我们只需将其指向由我们的特定设备中断处理程序唤醒的等待队列即可。

## 2.6 内核定时器

现在让我们将注意力转向内核定时器。内核定时器用于在未来指定时间分发特定函数（称为“定时器处理程序”）的执行。主要数据结构是 `include/linux/timer.h` 中声明的 `struct timer_list`：

```c
struct timer_list {
    struct list_head list;
    unsigned long expires;
    unsigned long data;
    void (*function)(unsigned long);
    volatile int running;
};
```



`list` 字段用于链接到内部列表中，由 `timerlist_lock` 自旋锁保护。`expires` 字段是当 `function` 处理程序应通过传入 `data` 作为参数时被调用时的 `jiffies` 值。`running` 字段在 SMP（对称多处理）系统中用于测试定时器处理程序是否正在其他 CPU 上运行。

函数 `add_timer()` 和 `del_timer()` 分别将给定定时器添加到列表或从列表中移除。当定时器过期时，它会被自动移除。在使用定时器之前，必须通过 `init_timer()` 函数对其进行初始化。并且在添加之前，必须设置 `function` 和 `expires` 字段。

## 2.7 下半部（Bottom Halves）

有时，将中断处理程序内部要执行的工作量拆分为立即工作（例如确认中断、更新统计数据等）和可以推迟到稍后、当中断启用时再执行的工作（例如对数据进行后处理、唤醒等待此数据的进程等）是合理的。

下半部是用于延迟执行内核任务的最早机制，自 Linux 1.x 起就已可用。在 Linux 2.0 中，增加了一种称为“任务队列”的新机制，这将是下一节讨论的主题。

下半部由 `global_bh_lock` 自旋锁进行序列化，即任一 CPU 上同一时间只能运行一个下半部。然而，在尝试执行处理程序时，如果无法获取 `global_bh_lock`，下半部会被标记（即调度）为待执行状态——这样处理就可以继续，而不必对 `global_bh_lock` 进行忙等待。

总共只能注册 32 个下半部。操纵下半部所需的函数如下（所有函数都导出供模块使用）：

- `void init_bh(int nr, void (*routine)(void))`：将由 `routine` 参数指向的下半部处理程序安装到插槽 `nr` 中。该插槽应在 `include/linux/interrupt.h` 中以 `XXXX_BH` 的形式进行枚举，例如 `TIMER_BH` 或 `TQUEUE_BH`。通常，子系统的初始化例程（对于模块来说是 `init_module()`）会使用此函数来安装所需的下半部。

- `void remove_bh(int nr)`：执行与 `init_bh()` 相反的操作，即卸载安装在插槽 `nr` 中的下半部。此处不进行错误检查，因此，例如，`remove_bh(32)` 会导致系统恐慌/错误。通常，子系统的清理例程（对于模块来说是 `cleanup_module()`）使用此函数来释放插槽，以便稍后被其他子系统重用。（TODO：如果 /proc/bottom_halves 能列出系统中所有已注册的下半部不是更好吗？那意味着 `global_bh_lock` 显然必须被改为读写锁）

- `void mark_bh(int nr)`：标记插槽 `nr` 中的下半部以供执行。通常，中断处理程序会在“更安全的时间”标记其下半部以执行（这就是其名称的由来！）。

下半部是全局锁定的任务片段（tasklet），因此问题“下半部处理程序何时执行？”实际上就是“任务片段何时执行？”。答案是在两个地方：a) 每次调用 `schedule()` 时，以及 b) `entry.S` 中每次中断/系统调用返回路径时。（TODO：因此，`schedule()` 的情况实际上很无聊——它就像添加又一个非常非常慢的中断，为什么不干脆从 `schedule()` 中彻底移除 `handle_softirq` 标签？）

## 2.8 任务队列

任务队列可以被视为旧下半部的动态扩展。事实上，在源代码中它们有时被称为“新”下半部。更具体地说，上一节讨论的旧下半部具有以下局限性：

1. 只有固定数量（32 个）。
2. 每个下半部只能与一个处理函数相关联。
3. 下半部在持有自旋锁的情况下被消耗，因此它们不能阻塞。

因此，通过任务队列，可以将任意数量的函数链接起来，并在稍后按顺序处理。使用 `DECLARE_TASK_QUEUE()` 宏创建新的任务队列，并使用 `queue_task()` 函数将任务加入队列。然后可以使用 `run_task_queue()` 处理任务队列。除了创建自己的任务队列（并且必须手动消耗它）之外，你还可以使用 Linux 预定义的任务队列，这些队列在已知点被消耗：

1. `tq_timer`：定时器任务队列，在每次定时器中断以及释放 tty 设备（关闭或释放半打开的终端设备）时运行。由于定时器处理程序在中断上下文中运行，`tq_timer` 任务也在中断上下文中运行，因此不能阻塞。
2. `tq_scheduler`：调度器任务队列，由调度器消耗（也在关闭 tty 设备时消耗，类似 `tq_timer`）。由于调度器在正在重新调度的进程上下文中执行，`tq_scheduler` 任务可以做任何它们喜欢的事情，即阻塞、使用进程上下文数据（尽管它们为什么要这样做呢），等等。
3. `tq_immediate`：这实际上是一个下半部 `IMMEDIATE_BH`，因此驱动程序可以执行 `queue_task(task, &tq_immediate)`，然后标记 `bh`（`IMMEDIATE_BH`）以在中断上下文中消耗。
4. `tq_disk`：由低级块设备访问（和 RAID）用于启动实际请求。此任务队列导出给模块使用，但不应用于其设计目的以外的特殊用途。

除非驱动程序使用自己的任务队列，否则它不需要调用 `run_tasks_queues()` 来处理队列，除非在以下解释的情况下例外。

如果记得驱动程序可以在队列上调度任务，而这些任务只在特定设备实例仍然有效期间才有意义——这通常意味着直到应用程序关闭它——那么 `tq_timer/tq_scheduler` 任务队列不仅在通常的地方被消耗，还在其他地方（关闭 tty 设备只是一个例子）被消耗的原因就显而易见了。因此，驱动程序可能需要调用 `run_task_queue()` 来刷新它（以及其他任何进程）放入队列中的任务，因为允许它们在稍后执行可能没有意义——也就是说，相关的数据结构可能已被另一个实例释放/重用。这就是为什么你在定时器中断和 `schedule()` 以外的其他地方看到 `tq_timer` 和 `tg_scheduler` 使用 `run_task_queue()` 的原因。

## 2.9 任务片（Tasklets）

尚未介绍，将在未来版本中补充。

## 2.10 软中断（Softirqs）

尚未介绍，将在未来版本中补充。

## 2.11 在 i386 架构上如何实现系统调用？

Linux 下有两种实现系统调用的机制：

- `iCALL7/lCALL27` 调用门；
- `int 0x80` 软件中断。

本地 Linux 程序使用 `int 0x80`，而来自其他 UNIX 变体（Solaris、UnixWare 7 等）的二进制文件则使用 `iCALL7` 机制。名称“`iCALL7`”在历史上具有误导性，因为它也涵盖了 `lCALL27`（例如 Solaris/x86），但处理函数被称为 `iCALL7_func`。

当系统启动时，会调用函数 `arch/i386/kernel/traps.c:trap_init()`，它设置 IDT，使得向量 `0x80`（类型 15，dpl 3）指向来自 `arch/i386/kernel/entry.S` 的 `system_call` 入口地址。

当用户空间应用程序发起系统调用时，参数通过寄存器传递，并且应用程序执行“`int 0x80`”指令。这会触发陷入内核模式，处理器跳转到 `entry.S` 中的 `system_call` 入口点。其执行的操作如下：

1. 保存寄存器。
2. 将 `%ds` 和 `%es` 设置为 `KERNEL_DS`，以便所有数据（和附加段）引用都在内核地址空间中进行。
3. 如果 `%eax` 的值大于 `NR_syscalls`（当前为 256），则返回 `ENOSYS` 错误并失败。
4. 如果该任务正在被 ptrace 跟踪（`tsk->ptrace & PF_TRACESYS`），则执行特殊处理。这是为了支持 strace（类似 SVR4 的 `truss()`）或调试器等程序。
5. 调用 `sys_call_table+4* (来自 %eax 的 syscall_number)`。该表在同一个文件（`arch/i386/kernel/entry.S`）中初始化，指向各个系统调用处理程序，这些处理程序在 Linux 下通常以 `sys_` 为前缀，例如 `sys_open`、`sys_exit` 等。这些 C 语言系统调用处理程序会在堆栈上找到参数，这些参数由 `SAVE_ALL` 存储。
6. 进入“系统调用返回路径”。这是一个独立的标签，因为它不仅被 `int 0x80` 使用，也被 `iCALL7`、`lCALL27` 使用。这涉及处理任务片（包括下半部），检查是否需要 `schedule()`（`tsk->need_resched != 0`），检查是否有待处理信号，如果有则进行处理。



Linux 支持最多 6 个系统调用参数。它们通过 `%ebx`、`%ecx`、`%edx`、`%esi`、`%edi` 传递（`%ebp` 临时使用，见 `asm-i386/unistd.h` 中的 `_syscall6()`）。系统调用编号通过 `%eax` 传递。

## 2.12 原子操作

原子操作有两种类型：位图和 `atomic_t`。位图对于维护大型集合中某些“已分配”或“空闲”单元的概念非常有用，其中每个单元由某个数字标识，例如空闲 inode 或空闲块。它们也广泛用于简单的锁定，例如提供对打开设备的独占访问权。`arch/i386/kernel/microcode.c` 中有一个例子：

```c
/*
 *  microcode_status 中的位。（31 位空间用于未来扩展）
 */
#define MICROCODE_IS_OPEN    0       /* 如果设备正在使用中则设置 */

static unsigned long microcode_status;
```

无需将 `microcode_status` 初始化为 0，因为在 Linux 下 BSS 段会被显式清零。

```c
/*
 * 这里我们强制同一时间只有一个用户进行 open/close。
 */
static int microcode_open(struct inode *inode, struct file *file)
{
    if (!capable(CAP_SYS_RAWIO))
        return -EPERM;

    /* 请同一时间只允许一个 */
    if (test_and_set_bit(MICROCODE_IS_OPEN, &microcode_status))
        return -EBUSY;

    MOD_INC_USE_COUNT;
    return 0;
}
```

位图上的操作包括：

- `void set_bit(int nr, volatile void *addr)`: 设置由 `addr` 指向的位图中的第 `nr` 位。
- `void clear_bit(int nr, volatile void *addr)`: 清除由 `addr` 指向的位图中的第 `nr` 位。
- `void change_bit(int nr, volatile void *addr)`: 切换由 `addr` 指向的位图中的第 `nr` 位（如果已设置则清除，如果未设置则设置）。
- `int test_and_set_bit(int nr, volatile void *addr)`: 原子性地设置第 `nr` 位并返回旧的位值。
- `int test_and_clear_bit(int nr, volatile void *addr)`: 原子性地清除第 `nr` 位并返回旧的位值。
- `int test_and_change_bit(int nr, volatile void *addr)`: 原子性地切换第 `nr` 位并返回旧的位值。

这些操作使用 `LOCK_PREFIX` 宏，该宏在 SMP 内核上评估为总线锁定指令前缀，而在 UP 内核上则评估为空。这保证了在 SMP 环境中的访问原子性。

有时位操作并不方便，而是需要执行算术操作——加法、减法、递增或递减。典型的用例是引用计数（例如 inode 的引用计数）。这一功能由 `atomic_t` 数据类型和以下操作提供：

- `atomic_read(&v)`: 读取 `atomic_t` 变量 `v` 的值。
- `atomic_set(&v, i)`: 将 `atomic_t` 变量 `v` 的值设置为整数 `i`。
- `void atomic_add(int i, volatile atomic_t *v)`: 将整数 `i` 加到由 `v` 指向的原子变量的值上。
- `void atomic_sub(int i, volatile atomic_t *v)`: 从由 `v` 指向的原子变量的值中减去整数 `i`。
- `int atomic_sub_and_test(int i, volatile atomic_t *v)`: 从由 `v` 指向的原子变量的值中减去整数 `i`；如果新值为 0 则返回 1，否则返回 0。
- `void atomic_inc(volatile atomic_t *v)`: 将值递增 1。
- `void atomic_dec(volatile atomic_t *v)`: 将值递减 1。
- `int atomic_dec_and_test(volatile atomic_t *v)`: 将值递减；如果新值为 0 则返回 1，否则返回 0。
- `int atomic_inc_and_test(volatile atomic_t *v)`: 将值递增；如果新值为 0 则返回 1，否则返回 0。
- `int atomic_add_negative(int i, volatile atomic_t *v)`: 将 `i` 的值加到 `v` 上，如果结果为负则返回 1。如果结果大于或等于 0 则返回 0。此操作用于实现信号量。

## 2.13 自旋锁、读写自旋锁和大读者自旋锁

从 Linux 支持早期（本世纪 90 年代初）开始，开发者就面临在不同类型的上下文（用户进程与中断）以及同一上下文在多个 CPU 上的不同实例之间访问共享数据的经典问题。

SMP 支持在 1995 年 11 月 15 日添加到了 Linux 1.3.42 中（原始补丁在同年 10 月应用于 1.3.37）。

如果代码的关键区域可能由进程上下文和中断上下文执行，那么在 UP 上使用 `cli`/`sti` 指令保护它的方法是：

```c
unsigned long flags;

save_flags(flags);
cli();
/* 关键代码 */
restore_flags(flags);
```

虽然这在 UP 上没问题，但在 SMP 上显然毫无用处，因为相同的代码序列可能同时在另一个 CPU 上执行，虽然 `cli()` 在单个 CPU 上提供了针对中断上下文的竞态保护，但它完全不能防止在不同 CPU 上运行的上下文之间的竞态。这就是自旋锁有用的地方。

有三种类型的自旋锁：普通（基本）自旋锁、读写自旋锁和大读者自旋锁。当存在“多读者少写者”的自然倾向时，应使用读写自旋锁。一个例子是访问已注册文件系统列表（参见 `fs/super.c`）。该列表由 `file_systems_lock` 读写自旋锁保护，因为只有在注册/注销文件系统时才需要独占访问权，但任何进程都可以读取文件 `/proc/filesystems` 或使用 `sysfs(2)` 系统调用来强制对 `file_systems` 列表进行只读扫描。这使得使用读写自旋锁变得合理。使用读写自旋锁时，同一时间可以有多个读者，但只能有一个写者，并且当有写者时不能有任何读者。顺便提一下，如果有写者正在尝试获取锁，新的读者最好不能获得锁，也就是说，如果 Linux 能正确解决由于多个读者导致的潜在写者饥饿问题那就更好了。这意味着当有写者尝试获取锁时，读者必须被阻塞。目前情况并非如此，而且是否应该修复这一点并不明显——反方的论点是——读者通常获取锁的时间非常短，因此当写者获取锁可能持续较长时间时，读者真的应该被饥饿吗？

大读者自旋锁是读写自旋锁的一种形式，针对非常轻量的读取访问进行了严重优化，但写入会有惩罚。大读者自旋锁的数量有限——目前只有两个存在，其中一个仅用于 sparc64（glocal irq），另一个用于网络。在所有其他访问模式不符合这两种情况之一的场景中，应使用基本自旋锁。持有任何一种自旋锁时都不能阻塞。

自旋锁有三种变体：`普通`、`_irq()` 和 `_bh()`。

1.  普通 `spin_lock()/spin_unlock()`：如果你知道中断始终关闭，或者你不与中断上下文竞争（例如从中断处理程序内部），那么你可以使用这种。它不会触及当前 CPU 的中断状态。
2.  `spin_lock_irq()/spin_unlock_irq()`：如果你知道中断始终开启，那么你可以使用这个版本，它简单地禁用（在锁定时）并重新启用（在解锁时）当前 CPU 的中断。例如，`rtc_read()` 使用

    ```text
    spin_lock_irq(&rtc_lock)  （read() 内部中断始终开启）
    而
    rtc_interrupt() 使用
    spin_lock(&rtc_lock)  （中断处理程序内部中断始终关闭）。
    ```

    注意 `rtc_read()` 使用的是 `spin_lock_irq()` 而不是更通用的 `spin_lock_irqsave()`，因为在进入任何系统调用时，中断始终开启。
3.  `spin_lock_irqsave()/spin_unlock_irqrestore()`：最强形式，在中断状态未知时使用，但仅在中断实际上重要时才有意义，即如果我们的中断处理程序不执行任何关键代码，使用它就没有意义。



如果你与中断处理程序竞争，不能使用普通 `spin_lock()`，因为如果你获取了锁然后同一个 CPU 上来了中断，它将永远忙等待该锁：锁持有者被中断后，在中断处理程序返回之前不会继续执行。

自旋锁最常见的用途是访问在用户进程上下文和中断处理程序之间共享的数据结构：

```text
spinlock_t my_lock = SPIN_LOCK_UNLOCKED;

my_ioctl()
{
      spin_lock_irq(&my_lock);
      /* 关键区域 */
      spin_unlock_irq(&my_lock);
}

my_irq_handler()
{
    spin_lock(&lock);
    /* critical section */
    spin_unlock(&lock);
}
```

关于这个例子，有几点需要注意：

1.  进程上下文，在此表现为典型的驱动程序方法 `ioctl()`（为清晰起见，省略了参数和返回值），必须使用 `spin_lock_irq()`，因为它知道在执行设备 `ioctl()` 方法时中断始终处于启用状态。
2.  中断上下文，在此由 `my_irq_handler()` 表示（同样，为清晰起见省略了参数）可以使用普通的 `spin_lock()` 形式，因为中断处理程序内部中断是被禁用的。

## 2.14 信号量和读写信号量

有时，在访问共享数据结构时，必须执行可能会阻塞的操作，例如将数据复制到用户空间。Linux 中适用于此类场景的锁原语称为信号量。有两种类型的信号量：基本信号量和读写信号量。根据信号量的初始值，它们可以用于互斥（初始值为 1）或提供更复杂的访问类型。

读写信号量与基本信号量的区别方式与读写自旋锁与基本自旋锁的区别方式相同：一次可以有多个读者，但只能有一个写者，并且当存在写者时不能有读者 - 即写者阻塞所有读者，而当写者等待时新的读者也会被阻塞。

此外，基本信号量是可中断的 - 只需使用操作 `down_interruptible()`/`down_read_interruptible()` 代替普通的 `down()`/`down_read()`，并检查从 `down_interruptible()` 返回的值：如果操作被中断，该值将为非零。

在临界代码段可能按引用调用由其他子系统/模块注册的未知函数的情况下，使用信号量进行互斥是理想的，即调用者无法先验地知道函数是否会阻塞。

信号量使用的简单示例位于 `kernel/sys.c` 中，是 `sethostname(2)`/`gethostname(2)` 系统调用的实现。

```c
asmlinkage long sys_sethostname(char *name, int len)
{
    int errno;

    if (!capable(CAP_SYS_ADMIN))
        return -EPERM;
    if (len < 0 || len > _NEW_ UTS_LEN)
        return -EINVAL;
    down_write(&uts_sem);
    errno = -EFAULT;
    if (!copy_from_user(system_utsname.nodename, name, len)) {
        system_utsname.nodename[len] = 0;
        errno = 0;
    }
    up_write(&uts_sem);
    return errno;
}

asmlinkage long sys_gethostname(char *name, int len)
{
    int i, errno;

    if (len < 0)
        return -EINVAL;
    down_read(&uts_sem);
    i = 1 + strlen(system_utsname.nodename);
    if (i > len)
        i = len;
    errno = 0;
    if (copy_to_user(name, system_utsname.nodename, i))
        errno = -EFAULT;
    up_read(&uts_sem);
    return errno;
}
```

关于这个例子的注意事项有：

1.  函数在通过 `copy_from_user()`/`copy_to_user()` 从/向用户空间复制数据时可能会阻塞。因此，它们不能在此处使用任何形式的自旋锁。
2.  选择的信号量类型是读写信号量，而非基本信号量，因为可能存在许多并发的 `gethostname(2)` 请求，这些请求不需要互斥。

尽管 Linux 对信号量和读写信号量的实现非常复杂，但可以想象到一些尚未实现的场景，例如没有可中断的读写信号量的概念。这显然是因为不存在需要这些奇特原语变体的现实情况。

## 2.15 内核对加载模块的支持

Linux 是一个单核操作系统，尽管现代关于基于微内核设计的操作系统所提供的一些“优势”炒作不断，但事实依然如此（引用 Linus Torvalds 本人的话）：

> ……将消息传递作为操作系统的基本操作

> 只是计算机科学中的自慰行为。它可能

> 感觉很爽，但你实际上并没有完成任何工作。

因此，Linux 一直是并将永远基于单核设计，这意味着所有子系统都在相同的特权模式下运行并共享相同的地址空间；它们之间的通信通过通常的 C 函数调用方式实现。

然而，虽然将内核功能分离为微内核中那样独立的“进程”绝对是一个坏主意，但在某些情况下（例如在内存有限的机器上，或者在安装内核时，这些内核否则可能包含相互排斥的 ISA 自动探测设备驱动程序），将其分离为可动态按需加载的内核模块是可取的。是否包含对可加载模块的支持是在编译时决定的，由 `CONFIG_MODULES` 选项确定。通过 `request_module()` 机制支持模块自动加载是一个单独的编译选项（`CONFIG_RMOD`）。

在 Linux 下，以下功能可以作为可加载模块实现：

-   字符设备和块设备驱动程序，包括杂项设备驱动程序。
-   终端行规程。
-   `/proc` 和 `devfs` 中的虚拟（常规）文件（例如 `/dev/cpu/microcode` 对比 `/dev/misc/microcode`）。
-   二进制文件格式（例如 `ELF`, `aout` 等）。
-   执行域（例如 `Linux`, `UnixWare7`, `Solaris` 等）。
-   文件系统。
-   `System V IPC`。

在 Linux 下，有几样东西不能作为模块实现（可能是因为将它们的模块化没有意义）：

-   调度算法。
-   虚拟内存策略。
-   缓冲缓存、页缓存和其他缓存。

Linux 提供几个系统调用以协助加载模块：

-   `caddr_t create_module(const char *name, size_t size)`: 使用 `vmalloc()` 分配 `size` 字节，并在其开头映射一个模块结构。然后，这个新模块被链接到由 `module_list` 头部的列表中。只有具有 `CAP_SYS_MODULE` 权限的进程才能调用此系统调用，否则将返回 `EPERM`。
-   `long init_module(const char *name, struct module *image)`: 加载重定位后的模块映像，并导致调用模块的初始化例程。只有具有 `CAP_SYS_MODULE` 权限的进程才能调用此系统调用，否则将返回 `EPERM`。
-   `long delete_module(const char *name)`: 尝试卸载模块。如果 `name == NULL`，则尝试卸载所有未使用的模块。
-   `long query_module(const char *name, int which, void *buf, size_t bufsize, size_t *ret)`: 返回关于模块（或所有模块）的信息。

向用户提供的命令接口包括：

-   `insmod`：插入单个模块。
-   `modprobe`：插入模块及其依赖的所有其他模块。
-   `rmmod`：移除模块。
-   `modinfo`：打印关于模块的某些信息，例如作者、描述、模块接受的参数等。

除了能够使用 `insmod` 或 `modprobe` 手动加载模块外，还可以在内核需要特定功能时让模块自动插入。内核用于此功能的接口是名为 `request_module(name)` 的函数，该函数被导出给模块，以便模块也可以加载其他模块。`request_module(name)` 内部创建一个内核线程，该线程执行用户空间命令 `modprobe -s -k module_name`，使用标准的 `exec_usermodehelper()` 内核接口（该接口也导出给模块）。该函数成功时返回 `0`，但是通常不值得检查 `request_module()` 的返回代码。相反，编程习惯是：



```c
if (check_some_feature() == NULL)
    request_module(module);
if (check_some_feature() == NULL)
    return -ENODEV;
```

例如，当尝试打开主要号为 `N` 的块设备时，`fs/block_dev.c:get_blkdevops()` 就是这样做的，以加载模块 `block-major-N`。显然，没有名为 `block-major-N` 的这样的模块（Linux 开发人员仅为他们的模块选择了合理的名称），但它是使用文件 `/etc/modules.conf` 映射到正确的模块名称的。然而，对于大多数众所周知的主要号（和其他类型的模块），`modprobe/insmod` 命令知道要加载哪个真实模块，而无需在 `/etc/modules.conf` 中显式的别名声明。

加载模块的一个好例子是在 `mount(2)` 系统调用中。`mount(2)` 系统调用接受文件系统类型作为字符串，然后 `fs/super.c:do_mount()` 将其传递给 `fs/super.c:get_fs_type()`：

```c
static struct file_system_type *get_fs_type(const char *name)
{
    struct file_system_type *fs;

    read_lock(&file_systems_lock);
    fs = *(find_filesystem(name));
    if (fs && !try_inc_mod_count(fs->owner))
        fs = NULL;
    read_unlock(&file_systems_lock);
    if (!fs && (request_module(name) == 0)) {
        read_lock(&file_systems_lock);
        fs = *(find_filesystem(name));
        if (fs && !try_inc_mod_count(fs->owner))
            fs = NULL;
        read_unlock(&file_systems_lock);
    }
    return fs;
}
```

此函数中有几点需要注意：

1.  首先，我们尝试在已注册的文件系统中查找给定名称的文件系统。这是在 `file_systems_lock` 的读保护下进行的（因为我们没有修改已注册文件系统的列表）。

2.  如果找到这样的文件系统，我们尝试通过尝试增加其模块的保留计数来获得对它的新引用。对于静态链接的文件系统或当前未被删除的模块，这总是返回 1。如果 `try_inc_mod_count()` 返回 0，我们认为这是失败 – 即如果模块存在但正在被删除，那么它就好像完全不存在一样。

3.  我们释放 `file_systems_lock`，因为我们接下来要做的事（`request_module()`）是一个阻塞操作，因此我们不能在持有自旋锁的同时执行它。

## 3. 虚拟文件系统 (VFS)

## 3.1 索引节点缓存及其与 Dcache 的交互

实际上，在这种特定情况下，即使 `request_module()` 保证是非阻塞的，并且模块加载在同一上下文中原子执行，我们也必须释放 `file_systems_lock`。这样做的原因是，模块的初始化函数将尝试调用 `register_filesystem()`，而该函数会获取同一个 `file_systems_lock` 读写自旋锁的写锁。

4. 如果加载尝试成功，我们将获取 `file_systems_lock` 自旋锁，并尝试在列表中定位新注册的文件系统。请注意，这在原则上略有错误，因为 `modprobe` 命令中的 bug 可能导致其在成功加载请求的模块后发生核心转储，在这种情况下，尽管新文件系统已注册，但 `request_module()` 仍会失败，且 `get_fs_type()` 无法找到该文件系统。

5. 如果找到该文件系统并且我们能够获取其引用，则返回该文件系统。否则返回 `NULL`。

当模块加载到内核中时，它可以使用 `EXPORT_SYMBOL()` 宏或其他当前已加载模块导出的任何公共符号来引用内核中导出的任何符号。如果模块使用另一个模块的符号，则在重新计算依赖项时会标记为依赖于该模块，这是通过启动时运行 `depmod` 命令来实现的（例如，在安装新内核之后）。

通常，必须将模块集合与其使用的内核接口版本进行匹配，在 Linux 下，这仅意味着“内核版本”，因为通常没有特殊的内核接口版本化机制。然而，有一种称为“模块版本化”或 `CONFIG_MODVERSIONS` 的有限功能，它允许在切换到新内核时避免重新编译模块。这里发生的情况是，内核符号表在内部访问和模块访问时的处理方式不同。公共部分（即导出的部分）符号表的元素是通过 32 位校验和 C 声明构建的。因此，为了解析模块加载期间使用的符号，加载器必须匹配包括校验和在内的符号完整表示；如果这些符号不同，它将拒绝加载该模块。这种情况仅在内核和模块都启用模块版本化编译时发生。如果其中任何一个使用原始符号名称，加载器将尝试匹配模块声明的内核版本和内核导出的版本，如果不同则拒绝加载。

为了支持多个文件系统，Linux 包含一个称为 VFS（虚拟文件系统切换，Virtual Filesystem Switch）的特殊内核接口层。这与 SVR4 衍生品中发现的 `vnode/vfs` 接口类似（最初来自 BSD 和 Sun 的原始实现）。

Linux 索引节点缓存在一个文件 `fs/inode.c` 中实现，由 977 行代码组成。值得注意的是，在过去 5-7 年中，对它的修改并不多：通过将最新版本与 1.3.42 等版本进行比较，人们仍能识别出一些代码。

Linux 索引节点缓存的结构如下：

- 1. 一个全局哈希表 `inode_hashtable`，其中每个索引节点都通过超级块指针和 32 位索引节点号进行哈希。没有超级块的索引节点（`inode->i_sb == NULL`）则被添加到由 `anon_hash_chain` 开头的双向链表中。匿名索引节点的示例包括由 `net/socket.c:sock_alloc()` 创建的套接字，或者通过调用 `fs/inode.c:get_empty_inode()` 创建的索引节点。

- 2. 一个全局类型 `in_use` 列表（`inode_in_use`），其中包含具有 `i_count>0` 和 `i_nlink>0` 的有效索引节点。由 `get_empty_inode()` 和 `get_new_inode()` 新分配的节点被添加到 `inode_in_use` 列表中。

- 3. 一个全局类型 `unused` 列表（`inode_unused`），其中包含具有 `i_count = 0` 的有效索引节点。

- 4. 每个超级块的脏列表（`sb->s_dirty`），其中包含具有 `i_count > 0`、`i_nlink>0` 和 `i_state & I_DIRTY` 的有效索引节点。当索引节点被标记为脏时，如果它也被哈希了，则被添加到 `sb->s_dirty` 列表中。维护每个超级块的索引节点脏列表允许快速同步索引节点。

- 5. 真正的索引节点缓存 - 一个名为 `inode_cache_p` 的 SLAB 缓存。随着索引节点对象的分配和释放，它们从该 SLAB 缓存中取出并返回到该缓存。

类型列表从 `inode->i_list` 锚定，哈希表从 `inode->i_hash` 锚定。每个索引节点可以在一个哈希表和且仅在一个类型列表（`in_use`、`unused` 或 `dirty`）上。

所有这些列表都由一个自旋锁保护：`inode_lock`。

当从 `init/main.c:start_kernel()` 调用 `inode_init()` 函数时，索引节点缓存子系统被初始化。该函数被标记为 `__init`，这意味着其代码稍后会被丢弃。它接受单个参数 - 系统中的物理页数量。这使得索引节点缓存可以根据可用内存量进行自我配置，即如果有足够的内存，则创建更大的哈希表。

关于索引节点缓存的唯一统计信息是未使用索引节点的数量，存储在 `inodes_stat.nr_unused` 中，并可以通过文件 `/proc/sys/fs/inode-nr` 和 `/proc/sys/fs/inode-state` 供用户程序访问。

我们可以这样在运行中的内核上使用 `gdb` 检查其中一个列表：



```
(gdb) printf "%d\n", (unsigned long)(&((struct inode *)0)->i_list)
8
(gdb) p inode_unused
$34 = 0xdfa992a8
(gdb) p (struct list_head)inode_unused
$35 = {next = 0xdfa992a8, prev = 0xdfcdd5a8}
(gdb) p ((struct list_head)inode_unused).prev
$36 = (struct list_head *) 0xdfcdd5a8
(gdb) p ((struct list_head *)inode_unused).prev)->prev
$37 = (struct list_head *) 0xdfb5a2e8
(gdb) set $i = (struct inode *)0xdfb5a2e0
(gdb) p $i->i_ino
$38 = 0x3bec7
(gdb) p $i->i_count
$39 = (counter = 0x0)
```

请注意，我们从地址 `0xdfb5a2e8` 中减去 8，根据 `include/linux/list.h` 中 `list_entry()` 宏的定义，得到了 `struct inode` 的地址（`0xdfb5a2e0`）。

为了理解索引节点缓存的工作原理，让我们跟踪 ext2 文件系统中常规文件的索引节点在其打开和关闭过程中的生命周期：

`open(2)` 系统调用由 `fs/open.c:sys_open` 函数实现，实际工作由 `fs/open.c:filp_open()` 函数完成，该函数分为两部分：

- `open_namei()`：填写包含 `dentry` 和 `vfsmount` 结构的 `nameidata` 结构。
- `dentry_open()`：给定 `dentry` 和 `vfsmount`，此函数分配一个新的 `struct file` 并将它们链接在一起；它还调用在 `open_namei()` 中读取索引节点时（通过 `dentry->d_inode` 提供索引节点）在 `inode->i_op` 中设置的特定于文件系统的 `f_op->open()` 方法。

`open_namei()` 函数通过 `path_walk()` 与 dentry 缓存交互，后者调用 `real_lookup()`，进而调用特定于文件系统的 `inode_operations->lookup()` 方法。该方法的作用是找到父目录中与名称匹配的条目，然后执行 `iget(sb, ino)` 以获取相应的索引节点 - 这将我们带到索引节点缓存。当读取索引节点时，通过 `d_add(dentry, inode)` 实例化 dentry。与此同时，请注意，对于具有磁盘上索引节点号概念的 UNIX 风格文件系统，查找方法的工作是将该索引节点号的大小端格式映射到当前 CPU 格式，例如，如果原始（特定于文件系统的）目录项中的索引节点号是小端 32 位格式，可以这样做：

```
unsigned long ino = le32_to_cpu(de->inode);
inode = iget(sb, ino);
d_add(dentry, inode);
```

因此，当我们打开文件时，我们会遇到 `iget(sb, ino)`，这实际上是 `iget4(sb, ino, NULL, NULL)`，它执行以下操作：

- 在 `inode_lock` 的保护下，尝试在哈希表中查找具有匹配超级块和索引节点号的索引节点。如果找到索引节点，则增加其引用计数（`i_count`）；如果增加前的值为 0 且索引节点不脏，则将其从其当前所在的任何类型列表（`inode->i_list`）中移除（当然必须是 `inode_unused` 列表）并插入到 `inode_in_use` 类型列表中；最后，`inodes_stat.nr_unused` 递减。
- 如果索引节点当前被锁定，我们等待其解锁，以确保 `iget4()` 返回未锁定的索引节点。
- 如果在哈希表中未找到索引节点，则这是我们第一次遇到此索引节点，因此我们调用 `get_new_inode()`，并传递指向哈希表中应插入位置的指针。
- `get_new_inode()` 从 `inode_cache_p` SLAB 缓存中分配一个新的索引节点，但此操作可能阻塞（`GFP_KERNEL` 分配），因此必须释放保护哈希表的 `inode_lock` 自旋锁。由于已释放自旋锁，之后必须在哈希表中重试搜索索引节点；如果此时找到，则（在通过 `__iget` 增加引用计数后）返回在哈希表中找到的索引节点，并销毁新分配的索引节点。如果仍不能在哈希表中找到，则我们刚刚分配的新索引节点将被使用；因此，它被初始化为所需的值，并调用特定于文件系统的 `sb->s_op->read_inode()` 方法来填充索引节点的其余部分。这使我们从索引节点缓存回到文件系统代码 -

### 3.2 Inode 缓存生命周期

请回忆一下，我们在文件系统的特定 `lookup()` 方法调用 `iget()` 时进入了 inode 缓存。当 `s_op->read_inode()` 方法正在从磁盘读取 inode 时，inode 处于锁定状态（`i_state = I_LOCK`）；在 `read_inode()` 方法返回后，inode 被解锁，并唤醒所有等待它的进程。

现在，让我们看看当关闭此文件描述符时发生了什么。`close(2)` 系统调用实现在 `fs/open.c::sys_close()` 函数中，该函数调用 `do_close(fd, 1)`，它将进程文件描述符表中的描述符“撕掉”（替换为 `NULL`），并调用 `filp_close()` 函数，后者完成了大部分工作。有趣的事情发生在 `fput()` 中，它检查这是否是该文件的最后一个引用，如果是，则调用 `fs/file_table.c::fput()`，进而调用 `__fput()`（这就是与 dcache（因此与 inode 缓存——请记住 dcache 是 inode 缓存的掌控者！）发生交互的地方）。`fs/dcache.c::dput()` 执行 `dentry_iput()`，通过 `iput(inode)` 让我们回到 inode 缓存，因此让我们理解一下 `fs/inode.c::iput(inode):`

- 如果传递给我们的参数是 `NULL`，我们什么都不做并直接返回。
- 如果存在文件系统特定的 `sb->s_op->put_inode()` 方法，则立即调用它（此时未持有自旋锁，因此它可以阻塞）。
- 获取 `inode_lock` 自旋锁并递减 `i_count`。如果这不是该 inode 的最后一个引用，则我们仅检查是否存在过多的引用，从而导致 `i_count` 在其分配的 32 位范围内发生回绕；如果是这样，我们会打印一条警告并返回。请注意，我们在持有 `inode_lock` 自旋锁时调用了 `printk()`（这是可以接受的，因为 `printk()` 永远不会阻塞，因此可以在任何上下文（甚至从中断处理程序！）中调用）。
- 如果这是最后一个活动引用，则需要执行一些工作。

`iput()` 在最后一个 inode 引用时执行的工作相当复杂，因此我们将其分离成一个独立的列表：

- 如果 `i_nlink == 0`（例如，在保持文件打开的状态下将其解除链接），则 inode 从哈希表和类型列表中移除；如果页缓存中持有任何属于此 inode 的数据页，则通过 `truncate_all_inode_pages(&inode->i_data)` 将其移除。然后调用文件系统特定的 `s_op->delete_inode()` 方法，这通常会删除 inode 的磁盘副本。如果文件系统没有注册 `s_op->delete_inode()` 方法（例如 `ramfs`），则我们调用 `clear_inode(inode)`，如果注册了 `s_op->clear_inode()` 则调用它，并且如果 inode 对应块设备，则该设备的引用计数通过 `bput(inode->i_bdev)` 减少。
- 如果 `i_nlink != 0`，则检查同一哈希桶中是否有其他 inode，如果没有，并且 inode 不是脏状态，则从类型列表中删除并将其添加到 `inode_unused` 列表中，增加 `inodes_stat.nr_unused`。如果同一哈希桶中存在其他 inode，则从类型列表中删除并将其添加到 `inode_unused` 列表中。如果这是一个匿名 inode（NetApp .snapshot），则从类型列表中删除并完全清除/销毁它。

## 3.2 文件系统注册/注销

Linux 内核提供了一种机制，以便新文件系统可以以最少的努力来编写。其历史原因是：



- 在人们仍在使用非 Linux 操作系统以保护其对遗留软件的投资的世界里，Linux 必须通过支持大量不同的文件系统来提供互操作性——其中大多数本身不值得存在，但仅为了与现有的非 Linux 操作系统兼容而存在。

- 文件编写者的接口必须非常简单，以便人们可以通过编写它们的只读版本来尝试逆向工程现有的专有文件系统。因此，Linux VFS 使实现只读文件系统变得非常容易；95% 的工作是通过添加完整的写支持来完成它们。作为一个具体的例子，我在大约 10 小时内为 Linux 编写了只读的 `BFS` 文件系统，但花费了数周时间才完成它以获得完整的写支持（甚至今天，一些纯粹主义者声称它不完整，因为“它没有碎片整理支持”）。

- `VFS` 接口是导出的，因此所有 Linux 文件系统都可以作为模块实现。

让我们考虑在 Linux 下实现文件系统所需的步骤。实现文件系统的代码可以是动态加载的模块，也可以是静态链接到内核中的，而在 Linux 下实现它的方式非常透明。只需填充一个 `struct file_system_type` 结构，并使用 `register_filesystem()` 函数向 `VFS` 注册它，如下一个来自 `fs/bfs/inode.c` 的示例所示：

```c
#include <linux/module.h>
#include <linux/init.h>

static struct super_block *bfs_read_super(struct super_block *, void *, int);

static DECLARE_FSTYPE_DEV(bfs_fs_type, "bfs", bfs_read_super);

static int __init init_bfs_fs(void)
{
    return register_filesystem(&bfs_fs_type);
}

static void __exit exit_bfs_fs(void)
{
    unregister_filesystem(&bfs_fs_type);
}

module_init(init_bfs_fs)
module_exit(exit_bfs_fs)
```

`module_init()` / `module_exit()` 宏确保，当 `BFS` 编译为模块时，函数 `init_bfs_fs()` 和 `exit_bfs_fs()` 分别转变为 `init_module()` 和 `cleanup_module()`；如果 `BFS` 静态链接到内核中，`exit_bfs_fs()` 代码会消失，因为它是不必要的。

`struct file_system_type` 在 `include/linux/fs.h` 中声明：

```c
struct file_system_type {
    const char *name;
    int fs_flags;
    struct super_block *(*read_super)(struct super_block *, void *, int);
    struct module *owner;
    struct vfsmount * kern_mnt; /* For kernel mount, if it's FS_SINGLE fs */
    struct file_system_type * next;
};
```

其字段解释如下：

- `name`：人类可读的名称，出现在 `/proc/filesystems` 文件中，并用作按键查找文件系统的键；此相同名称用于 `mount(2)` 中的文件系统类型，并且应该是唯一的；显然，只能有一个具有给定名称的文件系统。对于模块，`name` 指向模块的地址空间并且不会复制：这意味着如果模块已卸载但文件系统仍已注册，`cat /proc/filesystems` 可能会触发内核崩溃（`oops`）。

- `fs_flags`：一个或多个（按位或运算）标志：用于只能挂载在块设备上的文件系统的 `FS_REQUIRES_DEV`，用于只能有一个超级块的文件系统的 `FS_SINGLE`，用于不能通过用户空间意味着通过 `mount(2)` 系统调用挂载的文件系统的 `FS_NOMOUNT`；不过，它们可以通过 `kern_mount()` 接口在内部挂载，例如管道。

- `read_super`：指向在挂载操作期间读取超级块的函数的指针。此函数是必需的；如果未提供，挂载操作（无论是来自用户空间还是内核）将始终失败，除非在 `FS_SINGLE` 情况下，它将在 `get_sb_single()` 中尝试解引用 `fs_type->kern_mnt->mnt_sb` 中的 `NULL` 指针（`fs_type->kern_mnt = NULL`）时触发 `Oops`。

- `owner`：指向实现此文件系统的模块的指针。如果文件系统静态链接到内核中，则此值为 `NULL`。您不需要手动设置它，因为宏 `THIS_MODULE` 会自动执行正确的操作。

- `kern_mnt`：仅用于 `FS_SINGLE` 文件系统。这是由 `kern_mount()` 设置的（`TODO`：如果未设置 `FS_SINGLE`，`kern_mount()` 应拒绝挂载文件系统）。

- `next`：链接到由 `file_systems`（参见 `fs/super.c`）为头的单向链表中。该列表由 `file_systems_lock` 读写自旋锁保护，函数 `register/unregister_filesystem()` 通过从列表中链接和解除链接条目来修改它。

`read_super()` 函数的任务是填充超级块的字段，分配根 `inode` 并初始化与此挂载实例关联的文件系统私有信息。因此，通常 `read_super()` 会执行以下操作：

- 使用缓冲缓存 `bread()` 函数从通过 `sb->s_dev` 参数指定的设备读取超级块。如果预计立即读取几个后续元数据块，则使用 `breada()` 安排异步读取额外的块是有意义的。

- 验证超级块是否包含有效的魔数，并且整体看起来是否“正常”。

- 初始化 `sb->s_op` 以指向 `struct super_block_operations` 结构。此结构包含实现诸如“读取 `inode`”、“删除 `inode`”等操作的文件系统特定函数。

- 使用 `d_alloc_root()` 分配根 `inode` 和根 `dentry`。

- 如果文件系统不是只读挂载的，则将 `sb->s_dirty` 设置为 `1`，并将包含超级块的缓冲区标记为脏（`TODO`：为什么我们要这样做？我在 `BFS` 中这样做是因为 `MINIX` 也这样做了...）。

### 3.3 文件描述符管理

在 Linux 下，用户文件描述符和内核 `inode` 结构之间存在多个间接层。当进程发出 `open(2)` 系统调用时，内核返回一个小的非负整数，该整数可用于此文件的后续 I/O 操作。此整数是指向 `struct file` 指针数组的索引。每个文件结构通过 `file->f_dentry` 指向一个 `dentry`。每个 `dentry` 通过 `dentry->d_inode` 指向一个 `inode`。

每个任务包含一个字段 `task->files`，它是指向在 `include/linux/sched.h` 中定义的 `struct files_struct` 的指针。

### 3.4 文件结构管理

`file->count` 是一个引用计数，由 `get_file()`（通常由 `fget()` 调用）递增，并由 `fput()` 和 `put_filp()` 递减。`fput()` 与 `put_filp()` 的区别在于，`fput()` 执行更多常规文件所需的工作，例如释放 `flock` 锁、释放 `dentry` 等；而 `put_filp()` 仅操作文件表结构，即在 `files_lock` 自旋锁的保护下，递减计数，将文件从 `anon_list` 中移除，并将其添加到 `free_list`。

如果子线程是通过在 `clone()` 系统调用的克隆标志参数中设置 `CLONE_FILES` 而创建的，那么 `tsk->files` 可以在父进程和子进程之间共享。这一点可以在 `kernel/fork.c:copy_files()`（由 `do_fork()` 调用）中看到，当设置了 `CLONE_FILES` 时，它只会递增 `file->count`，而不是按照传统 UNIX `fork(2)` 的惯例去复制文件描述符表。



当文件被打开时，为其分配的文件结构会被安装到 `current->files->fd[fd]` 槽位中，并且位图 `current->files->open_fds` 中对应的 `fd` 位会被置位。这一切都是在 `current->files->file_lock` 读写自旋锁的写保护下完成的。当描述符被关闭时，`current->files->open_fds` 中的 `fd` 位会被清除，并且 `current->files->next_fd` 会被设置为等于 `fd`，作为下一次该进程想要打开文件时查找第一个未使用描述符的提示。

文件结构在 `include/linux/fs.h` 中声明：

```c
struct fown_struct {
	int pid;        /* pid or -pgpr where SIGIO should be sent */
	uid_t uid, eid; /* uid/euid of process setting the owner */
	int signum;    /* posix.1b rt signal to be delivered on IO */
};

struct file {
	struct list_head	f_list;
	struct dentry	*f_dentry;
	struct vfsmount	*f_vfsmnt;
	struct file_operations	*f_op;
	atomic_t		f_count;
	unsigned int	f_flags;
	mode_t		f_mode;
	loff_t f_pos;
	unsigned long f_reada, f_ramax, f_raend, f_ralen, f_rawin;
	struct fown_struct f_owner;
	unsigned int f_uid, f_gid;
	int f_error;
	unsigned long f_version;
	/* needed for tty driver, and maybe others */
	void *private_data;
};
```

让我们来看看 `struct file` 的各个字段：

- `f_list`：此字段将文件结构链接到其中一个（且仅一个）列表中：a) 如果对应的 inode 不是匿名的，则链接到该文件系统上所有打开文件的 `sb->s_files` 列表中，此时由 `dentry_open()`（由 `filp_open()` 调用）将文件链接到此列表；b) `fs/file_table.c` 中的 `free_list`，包含未使用的文件结构；c) `fs/file_table.c` 中的 `anon_list`，当通过 `get_empty_filp()` 创建新的文件结构时，它会放在此列表中。所有这些列表都由 `files_lock` 自旋锁保护。

- `f_dentry`：与此文件对应的 dentry。dentry 在 nameidata 查找期间由 `open_namei()`（或者更确切地说是它调用的 `path_walk()`）创建，但实际的 `file->f_dentry` 字段是由 `dentry_open()` 设置为包含找到的 dentry 的。

- `f_vfsmnt`：指向包含该文件的文件系统的 `vfs` 挂载结构的指针。这是由 `dentry_open()` 设置的，但在 nameidata 查找期间由 `open_namei()`（或者更确切地说是它调用的 `path_init()`）作为一部分找到。

- `f_op`：指向 `file_operations` 的指针，其中包含可以在此文件上调用的各种方法。这是从 `inode->i_fop` 复制而来的，后者在 nameidata 查找期间由特定于文件系统的 `s_op->read_inode()` 方法放置在那里。我们将在本节的稍后部分详细查看 `file_operations` 方法。

- `f_count`：由 `get_file`、`put_filp`、`fput` 操作的引用计数。

- `f_flags`：来自 `open(2)` 系统调用的 `O_XXX` 标志，由 `dentry_open()` 复制到此处（经过 `filp_open()` 的轻微修改），在清除 `O_CREAT`、`O_EXCL`、`O_NOCTLY`、`O_TRUNC` 之后——永久存储这些标志没有意义，因为它们不能被 `F_SETFL` 修改（或被 `F_GETFL`/`fcntl(2)` 查询）。

- `f_mode`：用户空间标志和模式的一个组合，由 `dentry_open()` 设置。转换的目的是将读和写访问存储在单独的位中，以便可以进行诸如 `f_mode & FMODE_WRITE` 和 `f_mode & FMODE_READ` 这样的简单检查。

- `f_pos`：文件的当前位置，用于下一次对文件的读取或写入。在 i386 上，其类型为 `long long`，即 64 位值。

- `f_reada`, `f_ramax`, `f_raend`, `f_ralen`, `f_rawin`：用于支持 `readahead`——对于凡人来说太复杂了，无法讨论 :)

- `f_owner`：文件 I/O 的所有者，通过 `SIGIO` 机制接收异步 I/O 通知（参见 `fs/fcntl.c`：`kill_fasync`）。

- `f_uid`, `f_gid` – 当文件结构在 `get_empty_filp()` 中创建时，设置为打开该文件的进程的用户 ID 和组 ID。如果文件是套接字，则被 `ipv4` netfilter 使用。

- `f_error`：用于 NFS 客户端返回写错误。它在 `fs/nfs/file.c` 中设置，并在 `mm/fiemap.c`：`generic_file_write()` 中检查。

- `f_version` – 用于使缓存失效的版本控制机制，每当 `f_pos` 变化时递增（使用全局事件）。

- `private_data`：每个文件的私有数据，可由文件系统（例如 coda 在此存储凭据）或设备驱动程序使用。在存在 devfs 的情况下，设备驱动程序可以使用此字段来区分多个实例，而不是使用编码在 `file->f_dentry->d_inode->i_rdev` 中的经典次要设备号。

现在让我们看看 `file_operations` 结构，其中包含可以在文件上调用的方法。让我们回顾一下，它是从 `inode->i_fop` 复制而来的，而 `inode->i_fop` 是由 `s_op->read_inode()` 方法设置的。它声明在 `include/linux/fs.h` 中。



```c
struct file_operations {
	struct module *owner;
	loff_t (*llseek) (struct file *, loff_t, int);
	ssize_t (*read) (struct file *, char *, size_t, loff_t *);
	ssize_t (*write) (struct file *, const char *, size_t, loff_t *);
	int (*readdir) (struct file *, void *, filldir_t);
	unsigned int (*poll) (struct file *, struct poll_table_struct *);
	int (*ioctl) (struct inode *, struct file *, unsigned int, unsigned long);
	int (*mmap) (struct file *, struct vm_area_struct *);
	int (*open) (struct inode *, struct file *);
	int (*flush) (struct file *);
	int (*release) (struct inode *, struct file *);
	int (*fsync) (struct file *, struct dentry *, int datasync);
	int (*fasync) (int, struct file *, int);
	int (*lock) (struct file *, int, struct file_lock *);
	ssize_t (*readv) (struct file *, const struct iovec *, unsigned long, loff_t *);
	ssize_t (*writev) (struct file *, const struct iovec *, unsigned long, loff_t *);
};
```

- `owner`: 指向拥有该子系统模块的指针。只有驱动程序需要将其设置为`THIS_MODULE`，文件系统可以很高兴地忽略它，因为它们的模块计数在挂载/卸载时受控，而驱动程序需要在打开/释放时进行控制。

- `llseek`: 实现`lseek(2)`系统调用。通常省略并使用`fs/read_write.c:default_llseek`，它会做正确的事情（TODO：强制那些目前将其设置为`NULL`的人使用`default_llseek` -- 这样我们可以在`llseek()`中节省一个`if()`）。

- `read`: 实现`read(2)`系统调用。文件系统可以使用`mm/filemap.c:generic_file_read()`来处理常规文件，并使用`fs/read_write.c:generic_read_dir()`（它只是返回`-EISDIR`）来处理目录。

- `write`: 实现`write(2)`系统调用。文件系统可以使用`mm/filemap.c:generic_file_write()`来处理常规文件，并在此处忽略目录。

- `readdir`: 由文件系统使用。对于常规文件被忽略，并为目录实现`readdir(2)`和`getdents(2)`系统调用。

- `poll`: 实现`poll(2)`和`select(2)`系统调用。

- `ioctl`: 实现特定于驱动程序或文件系统的ioctls。请注意，通用的文件ioctls，如`FIBMAP`、`FIBGETBSZ`、`FIONREAD`是由更高层实现的，因此它们永远不会读取`f_op->ioctl()`方法。

- `mmap`: 实现`mmap(2)`系统调用。文件系统可以使用`generic_file_mmap`来处理常规文件，并忽略目录。

- `open`: 在`open(2)`时由`dentry_open()`调用。文件系统很少使用这个，例如coda尝试在打开时本地缓存文件。

- `flush`: 在该文件的每次`close(2)`时调用，不一定是最后一次（参见下面的`release()`方法）。唯一使用此功能的文件系统是NFS客户端，用于刷新所有脏页。请注意，这可以返回一个错误，该错误将被传回触发`close(2)`系统调用的用户空间。

- `release`: 在此文件的最后一个`close(2)`时调用，即当`file->f_count`变为`0`时。尽管定义上返回`int`，但其返回值被VFS忽略（参见`fs/file_table.c:__fput()`）。

- `fsync`: 直接映射到`fsync(2)`/`fdatasync(2)`系统调用，最后一个参数指定它是`fsync`还是`fdatasync`。围绕此操作，VFS几乎不做任何工作，除了将文件描述符映射到文件结构（`file = fget(fd)`以及`inode->i_sem`信号量的down/up）。Ex2文件系统目前忽略最后一个参数，对`fsync(2)`和`fdatasync(2)`执行完全相同的操作。

- `fasync`: 当`file->f_flags & FASYNC`发生变化时调用此方法。

- `lock`: POSIX`fcntl(2)`文件区域锁定机制中文件系统特定的部分。这里唯一的bug是，因为它在独立于文件系统的部分（`posix_lock_file()`）之前被调用，如果它成功但标准的POSIX锁代码失败，那么在文件系统依赖的层面上永远不会解锁。

- `ready`: 实现`ready(2)`系统调用。

- `writenv`: 实现`writenv(2)`系统调用。

### 3.5 超级块和挂载点管理

在Linux下，已挂载文件系统的信息存储在两个独立的结构中 - `super_block`和`vfsmount`。这样做的原因是Linux允许将同一个文件系统（块设备）挂载到多个挂载点，这意味着同一个`super_block`可以对应多个`vfsmount`结构。

让我们首先看看在`include/linux/fs.h`中声明的`struct super_block`：



```c
struct super_block {
    struct list_head s_list; /* Keep this first */
    kdev_t s_dev;
    unsigned long s_blocksize;
    unsigned char s_blocksize_bits;
    unsigned char s_lock;
    unsigned char s_dirty;
    struct file_system_type *s_type;
    struct super_operations *s_op;
    struct quot_operations *dq_op;
    unsigned long s_flags;
    unsigned long s_magic;
    struct dentry *s_root;
    wait_queue_head_t s_wait;
    struct list_head s_dirty; /* dirty inodes */
    struct list_head s_files;
    struct block_device *s_bdev;
    struct list_head s_mounts; /* vfsmont(s) of this one */
    struct quota_mount_options s_dquot; /* Diskquota specific options */
    union {
        struct minix_sb_info minix_sb;
        struct ext2_sb_info ext2_sb;
        /* ... all filesystems that need sb-private info ... */
        void *generic_sbp;
    } u;
    /*
    * The next field is for VFS *only*. No filesystems have any business
    * even looking at it. You had been warned.
    */
    struct semaphore s_vfs_rename_sem; /* Kludge */

    /* The next field is used by knfsd when converting a (inode number based)
    * file handle into a dentry. As it builds a path in the dcache tree from
    * the bottom up, there may for a time be a subpath of dentries which is not
    * connected to the main tree. This semaphore ensure that there is only ever
    * one such free path per filesystem. Note that unconnected files (or other
    * non-directories) are allowed, but not unconnected directories.
    */
    struct semaphore s_nf sd_free_path_sem;
};
```

`super_block` 结构中的各个字段如下：

1. `s_list`：所有活动超级块的双向链表；注意我没有说“所有已挂载文件系统”，因为在 `Linux` 下，一个超级块可以对应一个已挂载文件系统的多个实例。

2. `s_dev`：对于需要挂载到块上的文件系统，即 `FS_REQUIRES_DEV` 文件系统，这是块设备的 `i_dev`。对于其他文件系统（称为匿名文件系统），这是整数 `MKDEV(UNNAMED_MAJOR, i)`，其中 `i` 是 `unnamed_dev_in_use` 数组中第一个未设置的位，范围在 1 到 255 之间（包括两端）。参见 `fs/super.c:get_unnamed_dev()/put_unnamed_dev()`。多次有人建议匿名文件系统不应使用 `s_dev` 字段。

3. `s_blocksize`、`s_blocksize_bits`：块大小和 `log2(块大小)`。

4. `s_lock`：指示超级块当前是否被 `lock_super()/unlock_super()` 锁定。

5. `s_dirty`：当超级块更改时设置，每当写回磁盘时清除。

6. `s_type`：指向对应文件系统的 `struct file_system_type`。文件系统的 `read_super()` 方法不需要设置它，因为如果特定于文件系统的 `read_super()` 成功，`VFS fs/super.c:read_super()` 会为您设置它；如果失败，则重置为 `NULL`。

7. `s_op`：指向 `super_operations` 结构，其中包含特定于文件系统的方法来读写 `inode` 等。正确初始化 `s_op` 是文件系统 `read_super()` 方法的工作。

8. `dq_op`：磁盘配额操作。

9. `s_flags`：超级块标志。

10. `s_magic`：文件系统的魔数。`Minix` 文件系统使用它来区分自身的多种变体。

11. `s_root`：文件系统根目录的 `dentry`。`read_super()` 的工作是从磁盘读取根 `inode`，并将其传递给 `d_alloc_root()` 以分配 `dentry` 并实例化它。一些文件系统将“root”拼写为其他字符而不是 `"/"`，因此使用更通用的 `d_alloc()` 函数将 `dentry` 绑定到一个名称，例如，`pifs` 将自己挂载在 `"/pipe"`：作为其自身的根，而不是 `"/"`。

12. `s_wait`：等待超级块解锁的进程等待队列。

13. `s_dirt`：所有脏 `inode` 的列表。请记住，如果 `inode` 是脏的（`inode->i_state & I_DIRTY`），则它位于特定于超级块的脏列表中，通过 `inode->i_dirt` 链接。

14. `s_files`：此超级块上所有打开文件的列表。对于判断文件系统是否可以重新挂载为只读很有用，参见 `file_table.c:fs_may_remount_ro()`（它遍历 `sb->s_files` 列表，如果存在以写模式打开的文件（`file->f_mode & FMODE_WRITE`）或有待删除的文件（`inode->i_nlink == 0`），则拒绝重新挂载）。

15. `s_bdev`：对于 `FS_REQUIRES_DEV`，这指向描述文件系统所在设备的 `block_device` 结构。

16. `s_mounts`：所有 `vfsmount` 结构的列表，每个挂载实例对应一个。

17. `s_dquot`：更多磁盘配额相关内容。

超级块操作在 `super_operations` 结构中进行描述，该结构在 `include/linux/fs.h` 中声明：

```c
struct super_operations {
    void (*read_inode) (struct inode *);
    void (*write_inode) (struct inode *, int);
    void (*put_inode) (struct inode *);
    void (*delete_inode) (struct inode *);
    void (*put_super) (struct super_block *);
    void (*write_super) (struct super_block *);
    int (*statfs) (struct super_block *, struct statfs *);
    int (*remount_fs) (struct super_block *, int *, char *);
    void (*clear_inode) (struct inode *);
    void (*umount_begin) (struct super_block *);
};
```



1. `read_inode`：从文件系统读取 inode。它仅从 `iget4()` 中的 `fs/inode.c:get_new_inode()`（因此也包括 `iget()`）调用。如果文件系统希望使用 `iget()`，则必须实现 `read_inode()` – 否则 `get_new_inode()` 将引发 panic（内核恐慌）。在读取 inode 期间它是锁定的（`inode->i_state = I_LOCK`）。当函数返回时，所有等待在 `inode->i_wait` 上的进程都会被唤醒。文件系统的 `read_inode()` 方法的工作是定位包含要读取的 inode 的磁盘块，并使用缓冲区缓存 `bread()` 函数将其读入，并初始化 inode 结构的各个字段，例如 `inode->i_op` 和 `inode->i_fop`，以便 VFS 层知道可以在该 inode 或对应文件上执行哪些操作。未实现 `read_inode()` 的文件系统是 ramfs 和管道。例如，ramfs 有自己的 inode 生成函数 `ramfs_get_inode()`，根据需要调用所有的 inode 操作。

2. `write_inode`：将 inode 写回磁盘。类似于 `read_inode()`，它需要定位磁盘上相关的块，并通过调用 `mark_buffer_dirty(bh)` 与缓冲区缓存交互。当 inode 需要单独或作为整个文件系统同步的一部分进行同步时，此方法会在脏 inode（那些用 `mark_inode_dirty()` 标记为脏的 inode）上调用。

3. `put_inode`：每当引用计数减少时调用。

4. `delete_inode`：每当 `inode->i_count` 和 `inode->i_nlink` 都达到 0 时调用。文件系统删除 inode 的磁盘副本，并调用 VFS inode 的 `clear_inode()` 以“以最极端的方式终止它”。

5. `put_super`：在 `umount(2)` 系统调用的最后阶段调用，以通知文件系统应释放关于此实例的任何私有信息。通常，这会 `brelse()` 包含超级块的块，并 `kfree()` 为空闲块、inode 等分配的任何位图。

6. `write_super`：当超级块需要写回磁盘时调用。它应找到包含超级块的块（通常保存在 `sb-private` 区域）并 `mark_buffer_dirty(bh)`。它还应清除 `sb->s_dirt` 标志。

7. `statfs`：实现 `statfs(2)` 系统调用。注意，作为参数传递的 `struct statfs` 指针是内核指针，而不是用户指针，因此我们不需要执行任何到用户空间的 I/O。如果未实现，则 `statfs(2)` 将因 `ENOSYS` 而失败。

8. `remount_fs`：每当文件系统正在重新挂载时调用。

9. `clear_inode`：从 VFS 层的 `clear_inode()` 调用。将私有数据附加到 inode 结构（通过 `generic_ip` 字段）的文件系统必须在此处释放它。

### 3.6 虚拟文件系统示例：pipefs

那么，让我们来看看挂载一个基于磁盘的（`FS_REQUIRES_DEV`）文件系统时会发生什么。 `mount()` 系统调用的实现在 `fs/super.c:sys_mount()` 中，它只是一个包装器，将选项、文件系统类型和设备名称复制给 `do_mount()` 函数，而真正的繁重工作是由 `do_mount()` 完成的：

- 如果必要，加载文件系统驱动程序，并增加其模块的引用计数。请注意，在挂载操作期间，文件系统模块的引用计数被增加了两次——一次是 `do_mount()` 调用 `get_fs_type()` 时，另一次是如果 `read_super()` 成功，`get_sb_dev()` 调用 `get_filesystem()` 时。第一次增加是为了防止我们在 `read_super()` 方法内部时模块被卸载，而第二次增加是为了表明该模块正被此挂载实例使用。显然，`do_mount()` 在返回前会减少计数，因此总体而言，每次挂载后计数只增加 1。

- 由于在我们的情况下，`fs_type->fs_flags & FS_REQUIRES_DEV` 为真，超块通过调用 `get_sb_bdev()` 进行初始化，该函数获取对块设备的引用，并与文件系统的 `read_super()` 方法交互以填充超块。如果一切顺利，`super_block` 结构体将被初始化，我们将拥有对文件系统模块的额外引用以及对底层块设备的引用。

- 分配一个新的 `vfsmount` 结构体，并将其链接到 `sb->s_mounts` 列表和全局的 `vfsmnt_list` 列表。 `vfsmount` 字段 `mnt_instances` 允许找到所有挂载在相同超块上的实例。 `mnt_list` 字段允许找到系统中所有超块的所有实例。 `mnt_sb` 字段指向此超块，而 `mnt_root` 持有 `sb->s_root` 目录项（dentry）的新引用。

作为一个不需要块设备即可挂载的 Linux 文件系统的简单示例，让我们来看看 `fs/pipe.c` 中的 pipefs。文件系统的序言相当简单明了，几乎不需要解释：

```c
static DECLARE_FSTYPE(pipe_fs_type, "pipefs", pipefs_read_super,
                      FS_NOMOUNT|FS_SINGLE);

static int __init init_pipe_fs(void)
{
    int err = register_filesystem(&pipe_fs_type);
    if (!err) {
        pipe_mnt = kern_mount(&pipe_fs_type);
        err = PTR_ERR(pipe_mnt);
        if (!IS_ERR(pipe_mnt))
            err = 0;
    }
    return err;
}

static void __exit exit_pipe_fs(void)
{
    unregister_filesystem(&pipe_fs_type);
    kern_umount(pipe_mnt);
}

module_init(init_pipe_fs)
module_exit(exit_pipe_fs)
```

文件系统类型为 `FS_NOMOUNT | FS_SINGLE`，这意味着它不能从用户空间挂载，且系统范围内只能有一个超块。 `FS_SINGLE` 标志还意味着它必须通过 `kern_mount()` 进行挂载（在它通过 `register_filesystem()` 成功注册之后，这正是 `init_pipe_fs()` 中所做的）。此函数中唯一的 bug 是，如果 `kern_mount()` 失败（例如，因为 `add_vfsmnt()` 中的 `kmalloc()` 失败），那么文件系统将保持已注册状态，但模块初始化失败。这将导致 `/proc/filesystems` 失败。（我刚刚发送了一个补丁给 Linus，指出虽然这不是当今的一个真正的 bug，因为管道不能被编译为模块，但应该考虑到将来它可能会变成模块化的观点）。

`register_filesystem()` 的结果是 `pipe_fs_type` 被链接到 `file_systems` 列表中，因此可以读取 `/proc/filesystems` 并找到其中的“pipefs”条目，其中带有“nodev”标志，表明未设置 `FS_REQUIRES_DEV`。 `/proc/filesystems` 文件实际上应该增强以支持所有新的 `FS_` 标志（我制作了一个补丁来实现这一点），但由于这会破坏所有使用它用户应用程序，所以无法这样做。尽管 Linux 内核接口在用户空间兼容性方面每分钟都在变化（只有改进），但 Linux 是一个非常保守的操作系统，它允许许多应用程序在很长一段时间内无需重新编译即可使用。

`kern_mount()` 的结果是：

- 通过在 `unnamed_dev_in_use` 位图中设置一位来分配一个新的未命名（匿名）设备号；如果没有更多位可用，则 `kern_mount()` 以 `EMFILE` 失败。

- 通过 `get_empty_super()` 分配一个新的超块结构体。 `get_empty_super()` 函数遍历由 `super_block` 引导的超块列表，寻找空条目，即 `s->s_dev == 0`。如果找不到这样的空超块，则使用 `GFP_USER` 优先级通过 `kmalloc()` 分配一个新的。系统范围内超块的最大数量在 `get_empty_super()` 中进行检查，因此如果开始失败，可以调整可调节的 `/proc/sys/fs/super-max`。



- 3. 调用文件系统特定的 `pipe_fs_type->read_super()` 方法，即 `pipes_read_super()`，该方法分配根 inode 和根目录项 `sb->s_root`，并将 `sb->s_op` 设置为 `pipefs_ops`。

- 4. 然后 `kern_mount()` 调用 `add_vfsmnt(NULL, sb->s_root, "none")`，该函数分配一个新的 `vfsmnt` 结构体并将其链接到 `vfsmnt_list` 和 `sb->s_mounts`。

- 5. `pipe_fs_type->kern_mnt` 被设置为这个新的 `vfsmount` 结构体并被返回。 `kern_mount()` 的返回值是一个 `vfsmount` 结构体的原因是，即使是 `FS_SINGLE` 文件系统也可以被多次挂载，它们的 `mnt->mnt_sb` 将指向相同的东西，从多次 `kern_mount()` 调用中返回这会显得愚蠢。

现在文件系统已注册并在内核中挂载，我们可以使用它。进入管道文件系统的入口点是`pipe(2)`系统调用，它由架构相关的函数`sys_pipe()`实现，但真正的工作是由可移植的`fs/pipe.c:do_pipe()`函数完成的。让我们来看看`do_pipe()`。与管道的交互发生在`do_pipe()`调用`get_pipe_inode()`以分配一个新的管道 inode 时。对于这个节点，`inode->i_sb`被设置为管道的超块`pipe_mnt->mnt_sb`，文件操作`i_fop`被设置为`rdwr_pipe_fops`，读者和写者的数量（`inode->i_pipe`中的字段）被设置为 1。之所以有一个单独的 inode 字段`i_pipe`而不是将其保存在`fs->private`联合体中，是因为管道和 FIFO 共享相同的代码，而 FIFO 可以存在于使用同一联合体中其他访问路径的其他文件系统中，这在 C 语言中是非常糟糕的，且只能靠纯粹的运气才能正常工作。

### 3.7 磁盘文件系统示例：BFS

是的，2.2.x 内核只是靠纯粹的运气才工作，一旦你稍微重新排列 inode 中的字段，它就会停止工作。

每次`pipe(2)`系统调用都会增加`pipe_mnt`挂载实例上的引用计数。

在 Linux 下，管道不是对称的（双向或流管道），即文件的两侧具有不同的`file->f_op`操作——分别是`read_pipe_fops`和`write_pipe_fops`。在读取端写入会返回 EBADF，在写入端读取也是如此。

作为一个基于磁盘的 Linux 文件系统的简单示例，让我们来看看 BFS。BFS 模块的序言在`fs/bfs/inode.c`中：

```c
static DECLARE_FSTYPE_DEV(bfs_fs_type, "bfs", bfs_read_super);

static int __init init_bfs_fs(void)
{
    return register_filesystem(&bfs_fs_type);
}

static void __exit exit_bfs_fs(void)
{
    unregister_filesystem(&bfs_fs_type);
}

module_init(init_bfs_fs)
module_exit(exit_bfs_fs)
```

使用了一个特殊的 fstype 声明宏`DECLARE_FSTYPE_DEV()`，它将`fs_type->flags`设置为`FS_REQUIRES_DEV`，以表明 BFS 需要挂载到一个真实的块设备上。

模块的初始化函数将文件系统注册到 VFS，而清理函数（仅在 BFS 被配置为模块时存在）将其注销。

随着文件系统注册完成，我们可以继续进行挂载，这将调用我们的`fs_type->read_super()`方法，该方法实现在`fs/bfs/inode.c::bfs_read_super()`中。它执行以下操作：

- 1. `set_blocksize(s->s_dev, BFS_BSIZE)`：由于我们即将通过缓冲区缓存与块设备层交互，我们必须初始化一些东西，即设置块大小，并通过字段`s->s_blocksize`和`s->s_blocksize_bits`通知 VFS。

- 2. `bh = bread(dev, 0, BFS_BSIZE)`：我们读取通过`s->s_dev`传递的设备块 0。这个块是文件系统的超块。

- 3. 超块针对`BFS_MAGIC`号进行验证，如果有效，则存储在 sb--私有字段`s->su_sbh`（实际上是`s->u.bfs_sb.s_bhn`）中。

- 4. 然后使用`kmalloc(GFP_KERNEL)`分配 inode 位图，并将所有位清除为 0，除了前两位被设置为 1，以表明我们应该永远不分配 inode 0 和 1。inode 2 是根，对应的位反正会在稍后的几行被设置为 1——文件系统应该有一个

挂载时有效的根 inode！

- 5. 然后我们初始化`s->s_op`，这意味着从这一点开始，我们可以调用`iget()`来访问 inode 缓存，这将导致调用`s_op->read_inode()`。该操作会找到包含指定（由`inode->i_ino`和`inode->i_dev`指定）inode 的块并将其读入。如果我们无法获取根 inode，则释放 inode 位图并将超级块缓冲区交还给缓冲区缓存，然后返回`NULL`。如果成功读取了根 inode，则分配一个名为`/`（因为这是根）的 dentry，并用该 inode 对其进行实例化。

- 6. 现在，我们遍历文件系统上的所有 inode 并将它们全部读入，以设置内部 inode 位图中相应的位，并计算其他一些内部参数，例如最后一个 inode 的偏移量以及最后一个文件的起始/结束块。我们读取的每个 inode 都会通过`iput()`交还给 inode 缓存——我们不会比需要的时间更长时间地持有其引用。

- 7. 如果文件系统不是以只读方式挂载的，我们将超级块缓冲区标记为脏，并设置`s->s_dirty`标志（TODO：我为什么要这样做？最初，我这样做是因为`minix_read_super()`这样做，但 minix 和 BFS 似乎都没有在`read_super()`中修改超级块）。

- 8. 一切顺利，所以我们向 VFS 级别的调用者（即`fs/super.c:read_super()`）返回这个已初始化的超级块。

当`read_super()`函数成功返回后，VFS 通过调用`fs/super.c:get_sb_bdev()`中的`get_filesystem(fs_type)`获得文件系统模块的引用，以及块设备的引用。

现在，让我们看看在文件系统进行 I/O 时会发生什么。我们已经检查了在调用`iget()`时 inode 是如何被读取的，以及在调用`iput()`时它们是如何被释放的。读取 inode 会设置（除其他内容外）`inode->i_op`和`inode->i_fop`；打开文件会将`inode->i_fop`传播到`file->f_op`。

让我们检查`link(2)`系统调用的代码路径。系统调用的实现位于`fs/namei.c:sys_link()`中：

- 1. 用户空间的名称通过`getname()`函数复制到内核空间，该函数还执行错误检查。

- 2. 使用与 dcache 交互的`path_init()/path_walk()`将这些名称转换为 nameidata。结果存储在`old_nd`和`nd`结构中。

- 3. 如果`old_nd.mnt != nd.mnt`，则返回 "cross-device link" EXDEV 错误——不能在不同文件系统之间创建链接，在 Linux 中这意味着不能在不同挂载的文件系统实例（或特定地，不同文件系统）之间创建链接。

- 4. 通过`lookup_create()`创建对应于`nd`的新 dentry。

- 5. 调用通用的`vfs_link()`函数，该函数检查我们是否可以在目录中创建新条目，并调用`dir->i_op->link()`方法，这将我们带回到文件系统特定的`fs/bfs/dir.c:bfs_link()`函数。

- 6. 在`bfs_link()`内部，我们检查是否试图链接目录，如果是，则以 EPERM 错误拒绝。这与标准（ext2）的行为相同。

- 7. 我们通过调用辅助函数`bfs_add_entry()`尝试将新的目录项添加到指定目录中，该函数遍历所有条目以查找未使用的槽位（`de->ino == 0`），并在找到时，将名称/inode 对写入对应的块并将其标记为脏（以非超级块优先级）。



- 8. 如果我们成功添加了目录项，则操作没有失败的方式，因此我们递增 `inode->i_nlink`，更新 `inode->i_ctime`，并将此 inode 标记为脏，同时用该 inode 实例化新的 dentry。

其他相关的 inode 操作如 `unlink()` `/ rename()` 等以类似的方式工作，因此详细检查它们并没有太大收获。

### 3.8 执行域和二进制定位

Linux 支持从磁盘加载用户应用程序二进制文件。更有趣的是，这些二进制文件可以存储在不同的格式中，并且操作系统通过系统调用对程序的响应可以根据需要偏离常规（常规是指 Linux 的行为），以模拟其他 UNIX 变体（COFF 等）中发现的格式，同时也模拟其他变体（Solaris, UnixWare 等）的系统调用行为。这就是执行域和二进制定位格式的作用所在。

每个 Linux 任务都在其 `task_struct (p->personality)` 中存储了一个 personality（个性/人格）。当前存在的（在内核官方中或作为附加补丁） personalities 包括对 FreeBSD、Solaris、UnixWare、OpenServer 以及其他许多流行操作系统的支持。`current->personality` 的值分为两部分：

- 1. 高三个字节 – bug 模拟：`STICKY_TIMEOUTS`、`WHOLE_SECONDS` 等

- 2. 低字节 – 真正的 personality，一个唯一的编号。

通过更改 personality，我们可以改变操作系统处理某些系统调用的方式，例如，向 `current->personality` 添加 `STICKY_TIMEOUT` 会使 `select(2)` 系统调用保留最后一个参数（timeout）的值，而不是存储未睡眠的时间。某些有缺陷的程序依赖于有缺陷的操作系统（非 Linux），因此 Linux 提供了一种方法来模拟 bug，在源代码不可用因此无法修复 bug 的情况下。

执行域是由单个模块实现的一组连续的 personality 范围。通常，单个执行域实现单个 personality，但有时也可以在单个模块中实现“接近”的 personality，而无需太多的条件判断。

执行域在 `kernel/exec_domain.c` 中实现，与 2.2.x 相比，在 2.4 内核中进行了完全重写。通过读取 `/proc/execdomains` 文件，可以查看内核当前支持的执行域列表以及它们支持的 personality 范围。除了 `PER_LINUX` 之外，执行域可以作为动态加载模块实现。

用户界面通过 `personality(2)` 系统调用，它设置当前进程的 personality，或者如果参数设置为不可能的 personality `0xffffffff`，则返回 `current->personality` 的值。显然，该系统调用本身的行为不依赖于 personality。

内核接口用于执行域注册，由两个函数组成：

- `int register_exec_domain(struct exec_domain *);` 通过将其链接到单链表 `exec_domains` 来注册执行域，并在读写自旋锁 `exec_domains_lock` 的写保护下进行操作。成功返回 `0`，失败返回 `non-zero`。

- `int unregister_exec_domain(struct exec_domain *);` 通过将其从 `exec_domains` 列表中解除链接来注销执行域，再次使用写模式的 `exec_domains_lock` 自旋锁。成功返回 `0`。

`exec_domains_lock` 是读-写自旋锁的原因是，只有注册和注销请求会修改列表，而执行 `cat /proc/filesystems` 会调用 `fs/exec_domain.c::get_exec_domain_list()`，这只需要对列表进行读访问。

注册新的执行域定义了“lcall7 处理器”和一个信号编号转换映射。实际上，ABI 补丁将此执行域概念扩展以包含额外信息（如 socket 选项、socket 类型、地址族和 errno 映射）。

二进制定位格式以类似的方式实现，即在 `fs/exec.c` 中定义一个单链表 `formats`，并由读-写锁 `binfmt_lock` 保护。与 `exec_domains_lock` 一样，`binfmt_lock` 在大多数情况下以读模式获取，除了二进制格式的注册/注销外。注册新的二进制定位格式增强了 `execve(2)` 系统调用，增加了新的 `load_binary()` / `load_shlib()` 函数以及 `core_dump()` 的能力。`load_shlib()` 方法仅由旧的 `usrleib` 系统调用使用，而 `load_binary()` 方法由 `do_execve()` 中的 `search_binary_handler()` 调用，后者实现了 `execve(2)` 系统调用。

进程的 personality 在加载二进制定位格式时由相应格式的 `load_binary()` 方法通过一些启发式方法确定。例如，为了确定 UnixWare7 二进制文件，首先使用 `elfmark(1)` 实用工具标记二进制文件，该工具将 ELF 头的 `e_flags` 设置为魔术值 `0x314B4455`，这在 ELF 加载时会被检测到，并将 `current->personality` 设置为 `PER_UW7`。如果此启发式方法失败，则使用更通用的方法，例如将 ELF 解释器路径视为 `/usr/lib/ld.so.1` 或 `/usr/lib/libc.so.1` 以指示 SVR4 二进制文件，并将 personality 设置为 `PER_SVR4`。可以编写一个小实用工具，利用 Linux 的 `prace(2)` 能力单步执行代码，强制运行中的程序进入任何 personality。

一旦知道 personality（因此也知道了 `current->exec_domain`），系统调用将按以下方式处理。让我们假设一个进程通过 lcall7 门指令进行系统调用。由于在 `arch/i386/kernel/traps.c:trap_init()` 中进行了准备，这将控制权转移到 `arch/i386/kernel/entry.S` 中的 `ENTRY (lcall7)`。在适当的栈布局转换后，`entry.S:lcall7` 从 `current` 获取 `exec_domain` 的指针，然后获取 `exec_domain` 中 lcall7 处理器的偏移量（这在汇编代码中硬编码为 4，因此你不能在 `struct exec_domain` 的 C 声明中移动 handler 字段）并跳转到它。因此，在 C 中，它看起来像这样：

```c
static void UW7_lcall7(int segment, struct pt_regs * regs)
{
    abI_dispatch(regs, &uw7_funcs[regs->eax & 0xff], 1);
}
```

其中 `abi_dispatch()` 是实现此 personality 的系统调用 `uw7_funcs` 的函数指针表的包装器。

## 4. Linux 页缓存

在本章中，我们描述 Linux 2.4 的页缓存。页缓存——顾名思义——是物理页面的缓存。在 UNIX 世界中，页缓存的概念随着 SVR4 UNIX 的引入而变得流行，它取代了用于数据 IO 操作的缓冲区缓存。

虽然 SVR4 页缓存仅用于文件系统数据缓存，因此使用 `struct vnode` 和文件中的偏移量作为哈希参数，但 Linux 页缓存旨在更通用，因此使用

## 5. 进程间通信机制

本章描述了 Linux 2.4 内核中实现的信号量、共享内存和消息队列进程间通信机制。本章分为四个部分。前三个部分分别介绍了信号量、消息队列和共享内存的接口和支持函数。最后一个部分描述了一组由所有三种机制共享的公共函数和数据结构。

### 5.1 信号量

本节描述的函数实现了用户级信号量机制。请注意，此实现依赖于内核自旋锁和内核信号量的使用。为了避免混淆，术语“内核信号量”将专门用于指代内核信号量。单词“信号量”的其他所有用法均指代用户级信号量。

#### 信号量系统调用接口

##### sys_semget()

对 `sys_semget()` 的整个调用都由全局信号量内核信号量 `sem_ids.sem` 保护。

- 如果需要创建一组新的信号量，则调用 `newary()` 函数来创建并初始化一个新的信号量集。新集合的 ID 将返回给调用者。

- 如果为现有的信号量集提供了键值，则调用 `ipc_findkey()` 以查找相应的信号量描述符数组索引。在返回信号量集 ID 之前，会验证调用者的参数和权限。

##### sys_semctl()

- 对于 `IPC_INFO`、`SEM_INFO` 和 `SEM_STAT` 命令，调用 `semctl_nolock()` 来执行必要的功能。



- 对于 `GETALL`、`GETVAL`、`GETPID`、`GETNCNT`、`GETZCNT`、`IPC_STAT`、`SETVAL` 和 `SETALL` 命令，调用 `semctl_main()` 来执行必要的功能。

- 对于 `IPC_RMID` 和 `IPC_SET` 命令，调用 `semctl_down()` 来执行必要的功能。在这两个操作的全程中，都会持有全局信号量内核信号量 `sem_ids.sem`。

### `sys_semmop()`

在验证调用参数后，信号量操作数据会从用户空间复制到临时缓冲区。如果小型临时缓冲区足够，则使用栈缓冲区。否则，将分配一个较大的缓冲区。在复制入信号量操作数据后，锁定全局信号量自旋锁，并验证用户指定的信号量集 `ID`。同时还会验证信号量集的访问权限。

解析所有用户指定的信号量操作。在此过程中，维护一个计数，统计所有设置了 `SEM_UNDO` 标志的操作。如果任何操作都从信号量值中减去，则设置一个递减标志；如果任何信号量值被修改（即增加或减少），则设置一个更改标志。验证要修改的每个信号量的数量。

### 非阻塞信号量操作

如果信号量操作中的任何一个都断言了 `SEM_UNDO`，则会在当前任务的撤销列表中查找与该信号量集关联的撤销结构。在此搜索过程中，如果发现任何撤销结构的信号量集 `ID` 为 `-1`，则调用 `freecundos()` 以释放撤销结构并将其从列表中移除。如果未找到该信号量集的撤销结构，则调用 `alloc_undo()` 来分配并初始化一个。

调用 `try_atomic_semop()` 函数，并将 `do_undo` 参数设置为 `0`，以执行操作序列。返回值指示操作是通过、失败，还是因为需要阻塞而未执行。下面将分别详细介绍这些情况：

当序列中的所有操作都成功时，`try_atomic_semop()` 函数返回零。在这种情况下，调用 `update_queue()` 遍历信号量集的挂起信号量操作队列，唤醒任何不再需要阻塞的休眠任务。这就完成了该情况下 `sys_semop()` 系统调用的执行。

### 失败的信号量操作

如果 `try_atomic_semop()` 返回负值，则说明遇到了失败条件。在这种情况下，没有执行任何操作。当某个信号量操作会导致无效的信号量值，或者标记为 `IPC_NOWAIT` 的操作无法完成时，就会发生这种情况。随后，错误条件返回给 `sys_semop()` 的调用者。

在 `sys_semop()` 返回之前，会调用 `update_queue()` 遍历信号量集的挂起信号量操作队列，并唤醒任何不再需要阻塞的休眠任务。

### 阻塞的信号量操作

当其中一个信号量会阻塞时，`try_atomic_semop()` 函数返回 `1`，指示信号量操作序列未被执行。针对这种情况，会初始化一个新的 `sem_queue` 元素，其中包含这些信号量操作。如果其中任何一个操作会改变信号量的状态，则新的队列元素被添加到队列的尾部；否则，新的队列元素被添加到队列的头部。

当前任务的 `semsleeping` 元素被设置为指示该任务正在此 `sem_queue` 元素上休眠。当前任务被标记为 `TASK_INTERRUPTIBLE`，并且 `sem_queue` 的 `sleeper` 元素被设置以标识此任务为休眠者。然后解锁全局信号量自旋锁，并调用 `schedule()` 使当前任务进入睡眠状态。

被唤醒时，任务重新锁定全局信号量自旋锁，确定其被唤醒的原因以及应如何响应。处理以下情况：

- 如果信号量集已被移除，则系统调用以 `EIDRM` 失败。
- 如果 `sem_queue` 结构的 `status` 元素设置为 `1`，则任务被唤醒是为了重试信号量操作。再次调用 `try_atomic_semop()` 以执行信号量操作序列。如果 `try_atomic_semop()` 返回 `1`，则任务必须如上所述再次阻塞。否则，成功时返回 `0`，失败时返回适当的错误码。在 `sys_semop()` 返回之前，清除 `current->semsleeping`，并将 `sem_queue` 从队列中移除。如果指定的信号量操作中有任何修改操作（增加或减少），则调用 `update_queue()` 遍历信号量集的挂起信号量操作队列，并唤醒任何不再需要阻塞的休眠任务。
- 如果 `sem_queue` 结构的 `status` 元素未设置为 `1`，且 `sem_queue` 元素尚未出队，则任务是被中断唤醒的。在这种情况下，系统调用以 `EINTR` 失败。在返回之前，清除 `current->semsleeping`，并将 `sem_queue` 从队列中移除。此外，如果任何操作都是修改操作，则调用 `update_queue()`。
- 如果 `sem_queue` 结构的 `status` 元素未设置为 `1`，且 `sem_queue` 元素已经出队，则信号量操作已经由 `update_queue()` 执行完毕。队列的 `status`（成功时为 `0`，失败时为取反的错误码）成为系统调用的返回值。

### 信号量专用支持结构

以下结构专门用于信号量支持：

#### `struct sem_array`

```c
/* 系统中每个信号量集对应一个 sem_array 数据结构。 */
struct sem_array {
    struct kern_ipc_perm sem_perm; /* 权限 .. 参见 ipc.h */
    time_t sem_otime; /* 最后一次 semop 时间 */
    time_t sem_ctime; /* 最后一次变更时间 */
    struct sem *sem_base; /* 指向数组中第一个信号量的指针 */
    struct sem_queue *sem_pending; /* 待处理的操作 */
    struct sem_queue **sem_pending_last; /* 最后一个待处理操作 */
    struct sem_undo *undo; /* 针对此数组的撤销请求 */
    unsigned long sem_nsems; /* 数组中的信号量数量 */
};
```

#### `struct sem`

```c
/* 系统中每个信号量对应一个结构体。 */
struct sem {
    int semval; /* 当前值 */
    int sempid; /* 最后一次操作的进程 ID */
};
```

#### `struct seminfo`

```c
struct seminfo {
    int semmap;
    int semmni;
    int semmns;
    int semmnu;
    int semmsl;
    int semopm;
    int semume;
    int semusz;
    int semvmx;
    int semaseg;
};
```

#### `struct semid64_ds`

```c
struct semid64_ds {
    struct ipc64_perm sem_perm; /* 权限 .. 参见 ipc.h */
    __kernel_time_t sem_otime; /* 最后一次 semop 时间 */
    unsigned long __unused1;
    __kernel_time_t sem_ctime; /* 最后一次变更时间 */
    unsigned long __unused2;
    unsigned long sem_nsems; /* 数组中的信号量数量 */
    unsigned long __unused3;
    unsigned long __unused4;
};
```

#### `struct sem_queue`

```c
/* 系统中每个休眠进程对应一个队列。 */
struct sem_queue {
    struct sem_queue * next; /* 队列中的下一个条目 */
    struct sem_queue ** prev; /* 队列中的上一个条目，* (\n q->prev) == q */
    struct task_struct *sleeper; /* 此进程 */
    struct sem_undo * undo; /* 撤销结构 */
    int pid; /* 请求进程的进程 ID */
    int status; /* 操作的完成状态 */
    struct sem_array * sma; /* 操作所在的信号量数组 */
    int id; /* 内部信号量 ID */
    struct sembuf * sops; /* 待操作数组 */
    int nsops; /* 操作数量 */
    int alter; /* 操作将修改信号量 */
};
```

#### `struct sembuf`



```c
/* semop 系统调用使用这些元素的数组。 */
struct sembuf {
    unsigned short sem_num; /* 信号量在数组中的索引 */
    short sem_op; /* 信号量操作 */
    short sem_flg; /* 操作标志 */
};
```

#### `struct sem_undo`

```c
/* 每个任务都有一个撤销请求列表。当进程退出时，它们会被自动执行。 */
struct sem_undo {
    struct sem_undo *    proc_next;    /* 此进程中的下一个条目 */
    struct sem_undo *    id_next;      /* 此信号量集中的下一个条目 */
    int                  semid;        /* 信号量集标识符 */
    short *              semadj;       /* 调整数组，每个
                                          信号量对应一个 */
};
```

### 信号量支持函数

以下函数专门用于支持信号量：

#### `newary()`

`newary()` 依赖 `ipc_alloc()` 函数来分配新信号量集所需的内存。它分配足够内存用于信号量集描述符以及集中的每个信号量。分配的内存被清空，并将信号量集描述符第一个元素的地址传递给 `ipc_addid()`。`ipc_addid()` 为新信号量集描述符预留数组条目，并初始化该集的 `struct kern_ipc_perm` 数据。全局 `used_sems` 变量会根据新集中的信号量数量进行更新，并且完成新集的 `struct kern_ipc_perm` 数据的初始化。该集的其他初始化操作如下所列：

- 该集的 `sem_base` 元素初始化为紧随新分配数据中 `struct sem_array` 部分之后的地址。这对应于该集中第一个信号量的位置。
- `sem_pending` 队列初始化为空。

在调用 `ipc_addid()` 之后的所有操作都在持有全局信号量自旋锁的情况下执行。解锁全局信号量自旋锁后，`newary()` 调用 `ipc_buildid()`（通过 `sem_buildid()`）。该函数使用信号量集描述符的索引创建唯一 ID，然后将其返回给 `newary()` 的调用者。

#### `freeary()`

`freeary()` 由 `semctl_down()` 调用以执行以下列出的功能。调用它时全局信号量自旋锁处于锁定状态，并且返回时自旋锁处于解锁状态。

- 调用 `ipc_rmid()` 函数（通过 `sem_rmid()` 包装器）以删除信号量集的 ID 并获取指向信号量集的指针。
- 使信号量集的撤销列表失效。
- 唤醒所有挂起进程，并使其以 `EIDRM` 失败。
- 已使用信号量的数量减去被移除集中的信号量数量。
- 释放与信号量集关联的内存。

### `semctl_down()`

`semctl_down()` 提供了 `semctl()` 系统调用的 `IPC_RMID` 和 `IPC_SET` 操作。在执行这些操作之前，会验证信号量集 ID 和访问权限，并且在这两种情况下，整个操作过程中都会持有全局信号量自旋锁。

#### `IPC_RMID`

`IPC_RMID` 操作调用 `freeary()` 来移除信号量集。

#### `IPC_SET`

`IPC_SET` 操作更新信号量集的 `uid`、`gid`、`mode` 和 `ctime` 元素。

### `semctl_nolock()`

`semctl_nolock()` 由 `sys_semctl()` 调用，用于执行 `IPC_INFO`、`SEM_INFO` 和 `SEM_STAT` 功能。

#### `IPC_INFO` 和 `SEM_INFO`

`IPC_INFO` 和 `SEM_INFO` 会导致初始化一个临时的 `seminfo` 缓冲区，并加载不变的信号量统计数据。然后，在全局 `sem_ids.sem` 内核信号量保持持有的状态下，根据给定的命令（`IPC_INFO` 或 `SEM_INFO`）更新 `seminfo` 结构中的 `semusz` 和 `semaem` 元素。系统调用的返回值被设置为最大信号量集 ID。

#### `SEM_STAT`

`SEM_STAT` 会导致初始化一个临时的 `semid64_ds` 缓冲区。然后，在持有全局信号量自旋锁的同时，将 `sem_otime`、`sem_ctime` 和 `sem_nsems` 值复制到缓冲区中。这些数据随后被复制到用户空间。

### `semctl_main()`

`semctl_main()` 由 `sys_semctl()` 调用，用于执行以下子节中描述的许多支持的功能。在执行以下任何操作之前，`semctl_main()` 会锁定全局信号量自旋锁，并验证信号量集 ID 和权限。在返回之前释放自旋锁。

#### `GETALL`

`GETALL` 操作将当前的信号量值加载到临时内核缓冲区，并将其复制到用户空间。如果信号量集较小，则使用小型栈缓冲区。否则，临时释放自旋锁以分配较大的缓冲区。在将信号量值复制到临时缓冲区时持有自旋锁。

#### `SETALL`

`SETALL` 操作将信号量值从用户空间复制到临时缓冲区，然后再复制到信号量集中。在将值从用户空间复制到临时缓冲区以及验证合理值的过程中，会释放自旋锁。如果信号量集较小，则使用栈缓冲区，否则分配较大的缓冲区。在对信号量集执行以下操作时，重新获取并保持持有自旋锁：

- 将信号量值复制到信号量集中。
- 清除信号量集撤销队列中的信号量调整值。
- 设置信号量集的 `sem_ctime` 值。
- 调用 `update_queue()` 函数遍历待处理的 `semops` 队列，查找因 `SETALL` 操作而可以完成的任务。唤醒那些不再阻塞的待处理任务。

#### `IPC_STAT`

在 `IPC_STAT` 操作中，`sem_otime`、`sem_ctime` 和 `sem_nsems` 值被复制到栈缓冲区中。然后在释放自旋锁后，数据被复制到用户空间。

#### `GETVAL`

对于非错误情况下的 `GETVAL`，系统调用的返回值被设置为指定信号量的值。

#### `GETPID`

对于非错误情况下的 `GETPID`，系统调用的返回值被设置为与最近一次对信号量的操作相关联的 `pid`。

#### `GETNCNT`

对于非错误情况下的 `GETNCNT`，系统调用的返回值被设置为等待信号量值小于零的进程数量。该数量由 `count_semcnt()` 函数计算得出。

#### `GETZCNT`

对于非错误情况下的 `GETZCNT`，系统调用的返回值被设置为等待信号量值为零的进程数量。该数量由 `count_semzcnt()` 函数计算得出。

#### `SETVAL`

在验证新的信号量值之后，执行以下操作：

- 搜索撤销队列以查找对该信号量的任何调整。将找到的任何调整重置为零。
- 将信号量值设置为提供的值。
- 更新信号量集的 `sem_ctime` 值。
- 调用 `update_queue()` 函数遍历待处理的 `semops` 队列，查找因 `SETALL` 操作而可以完成的任务。唤醒那些不再阻塞的待处理任务。

### `count_semcnt()`

`count_semcnt()` 统计等待信号量值小于零的任务数量。

### `count_semzcnt()`

`count_semzcnt()` 统计等待信号量值为零的任务数量。

### `update_queue()`

`update_queue()` 遍历信号量集的待处理 `semops` 队列，并调用 `try_atomic_semop()` 来确定哪些信号量操作序列将会成功。如果队列元素的状态表明阻塞的任务已经被唤醒，则跳过该队列元素。对于队列的其他元素，将 `q-alter` 标志作为撤销参数传递给 `try_atomic_semop()`，表明在返回之前应该撤销任何更改操作。

如果操作序列会导致阻塞，则 `update_queue()` 不进行任何更改即返回。

如果其中一个信号量操作会导致无效的信号量值，或者标记为 `IPC_NOWAIT` 的操作无法完成，则操作序列可能会失败。在这种情况下，阻塞在该信号量操作序列上的任务被唤醒，并且队列状态被设置为适当的错误代码。该队列元素也被出队。

如果操作序列是非更改性的，那么它们会将零值作为撤销参数传递给 `try_atomic_semop()`。如果这些操作成功，则被视为已完成并从队列中移除。唤醒阻塞的任务，并将队列元素的状态设置指示成功。

如果操作序列会更改信号量值但可以成功，则唤醒不再需要阻塞的休眠任务。队列状态被设置为 1，以指示阻塞任务已被唤醒。由于操作尚未执行，因此队列元素未从队列中移除。信号量操作将由被唤醒的任务执行。

### `try_atomic_semop()`



`try_atomic_semop()` 由 `sys_semop()` 和 `update_queue()` 调用，以确定一系列信号量操作是否都会成功。它通过尝试执行每个操作来确定这一点。

如果遇到阻塞操作，则中止进程并反转所有操作。如果设置了 `IPC_NOWAIT`，则返回 `-EAGAIN`。否则，返回 1 以指示该信号量操作序列被阻塞。

如果信号量值超出系统限制而被调整，则反转所有操作，并返回 `-ERANGE`。

如果序列中的所有操作都成功，且 `do_undo` 参数非零，则反转所有操作，并返回 0。如果 `do_undo` 参数为零，则所有操作成功并保持生效，并更新信号量集的 `sem_otime` 字段。

### `sem_revalidate()`

`sem_revalidate()` 在全局信号量自旋锁被临时释放并需要再次锁定时调用。它由 `semctl_main()` 和 `alloc_undo()` 调用。它验证信号量 ID 和权限，成功时，在全局信号量自旋锁锁定的状态下返回。

### `freeundos()`

`freeundos()` 遍历进程撤销列表以查找所需的撤销结构。如果找到，则从列表中移除该撤销结构并释放它。返回进程列表中下一个撤销结构的指针。

### `alloc_undo()`

`alloc_undo()` 期望在全局信号量自旋锁锁定时调用。在发生错误的情况下，它会解锁后返回。

解除全局信号量自旋锁，并调用 `kmalloc()` 为 `sem_undo` 结构以及集中每个信号量的一个调整值数组分配足够的内存。成功时，通过调用 `sem_revalidate()` 重新获取全局自旋锁。

然后初始化新的 `semundo` 结构，并将该结构的地址放置在调用者提供的地址处。新的撤销结构随后被放置在当前任务的撤销列表的头部。

### `sem_exit()`

`sem_exit()` 由 `do_exit()` 调用，并负责执行退出任务的所有撤销调整。

如果当前进程阻塞在某个信号量上，则在持有全局信号量自旋锁的情况下将其从 `sem_queue` 列表中移除。

然后遍历当前任务的撤销列表，在处理列表的每个元素时持有和释放全局信号量自旋锁，并执行以下操作。对每个撤销元素执行以下操作：

- 验证撤销结构和信号量集 ID。
- 搜索相应信号量集的撤销列表，以找到对同一撤销结构的引用，并将其从该列表中移除。
- 将撤销结构中指示的调整值应用到信号量集。
- 更新信号量集的 `sem_otime` 参数。
- 调用 `update_queue()` 遍历待处理的 `semops` 队列，并唤醒因执行撤销操作而不再需要阻塞的休眠任务。
- 释放撤销结构。

当列表处理完成后，`current->semundo` 值被清除。

## 5.2 消息队列

### 消息系统调用接口

#### `sys_msget()`

整个对 `sys_msget()` 的调用由全局消息队列信号量（`msg_ids_sem`）保护。

如果需要创建新的消息队列，则调用 `newque()` 函数来创建并初始化一个新的消息队列，并将新的队列 ID 返回给调用者。

如果为已存在消息队列提供了键值，则调用 `ipc_findkey()` 在全局消息队列描述符数组（`msg_ids.entries`）中查找对应的索引。在返回消息队列 ID 之前，会验证调用者的参数和权限。查找操作和验证是在持有全局消息队列自旋锁（`msg_ids.ary`）的情况下执行的。

#### `sys_msgctl()`

传递给 `sys_msgctl()` 的参数包括：消息队列 ID（`msgid`）、操作（`cmd`）以及指向用户空间缓冲区（类型为 `msgid_ds`）的指针（`buf`）。该函数提供了六种操作：`IPC_INFO`、`MSG_INFO`、`IPC_STAT`、`MSG_STAT`、`IPC_SET` 和 `IPC_RMID`。验证消息队列 ID 和操作参数后，按以下方式执行操作（`cmd`）：

##### `IPC_INFO` (或 `MSG_INFO`)

将全局消息队列信息复制到用户空间。

##### `IPC_STAT` (或 `MSG_STAT`)

初始化一个类型为 `struct msgid64_ds` 的临时缓冲区，并锁定全局消息队列自旋锁。在验证调用进程的访问权限后，将关联于该消息队列 ID 的消息队列信息加载到临时缓冲区中，解锁全局消息队列自旋锁，然后通过 `copy_msgid_to_user()` 将临时缓冲区的内容复制到用户空间。

##### `IPC_SET`

通过 `copy_msgid_to_user()` 复制用户数据。获取全局消息队列信号量和自旋锁，并在最后释放。在验证消息队列 ID 和当前进程访问权限后，使用用户提供的数据更新消息队列信息。随后，调用 `expunge_all()` 和 `ss_wakeup()` 唤醒所有在消息队列的接收者等待队列和发送者等待队列上睡眠的进程。这是因为某些接收者可能因更严格的访问权限而被排除，而某些发送者可能由于队列大小增加而能够发送消息。

##### `IPC_RMID`

获取全局消息队列信号量并锁定全局消息队列自旋锁。在验证消息队列 ID 和当前任务访问权限后，调用 `freemsg()` 释放与消息队列 ID 相关的资源。释放全局消息队列信号量和自旋锁。

#### `sys_msgsnd()`

`sys_msgsnd()` 接收的参数包括：消息队列 ID（`msqid`）、指向类型为 `struct msg_msg` 缓冲区的指针（`msgp`）、要发送消息的大小（`msgsz`）以及指示等待或不等标志（`msgflg`）。与消息队列 ID 关联有两个任务等待队列和一个消息队列。如果接收者等待队列中有任务正在等待此消息，则直接将消息交付给接收者，并唤醒接收者。否则，如果消息等待队列中有足够的可用空间，则将该消息保存在此队列中。作为最后的手段，发送任务会将其自身加入发送者等待队列。以下是关于 `sys_msgsnd()` 执行操作更深入讨论：

1. 验证用户缓冲区地址和消息类型，然后调用 `load_msg()` 将用户消息的内容加载到类型为 `struct msg_msg` 的临时对象 `msg` 中。同时初始化 `msg` 的消息类型和消息大小字段。
2. 锁定全局消息队列自旋锁并获取与消息队列 ID 关联的消息队列描述符。如果不存在这样的消息队列，则返回 `EINVAL`。
3. 通过 `msg_checkid()` 调用 `ipc_checkid()` 以验证消息队列 ID 有效，并调用 `ipcperms()` 检查调用进程的访问权限。
4. 检查消息大小和消息等待队列中剩余空间，以确定是否有足够的空间存储该消息。如果没有，则执行以下子步骤：
   1. 如果 `msgflg` 中指定了 `IPC_NOWAIT`，则解锁全局消息队列自旋锁，释放该消息的内存资源，并返回 `EAGAIN`。
   2. 调用 `ss_add()` 将当前任务加入发送者等待队列。它还解锁全局消息队列自旋锁并调用 `schedule()` 使当前任务进入睡眠状态。
   3. 当被唤醒时，重新获取全局自旋锁并验证消息队列 ID 是否仍然有效。如果消息队列 ID 无效，则返回 `ERMID`。
   4. 调用 `ss_del()` 将发送任务从发送者等待队列中移除。如果该任务有任何待处理信号，`sys_msgsnd()` 解锁全局自旋锁，调用 `free_msg()` 释放消息缓冲区，并返回 `EINTR`。否则，函数返回重新检查消息等待队列中是否有足够的空间。
5. 调用 `pipelined_send()` 尝试直接将该消息发送给等待的接收者。
6. 如果没有接收者正在等待此消息，则将该消息入队至消息等待队列（`msq->q_messages`）。更新消息队列描述符的 `q_cbytes` 和 `q_cnum` 字段，以及全局变量 `msg_bytes` 和 `msg_hdrs`，后者分别指示系统中消息使用的总字节数和消息总数。
7. 如果消息成功发送或入队，则更新消息队列描述符的 `q_lspid` 和 `q_stime` 字段，并释放全局消息队列自旋锁。

#### `sys_msgrcv()`

`sys_msgrcv()` 函数接收的参数包括：消息队列 ID（`msqid`）、指向类型为 `msg_msg` 缓冲区的指针（`msgp`）、期望的消息大小（`msgsz`）、消息类型（`msgtyp`）以及标志（`msgflg`）。它搜索与消息队列 ID 关联的消息等待队列，找到队列中第一个符合请求类型的消息，并将其复制到给定的用户缓冲区中。如果在消息等待队列中未找到这样的消息，则请求任务被加入接收者等待队列，直到所需消息可用。以下是关于 `sys_msgrcv()` 执行操作更深入讨论：

1. 首先，调用 `convert_mode()` 从 `msgtyp` 推导搜索模式。`sys_msgrcv()` 随后锁定全局消息队列自旋锁并获取与消息队列 ID 关联的消息队列描述符。如果不存在这样的消息队列，则返回 `EINVAL`。
2. 检查当前任务是否具有访问该消息队列的正确权限。



3. 从消息等待队列中的第一条消息开始，调用 `testmsg()` 检查消息类型是否匹配所需类型。`sys_msgrcv()` 继续搜索，直到找到匹配的消息或整个等待队列遍历完毕。如果搜索模式为 `SEARCH_LESSEQUAL`，则搜索队列中类型小于或等于 `msgtype` 的第一个消息。

4. 如果找到消息，`sys_msgrcv()` 执行以下子步骤：

    1. 如果消息大小大于期望大小且 `msgflg` 指示不允许错误，则解锁全局消息队列自旋锁并返回 `E2BIG`。

    2. 将消息从消息等待队列中移除并更新消息队列统计信息。

    3. 唤醒所有在发送者等待队列上睡眠的任务。上一步中从队列中移除消息使得其中一个发送者有可能继续推进。进入最后一步。

5. 如果在消息等待队列中未找到符合接收者条件的消息，则检查 `msgflg`。如果设置了 `IPC_NOWAIT`，则解锁全局消息队列自旋锁并返回 `ENOMSG`。否则，按如下方式将接收者加入接收者等待队列：

    1. 分配一个 `msgr` 数据结构并将其添加到等待队列头部。

    2. 将 `msgr` 的 `r_task` 字段设置为当前任务。

    3. 将 `r_msgtype` 和 `r_mode` 字段分别初始化为期望的消息类型和模式。

    4. 如果 `msgflg` 指示 `MSG_NOERROR`，则将 `msgr` 的 `r_maxsize` 字段设置为 `msgsz` 的值；否则设置为 `INT_MAX`。

    5. 将 `r_msg` 字段初始化为指示尚未接收到任何消息。

    6. 初始化完成后，将接收任务的状态设置为 `TASK_INTERRUPTIBLE`，解锁全局消息队列自旋锁，并调用 `schedule()`。

    7. 接收者被唤醒后，检查 `msgr` 的 `r_msg` 字段。该字段用于存储流水线消息，或在发生错误时存储错误状态。如果 `r_msg` 字段包含所需消息，则进入最后一步。否则，重新锁定全局消息队列自旋锁。

7. 获取自旋锁后，重新检查 `r_msg` 字段，以确定在等待自旋锁期间是否已接收到消息。如果消息已接收，则执行最后一步。

8. 如果 `r_msg` 字段保持不变，则表示任务是被唤醒以重试。在这种情况下，将 `msgr` 出队。如果该任务有悬置的信号，则解锁全局消息队列自旋锁并返回 `EINTR`。否则，函数需要返回重试。

9. 如果 `r_msg` 字段显示在睡眠过程中发生了错误，则解锁全局消息队列自旋锁并返回该错误。

10. 在验证用户缓冲区 `msg` 的地址有效后，将消息类型加载到 `msg` 的 `mtype` 字段中，并调用 `store_msg()` 将消息内容复制到 `msg` 的 `mtext` 字段中。最后，由函数 `free_msg()` 释放该消息的内存。

#### 消息特定结构

消息队列的数据结构定义在 `msg.c` 中。

##### `struct msg_queue`

```c
/* one msg_queue structure for each present queue on the system */
struct msg_queue {
       struct kern_ipc_perm q_perm;
};
```

### Linux 内核 2.4 内部机制

##### `struct msg_queue`

```c
time_t q_ostime;		/* last msgsnd time */
time_t q_otime;		/* last msgcvt time */
time_t q_ctime;		/* last change time */
unsigned long q_cbytes;	/* current number of bytes on queue */
unsigned long q_gnum;		/* number of messages in queue */
unsigned long q_qbytes;	/* max number of bytes on queue */
pid_t q_lspid;		/* pid of last msgsnd */
pid_t q_lrpid;		/* last receive pid */

struct list_head q_messages;
struct list_head q_receivers;
struct list_head q_senders;
};
```

##### `struct msg_msg`

```c
/* one msg_msg structure for each message */
struct msg_msg {
	struct list_head m_list;
	long m_type;
	int m_ts;		/* message text size */
	struct msg_msgseg* next;
	/* the actual message follows immediately */
};
```

##### `struct msg_msgseg`

```c
/* message segment for each message */
struct msg_msgseg {
	struct msg_msgseg* next;
	/* the next part of the message follows immediately */
};
```

##### `struct msg_sender`

```c
/* one msg_sender for each sleeping sender */
struct msg_sender {
	struct list_head list;
	struct task_struct* tsk;
};
```

##### `struct msg_receiver`

```c
/* one msg_receiver structure for each sleeping receiver */
struct msg_receiver {
	struct list_head r_list;
	struct task_struct* r_tsk;
	int r_mode;
	long r_msgtype;
	long r_maxsize;
	struct msg_msg* volatile r_msg;
};
```

##### `struct msqid64_ds`

```c
struct msqid64_ds {
__kernel_ipc64_perm msg_perm;
__kernel_time_t msg_stime; /* last msgsnd time */
unsigned long __unused1;
__kernel_time_t msg_rtime; /* last msgrcv time */
unsigned long __unused2;
__kernel_time_t msg_ctime; /* last change time */
unsigned long __unused3;
unsigned long msg_cbytes; /* current number of bytes on queue */
unsigned long msg_qnum; /* number of messages in queue */
unsigned long msg_qbytes; /* max number of bytes on queue */
__kernel_pid_t msg_lspid; /* pid of last msgsnd */
__kernel_pid_t msg_lrpid; /* last receive pid */
unsigned long __unused4;
unsigned long __unused5;
};
```

##### `struct msqid_ds`



```c
struct msqid_ds {
struct ipc_perm msg_perm;
struct msg *msg_first; /* first message on queue,unused */
struct msg *msg_last; /* last message in queue,unused */
__kernel_time_t msg_stime; /* last msgsnd time */
__kernel_time_t msg_rtime; /* last msgrcv time */
__kernel_time_t msg_ctime; /* last change time */
unsigned long msg_lbytes; /* Reuse junk fields for 32 bit */
unsigned long msg_qbytes; /* dito */
unsigned short msg_cbytes; /* current number of bytes on queue */
unsigned short msg_qnum; /* number of messages in queue */
unsigned short msg_qbytes; /* max number of bytes on queue */
__kernel_ipc_pid_t msg_lspid; /* pid of last msgsnd */
__kernel_ipc_pid_t msg_lrpid; /* last receive pid */
};
```

#### 结构 `msg_setbuf`

```c
struct msg_setbuf {
unsigned long qbytes;
uid_t uid;
gid_t gid;
};
```

### 消息支持函数

#### `newque()`

`newque()` 为新消息队列描述符（`struct msg_queue`）分配内存，然后调用 `ipc_addid()`，为新消息队列描述符保留一个消息队列数组条目。消息队列描述符的初始化如下：

- 初始化 `kern_ipc_perm` 结构。
- 消息队列描述符的 `q_cstime` 和 `q_rtime` 字段初始化为 `0`。`q_ctime` 字段设置为 `CURRENT_TIME`。
- 此队列消息允许的最大字节数（`q_cbytes`）设置为 `MSGMNB`，队列当前使用的字节数（`q_cbytes`）初始化为 `0`。
- 消息等待队列（`q_messages`）、接收方等待队列（`q_receivers`）和发送方等待队列（`q_senders`）均初始化为空。

在调用 `ipc_addid()` 之后的所有操作都在持有全局消息队列自旋锁的情况下执行。释放自旋锁后，`newque()` 调用 `msg_buildid()`，该函数直接映射到 `ipc_buildid()`。`ipc_buildid()` 使用消息队列描述符的索引创建一个唯一的消息队列 ID，然后将其返回给 `newque()` 的调用者。

#### `freeque()`

当消息队列即将被删除时，会调用 `freeque()` 函数。该函数假设调用函数已经锁定了全局消息队列自旋锁。它释放与该消息队列相关的所有内核资源。首先，它调用 `ipc_rmid()`（通过 `msg_rmid()`）从全局消息队列描述符数组中移除消息队列描述符。然后它调用 `expunge_all()` 唤醒所有接收者，并调用 `ss_wakeup()` 唤醒在此消息队列上睡眠的所有发送者。随后释放全局消息队列自旋锁。存储在此消息队列中的所有消息被释放，消息队列描述符的内存也被释放。

#### `ss_wakeup()`

`ss_wakeup()` 唤醒给定消息发送者等待队列中等待的所有任务。如果此函数由 `freeque()` 调用，则队列中的所有发送者都会出队。

#### `ss_add()`

`ss_add()` 接收一个消息队列描述符和一个消息发送者数据结构作为参数。它使用当前进程填充消息发送者数据结构中的任务字段，将当前进程的状态更改为 `TASK_INTERRUPTIBLE`，然后将消息发送者数据结构插入给定消息队列的发送者等待队列头部。

#### `ss_del()`

如果给定的消息发送者数据结构（`mss`）仍在相关的发送者等待队列中，则 `ss_del()` 将 `mss` 从队列中移除。

#### `expunge_all()`

`expunge_all()` 接收一个消息队列描述符（`msgq`）和一个整数值（`res`）作为参数，其中 `res` 指示唤醒接收者的原因。对于与 `msgq` 关联的每个睡眠接收者，`r_msg` 字段被设置为指示的唤醒原因（`res`），并唤醒相关的接收任务。当消息队列被移除或执行了消息控制操作时，会调用此函数。

#### `load_msg()`

当进程发送消息时，`sys_msgsnd()` 函数首先调用 `load_msg()` 函数将消息从用户空间加载到内核空间。消息在内核内存中表示为数据块的链表。与第一个数据块关联的是一个 `msg_msg` 结构，该结构描述了整体消息。与 `msg_msg` 结构关联的数据块大小限制为 `DATA_MSG_LEN`。数据块和结构在一个连续的内存块中分配，该内存块最大可以是一个内存页的大小。如果完整消息无法装入第一个数据块，则分配额外的数据块并将其组织成一个链表。这些额外的数据块大小限制为 `DATA_SEG_LEN`，并且每个都包含一个关联的 `msg_msgseg` 结构。`msg_msgseg` 结构和关联的数据块在一个连续的内存块中分配，该内存块最大可以是一个内存页的大小。此函数在成功时返回新 `msg_msg` 结构的地址。

#### `store_msg()`

`store_msg()` 函数由 `sys_msgrcv()` 调用，用于将接收到的消息重新组装到调用者提供的用户空间缓冲区中。`msg_msg` 结构以及任何 `msg_msgseg` 结构描述的数据被顺序复制到用户空间缓冲区。

#### `free_msg()`

`free_msg()` 函数释放消息数据结构 `msg_msg` 和消息段的内存。

#### `convert_mode()`

`convert_mode()` 由 `sys_msgrcv()` 调用。它接收指定消息类型（`msgtyp`）的地址和一个标志（`msgflg`）作为参数。它根据 `msgtyp` 和 `msgflg` 的值向调用者返回搜索模式。如果 `msgtyp` 为 `null`，则返回 `SEARCH_ANY`。如果 `msgtyp` 小于 `0`，则 `msgtyp` 被设置为其绝对值并返回 `SEARCH_LESSEQUAL`。如果 `msgflg` 中指定了 `MSG_EXCEPT`，则返回 `SEARCH_NOTEQUAL`。否则返回 `SEARCH_EQUAL`。

#### `testmsg()`

`testmsg()` 函数检查消息是否满足接收者指定的条件。如果以下任一条件为真，则返回 `1`：

- 搜索模式表示搜索任意消息（`SEARCH_ANY`）。
- 搜索模式为 `SEARCH_LESSEQUAL`，且消息类型小于或等于指定类型。
- 搜索模式为 `SEARCH_EQUAL`，且消息类型与指定类型相同。
- 搜索模式为 `SEARCH_NOTEQUAL`，且消息类型与指定类型不相同。

### `pipelined_send()`

`pipelined_send()` 允许进程直接向等待的接收者发送消息，而不是将消息放入相关的消息等待队列中。调用 `testsig()` 函数以查找第一个正在等待给定消息的接收者。如果找到，该等待的接收者将从接收者等待队列中移除，相关的接收任务将被唤醒。消息将存储在接收者的 `r_msg` 字段中，并返回 `1`。如果没有接收者在等待该消息，则返回 `0`。

在搜索接收者的过程中，可能会发现一些请求大小对于给定消息来说太小的潜在接收者。这些接收者将从队列中移除，并以 `E2BIG` 错误状态被唤醒，该状态存储在 `r_msg` 字段中。搜索将继续，直到找到有效的接收者或队列耗尽为止。

### `copy_msqid_to_user()`

`copy_msqid_to_user()` 将内核缓冲区的内容复制到用户缓冲区。它接收的参数包括用户缓冲区、类型为 `msqid64_ds` 的内核缓冲区，以及指示新 IPC 版本与旧 IPC 版本的版本标志。如果版本标志等于 `IPC_64`，则调用 `copy_to_user()` 直接从内核缓冲区复制到用户缓冲区。否则，初始化一个类型为 `struct msqid_ds` 的临时缓冲区，并将内核数据转换到该临时缓冲区中。随后调用 `copy_to_user()` 将临时缓冲区的内容复制到用户缓冲区。

### `copy_msqid_from_user()`



`copy_msqid_from_user()` 函数接收的参数包括类型为 `struct msq_subbuf` 的内核消息缓冲区、用户缓冲区，以及指示新 IPC 版本与旧 IPC 版本的版本标志。对于新 IPC 版本的情况，调用 `copy_from_user()` 将用户缓冲区的内容复制到类型为 `msqid64_ds` 的临时缓冲区中。然后，内核缓冲区的 `bytes`、`uid`、`gid` 和 `mode` 字段将被填充为临时缓冲区中对应字段的值。对于旧 IPC 版本的情况，则使用类型为 `struct msqid_ds` 的临时缓冲区。

### 5.3 共享内存

#### 共享内存系统调用接口

##### `sys_shmget()`

整个对 `sys_shmget()` 的调用都受到全局共享内存信号量的保护。

如果需要创建一个新的共享内存段，则调用 `newseg()` 函数来创建并初始化一个新的共享内存段。新段的 ID 将返回给调用者。

如果提供了现有共享内存段的键值，则查找共享内存描述符数组中相应的索引，并在返回共享内存段 ID 之前验证调用者的参数和权限。查找操作和验证是在持有全局共享内存自旋锁期间执行的。

##### `sys_shmctl()`

###### `IPC_INFO`

一个临时的 `shminfo64` 缓冲区加载了系统范围的共享内存参数，并被复制到用户空间以供调用应用程序访问。

###### `SHM_INFO`

在收集共享内存的系统范围统计信息时，持有全局共享内存信号量和全局共享内存自旋锁。调用 `shm_get_stat()` 函数来计算驻留在内存中的共享内存页数和被换出的共享内存页数。其他统计信息包括共享内存总页数和正在使用的共享内存段数量。`swap_attempts` 和 `swap_successes` 的计数被硬编码为零。这些统计信息存储在临时的 `shm_info` 缓冲区中，并复制到用户空间供调用应用程序使用。

###### `SHM_STAT`, `IPC_STAT`

对于 `SHM_STAT` 和 `IPC_STAT`，初始化一个类型为 `struct shmid64_ds` 的临时缓冲区，并锁定全局共享内存自旋锁。

对于 `SHM_STAT` 情况，共享内存段 ID 参数预期是一个直接索引（即 0 到 `n`，其中 `n` 是系统中共享内存 ID 的数量）。在验证索引后，调用 `ipc_buildid()`（通过 `shm_buildid()`）将索引转换为共享内存 ID。在 `SHM_STAT` 成功的情况下，共享内存 ID 将是返回值。请注意，这是一个未记录的特性，但为了 `ipcstat(8)` 程序而保留。

对于 `IPC_STAT` 情况，共享内存段 ID 参数预期是由调用 `shmget()` 生成的 ID。在继续之前会验证该 ID。在 `IPC_STAT` 成功的情况下，0 将是返回值。

对于 `SHM_STAT` 和 `IPC_STAT` 两种情况，都会验证调用者的访问权限。所需的统计信息会被加载到临时缓冲区中，然后复制到调用应用程序。

###### `SHM_LOCK`, `SHM_UNLOCK`

在验证访问权限后，锁定全局共享内存自旋锁，并验证共享内存段 ID。对于 `SHM_LOCK` 和 `SHM_UNLOCK`，都调用 `shm_lock()` 来执行功能。`shm_lock()` 的参数确定要执行的功能。

###### `IPC_RMID`

在 `IPC_RMID` 期间，整个函数持有全局共享内存信号量和全局共享内存自旋锁。验证共享内存 ID，然后如果没有当前附加项，则调用 `shm_destroy()` 销毁共享内存段。否则，设置 `SHM_DEST` 标志以标记其待销毁，并设置 `IPC_PRIVATE` 标志以防止其他进程引用该共享内存 ID。

###### `IPC_SET`

在验证共享内存段 ID 和用户访问权限后，使用用户数据更新共享内存段的 `uid`、`gid` 和 `mode` 标志。同时更新 `shm_ctime` 字段。这些更改是在持有全局共享内存信号量和全局共享内存自旋锁期间进行的。

##### `sys_shmat()`

`sys_shmat()` 接收以下参数：共享内存段 ID、应附加共享内存段的地址（`shmaddr`），以及将在下文描述的标志。

如果 `shmaddr` 非零，且指定了 `SHM_RND` 标志，则 `shmaddr` 会向下舍入为 `SHMLBA` 的倍数。如果 `shmaddr` 不是 `SHMLBA` 的倍数且未指定 `SHM_RND`，则返回 `EINVAL`。

验证调用者的访问权限，并增加共享内存段的 `shm_nattch` 字段。请注意，此增加保证了附加计数非零，并防止在附加到段的过程中销毁该共享内存段。这些操作是在持有全局共享内存自旋锁期间执行的。

调用 `do_mmap()` 函数创建指向共享内存段页面的虚拟内存映射。这是在持有当前任务的 `mmap_sem` 信号量期间完成的。向 `do_mmap()` 传递 `MAP_SHARED` 标志。如果调用者提供了地址，则也向 `do_mmap()` 传递 `MAP_FIXED` 标志。否则，`do_mmap()` 将选择映射共享内存段的虚拟地址。

注意：在 `do_mmap()` 函数调用中，会通过 `shm_file_operations` 结构体调用 `shm_inc()`。调用此函数用于设置 PID、设置当前时间，并增加该共享内存段的附加次数。

在调用 `do_mmap()` 之后，同时获取全局共享内存信号量和全局共享内存自旋锁。然后减少附加计数。由于调用了 `shm_inc()`，`shmat()` 调用对附加计数的净变化为 1。如果减少附加计数后，发现结果计数为零，且该段被标记为待销毁（`SHM_DEST`），则调用 `shm_destroy()` 释放共享内存段资源。

最后，共享内存映射的虚拟地址返回给调用者在用户指定的地址处。如果 `do_mmap()` 返回了错误代码，则该失败代码作为系统调用的返回值传递。

##### `sys_shmdt()`

在执行 `sys_shmdt()` 时，会持有全局共享内存信号量。当前进程的 `mm_struct` 会被搜索，以找到与共享内存地址相关的 `vm_area_struct`。一旦找到，就会调用 `do_munmap()` 来撤销共享内存段的虚拟地址映射。

请注意，`do_munmap()` 会回调 `shm_close()`，该函数执行共享内存的簿记功能，如果不存在其他附加（attachments），则释放共享内存段资源。

`sys_shmdt()` 无条件返回 0。

#### 共享内存支持结构

##### `struct shminfo64`

```c
struct shminfo64 {
    unsigned long shmmax;
    unsigned long shmin;
    unsigned long shmmni;
    unsigned long shmseg;
    unsigned long shmall;
    unsigned long __unused1;
    unsigned long __unused2;
    unsigned long __unused3;
    unsigned long __unused4;
};
```

##### `struct shm_info`

```c
struct shm_info {
    int used_ids;
    unsigned long shm_tot;  /* total allocated shm */
    unsigned long shm_rss;  /* total resident shm */
    unsigned long shm_swp;  /* total swapped shm */
    unsigned long swap_attempts;
    unsigned long swap_successes;
};
```

##### `struct shmid_kernel`

```c
struct shmid_kernel /* private to the kernel */
{
    struct kern_ipc_perm  shm_perm;
    struct file *         shm_file;
    int                   id;
    unsigned long         shm_nattch;
    unsigned long         shm_segsz;
    time_t                shm_atim;
    time_t                shm_dtim;
    time_t shm_ctim;
    pid_t shm_cpid;
    pid_t shm_lpid;
};
```

##### `struct shmid64_ds`



```c
struct shmid64_ds {
struct ipc64_perm shm_perm; /* operation perms */
size_t shm_segsz; /* size of segment (bytes) */
__kernel_time_t shm_atime; /* last attach time */
__unsigned long __unused1;
__kernel_time_t shm_dtime; /* last detach time */
unsigned long __unused2;
__kernel_time_t shm_ctime; /* last change time */
__unsigned long __unused3;
__kernel_pid_t shm_cpid; /* pid of creator */
__kernel_pid_t shm_lpid; /* pid of last operator */
unsigned long shm_nattch; /* no. of current attaches */
unsigned long __unused4;
unsigned long __unused5;
};
```

##### `struct shmem_inode_info`

```c
struct shmem_inode_info {
spinlock_t lock;
unsigned long max_index;
swp_entry_t i_direct[SHMEM_NR_DIRECT]; /* for the first blocks */
swp_entry_t **i_indirect; /* doubly indirect blocks */
unsigned long swapped;
int locked; /* into memory */
struct list_head list;
};
```

#### 共享内存支持函数

##### `newseg()`

当需要创建新的共享内存段时，会调用`newseg()`函数。它针对新段作用于三个参数：密钥（`key`）、标志（`flag`）和大小（`size`）。在验证要创建的共享内存段大小介于`SHMMIN`和`SHMMAX`之间，且共享内存段总数未超过`SHMALL`之后，它会分配一个新的共享内存段描述符。稍后会调用`shmem_file_setup()`函数来创建一个未链接的`tmpfs`类型文件。返回的文件指针保存在关联的共享内存段描述符的`shm_file`字段中。文件大小被设置为与段大小相同。新的共享内存段描述符被初始化并插入到全局`IPC`共享内存描述符数组中。共享内存段`ID`由`shm_buildid()`（通过`ipc_buildid()`）创建。该段`ID`保存在共享内存段描述符的`id`字段以及关联`inode`的`i_ino`字段中。此外，结构体`shm_file_operation`中定义的共享内存操作地址存储在关联文件中。全局变量`shm_tot`（指示系统范围内共享内存段总数）的值也会增加，以反映此变更。成功时，段`ID`返回给调用应用程序。

##### `shm_get_stat()`

`shm_get_stat()`遍历所有共享内存结构，并计算共享内存正在使用的内存页总数以及被换出（`swapped out`）的共享内存页总数。每个共享内存段都有一个文件结构体和一个`inode`结构体。由于所需数据是通过`inode`获取的，因此按顺序锁定并解锁每个被访问的`inode`结构体的自旋锁。

##### `shmem_lock()`

`shmem_lock()`接收指向共享内存段描述符的指针以及一个指示锁定或解锁的标志作为参数。共享内存段的锁定状态存储在关联的`inode`中。将该状态与期望的锁定状态进行比较；如果它们匹配，`shmem_lock()`直接返回。

在持有关联`inode`信号量的同时，设置`inode`的锁定状态。对于共享内存段中的每个页，发生以下一系列操作：

- 调用`find_lock_page()`来锁定该页（设置`PG_locked`）并递增该页的引用计数。递增引用计数确保在此操作期间，共享内存段保持在内存中处于锁定状态。
- 如果期望状态为锁定（`locked`），则清除`PG_locked`，但引用计数保持递增状态。
- 如果期望状态为解锁（`unlocked`），则引用计数减少两次：一次针对当前引用，一次针对导致该页保持在内存中锁定的现有引用。然后清除`PG_locked`。

##### `shm_destroy()`

在`shm_destroy()`期间，共享内存页的总数会被调整，以反映共享内存段的移除。调用`ipc_rmid()`（通过`shm_rmid()`）来移除共享内存`ID`；调用`shmem_lock`来解锁共享内存页，有效地将每个页的引用计数减至零。调用`fput()`来递减关联文件对象的使用计数器`f_count`，并在必要时释放文件对象资源。调用`kfree()`来释放共享内存段描述符。

##### `shm_inc()`

`shm_inc()`设置`PID`，设置当前时间，并递增给定共享内存段的附加数量。这些操作是在持有全局共享内存自旋锁的同时执行的。

##### `shm_close()`

`shm_close()`更新`shm_lprid`和`shm_dtim`字段，并递减附加的共享内存段数量。如果该共享内存段没有其他附加，则调用`shm_destroy()`来释放共享内存段资源。这些操作都是在同时持有全局共享内存信号量和全局共享内存自旋锁的情况下执行的。

##### `shmem_file_setup()`

函数`shmem_file_setup()`在`tmpfs`文件系统中建立一个具有给定名称和大小且未链接的文件。如果系统内存资源足够用于该文件，它会在`tmpfs`的挂载根目录下创建一个新的`dentry`，并分配一个新的文件描述符和一个新的`tmpfs`类型的`inode`对象。然后，通过调用`d_instantiate()`将新的`dentry`对象与新的`inode`对象关联起来，并将`dentry`对象的地址保存在文件描述符中。`inode`对象的`i_size`字段被设置为文件大小，`i_nlink`字段被设置为`0`，以标记该`inode`为未链接状态。此外，`shmem_file_setup()`将`shmem_file_operations`结构体的地址存储在`f_op`字段中，并正确初始化文件描述符的`f_mode`和`f_vfsmnt`字段。调用函数`shmem_truncate()`来完成节点对象的初始化。成功时，`shmem_file_setup()`返回新的文件描述符。

### 5.4 Linux IPC 原语

#### 用于信号量、消息和共享内存的通用 Linux IPC 原语

Linux 的信号量、消息和共享内存机制建立在一组通用原语之上。这些原语在以下章节中描述。

##### `ipc_alloc()`

如果内存分配大于`PAGE_SIZE`，则使用`vmalloc()`分配内存。否则，调用`kmalloc()`并传入`GFP_KERNEL`来分配内存。

##### `ipc_addid()`

当添加新的信号量集、消息队列或共享内存段时，`ipc_addid()`首先调用`grow_ary()`以确保对应描述符数组的大小足够大，以满足系统最大值。描述符数组会被搜索以找到第一个未使用的元素。如果找到未使用的元素，则正在使用的描述符计数加一。然后初始化新资源描述符的`kern_ipc_perm`结构体，并返回新描述符的数组索引。当`ipc_addid()`成功时，它会在锁定给定`IPC`类型的全局自旋锁的情况下返回。

##### `ipc_rmid()`

`ipc_rmid()`从给定`IPC`类型的全局描述符数组中移除`IPC`描述符，更新正在使用的`ID`计数，并在必要时调整对应描述符数组中的最大`ID`。返回指向与给定`IPC ID`关联的`IPC`描述符的指针。

##### `ipc_buildid()`

`ipc_buildid()`创建唯一`ID`，以便与给定`IPC`类型内的每个描述符关联。此`ID`在添加新`IPC`元素时（例如新的共享内存段或新的信号量集）创建。`IPC ID`很容易转换为对应的描述符数组索引。每个`IPC`类型维护一个序列号，每次添加描述符时该序列号递增。`ID`通过将序列数乘以`SEQ_MULTIPLIER`，然后将乘积加到描述符数组索引上创建。创建特定`IPC ID`时使用的序列号随后存储在对应的描述符中。该

##### 8.4.1 IPC ID 序列号

序列号的存在使得检测过期`IPC ID`的使用成为可能。

##### 8.4.2 IPC 校验 ID

`ipc_checkid()`将给定的`IPC ID`除以`SEQ_MULTIPLIER`，并将商与该描述符对应的已保存`seq`值进行比较。如果相等，则视为该`IPC ID`有效并返回`1`。否则，返回`0`。

##### 8.4.3 扩展数组



`grow_ary()` 处理给定 IPC 类型的最大 ID 数量（可调整）动态变化的可能性。它强制执行当前最大限制，确保其不超过永久性系统限制（`IPCMNI`），并在必要时将其下调。它还确保现有的描述符数组足够大。如果现有数组大小足够大，则返回当前最大限制。否则，分配一个新的更大数组，将旧数组复制到新数组中，并释放旧数组。在更新给定 IPC 类型的描述符数组时，会持有相应的全局自旋锁。

##### 8.4.4 查找键

`ipc_findkey()` 遍历指定的 `ipc_ids` 对象的描述符数组，并搜索指定的键。一旦找到，则返回相应描述符的索引。如果未找到键，则返回 -1。

##### 8.4.5 检查权限

`ipcperms()` 检查对 IPC 资源访问的用户、组和其他权限。如果权限被授予则返回 0，否则返回 -1。

##### 8.4.6 加锁

`ipc_lock()` 以 IPC ID 作为其参数之一。它锁定给定 IPC 类型的全局自旋锁，并返回指向指定 IPC ID 对应描述符的指针。

##### 8.4.7 解锁

`ipc_unlock()` 释放指定 IPC 类型的全局自旋锁。

##### 8.4.8 全部加锁

`ipc_lockall()` 锁定给定 IPC 机制（即共享内存、信号量和消息传递）的全局自旋锁。

##### 8.4.9 全部解锁

`ipc_unlockall()` 解锁给定 IPC 机制（即共享内存、信号量和消息传递）的全局自旋锁。

#### 8.5 通用 IPC 获取/解析函数

##### 8.5.1 ipc_get()

`ipc_get()` 接受指向特定 IPC 类型（即共享内存、信号量或消息队列）的指针和一个描述符 ID，并返回指向相应 IPC 描述符的指针。注意，虽然每种 IPC 类型的描述符数据类型不同，但通用的 `kern_ipc_perm` 结构类型在每种情况下都作为第一个实体嵌入其中。`ipc_get()` 函数返回此通用数据类型。预期的模型是 `ipc_get()` 通过包装函数（例如 `shm_get()`）调用，该函数将数据类型强制转换为正确的描述符数据类型。

##### 8.5.2 ipc_parse_version()

`ipc_parse_version()` 如果存在 `IPC_64` 标志则将其从命令中移除，并返回 `IPC_64` 或 `IPC_OLD`。

#### 8.6 用于信号量、消息和共享内存的通用 IPC 结构

信号量、消息和共享内存机制都使用以下通用结构：

##### 8.6.1 struct kern_ipc_perm

每个 IPC 描述符的第一个元素都是此类型的数据对象。这使得可以使用此数据类型的指针从任何通用 IPC 函数访问任何描述符。

```c
/* used by in-kernel data structures */
struct kern_ipc_perm {
    key_t key;
    uid_t uid;
    gid_t gid;
    uid_t cuid;
    gid_t cgid;
    mode_t mode;
    unsigned long seq;
};
```

##### 8.6.2 struct ipc_ids

`ipc_ids` 结构描述了信号量、消息队列和共享内存的通用数据。该数据结构有三个全局实例——`semids_ds`、`msgids_ds` 和 `shmid_ds`——分别用于信号量、消息和共享内存。在每个实例中，`sem` 信号量用于保护对该结构的访问。`entries` 字段指向 IPC 描述符数组，而 `ary` 自旋锁保护对该数组的访问。`seq` 字段是一个全局序列号，当创建新的 IPC 资源时会递增。

```c
struct ipc_ids {
    int size;
    int in_use;
    int max_id;
    unsigned short seq;
    unsigned short seq_max;
    struct semaphore sem;
    spinlock_t ary;
    struct ipc_id* entries;
};
```

##### 8.6.3 struct ipc_id

每个 `ipc_ids` 结构实例中都有一个 `struct ipc_id` 数组。该数组是动态分配的，并且根据需要可通过 `grow_ary()` 替换为更大的数组。该数组有时被称为描述符数组，因为 `kern_ipc_perm` 数据类型被 IPC 通用函数用作通用描述符数据类型。

```c
struct ipc_id {
    struct kern_ipc_perm* p;
};
```
