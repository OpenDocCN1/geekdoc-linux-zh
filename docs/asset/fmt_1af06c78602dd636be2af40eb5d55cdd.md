
如果你的进程寿命很短，很难在它退出之前暂停它。也许其他人对如何以暂停状态启动进程有好的建议；我使用另一个程序来捕获进程并暂停它以便我附加调试器。

标签：`gdb` (Prev Q) (Next Q)

## Q: 逆向 64 位 LSB 可执行文件 gdb

标签：`gdb` (Prev Q) (Next Q)

我是个新手，刚拿到 64 位 LSB 可执行文件，x86-64。我正尝试逆向它。首先尝试在第 1 行设置断点：

```bash
gdb ./filename
break 1
```

Gdb 说没有符号表。使用 "`file`" 命令。

```bash
(gdb) file
Reading symbols from ./filename(no debugging symbols)...
```

我该如何设置断点??

标签：`gdb` (Prev Q) (Next Q)

用户：nikikhil

perror 的回答：获取入口点

如果没有符号符号，首先需要找到执行文件的入口点。有几种方法（取决于你拥有的工具）：

1. 使用 `readelf`

```bash
$ readelf -h /bin/ls
ELF Header:
Magic: 7f 45 4c 02 01 00 00
Class: ELF64
Data: little endian
Version: 1 (current)
OS/ABI: UNIX
ABI Version:
Type: EXEC (Executable file)
Machine: X86-64
Version: 1
Entry address: 0x4089c
Start of program headers: 0x64 (bytes)
Start of section headers: 0x264 (bytes)
Flags: 0
Size of header: 64 (bytes)
Size of program headers: 56 (bytes)
Number of program headers: 9
Size of section headers: 64 (bytes)
Number of section headers: 27
```

所以入口点是 `0x4089c`。

2. 使用 `objdump -f /bin/ls`

```bash
$ objdump -f /bin/ls
/bin/ls: file elf64-x86-64
architecture: i386:x86-64, flags: 0x00000012 EXEC_P, HAS_MS, D_PG
start address: 0x000000004089c
```

再次，入口点是 `0x000000004089c`。

3. 使用 `gdb`

```bash
$ gdb /bin/ls
GNU gdb 7.6.2 (Debian 7.6-6)
Reading symbols from /bin/ls(no debugging symbols)...
(gdb)
Symbols from '/bin/ls'.
Local object file:
'/bin/ls', file elf64-x86-64.
Entry point: 0x4048c
0x000000004040238 - 0x000000004000254 is .interp
0x000000004000254 - 0x000000004000274 is .note.ABI_tag
0x000000004000274 - 0x000000004000298 is .note.build-id
0x000000004000298 - 0x000000004000300 is .gnu.hash
0x000000004000300 - 0x000000004000318 is .dynym
0x000000004000318 - 0x00000000400041a is .dynstr
0x00000000400041a - 0x00000000400015e is .version
0x000000004000150 - 0x000000004001640 is .gnu_version
0x000000000410160 is relia_dyn
0x00000000041016e is relia_plt
0x000000000410218 is .init
0x00000000041021c is .plt
0x000000000410290 is 0x28a0
0x000000000410a8 is .text
0x000000000411a0 is .text
0x000000000411f0 is .fini
0x000000000411f2 is .rodata
0x0000000004171c is .eh_frame
```

入口点是 `0x4089c`

之所以得到这个结果仅仅是因为我们执行了 `gdb` 进行的线性扫描。所以，位于 `@plt` 处的点是相关的（因为这会超出问题的范围）`__libc_start_main`（我不想让它变长）

事实上，`__libc_start_main` 程序初始化了带有 `libc` 动态库运行进程的内存。然后，跳转到位于 `%rdi` 的程序（通常是主程序）。

所以，主程序的地址确实是 `0x4028c0`。让我们反汇编该地址的代码：

```
(gdb) /10i 0x4028c0
0x4028c0: push %r15
0x4028c2: push %r14
0x4028c4: push %r13
0x4028c6: push %r12
0x4028c8: mov %rdi,%rbp
0x4028cc: push %rbx
0x4028cd: mov %edx,%ebx
0x4028cf: sub $0x308,%rsp
0x4028d0: mov (%r15),%rdi
```

而且，如果你观察它，这确实是主程序（main procedure）。所以，这里就是分析开始的地方。

### 警告

即使这种寻找主程序的方法在大多数情况下有效，你也必须知道，我们强烈依赖于以下假设：

- 1. 程序已经过编译并且没有直接从入口点（entrypoint）开始。用汇编编写并使用 `gcc -nostdlib` 编译的程序不会调用 `__libc_start_main` 的因子，并将直接从入口点启动。

- 2. 我们还强烈依赖于 `__libc_start_main` 的工作原理，以及 `gcc` 团队是如何设计该过程的。因此，如果你分析的程序是用另一个编译器编译的，你可能需要进一步研究该编译器以及它在运行主程序之前是如何进行内存设置的。

无论如何，如果你仔细阅读这个答案，你现在应该能够追踪到一个没有任何符号的程序。

标签：`gdb` (上一个 Q) (下一个) `elf` (上一个 Q) (下一个)

## Q：在禁用 ASLR 的情况下，为去符号的 PIE 二进制文件的 GDB 入口点设置断点

标签：`gdb` (上一个 Q) `elf` (上一个 Q) (下一个) `debugging` (上一个 Q) (下一个)

对于位置无关、静态链接、去符号的二进制文件，在 GDB 中似乎没有办法在不禁用 ASLR 的情况下在入口点设置断点。

- `break start` 和类似的函数 1 不工作，因为没有符号信息

- `stop-on-solib-events` 1 不工作，因为二进制文件不是动态链接的

- `break *0deadbeef` 入口点不工作，因为在二进制文件启动之前入口点是未解析的

- `catch load` 不工作，因为它没有加载任何库

- `start` 不工作，因为是 main 且没有加载任何库

在不修补二进制文件的情况下，我 own可以使用什么机制在执行的第一条指令处断点呢？

### 可能吗？

由于之前被删除的回答说 PIE 静态链接二进制文件是不可能的，一个显而易见的例子是链接器 it-so

它是静态链接的。

```
$ ldd /lib/x86_64-linux-gnu/ld-2.19.so
    statically linked
```

它是可执行的。

```
$ strace /lib/x86_64-linux-gnu/ld-2.19.so
execve("/lib/x86_64-linux-gnu/ld.2.19.so", ["ld", "96 vars"]) = 0x7ff783b3d000)
write(2, ["Usage: ld.so [OPTION]... EXECUT...", 1733], 1, EXECUTABLE-FILE
```

它是位置无关的。

```
$ readelf -h /lib/x86_64-linux-gnu/ld-2.19.so | grep DYN
Type:                               YN (Shared object file)
```

### 解决方案

看起来可以通过 Python 利用一些创建的事件来实现：

http://asciin.org/19078

然而，我需要原生的 GDB 解决方案。

成功的解决方案在没有 ASLR 的情况下直接执行时，会在 `ld.so` 的 `_start` 处断开。看起来如下：

```
$ sh /lib/x86_64-linux-gnu/ld-2.19.so -o ld.so
$ sh /ld.so
(gdb) set disable-randomization off
(gdb) $ your magic commands
(gdb) $ x /1 Spc
=> 0x7fffab1d20:
(gdb) info proc map
process 10432
```

| 起始地址 | 结束地址 | 大小 | 偏移 | 文件 |
|---|---|---|---|---|
| 0x7ffba51c00 | 0x7ffba51700 | 0x20000 | 0x0 | /lib/x86_64-linux-gnu/ld-2.19.so |
| 0x7ffba51700 | 0x7ffba53900 | 0x20000 | 0x22000 | /lib/x86_64-linux-gnu/ld-2.19.so |
| 0x7ffba53900 | 0x7ffba5b100 | 0x10000 | 0x0 | |
| 0x7ff3c4c700 | 0x7ff3c38400 | 0x49000 | 0x0 | [stack] |
| 0x7ff3c3fb00 | 0x7ff3c3ffd00 | 0x20000 | 0x0 | [do] |
| 0xffffff8000000 | | | 0x1800 | [syscall] |

标签：`gdb` (上一个 Q) `elf` (下一个) `debugging` (上一个 Q) (下一个)

用户：zachriggle

## zachriggle 的回答

在启动进程之前在未映射地址上设置断点是有效的。这并不是功能本身，而是设置断点失败的结果。

```
(gdb) break *0
Breakpoint 1 at 0x0
(gdb) Starting program: /home/user/ld.so
Error in setting breakpoint 1: Warning:
Cannot insert breakpoint 1.
Cannot access memory at address 0x0
Warning:
Cannot insert breakpoint 1.
Cannot access memory at address 0x0
(gdb) x/i $sp
=> 0x7ffae3cd0: mov rdi,rsp
```

标签：`gdb` (上一个 Q), `elf` (下一个), `debugging` (上一个 Q) (下一个)

## 解包

### 问题

Q：什么是导入恢复（import reconstruction），为什么是必要的？

标签：unpack (上一个 Q) (下一个)

在阅读关于解包的内容时，有时会看到“导入恢复”步骤。这是什么？为什么必要？

标签：unpack (上一个 Q) (下一个)

userfrolls 的回答

在典型的未加壳 PE 可执行文件中，头部包含描述可执行文件依赖的其他库的符号。操作系统的加载器负责将这些库加载到内存中（尚未加载），并将这些导入符号的地址放入执行文件内存映像中的结构中（其位置由元数据指定）。另一方面，壳会破坏这些元数据，转而执行重建阶段（通常由加载器执行）。解包的目标是移除保护，分析人员（或解包工具）必须确定壳为可执行文件加载的导入集合，并在解包后的执行文件映像中重建元数据，以便操作系统像往常一样正确导入。

通常在这种情况下，分析人员将确定执行文件内存映像的位置。特别是，分析人员通常定位 `IMAGE_THUNK_DATA` 数组，这些是以 NULL 终止的包含导入符号地址的数组。然后，分析人员将运行一个执行 `GetProcAddress` 逆过程的工具：给定一个导入符号的指针，它将确定指针所在的 DLL 以及指针引用的特定导出函数。例如，我们可能将 `0x76AE3FC` 解析为 `Kernel32!CreateFile`。我们使用这些信息重建 `IMAGE_DESCRIPTOR` 结构，描述 `IMAGE_THUNK_DATA` 数组的原始地址、二进制文件中 DLL 名称和导入符号（可能在新节中），并将 `IMAGE_THUNK_DATA` 条目指向这些新名称。

`ImpRec` 是一个流行的工具，它可以根据壳自动大部分或全部这些操作。我描述的内容反映了大约 95% 情况的情况。更严重的保护如复制保护和复杂的自定义恶意软件可能会进一步干扰重建过程。

## Q：解包 Billion 5102 固件

标签：unpack (上一个 Q), firmware (上一个 Q) (下一个)

我正在尝试解包固件映像，但在结构上遇到了一些问题。

首先，我有一个名为 `firmware.bin` 的映像，`file` 命令显示它是 LIF 文件：

```
firmware.bin: if binwalk
```

之后，我用十六进制对它进行分析

| 十进制 | 十六进制 | 描述 |
| --- | --- | --- |
| 84992 | 0x1AC00 | Zynos头部，头部 48 字节，ROM 图像类型为 ROMBIN，解压 |
| 85043 | 0x14C33 | LZMA 压缩数据，属性 0x50，字典大小 838608 字节，解压 |
| 128002 | 0x1F402 | GIF 图像数据，版本 8x7a, 153 x 55 |
| 136104 | 0x213D8 | Zynos头部，头部 48 字节，图像图像类型为 ROMBIN，解压 |
| 394184 | 0x5F400 | LZMA 压缩数据，属性 0x50，字典大小 838608 字节，解压 |

如所示，有 2 个 LZMA，2 个 Zynos（LZMA 也被切割过一次）以及 2 个图像。一旦我提取并解压 LZMA，第一个是单个二进制文件，第二个是包含 127 个文件的另一个 LZMA 文件，每个这些文件内部都有新文件集。

![](img/6b9e3d3281d0838532edd532056c8b57_528_0.png)

我猜我没有遵循正确的解包步骤，所以我在想如何才能获得干净的文件系统？

标签：unpack (上一个 Q), firmware (上一个 Q) (下一个)

用户：nuclear

devttys0 的回答

你可能已经猜到了，文件实用工具的输出是一个误报（false positive）。`firmware.bin` 文件包含的内容似乎是一个基本标头（注意文件开头的“SIG”），以及一堆 MIPS 可执行代码，这可能是引导加载程序：

# Skip code block

| DECIMAL | HEX | DESCRIPTION |
| :--- | :--- | :--- |
| 196 | 0xC4 | MIPS 指令,函数尾部 |
| 284 | 0x1C | MIPS 指令,函数尾部 |
| 372 | 0x74 | MIPS 指令,函数尾部 |
| 388 | 0x84 | MIPS 指令,函数尾部 |
| 416 | 0xA0 | MIPS 指令,函数尾部 |
| 424 | 0xA8 | MIPS 指令,函数序言 |
| 592 | 0x20 | MIPS 指令,函数尾部 |
| 712 | 0xC8 | MIPS 指令,函数尾部 |
| 720 | 0xD0 | MIPS 指令,函数序言 |
| 840 | 0x34 | MIPS 指令,函数尾部 |
| 896 | 0x3A | MIPS 指令,函数序言 |
| 912 | 0x38 | MIPS 指令,函数序言 |
| 920 | 0x39 | MIPS 指令,函数序言 |
| 976 | 0x3C | MIPS 指令,函数尾部 |
| 984 | 0x3D | MIPS 指令,函数尾部 |
| 1084 | 0x43 | MIPS 指令,函数尾部 |
| 1192 | 0x48 | MIPS 指令,函数尾部 |
| 1264 | 0x4F | MIPS 指令,函数尾部 |

在 `firmware.bin` 上运行 `strings` 命令证实了这一假设，其中许多关于校验和和解压错误的引用：

# Skip code block
