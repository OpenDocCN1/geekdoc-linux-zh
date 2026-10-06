
Baboon IC 的地址解码部分为 IC 的 IDE 控制部分提供地址解码。它还为 TREX 定制 IC 提供片选解码，并为两个 PCMCIA 插槽提供地址解码。

## Bandit

Bandit 定制 PCI 桥 IC 是 PCI 总线与主处理器及内存子系统之间的接口。Bandit IC 在处理器总线和 PCI 总线之间提供缓冲和地址转换。Bandit IC 支持双向长度长达 32 字节的突发传输——即一个缓存块的大小。

独立的逻辑设备（门阵列）按如下方式提供总线仲裁优先级：
- 1. Grand Central IC（I/O 设备控制器）；优先级最高
- 2. PCI 插槽和 Bandit 主设备，采用轮询顺序：即每个轮流执行，优先级相等

PCI 扩展槽直接连接到 PCI 总线。

## BART

BART 定制 NuBus 控制器芯片提供了 NuBus 与 CPU 总线之间的数据网关。它充当 CPU 总线主设备，传输单周期或四周期的事务。它符合 IEEE 1196 标准。

## Chaos

Chaos 定制 IC 在视频系统与处理器总线之间提供数据总线缓冲。

## CIVIC

Cyclone集成视频接口控制器 (CIVIC) 用于 AV 卡，是一种采用 144 引封装的定制 CMOS 芯片。CIVIC
- 管理从 1 MB 到 4 MB 的视频随机存储器 (VRAM)
- 控制 VRAM 与 SAA7194 芯片之间、以及 VRAM 与 Sebastian 视频调色板芯片之间的数据传输
- 在 VRAM 与主处理器之间提供 32 位或 64 位数据路径；支持所有传输模式下来自主处理器的数据突发
- 控制用于行交织显示的图形数据进行卷积处理
- 提供 NTSC 和 PAL 时序信号
- 生成垂直消隐和视频输入中断信号

## Combo

Combo 定制 IC 结合了 SCC IC (85C30 串行通信控制器) 和 SCSI 控制器 IC (53C80) 的功能。SCC 部分支持串行 I/O 端口。SCSI 部分支持内部 SCSI 硬盘；对于旧版 PowerBook Duo 机型的升级需要它。

## Control

Control 定制 IC 为视频子系统提供寻址和控制。

## CSC

CSC (色彩支持芯片) 定制 IC 是一种显示控制器，为 LCD 面提供数据和控制接口。它包含一个 256 颜色查找表 (CLUT)、RAMDAC、显示缓冲区控制器和平面面板控制电路。

## Cuda

Cuda IC 是摩托罗 MC68HC05 微控制器的定制版本。它提供了若干系统功能，包括
- 管理 Apple 桌面总线 (ADB)
- 系统重置
- 参数 RAM 管理
- 实时时钟管理
- 电源控制
- 来自 GeoPort 端口的 IIC 总线
- 在 IIC 总线上的设备支持主处理器的数据突发传输
- 在 IIC 总线上的设备包括 AWACS 音频 IC
- 数字解码器
- 视频输入 (DESC)

## Curio

Curio 是一个定制多功能 I/O 芯片，包含以太网访问控制器 (MACE)、SCSI 控制器和 串行通信控制器 (SCC)。Curio 的 SCC 部分包含用于发送和接收数据流的 8 字节 FIFO 缓冲区。Curio 支持其 I/O 端口与主内存之间的 DMA 传输。

## ECSC

ECSC (增强色彩支持芯片) 是一种定制显示器 IC，为 LCD面板提供数据和控制接口。ECSC 与 PowerBook 520 和 540 使用的 CSC 类似，但它可以寻址 1 MB 的视频内存。ECSC 包含 RAMDAC、显示缓冲区控制器和平面电路。

## Grand Central

Grand Central I/O 系统提供了标准 I/O 设备与 PCI 总线之间的接口。Grand Central IC 执行以下操作：
- 支持 Cuda IC (VIA 寄存器)
- 中央系统中断
- I/O 设备的描述符 DMA
- 软盘接口 (SWIM III)

Grand Central IC 中的 SWIM III 软盘控制器是早期 Macintosh 型设计的扩展。SWIM III 控制器支持 DMA 传输，且访问软磁盘时不需要禁用中断。

Grand Central IC 为以下 I/O 设备提供总线接口：
- Cuda 微控制器
- AWACS 音频输出 IC
- Curio 多功能 I/O IC
- 快速 SCSI 设备的 控制器

Grand Central IC 还为其他设备提供一条 16 位总线，包括非易失参数 RAM 和 Sixty6 IC。Grand Central IC 连接到 PCI 总线并使用 33 MHz 总线时钟。

## Hammerhead

Hammerhead 定制内存控制器 IC 控制内存和缓存子系统，系统总线、主内存（128 位 DRAM 阵列）、ROM 和 L2 缓存。内存提供了低延迟访问和更高的带宽。Hammerhead IC 支持高达 2 GB 的内存容量。Hammerhead IC 的组件有
- 系统总线控制器
- DRAM 控制器
- ROM 控制器
- 二级 (L2) 缓存控制器

**数据交错**：尽管系统总线仅 64 位宽，但 Hammerhead IC 中的内存控制器通过交错两个 DIMM 槽的数据来支持 128 位的数据读取操作。当启动软件检测到相邻存储体（Bank 0-Bank 1）具有相同的两个 DIMM 时，会启用这对 DIMM 的交错。对于交错传输，内存控制器同时将两个存储体的数据循环到 128 位缓冲区中，每次传输 64 位到系统数据总线。内存控制器根据携带关键字优先行为的地址信号决定先传输哪个存储体的数据。控制器支持 PowerPC 601 的关键四字优先行为以及 PowerPC 603 和 PowerPC 604 的关键双字优先行为。

250 MkLinux: 用于 Power Macintosh 的微内核 Linux

**库基寄存器（Bank Base Registers）。** Overhead IC 为每个主内存 库包含一个库基寄存器。每个库基寄存器都有存储基地址和控制位的空间。控制位设置地址复用模式并启用或禁用数据总线交织。

库基地址用于使内存库变得连续。系统软件根据每个 SIMM 中内存的大小来计算基地址。每个库的基地址基于所有编号较小的库的大小之和。

## HMC

高速内存控制器 (HMC) 是一块定制芯片，用于控制 Power Macintosh 计算机所有内存操作。HMC 具有以下特性，以支持与 PowerPC 601 处理器之间的数据传输：
- 支持所有基本传输协议，包括所有单周期访问
- 支持四周期 32 字节缓存访问
- 将未对齐的读操作转换为双字字读操作
- 实现仅限地址的事务
- 总线仲裁（仅限地址总线）

HMC 不支持以下功能：
- 内存总线事务的流水线
- 缓存嗅探（cache snooping）
- 从传输错误确认信号中恢复
- 小端传输模式

## Iridium

Iridium 定制 IC 与 Platinum 内存控制器 IC 配合工作，优化 ROM、DRAM 和 VRAM 数据事务期间的数据吞吐量。它还与 Platinum IC 配合以加速某些 QuickDraw 显示操作。

## 第 17 章：Power Mac 系统

## Keystone

Keystone 视频控制器定制 IC 包含外部视频电路的时序控制电路。Keystone IC 具有内部寄存器，视频驱动程序使用这些寄存器设置水平和垂直计时参数。Keystone IC 还为 VRAM 生成视频刷新地址。

## MESH

MESH 定制高速 SCSI 接口 IC 控制内部 SCSI 设备的 SCSI 总线。由于该总线不需要驱动长外部总线，因此其传输速率比外部 SCSI 总线更高。内部 SCSI 总线支持每秒 10 MB 的传输；外部 SCSI 总线的工作速度为每秒 5 MB。

## Mickey

Mickey 是一个 28 引脚高级双极性 CMOS 芯片中的复合视频编码器。用于 AV 卡。Mickey
- 接受来自 Sebastian 视频调色板芯片的模拟 RGB 视频信号
- 编码为 NTSC 或 PAL 格式
- 输出 S-video、复合或 RGB 视频输出

## O'Hare

O'Hare 定制 IC 基于 Power Macintosh 7500 计算机中的 Grand Central IC。它是使用 PCI 总线架构的 Power Macintosh 计算机的 I/O 控制器和 DMA 引擎。它为 Power Macintosh 5400 计算机中包含的符合 Energy Star 标准的功能提供电源管理控制。O'Hare IC 连接到 PCI 总线并使用 32 MHz PCI 总线时钟。

O'Hare IC 包含了等效于 IDE、SCC、SCSI、音频、SWIM3 和 VIA 控制器 IC 的电路。O'Hare IC 中的功能块包括：
- 支持基于描述符的 I/O 设备 DMA
- 系统级中断处理

MkLinux: 用于 Power Macintosh 的微内核 Linux
- 一个 SWIM3 软驱器控制器
- SCSI 控制器（基于 MESH）
- SCC 串口 I/O 控制器
- IDE 硬盘接口控制器
- 音频控制逻辑和缓冲区

O'Hare IC 为以下 I/O 设备提供总线接口：
- Cuda ADB 控制器 IC（VIA1 和 VIA2 寄存器）
- AWACS 音频输入输出 IC
- 8 KB 非易失性 RAM 控制
- Macintosh 5400 用于亮度和对比控制的 PWM 输出

O'Hare IC 中的 SCSI 控制器是 MESH 控制器。O'Hare IC 中的 DMA 通道用于支持数据传输。在 Power Macintosh 5400 计算机中，到 SCSI 控制器的时钟信号为 45 MHz。

O'Hare IC 还包含音频控制逻辑以及音频输入输出缓冲区。有两个 DMA 数据缓冲区——一个用于音频输入，一个用于音频输出——因此计算机可以同时录制音频输入和处理音频输出。数据缓冲区包含交织的左右通道数据以支持立体声。

O'Hare IC 中的 SCC 电路是一个 8 位设备。到 SCC 的 PCLK 信号是 16 MHz 时钟。SCC 电路支持 GeoPort 和 LocalTalk 协议。

## PBX

PBX 内存控制器定制 IC 提供 RAM 和 ROM 内存控制，并作为处理器端总线、内存子系统与主板上 68030 型 I/O 总线之间的桥梁。PBX IC 还为 SWIM 软盘控制器提供周期解码。

## 第 17 章：Power Mac 系统

**内存控制。** PBX IC 控制系统 RAM 和 ROM，并为 DRAM 设备提供复用和刷新信号。

PBX IC 具有以索引寄存器文件形式存在的内存库解码器。寄存器文件中的每个字节（nibble）代表内存地址空间（64 MB）中的一个 2 MB 页面。每个字节中的值将相应的页面映射到物理 RAM 八个库中的一个。通过在启动时向寄存器文件写入适当的值，系统软件使内存地址变得连续。

**总线桥。** PBX IC 充当处理器总线和 I/O 总线之间的桥梁，将一个总线上的信号转换为另一个总线上的等信号。桥接功能由两个转换器执行。一个接受处理器总线的请求并将其提交给 I/O 总线。另一个接受 I/O 总线的请求并提供对处理器总线端 RAM 的访问。处理器总线工作频率为 33.33 MHz；I/O 总线工作频率为 25 MHz。

## Plan B

Plan B 为 7196 IC 提供两个 DMA 通道。写入通道从 7196 中的像素 FIFO 缓冲区获取数据，附加 DMA 地址并执行写入。读取通道从主内存读取每像素 位的裁剪掩码。

## Platinum

定制的内存视频控制器控制内存和缓存子系统，包括系统总线、主内存、ROM、VRAM 帧缓冲区和 L2 缓存。Platinum 支持高达 1 GB 的内存。

**数据交织。** 与 Power Macintosh 7500、8500 和 9500 计算机中的 Hammerhead 内存控制器不同，Platinum 只支持线性内存组织。当 RAM 扩展槽中安装成对的 DIMM 模块时，它不支持数据交织。

## 第 17 章：Power Mac 系统

欲需完整的技术细节，请参阅《Motorola PowerPC 601 RISC 微处理器用户手册》。

## PPC 603e

PowerPC 603e 微处理器是 PowerPC 603 的增强版本。其主要特性包括：
- 完整的 RISC 处理架构：一个整数单元和一个浮点单元
- 并行处理单元：一个与处理单元并行运行的加载存储单元
- 分支管理器：通常可以通过重新加载载入的指令队列来实现分支，而无需消耗任何处理时间
- 两个内部内存管理单元 (MMU)，一个用于指令，一个用于数据
- 两个独立的片上缓存（各 16 KB），分别用于数据和指令

欲需完整的技术细节，请参阅《PowerPC 603 微处理器实现定义书 第 IV》。

## PPC 604

PowerPC 604 微处理器的主要特性包括：
- 完整的 RISC 处理架构
- 并行处理单元：加载存储单元、两个整数单元、一个复杂整数单元和一个浮点单元
- 分支管理器：通常可以通过重新加载载入的指令队列来实现分支，而无需消耗任何处理时间
- 一个内部内存管理单元 (MMU)
- 独立的数据和指令缓存，各 16 KB，采用四路组关联映射

## 256 MkLinux：用于 Power Macintosh 的微内核 Linux

欲需完整的技术细节，请参阅《PowerPC 604 微处理器实现定义书 第 IV》。

## PSX

PSX 自定义 IC 提供缓存和 ROM 的桥接控制。它充当 PowerPC 603e 与 PCI 总线之间的桥梁，提供从一个总线到另一个总线的缓冲和地址转换。

PSX IC 还为系统缓存、ROM 和 RAM 提供控制和定时信号。内存控制逻辑支持对系统内存进行字节、字、长字（long word）和突发访问。如果访问未对齐相应的地址边界，PSX 会总线上产生多次数据传输。

## RaDACal

RaDACal 是一种高性能数字模拟转换器 (DAC)，用于视频流到显示器。

## SAA7194

SAA7194 是一颗飞利 CMOS 芯片，使用与其行频同步的时钟来解码 NTSC、PAL 和 SECAM 视频格式中的颜色信息。它用于 AV 卡。SAA7194 还：
- 执行带有水平和垂直滤波的输入视频窗口缩放
- 输出 16 位 1:5:5 RGB、8 位灰度以及 YUV 4:2:2 输出

## Sebastian

Sebastian 是一种采用 100 脚 CMOS 配置的视频颜色调色板和视频数字模拟转换器 (DAC)，用于 AV 卡。Sebastian：
- 接受宽度高达 64 位的数字数据，可以作为一个 64 位端口或两个 32 位端口
- 让一个 32 位端口处理数字视频，而另一个端口处理图形（包括 QuickTime），它们可以使用相同或不同的颜色查找表
- 支持视频与静态图形的混合，即使颜色深度不同也支持
- 支持带有 Alpha 颜色查找的真色彩色（Truecolor）和伪色彩（pseudocolor）
- 在每像素 1 到 8 位的 Alpha 通道位控制下，支持视频与静态图形混合时的透明效果
- 使用卷积滤波器以减少行间交织显示器中的闪烁
- 支持点时钟高达 100 MHz 的显示

## Singer

Singer 自定义 IC 是一颗 16 位数字音频解码器（编解码器）。它符合 IT&T ASCO 2300 音频立体声编码规范。音频样本通过 Singer IC 从 Whitney IC 在主内存中维护的音频 I/O 缓冲区进出。

## Sixty6

Sixty6 是一个 RGB 转 YUV 转换器，也是第二个视频输出的转换器（仅用于 Power Macintosh 8500 ）。Sixty6 将视频数据从 RGB 颜色空间转换为 YUV 颜色空间，然后对 YUV 空间中的数据进行卷积处理。7187 DENC IC 从 Sixty6 获取 YUV 格式的正方形像素，并将其编码为 NTSC 或 PAL 格式的复合视频。

## Squidlet

Squidlet 是一颗 28 脚芯片，为 Power Macintosh 提供一组同步系统时钟。

## SWIM III

SWIM III 自定义软驱驱动控制器是 Macintosh Quadra 800 和 Macintosh Centris 650 等机型使用的 SWIM II 电路的的扩展。它包含以下新功能：
- 支持 DMA 数据传输，最大限度地减少对主处理器的使用
- 不需要在软驱访问期间禁用中断
- 支持 1.44 MB 磁盘上的 GCR 和 MFM 格式
- 兼容手动插入的软驱驱动器

设计用于兼容 Macintosh Quadra 840AV 和 Macintosh Centris 660AV 使用的 New Age 控制器的软驱驱动器可以轻松适配 SWIM III 控制器。

## TREX

TREX 自定义 IC 为 PCMCIA 插槽提供接口和控制信号。TREX IC 的主要特性包括：
- PCMCIA 插槽的中断结构
- 与 PCMCIA 插槽之间单字节和字数据的传输
- PCMCIA 插槽的电源管理，包括睡眠模式
- 对单个插槽的控制
- 支持在计算机运行时插入和拔出卡
- 卡弹出

## Valkyrie-AR

Valkyrie-AR 是一个包含显示逻辑的自定义 IC。它包括：
- 显示内存控制器
- 视频 CLUT（颜色查找表）
- 视频 DAC（数字模拟转换器）

一个独立的数据线处理 Valkyrie-AR 与显示内存之间的数据传输。显示内存总线宽度为 32 位，所有数据传输均为 32 位。Valkyrie-AR 将其拆分为适用于当前显示模式的像素。为了跟上进入和离开显示内存的大量数据，Valkyrie-AR 拥有多个内部缓冲区。除了显示数据的输入输出缓冲区外，Valkyrie-AR 还具有一个用于主处理器发送的地址和数据的缓冲区。该缓冲区可以存放四个事务，允许主处理器完成写入指令，以等待显示内存上可能发生的其他事务。
