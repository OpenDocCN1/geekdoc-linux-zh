
本节描述了如何从基于 Intel 的 Apple Mac 电脑（我以 Mac Mini 为例）开始，并将其配置为与 Mac OS X 双启动或单独运行 Fedora。

> **警告：** 在基于 Intel 的硬件上安装 Fedora 在 Fedora 社区中仍然是一项实验性技术。某些硬件组件仍需要额外调整或根本无法工作。如果您无法承担磁盘可能损坏并需要从 scratch 重新安装的可能性，我不建议您执行此操作。

## 在 Mac 上安装 Fedora 之前

让我们提醒一下，此操作仅适用于基于 Intel 架构的 Apple Mac 电脑。我在新的 Mac Mini 1.1（Intel Core Duo CPU，512MB RAM）上执行了此操作。然而，相同的操作应适用于基于 Intel 的 iMac、MacBook、MacBook Pro 或 Mac Pro 计算机。

此操作不适用于采用 PowerPC 架构的 Mac。Fedora 确实支持该配置，但您需要从 Fedora 下载 ppc 安装介质，而不是使用随本书附带的光盘。（从 `http://fedoraproject.org/wiki/distribution/Download` 获取用于在 PowerPC 上安装的介质。）

购买 Mac 时，整个硬盘都用于 Mac OS X。为了在计算机上保留 Mac OS X 安装（以便您可以启动 Mac OS X 或 Fedora），您需要减少分配给 Mac OS X 的空间。然后，您需要使用这些空间创建一个或多个用于安装 Fedora 的分区。

虽然调整磁盘大小和重新分区的操作相对安全，但存在一些风险，可能会损坏您的 Mac OS X 分区或使计算机（暂时）无法启动。因此，在开始以下操作之前，请 ...

... 备份所有重要数据！

## 安装 Fedora

Mac OS X Leopard 及更高版本提供称为 Boot Camp 的软件，可用于调整 Mac 硬盘的大小（使用默认的 HFS+ 文件系统类型）。以下操作描述了如何更新固件、调整磁盘大小并安装 Fedora。

1. **检查固件更新** — 将您的 Mac OS X 系统更新到最新的固件。参阅 Mac OS X 固件更新页面了解如何操作（`http://support.apple.com/kb/HT1237`）。然后前往 Apple 下载中心（`http://www.apple.com/support/downloads/`）获取固件更新（如果需要）。

2. **运行 Boot Camp** — 启动 Boot Camp 助理（位于实用工具文件夹中）。由于您对 Boot Camp 的兴趣在于调整 Mac 磁盘分区，请跳过制作 Mac CD 的请求。然后移动分隔线以选择分配给 Mac OS X 和 Windows 的磁盘空间量（您将使用 Windows 区域用于 Linux 而不是 Windows）。当每个操作系统都拥有您想要的磁盘空间时，选择“分区”按钮。（我选择创建一个 10GB 的 Windows 分区。）

> **注意：** 由于 Mac OS X Leopard 之前的版本不再提供 Boot Camp，因此没有官方方法来调整磁盘大小以允许 Mac 上存在多个启动分区。然而，从理论上讲，您应该可以使用支持 HFS+ 调整大小的分区工具来准备磁盘，以便与 Mac OS X 一起安装 Fedora。参阅第 2 章了解如何使用 GParted 或 QTParted 调整分区大小（如 HFS+ 分区）。如果您决定尝试，结果概不负责。（换句话说，您得自己负责。）

3. **插入 Fedora DVD** — 分区完成后，不要插入 Windows 安装 CD，而是插入 Fedora 安装 CD 或 DVD，并单击“重新启动 Mac OS X”或“安装 Windows”以重新启动计算机。计算机重新启动后，您应该看到 Fedora 安装程序的启动屏幕。

4. **安装 Fedora** — 开始正常的 Fedora 安装（如本章前所述），只需注意以下几点：

    - **分区** — Fedora 安装程序的默认分区应该正常工作（保留您的 Mac HFS+ 分区不变，并使用剩余空间创建 Fedora `/boot` 和 LVM 分区）。

    - **引导加载程序** — 再次，安装程序应该做正确的事情，配置引导加载程序安装到 Fedora 分区上，而不是主引导记录（MBR）上，因为通常情况下

通常是这样。（引导加载程序不应安装在整个磁盘的主引导记录中，否则磁盘将无法引导。）

5. **重启并按住 Alt 键** — 当 Fedora 安装完成后，按照指示重启。在机器重启时按住 Alt 键。当您看到 Boot Camp 菜单时，选择 Windows，计算机将会引导到 Fedora。只需使用 Fedora 的默认引导项，因为尝试更改 GRUB 引导标签可能会导致计算机死机。（顺便说一句，如果您的 DVD 卡在光驱中，请在重启时按住鼠标按钮，DVD 将会弹出。）

请记住，在基于 Intel 的 Mac 上安装 Fedora 仍然被视为实验性功能。你越少偏离默认设置（分区、引导加载程序等），在 Mac 上运行可用的 Fedora 系统的机会就越大。

如果您遇到问题，建议您参考 Fedora 项目的 [Fedora On MacIntel](http://fedoraproject.org/wiki/FedoraOnMacIntel) 页面。还有其他 Linux 项目的资源可供参考，以实现在 Intel Mac 架构上引导 Linux。

### 使用 GRUB 引导加载程序

引导加载程序允许您选择何时以及如何启动安装在计算机硬盘上的可启动操作系统。GRUB 是 Fedora 安装过程中唯一供您配置引导加载程序。 (早期版本的 Fedora 中附带的 LILO 引导加载程序自 Fedora Core 5 起不再包含在内。) 以下章节描述了 GRUB 引导加载程序。

当安装了多个操作系统并设置了多个分区时，计算机如何知道该启动哪个操作系统？为了选择和管理哪个分区被引导以及如何引导，您需要一个引导加载程序。 Fedora 默认安装的引导加载程序称为 GRAnd Unified Boot loader (`GRUB`)。

`GRUB` 是一个 GNU 软件包 (`http://www.gnu.org/software/grub`)，它取代了 LILO 成为 Fedora 中唯一的引导加载程序。`GRUB` 提供了以下功能：

- 支持多种可执行文件格式。

- 支持多引导操作系统（如 Fedora、FreeBSD、NetBSD、OpenBSD 以及其他 Linux 系统）。

- 通过链式加载功能支持非多引导操作系统（如 Windows 95、Windows 98、Windows NT、Windows XP、Windows Vista 和 OS/2）。链式加载是指从 `GRUB` 加载另一个引导加载程序（通常是专有的操作系统特定的引导加载程序）以启动所选操作系统的行为。

- 支持多种文件系统类型。

- 支持自动解压引导映像。

- 支持从网络下载引导映像。

有关 `GRUB` 工作原理的更多信息，请键入 `man grub` 或 `info grub`。`info` 命令包含有关 `GRUB` 的更多详细信息。或者，请查看 `GRUB` Wiki：`http://grub.enbug.org`。

当您安装 Fedora 时，引导计算机（带有一个或多个操作系统）所需的信息会自动设置并准备就绪。只需重新启动您的计算机。当您看到引导消息时，按 `Enter` 键（在超时前快速操作），将出现 `GRUB` 引导屏幕（顶部显示 `GRUB`，下方列出可引导分区）。然后您可以执行以下任一操作：

- **默认** — 如果您什么都不做，默认操作系统将在几秒钟后自动引导。

- **选择操作系统** — 使用上下箭头键选择屏幕上显示的任一操作系统。然后按 `Enter` 引导该操作系统。

- **编辑引导过程** — 如果您想更改引导过程中使用的任何选项，请使用箭头键选择您想要的操作系统并键入 `e` 进行选择。按照接下来的步骤临时更改您的引导选项。

如果您想更改引导选项以便每次引导计算机时都生效，请参阅关于永久更改引导选项的章节。更改这些选项涉及编辑 `/boot/grub/grub.conf` 文件。

#### 临时更改引导选项

从 `GRUB` 引导屏幕，您可以选择更改或添加当前引导会话的引导选项。首先，在 `GRUB` 超时并引导默认系统之前，快速按任意键。

从出现的 `GRUB` 选择屏幕中，选择您想要的操作系统（使用箭头键）并键入 `e`（如前所述）。您将看到一个图形屏幕，其中包含文本信息，包括 `GRUB` 的根目录（`/boot` 分区）、内核以及初始 RAM 磁盘（initrd），后者包含引导过程中所需的最小文件和目录。

如果您要更改与引导过程相关的任何行，您可能只会更改第二行以添加或删除引导选项。以下是操作方法：

1. 将光标置于 `kernel` 行上并键入 `e`。

2. 在引导映像名称之后添加或删除选项。您可以使用最少的 bash shell 命令行编辑功能来编辑该行。甚至可以使用命令补全（输入文件名的一部分并按 Tab 键以完成输入）。以下是您可能想要添加或删除的几个选项：
