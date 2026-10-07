
# 13

### 本章内容

- GUI 开发
- 实时能力
- 嵌入式 Linux 厂商方案
- Project Trailblazer 硬件
- 扩展阅读

## 结语

本书介绍了了许多用于自动化项目的嵌入式 Linux 主题。第 2 章“系统架构”介绍了 Project Trailblazer，并为本书的技术内容奠定了方向。第 3 章“选择平台和安装工具集”、第 4 章“启动 Linux”以及第 5 章“调试”将帮助你构建开发工作空间、GNU 工具链以及跨平台远程调试环境。其余章节将向你展示如何将各种硬件设备连接到 Project Trailblazer 目标板，并使用 Linux 进行数据采集和控制。所有这些信息构成了嵌入式 Linux 的基础，你可以在你的设计中使用这些基础。

本章简要讨论了 GUI 开发、实时能力以及嵌入式 Linux 厂商方案。这些主题并未在 Project Trailblazer 中使用，但对你的设计可能很重要。本章最后以一项讨论结束，总结了 Project Trailblazer 硬件的性能。

## GUI 开发

你的应用程序无疑会包含基于本书基础基础的额外技术。你可能需要使用窗口软件来为机顶盒、销售点系统（POS 系统）、人机界面和图形用户界面开发易用的客户解决方案。

X Window 系统驱动着 Linux 桌面，但不适用于嵌入式设备。它的存储和 CPU 要求超过了大多数嵌入式硬件设计的能力。幸运的是，存在许多解决方案，每种方案都为嵌入式 Linux GUI 开发提供窗口系统¹。如果你的产品需要图形功能，你的设计有多种可选方案（例如：`Microwindows`、`Qt/Embedded`、`GtkFB`、`PicoGUI`、`Micro-X`）。

## 实时能力

自从作为嵌入式操作系统以来，Linux 因缺乏实时能力而受到批评。Linux 及其调度器是为了最大吞吐量而设计的，而不是为了确定性响应。开源内核允许开发者为 Linux 提供实时解决方案。这些解决方案遵循两种方法：

- 你可以将 Linux 作为小型实时操作系统中的一个线程来运行。
- 你可以修改 Linux 调度器并在内核中创建抢占点。

线程方法的支持者声称，对 Linux 内核的任何修改都无法使其具有确定性。调度器和可抢占内核的支持者则认为，得益于今天的高性能处理器，他们的修改完全适用于绝大多数应用。这两种观点都有道理：采用任何一种方法都会增加你设计的复杂性，增加开发时间。采用实时解决方案可能会将你的设计锁定在特定的内核版本上。你在第 11 章“使用中断进行计时”中已经获悉，Linux 内核在所有 Project Trailblazer 目标板上都有良好的平均中断延迟——足以开发出精度为 1ms 的事件定时器。在采用实时解决方案之前，你理应该认真考虑按照第 11 章描述的方法对你的硬件进行基准测试。

窗口和实时解决方案需要硬件与软件之间的交互。这些解决方案并不适用于所有 CPU 架构或图形硬件。在设计的早期，你应该确保为你的硬件存在软件移植版本。请记住，Linux 开发者无疑（有时是激烈地）有自己的独特见解，特别是当这些见解涉及个人、技术或业务性质时。如果你的设计需要窗口功能或实时能力，你应该彻底研究并调查软件和硬件的所有选项。许多窗口和实时解决方案都有许可要求，这可能会影响你的决策和设计的成本。

## 嵌入式 Linux 厂商方案

对 Linux 的另一个批评是它缺乏支持结构。然而，商业 Linux 发行版厂商确实为桌面、服务器以及现在的嵌入式系统提供支持。有四种主要的商业嵌入式 Linux 厂商：

| 行 | URL |
| :--- | :--- |
| Lineo | www.lineo.com |
| LynuxWorks | www.lynuxworks.com |
| MontaVista Software | www.mvista.com |
| Red Hat | www.redhat.com/embedded |

这些厂商很快指出，他们提供基于 Linux 的产品——他们不仅仅是包装和支持组织。事实确实如此。这些厂商提供的基础产品是一个嵌入式 Linux 工具包，其至少能够配置和编译内核、配置和构建根文件系统，并提供文档。

> 注意
> Jerry Epplin 在 www.linuxdevices.com 上评审了这四个厂商的工具包。

这种嵌入式 Linux 工具包运行在主机计算机上（通常是 Red Hat 机器），机器可以是 x86、ARM、PowerPC、MIPS、SuperH 和 XScale。这些厂商提供其嵌入式 Linux 工具包的免费下载或评估版本。他们的业务模式基于基础工具包，以提供扩展其工具包能力的产品（例如，MontaVista 的 Library Optimizer 或 Lineo 的 GPL Compliance Toolset）。除了工具包和额外产品外，每家厂商还提供设计、咨询和工程服务。

从上看，这些厂商的方案可能看起来是完全相同的。然而，通过交流或使用他们的免费或评估工具包，你将了解到它们的独特之处。如果你担心厂商对你产品设计的协助，可以访问网站并致电厂商。如果你有时间，可以参加嵌入式系统会议并与厂商面谈；这将让你遇到每个机构内的许多人，并允许你与公司工程师详细讨论你的设计。在会议上，你经常可以遇到负责你设计所依赖代码的开发者。如果厂商能跟进你的需求，你可能会获得更好的服务。

## Project Trailblazer 硬件

书中使用的硬件经过仔细挑选，以最大化示例的影响力。拥有三种架构让你接触到它们的相似之处和不同。你应该意识到，嵌入式世界并不是 x86 世界。Project Trailazer 的接口硬件是从常见的芯片和设备中选择的。

在大多数情况下，Project Trailazer 的硬件性能都符合预期。在处理硬件设计时，有时会遇到产品的问题。重要的是是否存在问题，而不是解决问题的速度有多快。Brightstar Engineering、Embedded Planet、Silicon Storage Technology 和 Tri-M Systems 为本书提供了卓越的硬件支持。

x86 单板机的一个关键卖点是它们与桌面电脑的二进制兼容性。你应该能够在桌面上开发应用程序，将其复制到目标板，然后完成。本书的示例表明，使用 MediaEngine 和 RPX-CLLF 就像使用 MZ04 一样简单。一旦你配置了编译或交叉编译，二进制兼容性就不是障碍。

除了二进制兼容性，桌面与嵌入式硬件之间的相对速度差异可能会对目标板性能产生误导。你可能在桌面上开发一个应用程序，结果发现它在目标板上的性能并不理想。此外，如果你在为嵌入式设计开发硬件接口，在桌面上开发可能会引入额外的复杂性。许多单板计算机实现了 PC104 规格或其他板和物理标准。你的桌面机有 PCI 插槽和许多 ISA 插槽，但显然没有 PC104 接口。

对于非 x86 板板而言，MediaEngine 和 RPX-CLLF 通过其 StrongARM 和 PowerPC 处理器具有优秀的设计和能力。MediaEngine 和 RPX-CLLF 都包含引导加载程序代码和一组诊断工具。这些工具允许你配置启动选项、编写板载 Flash 存储器以及检查处理器寄存器和内存。这些诊断工具对于调试硬件设计来说非常宝贵。它们允许你配置 CPU 寄存器，从而在不启动操作系统的情况下测试硬件。

## 扩展阅读 403

大多数连接 MediaEngine 或 RPX-CLLF 的 Project Trailblazer 硬件都是使用此功能进行调试的。这些目标板还提供了 CPU 总线的接口连接器。StrongARM 1110 和 PowerPC MPC860 处理器包含多种板载外设，允许在不需要额外外部控制器的情况下进行外部接口。您的设计可能需要通用串行总线、内部集成电路（I2C）通信、串行外接口（SPI）或内存映射输入输出。ARM 或 PowerPC 处理器可能刚好包含您的设计所需的外设。这将减少您的设计时间、部件数量、物理尺寸和成本，同时提高可靠性。内核版本的可用性是选择 ARM 或 PowerPC 解决方案的一个缺点。ARM 和 PowerPC 内核需要开发时间。这些处理器的补丁发布通常落后于内核。

### 总结

世界渴望智能的、联网的设备。这种渴望只会增加，这些设备将以我们无法想象的方式渗透到生活中。处理器和内存的进步使开发者能够专注于应用程序，而不是底层技术。强大的硬件不仅随处可见而且价格廉廉。这种组合让 Linux 进入了嵌入式世界。它带来了可靠性、功能、开源代码和经过验证的记录。

你现在拥有了构建未来所需的工具、开发环境、硬件示例和知识。不再受技术的束缚，你可以运用想象力、创造力和专业知识来创造出非凡的产品。你的设计可以也将为世界提供动力。

### 扩展阅读

- Rick Lehrbaum, “嵌入式 Linux GUI/窗口快速参考指南，”www.linuxdevices.com/articles/AT9202043619.html.
- Rick Lehrbaum, “实时 Linux 软件快速参考指南，”www.linuxdevices.com/articles/AT8073314981.html.
- Jerry Epplin, “开发者对领先嵌入式 Linux 工具包的评审，”www.linuxdevices.com/articles/AT8402180338.html.

## 索引

### A

- 账户设置 accounts, setting, 31
- 激活分区 activating partitions, 28
- 应用程序（系统集成） applications (system integration), 369-373
- Apt (Debian 软件包系统), 31-32
- 架构（系统）architect (system), 13-19
- 异步串行通信 asynchronous serial communications
  - bash 脚本, 153, 158
  - 读取 reading, 148, 151-152
  - 设置 setting, 144, 147-148
- 认证 authentications, 18

### B

- 基础系统配置 base systems, configuring, 30
- bash (Bourne Again Shell), 66, 69-71, 100
  - 二进制文件 binary files, 72-73
- 板（目标）boards (target), 66-67
- 启动过程（Linux）boot process (Linux), 67-68
- 启动 booting
  - COTS PC, 109
  - Flash IDE, 109
  - MediaEngine (Brightstar Engineering), 102-105
  - RPX-CLLF (Embedded Planet), 95-99
  - tbdev 工作站, 26
  - Tri-M MZ104, 109, 114-116
  - Flash IDE, 109
  - liftmon_snowcon, 201-204
- 开源代码 open-source codes, 23
- 视频帧采集 video frame grabbers, 217-219
- 计算机板网站 Computer Boards Web site, 162
- Bourne Again Shell. 参见 bash
- 构建目录（根文件系统）build directory (root filesystem), 89
- buildrootfilesystem
  - 配置
    - Apt (Debian 软件包系统), 31-32
    - 基础系统, 30
    - 内核 (版本 2.4.10), 209-211
    - 内核 (USB)
  - 在 Compact Flash IDE 设备上构建, 113
  - 复制所需程序, 90
  - 创建
    - /dev 目录中的设备 devices, 91
    - 发行版 distries, 89
    - 额外的配置文件, 91
    - PACKAGES, 90
    - 准备运行, 91-93
  - 根文件系统 root filesystems
    - 运行, 89
    - 去除调试信息, 90-91
  - 网站 Web sites, 73
  - 内存存储 memory storage, 221-228
  - minicom 串口 minicom serial ports, 95
  - NFS 服务器 NFS servers, 131-132
  - 目标内核 target kernels, 133-136
  - 键盘 keyboards, 28
  - 网络 networks, 29-30

### C

- 摄像头 (USB) cameras (USB). 参见 数字数相机 (USB)
- 读器 (USB) card readers (USB), 222-224
- 卡（以太网）cards (Ethernet), 29
- 代码（开源）codes (open-source), 23
- 编译 compiling
  - 控制 control
    - 寄存器 registers, 164
  - 信号 signals
    - 串口 serial port, 153, 158
    - 读取 reading, 148, 151-152
    - 设置 setting, 144, 147-148
  - helloworld_proc_module, 184-186
  - 内核 (版本 2.4.10) kernel (version 2.4.10), 209-211
  - COTS PC 启动, 109
  - Flash IDE, 109-111
  - 驱动 drivers
    - 编译 compiling, 112
    - RPX-CLLF (Embedded Planet), 252-257, 261-262, 274
    - 内存映射 I/O (输入/输出) memory-mapped I/O (input/output), 228
    - 创建根文件系统 creating root filesystem
      - 配置文件, 91
      - 设备, 91
      - 目录, 86, 89
      - 设备驱动 device drivers
        - 开发 developing, 176-178
        - helloworld_proc_module, 179, 184
        - liftmon_snowcon, 188, 201-204
    - MediaEngine (Brightstar Engineering), 233-238-239
    - RPX-CLLF (Embedded Planet), 257
    - 写入 writing, 239, 252, 274
  - 交叉编译编译器 (GNU 工具链) cross-compilers (GNU tool chain), 33-35, 38, 41, 44-47, 50, 53-63
    - 自定义设备驱动 custom device drivers
      - 开发 developing, 176-178
      - helloworld_proc_module, 179, 184
      - liftmon_snowcon, 188, 201-204
    - MediaEngine (Brightstar Engineering), 233-238-239, 252, 256

### D

- 数据库 databases, 创建/测试, 373, 377
- 日期 dates, 321
- Debian 网站, 25
- Debian Linux 网站, 72, 86
- 调试 (gdb) debugging (gdb), 121
  - 本地 local, 122-126
  - 远程 remote, 131
- 数字相机 (USB) digital cameras (USB), 214-219
- 目录（根文件系统）directories (root filesystem), 89-91
- 磁盘（硬盘）disks (hard), partitioning 27
- 显示（状态）displays (status), 系统计时, 350, 363
- 下载内核 (版本 2.4.10) downloading kernel (version 2.4.10), 209-211
- MP3 解码程序 MP3 decoder programs, 213
- 视频帧采集 video frame grabbers, 217-219
- do_gettimeofday, 322
- 驱动（设备）drivers (device)
  - helloworld_proc_module, 178-179, 184-186
- I2C 通信, 298
- I2C SAA1064 (飞浦半导体) LED 显示, 278
- 中断延迟媒体设备 interrupt_latency_mediaengine device, 338
- liftmon_snowcon, 188, 201-204
- 解码程序 (MP3) decoder programs (MP3), 213
- 设计外部接口 designing external interface
  - MediaEngine (Brightstar Engineering), 229-233, 238-239, 252, 256

### F

- MediaEngine (Brightstar Engineering), 233, 238-239, 252, 305-307, 317
- file 命令 file, 90
- RPX-CLLF (Embedded Planet), 257, 261-262, 274
- 文件 files
  - bash (Bourne Again Shell), 70-71
  - 二进制 binary, 68-73
  - 驱动器 drives, 分, 110-111
  - 网站 sites, 109
- SAA1064 设备, 305
- Flash IDE, x86 并行打印口, 299-301, 305-307, 317

### E

- ELC (嵌入式 Linux 联盟) 网站 ELC (Embedded Linux Consortium) Web site, 21

### G

- ELJ (嵌入式 Linux 日志) 网站 ELJ (Embedded Linux Journal) Web site, 22
- Embedded Planet RPX-CLLF. 参见 RPX-CLLF
- 以太网卡 Ethernet cards, 29
- gdb, 121
- getSerialprogram, 148, 151-152
- get_cycles, 322
- GNU 工具链 GNU tool chain, 33-35, 38, 41, 44-47, 50, 53-63
- GPL (通用公共许可证) GPL (General Public License), 10-11
- Grayhill 网站, 165
- 客户操作需求 (Project Trailblazer) guests operation requirements (Project Trailblazer), 18
- GUI (图形用户界面) GUI (graphical user interfaces), 399
- 事件计时 event timing
  - 日期 dates, 321
  - do_gettimeofday, 322
  - get_cycles, 322
  - jiffies, 321
- PSRs (处理器特定寄存器) PSRs (processor-specific registers), 322
- 外部接口硬件 external interface hardware
  - 设备驱动 device drivers, 233, 238-239, 252, 257, 261-262, 274
  - I/O (输入/输出) 端口, 233

### H

- MediaEngine (Brightstar Engineering), 229-230
- 硬盘 disks, 27
- 内存控制器 memory controller, 232, 255
- 内存映射空间 memory map space, 253-254
- 内存映射硬件 memory-mapped hardware, 228
- MediaEngine (Brightstar Engineering), 233
- RPX-CLLF (Embedded Planet), 257
- 输出模块 output module, 233
- 实时解决方案 real-time solutions, 400
- 寄存器地址 register address, 232, 255
- RPX-CLLF (Embedded Planet), 252

## HOWTOs

- GNU 工具链网站, 34
- 用于 PowerPC 的嵌入式 Linux 网站, 34

### I

- I/O (输入/输出)
- I2C 通信, 298
- I2C SAA1064 (飞浦半导体) LED 显示, 278
- 中断延迟媒体设备 interrupt_latency_mediaengine device, 338
- liftmon_snowcon, 188, 201-204
- 解码程序 (MP3), 213
- 设计外部接口 designing external interface
  - MediaEngine (Brightstar Engineering), 229-233, 238-239, 252, 256
- i386 内核, 112
- 初始化 init, 67-69
- helloworld_proc_module, 179, 184-186
- 插入 GNU 工具链 inserting GNU tool chain, 33-35, 38, 41, 44-47, 50, 53-63
- 集成数据库 integrating databases
  - 创建/测试, 373, 377
  - 开发集成脚本 developing integration scripts, 378
- 安装应用程序 installing applications, 369-373
- RFID (无线频率识别), 392-396
- 收集/分数据, 378-381, 385
- 收集/分图像数据, 385-386, 390-392
- 开发, 378
- RFID (无线频率识别), 392-396
- 系统, 367

410

接口
- 为 RPX-CLLF (Embedded Planet) 设计, 252-253
- 目标 (target), 133-136
- 寻找内存映射空间, 232, 253-254
- 版本 2.4.10, 209-211
- 视频, 209, 215
- 寻找寄存器基地址, 232, 245
- 编写设备驱动, 239, 252, 262, 274
- 内核与模块 (Linux操作系统), 安装, 28-29
- 编写测试设备驱动, 233, 238-239, 257, 261-262
- 键盘, 28

# L
- OHCI (开放主机控制器接口), 207
- 布局 (PBRs), 66-69
- 同步串行通信, 277
- LGPL (库通用公共许可证), 11
- UHCI (通用主机控制器接口), 207
- 许可证
  - GPL (通用公共许可证) get, 10-11
  - LGPL (库通用公共许可证), 11
- 中断延迟
  - 测量, 323-324, 346
- MediaEngine (Brightstar Engineering), 331, 338-339
- liftmon_snowcon, 201-204
- MZ104, 325, 330
- Lineo 网站, 401
- RPX-CLLF (Embedded Planet), 339, 345
- Linux
  - interrupt_latency_mediaengine 设备驱动, 338
  - 设备网站, 22
  - 操作系统
    - 安装, 26
    - 内核与模块, 安装, 28-29
  - PowerPC 嵌入式系统网站, 34
  - jiffies, 321
  - Journeyman (MontaVista), 72, 87
  - 工具包

# 内核
  - 二进制文件, 72-73
  - 启动过程, 67-68
  - 编译, 88
  - i386, 112
  - 创建, 86
  - 内存存储 (USB), 221-222
  - 网络挂载, 178
  - 根文件系统, 68-71
  - MontaVista 软件网站
- NFS 服务器配置, 131-132
- 根文件系统, 68-69, 71
- 目标内核配置, 133-136
- 网站, 401
- 配置配置 I/O (输入/输出) 端口
  - 控制器, 233
  - 配置内存控制器, 232, 256
  - 设计, 229-230
  - 寻找内存映射空间, 232
  - 寻找寄存器基地址, 232
  - 编写设备驱动, 233, 238-299, 252
- LM70 SPI (美国半导体公司) 数字温度传感器, 278
- SPI 通信, 279
- 连接到 MediaEngine (Brightstar Engineering), 289, 297
- 连接到 x86 打印机端口, 280, 288
- 本地调试, 122-126
- LinuxWorks 网站, 401
- helloworld_proc_module, 184-186
- 中断延迟, 测量, 331, 338-339
- LM70 SPI (美国半导体公司) 数字温度传感器, 289, 297
- 内存控制器, 232, 256
- PBRs (平台启动需求), 106-108

# M
- 手页, 44
- 映射 (内存)
  - 为 MediaEngine (Brightstar Engineering) 寻找空间, 232
  - 为 RPX-CLL (Embedded Planet) 寻找空间, 253-254
- 测量
  - 中断延迟, 323-324, 346
  - MediaEngine (Brightstar Engineering), 331, 338-339
  - MZ104, 325, 330
  - RPX-CLL (Embedded Planet), 339, 345
- 内存
  - 读读器 (USB), 222-224
  - 控制器
    - MediaEngine (Brightstar Engineering), 232, 256
    - RPX-CLL (Embedded Planet), 255
    - 内核 (USB), 221-222
  - 映射
    - MediaEngine (Brightstar Engineering), 232
    - RPX-CLL (Embedded Planet), 253-254
- MediaEngine (Brightstar Engineering) 启动, 102, 104-105
- 外部接口硬件
  - 分配输出模块启用信号, 233
- 内存映射 I/O (输入/输出) 硬件, 228
- minicom, 配置, 228
- MontaVista 网站, 401
- 挂载 USB 读卡器, 222-224
- 挂载 MP3 解码器, 213
- MZ104, 325, 330
- MediaEngine (Brightstar Engineering) 启用信号, 233
- RPX-CLL (Embedded Planet), 257
- 输出模块 (output), 228
# N
- National Semiconductor (美国半导体)网站, 278
- 网络配置, 279
- 根文件系统挂载, 68-71
- NFS 服务器, 131-132
- 目标内核配置, 133-136

# P
- 软件包
  - 下载, 90
  - 提取, 90
  - 端口
    - I/O (输入/输出) 端口, 166, 172
    - 并行端口, 173
    - I2C SAE164 (美国半导体) 显示, 299, 301, 305, 317
    - LM70 SPI (美国半导体) 数字温度传感器, 280, 288
    - RPX-CLLF (Embedded Planet) 启动, 95-99
    - PBRs (平台启动需求), 100-102
- 点对点 (Point-to-Point), PPP
- Project Trailazer
  - 数据库, 37
  - 设计, 29-30
  - 测试, 37
  - 查看 PBRs (平台启动需求), 66-67
  - 查看 MediaEngine (Brightstar Engineering), 102, 104-105
  - 查看 RPX-CLLF (Embedded Planet), 257
  - 查看 PBRs (平台启动需求), 106-108
  - I/O (输入/输出) 端口, 163, 170
  - 根文件系统, 71
  - 安全性, 17
  - 硬件, 19
  - 串口 (minicom) 配置, 95
  - 单源, 19
  - tb 工作站, 24-25
  - x86 打印机端口, 18

# Project Trailazer
- tb 工作站内存存储, 220
- 激活分区, 28
- 启动, 26
- 编译 GNU 工具链用于交叉编译, 33-35, 38, 44-47, 50-63
- 配置 Apt (Debian 软件包系统), 32
- 配置内核, 28-29
- 内核与模块, 安装, 28-29
- 直接从 31 启动
- MediaEngine (Brightstar Engineering), 232
- 内存映射 I/O (输入/输出) 硬件, 228
- 内存控制器, 232, 256
- 内存存储 (USB), 221-222
- 根文件系统, 68-71
- 目标内核配置, 133-136
- 版本 2.4.10, 209-211
- 视频, 209, 215
- 寻找寄存器基地址, 232, 245
- 寻找内存映射空间, 232, 253-254
- 编写设备驱动, 239, 252, 262, 274
- 编写测试设备驱动, 233, 238-239, 257, 261-262

# Q
- 查询, 145
# R
- RPX-CLLF (Embedded Planet), 339, 345
- 根文件系统, 68-69, 71
# S
- 串行通信
  - 异步, 144
  - bash 脚本, 153, 158
  - 串口控制信号
    - 读取, 148, 151-152
    - 设置, 144, 147-148





# 串口控制信号

串口控制信号，153, 158

- 文件打开系统调用，152
- 读取，148, 151-152
- 设置，144, 147-148
- 串口 (minicom), 95
- 服务器
  - NFS, 131-132
  - TFTP (简单文件传输协议), 93-94
- setSerialSignal 程序，144, 147-148
- 设置
  - 软件（开源），10
- 声器，连接，211-213
- SPI 通信
  - LM70 SPI (美国国家半导体), 279
  - MediaEngine (Brightstar Engineering)，连接到，289, 297
  - x86 并行打印口，连接到，280, 288
- SPP (标准并行口)，163
- 控制寄存器，166
- 自定义设备驱动程序，187
- I/O (输入/输出)端口，166, 172
- ppdev，173, 176
- 状态显示（系统计时器），350, 360-363

# 存储

- 读卡器，222-222
- 内核，221-222
- 内存 (USB)，220
- 供应商需求 (Project Trailblazer)，19
- 同步串口通信接口，277

- 系统架构，13
  - Project Trailblazer，14-16, 19
  - 操作需求，18-19
  - 安全需求，17
  - 供应商需求，19
- 系统
  - 设计 (Project Trailblazer)
    - 硬件，23
    - 研究，21
    - 策略，22-23
  - 系统架构，13-19
  - 工作站，24-35, 38, 41-44, 50, 53-63
  - 集成，367
  - 应用，安装，369-377
  - 数据库，创建/测试，373, 377
  - 集成脚本，收集/发布数据，378-381, 385
  - 集成脚本，收集/发布图像数据，385-396, 390-392
  - RFID (射频识别)，392-396
- TFTP 服务器 417

# 计时器

- 硬盘，分区，27
- 实现，347-348
- 键盘，配置，28
- 中断处理，349
- Linux 操作系统内核和模块
  - 任务队列 (tasklets)，349
  - 安装，28-29
  - 状态显示，350, 360-363
  - 直接从硬盘使 Linux 可可启动，31

# 系统（基础）

- 网络，配置，29-30
- 配置，30
- 分区
  - 嵌入式，8
  - 激活，28
  - 设置账户，31
  - 设置密码，31
  - 设置 PPP (点对点协议)，31

# T

- tar 命令，90
- 目标板
  - 启动过程 (Linux)，67-68
  - 温度信息安全需求 (Project Trailblazer)，17
- 温度传感器
  - PBRs (平台启动需求)，66-67
  - LM70 SPI (美国国家半导体)数字型，278
- 根文件系统，91-93
- 目标
  - SPI 通信，279
  - 内核，配置，133-136
  - MediaEngine (Brightstar Engineering)，连接到，289, 297
  - 平台 (PBRs)，66-67
  - x86 并行打印口，连接到，280, 288
  - 任务队列 (tasklets)，349
- 测试
- tbdev 工作站
- 数据库
- 基础系统
  - Project Trailblazer，373, 377
  - 启动，26
  - helloworld_proc_module，184-186
  - 配置，30-32
  - liftmon_snowcon，201-204
  - 创建，25
  - 读卡器 (USB)，223-224
  - 安装 Linux 操作系统，26
  - 德州仪器 (Texas Instruments) 网站，166
- GNU 工具链
  - 交叉编译，33-35, 38, 41, 44-47, 50, 53, 55-63
  - TFTP (简单文件传输协议) 服务器，安装，93-94
  - 安装，33

# 计时器（系统）

- 实现，347-348
- 中断处理，349
- 状态显示，350, 360-363

# 计时，321

- 日期，321
  - do_gettimeday，322
  - get_cycles，322
  - jiffies，321
  - PSRs (处理器特定寄存器)，322
  - races (竞态)
  - Project Trailblazer 操作需求，18

# 工具包 (Linux) 网站，401

- 跟踪 (Project Trailblazer 操作需求)，18

# Tri-M

- 启动，109, 114-116
- Flash IDE，109-111
- i386 内核，112
- PBRs (平台启动需求)审查，116, 118
- 准备，109-110

# U

- UHCI (通用主机接口)，207
- USB (通用总线)，206
- 读卡器，222
- 连接，222
- 挂载，223-224
- 测试，223-224
- 数字摄像头，214
- 连接，216-217
- 配置，215
- 视频抓取器编译，217-219
- 硬件 (Project Trailblazer)，208
- 音频，208
- 内存，220
- 配置，222-222
- MP3 解码器下载，213
- 声器，连接，211, 213
- UHCI (通用主机接口)，207
- 网站，207
- 变量，设置 (PACKAGES)，89
- 视频抓取器编译，217-219
- 下载，217-219
- 内核，配置，215
- USB (通用总线) 数字摄像头
- 视觉信息安全需求 (Project Trailblazer)，17

# x86 并行打印口

# W-Z 网站

- buildroot，73
- 电脑板，162
- Debian，25
- Debian Linux，72
- ELC (嵌入式 Linux 联盟)，21
- ELJ (嵌入式 Linux 杂志)，22
- Flash IDE，109
- GNU 工具链，34
- Grayhill，165
- Journeyman (MontaVista)，72
- 内核，209
- Lineo，401
- Linux 设备，22
- PowerPC 嵌入式系统 Linux，34
- LinuxWorks，401
- MontaVista 软件，401
- 美国国家半导体，278-279
- 并行口，163
- 飞利浦半导体，278
- Red Hat，401
- 德州仪器，166
- 工具包 (Linux)，401
- USB (通用总线)，207
- 窗口，400
- 工作站
  - 启动
    - Project Trailblazer，26
    - 以太网卡，29
    - tbdev，24-26
x86 并行打印口

  - I2C SAA1064 (飞利浦半导体)
  - LED 显示驱动，连接到，299-301, 305-307, 317
  - LM70 SPI (美国国家半导体) 数字温度传感器，连接到，280, 288

# 嘿，你已经够烦恼了。
不要让 IT 培训成为其中。

![](img/c075000fa5feb4594b144d501c7cd8_433_0.png)

通过您的信息技术网络 InformIT 开启 IT 培训的快速通道。

| InformIT | www.informit.com | SAMS |
| :--- | :--- | :--- |
| | 关于数十个主题的数百篇及时文章 - 来自我们所有出版伙伴（包括 Sams Publishing）的 IT 书籍折扣 - InformIT 免费库的免费完整书籍 - “专家问答”——与 IT 专家的在线聊天 - 通过我们的网络或课堂培训课程获得更快速、更方便的认证和培训 - 当前 IT 新闻 - 软件下载 - 职业发展提升资源 | |

InformIT 是 Pearson 的注册商标。Copyright ©2001 by Pearson. Copyright ©2001 by Sams Publishing.

# Linux, 硬件, 设备驱动程序

# 嵌入式 Linux 硬件、软件与接口
Craig Hollabaugh, Ph.D.

嵌入式 Linux 涵盖了嵌入式 Linux 平台上接口应用的开发和实现。它包含了对平台选择、交叉编译、内核编译、根文件系统创建、启动、远程调试、现实接口、应用控制、数据收集、存档和演示的全面讨论。

本书包含了使用 x86-、StrongARM® 和 PowerPC® 目标的串口、并行、内存 I/O、USB 和中断驱动的硬件设计。此外，你还将找到将外部设备连接到内核的简单设备驱动代码以及将嵌入式 Linux 字段连接到中央控制中心的集成代码。示例了硬件开发者如何使用开源软件存储和激活字段并交付进程信息。如果你是硬件开发人员、软件开发者、系统集成商或开始探索 Linux 应用的产品经理，这本书正适合你。

- 选择嵌入式 Linux 平台（涵盖了提及的架构）
- 创建交叉编译和调试环境
- 为每个架构构建自定义内核
- 创建根文件系统
- 在 x86、SA110 和 MPC860 微处理器板上启动 Linux 内核
- 通过以太网使用 GNU 工具在目标板上远程调试程序
- 使用微处理器的串口、并行、内存 I/O 和 USB 接口连接数据采集和控制电子
- 测量 x86、SA110 和 MPC860 微处理器的中断延迟，并设计 1ms 精度的中断驱动进程计时器
- 使用设备驱动模块将外围接口到内核和应用程序
- 分析嵌入式 Linux 产品提供

Craig Hollabaugh, Ph.D. 在佐治亚理工学院攻读电气工程博士期间，首次管理 Sun® 和 Digital® 工作站。他的第一个嵌入式设计（美国专利 5,222,027）远程监控一个石油处理器。1995 年，在 Wireless Scientific® 开始使用 Linux 进行工业控制。Craig 目前在科罗拉多州的家中为三家公司服务。他为 Antec 开发了 Proteus Scalar Node™。在 Clifton, Weiss and Associates，他是一个运营商级电信网络设计团队的成员。他还在为 Arriva® 设计 FM、MP3 和蓝牙™ 耳机电子设备。

![](img/c075000fa5feb4594b142d501c7cd8_435_0.png)
