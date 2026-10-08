
取自于。在以下示例中，使用 2.6.21 内核的模块在 /boot 目录下创建一个名为 **initrd-2.6.version.img** 的 RAM 磁盘镜像。您的系统中必须已安装 2.6.21 内核，并且其模块已创建。

```
# mkinitrd /boot/initrd-2.6.version.img 2.6.21-1.3116.fc7
```

您可以选择某些模块在任何 SCSI 模块之前或之后加载。**--preload** 选项会在 SCSI 模块之前加载，而 **--with** 则在之后加载。例如，要在 SCSI 模块之前加载 RAID5 支持，请使用 **--preload=raid5**：

```
mkinitrd --preload=raid5 raid-ramdisk 2.6.21-1.3116.fc7
```

在新内核的 **grub.conf** 部分中，放置一个指定新 RAM 磁盘的 **initrd** 条目：

```
initrd /boot/initrd-2.6.21-1.3116.fc7.img
```

## 虚拟化

目前，Fedora 上有多种可用的虚拟化方法。这些方法从 Xen 使用的半虚拟化实现，到 Intel 和具有硬件虚拟化支持的 AMD 处理器使用的内核级虚拟化机（KVM）硬件加速，种类繁多。您甚至可以使用软件模拟。所有这些都可以轻松安装和管理，使用虚拟机管理器，这是一个基于 GNOME 的工具，提供用于管理您的虚拟机和安装新虚拟机的简单 GUI 界面。Fedora 还提供 GNOME VM 小部件，gnome-applet-vm，一个可以监控您虚拟机的面板小部件。有关虚拟化资源列表，请参见表 33-2。所有虚拟化软件包均可从 Fedora 软件源获取。有关一般虚拟化链接和概述，请参见 **virt.kernelnewbies.org**。

| 资源 | 描述 |
|:---|:---|
| fedoraproject.org/wiki/Docs/Fedora7VirtQuickStart | Fedora 上的虚拟化，包括 KVM 和 Xen，以及虚拟机管理器的详细信息 |
| fedoraproject.org/wiki/Tools/Virtualization | Fedora 虚拟化资源 |
| virt-manager.et.redhat.com/ | 虚拟机管理器，virt-manager |
| fedoraproject.org/wiki/Tools/Xen | Fedora Xen 文档 |
| www.xensource.com | Xen 半虚拟化网站 |
| fabrice.bellard.free.fr/qemu/ | QEMU 软件虚拟化 |
| kvm.qumranet.com/kvmwiki | KVM 硬件虚拟化 |
| libvirt.org/ | 用于访问 Linux 虚拟化功能的 libvirt 工具包 |

**表 33-2 虚拟化资源**

所有虚拟化方法都可以使用虚拟机管理器进行安装和管理。虚拟机管理器极大地简化了安装和管理虚拟操作系统（客户机 OS）的过程。只需几个步骤，您就可以在 Fedora 系统上安装 Windows 或其他 Linux 发行版，并在需要时作为客户机操作系统运行。KVM 虚拟主机将直接从处理器运行，运行速度和稳定性几乎与单独安装并使用双启动配置一样快。

目前用于虚拟化的两种主要方法是完全虚拟化和半虚拟化。完全虚拟化（KVM 或 QEMU）独立运行客户机 OS，而半虚拟化（Xen）要求您首先引导 Xen Linux 内核，从中启动半虚拟化客户机 OS 系统。这意味着，完全虚拟化的 OS 可以从常规 Linux 内核使用虚拟机管理器启动，而半虚拟化的 OS 需要引导 Xen 内核。

## 虚拟机管理器：virt-manager

您可以轻松使用虚拟机管理器（virt-manager）管理和设置 KVM 或 Xen 虚拟机。请确保已安装 virt-manager。从应用程序 | 系统工具菜单中选择虚拟机管理器。这将显示一个列出您虚拟机的窗口（参见图 33-1）。将显示机器 ID、名称、统计信息、CPU 和内存使用情况等功能。您可以使用“查看”菜单确定要显示哪些功能。点击“帮助”菜单中的“帮助”条目以显示虚拟机管理器的详细手册。

有关主机机器的详细信息，请点击“编辑”菜单中的“主机详细信息”。“概览”面板将显示主机名、CPU 数量以及它可启动的 hypervisor 类型等信息。“虚拟网络”面板显示您的虚拟网络，列出 IPv4 连接信息、设备名称和网络名称（默认已设置）。选择客户机并点击“详细信息”按钮以获取客户机信息。

要创建虚拟机，请从“文件”菜单中选择“新建机器”。这将启动 virt-install 向导。系统将提示您输入名称、虚拟化类型、操作系统安装磁盘或文件的位置、用于客户机操作系统的存储以及要分配给客户机 OS 的系统内存量。

输入名称后，您需要选择虚拟化方法。如果您运行的是标准内核，您将只能选择使用完全虚拟化方法。

![](img/ab68ea377332b50bf70ef1316c8175b6_807_0.png)

在具有 Intel VT 和 AMD SVM 处理器的系统上，您还可以选择启用硬件加速。这意味着使用 KVM（内核级虚拟机）支持，提供处理器级别的硬件虚拟化。对于没有硬件虚拟化支持的处理器，则使用软件模拟。

相反，如果您从 Xen 内核（作为 Domain 0）运行虚拟机管理器，您可以使用半虚拟化。对于特别修改过以用于 Xen 的客户机 OS 版本，可以使用虚拟化按需运行该客户机 OS。此外，对于 Intel VT 和 AMD SVM，可以使用 Xen HVM 方法在需要虚拟化时采用硬件虚拟化。

> *提示* 对于具有大量内存和处理器支持的系統，您甚至可以使用虚拟机管理器通过 KVM 同时运行或安装客户机操作系统。

然后您选择 OS 安装介质的位置。对于完全虚拟化的 OS，这可以是磁盘镜像或 CD/DVD-ROM，如 Windows 类别磁盘。然后您选择正在安装的操作系统类型，首先选择像 Linux 或 Windows 这样的类别，然后选择特定的发行版或版本，如 CentOS Linux 或 Windows XP。对于半虚拟化的 OS（Xen），您选择安装介质的网络位置。

然后您选择存储模块。这可以是现有分区或文件。如果您选择文件，您可以设置固定大小（像固定分区一样），或者让文件根据需要扩展。如果文件位于有大量可用空间的分区上，这可能不会成为问题。

然后您选择虚拟网络或物理设备作为网络连接。然后选择分配给每个虚拟机的系统内存量，以及要使用的虚拟 CPU 数量。最后一个屏幕在开始安装之前显示新虚拟机的所有配置信息。此时您仍可以取消。开始安装时，将显示客户机 OS 的安装窗口，您照常安装。已安装的 OS 在虚拟机控制台窗口中运行。有按钮用于运行、暂停和关闭 OS。

> *提示* 您也可以使用 *virsh* 从命令行管理您的虚拟机。

## **内核级虚拟化机（KVM）：硬件虚拟化**

在内核版本 2.6.20 中，内核现在直接支持硬件虚拟化（之前的版本使用内核模块）。硬件虚拟化由 Intel 和 AMD 实现为硬件虚拟机抽象层。具有硬件虚拟化支持的 Intel 处理器标记为 VT（Virtualization Technology），AMD 处理器标记为 SVM（Secure Virtual Machine）。HVM 系统具有提供完全虚拟化的能力，不需要像 Xen 的半虚拟化方法那样使用特别修改的 OS 内核版本。您甚至可以使用 HVM 功能直接从 Linux 运行 Windows XP。KVM 是由 Qumranet 开发的开源项目，*kvm.qumranet.com/kvmwiki*。请确保查看 Fedora 项目虚拟化快速入门指南中的 KVM 条目，以了解有关如何实现 KVM 的详细信息，*fedoraproject.org/wiki/Docs/Fedora7/VirtQuickStart*。

