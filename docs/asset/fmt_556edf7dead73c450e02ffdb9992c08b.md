
双核 SiByte 处理器包括 `BCM1250`、`BCM1255` 和 `BCM1280`。同样基于 MIPS64 内核，这些处理器的运行频率从 600MHz（`BCM1250`）到最高 1.2GHz（`BCM1255` 和 `BCM1280`）。这些双核芯片包含集成的外设控制器，如 DDR SDRAM 控制器、各种千兆以太网控制器组合、64 位 PCI-X 接口，以及 SMBus、PCMCIA 和多个 UART 接口。与单核同类产品一样，这些双核实现也具有低功耗特性。例如，`BCM1255` 在 1GHz 运行时功耗预算为 13W。

四核 SiByte 处理器包括 `BCM1455` 和 `BCM1480` 通信处理器。与其他 SiByte 处理器一样，它们基于 MIPS64 内核。内核运行频率可从 800MHz 到 1.2GHz。这些 SOC 包含集成的 DDR SDRAM 控制器、四个独立的千兆以太网 MAC 控制器和 64 位 PCI-X 主机控制器，并包含 SMBus、PCMCIA 和四个串行 UART。

表 3-7 总结了精选的 Broadcom SiByte 处理器。

### 表 3-7
Broadcom 精选 SiByte 处理器亮点

| 特性 | `BCM1125H` | `BCM1250` | `BCM1280` | `BCM1480` |
| :--- | :--- | :--- | :--- | :--- |
| 内核/速度 | SB-1 MIPS64 | 双核 SB-1 MIPS64 | 双核 SB-1 MIPS64 | 四核 SB-1 MIPS64 |
| | 400–900MHz | 600–1000MHz | 800–1200MHz | 800–1200MHz |
| DRAM 控制器 | Y- DDR | Y- DDR | Y- DDR | Y- DDR |
| 串行接口 | 2–55Mbps | 2–55Mbps | 4 UART | 4 UART |
| SMBus 接口 | 2 | 2 | 2 | 2 |
| PCMCIA | Y | Y | Y | Y |
| 千兆以太网 (10/100/1000Mbps) | 2 | 3 | 4 | 4 |
| PCI 控制器 | Y | Y | Y PCI/PCI-X | Y PCI/PCI-X |
| 安全引擎 | N | N | N | N |
| 高速 I/O (HyperTransport) | 1 | 1 | 3 | 3 |

#### 3.2.6 AMD MIPS

Advanced Micro Devices（AMD）在嵌入式 MIPS 控制器市场中也发挥着重要作用。该公司 2002 年收购 Alchemy Semiconductor 获得了几个基于 MIPS32 内核和架构的热门单芯片集成 SOC。AMD 的 Alchemy 产品线基于流行的 MIPS32 内核。所有产品都具有相对较低的功耗和高水平的片上系统集成。

`Au1000` 和 `Au1100` 的运行频率为 266–500MHz。两者都具备片上 SDRAM 控制器和用于连接 Flash 和 PCMCIA 等外部设备的独立总线控制器。表 3-8 总结了当前的 Alchemy 产品线。

### 表 3-8
AMD Alchemy MIPS 亮点总结

| 特性* | `Au1000` | `Au1100` | `Au1200` | `Au1500` | `Au1550` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 内核/速度 | MIPS32 | MIPS32 | MIPS32 | MIPS32 | MIPS32 |
| | 266–500MHz | 333–500MHz | 333–500MHz | 333–500MHz | 333–500MHz |
| DRAM 控制器 | SDRAM | SDRAM | DDR SDRAM | SDRAM | DDR SDRAM |
| 以太网 10/100 | 2 | 1 | – | 2 | 2 |
| GPIO 引脚 | 32 | 48 | 48 | 39 | 43 |
| UARTs | 4 | 3 | 2 | 2 | 3 |
| USB 1.1 | 主机 + 设备 | 主机 + 设备 | USB 2.0 | 主机 + 设备 | 主机 + 设备 |
| AC-97 音频 | 1 | 1 | 通过 SPC | 1 | 通过 SPC |
| I²S 控制器 | 1 | 1 | 通过 SPC | – | 通过 SPC |
| SD/MMC | N | 2 | 2 | N | N |

\*其他外设包括 IrDA 控制器、LCD 控制器、2 个 SPC、电源管理、DMA 引擎、RTC、摄像头接口、LCD 控制器、加密/解密硬件加速、PCI 主机控制器、4 个 SPC 和安全引擎。

#### 3.2.7 其他 MIPS

正如我们之前指出的，MIPS 技术公司的授权商网页上列出了近 100 家当前的 MIPS 授权商，网址为 `www.mips.com/content/Licensees/ProductCatalog/licensees`。遗憾的是，在此篇幅内无法涵盖所有授权商。您不妨从 MIPS 技术公司的网站开始搜索，以了解 MIPS 处理器厂商的广泛情况。

例如，ATI 科技在其 Xilleon 机顶盒芯片家族中使用了 MIPS 内核。Cavium Network 的 Octeon 家族在各种多核处理器实现中使用了 MIPS64 内核。Integrated Device Technology, Inc.（IDT）有一个名为 Interprise 的集成通信处理器家族，基于 MIPS 架构。PMC-Sierra、NEC、东芝等公司也有基于 MIPS 的集成处理器。所有这些以及其他更多产品都在 Linux 下得到良好支持。

### 3.2.8 ARM

ARM 架构在消费电子市场中占据了非常大的市场份额。许多流行且如今随处可见的产品都包含 ARM 内核。一些知名例子包括索尼 PlayStation Portable (PSP)、Apple iPod Nano、任天堂 Game Boy Micro 和 DS、Tom Tom GO 300 GPS 以及内置 Linux 的摩托罗拉 E680i 移动电话。根据 ARM 公司背景介绍（`www.arm.com/miscPDFs/3822.pdf`），包含 ARM 内核的处理器驱动着世界上大多数数字蜂窝电话。

ARM 架构由 ARM Holdings, plc 开发，并授权给全球各地的半导体制造商。许多世界领先的半导体公司已获得 ARM 技术授权，并正在出货基于多种 ARM 内核之一的集成处理器。

#### 3.2.9 TI ARM

德州仪器（Texas Instruments）在 OMAP 系列集成处理器中使用 ARM 内核。这些处理器包含许多集成外设，旨在作为各种消费类产品（如蜂窝手持机、PDA 和类似的多媒体平台）的单芯片解决方案。除了通常发现的接口外

> 据报道，这是 2005 年圣诞购物季在美国销量最高的玩具。

集成处理器，例如 UART 和 I²C，OMAP 设备包含大量专用接口，包括以下各项：

- LCD 屏幕和背光控制器
- 蜂鸣器驱动器
- 摄像头接口
- MMC/SD 卡控制器
- 电池管理硬件
- USB 客户端/主机接口
- 无线电调制解调器接口逻辑
- 集成 2D 或 3D 图形加速器
- 集成安全加速器
- S-Video 输出
- IrDA 控制器
- 用于直接电视（PAL/NTSC）视频输出的 DAC
- 用于视频和音频处理的集成 DSP

许多流行的蜂窝手机和 PDA 设备均基于 TI OMAP 平台进行市场推广。由于其基于 ARM 内核，这些处理器目前均受 Linux 支持。表 3-9 比较了 TI OMAP 家族中一些较新的成员。

### 表 3-9
TI ARM OMAP 亮点汇总

| 特性 | `OMAP1710` | `OMAP2420` | `OMAP2430` | `OMAP3430` |
|---|---|---|---|---|
| 内核/速度 | ARM926 TE | ARM11 | ARM1136 | ARM Cortex A8 |
| | 最高 200MHz | 330MHz | 330MHz | 550MHz |
| DRAM 控制器 | Y | Y | Y | Y |
| UART | Y | Y | Y | Y |
| USB | 客户端 + 主机 | 客户端 + 主机 | 客户端 + 主机 | 客户端 + 主机 |
| FC 控制器 | Y | Y | Y | Y |
| MMC-SD 接口 | Y | Y | Y | Y |
| 键盘控制器 | Y | Y | Y | Y |
| 摄像头接口 | Y | Y | Y | Y |
| 图形加速器 | 2D | 2D/3D | 2D/3D | Y |
| 集成 DSP | TM320C55x | TM320C55x | N | N |
| 视频加速硬件 | N | 成像视频加速器 (IVA) | 成像视频加速器 (IVA 2) | 成像视频加速器 (IVA 2+) |
