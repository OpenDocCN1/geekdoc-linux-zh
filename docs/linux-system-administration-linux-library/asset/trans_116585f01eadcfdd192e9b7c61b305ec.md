

## 系统调优

你不需要许多驱动程序。例如，大多数安装并不需要像对称多处理（SMP）或集成业务数字网络（ISDN）等功能的支持。这些“额外”程序会占用内存，损害系统性能。在安装后尽早，你应该重新编译内核，去掉你你不具备的硬件驱动程序，并消除你不会使用的功能。

另一个重新编译的原因是，最近内核允许根据处理器进行优化，但大多数发行版分发的是针对 386 系统优化的内核。为 386 机器开发的内核在性能更强的机器上运行速度会比为该机器处理器编译的代码要慢。如果内核必须在各种机器间具有移植性，你必须为最低配置的处理器类型进行编译，但除此之外，你应该为内核将运行的计算机选择合适的处理器类型。

处理器优化选项的数量正在增加。在内核 2.2.5 时，有五种优化方案可以选择。表 9.1 列出了 2.2.17 内核中可用的优化方案，表 9.2 列出了 2.4.0-test9 内核的优化选项。（可以通过对 2.2.x 内核应用内核补丁来增加它们提供的优化数量，但通常不值得费精力。）

## 表 9.1 2.2.17 内核中的优化方案

| 优化方案 | 处理器 |
|---|--|
| 386 | AMD/Cyrix/Intel 386DX/DX/SL/SLC/SX, Cyrix/TI 486DLC/DLC2 and UMC 486SX-S |
| 486 | AMD/Cyrix/IBM/Intel DX4 or DX2/SL/SX/SX2, AMD/Cyrix 5x86, NexGen Nx586, and UMC U5D or U5S |
| 586/K5/5x86/6x86 | 通用 Pentium 类 CPU，可能缺少 TSC（时间计数）寄存器 |
| Pentium/K6/TSC | Intel Pentium/Pentium MMX, AMD K6 and K6-3D |
| Ppro | Intel Pentium II/Pentium Pro, Cyrix/IBM/National-conductor 6x86MX and MII |

![](img/4fb617eb648f87def380ef5d92052d01_320_0.png)

## 第 9 章 性能调优

## 表 9.2 2.4.0-test9 内核中的优化方案

| 优化方案 | 处理器 |
|---|--|
| 386 | 所有 Intel, AMD 和 Cyrix 386 CPU，以及 Cyrix 486DLC 系列和 NexGen Nx586 |
| 486 | 所有 Intel, AMD 和 Cyrix 486 CPU，以及 UMC U5D 和 U5S |
| 586/K5/x5x86/x86/x86MX | 通用 Pentium 类 CPU，可能缺少 TSC 寄存器 |
| Pentium-Classic | 原版 Intel Pentium |
| Pentium-MMX | Intel Pentium MMX |
| Pentium-Pro/Celeron/Pentium-II | Intel Pentium Pro, Celeron 和 Pentium-II |
| Pentium-III | Intel Pentium-III |
| K6/K6-II/K6-III | AMD K6, K6-2 和 K6-III |
| Athlon/K7 | AMD Athlon (K7)，包括 Duron |
| Crusoe | Transmeta Crusoe 系列 |
| Winchip-C6 | 原版 IDT Winchip |
| Winchip-2 | IDT Winchip 2 |
| Winchip-2A/Winchip-3 | 带 3dNow 能力的 IDT Winchip |

此外，内存容量也是编译新内核时的一个因素。如果你的系统拥有超过 1GB 的内存，你需要开启大内存支持（Big Memory Support）。在提示时，选择 2GB 最大物理内存（而不是默认的 1GB）。

还有许多其他内核参数可以为你带来性能提升。如果你的系统拥有超过 1GB 的内存，你需要开启大内存支持。在提示时，选择 2GB 最大物理内存（而不是默认的 1GB）。

还有许多其他内核参数可以为你带来性能提升。如果你的系统拥有超过 1GB 的内存，你需要开启大内存支持。在提示时，选择 2GB 最大物理内存（而不是默认的 1GB）。

## 优化应用程序

正如内核可以重新编译一样，你也可以优化应用程序。如果你下载了压缩包（tarball），请阅读 README 查看是否有特定的。第 8 章涵盖了其他选项。

## 调优 X 系统

另一个性能问题涉及启动过程，尽管该过程比应的慢得多。什么可以让它变快？如果你观察 startx 命令的输出，你会看到很多这样的行：

- SVGA: Removing (640x400)

这一行表示一种经过检查并确定不符合你的显卡/显示器的模式。该行看起来像：

```

Modeline "640x400" 31.50 640 672 736 832 400 401 445 -hsync -vsync

```

只需在 Modeline 前加一个 # 符号将其注释掉。下次启动 X 时，这些模式将不再被尝试，从而为每个模式节省时间。我们在 X 运行时不会提高性能。

## 窗口管理器和集成环境

窗口管理器和集成环境（IDEs）可以释放内存。其中一些是特定的。我们将在第 16 章讨论。

## 升级

“我什么时候应该升级操作系统？”是一个困扰许多系统管理员的问题。你仅仅因为出了新版本就进行升级吗？你会在有错误修复时升级单个软件包吗？你选择从头开始安装还是执行发行版的升级？

最好的方法是备份系统、重新安装，并将配置文件和用户覆盖到新系统。这起初可能会让你感到不安，因为你不确定是否记回了所有的配置数据；你可能认为会漏了东西。如果你使用安装过程的升级功能，可能永远不会遇到问题。

