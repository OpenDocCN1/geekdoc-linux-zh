
## 可加载模块支持

此组选项询问你关于可加载模块的支持。可加载模块是一块代码，Linux 内核可以加载并执行它，就好像它是操作系统的一部分一样。

- 可加载模块支持
  - 启用可加载模块支持 (`MODULES`) [Y/n/?]
  - 模块卸载 (`MODULE_UNLOAD`) [Y/n/?]
  - 强制模块卸载 (`MODULE_FORCE_UNLOAD`) [N/y/?]
  - 模块版本支持 (EXPERIMENTAL) (`MODVERSIONS`) [Y/n/?]
  - 所有模块的源校验和 (`MODULE_SRCVERSION_ALL`) [Y/n/?]
  - 模块签名验证 (EXPERIMENTAL) (`MODULE_SIG`) [Y/n/?]
  - 必需模块必须有效签名 (EXPERIMENTAL) (`MODULE_SIG_FORCE`) [N/y/?]
  - 自动内核模块加载 (`KMOD`) [Y/n/?]

如果你希望包含模块支持，请对第一个问题回答“是”（Yes），并接受其他问题的默认设置。注意，有一些选项标记为 EXPERIMENTAL（实验性）。只有在你配置会话开始时启用了 EXPERIMENTAL 代码支持时，这些问题才会出现。

## 处理器类型和功能

此组选项用于设置子体系结构类型、处理器家族以及对特定处理器相关功能的支持：

- 处理器类型和功能
- 子体系结构类型
  1. PC 兼容 (`X86_PC`)
  2. AMD Elan (`X86_ELAN`)
  3. Voyager (NCR) (`X86_VOYAGER`)
  4. NUMAQ (IBM/Sequent) (`X86_NUMAQ`)
  5. SGI 320/540 (Visual Workstation) (`X86_VISWS`)
  - 选择(1-5):

子体系结构类型选项允许你从使用 Intel x86 处理器家族的不同类型的基本系统设计中进行选择，但这些设计可能与众所周知的 PC 兼容机有根本区别。在版本 2.6 之前，Linux 内核隐式假设系统架构基于旧的 IBM PC-AT 系列。从内核版本 2.6 开始，你可以为其他类型的基于 Intel x86 的架构构建内核，例如 SGI 图形工作站和具有非均匀内存访问（NUMA）的多处理器系统。你可能可以默认选择 PC 兼容子体系结构，但如果你必须为不同类型的基于 x86 的系统构建内核，其他选项是可用的。

下一组选项提示你选择处理器家族：

1. 386 (`M386`)
2. 486 (`M486`)
3. 586/ES/5x86/6x86/5x86MX (`M586`)
4. Pentium-Classic (`M586TSC`)
5. Pentium-MDX (`M586MMX`)
6. Pentium-Pro (`M686`)
7. Pentium-II/Celeron (pre-Coppermine) (`MPENTIUMII`)
8. Pentium-II/Celeron (Coppermine)/Pentium-III Xeon (`MPENTIUMIII`)
9. Pentium M (`MPENTIUMM`)
10. Pentium-4/Celeron (P4-based)/Pentium-4 M/Xeon (`MPENTIUM4`)
11. K6/K6-II/K6-III (`MK6`)
12. Athlon/Duron/K7 (`MK7`)
13. Opteron/Athlon64/Hammer/K8 (`MK8`)
14. Crusoe (`MCRUSOE`)
15. Efficeon (`MEFFICEON`)
16. Winchip-C6 (`MWINCHIP6C`)
17. Winchip-2 (`MWINCHIP2`)
18. Winchip-2A/Winchip-3 (`MWINCHIP3D`)
19. MediaGX/Gesode (`MGEODEX`)
20. CrixVII/VIA-C3 (`MCYRIXIII`)
21. VIA C3-2 (Nehemiah) (`MVIA_C3_2`)
- 选择[1-21]:

如果你选择 386，编译后的内核可以在任何其他处理器（例如 486 或任何类型的 Pentium）上运行。然而，如果你正在为系统特定的处理器创建内核，请从列表中选择你的处理器类型。

后续选项提示你一系列其他与处理器相关的选项，你可以将它们保留在默认设置中。如果有疑问，你可以按 `?` 阅读每个选项的帮助，并选择适用于你系统的那些。

## 电源管理选项

此组选项涉及管理系统电源，包括高级配置和电源接口（ACPI）、高级电源管理（APM）BIOS 支持以及 CPU 频率缩放。你可以简单地接受这些选项的默认设置。如果你不理解某个选项的含义，按 `?` 获取该选项的帮助。

## 总线选项

这些选项询问你对特定总线的支持：PCI、ISA、EISA、MCA 和 PCMCIA。工业标准结构（ISA）总线曾经是最广泛使用的总线（直到 PCI 总线出现之前）；这种总线用于原始的 IBM PC-AT。微通道结构（MCA）总线是 IBM 的专有总线，最早出现在 PS/2 PC 中。IBM 设计这种总线作为高速总线，但其专有性质阻碍了它在 PC 中的广泛使用。扩展工业标准结构（EISA）总线作为 MCA 总线的替代品出现，其性能与 MCA 相当。EISA 总线未得到广泛使用，因为 EISA 总线外设卡比其 ISA 总线对应物更昂贵。外围组件互连（PCI）总线是最新的高速总线；当前的 PC 使用 PCI 总线，但也提供 ISA 总线插槽，以便你可以继续使用 ISA 卡。

PCMCIA 代表个人计算机存储卡国际协会（Personal Computer Memory Card International Association），这是一个非营利组织，标准化了向笔记本电脑添加存储卡的接口。虽然最初是为存储卡构思的，但 PCMCIA 设备对于笔记本电脑的多种外接设备变得很流行。PCMCIA 设备称为 PC 卡，而术语 CardBus 指的是 PC 卡的电气规范。

通常，你需要内置对 PCI 和 ISA 的支持，并为 PCMCIA 支持构建模块。如果你的系统支持在系统加电运行时添加或移除 PCI 卡，你还可以添加对 PCI 热插拔的支持。

## 可执行文件格式

开启对可执行与可链接格式（ELF）的支持，这是 Linux 中可执行文件和库的标准格式。在 ELF 之前，可执行文件的格式称为 `a.out`（基于 C 编译器生成的可执行文件的默认名称）。在内核版本 2.6 中，你可以构建一个模块以支持旧的 `a.out` 格式。

## 内存技术设备

此类别选项为驻留在内存技术设备（如闪存和随机存取存储器）上的文件系统提供支持。这些文件系统通常用于嵌入式设备。此类别包括多个选项，用于构建支持各种内存设备的内核模块。构建这些模块没有害处，因为如果你的电脑没有适当的内存设备，它们不会被加载。

## 并口支持

如果你使用通过 PC 并口连接的设备（如打印机或并口 Zip 驱动器），这些选项非常重要。对 `并口支持` 和 `PC 风格硬件` 选项回答 `m`，以便将驱动程序构建为模块。

## 即插即用支持

这些选项询问你是否希望在内核中启用即插即用（PnP）支持。如果你启用 PnP 支持，内核会自动配置 PnP 设备（就像 Windows 那样）。启用这些选项。

## 块设备

块设备（如磁盘驱动器）以块为单位传输数据（与键盘不同，键盘一次传输一个字符）。此组选项涉及连接在 PC 并口上的软盘和 IDE（集成驱动器电子学）设备以及其他块设备。

- 块设备
  - 正常软盘支持 (`BLK_DEV_FD`) [**M/n/y/?**]
  - XT 硬盘支持 (`BLK_DEV_XD`) [**N/m/y/?**]
  - 并口 IDE 设备支持 (`PARIDE`) [**M/n/?**]

第一个问题询问你是否需要软盘驱动器支持。因为大多数 PC 都有软盘驱动器，所以你通常回答“是”（Yes）。如果你有通过 PC 并口连接的外部 CD-ROM 或磁盘设备，你应该按 Enter 接受第三个问题的默认设置。某些 IDE 设备使用并口 IDE 适配器——这就是 `PARIDE` 选项所指的内容。

下一组选项用于各种并行 IDE 驱动程序。你可能希望通过可加载模块内置对并口 IDE 设备的支持。这样，如果你需要它们，模块就在那里，但内核不会因为额外的代码而臃肿。

接下来是另一组块设备选项。`BLK_DEV_LOOP` 选项用于回环设备。启用回环设备让 Linux 内核操作存储在单个大文件中的完整文件系统映像。如果你想要挂载 CD 或 DVD 映像（例如，Linux ISO 文件）并在实际刻录 CD 或 DVD 之前检查它，这个选项很有用。

RAM 磁盘支持允许内核使用系统内存的一部分作为能够存储文件系统的磁盘。通常，RAM 磁盘仅在系统启动期间起作用，此时硬盘可能不可用。

如果启动的是 SCSI 磁盘，且未将 SCSI 驱动程序编译进内核，则 RAM 磁盘是必需的。

## ATA/ATAPI/MFM/RLL 支持
