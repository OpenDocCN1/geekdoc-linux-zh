
对应于第一块 SCSI 板上最低目标/lun。

## 10 购买指南

一个常见的问题是：

“Linux 支持许多不同的板，那么我应该买哪种 SCSI 主机适配器？”

答案取决于你预期或需要的性能、主板以及计划连接到机器上的 SCSI 外设。

### 10.1 传输类型

影响性能（在 I/O 期间的吞吐量和响应时间）的最大因素是使用的传输类型。下表列出了各种传输类型、它们对性能的影响以及使用建议。

| 传输类型 | 说明 / 性能 / 建议 |
| :--- | :--- |
| P 轮询 (Polled) | 轮询 I/O 板将使用 CPU 处理所有的 SCSI 操作，包括 REQ/ACK 握手。即使是快速 CPU，处理 REQ/ACK 握手序列的速度也比简单的状态机慢，导致在快速机器上的峰值传输率约为 150K/sec，在慢机器上（通过文件系统）可能只有 60K/sec。当 SCSI 忙时，驱动程序必须处于紧循环中，导致接近 100% 的 CPU 占用，且对 SCSI I/O 的响应极差。不会断开/重连的慢速光驱会严重破坏此类板的交互性能。 |
| 互锁轮询 (Interlocked Polled) | 使用互锁轮询 I/O 的板本质上与纯轮询 I/O 板相同；SCSI REQ/ACK 握手与 PC 总线定时交替进行。握手机的所有 SCSI 处理都由 CPU 完成。这些板通过文件系统可以实现 500-600K/sec 的峰值传输率。作为纯轮询 I/O 板，当 SCSI 忙时驱动程序必须处于紧循环中，导致 CPU 占用取决于设备的传输速率以及它们断开/重连的情况。对于处理断开/重连几乎达到 100% 的单速光盘，以及更快的驱动或损坏的光驱，CPU 占用可能在 25% 之间波动。在我的带有 T128 板的 486-66 上，我使用 90% 的 CPU 时间来维持头速率为 180K/sec 的驱动器的 547K/sec 吞吐量。有时适用于对成本至关重要的慢速磁带和光驱。 |
| FIFO 轮询 (FIFO Polled) | 使用 FIFO I/O 的板在 CPU 和 SCSI 总线之间放置了一个小型（通常为 8K）缓冲区，并通常实现了一定的智能性。最终效果是，只有当以高速向 FIFO 传输数据以及在处理 FIFO 空状态、断开/重连等处理结果时，CPU 才会被占用。峰值传输率足以处理大多数 SCSI 板，在带有 Adaptec 1520 的 Seagate Barracuda 硬盘上，通过原始 SCSI 命令读取 64 块的测得速率高达 4M/sec。CPU 占用取决于设备的传输速率，较快的设备单位时间内产生更多中断，需要更多的 CPU 处理时间。尽管在使用快速设备时 CPU 使用率可能较高（也许 75%），但系统仍然可用。这些板对于不会断开/重连的损坏设备（通常是廉价的 CSG 光驱）提供出的性能。推荐预算有限的用户使用。 |
| 从机 DMA (Slave DMA) | 驱动程序在数据传输时使用 PC 的 CPU 主控制器作为通道，并将控制权返回给 CPU。峰值传输率通常由 PC 上的 DMA 控制器处理，一个 8 位板在单块主板上超过 140-150K/sec 就会出现问题（注：原文 "problems faster than" 疑有误，应为“超过...时出现问题”）。CPU 占用相当轻微，低于 FIFO I/O 板。这些板对不会断开/重连的损坏设备（通常是廉价的 CSG 限制驱动器）具有很强的兼容性。适用于慢速光驱、磁带。 |
| 缓冲 DMA (Buffering DMA) | 这些板启动 SCSI 命令、目标目标和 lun 以及数据在结构中的存放位置，并告诉总线“嘿，我有一个命令要发”。驱动程序返回到各种程序。 |

# PCI

带宽约为 60M/sec。大多数 PCI 系统在主机桥上实现事后写入（posting writes），允许双方的速度不匹配对总线/CPU 的影响降至最低。PCI 中断驱动程序使用开集极（open collector），允许与支持该特性的驱动程序共享。提供了机制来防止总线跳跃，并允许主设备和从设备挂起主控操作。

由于 PCI 提供了即插即用机制，且每个板卡上的配置寄存器都位于独立的地址中，因此实现良好的 PCI 系统是即插即用的。

PCI 对布线长度、负载、机械规格的要求极其严格，最终性能应该优于 VESA 或 ISA。

总而言之，PCI 是最好的 PC 总线，尽管它也有其阴暗面。PCI 仍处于婴儿阶段，尽管许多制造商已经解决了这些问题，但它仍然受限于旧的、带有 Bug 的 PCI 硬件和损坏的 BIOS。对于这些设备，我强烈建议退换硬件。虽然最新的 PCI 主板大多是即插即用的，但旧的 PCI 板可能需要用户通过跳线帽和软件设置选项（例如中断分配）。许多用户已经解决了 PCI 问题，但这花费了时间，由于这个原因，如果系统运行至关重要，我无法建议购买 PCI。

对于许多较慢的 SCSI 设备（其头速率在 2M/sec 或以下）、CD-ROM 和磁带，使用 PCI 总线接口的差异可能很小。对于现代 SCSI 驱动器（典型具有头速率 4-M/sec 的高端数 GB 驱动器，Ultra 头速率为 14M/sec），在较快总线上的控制器其吞吐量将显著提高；一位用户注意到，从 Adaptec 1542 ISA 板切换到 NCR53c810 PCI 板时，性能提升了 2.5 倍。

除了使用 PCI 写入事后或简单的写入缓冲的情况外，当系统中的某个总线忙碌时，所有总线将无法访问。虽然总线饱和可能不会干扰 SCSI 性能，但可能会对其他接口产生负面影响。例如，如果你有一个 4M/sec 的 SCSI 磁盘，你将拥有80% 的带宽，而在 EISA 系统中可以达到 6M/sec 的速度。在大多数情况下，只会感觉到对后台处理任务产生了简单影响。

注意，超过 16M 的内存并不排除使用 ISA 主控的操作系统，当使用 ISA 控制器进行 DMA 且传输目标位于 16M 以上时，Linux 会使用双倍缓冲。这些传输的性能仅提升了 1.5%，并不明显。

最后，不同总线接口提供的主控设备价格差异通常微乎其微。

考虑到所有这些，根据你的优先级，你将会有特定的总线偏好：

| 优先级 | 接口 |
| :--- | :--- |
| 稳定性、对时间敏感的安装 | EISA ISA VESA PCI |
| 性能、典型爱好者 | PCI EISA VESA ISA（退货政策较差） |

正如我之前指出的，主控模式与其他传输模式对比对总性能的影响更大，在购买 SCSI 控制器时，认为这比总线类型更重要。

# 10.5 多设备

如果你的 SCSI 总线上有多个设备，你可能想要检查主机/驱动程序是否支持同时处理多个待处理命令。如果你将运行磁带机，这几乎是必须的；如果你在使用不同速度的设备（如 CD-ROM 和磁盘驱动器），这将非常理想。Linux 驱动程序仅支持一个待处理命令，当磁带机回带或寻道到媒体末尾时（可能持续半小时），你的磁盘驱动器可能会被锁定。当有两个驱动器时，问题不会那么明显，尽管其传输速率更接近两个速率的平衡值而非两者之和。

# 10.6 SCSI-I, SCSI-II, SCSI-III FAST 和 VIDEO 等

多年来，SCSI 一直在演进，标准的修订引入了更高的传输速率、增加吞吐量的方法、针对新设备的标准命令以及针对以前支持的设备的新命令。

在其他情况下，版本级别并不代表什么。除了像 SCSI-II 不允许 SCSI-I 的单启动器选项等情况，SCSI 是向后兼容的，新功能作为选项引入而非强制要求。因此，将一个 SCSI 适配器称为 SCSI、SCSI-II 或 SCSI-III 的决定几乎完全出于营销。

# 10.7 驱动程序功能比较

驱动程序功能比较（出厂芯片列在括号中）

| 驱动程序 | 同时命令总数/运行 | SG 限制 | > 1 块板卡 |
| :--- | :--- | :--- | :--- |
| AM53C94 | Busmaster DMA | 12s/1s | 255s | Y |
| aha152x (AIC6260) | FIFO(8k) 轮询 | 7s/1s | 255s | N |
| (AIC6260) | Busmaster DMA | 8s/1s | 16 | Y |
| aha1542 | Busmaster DMA | 32s | 16 | N |
| aha1740 | Busmaster DMA | 4s/1s | 255s | Y |
| aha274x | Busmaster DMA | 192/31 | 128s, 8192h | Y |
| BusLogic (var. 为 FT-98/958/958, 旧板卡支持命令较少) | Busmaster DMA | 64s-8192h/64 | 512s, 8192h |
||data_f | Busmaster DMA FIFO(8k) 轮询 | 1s | 64s | N |
| (TMC1800, TMC18c30, TMC18c50, TMC370) | TMC18c30 2k FIFO | | |
| in2000* | FIFO(2k) 轮询 | 1s | 255s | N |
| g_NCR5380 (5380, NCR53c80, NCR531c40) | 轮询 | 16s/2s | 255s | Y |
| gsi8 (NCR5380) | Slave DMA | 16s/2s | 255s | |
| PAS16 (NCR5380) | 轮询或互锁轮询 (某些系统失败！) | 1s/1s | 255s | N |
| seagate wd7000 | 互锁轮询 Busmaster DMA | 16s/1s | 16 | Y |
| t128 (NCR5380) | 互锁轮询 | 16s | 255s | Y |
| qlogic ultra 53c7,8xx | 互锁轮询 Busmaster DMA | 1s/1s | 255s | N |
| (NCR53c810, NCR53c15, NCR53c20, NCR53c25) | Busmaster DMA | 16s/2s | 32 | Y |
| rel15 | | 1s/1s | 127s | N |
| rel10 | | 8s/1s | 127s | Y |

*带有 '*' 的驱动程序未包含在发行内核中，二进制镜像可能不可。带有 's' 后缀的数字是软件设置的任意限制，可能与 Linux 驱动程序的限制不同。带有 'h' 后缀的数字指示硬件限制。rel5 的 NCR53c680 包含在 1.2.x 和 1.3.x 内核中；rel10 通过匿名 FTP 提供。除 AM53C974 外，主控 DMA 是智能的；从主内存执行微代码，从芯片 RAM 执行微代码，其余使用邮箱式接口。

# 10.8 板卡比较

| 板卡 | 驱动程序 | 总线 | 价格 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| Adaptec AIC-6260 | aha152x | ISA | | 芯片，而非板卡 |
| Adaptec AIC-6360 | aha152x | VLB | | 芯片，而非板卡（用于大多数 VESA/ISA 多 IO 板卡、Zen 主板） | |
| Adaptec 1520 | aha152x | ISA | | |
| Adaptec 1522 | aha152x | ISA | $80 | 1520 带 FDC 版本 |
| Adaptec 1510 | aha152x | ISA | | 1520 带启动 ROM，不支持自动探测 |
| Adaptec 1540C | aha1542 | ISA | | |
| Adaptec 1542C | aha1542 | ISA | | 1540C 带 FDC 版本 |
| Adaptec 1540CF | aha1542 | ISA | | FAST SCSI-II |
| Adaptec 1542CF | aha1542 | ISA | $200 | 1540CF 带 FDC 版本 |
| Adaptec 1640 | aha1542 | MCA | | |
| Adaptec 1740 | aha1740 | EISA | | |
| Adaptec 1742 | aha1740 | EISA | | 停产，1740 带 FDC 版本 |
| Adaptec 2740 | aha274x | EISA | | |
| Adaptec 2742 | aha274x | EISA | | 带 FDC 版本 |
| Adaptec 2840 | aha274x | VLB | | |
| Adaptec 2842 | aha274x | VLB | | 带 FDC 版本 |
| Adaptec 2940 | aha274x | PCI | | |
| Always IN2000 | in2000 | ISA | | |
| BusLogic BT-948 | BusLogic | PCI | $180 | Ultra SCSI |
| BusLogic BT-958 | BusLogic | PCI | $230 | Wide SCSI |

（所有 BusLogic 板卡描述请见 5.8 节）

| PM2011 | eata_dma | ISA | | FAST SCSI-II |
| PM2012A | eata_dma | EISA | | FAST SCSI-II |
| PM2012B | eata_dma | EISA | | FAST SCSI-II |
| PM2021 | eata_dma | ISA | | FAST SCSI-II |
| PM2022 | eata_dma | EISA | | FAST SCSI-II |
| PM2024 | eata_dma | PCI | | FAST SCSI-II |
| PM2122 | eata_dma | EISA | | FAST SCSI-II |
| PM2322 | eata_dma | EISA | | FAST SCSI-II |
| PM2124 | eata_dma | PCI | | FAST SCSI-II |

# 购买指南

| | | | |
|---|---|---|---|
| PM2124 | eata_dma | PCI | 极速 SCSI-II |
| PM2041W | eata_dma | ISA | 宽单端 |
| PM2041UW | eata_dma | ISA | 超宽单端 |
| PM2042W | eata_dma | EISA | 宽单端 |
| PM2042UW | eata_dma | EISA | 超宽单端 |
| PM2044W | eata_dma | PCI | 宽单端 |
| PM2044UW | eata_dma | EISA | 超宽单端 |
| PM2142W | eata_dma | PCI | 宽单端 |
| PM2142UW | eata_dma | EISA | 超宽单端 |
| PM2144W | eata_dma | PCI | 宽单端 |
| PM2144UW | eata_dma | PCI | 超宽单端 |
| PM3021 | eata_dma | ISA | 多通道 raid/simm 插槽 |
| PM3122 | eata_dma | EISA | 多通道/raid/simm 插槽 |
| PM3222 | eata_dma | EISA | 多通道 raid/simm 插槽 |
| PM3224 | eata_dma | PCI | 多通道 raid/simm 插槽 |
| PM3334 | eata_dma | PCI | 宽超 SCSI 多通道 raid/simm 插槽 |

DTC 3290 aha1542 EISA 尽管它可以工作，但由于文档发布策略，硬件不受支持。

| | | | |
|---|---|---|---|
| DTC 3130 | 53c7,8xx | PCI | '80 型 |
| DTC 3130B | 53c7,8xx | PCI | '85 型 |
| DTC 3292 | aha1542 | EISA | 带 FDC 的 3290 |
| DTC 3292 | aha1542 | EISA | 带 FDC 的 3290 |
| Future Domain 1680 | fdomain | ISA | FDC |
| Future Domain 3260 | fdomain | | | |
| NCR53c810 (板型 53c7,8xx) | | PCI | $60 芯片，非板卡。板卡 |
| 由 Fiche, Chaintech, | | | (没有) BIOS，几乎大部分 |
| Nextor, Gigabyte, 等. | | | 非配备 NCR 芯片的主板 |
| 带有以下芯片的主板 | | | 主板配备了 SDMS |
| AMI, ASIS, J-Bond, | | | BIOS |
| 等. 常见于 DEC | | | |
| PCI 系统 | | | |
| NCR53c815 ( | 53c7,8xx | PCI | $100 包含 NCR53c810 加上 |
| Intel PCICSKSIKIT, | | | bios |
| NCR81505,等) | | | $120 宽变体。注意 |
| NCR53c825 | 53c7,8xx | | | 当前的 Linux 驱动程序 |
| | | | 不为 |
| | | | 宽传输进行协商 |
| | | |。 |

| Pro Audio Spectrum 16 pas156 ISA 声卡（带SCSI） |
| Seagate ST01 seagate ISA $20 BIOS 仅对某些驱动器有效 |
| Seagate ST02 seagate ISA $40 ST01 带 FDC |
| Sound Blaster 16 SC-SI aha152x ISA 声卡（带SCSI） |
| Western Digital 7000 wd7000 ISA 带 FDC |

| | | | |
|---|---|---|---|
| Trantor T128 | t128 | ISA | |
| Trantor T128F | t128 | ISA | T128 带 FDC 支持，支持高优先级中断 |
| Trantor T130B | g_NCR5380 | ISA | |
| Ultrastor 14F | ultrastor | ISA | 带 FDC |
| Ultrastor 24F | ultrastor | EISA | 带 FDC |
| Ultrastor 34F | ultrastor | VLB | |

备注：

1. Trantor 近期被 Adatec 收购，部分产品以 Adatec 之名销售。
2. Ultrastor 近期申请了第 11 章破产，目前没有任何支持。
3. 总线主机 NCR53c810 板卡的价格并非笔误，可以免费下载用于 DOS、OS2 Windows (32位访问) 标准 ASI/CAM 驱动程序包以及其他驱动程序。

一些用户在使用以下公司遇到过问题：

```
