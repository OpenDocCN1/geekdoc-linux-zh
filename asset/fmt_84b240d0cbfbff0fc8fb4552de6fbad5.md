
有什么建议吗？如果你只想偶尔运行 Windows 应用程序，请使用 `VirtualBox`。如果你想在桌面系统上尝试复杂的虚拟化技术，请尝试 `KVM`。如果你可以使用 `Xen`（遗憾的是本章没有讨论它，但有很多关于 `Xen` 的优秀书籍，其中一本由本作者编写 [Professional Xen Virtualization, Wrox, 2008, ISBN: 0470138114]）。如果你需要运行 Windows 虚拟机并且拥有 Intel VT 或 AMD-V 处理器，可以使用 `KVM` 或 `Xen` 运行虚拟机，利用你的处理器提供的硬件虚拟化支持。

## Linux 常用模拟软件

对于大多数系统，最著名的模拟软件包根本不是桌面模拟器——它是多游戏机模拟器（`MAME`: `.mame`, `.net`），它能够直接从只读存储器镜像中运行各种古老视频游戏
(ROM) 芯片——街机视频游戏是我对计算机感兴趣的动力。尽管事实证明系统管理对我来说更有趣，但通过 `MAME` 玩一些古老的视频游戏非常有趣，`MAME` 技术简直令人惊叹。关于 `Xen`，即这些游戏 ROM，它们存在一些法律问题，因为它们在技术上仍然属于原始制造商——在从成百上千运行它们的网站下载任何 ROM 之前，你应该先对这些进行调查。然而，我已经丢失了许多 ROM 的版权，而且我的客厅里确实有一台“中心节虫（Centipede）”街机，所以我对此并不觉得太糟糕。Ubuntu 存储库中提供了多种 `MAME` 软件包——通常只需要安装基础的 `xname-x` 包即可，它包含了 `MAME` 的 X Window 系统二进制文件。`xname-sd1` 软件包稍微现代一些，但它默认会接管你的屏幕，这可能会让人不安（而且 `Compiz` 无法从中恢复）。如果你想简化从 `MAME` 文档中确定 ROM 镜像放置于何处的过程，那么用于该包的许多端程序（如 `gameui`，用于 GNOME 桌面）会非常方便。

如果你真的想用模拟器做些事情，Linux 圈中最实用的模拟器是 `QEMU`，它可以模拟许多不同的平台和相关硬件。`QEMU` 不仅是一个优秀的独立模拟器，开源虚拟化软件包（如 `Xen`、`VirtualBox` 和 `KVM`）也使用了 `QEMU` 的大部分代码，以避免在控制台模拟、图形模拟等方面重复造轮子。

今天有大量的模拟器可用，特别是许多人想要重温青春的光辉（或至少是他们运行过的系统）。与其试图让一台来自已倒闭厂商、有 20 年历史的个人电脑复活，编写一个模拟器可能很有趣，对其他对硬件感兴趣的人也很有用，并提供了一个有趣的技术挑战。在互联网上搜索 Linux 模拟器会返回成百结果的结果。两个特别好的总结页面是 Zopher 的 UNIX/Linux 模拟器页面（www.zopher.net/linux.html）以及位于 www.usinglinux.org/emulators/ 上的 Using Linux 总结。

# 管理虚拟机和模拟机

正如本章讨论过的，`VirtualBox` 和 `VMware Server` 等虚拟化软件包提供了一个图形化虚拟化控制台，可以轻松地配置、管理和切换你使用这些技术已配置并可以运行的虚拟机。然而，这些管理控制台仅对相关类型的虚拟机有效。许多软件包正在开发中，旨在为使用多种虚拟化技术创建的虚拟机提供单一的管理、创建和执行框架。其中广为人知的虚拟机管理器（Virtual Machine Manager），它在 Ubuntu 存储库中以 `virt-manager` 软件包的形式提供。有关虚拟机管理器的更多信息，请访问其主页 http://virt-manager.et.redhat.com。

# 第 24 章：使用虚拟机和模拟器

本章侧重于不同类型虚拟机的手动配置、创建和管理，而不是使用图形化管理包。其主要原因如下：

- 虚拟机管理器仅支持 `KVM`、`QEMU` 和 `Xen` 虚拟机，但 `VirtualBox` 或 `VMware` 等虚拟化技术可能更符合你的需求。
- 如果你计划在服务器环境中使用 `KVM` 或 `Xen` 等虚拟化技术，可能没有图形用户界面，在这种情况下，你无法使用虚拟机管理器。
- 和大多数图形化工具一样，虚拟机管理器旨在简化其主体领域的配置、执行、管理和监控（在本例中即虚拟机）。如果你刚开始接触虚拟化并计划在 SOHO 企业环境中使用它，那么理解与虚拟化相关的系统级配置更改和底层程序，特别是网络配置是非常重要的。

虚拟机管理器是一个非常棒且非常有用的软件包。然而，在我看来，了解内部运行机制并专注于与特定虚拟化技术相关的创建和管理工具，能为开始虚拟化提供更好的基础。如果这让你失望，我很抱歉。

Ubuntu 存储库中提供的其他虚拟化管理工具包括用于 `Xen` 虚拟机的 `quenman` 软件包，以及用于管理 `QEMU` 虚拟机的 `qemu-launcher` 等软件包。

# 获取更多关于虚拟化的信息

Ubuntu 网站提供了关于 Ubuntu 虚拟化的通用信息、Canonical 在商业虚拟化领域的模式等。讨论特定虚拟化解决方案的章节将提供有关该特定解决方案附加信息的线索。你可以在以下位置获取有关 Ubuntu 系统虚拟化的额外通用信息：

- Ubuntu 虚拟化概览 (www://ubuntu.com/products/server/edition/technologies/virtualization)：这是 Canonical 对 Ubuntu 基础虚拟化选项的企业描述。遗憾的是，这并不意味着 `VirtualBox` 和 `Xen` 等东西！幸运的是，它指向了社区文档页面（此列表中的 Ubuntu 社区虚拟化概览页面）。
- Ubuntu 社区虚拟化概览 (https://help.ubuntu.com/community/Virtualisation)：关于 Ubuntu 上不同虚拟化解决方案信息的 Ubuntu 社区文档“首页”。

### 第二部分：面向桌面用户的 Ubuntu

如果你对虚拟化普遍感兴趣并想获取更多信息，有许多网站提供了关于通用硬件上虚拟化和模拟的通用信息。以下是我最喜欢的几个：

- IBM developerWorks: “虚拟化 Linux: 虚拟化方法、架构和实现概述” (https://www.ibm.com/developerworks/linux/library/1-linuxvirt/)：如果你对 Linux 系统上虚拟化的通用信息感兴趣，这是一篇非常棒的文章。IBM 的 developerWorks 总是提供大量详尽、技术准确的信息。这篇文章对 Linux 上的虚拟化提供了良好的概述和解释，并附有许多其他网站的链接。
- Linux 虚拟化 Wiki (http://virt.kernelbies.org)：这是一个很好的网站，提供了 Linux 虚拟化的良好概述以及对 Linux 虚拟化技术的更详细的讨论。它还对管理 `Xen` 虚拟机的各种工具进行了很好的介绍，并对各种 x86 Linux 发行版（以及其他操作系统，如 OpenSolaris）中提供的 `Xen`（以及其他）虚拟化支持进行了良好的概述。
- SearchServerVirtualization (http://searchservervirtualization.techtarget.com/)：这是一个优秀的 TargetSite，提供了关于服务器虚拟化、相关虚拟化主题等大量信息。该网站的优势之一是许多供应商在上面发布论文和商业公告，这对于跟踪商业虚拟化产品的动态非常有用。
- TheFreeCountry (www.freecountry.com/emulators/index.shtml)：“免费模拟器和虚拟机”是对基于 Intel x86（及兼容）机器的免费模拟和虚拟化软件的很好的总结。这是一个极好的资源，但请记住免费并不意味着开源。
- Wikipedia (www.wikipedia.org)：维基百科关于 `Xen` (http://en.wikipedia.org/wiki/Xen)、通用虚拟化 (http://en.wikipedia.org/wiki/Virtualization)、模拟 (http://en.wikipedia.org/wiki/Emulation) 以及今天虚拟化市场上大多数其他术语和参与者的广泛文章。维基百科是一个信息来源，如既往——尽管它是公开编辑的，任何人都可以添加他们想要的内容。

# 安装和使用 VirtualBox

`VirtualBox` (www.virtualbox.org) 是一个开源的客操作系统虚拟化软件包，可以运行并托管 32 位和 64 位操作系统，如 Linux、BSD、Solaris 和 Microsoft Windows 系统。`VirtualBox` 本身运行在 Linux、Mac OS X（仅限 Intel）、Solaris 和 Microsoft Windows 系统上。`VirtualBox` 是一个最初由开发的应用程序

## 第 24 章：使用虚拟机和仿真器

InnoTek Systemierung GmbH (www.innotek.de/) 是一家位于德国斯图加特的软件公司，被太阳微系统（www.sun.com）收购。`VirtualBox` 与其他 Linux 虚拟化软件包一样，利用开源 `QEMU` 仿真器来提供某些基础控制台和输入支持；
