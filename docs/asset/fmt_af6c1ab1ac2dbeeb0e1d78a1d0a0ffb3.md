
`-P` 表示使用特权端口。将 `jukebox.linxtoys.net` 和 `/var/music` 分别替换为服务器名称和共享目录。用户现在可以通过 Mac OS X 客户端上的 `/Users/chris/music` 目录访问 `/var/music`。

# 第 26 章：将 Fedora 与 Apple Mac 集成

## 在基于 Intel 的 Mac 上安装 Fedora

最新的苹果计算机采用了基于 Intel 的计算机架构。Fedora 项目已经增强了 Fedora，使其能够安装在这些新的 Apple 硬件上（单独安装或与 Mac OS X 双启动）。你可能想在其中一台“Macel”计算机上安装 Fedora 的原因包括：

- 双启动 —— 你可能为自己或家人保留了 Mac OS X 桌面（Aqua）和专有应用程序（如 iPod 或 iTunes）。然而，你可能想要访问服务器应用程序、管理工具、开发环境，或通过 Fedora 获取的数千个免费应用程序。
- 仅使用 Fedora —— 虽然你为 Apple 硬件支付了溢价（尽管没有以前那么贵），但你可能足够喜欢这些可爱苹果计算机的外观和功能，愿意多花钱将其作为你的主桌面电脑。

本节介绍了如何从一台基于 Intel 的 Apple Mac 计算机开始（我为此使用了一台 Mac Mini），并将其配置为 Mac OS X 双启动或单独运行 Fedora。

> 警告：在基于 Intel 的硬件上安装 Fedora 仍然是 Fedora 社区的一项实验性技术。某些硬件组件仍然需要额外的调整，或者根本无法工作。如果你无法承受磁盘被清空并必须从头开始重新安装的，我建议你不要这样做。

## 在你的 Mac 上安装 Fedora 之前

首先提醒一下，此过程仅适用于基于 Intel 架构的 Apple Mac 计算机。我在这台新的 Mac Mini（Core Duo CPU，512MB RAM）上运行了此过程。此过程应适用于 iMac、MacBook、MacBook Pro 或 Mac Pro。由于 Leopard 之前的 Mac 版本不再提供 Boot Camp，因此没有官方方法可以调整你的磁盘大小以允许创建多个分区。然而，从理论上讲，你应该可以使用支持 HFS+ 调整大小的分区工具来准备磁盘，以便在 Mac OS X 旁安装 Fedora。如果你决定尝试，结果概不保证成功。

## 安装 Fedora

Mac OS Leopard 提供了一个名为 Boot Camp 的软件，可用于调整硬盘大小。在 Leopard 发布之前，Boot Camp 的测试版本已经可用。以下步骤描述了如何更新固件、调整磁盘大小并安装 Fedora。

> 注意：在开始此步骤之前，请**备份任何重要数据**！存在导致机器无法启动的风险。此过程不适用于 PowerPC 架构的 Mac。

- 1. **检查固件更新** —— 更新你的 Mac OS X 系统。请参考 Apple 更新页面获取有关如何进行操作的信息。
- 2. **运行 Boot Camp** —— 启动 Boot Camp 助理（位于“实用工具”文件夹）。由于你使用 Boot Camp 的目的是调整 Mac，请跳过刻录 Mac CD 的请求。然后移动滑块以选择为 Mac OS X 分配多少磁盘空间，为 Fedora 分配多少（我选择创建一个 10GB 的分区）。
- 3. **插入 Fedora DVD** —— 分区完成后，不要按照要求插入 Windows 安装光，而是插入 Fedora 安装光或 DVD 并点击“重启 Mac OS X”以重启计算机。当计算机重启时，你会看到 Fedora 启动界面。
- 4. **安装 Fedora** —— 开始正常的 Fedora 安装（如第 2 章所述），有几点注意：
  - 分区：Fedora 安装程序的默认分区应能正常工作（保持你的 Mac HFS+ 分区不变，并使用剩余空间创建一个 Fedora `/boot` LVM 分区）。
  - 引导加载程序：同样，安装程序应该执行正确的操作，并将引导加载程序安装在 Fedora 分区而不是主引导记录（MBR），通常情况下是如此。（引导加载程序不能安装在整个磁盘的主引导记录中，否则磁盘将无法启动）。
- 5. **重启并按 Alt 键** —— Fedora 安装完成后，重启。当你看到 Boot Camp 菜单时，选择 Alt 键并住电脑以启动到 Fedora。使用 Fedora 的默认启动项。

因为尝试更改 GRUB 启动标签可能会导致电脑死机。
（顺便说一下，如果你的 DVD 卡卡在驱动器里，重启时按住鼠标按钮，DVD 就会弹出。）

请记住，在基于 Intel 的 Mac 上安装 Fedora 仍然被视为实验性操作。
偏离默认设置（分区、引导加载程序等）越少，在你的 Mac 上成功运行一个可用的 Fedora 系统的机会就越大。

如果你遇到问题，我建议你参考 Fedora 项目的 Fedora On Mactel 页面（http://fedoraproject.org/wiki/FedoraOnMactel）。其他 Linux 项目也提供了资源，可以使 Linux 在 Intel Mac 架构上启动。

### 总结

由于 Darwin（一种类 UNIX 操作系统）是 Mac OS 操作系统系统的核心，原生的 Linux 和 UNIX 网络服务器可以通过多种方式轻松连接到这些新的 Mac。Mac OS X 可以利用从 Linux 服务器通过 `Samba`（Windows 文件/打印机共享）和 `NFS`（UNIX 文件/打印机共享）共享的文件。

你不仅可以使用原生的 Linux 特性，还可以使用 `netatalk` 软件包将 Linux 配置为像 AppleTalk 文件和打印机服务器。通过 `netatalk`，你可以建立多个文件服务器，并使用各种密码和权限技术保护它们共享的卷（目录）。随着苹果最近转向基于 Intel 的架构，你现在可以在 Intel Mac 电脑上安装 Fedora。你可以选择让 Fedora 接管整台电脑，或者将 Fedora 设置为与 Mac OS X 双系统。

# 附录 A

## 关于介质

如果你在标准 PC（32 位 i386 架构）上带有 CD-ROM 或 DVD 驱动器，你可以可以使用随附的介质安装 Fedora 11。这些介质包括：

- **Fedora 11 安装 DVD** —— 这是官方的 Fedora 11 安装版现场 DVD。它代表了 Fedora 7 之前的版本中所谓的 Fedora Core 和 Fedora Extras 的结合。
- **Fedora 11 Live/Install 桌面 CD** —— 这是该项目的任何一个启动 CD。无论你的电脑硬盘上安装了什么内容，它都会启动到带有各种应用程序的 GNOME 桌面。你可以通过从启动 CD 桌面启动安装程序图标，将此 CD 的内容安装到硬盘。如果已经安装了软件，你可以从在线仓库安装任何其他软件。

如果你有一个同时支持 DVD 和 CD 的驱动器，请使用 DVD 安装 Fedora。它提供了更多软件选择选项，并且不需要访问在线仓库即可获得基础桌面系统以外的内容。然而，对于普通用户来说，CD 可以作为运行可用的 Fedora 桌面系统的良好起点。

> 注意：此书中附带的 CD 和 DVD 适用于 32 位 PC 架构。它们无法在其他架构上运行。不过，你可以从 Fedora 下载页面（http://fedaproject.org/get-fedora.html）下载 适用于 X86 64 位 (x86_64)、PowerPC (ppc) 或 PowerPC 64 位 (ppc64) 架构的 Fedora 启动及安装 CD 和 DVD 镜像。

要从 DVD 或 CD 安装 Fedora 11，请遵循第 2 章以及 DVD 或 CD 上 README 的说明。

如果由于某种原因你手头没有 DVD，你可以在 Fedora 项目网站 http://fedaproject.org 找到有关如何下载启动和安装 CD 及 DVD 的信息。如果你在局域网的另一台电脑上有 DVD 驱动器，请参阅第 2 章关于设置 Fedora 安装服务器的信息，这样你就可以通过局域网在选定的机器上安装 Fedora。

如 http://rpmfusion.org/fedora 等仓库可以帮助你找到 Fedora（或任何其他 Red Hat 发行版）中没有的额外实用软件包。其中一些

## Fedora 源代码

站点作为 yum 或 apt 仓库，允许你下载一组依赖包（参见第 5 章中关于 yum 和有用仓库的描述）。

有时，你可能想要重新编译 Linux 内核或随 Fedora 提供的其他软件包。像二进制软件包一样，源代码包也可以从 Fedora 项目网站（http://fedoraproject.org/get-fedora.html）获取。要处理 Fedora 源包，你需要：

- `kernel-devel` —— `kernel-devel` 软件包带有 Fedora 二进制包。包名包含了它包含的内核版本。当前内核的源代码位于 `/usr/src/kernels` 目录，如果安装了 `kernel-devel` 软件包，就可以进行重新编译。
- SRP 目录 ——位于任何 Fedora 仓库的每个二进制包的源代码。安装你感兴趣的软件包（名称以 `.src` 结尾）以及你本地 `rpmbuild` 目录下的该软件副本。

要进行实际编译，你至少需要安装 `gcc` 软件包。对于安装 DVD，如果你想下载包含 Fedora 源代码的 DVD，可以从 Fedora 下载站点获取。适用于 Fedora 源代码的独立软件包位于相同的 Fedora 镜像站点中。

# 附录 B：运行网络服务入门

本附录的其余部分将概述与 Fedora 和 RHEL 自带的网络服务相关的守护进程、启动脚本、配置文件和软件包。

## 调试服务

几乎每个服务都提供了一个选项，允许可以在不同的调试级别下运行。通过开启调试功能，你可以看到从失败消息到该服务执行的任何操作的详细信息。通常，你可以在 init 脚本中添加调试选项（通常通过 `/etc/sysconfig/` 文件中设置的选项传递），或者在添加调试选项后手动运行守护进程。例如：

```
