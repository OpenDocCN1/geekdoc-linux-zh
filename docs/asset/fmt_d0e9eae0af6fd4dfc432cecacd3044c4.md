
>要理解争论，有 3 个 init 系统你应该了解：`sysinit`、`upstart` 和 `systemd`。`SysVinit` 真的很老、过时，并且只允许顺序启动系统，也就是说，由其启动的所有服务必须等待前一个服务完成启动过程后下一个才能启动。Both `upstart` and `systemd` are designed to handle the limitations of `init`, and allows for concurrent initialization, that multiple services can start at the same time, as long as they are not dependent on each other, and allows taking advantage of multiple core processing. They allow service to start and shutdown for specific events, such as a network connection up or another service has started. `Upstart` was developed by Canonical was initially released in 2006 and was used in Ubuntu, Debian, Fedora, CentOS, and others. `Systemd` is a much younger system that was initially released in 2011, however, major distros have already migrated to using `systemd` by default.

>Both `Upstart` and `Systemd` are event based, however their architecture and configuration setup are very different and this is where the worrying comes from. If the configurations arent not corrected then systems are behaving differently than what's expected and can lead to issues for many users.

—hitsujitMO (Reddit Inc.) https://www.reddit.com/r/ubuntu/comments/2yeyyi/grab_your_picknofurches_ubuntu_to_systemd/

你可以通过配置和排序启动脚本以及使用 Ubuntu 附带的系统管理实用程序来管理计算机的几乎每个方面以及启动后的行为。在本章中，你将学习如何使用这些启动脚本和系统管理实用程序。本章还提供了有关故障排除和修复可能因软件配置或从系统移除各种类型硬件而出现的问题的建议。

## 开始启动加载过程

Linux 的实际启动加载机制在不同的硬件平台上有所不同（例如 SPARC、Alpha 和 PowerPC 系统），运行 Ubuntu 的基于 Intel 的 PC 通常在产品线中使用相同的机制。此过程传统上是通过 `BIOS` 完成的。`BIOS` 是存储在主板芯片上的应用程序，用于初始化主板上的硬件（并且通常是硬件

## 开始引导加载过程

（连接到主板上）。`BIOS` 使系统准备好加载和运行我们所识别为操作系统的软件。

作为最后一步，`BIOS` 会查找一个名为引导加载程序或引导代码的特殊程序。这段代码中的指令告诉 `BIOS` Linux 内核位于何处、应如何加载到内存中以及应如何启动。

如果一切顺利，`BIOS` 会查找可启动卷，例如软盘、CD-ROM、硬盘、RAM 磁盘、USB 驱动器或其他设备。可启动卷包含一个特殊的十六进制值，该值由引导加载程序（Ubuntu 默认的 `GRUB2`）在引导加载程序代码首次安装到系统驱动器时写入卷中。`BIOS` 会按 `BIOS` 设置中建立的顺序搜索卷（例如，先 USB，然后是 DVD-ROM，最后是硬盘），然后从找到的第一个可启动卷启动。现代 `BIOS` 在选择用于启动系统的设备时允许相当大的灵活性。

### 注意

> 如果 `BIOS` 检测到硬件问题，启动过程会失败，并且 `BIOS` 会通过系统扬声器发出几声蜂鸣。“蜂鸣代码”表示 `BIOS` 遇到的问题的性质。代码因制造商而异，在此阶段启动过程中出现的问题的诊断超出了本书的范围，并且不涉及 Linux。如果您遇到问题，请参阅主板手册或联系主板制造商。了解蜂鸣声的另一个好来源是 www.computerhope.beep.htm。

接下来，`BIOS` 会在可启动卷上查找第一个硬盘的分区引导扇区（也称为主引导记录 `MBR`）中的引导代码。`MBR` 包含引导加载程序代码和分区表；你可以把它想象成一本书的索引，几条关于如何开始阅读书的注释。如果 `BIOS` 找到引导程序，它会将引导代码加载到内存中。此时，`BIOS` 的工作已完成，并将系统控制权传递给引导加载程序。

随着计算的发展，由于其局限性，`BIOS` 成为限制因素，很难克服。英特尔在 20 世纪 90 年代末开发 Itanium 系统时首先注意到了这一点。这最终成为统一可扩展固件接口（`UEFI`）的基础。

`UEFI` 在大多数现代系统中发挥着与 `BIOS` 类似的作用，并取代了 `BIOS`。对于大多数用户来说，区别可以忽略不计，除非您使用的是 `UEFI` 计算机，在这种情况下，您可能需要做一些研究来安装 Ubuntu。`UEFI` 固件通常允许固件像传统 `BIOS` 一样工作，并且兼容性更好，特别是如果您将 Ubuntu 安装为计算机上唯一的系统而不是双启动。早期存在一些重大问题，但随着 Linux 社区对 `UEFI` 了解更多并使其更易于兼容，这些问题似乎有所减少。要了解更多信息，特别是如果您遇到困难，请参阅 https://help.ubuntu.com/community/UEFI。

使用 `UEFI` 的一个有趣方面是硬盘分区。当 `UEFI` 与 Windows 8.x 或 10 一起使用时，分区是使用 `GPT`（GUID 分区表）而不是现有的 `MBR` 标准设置的。您可以在 Ubuntu 上使用 `GPT`，但如果只在驱动器上安装 Ubuntu，通常更容易将硬盘格式化为 `MBR`。对于 `BIOS` 和 `UEFI`，大多数人不需要知道或关心他们使用的是 `MBR` 还是 `GPT`。要了解更多信息，请参阅 http://www.hotgeek.com/193669/what-the-difference-between-gpt-and-mbr-when-partitioning-a-drive/

引导加载程序在磁盘上定位 Linux 内核并将其加载到内存中。任务完成后，引导加载程序将系统控制权传递给 Linux 内核。你可以看到一个过程如何建立在一种方法之上，使许多不同的操作系统能够在同一硬件上工作。

Linux 非常灵活，可以从 CD-ROM 上的多个映像启动，也可以通过网络使用 `UEFI`（发音为“pixie”）或 `NetBoot` 启动，或在无头服务器上启动，控制台显示通过串行或网络连接发送。`coreboot.org` 甚至正在进行创建特殊 Linux `BIOS` 的工作，以加快启动过程，因为 Linux 不需要典型 `BIOS` 提供的许多服务。

这种灵活性使 Linux 可以以多种方式使用，例如用于远程服务器或工作站，这些通常不会在个人家庭使用中看到。

## 加载 Linux 内核

从广义上讲，内核管理系统资源。作为用户，您通常不会与内核交互，而是与您使用的应用程序交互。Linux 将每个应用程序称为 *process*，内核为每个进程分配一个称为进程 ID（`PID`）的编号。传统上，内核加载并运行名为 *init* 的进程，它也被称为“所有进程的祖先，因为它启动每个子进程”。这些选项最初是 `SysVinit`。它已被更新的选项取代。其中一个是 `Upstart`，由 Ubuntu 开发者编写，可用于任何发行版。`Upstart` 在 Ubuntu 15.04 中被 `systemd` 取代。本章将介绍传统的 `SysVinit` 方法，然后提供有关 `Upstart` 和 `systemd` 的详细信息。

启动过程的下一步传统上以一条消息开始，表明 Linux 内核正在加载以及每个命令的状态。失败时应显示错误消息。*quiet* 选项可在启动时传递给内核以抑制其中许多消息。Ubuntu 默认不显示这些消息，而是使用由 Fedora/Red Hat 开发者创建的名为 `Plymouth` 的启动过程，该过程速度快并包含漂亮的启动屏幕。

## 系统服务和运行级别

`init` 命令将 Linux 系统引导到特定的系统状态，通常称为其运行级别。

运行级别决定启动哪些可用的系统服务，以及它们的启动顺序。特殊运行级别用于停止系统，另一个特殊运行级别用于系统维护。正如您将看到的，还有其他运行级别用于特殊目的。

您传统上使用运行级别来管理在 Linux 计算机上运行的系统服务。所有这些文件和脚本都在安装期间设置，但您可以手动更改和控制它们。
