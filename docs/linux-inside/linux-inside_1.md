
# 引导

## 内核引导过程

本章介绍了 Linux 内核引导过程。你将在这看到一些描述内核加载过程的整个周期的相关文章：

*   [从引导加载程序内核](http://xinqiu.gitbooks.io/linux-inside-zh/content/Booting/index.html/linux-bootstrap-1.html) - 介绍了从启动计算机到内核执行第一条指令之前的所有阶段;
*   [在内核安装代码的第一步](http://xinqiu.gitbooks.io/linux-inside-zh/content/Booting/linux-bootstrap-2.html) - 介绍了在内核设置代码的第一个步骤。你会看到堆的初始化，查询不同的参数，如 EDD，IST 和等...
*   [视频模式初始化和转换到保护模式](http://xinqiu.gitbooks.io/linux-inside-zh/content/Booting/linux-bootstrap-3.html) - 介绍了视频模式初始化内核设置代码并过渡到保护模式。
*   [过渡到 64 位模式](http://xinqiu.gitbooks.io/linux-inside-zh/content/Booting/linux-bootstrap-4.html) - 介绍了过渡到 64 位模式的准备并过渡到 64 位。
*   [内核解压缩](http://xinqiu.gitbooks.io/linux-inside-zh/content/Booting/linux-bootstrap-5.html) - 介绍了内核解压缩之前的准备然后直接解压缩。

## 从引导加载程序内核

### 内核引导过程. Part 1.

如果你已经看过我之前的[文章](http://0xax.blogspot.com/search/label/asm)，就知道之前我开始和底层编程打交道。我写了一些关于 Linux x86_64 汇编的文章。同时，我开始深入研究 Linux 源代码。底层是如果工作的，程序是如何在电脑上运行的，他们是如何在内存中定位的，内核是如何管理进程和内存，网络堆栈是如何在底层工作的等等，这些我都非常感兴趣。因此，我决定去写另外的一系列文章关于**x86_64**框架的 Linux 内核。

值得注意的是我不是一个专业的内核黑客并且我的工作不是为内核贡献代码。这只是小兴趣。我只是喜欢底层的东西，底层是如何工作的让我产生了很大的兴趣。如果你发现任何迷惑的地方或者你有任何问题/备注，[twitter](https://twitter.com/0xAX)，email 我或者提一个[issue](https://github.com/0xAX/linux-insides).(PS:翻译上的问题请 mail 我:xinqiu.94@gmail.com 或 github 上@xinqiu)。我会很高兴。所有的文章也可以在[linux-insides](https://github.com/0xAX/linux-insides)上看，如果你发现哪里英文或内容错误，随意提个 PR。(PS:中文版地址：[`github.com/xinqiu/linux-insides`](https://github.com/xinqiu/linux-insides))

*注意这不是官方文档，只是学习和分享知识*

**需要的基础知识**

*   理解 C 代码
*   理解 汇编语言 代码 （AT&T 语法）

不管怎样，如果你才开始学一些，我会在这些文章中尝试去解释一些部分。好了，小的介绍结束，我们开始深入内核和底层。

所有的代码实际上是内核 - 3.18.如果有任何改变，我将会做相应的更新。

### 神奇的电源按钮，接下来会发生什么？

尽管这一系列文章关于 Linux 内核，我们还没有从内核代码（至少在这一章）开始。好了，当你按下你笔记本或台式机的神奇电源按钮，它开始工作。在主板发送一个信号给[电源](https://en.wikipedia.org/wiki/Power_supply)，电源提供电脑适当量的电力。一旦主板收到了[电源备妥信号](https://en.wikipedia.org/wiki/Power_good_signal),它会尝试运行 CPU 。CPU 复位寄存器里的所有剩余数据，设置预定义的值给每个寄存器。

[80386](https://en.wikipedia.org/wiki/Intel_80386) 以及后来的 CPUs 在电脑复位后，在 CPU 寄存器中定义了如下预定义数据：

```
IP          0xfff0
CS selector 0xf000
CS base     0xffff0000 
```

处理器开始在[实模式](https://en.wikipedia.org/wiki/Real_mode)工作，我们需要退回一点去理解在这种模式下的内存分割。所有 x86 兼容处理器都支持实模式，从[8086](https://en.wikipedia.org/wiki/Intel_8086)到现在的 Intel 64 位 CPU。8086 处理器有一个 20 位寻址总线，这意味着它可以对 0 到 2²⁰ 位地址空间进行操作(1Mb).不过它只有 16 位的寄存器，通过这个 16 位寄存器最大寻址是 2¹⁶ 即 0xffff(64 Kb)。[内存分配](http://en.wikipedia.org/wiki/Memory_segmentation) 被用来充分利用所有空闲地址空间。所有内存被分成固定的 65535 字节或 64 KB 大小的小块。由于我们不能用 16 位寄存器寻址小于 64KB 的内存，一种替代的方法被设计出来了。一个地址包括两个部分：数据段起始地址和从该数据段起的偏移量。为了得到内存中的物理地址，我们要让数据段乘 16 并加上偏移量：

```
PhysicalAddress = Segment * 16 + Offset 
```

举个例子，如果 `CS:IP` 是 `0x2000:0x0010`, 相关的物理地址将会是：

```
>>> hex((0x2000 << 4) + 0x0010)
'0x20010' 
```

不过如果我们让最大端进行偏移：`0xffff:0xffff`，将会是：

```
>>> hex((0xffff << 4) + 0xffff)
'0x10ffef' 
```

这超出 1MB65519 字节。既然只有 1MB 在实模式中可以访问，`0x10ffef` 变成有[A20](https://en.wikipedia.org/wiki/A20_line)缺陷的 `0x00ffef`。

我们知道实模式和内存地址。回到复位后的寄存器值。

`CS` register consists of two parts: the visible segment selector and hidden base address. We know predefined `CS` base and `IP` value, logical address will be:

```
0xffff0000:0xfff0 
```

In this way starting address formed by adding the base address to the value in the EIP register:

```
>>> 0xffff0000 + 0xfff0
'0xfffffff0' 
```

We get `0xfffffff0` which is 4GB - 16 bytes. This point is the [Reset vector](http://en.wikipedia.org/wiki/Reset_vector). This is the memory location at which CPU expects to find the first instruction to execute after reset. It contains a [jump](http://en.wikipedia.org/wiki/JMP_%28x86_instruction%29) instruction which usually points to the BIOS entry point. For example, if we look in [coreboot](http://www.coreboot.org/) source code, we will see it:

```
 .section ".reset"
    .code16
.globl    reset_vector
reset_vector:
    .byte  0xe9
    .int   _start - ( . + 2 )
    ... 
```

We can see here the jump instruction [opcode](http://ref.x86asm.net/coder32.html#xE9) - `0xe9` to the address `_start - ( . + 2)`. And we can see that `reset` section is 16 bytes and starts at `0xfffffff0`:

```
SECTIONS {
    _ROMTOP = 0xfffffff0;
    . = _ROMTOP;
    .reset . : {
        *(.reset)
        . = 15 ;
        BYTE(0x00);
    }
} 
```

Now the BIOS has started to work. After initializing and checking the hardware, it needs to find a bootable device. A boot order is stored in the BIOS configuration. The function of boot order is to control which devices the kernel attempts to boot. In the case of attempting to boot a hard drive, the BIOS tries to find a boot sector. On hard drives partitioned with an MBR partition layout, the boot sector is stored in the first 446 bytes of the first sector (512 bytes). The final two bytes of the first sector are `0x55` and `0xaa` which signals the BIOS that the device is bootable. For example:

```
;
; Note: this example is written in Intel Assembly syntax
;
[BITS 16]
[ORG  0x7c00]

boot:
    mov al, '!'
    mov ah, 0x0e
    mov bh, 0x00
    mov bl, 0x07

    int 0x10
    jmp $

times 510-($-$$) db 0

db 0x55
db 0xaa 
```

Build and run it with:

```
nasm -f bin boot.nasm && qemu-system-x86_64 boot 
```

This will instruct [QEMU](http://qemu.org) to use the `boot` binary we just built as a disk image. Since the binary generated by the assembly code above fulfills the requirements of the boot sector (the origin is set to `0x7c00`, and we end with the magic sequence). QEMU will treat the binary as the master boot record(MBR) of a disk image.

We will see:

![Simple bootloader which prints only `!`](img/37014685.jpg)

In this example we can see that this code will be executed in 16 bit real mode and will start at `0x7c00` in memory. After the start it calls the [0x10](http://www.ctyme.com/intr/rb-0106.htm) interrupt which just prints `!` symbol. It fills rest of 510 bytes with zeros and finish with two magic bytes `0xaa` and `0x55`.

You can see binary dump of it with `objdump` util:

```
nasm -f bin boot.nasm
objdump -D -b binary -mi386 -Maddr16,data16,intel boot 
```

A real-world boot sector has code for continuing the boot process and the partition table instead of a bunch of 0's and an exclamation point :) Ok so, from this point onwards BIOS hands over the control to the bootloader and we can go ahead.

**NOTE**: As you can read above the CPU is in real mode. In real mode, calculating the physical address in memory is done as following:

```
PhysicalAddress = Segment * 16 + Offset 
```

Same as I mentioned before. But we have only 16 bit general purpose registers. The maximum value of 16 bit register is: `0xffff`; So if we take the biggest values the result will be:

```
>>> hex((0xffff * 16) + 0xffff)
'0x10ffef' 
```

Where `0x10ffef` is equal to `1MB + 64KB - 16b`. But a [8086](https://en.wikipedia.org/wiki/Intel_8086) processor, which was the first processor with real mode. It had 20 bit address line and `2²⁰ = 1048576.0` is 1MB. So, it means that the actual memory available is 1MB.

General real mode's memory map is:

```
0x00000000 - 0x000003FF - Real Mode Interrupt Vector Table
0x00000400 - 0x000004FF - BIOS Data Area
0x00000500 - 0x00007BFF - Unused
0x00007C00 - 0x00007DFF - Our Bootloader
0x00007E00 - 0x0009FFFF - Unused
0x000A0000 - 0x000BFFFF - Video RAM (VRAM) Memory
0x000B0000 - 0x000B7777 - Monochrome Video Memory
0x000B8000 - 0x000BFFFF - Color Video Memory
0x000C0000 - 0x000C7FFF - Video ROM BIOS
0x000C8000 - 0x000EFFFF - BIOS Shadow Area
0x000F0000 - 0x000FFFFF - System BIOS 
```

But stop, at the beginning of post I wrote that first instruction executed by the CPU is located at the address `0xFFFFFFF0`, which is much bigger than `0xFFFFF` (1MB). How can CPU access it in real mode? As I write about it and you can read in [coreboot](http://www.coreboot.org/Developer_Manual/Memory_map) documentation:

```
0xFFFE_0000 - 0xFFFF_FFFF: 128 kilobyte ROM mapped into address space 
```

At the start of execution BIOS is not in RAM, it is located in the ROM.

### Bootloader



有许多引导加载程序可以启动 Linux，例如 [GRUB 2](https://www.gnu.org/software/grub/) 和 [syslinux](http://www.syslinux.org/wiki/index.php/The_Syslinux_Project)。Linux 内核有一个 [Boot protocol](https://github.com/torvalds/linux/blob/master/Documentation/x86/boot.txt)，它规定了引导加载程序实现 Linux 支持的要求。本示例将描述 GRUB 2。

现在，当 BIOS 选择了启动设备并将控制权转移到引导扇区代码后，执行从 [boot.img](http://git.savannah.gnu.org/gitweb/?p=grub.git;a=blob;f=grub-core/boot/i386/pc/boot.S;hb=HEAD) 开始。由于可用空间非常有限，这段代码非常简单，并包含一个指针，用于跳转到 GRUB 2 的核心映像位置。核心映像以 [diskboot.img](http://git.savannah.gnu.org/gitweb/?p=grub.git;a=blob;f=grub-core/boot/i386/pc/diskboot.S;hb=HEAD) 开始，它通常存储在第一扇区之后、第一个分区之前的未使用空间中。上述代码将核心映像的其余部分加载到内存中，其中包含 GRUB 2 的内核和用于处理文件系统的驱动程序。加载完核心映像的其余部分后，执行 [grub_main](http://git.savannah.gnu.org/gitweb/?p=grub.git;a=blob;f=grub-core/kern/main.c)。

`grub_main` 初始化控制台、获取模块的基地址、设置根设备、加载/解析 grub 配置文件、加载模块等。在执行结束时，`grub_main` 将 grub 切换到正常模式。`grub_normal_execute`（来自 `grub-core/normal/main.c`）完成最后的准备工作并显示用于选择操作系统的菜单。当我们选择其中一个 grub 菜单项时，`grub_menu_execute_entry` 开始执行，它会执行 grub 的 `boot` 命令，从而开始启动所选的操作系统。

正如我们在内核启动协议中所读到的，引导加载程序必须读取并填充内核 setup 头部的某些字段，该头部从内核 setup 代码的 `0x01f1` 偏移处开始。内核头文件 [arch/x86/boot/header.S](https://github.com/torvalds/linux/blob/master/arch/x86/boot/header.S) 从以下位置开始：

```
 .globl hdr
hdr:
    setup_sects: .byte 0
    root_flags:  .word ROOT_RDONLY
    syssize:     .long 0
    ram_size:    .word 0
    vid_mode:    .word SVGA_MODE
    root_dev:    .word 0
    boot_flag:   .word 0xAA55 
```

引导加载程序必须用从命令行获取或计算出的值来填充此头部及其余部分（在 Linux 启动协议中仅标记为 `write` 的部分，例如 [这里](https://github.com/torvalds/linux/blob/master/Documentation/x86/boot.txt#L354)）。我们不会描述和解释内核 setup 头部的所有字段，在内核使用它们时我们会再回来讨论。无论如何，你可以在 [boot protocol](https://github.com/torvalds/linux/blob/master/Documentation/x86/boot.txt#L156) 中找到任何字段的描述。

正如我们在内核启动协议中所看到的，内核加载后的内存映射如下：

```
 | Protected-mode kernel  |
100000   +------------------------+
         | I/O memory hole        |
0A0000   +------------------------+
         | Reserved for BIOS      | Leave as much as possible unused
         ~                        ~
         | Command line           | (Can also be below the X+10000 mark)
X+10000  +------------------------+
         | Stack/heap             | For use by the kernel real-mode code.
X+08000  +------------------------+
         | Kernel setup           | The kernel real-mode code.
         | Kernel boot sector     | The kernel legacy boot sector.
       X +------------------------+
         | Boot loader            | 
```

因此，在引导加载程序将控制权移交给内核后，它从以下位置开始执行：

```
0x1000 + X + sizeof(KernelBootSector) + 1 
```

其中 `X` 是内核引导扇区加载的地址。在我的例子中，`X` 是 `0x10000`，我们可以在内存转储中看到它：

![kernel first address](img/49d843b3.jpg)

好了，现在引导加载程序已将 Linux 内核加载到内存中，填充了头部字段并跳转到了内核。现在我们可以直接进入内核 setup 代码。

# 内核 Setup 的开始

终于我们进入内核了。从技术上讲，内核尚未运行，首先我们需要设置内核、内存管理器、进程管理器等。内核 setup 的执行从 [arch/x86/boot/header.S](https://github.com/torvalds/linux/blob/master/arch/x86/boot/header.S) 的 [_start](https://github.com/torvalds/linux/blob/master/arch/x86/boot/header.S#L293) 开始。乍一看有点奇怪，因为在此之前有很多指令。

实际上，很久以前 Linux 内核有自己的引导加载程序，但现在如果你运行例如：

```
qemu-system-x86_64 vmlinuz-3.18-generic 
```

你会看到：

![Try vmlinuz in qemu](img/a5ed9787.jpg)

实际上，`header.S` 从 [MZ](https://en.wikipedia.org/wiki/DOS_MZ_executable)（见上图）、错误消息打印和接下来的 [PE](https://en.wikipedia.org/wiki/Portable_Executable) 头部开始：

```
#ifdef CONFIG_EFI_STUB
# "MZ", MS-DOS header
.byte 0x4d
.byte 0x5a
#endif
...
...
...
pe_header:
    .ascii "PE"
    .word 0 
```

这是为了支持使用 [UEFI](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface) 加载操作系统。这里我们不会讨论它的工作原理（我们将在后面的部分中讨论）。

因此，实际的内核 setup 入口点是：

```
// header.S line 292
.globl _start
_start: 
```

引导加载程序（grub2 和其他引导加载程序）知道这个点（从 `MZ` 偏移 `0x200`）并直接跳转到这个点，尽管 `header.S` 是从打印错误消息的 `.bstext` 段开始的：

```
//
// arch/x86/boot/setup.ld
//
. = 0;                    // current position
.bstext : { *(.bstext) }  // put .bstext section to position 0
.bsdata : { *(.bsdata) } 
```

所以内核 setup 入口点是：

```
 .globl _start
_start:
    .byte 0xeb
    .byte start_of_setup-1f
1:
    //
    // rest of the header
    // 
```

这里我们可以看到跳转指令的操作码 `0xeb` 跳转到 `start_of_setup-1f` 位置。`Nf` 记号表示以下含义：`2f` 指下一个局部 `2:` 标签。在我们的例子中，它是紧跟在跳转指令之后的标签 `1`。它包含 setup [header](https://github.com/torvalds/linux/blob/master/Documentation/x86/boot.txt#L156) 的其余部分，在 setup 头部之后，我们可以看到从 `start_of_setup` 标签开始的 `.entrytext` 段。

实际上，这是除了前面的跳转指令之外，开始执行的第一段代码。在内核 setup 从引导加载程序获得控制权后，第一条 `jmp` 指令位于内核实模式起始地址偏移 `0x200`（前 512 字节）处。这一点我们可以在 Linux 内核启动协议中读到，也可以在 grub2 的源代码中看到：

```
 state.gs = state.fs = state.es = state.ds = state.ss = segment;
  state.cs = segment + 0x20; 
```

这意味着内核 setup 开始工作后，段寄存器将具有以下值：

```
fs = es = ds = ss = 0x1000
cs = 0x1020 
```

这是针对我的情况，即内核加载在 `0x10000` 时。

跳转到 `start_of_setup` 之后，它需要完成以下工作：

*   确保所有段寄存器的值相等
*   如果需要，设置正确的堆栈
*   设置 [bss](https://en.wikipedia.org/wiki/.bss)
*   跳转到 [main.c](https://github.com/torvalds/linux/blob/master/arch/x86/boot/main.c) 的 C 代码

让我们看一下实现。

## 段寄存器对齐

首先，它确保 `ds` 和 `es` 段寄存器指向相同的地址，并通过 `sti` 指令启用中断：

```
 movw    %ds, %ax
    movw    %ax, %es
    sti 
```

如上所述，grub2 将内核 setup 代码加载到 `0x10000` 地址，`cs` 加载到 `0x1020`，因为执行不是从文件开头开始的，而是从：

```
_start:
    .byte 0xeb
    .byte start_of_setup-1f 
```



`jump`，与`[4d 5a](https://github.com/torvalds/linux/blob/master/arch/x86/boot/header.S#L47)`相距512字节。同时，需要将`cs`从`0x10200`对齐到`0x10000`，以与其他所有段寄存器保持一致。之后，我们设置堆栈：

```
 pushw    %ds
    pushw    $6f
    lretw 
```

将`ds`的值压入堆栈，并压入`[6](https://github.com/torvalds/linux/blob/master/arch/x86/boot/header.S#L494)`标签的地址，然后执行`lretw`指令。当调用`lretw`时，它会将标签`6`的地址加载到[指令指针](https://en.wikipedia.org/wiki/Program_counter)寄存器中，并将`cs`设为`ds`的值。在此之后，`ds`和`cs`将具有相同的值。

## 堆栈设置

实际上，几乎所有的设置代码都是为实模式下的C语言环境做准备。下一步是检查`ss`寄存器的值，并在`ss`错误时建立正确的堆栈：

```
 movw    %ss, %dx
    cmpw    %ax, %dx
    movw    %sp, %dx
    je    2f 
```

通常，这里有三种不同的情况：

*   `ss`具有有效值`0x10000`（与除`cs`之外的所有其他段寄存器相同）

*   `ss`无效且`CAN_USE_HEAP`标志已设置（见下文）

*   `ss`无效且`CAN_USE_HEAP`标志未设置（见下文）

让我们逐一查看这些情况：

1.  `ss`具有正确的地址（`0x10000`）。在这种情况下，我们跳转到标签`[2](https://github.com/torvalds/linux/blob/master/arch/x86/boot/header.S#L481)`：

```
2:     andw    $~3, %dx
    jnz    3f
    movw    $0xfffc, %dx
3:  movw    %ax, %ss
    movzwl %dx, %esp
    sti 
```

在这里，我们可以看到将`dx`（包含引导加载程序给出的`sp`）对齐到4字节，并检查它是否为零。如果为零，则将`0xfffc`（最大段大小（64 KB）之前的4字节对齐地址）放入`dx`。如果非零，则继续使用引导加载程序给出的`sp`（在我的例子中是`0xf7f4`）。之后，我们将`ax`的值放入`ss`，它存储了正确的段地址`0x10000`，并设置正确的`sp`。在这之后，我们就有了正确的堆栈：

![stack](img/b10804f1.jpg)

1.  在第二种情况（`ss` != `ds`）中，首先将[_end](https://github.com/torvalds/linux/blob/master/arch/x86/boot/setup.ld#L52)（设置代码末尾的地址）的值放入`dx`。然后使用`testb`指令检查`loadflags`头字段，以确定是否可以使用堆。`[loadflags](https://github.com/torvalds/linux/blob/master/arch/x86/boot/header.S#L321)` 是一个位掩码头，定义如下：

```
#define LOADED_HIGH        (1<<0)
#define QUIET_FLAG        (1<<5)
#define KEEP_SEGMENTS    (1<<6)
#define CAN_USE_HEAP    (1<<7) 
```

正如我们在引导协议中读到的：

```
Field name:    loadflags

  This field is a bitmask.

  Bit 7 (write): CAN_USE_HEAP
    Set this bit to 1 to indicate that the value entered in the
    heap_end_ptr is valid.  If this field is clear, some setup code
    functionality will be disabled. 
```

如果`CAN_USE_HEAP`位已设置，则将`heap_end_ptr`放入`dx`，它指向`_end`，并将`STACK_SIZE`（最小堆栈大小 - 512 字节）加到其上。之后，如果`dx`没有进位，则跳转到`2`标签（不会发生进位，因为`dx = _end + 512`），如同前一种情况一样，建立正确的堆栈。

![stack](img/e358e174.jpg)

1.  最后一种情况，当`CAN_USE_HEAP`未设置时，我们仅使用从`_end`到`_end + STACK_SIZE`的最小堆栈：

![minimal stack](img/454d30ad.jpg)

## BSS 设置

在我们跳转到主 C 代码之前，最后两个步骤是设置[BSS](https://en.wikipedia.org/wiki/.bss)区域，并检查“魔术”签名。首先，进行签名检查：

```
cmpl    $0x5a5aaa55, setup_sig
jne    setup_bad 
```

这仅仅是将[setup_sig](https://github.com/torvalds/linux/blob/master/arch/x86/boot/setup.ld#L39)与魔术数字`0x5a5aaa55`进行比较。如果它们不相等，则会报告致命错误。

但如果魔术数字匹配，我们知道我们有了一组正确的段寄存器和堆栈，接下来只需在跳入 C 代码之前设置 BSS 段。

BSS 段用于存储静态分配的、未初始化的数据。Linux 确保首先清除这块内存区域，使用以下代码：

```
 movw    $__bss_start, %di
    movw    $_end+3, %cx
    xorl    %eax, %eax
    subw    %di, %cx
    shrw    $2, %cx
    rep; stosl 
```

首先，将[__bss_start](https://github.com/torvalds/linux/blob/master/arch/x86/boot/setup.ld#L47)地址移动到`di`，并将`_end + 3`地址（+3 用于 4 字节对齐）移动到`cx`。`eax`寄存器被清零（使用`xor`指令），计算 BSS 段大小（`cx`-`di`）并放入`cx`。然后，`cx`除以四（一个“字”的大小），并重复使用`stosl`指令，将`eax`（零）的值存储到`di`指向的地址，并将`di`自动增加四（此操作持续到`cx`达到零）。这段代码的最终效果是，在从`__bss_start`到`_end`的所有内存字中写入零：

![bss](img/1d9d2ae7.jpg)

## 跳转到主函数

就这样，我们有了堆栈和 BSS，现在可以跳转到`main()` C 函数了：

```
 calll main 
```

`main()` 函数位于 [arch/x86/boot/main.c](https://github.com/torvalds/linux/blob/master/arch/x86/boot/main.c)。那里会有什么？我们将在下一部分中看到。

## 结论

这是关于 Linux 内核内部的第一部分结束。如果您有任何问题或建议，请通过推特 [0xAX](https://twitter.com/0xAX) 联系我，发送电子邮件，或直接创建 [issue](https://github.com/0xAX/linux-internals/issues/new)。在下一部分中，我们将看到 Linux 内核设置中执行的第一段 C 代码，包括`memset`、`memcpy`等内存例程的实现，`earlyprintk`的实现以及早期控制台初始化等等。

**请注意，英语不是我的母语，对于造成的不便深表歉意。如果您发现任何错误，请向 [linux-internals](https://github.com/0xAX/linux-internals) 发送 PR。**

## 链接

*   [Intel 80386 程序员参考手册 1986](http://css.csail.mit.edu/6.858/2014/readings/i386.pdf)

*   [Intel® 架构最小引导加载程序](https://www.cs.cmu.edu/~410/doc/minimal_boot.pdf)

*   [8086](http://en.wikipedia.org/wiki/Intel_8086)

*   [80386](http://en.wikipedia.org/wiki/Intel_80386)

*   [重置向量](http://en.wikipedia.org/wiki/Reset_vector)

*   [实模式](http://en.wikipedia.org/wiki/Real_mode)

*   [Linux 内核启动协议](https://www.kernel.org/doc/Documentation/x86/boot.txt)

*   [CoreBoot 开发者手册](http://www.coreboot.org/Developer_Manual)

*   [Ralf Brown 的中断列表](http://www.ctyme.com/intr/int.htm)

*   [电源](http://en.wikipedia.org/wiki/Power_supply)

*   [电源良好信号](http://en.wikipedia.org/wiki/Power_good_signal)
