
通常情况下，只要 CPU 符合操作系统的架构要求，Intel CPU 是用于任何 x86 操作系统的稳妥选择。在 2000 年初，Pentium III 用于中端和高端系统，而 Celeron 用于低价入门级电脑。早期的 x86 型号很难找到。

2000 年 Intel CPU 系列的发展可能包括总线速度（CPU 与主板接口的速率）从 100MHz 增加到 133MHz，并且核心速度很可能会超过 1000MHz (1GHz)。Intel 可能会为包含这些更改的 CPU 应用 Pentium IV 的名称。Intel 还在准备发布一种真正的 64 位 CPU，该 CPU 应该与书中讨论的 32 位操作系统兼容。为了充分利用这种 CPU，需要新的操作系统——或至少是现有操作系统的变体。

AMD 电子设备（AMD; `http://www.amd.com`）是 x86 时代 Intel 最大的竞争对手。Intel 最初将其 x86 CPU 的设计授权给 AMD，以获得要求所有产品都需要第二供源的合同。后来，Intel 撤销了该许可，迫使 AMD 独立开发名为 K5 的 x86 核心 CPU。AMD 随后购买了一家较小的公司 NexGen，并使用其技术作为 K6 以及后续 AMD CPU 的基础。K6 系列 CPU 继续使用类似 Pentium CPU 的插槽式设计，这种设计生产成本较低，但产生的 L2 缓存性能低于 Pentium II 及后续 CPU 使用的设计。Athlon 是一种专有的插槽设计，其历史和特性在表 21.3 中概述。

## CPU 速度要求

### 表 21.3 AMD CPU 特性

| CPU | 特性 | Intel CPU 的直接替换 |
|---|---|---|
| 80386 & 80486 | 与同名 Intel CPU 几乎一致的克隆版本 | 同名的 Intel CPU |
| K5 | 类似 Pentium 的性能 | Pentium |
| K6 | 性能接近 Pentium II 水平，但使用旧款主板类型；MMX | Pentium MMX |
| K6-2 | 比 K6 速度更快 | Pentium MMX |
| K6-III | 比 K6-2 速度更快 | |
| Athlon | 比 K6-III 速度更快；CPU 封装上带有 L2 缓存 | 无；使用 Alpha EV6 接口 |

1999 年，最快的 x86 系统基于高端 Athlon CPU 构建。Athlon 和 Intel 的 Pentium III 都值得在高端系统考虑。在我写这些的时候，K6 系列对于低端系统仍然值得考虑，但这种情况可能不会持续到 2000 年。AMD 预计将在 2000 年突破 1GHz 的速度障碍。

在操作系统兼容性方面，AMD 的系列与 Intel 相当。当然，你不应该尝试在性能不足的 AMD CPU 上运行具有高 CPU 要求的操作系统（例如 Windows 2000），但只要你的 AMD CPU 等于或优于操作系统制造商列出的 Intel CPU，就没问题。我已经使用直到 K6-2 的 AMD CPU 运行了书中讨论的大多数操作系统。然而，Athlon 在某些操作系统上确实存在安装问题；如果你在使用 Athlon 时遇到问题，请检查操作系统制造商的更新。例如，SuSE Linux 6.2 (`http://www.suse.com`) 有一个更新的安装软盘，用于修复在 Athlon 系统上安装的故障。这些问题在较新的 SuSE Linux 6.3 版本中得到了修复。

VIA（`http://www.via.com`）长期以来一直是主板和其他组件芯片组的制造商。1999 年，VIA 购买了 Cyrix 和 IDT 的 x86 CPU 设计。VIA 继续进行 CPU 开发，其最新产品基于旧 Cyrix 设计的扩展。Cyrix 和 IDT（因此现在的 VIA）为它们的 CPU 使用独特的设计，但它们实现了与 Intel x86 CPU 相同的特性，并兼容 x86 操作系统和软件。表 21.4 总结了 VIA、Cyrix 和 IDT CPU 家族。

### 表 21.4 VIA/Cyrix/IDT CPU 特性

| CPU | 特性 | Intel CPU 的直接替换 |
|---|---|---|
| Cyrix 80386 & 80486 | 与同名 Intel CPU 几乎一致的克隆版本。SL 型号是精简版，以适应上一代主板。 | 同名的 Intel CPU |
| Cyrix 5x86 | 增强版的 486 | |
| Cyrix 6x86 | 实现了与 Intel x86 CPU 相同的特性。 | |
| Cyrix 6x86-3 | 比 686 速度更快。 | |
| IDT WinChip | 兼容 x86 操作系统。 | |
| VIA WinChip | CPU 的独特设计。 | |

### 21 资源

| CPU | 特性 | 操作系统最低要求 |
|---|---|---|
| Pentium | 速度增强和额外指令；64 位数据线，但内部仍为 32 位 | Windows 2000; BeOS 4.x |
| Pentium MMX | 带有多媒体扩展的 Pentium | |
| Pentium Pro | 对 32 位代码有优化的 Pentium；无 MMX；64GB 内存限制；CPU 封装上带有 L2 缓存 | |
| Pentium II | 带有 MMX 和速度增强的 Pentium Pro | |
| Pentium III | 带有速度增强的 Pentium II | |
| Celeron | CPU 封装上没有或 L2 缓存较小的 Pentium II（带缓存的模型以核心速度而非总线速度运行） | |
