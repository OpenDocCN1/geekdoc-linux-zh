
```
http://download.fedora.redhat.com/pub/fedora/linux/releases/7/Fedora/i386
```

> **注意：** 这里是如何将 Fedora DVD 作为客户端存储库的方法。安装 `nfs-utils` 包。

插入 DVD。假设它挂载在 `/media/disk`，添加以下行：

```
/media/disk * (ro)
```
到 `/etc/exports` 文件中。启动 nfs (`/etc/init.d/nfs start`)。当提示输入软件存储库时，输入此地址 `nfs:localhost:/media/disk`。如果 `localhost` 不起作用，请使用你计算机的 IP 地址。

- 8. **存储位置** — 选择使用现有文件系统上的文件或磁盘分区设备名称来存储安装的系统。例如，你可以将磁盘命名为 `/home/chris/xenimageA` 作为要使用的文件。我在执行此操作时创建了一个新的磁盘分区。确保你使用的位置有足够的磁盘空间来容纳即将安装的操作系统。你还需要分配内存。

- 9. **主机网络** — 选择你的新虚拟系统如何连接到主机网络。大多数情况下，选择虚拟网络。然而，你也可以选择共享物理设备（如以太网桥接或 MAC 地址）。

- 10. **分配内存** — 输入一个数字代表你想分配此虚拟机的最大兆字节内存内存以及你想启动时的数量，并点击下一步。建议至少 256 兆字节内存。如果你有更多可用内存，应该使用更多，因为它将提高性能。你还可以选择使用多个 CPU（1 是默认值）。

- 11. **完成** — 当输入所有信息后，将出现如图 5-6 所示的信息摘要。点击“完成”。新的虚拟机应该出现在虚拟机管理器中。选择它并点击“打开”。

- 12. **开始安装** — 应该出现一个虚拟控制台，准备好安装你的 Fedora 7 虚拟机。

- 13. **安装客户** — 因为你正在 Fedora 9 系统上安装 Fedora 7，你基本上可以按照本书第 2 章中的安装说明进行。对于磁盘分区，你可以指示安装程序使用整个分区，或者你可以创建多个分区。

在 Fedora 安装作为客户后，你可以根据需要从虚拟机管理器窗口打开虚拟机。如果你选择了以太网桥接，并且你的网络上有一个 DHCP 服务器，你的虚拟机就可以被分配它自己的 IP 地址。这样你就可以使用 Fedora 中的工具访问互联网并更新和获取所需的新软件了。

从命令行管理你的虚拟机，可以使用 `xm` 命令。要查看当前可用的虚拟机，输入以下命令：

```
# xm list
Name ID Mem VCPUs State Time
Domain-0 0 453 1 r----- 1675.5
Fedora 264 1 243.9
```

如果你想保存虚拟机的快照，请使用 `xm` 命令将其保存到文件。例如，要将名为 Fedora 的虚拟机保存到 `/tmp/virt-save`，你可以输入：

```
# xm save Fedora /tmp/virt-save
```

稍后，要恢复虚拟机，你可以输入：

```
# xm restore /tmp/virt-save
```

有关在 Fedora 中使用 Xen 虚拟机的详细信息，请参考 Fedora Xen 快速入门 (`http://fedoraproject.org/wiki/Docs/Fedora7VirtQuickStart`)。

图 5-6：虚拟机管理器 (`virt-manager`) 让你安装和运行客户操作系统。

## 使用 KVM 和 QEMU 虚拟运行应用程序

与 Xen 一样，内核虚拟机 (`KVM`) 化需要具有 Intel VT 或 AMD-V 处理器的计算机。然而，KVM 使用加载内核模块 (`kvm.ko`) 实现，它与标准内核配合，而不是使用特殊的 Xen 内核。QEMU (`www.qemu.org`) 用于最终运行客户操作系统。

在 KVM 下运行的每个虚拟机内部都是私有的虚拟化硬件，为你提供访问硬盘、网卡和其他硬件资源的权限。开始 KVM 虚拟化的某些要求与 Xen 相同：

- 每个客户机至少需要 256MB 内存。

- 对于磁盘空间，每个客户系统可能至少需要 2GB 和 3GB（根据平均大小的 Fedora 桌面安装判断）。

- 你需要安装 GRUB 引导程序。

- 你需要 Intel VT 或 AMD-V 处理器（参见“安装 Xen 之前”部分有关如何检查 `pae` 支持的信息）。

接下来，你想安装许多你为 Xen 安装的相同包。从“添加/安装软件”窗口中，你可以只需搜索并安装适当的 xen 包。特别是，将 `kvm` 和 `qemu` 包添加到 Xen 所需的包（如 `virt-manager`）中。

此时，你像通常为所选的操作系统那样运行安装过程。安装完成后，你可以从虚拟机管理器启动和关闭新的虚拟环境。

95/98/2000/NT/XP/Vista 以及 Macintosh 操作系统。从长期来看，如 Xen 和 KVM 等虚拟化软件将允许多个操作系统作为客机运行在 Fedora 上。这反过来又为在 Fedora 中的这些系统中运行各种应用程序提供了手段。

# 第 6 章

# 在 Fedora 和 RHEL 上发布

## 本章介绍

- 使用 OpenOffice.org

- 使用商业文字处理器

- 使用 Groff 和 LaTeX 创建文档

- 创建 DocBook 文档

- 使用 Linux 打印文档

- 使用 Ghostscript 和 Acrobat 显示文档

- 图形处理

- 使用由 SANE 驱动的扫描仪

一个操作系统若要在桌面系统中生存下去，它必须能够执行至少一项任务：生成文档。在 Windows 之后，Microsoft Word（包含在 Microsoft Office 中）成为微软在桌面端取得成功的基石，这并非偶然。Fedora 和 RHEL 包含了生成文档、处理图像、扫描和打印的工具。几乎你预期一个发布系统能做的一切工作，你都可以在 Fedora 和 RHEL 上完成。

OpenOffice 是一个强大的开源办公套件，作为 Fedora 和 RHEL 发行版的一部分提供。OpenOffice 基于 Sun Microsystems 的 StarOffice 生产力套件，包含了文字处理器、电子表格、演示文稿管理器和其他个人生产力工具。在许多情况下，OpenOffice.org 可以作为 Microsoft Office 的无缝替代，无论是在功能还是对 Excel、PowerPoint 等其他微软格式的支持上都是如此。

Linux 最初的文档和图形工具大多建立在旧的文本工具之上的。最近，增加了许多更复杂的用于写作、页面格式化和图形成的工具。尽管年代久远，但许多旧的发布工具（如 Groff 和 LaTeX）仍被技术社区的人使用。

在本章中，我描述了适用于 Fedora 和 RHEL 的基于文本和基于 GUI 的文档准备软件。我还描述了用于打印和显示文档的工具，以及处理图像的软件。

## 使用 OpenOffice。

有些人称 OpenOffice 是对 Microsoft Word 统治桌面市场地位的重大威胁。如果处理 Microsoft Word 格式文档的需求阻碍了你使用 Linux 作为桌面电脑，那么 OpenOffice.org 是消除这一障碍的一大步。

> 注意：如果你愿意支付几美元，来自 Codewavers.com 的 CrossOver 允许你在 Linux 桌面上安装和运行不同版本的 Microsoft Office（97, 2000, XP 和 2003）。更多信息请参见第 5 章或访问 `www.codewavers.com/products/cxoffice`。

Fedora 和 RHEL 包含了整个 OpenOffice.org 桌面应用程序套件。最新的 OpenOffice.org 版本（2.4）包含在此版本的 Fedora 中。基于 StarOffice 源码，OpenOffice.org 包含以下办公生产力应用：

- OpenOffice.org Writer — 一个文字处理程序，可以处理 Microsoft Word、StarOffice 以及其他多种格式的文档。Writer 还拥有一套完整的功能，用于使用模板、处理字体、导航文档（包括图像和效果）以及生成目录。

- OpenOffice.org Calc — 一个电子表格应用程序，允许你整合来自 Microsoft Excel、StarOffice、Dbase 和其他电子表格格式的数据。Calc 中的某些功能允许你创建图表、更新数据库范围（轻松地对电子表格区域中的数据进行排序）并使用数据透视从不同角度安排数据。

- OpenOffice.org Draw — 一个绘图程序，允许你创建、编辑和对齐对象；合并纹理；包含纹理和颜色；与对象层协作。它允许你将图像、矢量图形、AutoCAD 以及各种其他格式整合到你的图中。然后，你可以将图保存为 OpenOffice.org Drawing 或 StarOffice Draw 格式。

- OpenOffice.org Math — 一个计算程序，允许你创建数学公式。
