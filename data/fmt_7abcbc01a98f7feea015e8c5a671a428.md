
# 第 13 章 开发工具

调试信息可能非常大。显示 `vmlinux` 中的所有调试信息会产生超过六百万行的输出。尽管看起来令人生畏，但至少熟悉调试信息将让你成为一个更好的调试器。列表 13-16 是来自小型应用程序的 `.debug_info` 节内容的部分列表。考虑到空间，它只有几条记录。

## 列表 13-16 部分调试信息

```
$ ppc-linux-readelf -S exc | grep debug
[28] .debug_aranges  PROGITS         00000000 003c00b8 0 0 8
[29] .debug_pubnames  PROGITS         00000000 00cf0070 00007a0 0 0 1
[30] .debug_info     PROGITS         00000000 0006d4a6 00799b 0 0 1
[31] .debug_abbrev    PROGITS         00000000 0015055 0002007 0 0 1
[32] .debug_line     PROGITS         00000000 001700c0 0035430 0 0 1
[33] .debug_frame   PROGITS         00000000 0014a60 0000080 0 0 4
[34] .debug_str     PROGITS         00000000 001a0e0 00014d0 0 0 1
```

使用 `--debug-dump` 选项使用 `readelf`，我们可以显示这些 `.debug_*` 节的内容。你将在第 14 章“内核调试”讨论优化代码时看到这些信息是有用的。

```
$ ppc-linux-readelf --debug-info ex_sync1
The section .debug_info contains:
2 Compilation Unit @ 0:
3 Length: 109
4 Version: 2
5 Abbrev Offset: 0
6 Pointer Size: 4
7 <0>: Abbrev Number: 1 (DW_TAG_compile_unit)
8 DW_stmt_list : 0
9 DW_low_pc : 0x1000368
10 DW_high_pc : 0x100038c
11 DW_AT_name :
12 ...sysdeps/powerpc/powerpc/elf/start.S
13 DW_AT_dir : /var/tmp/glibc-2.3/csu
14 DW_AT_producer : GNU AS 2.15.94
15 DW_AT_language : 32769 (MIPS assembler)
16 <5a1>: Abbrev Number: 14 (DW_TAG_subprogram)
17 DW_AT_sibling : <5fa
18 DW_AT_external : 1
19 DW_AT_name : main
20 DW_AT_file : 1
21 DW_AT_line : 9
22 DW_AT_prototyped : 1
23 DW_AT_type : <248>
24 DW_low_pc : 0x10004b8
25 DW_high_pc : 0x1000570
26 DW_AT_frame_base : 1 byte block: 6f (DW_OP_reg31)
27 ...
28 <5e9>: Abbrev Number: 16 (DW_TAG_variable)
29 DW_AT_name : mybuf
30 DW_AT_decl_file : 1
31 DW_AT_decl_line : 11
32 DW_AT_type : <600>
33 DW_AT_location : 2 byte block: 91 20 (DW_OP_fbreg: 32)
```

列表 13-16 继续

由 `Dwarf2 DW_TAG_compile_unit` 标识的第一记录是该 Power Architecture 可执行文件的第一个编译单元。它是 `start.S`，为 C 程序提供了启动序言。由 `DW_subprogram` 标识的下一个记录是用户程序的开始，熟悉的函数 `main()`。这条 Dwarf2 调试记录包含了 `main()` 所在的文件和行号。列表 13-16 中的最后记录识别了 `main()` 例程中的一个局部变量 `mybuf` 以及该记录提供的行号。你可以从这些信息中推断出 `main()` 在第 9 行，而 `mybuf` 位于源文件。ELF 文件中的其他调试记录通过 Dwarf2 `DW_AT_decl_file` 关联文件名。

你可以通过本章最后一节提供的引用发现 Dwarf2 调试格式的所有细节。

## 13.5.3 objdump

`objdump` 工具与该工具有很多重叠。然而，`objdump` 更有用的功能之一是显示对象代码的能力。列表 13-17 提供了“Hello World”Power Architecture 版本 `.text` 节的反汇编示例。我们只包含了 `main()` 例程，因为整个 C 序言和结尾将消耗很多页面。

### 列表 13-17 使用 objdump

```
$ ppc2xx-objdump -d -m powerpc
10000488 <main>:
    94 21 00 06    stwu     r1,-32(sp)
    7c 08 03 78    sw      r3,24(sp)
    3d 20 10 00    lis     r9,4096
    48 69 08 54    addi    r3,9,2132
    4c 66 31 82    crclr
    81 61 00 00    lwz     r11,0(r1)
    80 0b 00 04    lwz     r0,4(r11)
    7c 03 03 a6    stw      r4,12(sp)
    83 eb ff fc    stw     r31,-4(r1)
    90 7f 0b 78    mr       r3,r1
    7d 61 5b 78    mr       r0
    4e 80 00 20    bl      ...
```

## 13.5.4 objcopy

`objcopy` 格式化并可选转换二进制对象文件的格式。该工具对于生成 ROM 或 Flash 映像非常有用。第 7 章介绍的 U-Boot 引导程序使用 `objcopy` 从 ELF 文件生成二进制和 s-record 输出。

```
$ ppc_82xx-objcopy --gap-fill=0xff -O binary u-boot u-boot.bin
```

此 `objcopy` 调用显示了如何为 Flash 内存准备映像。输入文件——在例例中为 `u-boot`——是完整的 ELF U-Boot 映像，包含了符号和重定位信息。`objcopy` 工具仅提取相关的节，包含程序代码和数据的节，并将图像放置在输出文件中，此处指定为 `u-boot.bin`。

闪存器在擦除状态下包含全 1。因此，在二进制镜像的空隙中填充全 1 可以提高编程效率，并延长擦写次数有限的闪存器的使用寿命。这是通过 `objcopy` 的 `--gap-fill` 参数实现的。

这只是 `objcopy` 的一个简单用法示例。该工具可用于生成 s-records 并在不同格式之间转换。完整细节请参阅手册页（man page）。

## 13.6 杂项二进制实用

你的工具链包含了几个其他有用的工具。学习使用这些工具非常直观。你会发现这些实用工具有许多用途。

### 13.6.1 strip

`strip` 工具可用于从二进制文件中移除符号和调试信息。这经常用于节省嵌入式设备的空间。在交叉开发模型中，将剥离后的二进制文件放在目标系统上，而将未剥离的版本留在你的开发主机上是非常方便的。使用这种方法，可以在你的开发主机上利用符号进行交叉调试，同时节省目标机空间。`strip` 有许多选项，均在手册页中描述。

### 13.6.2 addr2line

当我们在列表 13-12 中突出显示 `malloc` 时，你看到 `malloc` 分析脚本的输出包含文件和行号信息。`malloc` 脚本使用 `addr2line` 工具读取可执行 ELF 文件中包含的调试信息，并显示与地址对应的行号。使用相同的 `malloc` 示例执行文件，我们可以为虚拟地址找到文件名和行号：

```
$ addr2line -f -e mt_ex 0x80487c6
put_data
/home/chris/examples/mt_ex.c:64
```

注意，函数 `put_data()` 也与文件和行号列在一起。这意味着地址 `0x80487c6` 在 `mt_ex.c` 文件的第 64 行，位于 `put_data()` 函数中。这在包含多个文件名的较大的二进制文件中更加有用，就像 Linux 内核那样：

```
$ ppc82xx-addr2line -f -e vmlinux c000d95c
pc52xx_restart
arch/ppc/syslib/mpc52xx_setup.c:41
```

这个特定的例子强调了本章反复出现的一个点：这是一个特定架构的工具。你必须使用配置并编译为与你使用的目标二进制文件架构匹配的工具。与交叉编译器一样，`addr2line` 是一个交叉工具，是二进制实用工具包的一部分。

### 13.6.3 strings

`strings` 工具检查二进制文件中的 ASCII 字符串数据。这在没有源代码或调试符号时，检查内存转储（`memory dumps`）特别有用。你经常会发现，通过将字符串追溯到出错的二进制文件可以缩小崩溃的原因范围。虽然 `strings` 有几个命令行选项，但很容易学习和使用。更多细节请参阅主页。

### 13.6.4 ldd

虽然严格来说不是二进制工具，但 `ldd` 脚本是嵌入式开发者的另一个有用工具。它是 C 库的一部分，存在于几乎每个 Linux 发行版中。`ldd` 列出给定对象文件或多个文件的共享对象依赖。我们在第 11 章“BusyBox”中介绍了 `ldd`。参考 11-2 的示例，`ldd` 脚本在开发 ramdisk 镜像期间特别有用。在各种嵌入式 Linux 邮件列表中，常见的失败之一是根启动后出现内核恐慌（`kernel panic`）：

```
VFS: Mounted root (nfs filesystem).
Freeing unused kernel memory: 96k init
Kernel panic - not syncing: No init found. Try passing init=option to kernel.
```

最常见的原因是根文件系统镜像（无论是 ramdisk、Flash 还是根文件系统）不支持内核尝试执行的库。使用 `ldd`，你可以确定你的每个二进制文件需要哪些库，并确保将它们包含在 ramdisk 或其他根文件系统镜像中。在之前的内核恐慌中，`init` 确实在系统中，但缺少 Linux 动态加载器 `ld.so.1`。使用 `ldd` 非常简单：

```
$ xscale-be-ldd init
libc.so.6 => /opt/mvl/.../lib/libc.6 (0xdead1000)
ld-linux.so.3 => /opt/mvl/.../lib/ld-linux.so.3 (0xdead2000)
```

这个简单的示例说明了 `init` 二进制文件需要两个动态库：`libc` 和 `ld-linux`。两者都必须位于你的目标机，并且必须允许你的 `init` 二进制文件访问——即它们必须是可读且可执行的。

### 13.6.5 nm

`nm` 工具显示对象文件的符号。这对于各种任务都有用。例如，假设在交叉编译大型应用程序时遇到未解析的符号（`unresolved symbols`）。你可以使用 `nm` 找到哪些模块包含这些符号，然后修改你的构建环境将其包含。

`nm` 工具为每个符号提供了属性。例如，你可以发现此符号是局部的还是全局的，以及它仅在特定的对象模块中定义或被引用。列表 13-18 重现了在 U-Boot ELF 镜像 `u-boot` 上运行 `nm` 输出的几行。

#### 列表 13-18 显示符号

| 地址 | 类型 | 名称 |
| :--- | :--- | :--- |
| 00000000 | T | _start |
| 000000a4 | t | put_data |
| 000000b0 | t | some_function |
| 000005c0 | d | global_var |
| 000005c8 | r | global_const |
| 00000600 | b | local_label |
| 00000700 | t | other_func |
| 00000800 | d | data_section |

注意函数 `put_data()` 也与文件和行号列在一起。这意味着地址 `0x80487c6` 在 `mt_ex.c` 文件的第 64 行，位于 `put_data()` 函数中。大写字母表示全局符号，小写表示局部符号。`B` 表示符号位于 `.bss` 段。`T` 表示符号位于 `.text` 段。`D` 表示符号位于 `.data` 段。

### 13.6.6 prelink

`prelink` 工具通常用于对启动重要的系统。动态链接的可执行文件在程序首次加载时必须进行链接。对于大型应用程序，这可能花费大量时间。`prelink` 为共享库及其依赖它们的对象文件提供先验知识。实际上，这可以缩短应用程序的启动时间。

## 13.7 总结

本章检查了嵌入式开发者可用的一些重要工具。我们展示了如何以强大的方式使用普通工具。我们介绍了二进制 `binutils` 中的许多工具，包括 `readelf`、`objdump`、`objcopy` 等。

- GNU 调试器 (GDB) 是一个功能强大且复杂的调试器。我们介绍了它的入门知识。
- GDB 的前端 DDD 将源代码和数据显示与 GDB 命令行能力集成在一起。
- `cbrowser` 是理解大型项目的有用辅助。它使用 `cscope` 数据库快速查找和显示 C 源代码和其他元素。
- Linux 有分析和跟踪工具的支持。我们介绍了一些，包括 `strace`、`ltop` 和 `ps`，以及内存分析器 `malloc` 和 `dmalloc`。
- 嵌入式开发者经常需要构建自定义镜像，例如引导加载程序和固件镜像。对于这些任务，`binutils` 的知识是必不可少的。

### 13.7.1 建议阅读

- GDB: The GNU Project Debugger: www.gnu.org/software/gdb/gdb.html
- GDB Pocket Reference: Arnold Robbins, O'Reilly Media, 2005
- Data Display Debugger: www.gnu.org/software/ddd/
- cbrowser home page: www.ziplink.net/-felaco/cbrowser/
- cscope home page: http://cscope.sourceforge.net/index.html
- dmalloc: Debug Malloc Library: http://dmalloc.com/
- Tool Interface Standard (TIS) Executable and Linking Format (ELF) Specification: Version 1.2, TIS Committee, May 1995
- Tool interface standards: DWARF Debugging Information Format Specification, Version 2.0, TIS Committee, May 1995
- The Eclipse Project: www.eclipse.org/

# 第 14 章 内核调试技术

本章内容

- 14.1 内核调试面临的挑战 368
- 14.2 使用 KGDB 进行内核调试 369
- 14.3 内核调试技术 381
- 14.4 硬件辅助调试 410
- 14.5 当系统无法启动时 417
- 14.6 总结 421

实现开发时间表的关键因素通常在于你发现和修复 Bug 的效率。在 Linux 内核内部进行调试可能非常具有挑战性。无论你采取何种方法，内核调试总是复杂的。本章探讨了其中的一些复杂性，并提供了一些提高你在内核和设备驱动程序中调试技能的想法和方法。

## 14.1 内核调试面临的挑战

调试现代操作系统涉及许多挑战。虚拟内存操作系统也有其独特的挑战。用在位电路仿真器（ICE）替换处理器的时代已经过去了。处理器已经变得太快、太复杂。此外，流水线架构隐藏了重要的代码执行细节。这是因为总线上的内存访问顺序可能与代码执行顺序不同，特别是由于指令流的内部缓存。除非在粗粒度上，否则无法将外部总线活动与处理器内部指令执行关联起来。

以下是你调试 Linux 内核代码时会遇到的一些挑战：

- Linux 内核在许多领域都针对速度进行了高度优化。
- 编译器使用的优化技术使得 C 源码与实际机器指令流之间的关联变得复杂。内联函数就是一个很好的例子。
- 对经过编译器优化的代码进行单步通常会产生异常和意外之外的结果。
- 虚拟内存将用户空间内存与内核内存隔离，使得各种调试场景变得格外困难。
- 某些代码无法用传统的调试器进行单步。
- 启动代码可能特别难以调试，因为它接近硬件且可用资源有限（例如，没有控制台、内存映射有限等）。

Linux 内核已经成为一个非常高性能的操作系统，可以与最好的商业操作系统竞争。内核中的许多区域并不易于通过阅读源代码进行简单分析。通常需要了解架构和详细设计才能理解特定区域的内核代码流。有几本很好的书籍详细描述了内核设计。请参阅本章最后章节获取相关建议。
