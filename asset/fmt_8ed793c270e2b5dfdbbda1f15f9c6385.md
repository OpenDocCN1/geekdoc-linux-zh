
由 Intel 发明的 `x86` CPU 架构是目前桌面电脑中最受欢迎的。所有运行 `Windows 9x` 操作系统的电脑都使用 `x86` CPU。`x86` 这个名字源自 CPU 名称的缩写。在 20 世纪 80 年代和 90 年代初，Intel 的 CPU 都以数字命名，例如 `80286` 和 `80386`。`x86` 系列 CPU 之间的差异仅在于中间的数字，因此 `80x86` 成为了整个系列的缩写，这个缩写后来又进一步简化为 `x86`。缩写 `i386` 有时用于指代 `80386` 及后续的 CPU。

Intel `x86` CPU 极受欢迎——如此受欢迎，以至于在过去，多家公司生产过 `x86` 兼容 CPU，而目前仍有三家公司（`AMD`、`VIA` 和 `Transmeta`）继续这样做。`x86` CPU 系列——或者更准确地说，`80386` CPU——是 Linux 最初编写时所针对的 CPU。如今大多数 Linux 电脑都运行在 `x86` 硬件上，因此本书的大部分篇幅都集中在 `x86` 电脑上使用的硬件，尽管本书的许多内容也适用于其他架构。事实上，本章的大部分篇幅都献给了 `x86` CPU。

`x86` CPU 系列是大多数用户的不错选择；它提供的性能对于大多数桌面和服务器应用程序来说都绰绰有余。由于其普及程度，`x86` 硬件价格低廉，且该硬件的周边设备也非常常见。一个缺点是，许多 `x86` 周边设备质量较低，因此你需要懂得足够的知识来避开那些劣质产品——借助本书的帮助，这项任务应该会轻松很多。`x86` 硬件通常也不是现有硬件中最快的，特别是在浮点运算方面，因此如果你希望使用计算机进行非常苛刻的科学或工程模拟、图形渲染或其他高性能任务，`x86` 可能并不适合。

### Alpha

数字设备公司（`DEC`）开发了 `Alpha` CPU，用于高性能工作站和服务器。在推出时，`RISC` 架构的 `Alpha` CPU 比 `x86` CPU 更快，但由于缺乏软件支持，`Alpha` CPU 在获取市场份额方面一直很艰难。当 `DEC` 倒闭后，康柏（`http://www.compaq.com`）接管了 `Alpha` CPU 生产线，并继续销售 `Alpha` CPU 和电脑，包括预装 Linux 的选项。

如果你希望使用 Linux 进行高性能计算，`Alpha` CPU 是一个不错的选择。当前的 `Alpha` CPU 比最好的 `x86` CPU 更快，而且 Linux 的 `Alpha` 移植版本在此类系统中表现稳定且支持良好。事实上，电影《泰坦尼克号》中的特效就是用一群运行 Linux 的 `Alpha` 架构计算机完成的。

`Red Hat`（`http://www.redhat.com`）主导了 `Alpha` CPU 的 Linux 发行版，不过你也可以找到其他的 `Alpha` 发行版，其中最著名的是 `Debian GNU/Linux`（`http://www.debian.org`）。这两个发行版都非常稳定。

### SPARC

`SPARC` CPU 系列最常见于 `Sun` 的工作站。这些电脑自带其 `UNIX` 变体（`SunOS` 或 `Solaris`）。尽管有此事实，Linux 爱好者仍将 Linux 移植到了该架构上——部分原因是他们喜欢 Linux，部分原因是为了避免费用授权费，还部分原因是，正如攀登珠穆朗玛峰一样，面对挑战本身就是一种奖励。

`SPARC` 架构包括 32 位和 64 位 CPU，Linux 在这两种架构上都能运行。64 位 CPU 内部使用两倍的位数来表示数值，这可以加快大数值的处理速度。`SPARC` 处理器速度非常快，使得 `SPARC` 硬件成为 CPU 密集型工作的良好选择。

你可以在 `http://www.ultralinux.org` 了解更多关于 `UltraLinux` 项目（该项目托管 `SPARC` CPU 系列的 Linux 开发）的信息。`Red Hat`（`http://www.redhat.com`）有一个适用于 `SPARC` 处理器的 Linux 发行版，`Debian`（`http://www.debian.org`）也有。

### PowerPC

`PowerPC` CPU 是 `Apple`、`IBM` 和 `Motorola` 合作的成果。该 CPU 系列主要用在 `Macintosh` 电脑上，但 `IBM` 和 `Motorola` 也在部分计算机中使用了 `PowerPC` CPU，还有一些其他计算机也在使用。总体而言，如果你想使用 `PowerPC` CPU，通常必须购买一台 `Macintosh`。

> **注意**
>
> 早期的 `Macintosh` 使用 `Motorola 680x0` 系列 CPU。然而，基于 `680x0` 的 `Macintosh` 已经多年停止生产，因此你购买的任何新 `Macintosh` 都将使用 `PowerPC` CPU。如果你正考虑购买二手 `Macintosh` 或为一台已有的 `Macintosh` 使用 Linux，你必须确认它是 `680x0` 还是 `PowerPC` CPU。虽然两种 CPU 都有可用的 Linux，但 `PowerPC` 的发行版更加成熟。

`PowerPC` 采用 `RISC` 架构，速度相当快，特别是在浮点运算方面。在 2000 年初，最新的 `PowerPC` CPU（`G4` 系列）性能超过了最好的 `x86` CPU，尽管优势幅度不大，不足以说购买 `x86` CPU 是不明智的选择。在 Linux 支持方面，有多个发行版适用于 `PowerPC` 计算机：

*   [LinuxPPC](http://www.linuxppc.org)
*   [Yellow Dog Linux](http://www.yellowdoglinux.com)
*   [Debian GNU/Linux](http://www.debian.org)
*   [SuSE Linux](http://www.suse.com)

`LinuxPPC` 和 `Yellow Dog` 发行版都紧密基于 `Red Hat Linux`。`Debian` 和 `SuSE` 既生产在 `x86` 平台上流行的发行版，也提供 `PowerPC` 版本。

曾经，`Apple` 资助了 `MkLinux` 的开发，这是一个 `PowerPC` Linux 发行版，除了标准的 Linux 内核外，还使用了 `Mach` 微内核。然而，`MkLinux` 的开发已基本停止，因此我建议你尽可能使用 `PowerPC` 硬件上的其他 Linux 发行版。

在尝试在 `PowerPC` 系统上安装 Linux 之前，确认系统的兼容性至关重要。`ROM`、主板特性、周边设备等方面的差异会导致特定的 `PowerPC` Linux 发行版在硬件支持方面存在缺口。

### 其他架构

上述的只是当今桌面电脑上最流行的一些 CPU。不过，还有其他 CPU，包括：

*   **掌上电脑 CPU**
    Linux 已被移植到几种用于掌上电脑的 CPU 上，例如 `Psion` 电脑中使用的 `ARM` CPU（`http://www.calcaria.net`）、许多 `Windows CE` 掌上电脑中使用的 `NEC VR` 系列 CPU（`http://www.linuce.org`），甚至 `3COM PalmPilot`（`http://www.uclinux.org`）。这些移植中的一些也可以用于嵌入式设备——即内置于手机、工业机器人等中的计算机。

*   **稀有的桌面和工作站 CPU**
    Linux 可用于早期 `Macintosh`、`Amiga` 和 `Atari ST` 中使用的 `680x0` 系列（`http://www.linux-m68k.org`），某些 `Apollo` 工作站中使用的 `PA-RISC` CPU（`http://www.linux.esiea.fr/APOLLO/`），某些 `DECstation` 计算机中使用的 `MIPS` CPU（`http://decstation.unix-ag.org`），以及其他类型。

*   **大型机**
    甚至有一个项目正在让 Linux 在大型机上运行（`http://www.acude.org/roam.htm`），尽管进展不大。

你可以在 `http://www.linux.org/projects/ports.htm` 找到许多 Linux 移植项目的链接。除非 CPU 特别老旧或罕见，否则很可能有一个项目正在将 Linux 移植到该 CPU 上——或者该任务已经完成。在大多数情况下，我不建议你以运行 Linux 为目标去寻找这些特殊的系统。除非你找到了真正的 bargains，否则在 `x86` 系统上运行 Linux 的成本会更低；或者一台 `PowerPC`、`SPARC` 或 `Alpha` 工作站也能提供足够的计算能力。如果你有非常强的 CPU 需求，可以研究一下 Linux 集群，即由多台通过快速网络技术互联的 Linux 计算机组成，以产生超级计算机级别的计算能力。正在研究此项技术的一个组织是 `Beowulf Project`（`http://www.beowulf.org`）。

CPU 领域一个潜在的重要发展是 Intel 新的 64 位芯片，即 `Itanium`。这款 CPU 在 2000 年是全新的，虽然它与早期 Intel `x86` CPU 向后兼容，但它引入了大量新功能，这些功能只能由新操作系统——或旧操作系统的新版本——使用。Intel 一直与 Linux 内核程序员合作，确保 Linux 能够迅速且轻松地适应新 CPU。

### x86 CPU 的世代
