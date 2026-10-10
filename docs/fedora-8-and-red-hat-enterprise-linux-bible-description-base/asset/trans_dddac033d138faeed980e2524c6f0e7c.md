

如果您的计算机没有 DVD 光驱，您可以使用随书 DVD 中提供的 `boot.iso` CD 镜像（见下文）来启动网络安装（HTTP、FTP 或 NFS）。只需在启动提示符处键入 `linux askmethod`，即可开始安装过程。

如果您没有可启动的 DVD 或 CD 光驱，还有其他方法可以启动 Fedora 安装。与某些早期版本的 Fedora 和 Red Hat Linux 不同，Fedora 不支持软盘启动镜像（Linux 2.6 内核太大，无法存储在软盘上）。因此，如果您没有可启动的 DVD 或 CD 光驱，您需要通过其他介质（如 USB 设备、PXE 服务器或硬盘，本章后续内容将对此进行说明）来启动安装过程。

以下专业安装类型也可能适合您：

- **启动 CD** — 您可以从随本书提供的 Fedora 安装 DVD 中包含的启动镜像创建一张启动 CD。将 DVD 上 `images` 目录中的文件 `boot.iso` 复制并刻录到 CD 上。如果您有一个不可启动的 DVD 光驱，或者您拥有通过 `linux askmethod` 章节中描述的任一种介质可用的 Fedora 8 软件，您可以使用从该镜像创建的 CD 来开始安装过程。
- **USB 或其他可启动介质** — 如果您的计算机可以配置为从替代的可启动介质（如大于软盘的 USB 闪存盘）启动，您可以将 `diskboot.img` 文件复制到该介质上并从中安装。该镜像包含在 DVD 的 `images` 目录中。
- **Kickstart 安装** — 允许您创建一组针对 Fedora 安装过程中提出的问题的答案。如果您需要在许多具有相似配置的计算机上安装 Fedora，这可能是一种节省时间的方法。

Fedora 项目现在提供了一份《Fedora 安装指南》，如果您发现需要更多信息，可以参考该指南。不过，它可能不是最新的。您可以在此处访问该指南：`http://docs.fedoraproject.org/install`

## 选择计算机硬件

这可能并不是一个真正的选择。您可能只是手头有一台旧 PC，想要尝试在上面安装 Fedora。或者您可能有一台配置强劲的工作站，有一些额外的磁盘空间，并希望在单独的分区或整块硬盘上尝试安装 Fedora。为了成功安装 32 位 PC 版本的 Fedora（即随附 DVD 中的版本），计算机必须具备以下条件：

- **x86 处理器** — 您的计算机需要一颗 Intel 兼容的 CPU。对于最新版本，Fedora 建议至少拥有一颗奔腾级处理器来运行 Fedora。对于仅文本安装，最低要求为 200 MHz 的奔腾处理器，而对于图形用户界面（GUI）安装，最低要求为 400 MHz 的奔腾 II 处理器。
- **DVD 或 CD-ROM 光驱** — 您需要能够从 DVD、CD-ROM 或其他可启动驱动器启动安装过程。（其他驱动器包括可以使用 DVD 中包含的 `diskboot.img` 镜像的 USB 闪存驱动器。）一旦从上述介质之一启动，您可以使用互联网或局域网（LAN）连接从网络上的服务器安装 Fedora 软件包，或者想办法将 DVD 的内容复制到本地硬盘以从中进行安装。
- **硬盘** — 所需的最小空间取决于您选择的安装类型和软件包。如果您是一位缺乏经验的用户，至少需要 2.3GB 的空间以获取带有办公和生产力工具的 GUI，或者 3GB 的空间用于软件开发安装（如果您打算进行软件开发）。虽然 Fedora 不再支持不同的安装类型，但以下条目大致说明了安装不同类型的桌面或服务器系统所需的磁盘空间：
    - **办公和生产力** — 需要 2.3GB 的磁盘空间。
    - **软件开发** — 需要 3.0GB 的磁盘空间。
    - **Web 服务器** — 需要 1.1GB 的磁盘空间。
    - **最小化** — 至少需要 620MB 的磁盘空间。
- **内存（RAM）** — 安装 Fedora（仅限文本模式）至少需要 64MB 的 RAM。如果您以图形模式运行，至少需要 192MB。对于 GUI 模式，建议的最小 RAM（以获得良好的性能）至少为 256MB。

> **注意：** 随着 Openoffice.org 办公套件等要求较高的应用以及自动监控桌面的功能被添加，Fedora 需要比过去更多的 RAM 才能有效使用。Red Hat 的一位开发人员建议至少拥有 512MB 的 RAM 才能在 Fedora 中获得良好的性能。

- **键盘和显示器** — 虽然这看起来很明显，但事实是您在安装期间只需要键盘和显示器。您可以通过 LAN 使用网络登录的 shell 接口或 X 终端来很好地操作 Fedora。

> 本书未包含的 Fedora 版本可用于 AMD64 架构和 PowerPC。支持的最小的 PowerPC 硬件是 PowerPC G3/POWER4。支持的 PowerPC 产品包括 Apple Power Macintosh（1999 年或之后）、IBM 32-Bit RS/6000、Genesi Pegasos II，以及 IBM eServer pSeries 计算机中的 64 位 G5 和 POWER 处理器。请查看 Fedora 项目下载网站以获取有关 Fedora PPC 版本的信息。

对于其他硬件，如 Intel Itanium 和 IBM 大型机，有 Red Hat Enterprise Linux 的版本可用（您必须从 Red Hat, Inc. 购买）。然而，随本书提供的 DVD 和此处展示的安装步骤特定于 32 位 PC。本书中描述的大部分软件在任何这些硬件环境中都会以相同的方式工作。（请访问 http://fedoraproject.org/get-Fedora 查找提供适用于不同计算机硬件架构的 Fedora 的网站。）

> **注意**：Red Hat Enterprise Linux 支持的硬件列表可在互联网上的 `http://bugzilla.redhat.com/hwcert` 上找到。

## 在笔记本电脑上安装 Fedora

由于笔记本电脑可能包含非标准设备，在开始在笔记本电脑上安装之前，您应该了解其他人将在您的机型上安装 Linux 的经验。访问 Linux on Laptops 网站（`www.linux-on-laptops.com`）可以做到这一点。

大多数现代笔记本电脑都包含可启动的 CD-ROM 光驱。如果您的没有，您可能需要从连接到笔记本电脑 USB 或 PCMCIA 插槽的设备进行安装。PCMCIA 插槽允许您使用信用卡大小的卡片（有时称为 PC 卡）将各种设备连接到笔记本电脑。Linux 支持数百种 PCMCIA 设备。您可以使用笔记本电脑的 PCMCIA 插槽从几种不同类型的 PCMCIA 设备中安装 Fedora，包括：

- DVD 光驱
- CD-ROM 光驱
- 局域网（LAN）适配器

有关在笔记本电脑上使用 Linux 的更多信息，请参见第 10 章。

## 使用 Live CD 准备安装

在开始安装 Fedora 8 之前，有一些方法可以检查您的计算机硬件并为安装 Linux 做准备。通过启动 Live CD，您可以确保：

- Linux 内核（操作系统的心脏）可以启动。
- 您的计算机硬件拥有可用的设备驱动程序。
- 您的硬盘有足够的可用空间来安装 Fedora 或 RHEL（如果空间不足，您可以使用 Live CD 上的工具调整硬盘分区大小以腾出空间）。

您可以使用随本书提供的 Fedora 8 桌面 Live CD 来试用 Fedora，而不会对现有的设置做任何更改。您可以识别您的硬件驱动程序和磁盘分区。然后，如果需要，您可以更改硬盘以准备安装 Fedora（主要是在您需要保留现有操作系统，如 Windows，以便与 Linux 双启动的情况下）。

要使用 Fedora Live，插入随本书提供的 Fedora 8 Live CD，然后重新启动您的计算机。然后，在启动屏幕上，选择“Run from image”（从镜像运行）。

在花费几秒钟检测您的硬件并启动服务后，Fedora Live 应该会向您展示一个图形（GNOME）桌面。当 Live CD 在 PC 上运行时

