

表 3-5 总结了 PQ II Pro 家族中部分成员的特点。

### 表 3-5
飞思卡尔精选 PowerQUICC II Pro 亮点

| 特性 | MPC8343E | MPC8347E | MPC8349E | MPC8360E |
| :--- | :--- | :--- | :--- | :--- |
| 内核/速度 | e300 | e300 | e300 | e300 |
| | 266–400MHz | 266–667MHz | 400–667MHz | 266–667MHz |
| DRAM 控制器 | Y- DDR | Y- DDR | Y- DDR | Y- DDR |
| USB | Y | 2 | 2 | Y |
| SPI 控制器 | Y | Y | Y | Y |
| I²C 控制器 | 2 | 2 | 2 | 2 |
| 以太网 10/100/1000 | 2 | 2 | 2 | 通过 UCC |
| UART | 2 | 2 | 2 | 2 |
| PCI 控制器 | Y | Y | Y | Y |
| 安全引擎 | Y | Y | Y | Y |
| MCC | 0 | 0 | 0 | 1 |
| UCC | 0 | 0 | 0 | 8 |

PowerQUICC 家族的高端是 PQ III 处理器。这些处理器的运行速度介于 600MHz 和 1.5GHz 之间。它们基于 e500 内核，支持千兆以太网、DDR SDRAM、RapidIO、PCI 和 PCI/X、ATM、HDLC 等。该家族包含 MPC85xx 产品线。这些处理器已应用于高端产品，如无线基站控制器、光边缘交换机、中心局交换机以及类似设备。

表 3-6 强调了 PQ III 家族的一些成员。

### 表 3-6
PQ III 家族亮点

| 特性 | MPC8540 | MPC8548E | MPC8555E | MPC8560 |
| :--- | :--- | :--- | :--- | :--- |
| 内核/速度 | e500 | e500 | e500 | e500 |
| | 最高 1.0GHz | 最高 1.5GHz | 最高 1.0GHz | 最高 1.0GHz |
| DRAM 控制器 | Y- DDR | Y- DDR | Y- DDR | Y- DDR |
| USB | N | N | 通过 SCC | N |
| SPI 控制器 | N | N | Y | Y |
| I²C 控制器 | Y | Y | Y | Y |
| 以太网 10/100 | 1 | 通过 GigE | 通过 SCC | 通过 SCC |
| 千兆以太网 | 2 | 4 | 2 | 2 |
| UART | 2 | 2 | 2 | 通过 SCC |
| PCI 控制器 | PCI/PCI-X | PCI/PCI-X | PCI | PCI/PCI-X |
| Rapid IO | Y | Y | N | Y |
| 安全引擎 | N | Y | Y | N |
| SCC | – | – | 3 | 4 |
| FCC | – | – | 2 | 3 |
| SMC | – | – | 2 | 0 |
| MCC | – | – | 0 | 2 |

## 3.2.4 MIPS

您可能会惊讶地发现，基于 MIPS 架构的 32 位处理器已经出货 20 多年了。MIPS 架构由斯坦福大学的一个工程团队于 1981 年设计，该团队由约翰·亨尼西（John Hennessy）博士领导，他后来创立了 MIPS 计算机系统公司（MIPS Computer Systems, Inc.）。该公司已演变为现在的 MIPS 技术公司（MIPS Technologies），其主要角色是设计并授权 MIPS 架构和内核。

许多公司都获得了 MIPS 内核的授权，其中一些已成为嵌入式处理器市场的巨头。MIPS 是一种精简指令集计算（RISC）架构，其 32 位和 64 位实现已广泛应用于许多流行产品。MIPS 处理器出现在各种产品中，从高端设备到消费类电子产品。众所周知，MIPS 处理器驱动着许多知名的消费类电子产品，如索尼高清电视、Linksys 无线接入点以及流行的索尼 PlayStation 2 游戏机。

MIPS 技术公司的网站列出了 73 家目前正在使用 MIPS 处理器内核制造产品的授权商。其中一些公司是家喻户晓的名字，例如索尼（Sony）、德州仪器（Texas Instruments）、思科的 Scientific Atlanta（领先的有线电视机顶盒制造商）、摩托罗拉（Motorola）等。当然，其中最大且最成功的公司之一是 Broadcom 公司。

### 3.2.5 Broadcom MIPS

Broadcom 是有线电视机顶盒、有线电视调制解调器、HDTV、无线网络、千兆以太网和 IP 语音（VoIP）等市场的主要 SOC 解决方案供应商。Broadcom 的 SOC 在这些市场非常受欢迎。我们之前提到，即使您自己不知道，您的家中很可能也有 Linux。如果有，它很可能运行在基于 Broadcom MIPS 的 SOC 上。

2000 年，Broadcom 收购了 SiByte Inc.，这形成了该公司目前销售的通信处理器产品系列。这些处理器目前以单核、双核和四核配置出货。该公司仍称它们为 SiByte 处理器。

单核 SiByte 处理器包括 BCM1122 和 BCM1125H。它们都基于 MIPS64 内核，运行速度在 400–900MHz 之间。它们包含片上外设控制器，如 DDR SDRAM 控制器、10/100Mbps 以太网和 PCI 主机控制器。两者都包含 SBMux 串行配置接口、PCMCIA 和两个用于串口连接的 UART。BCM1125H 包含一个三倍速 10/100/1000Mbps 以太网控制器。这些处理器最令人印象深刻的特性之一是它们的功耗。两者在 400MHz 运行时功耗预算均为 4W。

双核 SiByte 处理器包括 BCM1250、BCM1255 和 BCM1280。同样基于 MIPS64 内核，这些处理器的运行频率从 600MHz（BCM1250）到最高 1.2GHz（BCM1255 和 BCM1280）。这些双核芯片包含集成的外设控制器，如 DDR SDRAM 控制器、各种千兆以太网控制器组合、64 位 PCI-X 接口，以及 SMBus、PCMCIA 和多个 UART 接口。与单核同类产品一样，这些双核实现也具有低功耗特性。例如，BCM1255 在 1GHz 运行时功耗预算为 13W。

四核 SiByte 处理器包括 BCM1455 和 BCM1480 通信处理器。与其他 SiByte 处理器一样，它们基于 MIPS64 内核。内核运行频率可从 800MHz 到 1.2GHz。这些 SOC 包含集成的 DDR SDRAM 控制器、四个独立的千兆以太网 MAC 控制器和 64 位 PCI-X 主机控制器，并包含 SMBus、PCMCIA 和四个串行 UART。

表 3-7 总结了精选的 Broadcom SiByte 处理器。

### 表 3-7
Broadcom 精选 SiByte 处理器亮点

| 特性 | BCM1125H | BCM1250 | BCM1280 | BCM1480 |
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

## 3.2.6 AMD MIPS

Advanced Micro Devices（AMD）在嵌入式 MIPS 控制器市场中也发挥着重要作用。该公司 2002 年收购 Alchemy Semiconductor 获得了几个基于 MIPS32 内核和架构的热门单芯片集成 SOC。AMD 的 Alchemy 产品线基于流行的 MIPS32 内核。所有产品都具有相对较低的功耗和高水平的片上系统集成。

Au1000 和 Au1100 的运行频率为 266–500MHz。两者都具备片上 SDRAM 控制器和用于连接 Flash 和 PCMCIA 等外部设备的独立总线控制器。表 3-8 总结了当前的 Alchemy 产品线。

**表 3-8**
AMD Alchemy MIPS 亮点总结

| 特性* | Au1000 | Au1100 | Au1200 | Au1500 | Au1550 |
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

## 3.2.7 其他 MIPS

正如我们之前指出的，MIPS 技术公司的授权商网页上列出了近 100 家当前的 MIPS 授权商，网址为 www.mips.com/content/Licensees/ProductCatalog/licensees。遗憾的是，在此篇幅内无法涵盖所有授权商。您不妨从 MIPS 技术公司的网站开始搜索，以了解 MIPS 处理器厂商的广泛情况。

例如，ATI 科技在其 Xilleon 机顶盒芯片家族中使用了 MIPS 内核。Cavium Network 的 Octeon 家族在各种多核处理器实现中使用了 MIPS64 内核。Integrated Device Technology, Inc.（IDT）有一个名为 Interprise 的集成通信处理器家族，基于 MIPS 架构。PMC-Sierra、NEC、东芝等公司也有基于 MIPS 的集成处理器。所有这些以及其他更多产品都在 Linux 下得到良好支持。

## 3.2.8 ARM

ARM 架构在消费电子市场中占据了非常大的市场份额。许多流行且如今随处可见的产品都包含 ARM 内核。一些知名例子包括索尼 PlayStation Portable (PSP)、Apple iPod Nano、任天堂 Game Boy Micro 和 DS、Tom Tom GO 300 GPS 以及内置 Linux 的摩托罗拉 E680i 移动电话。根据 ARM 公司背景介绍（www.arm.com/miscPDFs/3822.pdf），包含 ARM 内核的处理器驱动着世界上大多数数字蜂窝电话。

ARM 架构由 ARM Holdings, plc 开发，并授权给全球各地的半导体制造商。许多世界领先的半导体公司已获得 ARM 技术授权，并正在出货基于多种 ARM 内核之一的集成处理器。

## 3.2.9 TI ARM

德州仪器（Texas Instruments）在 OMAP 系列集成处理器中使用 ARM 内核。这些处理器包含许多集成外设，旨在作为各种消费类产品（如蜂窝手持机、PDA 和类似的多媒体平台）的单芯片解决方案。除了通常发现的接口外

> 据报道，这是 2005 年圣诞购物季在美国销量最高的玩具。

