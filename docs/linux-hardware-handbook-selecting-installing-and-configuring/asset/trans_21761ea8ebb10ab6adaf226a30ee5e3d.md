
在当今的 Linux 系统中，SoundBlaster 兼容模式几乎毫无用处。Linux 完全依赖于其自身的原生驱动程序来处理所有声音功能。当然，Linux 确实包含了大多数 SoundBlaster 型号驱动程序，但由于大多数兼容 SoundBlaster 的声卡需要专有命令才能启用 SoundBlaster 模式，因此除非声卡已经初始化在 SoundBlaster 模式下，否则这些驱动程序的作用非常有限。即便在这种情况下，由于大多数兼容 SoundBlaster 的声卡仅模拟 8 位 SoundBlaster Pro，你将无法使用声卡的 16 位功能。

**提示**
如果你拥有一块没有原生 Linux 驱动程序的兼容 SoundBlaster 声卡，你可能可以通过运行 DOS 以及声卡制造商提供的用于启动 SoundBlaster 兼容模式的任何 DOS 实用程序来使其工作。完成此操作后，你可以按 Ctrl+Alt+Del 重启进入 Linux，或者使用 LOADLIN.EXE 直接从 DOS 启动 Linux。如果一切顺利，Linux 将把该声卡识别为 SoundBlaster Pro，你可以将其作为此类设备使用。虽然无法使用 16 位声音功能，但 8 位声音可能优于没有声音。你甚至可能希望设置一个小的（1MB~2MB 应该足够）DOS 启动分区，并在其 AUTOEXEC.BAT 文件中包含对 LOADLIN.EXE 的调用，以便自动启动 Linux。然后，你就可以通过这个小 DOS 分区正常启动 Linux。更好的解决方案是更换声卡，除非它集成在计算机中（例如在笔记本电脑中）。

总之，请忽略你在任何广告或产品包装盒上看到的“SoundBlaster 兼容”字样。相反，应关注声卡使用的芯片组，寻找那些使用 Linux 存在稳定驱动程序的芯片组的声卡。

## 常见的 ISA 芯片组

在 20 世纪 90 年代中后期，ISA 声卡上出现了数十种音频芯片组。这些芯片组中的大多数被多个声卡制造商使用，尽管有些仅被一到两个制造商使用。大多数在 Linux 中都有支持。一些更流行的芯片组制造商和型号包括：

- **AMD**：AMD（http://www.amd.com）生产了一个主要的 ISA 声音芯片组，即 Interwave。该产品包括 Gravis UltraSound 兼容模式，实际上也被用于 UltraSound PnP 型号及其他产品中。
- **Aztech**：20 世纪 90 年代中期，来自 Aztech（http://www.aztechca.com）及其他厂商的许多低成本声卡使用了 Aztech 芯片组，通常命名为 Sound Galaxy 和 Washington。如今 Aztech 产品已不常见。Linux 存在大多数 Aztech 产品的驱动程序。
- **Creative Labs**：Creative Labs（http://www.creative.com）的产品长期以来一直是标准，因此非常常见。Creative Labs 最初使用专供该公司使用的定制芯片组，但 eventually Creative Labs 的 Vibra 芯片组及其后继产品最终出现在了主板上以及一些竞争产品中。Creative Labs 还收购了其他公司，因此一些 Creative Labs 产品使用了其他公司的芯片组。通常来说，Creative Labs 的产品在 Linux 中支持良好，但对于任何特定产品，你都应该检查驱动程序可用性和功能。
- **Crystal Semiconductor**：Crystal Semiconductor（CS；http://www.crystal.com），现在是 Cirrus 的一个部门，长期以来一直是声卡芯片组的主要供应商。CS ISA 系列在 Linux 中支持良好，尽管个别产品有时因各种原因存在问题。
- **ESS**：ESS（http://www.esstech.com）是另一个主要的声音芯片组制造商。ESS 产品是关于 SoundBlaster 兼容性的规则的例外：基于 ESS ISA 芯片组的产品通常使用 Linux 的 SoundBlaster 驱动程序。
- **Gravis**：Gravis（http://www.gravis.com）的 UltraSound 是 SoundBlaster 系列长寿命的竞争者。其独特之处在于不包含 SoundBlaster 兼容性，Gravis 在 UltraSound 中使用了其专有的芯片组。Gravis 后来与 AMD 合作开发了用于 UltraSound PnP 型号的 Interwave 芯片组。Linux 内核包含对 Gravis 产品的支持。
- **IBM**：IBM（http://www.mwave.com）生产了一系列非常精密的数字信号处理器（DSP）芯片，被称为 Mwave。这些产品出现在 20 世纪 90 年代中后期的各种调制解调器/声卡组合卡上，并用于一些 IBM 笔记本电脑。不幸的是，截至 2000 年初，尚未开发出 Mwave 的 Linux 驱动程序，尽管如前所述，可以通过首先运行 Mwave DOS SoundBlaster 初始化程序，使 2000 系列 Mwave 芯片在 SoundBlaster Pro 兼容模式下工作。
- **OPTi**：OPTi（http://www.opti.com）是另一个主要的 ISA 声卡芯片组制造商。与 CS 一样，Linux 包含出色的 OPTi ISA 驱动程序支持。
- **Yamaha**：Yamaha（http://www.yamaha.com）最著名的 ISA 产品是其 OPL2 和 OPL3 FM 合成芯片组以及其 OPL4 FM 合成和波形表芯片组。OPL3-SA 系列是 OPL3 的变种，包含数字音频功能。OPL2、OPL3 和 OPL4 芯片组通常与 CS、ESS、OPTi 或其他公司的芯片组一起用于声卡。Linux 支持所有这些芯片组。

2000 年 ISA 芯片组的发展很温和，因为制造商已将注意力转向日益增长的 PCI 市场。这一事实有利于 Linux 驱动的可用性和稳定性；无需适应不断变化的产品线，Linux 的 ISA 板驱动程序可以成熟并稳定下来。因此，就 Linux 驱动程序支持而言，大多数 ISA 声卡都是不错的选择。

## 常见的 PCI 芯片组

如今，大多数新的声卡设计都实现于 PCI 总线而非 ISA 总线上，原因是我在本章前面已经概述过的。因此，PCI 声卡市场和 Linux PCI 声卡支持都在迅速变化。2000 年可用的一些更常见的芯片组包括：

- **Aureal**：Aureal（http://linux.aureal.com）生产并分发其 Vortex 芯片组的 Linux 驱动程序，但这些驱动程序尚未被整合到 Linux 内核或 ALSA 项目驱动程序中。
- **Creative Labs**：Creative Labs 发布了许多 PCI 声卡，其中一些最初由 Creative 收购的其他公司生产，例如 Ensoniq AudioPCI。Creative 最近一直在积极开发 Linux 驱动程序；你可以在 http://opensource.creative.com 查看最新情况。
- **Crystal Semiconductor**：CS 一直在生产 PCI 芯片组，就像他们生产了许多 ISA 芯片组一样。其中一些产品受到一个或多个 Linux 驱动程序的支持，但你在购买之前应检查特定芯片组的支持情况。
- **ESS**：ESS 生产了多个 PCI 芯片组，其中大多数在 Linux 中都有支持，主要是在 Linux 内核中，也在其他驱动程序中。
- **S3**：S3（http://www.s3.com）生产一种名为 SonicVibes 的 PCI 芯片组，Linux 存在其驱动程序。
- **Trident**：Trident（http://www.tridentmicro.com）以一款名为 4D-Wave 的产品进入了声音芯片组市场，该产品也集成在一些 SIS（http://www.sis.com.tw）主板芯片组中。对该芯片组的支持存在于 2.3.x 系列内核和 ALSA 项目驱动程序中，但不存在于 2.2.x 内核中。
- **VIA**：主板芯片组制造商 VIA（http://www.via.com.tw）在其某些主板芯片组中包含独特的音频功能。该产品受 Linux 内核支持，但截至 2.3.47 内核仅支持 8 位模式。商业 OSS 驱动程序和开源 ALSA 驱动程序提供了更好的支持。

作为一般经验法则，Linux 对 PCI 声卡芯片组的音频支持不如对 ISA 声卡芯片组的成熟和完善。因此，在购买 PCI 声卡之前研究其 Linux 驱动程序尤为重要。

## Linux 音频驱动程序

对于大多数底层硬件设备，驱动程序随 Linux 内核提供，没有其他来源。偶尔，你可能需要寻找开发版驱动程序或硬件制造商以仅二进制形式提供的驱动程序，但大多数情况下，你的

