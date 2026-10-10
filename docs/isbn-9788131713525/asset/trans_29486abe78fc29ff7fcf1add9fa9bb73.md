

## 5.1.2 架构对象

沿着构建序列继续，会编译出一系列小型模块。其中包括几个汇编语言文件（如 `head.o`、`head-xscale.o` 等），它们执行低级别的架构和处理器特定任务。表 5-1 对每个对象进行了总结。特别值得注意的是创建名为 `piggy.o` 对象的序列。首先，使用该 gzip 命令对映像文件（二进制内核映像）进行压缩：

```
gzip -f -9 < vml > piggy.gz
```

这会创建一个名为 `piggy.gz` 的新文件，它仅仅是二进制内核映像的压缩版本。你可以在图 5-1 中直观地看到这一点。接下来的部分相当有趣。名为 `piggy.S` 的汇编语言文件被汇编，其中包含对压缩后的 `piggy.gz` 的引用。本质上，二进制内核映像被搭载（piggybacked）到一个低级别的汇编语言*引导加载程序*（bootstrap loader）中。[^3] 这个引导加载程序初始化处理器和所需的内存区域，解压缩二进制内核映像，并将其加载到系统内存中的正确位置，然后才将控制权移交给它。列表 5-2 完整复现了 `.../arch/arm/boot/compressed/piggy.S`。

### 列表 5-2

```
**汇编文件 piggy.S**

`.section .piggydata,$alloc`  
`.globl input_data`  
`input_data:`  
`.incbin "arch/arm/boot/compressed/piggy.gz"`  
`.globl input_data_end`  
`input_data_end:`
```

这个小型汇编语言文件虽然简单，但产生了一种并不显而易见的复杂性。该文件的目的是让汇编器将压缩后的二进制内核映像作为一个名为 `.piggydata` 的 ELF 节发出。这是由 `.incbin` 汇编器预处理器指令触发的，可以将其视为汇编器版本的 #include 文件。总之，这个汇编语言文件的净结果是包含压缩的二进制内核映像作为程序 ELF 输出的一部分，从而允许程序在运行时加载和解压内核映像。

[^3]: 不要与引导加载器（bootloader）混淆。引导加载程序（bootstrap loader）可以被视为第二级加载器，而引导加载器（bootloader）本身可以被视为第一级加载器。

### 5.1.3 引导加载程序（Bootstrap Loader）

不要与引导加载器（bootloader）混淆，许多架构使用*引导加载程序*（或第二级加载器）将 Linux 内核映像加载到内存中。一些引导加载程序会对内核映像执行校验和验证，大多数会执行内核映像的解压缩和重定位。在此上下文中，引导加载器（bootloader）和引导加载程序（bootstrap loader）之间的区别很简单：引导加载器（bootloader）在开机时控制主板，并不以任何方式依赖 Linux 内核。相比之下，引导加载程序（bootstrap loader）的主要生命周期目的是作为主板级引导加载器（bootloader）和 Linux 内核之间的胶水。引导加载程序（bootstrap loader）负责为内核提供适当的运行上下文，并执行解压缩和重定位内核二进制映像所需的步骤。这类似于 PC 架构中主加载器和从加载器的概念。

图 5-2 清晰地展示了这一概念。引导加载程序与内核映像拼接在一起进行加载。

![](img/7a1144833e62564667e7dd9eb4c9f03d_136_0.png)

**图 5-2**  
ARM XScale 的复合内核映像

在我们正在研究的示例中，引导加载程序由图 5-2 中显示的二进制映像组成。此引导加载程序执行的功能包括：

- 低级汇编处理器初始化，包括支持启用处理器内部指令和数据缓存、禁用中断以及设置 C 运行时环境。这些包括 `head.o` 和 `head-xscale.o`。
- 解压缩和重定位代码，体现在 `misc.o` 中。
- 其他处理器特定的初始化，例如 `big-endian.o`，它为特定处理器启用大端模式。

值得注意的是，前几节中我们检查的细节是特定于 ARM/XScale 内核实现的。每种架构都有不同的细节，但概念是相似的。使用与这里类似的分析方法，你可以了解你自己架构的要求。

### 5.1.4 启动消息

也许你曾见过 PC 工作站启动 Red Hat 或 SUSE Linux 等桌面 Linux 发行版。在 PC 自身的 BIOS 消息之后，你会看到 Linux 在初始化各种内核子系统时显示的一连串控制台消息。输出的很大一部分在不同架构和机器之间是通用的。两个更有趣的早期启动消息是内核版本字符串和内核命令行，稍后将详细说明。列表 5-3 复现了 ADI Engineering Coyote 参考平台在 Intel XScale IXP425 处理器上启动 Linux 的内核启动消息。该列表已加上行号以便参考。

### 列表 5-3

**IXP425 上的 Linux 启动消息**

```
1 Uncompressing Linux... done, booting the kernel.
2 Linux version 2.6.14-c1h (chris@pluto) (gcc version 3.4.3 (MontaVista 3.4.3-L_25.0.30.0501131 2005-07-23)) #11 Sat Mar 25 11:16:33 EST 2006
3 CPU: XScale-IXP425 Family [69054d1c] revision 1 (ARMv5TE)
4 Machine: ADI Engineering Coyote
5 Memory policy: ECC disabled, Data cache writeback
6 CPU0: D VIVT undefined 5 cache
7 CPU0: I cache: 32768 bytes, associativity 32, 32 byte lines, 32 sets
8 CPU0: D cache: 32768 bytes, associativity 32, 32 byte lines, 32 sets
9 Built 1 zonelist(s)
10 Kernel command line: console=ttyS0,115200 ipbootp root=/dev/nfs
11 FBD hash table entries: 512 (order: 9, 8192 bytes)
12 Console: colour dummy device 80x30
13 Denity cache hash table entries: 16384 (order: 4, 65536 bytes)
14 Inode-cache hash table entries: 16384 (order: 3, 32768 bytes)
15 Memory: 64MB = 64MB total
16 Memory: 62592KB available (1272K code, 339K data, 112K init)
17 Mount-cache hash table entries: 512
18 CPU: Testing write buffer coherency: ok
19 smpboot thread 0 started up
20 NBP: Registered protocol family 16
21 PCI: IXP4xx is host
22 PCI: IXP4Xx Using direct access for memory space
23 PCI: bus0: Fast back to back transfers enabled
24 dmacomice: registered device 0000:00:0f.0 on pci bus
25 NetWinder Floating Point Emulator V0.97 (double precision)
26 UPS52 version 2.2. (NAND) (C) 2001-2003 Red Hat, Inc.
27 Serial: 8250/16550 driver $Revision: 1.90 $ 2 ports, IRQ sharing disabled
28 ttyS0 at MMIO 0xc0001000 (irq = 13) is a XScale
29 io scheduler noop registered
30 io scheduler anticipatory registered
31 io scheduler deadline registered
32 io scheduler cfq registered
33 RARiDiS driver initialized: 16 RAM disks of 8192K size 1024 blocksize
34 loop: loaded (max 8 devices)
35 eepro100.c:v1.09-L-9/29/99 Donald Becker
L http://www.scyd.com/network/eeepro100.html
36 eepro100.c: $Revision: 1.36 $ 2000/11/17 Modified by Andrey V. Savochkin
L<saw@saw-sw.com.sg> and others
37 e0: 0000:00:0F.0, 00:0E:OC:0B:02:F8, IRQ 28.
38 Board assembly 741462-016, Physical connectors present: RJ45
39 Primary interface chip i82555 PHY #1.
40 General self-test: passed.
41 Serial subsystem-self-test: passed.
42 Internal registers self-test: passed.
43 ROM checksum self-test: passed (0xB51F404).
44 IXP4Xx-Flash.0: Found x 16 devices at 0x0 in 16-bit bank
45 Intel/Sharp Extend Query Datas Device At 0xc031
46 Using buffer write method
47 cf1_cmcsmbst_0001: Erase suspend on write enabled
48 Searching for RedBoot partition table in IXP4Xx-Flash.0 at offset 0xefe000
49 5 RedBoot partitions found on MTD device IXP4Xx-Flash.0
50 Creating 5 MTD partitions on "IXP4Xx-Flash.0":
51 0xc0000000-0xd0600000: "RedBoot"
52 0xc0010000-0xc0260000: "MyKernel"
53 0xc0030000-0xc0900000: "RootFS"
54 0xc0fc000-0xc0fc1000: "RedBoot confg"
```

