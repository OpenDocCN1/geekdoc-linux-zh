
# UIO

从 `2.6.23` 版本开始，内核包含一个名为 `UIO`（`用户空间 I/O`）的子系统，它简化了一些用户空间驱动程序的实现。`UIO` 的目的是允许开发用于中断处理等任务的最小化内核驱动程序，并将大多数设备 `I/O` 逻辑推送到用户空间。`UIO` 对于某些类别的工业 `I/O` 卡特别相关。

在 `drivers/uio/` 内部查找 `UIO` 源代码。用户指南位于 `Documentation/DocBook/uio-howto.tmpl` 下。探索 `UIO` 超出了本章的范围。

# 查看源代码

Linux 调度程序位于 `kernel/sched.c`。SCSI 通用实现位于 `drivers/scsi/sg.c`，而 `drivers/usb/core/devio.c` 负责支持用户空间 `USB` 驱动程序。启用用户模式 `I²C` 编程支持的 `i2c-dev` 驱动程序位于 `drivers/i2c/i2c-dev.c`。

表 19.1 包含本章使用的主要数据结构，表 19.2 列出了用于辅助用户模式驱动程序开发的函数。

**表 19.1. 数据结构摘要**

| 数据结构 | 位置 (用户空间) | 描述 |
|---|---|---|
| `sched_param` | `/usr/include/bits/sched.h` | 与调度优先级相关的信息。 |
| `fb_var_screeninfo` | `/usr/include/linux/fb.h` | 用于操作帧缓冲区。包含可变屏幕信息，如分辨率和像素时钟。更多细节请参见第 11 章。 |
| `sg_io_hdr_t` | `/usr/include/scsi/sg.h` | 用于管理 SCSI 通用设备的信息。 |
| `usb_dev_handle` | libusb 软件包中的头文件。 | 用于从用户空间操作 USB 设备的结构。 |
| `usb_bus` | libusb 软件包中的头文件。 | 用于从用户空间操作 USB 设备的结构。 |

**表 19.2. 用户空间函数摘要**

| 用户空间函数 | 描述 |
|---|---|
| `sched_getparam()` | 获取与给定进程相关的调度参数 |
| `sched_setscheduler()` | 设置与给定进程相关的调度参数 |
| `mlockall()` | 将调用进程的页面锁定在内存中，从而避免缺页中断 |
| `ioperm()` | 控制对前 0x3FF 个 I/O 端口的访问权限 |
| `iopl()` | 控制对所有 I/O 端口的访问权限 |
| `outb() / outw() / outl()` | 向指定端口输出字节/字/长整型 |
| `inb() / inw() / inl()` | 从指定端口输入字节/字/长整型 |
| `mmap()` | 将文件或设备地址区域与用户虚拟内存块关联 |
| `msync()` | 刷新对 mmap 内存区域所做的更改 |
| `munmap()` | mmap() 的逆操作 |
| `usb_init()` | libusb 库提供的用于帮助操作 usbfs 的函数 |
| `usb_find_buses()` | libusb 库提供的用于帮助操作 usbfs 的函数 |

| 用户空间函数 | 描述 |
| :--- | :--- |
| `usb_find_devices()` |  |
| `usb_open()` |  |
| `usb_control_msg()` |  |
| `usb_close()` |  |
| `i2c_smbus_read_byte_data()` | 作为 lm-sensors 包的一部分提供的用户空间 I²C/SMBus 数据访问例程 |
| `i2c_smbus_write_word_data()` | 作为 lm-sensors 包的一部分提供的用户空间 I²C/SMBus 数据访问例程 |

# 第 20 章。更多设备与驱动程序

- `ECC` 报告 578
- `频率调节` 583
- `嵌入式控制器` 584
- `ACPI` 585
- `ISA` 和 `MCA` 587
- `火线 (FireWire)` 588
- `智能输入/输出 (IIO)` 589
- `业余无线电` 590
- `IP` 语音 (`VoIP`) 590
- `高速互连` 591

迄今为止，我们为每个主要的设备驱动程序类别都专门编写了完整的一章，但在 `drivers/` 目录下还有几个子目录我们尚未深入探讨。在本章中，让我们以较快的节奏进入其中的一些目录内部。

## ECC 报告

多个内存控制器包含专门用于使用`纠错码` (`ECC`) 测量存储数据完整性的硅芯片。`错误检测与纠正` (`EDAC`) 驱动程序子系统会通告由支持 ECC 的内存控制器生成的内存错误事件的发生。典型的 ECC DRAM 芯片具有纠正`单比特错误` (`SBE`) 和检测`多比特错误` (`MBE`) 的能力。在 EDAC 术语中，前一类错误被称为`可纠正错误` (`CE`)，而后一类则被称为`不可纠正错误` (`UE`)。

ECC 操作对操作系统是透明的。这意味着，如果你的 DRAM 控制器支持 ECC，则错误纠正和检测会悄无声息地进行，无需操作系统参与。EDAC 的任务是报告此类事件，并允许用户制定错误处理策略（例如，更换可疑的 DRAM 芯片）。

EDAC 驱动程序子系统由以下部分组成：

- 一个名为 `edac_mc` 的核心模块，它提供了一组库例程。
- 用于与支持的内存在制控制器交互的独立驱动程序。例如，与 Intel 82860 北桥中内存控制器部分配合工作的驱动程序模块被称为 `i82860_edac`。

EDAC 通过 `sysfs` 目录 `/sys/devices/system/edac/` 中的文件报告错误。它还会生成消息，这些信息可以从内核错误日志中获取。

DRAM 芯片的布局是根据从内存控制器发出的片选数量以及内存控制器与 CPU 之间的数据传输宽度（通道）来指定的。DRAM 芯片阵列中的行数取决于前者，而列数则取决于后者。EDAC 的主要目标之一是指向有问题的 DRAM 芯片，因此 EDAC 的 sysfs 节点结构是根据物理芯片布局设计的：`/sys/devices/system/edac/mcX/csrowY/` 对应于内存控制器 X 中的片选行 Y。每个这样的目录都包含详细信息，例如检测到的 CE 数量 (`ce_count`)、UE 数量 (`ue_count`)、通道位置以及其他属性。

### 设备示例：支持 ECC 的内存控制器

让我们为尚未支持的内存控制器添加 EDAC 支持。假设你正在将 Linux 安装到一个中等档次的嵌入式 x86 衍生设备上。你主板上的北桥芯片组（包括第 12 章“视频驱动程序”中侧边栏“北桥”部分讨论的内存控制器）是支持 ECC 报告的 Intel `855GME`。连接到此系统中 855GME 的所有 DRAM 存储体都是支持 ECC 的芯片，因为这是一个对生命至关重要的设备。EDAC 尚不支持 855GME，所以让我们尝试实现它。

ECC DRAM 控制器有两个主要的与 ECC 相关的寄存器：一个错误状态寄存器和一个错误地址指针寄存器，如表 20.1 所示。当发生 ECC 错误时，前者包含状态（指示错误是 SBE 还是 MBE），而后者包含发生错误的物理地址。EDAC 核心定期检查这些寄存器，并通过 `sysfs` 将结果报告到用户空间。从配置角度来看，855GME 内部的所有设备似乎都位于 PCI 总线 0 上。DRAM 控制器位于该总线的设备 0 上。DRAM 接口控制寄存器（包括特定的 ECC 寄存器）映射到相应的 PCI 配置空间。要为 855GME 添加 EDAC 支持，请添加读取这些寄存器的钩子，如列表 20.1 所示。请参阅第 10 章“外围组件互连”，以了解 PCI 设备驱动程序方法的数据结构说明。

**表 20.1. DRAM 控制器上的 ECC 相关寄存器**

| 寄存器 | 描述 |
| :--- | :--- |
| `I855_ERRSTS_REGISTER` | 错误状态寄存器，指示 ECC 错误的发生。显示错误是 SBE 还是 MBE。 |
| `I855_EAP_REGISTER` | 错误地址指针寄存器，包含最近一次 ECC 错误发生的物理地址。 |

### 列表 20.1. 855GME 的 EDAC 驱动程序

```c

/* Based on drivers/edac/i82860_edac.c */

#define I855_PCI_DEVICE_ID    0x3584  /* PCI Device ID of the memory

                                      controller in the 855 GME */

#define I855_ERRSTS_REGISTER  0x62    /* Error Status Register's offset
```
