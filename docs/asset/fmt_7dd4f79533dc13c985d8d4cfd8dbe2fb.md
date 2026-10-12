
- 主机适配器支持特定数量的逻辑驱动。具体信息请参适配器文档。

## Linux 局限性与变通

下表列出了在 Linux 下使用 IBM TotalStorage FASIT Storage Manager 8.3 时的局限性（表 5-3）。

**表 5-3** IBM TotalStorage Manager 局限性列表

| 局限性 | 变通 |
| --- | --- |
| 使用固件版本为 04.01.02 的控制器的 Vixel Rapport 2000 光纤交换机会导致问题，包括数据损坏、系统不稳定和环活动中断。 | 当你的系统在控制器或 I/O 路径容错环境中运行时，请使用 Vixel Rapport 2000 光纤交换机。 |
| 单个 RAID 5 逻辑驱动允许的物理硬盘最大数量为 29。单个 RAID 1 逻辑驱动允许的物理硬盘最大数量为 28。 | 无 |
| 从存储子系统中移除硬盘后，在软件启动或执行受保护操作时，系统会提示输入密码，以及你输入的所有密码。 | 将其中一个硬盘添加到存储子系统并再次尝试操作。 |
| 不支持从一个存储子系统移除一组配置了逻辑驱动的硬盘插入另一个存储子系统，因为这可能会导致配置丢失。 | 联系 IBM 技术支持代表寻求帮助。 |
| 当 Linux 主机没有 TCP/IP 软件时，不支持标准的非网络配置。 | 在客户 Linux 主机上安装 TCP/IP 软件并协助主机静态 IP 地址。 |
| 多路故障转移仅在控制器处于活动/活动（active/active）模式时才有效。 | 当配置存储子系统时，将两个控制器都更改为活动状态。 |
| 控制器固件在仅填充 A 槽时无法识别或与控制器通信。此限制不适用于最初配置了两个控制器的存储子系统。 | 当你使用单个控制器配置新子系统时，将控制器放在 A 槽中。 |
| 当你在 256 色模式下运行时，你的窗口和在线帮助会显示棕色的图案。 | 以更高的显示模式运行 Storage Manager 8.3 程序。 |
| 从存储管理应用程序执行冗余检查（奇偶扫描）时，机型 3542 比机型 1742 和 3552 控制器平台慢几分钟。 | 无 |
| 如果你使用不同容量的硬盘，在自动配置期间可能看不到最大数量的硬盘。 | 使用手动配置选择单个硬盘并选择允许的最大硬盘数量。 |
| 当你将 IBM TotalStorage FASIT EXP707 存储扩展单元连接到 FASTT200 时，硬盘速度必须设置为每秒 1 Gb。 | 无 |

## X 架构的功能

本附录简要描述了第 25 页“Linux and functions of X-Architecture”中引入的 X 架构功能。

### XpandOnDemand

`XpandOnDemand` 是 X 架构的一部分。16 路服务器的威力现在通过 `xSeries 440` 提供，用于处理高级企业应用并驱动更高水平的性能。

（注：OCR 文本在该部分有大量重复，已清理实际内容流。）

`XpandOnDemand` 是 X 架构的一部分。16 路服务器的威力现在通过 `xSeries 440` 提供，用于处理高级企业应用并驱动更高水平的性能。

（注：此处原文包含 OCR 错误和重复，已根据要求清理逻辑流。）

### 系统分区

系统分区的益处包括：

- 硬件隔离
- 开发
- 恢复

### PCI-X

基于 PCI 的成功，企业 X 架构引入了 `Active-X`。

没有系统开销或支持要求；它对操作系统是透明的。因为它在标准的 `ECC DIMM` 上运行，因此您无需为此保护层付费。

- `IBM Chipkill ECC` 内存（在工业标准计算机中已进入第三代）当服务器在短时间内遇到大量错误，导致 `MemoryXion` 无法处理时，`Chipkill` 将派上用场。这应该是一个罕见的情况，但如果确实发生了，您仍然受到保护。与 `MemoryXion` 一样，`Chipkill` 内存的功能远超标准 `ECC` 内存的纠错能力，可以为每个 `DIMM` 纠错 4 位（每个控制器 8 位），无论是在单个芯片还是多个芯片上。此外，与 `MemoryXion` 一样，`Chipkill` 内存控制器的支持，因此它使用标准的 `ECC DIMM` 实现，并对操作系统是透明的。

- 防止故障导致服务器宕机的第三道防线是镜像。如果服务器由于某种方式遇到了大量的错误，以至于 `Memory ProXion` 和 `Chipkill` 无法全部纠正，镜像将保持您的系统运行。内存镜像在概念上的工作原理类似于 `RAID-1` 磁盘镜像（每张卡均独立配置）。

- 热插拔/热拔拔内存允许在服务器运行时更换部件。同样，热插拔支持允许随着内存需求的增加，向运行中的服务器添加新的 `DIMM`。`IBM xSeries` 服务器允许许可的人员根据需要添加新的驱动器、适配器、电源和风扇。现在我们将内存也加入了了该列表。

## Xce4 服务器加速缓存

另一个先进的性能增强功能是巨大的 `L4`（四级）缓存，在基于安腾（`Itanium`）的服务器中，每四路中央电子组件（`CEC`）配备 64 MB 数据传输率（`DDR`）高速 `ECC` 内存，在 `Xeon` 系统中为 32MB。多年前，当微处理器供应商正在寻找提高性能的方法时，排除了使用 `FASTL`，发现在处理器缓存中使用少量高速内存（存储主内存中最频繁访问数据的副本）可以提供相同的性能提升，但成本低得多。从那时起，处理器就包含了内置缓存。

## 激活诊断

可扩展性、性能和经济性都是服务器的重要特征，但预防或最大限度地减少服务器宕机的能力至关重要。`IBM Active Diagnostics` 是工业标准服务器的一项新技术，可以在这方面提供帮助。虽然 `XA-3-64` 芯片没有直接启用，但 `Active Diagnostics` 是另一项 X 架构特性，将整合到使用这些芯片的服务器内存中。

如果您今天在工业标准服务器中寻找这些功能的任何一个，都可以从 IBM 获取。这些服务器为应用提供了灵活性、创新技术以及管理电子商务的新工具。它们为工业标准服务器带来了以前仅供大型机和其他高端系统用户才具备的能力。与现有的 X 架构技术相结合，这些创新实现了基于处理器的服务器前所未有的规模经济，并提升了基于处理器的服务器可用性和性能的新水平。在英特尔架构（`IA`）服务器中，`Linux` 的进化迅速。与其他操作系统相比，来自开源社区的庞大开发环境不断整合了新的驱动程序和功能。自从带有内核 `2.4` 的发行版出现以来，用于英特尔架构服务器的 `Linux` 已被接受为操作系统。虽然完全作为企业操作系统的功能和稳定性在其他平台的市场份额增长很小，但使用 `Linux` 的英特尔架构服务器市场大幅增加。

有关更多关于 `X-Architecture™` 的信息，请访问：

<http://www.pc.ibm.com/us/eserver/xseries/xarchitecture/enterprise/index.html>

## 相关出版物

本节列出的出版物被认为特别适用于对本书（`redbook`）涵盖的主题进行更详细的讨论。

### IBM 红书

有关订购这些出版物的信息，请参见第 91 页的“如何获取 IBM 红书”。注意，此处引用的某些文档可能仅提供副本。

- `Linux Handbook：A Guide to IBM Linux Solutions and Resources, SG24-7000`
- `Implementing Linux with IBM Disk Storage, SG24-6261-01`
- `The IBM TotalStorage Handbook, SG24-5250`
- `Introduction to Storage Area Networks, SG24-5470`
- `Fibre Array Technology - A FASIT Introduction, SG24-6246`
- `IBM TotalStorage FASIT700 and Copy Services, SG24-6808`

## 在线资源

这些网站和 URL 也作为进一步的信息来源与之相关：

- IBM Linux 网站

<http://www.ibm.com/linux/>

- Linux 技术中心

<http://www.ibm.com/linux/ltc>

- IBM TotalStorage 网站

<http://www.storage.ibm.com/>

- IBM TotalStorage SAN fabric 网站

<http://www.storage.ibm.com/ibms/products/sanfabric.html>

- IBM eServer 网站

<http://www.ibm.com/eser>

## 如何获取 IBM 红书

您可以在此网站搜索、查看或下载红书、红皮、提示与技巧（`Hints and Tips`）、草案出版物和补充材料，并订购纸质红书或 `CD`：

<ibm.com/redbooks>

## 来自 IBM 的帮助

IBM 支持与下载

<ibm.com/support>

IBM 全球服务

<ibm.com/services>
