
# 列表 5-1 最终内核构建序列：ARM/IXP2S (Coyote)

```
$ make ARCH=arm CROSS_COMPILE=xscale_be- Image
  <省略了许多构建步骤以保持清晰>
LD vmlinux
SYSMAP System.map
SYSMAP .tmp_System.map
OBJCOPY arch/arm/boot/Image
Kernel: arch/arm/boot/Image is ready
AS arch/arm/boot/compressed/head.o
GZIP arch/arm/boot/compressed/piggy.gz
AS arch/arm/boot/compressed/piggy.o
AS arch/arm/boot/compressed/misc.o
CC arch/arm/boot/compressed/head-xscale.o
AS arch/arm/boot/compressed/big-endian.o
LD arch/arm/boot/compressed/vmlinux
OBJCOPY arch/arm/boot/zImage
Kernel: arch/arm/boot/zImage is ready
```

在列表 5-1 的第三行中，`vmlinux` 镜像（内核本身）被链接。随后，处理了一些额外的对象模块。这些包括

> 内核几乎总是以压缩格式存储，除非启动时间是关键问题。在这种情况下，镜像可能被称为 `uImage`，一个带有 U-Boot 头的压缩 `vmlinux` 文件。见第 7 章。

包括 `head.o`、`piggy.o` 以及特定架构的 `head-xscale.o` 等。（这些标签标识了每行正在发生的操作。例如，`AS` 表示调用了汇编器，`GZIP` 表示压缩，以此类推。）这些通用对象模块特定于特定的架构（在本例中为 ARM/XScale），并包含了在该特定架构上启动内核所需的低级公用程序。表 5-1 详细列出了来自列表 5-1 的组件。

## 表 5-1 ARM/XScale 低层对象

| 组件 | 描述 |
| --- | --- |
| vmlinux | 内核本身，采用 ELF 格式，包括符号、注释、调试信息（如果使用 `-g` 编译）以及架构通用组件。 |
| System.map | 用于 `vmlinux` 模块的基于文本的内核符号表。 |
| .tmp_System.map | 仅用于检查 `System.map` 的正确性而生成；否则不会在最终镜像中使用。 |
| Image | 二进制内核模块，已去除了符号、备注和注释。 |
| head.o | 适用于 ARM 处理器的通用 ARM 特定启动代码。该对象由引导程序传递控制权。 |
| piggy.gz | 使用 gzip 压缩的文件。 |
| piggy.o | 以汇编语言格式表示的文件 `piggy.gz`，以便其与后续对象 `misc.o` 链接（见正文）。 |
| misc.o | 用于解压内核 (`piggy.gz`) 的程序，以及在某些架构上常见的“Uncompress Linux Done”启动消息的来源。 |
| head-xscale.o | 针对 XScale 处理器族的处理器初始化。 |
| big-endian.o | 将 XScale 处理器切换到大端模式的微型汇编程序。 |
| vmlinux | 复合内核镜像。这是一个不幸的命名选择，因为它与内核本身的名称重复了；两者并非同一个。该二进制文件是内核本身与此表中的对象链接后的结果。具体解释请参正文。 |

插图将帮助你理解这一结构以及随后的讨论。图 5-1 显示了镜像组件及其在构建过程中的蜕变。接下来的章节详细描述了直到生成可引导内核镜像的组件和过程。

> “piggy”一词最初用于描述“寄生”（piggyback）概念。在这种情况下，二进制内核镜像被寄生在引导加载器上，从而产生复合内核镜像。

## 5.1 复合内核镜像：Piggy 和伙伴

图 5-1 复合内核镜像构建 (img/75da989fc023923ea1a768dd5...)

### 5.1.1 Image 对象

在 `vmlinux` 内核 ELF 文件构建完成后，内核构建系统继续处理表 5-1 中描述的目标。`Image` 对象是由 `vmlinux` 对象创建的。`Image` 基本上是去除了冗余段（备注和注释）以及可能存在的任何调试符号的 `vmlinux` ELF 文件的剥离版（stripped）。使用以下命令执行此目的：

```
xscale_be_objcopy -o binary -R .note -R .gnu.build-id -R .comment -S vmlinux arch/arm/boot/
```

`-o` 选项告诉 `objcopy` 生成二进制文件；`-R` 选项移除名为 `.note`、`.gnu.build-id` 和 `.comment` 的 ELF 段；`-S` 选项是剥离调试符号的标志。注意，`objcopy` 将 `vmlinux` ELF 镜像作为输入，并生成名为 `Image` 的目标二进制文件。总之，`Image` 不过是将内核本身从 ELF 格式转换为二进制格式，并剥离了调试符号以及上述的 `.note*` 和 `.comment` 段。

### 5.1.2 架构对象

继续后续构建序列，编译了许多小模块。这些包括几个汇编语言文件（`head.o`、`head-xscale.o` 等），它们执行低级架构和特定处理器的任务。这些对象中的每一个都已经在表 5-1 中进行了总结。特别值得注意的是创建名为 `piggy.o` 对象的序列。首先，使用此 gzip 命令对 `Image` 文件（二进制内核镜像）进行压缩：

```
cat Image | gzip -fp -9 > piggy.gz
```

创建了一个名为 `piggy.gz` 的新文件，它仅仅是二进制内核 `Image` 的压缩版本。接下来的步骤非常有趣。汇编汇编语言文件 `piggy.S`，它包含了对压缩后的 `piggy.gz` 的引用。本质上，二进制内核镜像正作为载荷被寄存在低级汇编语言引导加载器中。该引导加载器初始化处理器和所需的内存区域，解压二进制内核镜像，并在将控制权交给它之前将其加载到系统内存的正确位置。列表 5-2 生成了整个 `.../arch/arm/boot/compressed/piggy.S`。

#### 列表 5-2 汇编文件 Piggy.S

```
.section .piggydata,#alloc
.global input_data
input_data:
  .incbin "../arch/arm/boot/compressed/piggy.gz"
  .global input_data_end
input_data_end:
```

这个小语言文件虽然简单，但产生的复杂性并非显而易见。该文件的目的是让压缩后的内核镜像被汇编器输出为一个名为 `piggydata` 的 ELF 段。它是由 `.incbin` 汇编预处理器指令触发的，可以将其视为汇编器版本的 `#include` 文件，只不过它期望的是二进制数据。总而言之，该汇编文件的结果就是压缩后的内核镜像。

> 该文件的目的是让压缩后的内核镜像被汇编器输出为一个名为 `piggydata` 的 ELF 段。它是由 `.incbin` 汇编预处理器指令触发的，可以将其视为汇编器版本的 `#include` 文件，只不过它期望的是二进制数据。

### 5.1.3 引导加载器

在我们研究的示例中，引导加载器由图 5-2 所示的二进制镜像组成。该加载器的功能包括：

- 低级汇编处理器初始化，包括启用器的指令和数据缓存、禁用中断并设置 C 运行时。这些包括 `head-xscale.o`。
- 封装在 `misc.o` 中的解压缩和重定位代码。
- 其他处理器特定的初始化，例如大端模式。

注意的是，我们观察的细节特定的 ARM/XScale 实现。每个架构都有不同的细节，尽管概念是相似的。通过类似于此处的分析，你可以了解你的架构的要求。

### 5.1.4 启动消息

可能你见过 PC 启动 Red Hat 或 SUSE 等桌面 Linux 发行版。在 PC BIOS 消息之后，你会看到 Linux 输出大量的控制信息以初始化各种内核子系统。输出的大部分在不同架构和机器之间是通用的。两个最有趣的启动消息是内核版本和命令行，稍后会描述。列表 5-3 重现了 ADI 工程平台在 Linux XScale IP425 处理器上启动时的内核启动消息。列表已带有行号以便参考。

#### 列表 5-3 Linux 启动消息

| 行号 | 内容 |
| --- | --- |
| 1 | 使用基地址 0x01000000 和长度 0x01cell4 |
| 2 | 解压 Linux..., 完成，正在启动内核。 |
| 3 | Linux 版本 2.6.32-07500-g8bea867 (chris@brutus) (gcc 版本 4.2.0 20070126 (prerelease) (MontVista 4.2.0-3.0.0.072771 2007-03-10)) #2009年12月16日 周三 23:07:01 东部标准时间 |
| 4 | CPU: XScale-IP42x Family [690541c1] 版本 1 (ARMv5TE), cr=00039ff |
| 5 | CPU: VIVT 数据缓存，VIVT 指令缓存 |
| 6 | 机器: ADI Engineering Coyote |
| 7 | 内存策略：禁用 ECC，数据缓存写回 |
| 8 | 按区域顺序、移动性分组构建了 8 个区域列表 (zonelist)。总页数：16256 |
| 9 | 内核命令行：console=ttyS0,115200=/dev/nfs ipdhcp |
| 10 | PID 哈希表条目：256 (order: -2, 1024 bytes) |
| 11 | Dentry 缓存哈希表条目: 8192 (order: 3, 32768 bytes) |
| 12 | Inode 哈希表条目: 4096 (order: 2, 16384 bytes) |
| 13 | 内存：总计 64MB = 64MB |
| 14 | 内存：可用 6108KB (332k 代码, 199K 数据, 120K , OK) |
| 15 | SLUB: Genslabs=1,HW=32,Order=0-3, Minobjects=0, CPUs=1, Nodes=1 |
| 16 | 分层 RCU 实现。 |
| 17 | 已启用基于 RCU 的僵尸 CPU 检测。 |
| 18 | NR_IRQ:64 |
| 19 | 正在校准延迟循环... 52.48 BogoMIPS (lpj=2662400) |
| 20 | 挂载缓存哈希表条目：512 |
| 21 | CPU: 测试写缓冲区一致性：ok |
| 22 | NET: 注册协议族 16 |
| 23 | IP4XX: 使用 16MB 扩展总窗口大小 |
| 24 | PCI: IP4XX 主机 |
| 25 | PCI: IP4XX 使用内存空间直接访问 |
| 26 | PCI 总线 0: 启用快速背靠背传输 |
| 27 | SCSI 子系统初始化 |
| 28 | usbcore: 注册新接口驱动程序 usbfs |
| 29 | usbcore: 注册新接口驱动程序 hub |
| 30 | usbcore: 注册新设备驱动程序 usb |
| 31 | NET: 注册协议族 8 |
| 32 | NET: 注册协议族 20 |
| 33 | NET: 注册协议族 2 |
| 34 | IP4XX 队列管理器初始化。 |
| 35 | NetWinder 浮点数模拟器 0.97 (双精度) |
| 36 | JFFS2 版本 2.2. (NAND) 2001-2006 Red Hat, Inc. |
| 37 | I/O 调度器 noop 已注册 |
| 38 | I/O 调度器 deadline 已注册 |
| 39 | I/O 调度器 cfq 已注册 (默认) |
| 40 | 串口：8250/16550 驱动，2 个端口，禁用 irq 共享 |
| 41 | serial8250.0: MMIO 0x8c001000 ttyS0 (irq = 13) 是 XScale |
| 42 | 已启用控制台 [tty0] |
| 43 | 统一多平台 E-IDE 驱动 |
| 44 | ide-gd 驱动 1.18 |
| 45 | IP4XX-Flash.0: 在 0x0 处的 16 位存储器中找到 1x10 个设备 |
| 46 | 0x0031 处的 Intel/Sharp 扩展查询表 |
| 47 | 0x0031 处的 Intel/Sharp 扩展查询表 |
| 48 | 使用缓冲区写入方法 |
| 49 | 在 IP4XX-Flash.0 偏移 0xfe000 处搜索 RedBoot 分区表 |
| 50 | 在 MTD 设备 IXP4XX-Flash.0 上找到 RedBoot 分区 |
| 51 | 在 "IPX4XX-Flash.0" 上创建 5 个 MTD 分区 |
| 52 | 0x000000000000-0x000000060000 : "RedBoot" |
| 53 | 0x000000100000-0x000000260000 : "MyKernel" |
| 54 | 0x000000300000-0x000000900000 : "RootFS" |
| 55 | 0x000000fc0000-0x00000ffc1000 : "RedBoot config" |
| 56 | 0x000000fe0000-0x000001010000 : "FIS directory" |
| 57 | e100: Intel(R) PRO/100 网络驱动, 3.5.24-k-NAPI |
| 58 | e101: 版权所有 © 1999-2006 Intel |
| 59 | ehci_hcd: USB 2.0 "增强"主机控制器 (EHCI) 驱动 |
| 60 | ohci_hcd: USB 1.1 '开放'主机控制器 (OHCI) 驱动 |
| 61 | uhci_hcd: USB 通用主机控制器接口驱动 |
| 62 | 正在初始化 USB 批量存储驱动... |
| 63 | usbcore: 注册新接口驱动程序 usb-storage |
| 64 | USB 批量存储支持已注册。 |
| 65 | IXP4XX 看门狗计时器：心跳 60 秒 |
| 66 | usbcore: 注册新接口驱动程序 ushid |
| 67 | ushid: USB HID 核心驱动 |
| 68 | TCP cubic 已注册 |
| 69 | NET: 注册协议族 17 |
| 70 | 检测到 XScale DSP 协处理器。 |
| 71 | drivers/rtc/hctosys.c: 无法打开 rtc 设备 (rtc0) |
| 72 | e100 0000:00:0f.0: 固件: 使用内置固件 e100/d101m_ucode.bin |
| 73 | e100: eth0 NIC 链路已启动 100 Mbps 全双工 |
| 74 | IP-Config: 完成: |
| 75 | device=eth0,addr=192.168.0.29, mask=255.255.255.0, gw=255.255.255.255, |
| 76 | host=coyote1, nis-domain=(none), |
| 77 | bootserver=192.168.0.103, rootserver=192.168.0.103, rootpath= |
| 78 | 查找 192.168.0.103 上的 RPC 1003/2 |
| 79 | 查找 192.168.0.103 上的 RPC 1005/1 |
| 80 | VFS: 挂载在设备 0.11 上的根 (nfs 文件系统) |
| 81 | 释放 内存：120K |
| 82 | INIT: 版本 2.8 启动 |
| 83 | ... <省略部分消息> |
| 84 | coyote1 登录: |

内核在启动期间产生了许多有用信息，如列表 5-3 所示。我们在 RedBoot 引导加载程序中研究此输出。第 2 行是由之前介绍的引导加载程序产生的。此消息是由 `.../arch/arm/boot/compressed/misc.c` 中的 `decompress()` 函数产生的。

列表 5-3 的第 3 行是内核版本字符串。它是内核本身的第一行输出。内核进入 `start_kernel()` 时执行的 `.../init/main.c` 中的前几行 C 代码如下：

```
printk(KERN_NOTICE "%s", linux_banner);
```

此行产生了上述输出——内核版本字符串，列表 5-3 的第 3 行。该版本字符串包含了与内核镜像相关的多个数据点：

- 内核版本：`Linux 版本 2.6.32-07500-g8bea674`
- 编译内核的用户名/机器名称
- 工具链信息：`gcc 版本 4.2.0`，由 MontaVista 提供
- 构建版本
- 内核镜像编译的日期和时间

## 5.2 初始化控制流

现在你已经理解了内核的结构和组件，让我们检查从引导加载程序到内核的控制流。正如我们在第 2 章“概览”中所讨论的，引导加载程序是位于系统非易失性内存（Flash 或 ROM）中的底层组件。它在通电后立即接管控制权……2.6.32 之后的数字是标记在版本字符串上的；它们对于当前的讨论并不重要。第 4 章 4.1 节解释了这一点。

如前所述，引导加载器镜像有一个主要责任：为解压缩和重定位内核创建适当的环境，并将控制权传递给它。控制从引导加载器直接传递到内核本身，对于大多数架构，传递到一个名为 `head.o` 的模块。引导加载器内核和内核本身都包含一个名为 `head.o` 的模块是一个不幸的历史遗留，因为它是嵌入式 Linux 开发者的困惑来源。引导加载器中的 `head.o` 模块可能被更准确地命名为 `kernel_bootstrap_loader_head.o`，尽管我怀疑内核开发者不会接受这个补丁！事实上，最近的 Linux 2.6 源码树包含
