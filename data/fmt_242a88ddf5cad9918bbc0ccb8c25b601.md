
396 DW_AT_external: 1

397 DW_AT_name: main

398 DW_AT_decl_file: 1

399 DW_AT_decl_line: 9

400 DW_AT_prototype: 1

401 DW_AT_type: <248>

402 DW_AT_low_pc: 0x01004b8

403 DW_AT_high_pc: 0x0100570

404 DW_AT_frame_base: 1 byte block: 6f (DW_OP_reg31)

423 <259>: Abbrev Number: 16 (DW_TAG_variable)

424 DW_AT_name: mybuf

425 DW_AT_decl_file: 1

426 DW_AT_decl_line: 11

427 DW_AT_type: <600>

428 DW_AT_location: 2 byte block: 91 20 (DW_OP_fpreg:32)

由 `DWARF DW_TAG_compile_unit` 标识的第一条记录是 PowerPC 可执行文件的第一个编译单元。这是一个名为 `start` 文件，为 C 程序提供了启动序言。下一个由 `DW_TAG_subprogram` 标识的记录是用户程序的起点，函数 `main()`。此 DWARF 调试记录包含了指向 `main()` 所在的文件和行号的引用。列表 13-16 中的最后一条记录识别了 `main()` 例中一个名为 `mybuf` 的变量。同样，行和文件是由你的记录提供的。你可以从信息中推断 `main()` 在第 9 行，而 `mybuf` 在源文件的第 11 行。ELF 文件中的其他调试记录通过 `DWARF DW_AT_decl_file` 属性将文件名关联起来。

> [8] DWARF 调试信息规范的参考位于本书末尾。

你可以通过本章末尾第 13.7.1 节提供的参考，发现 DWARF 调试信息格式的所有细节。

### 13.5.3. objdump

`objdump` 工具与 `readelf` 工具有相当重叠。然而，`objdump` 更实的功能之一是它可以显示反汇编后的对象代码。列表 13-17 提供了一个简单的“hello world”PowerPC 版本 `.text` 节的反汇编示例。为了节省空间，我们只包含了 `main()` 例。整个转储（包括 C 库的序言和结尾）将占用许多页面。

# 列表 13-17. 反汇编 objdump

```
$ ppc_82xx-objdump -S - powerpc:common -j .text hello

...

10000488 <main>:

10000488:      94 21 ff e0   stwu      r1,-32(r1)

1000048c:      7c 02 08 6a   mflr      r0

10000490:      93 01 00 lc   stw      r31,28(r1)

10000494:      90 01 00 24   stw      r0,36(r1)

10000498:      7c 2f 08 78   mr        r31,r1

1000049c:      90 7f 00 88   stw      r3,8(r1)

100004a0:      90 9f 00 7c   stw      r4,12(r31)

100004a4:      32 30 10 00   lis      r9,4096

100004a8:      36 68 09 54   addi     r3,r9,2132

100004ac:      4c 3c 81 32   crclr    r4*1+eq

100004b0:      48 01 05 11   bl       100109c0

__bss_start+0x60:

100004b4:      38 00 00 00   li        r0,0

100004b8:      7c 03 03 78   mr        r3,0

100004bc:      81 61 00 00   lwz      r11,0(r1)

100004c0:      80 0b 00 04   lwz      r0,4(r1)

100004c4:      7c 08 03 6a   mtrl      r0

100004c8:      83 eb ff 6c   lwz      r31,-4(r1)

100004cc:      7d 61 5b 78   mr        r1,r1

100004d0:      4e 80 00 00   bl       
```

来自 `main()` 例程的代码片段是栈帧的创建和销毁。对 `printf()` 的实际调用由列表中心地址 `0x100004b0` 附近的分支 (`bl`) 指令表示。这是一个 PowerPC 函数。由于该程序被编译为动态链接对象，在运行时之前，我们将无法获得 `printf()` 函数的地址。它将与共享库 `printf()` 例程进行链接。如果我们将其编译为静态链接对象，我们就可以使用符号和相应的地址来调用 `printf()`。

## 13.5.4. objcopy

`objcopy` 用于格式化并可选转换二进制对象文件的格式。这对于生成 ROM 或 Flash 镜像的代码非常有用。第 7 章引入的 U-Boot 加载程序利用 `objcopy` 从最终的 ELF 文件生成二进制和 s-record 输出格式。本示例说明了 `objcopy` 的功能以及如何构建它。

> S-record 文件是二进制文件的 ASCII 表示形式，被许多设备程序和软件库使用。

```bash
$ ppc_82xx-objcopy --gap-fill=0xff -O binary u-boot u-boot.bin
```

此 `objcopy` 调用显示了如何为 Flash 内存准备镜像。在本示例中，输入文件 `u-boot` 是完整的 ELF U-Boot 镜像，包含了符号和重定位信息。`objcopy` 工具提取包含程序代码和数据的相关部分，并将镜像放在输出文件 `u-boot.bin` 中。

Flash 内存在其擦除状态下包含全 1。因此，用全 1 填充二进制镜像中的间隙可以提高编程效率并延长 Flash 内存的寿命，现在的 Flash 内存写循环次数有限。这是通过 `objcopy` 的 `--gap-fill` 参数实现的。

这只是 `objcopy` 的一个简单用法示例。该工具可以生成 s-records并在不同格式之间进行转换。详细信息请参见手册页（man page）。

## 13.6. 杂二进制工具

你的工具箱包含几个额外的实用用工具。学习使用这些工具非常简单。你会发现这些有用工具有许多用途。

### 13.6.1. strip

`strip` 工具用于从二进制文件中移除符号和调试信息。这经常用于节省嵌入式设备的空间。在交叉开发模型中，在目标系统上使用剥离（stripped）的二进制文件，而在你的开发主机上保留未剥离的版本是非常方便的。通过这种方法，符号可以在你的开发主机上用于交叉调试，同时 `strip` 具有许多选项，这些选项在手册页中有描述。

### 13.6.2. addr2line

当我们在列表 13-12 中突出显示 `mtr` 时，我们看到 `mtr` 分析的输出包含文件名和行号。`addr2line` 工具用于读取调试信息。它通过读取调试文件中的 ELF 信息并显示对应地址的行号：

```bash
$ addr2line -f -e myprog 0x100004b0

main

main.c:5
```

注意，`addr2line` 也有许多选项，这些选项在手册页中有描述。

### 13.6.3. strings

`strings` 工具检查二进制文件中的 ASCII 数据。当可能没有符号时，通过回溯 `strings` 可以发现崩溃的原因。这对于嵌入式开发者非常有用。

### 13.6.4. ldd

并非严格意义上的二进制工具，`ldd` 是另一个有用的工具。它显示二进制文件的依赖关系。在之前的内核示例中，`ldd` 显示了内核所需的库。在挂载根文件系统后，最常见的故障之一是内核发生内核 panic：

```
VFS: Mounted root (nfs)

Freeing unused kernel memory: 96k

Kernel panic: No init found.
```

### 13.6.5. nm

`nm` 工具显示对象文件的符号。这对于各种任务都非常有用。例如，在交叉编译大型应用程序时，你会遇到未解析的符号。你可以使用 `nm` 找到包含这些符号的对象模块，并修改构建环境以包含它。

`nm` 工具为每个符号提供属性。例如，你可以发现符号是局部的还是全局的，它是定义的还是仅在特定对象模块中引用的。列表 13-18 重现了在 U-Boot 镜像上运行 `nm` 输出的几行。

## 列表 13-18. 使用 nm 显示符号

```bash
$ ppc_85xx-nm u-boot

...

fff23140 b base_address

ff24c98 B BootFile

fff00118 t boot_warm

fff21010 d border

fff23000 A _bss_start

...
```
