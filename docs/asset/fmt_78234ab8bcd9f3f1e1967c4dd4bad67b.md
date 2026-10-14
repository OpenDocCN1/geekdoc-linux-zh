
本节说明了使用 KVM 模块和工具创建虚拟机的两种方法。我已经在具有双核 CPU 的笔记本系统上测试了这些方法。我为此使用了之前描述的 Ubuntu ISO 文件。JeOS 的优势之一是它所需的资源较少。我将通过使用 `virt-install` 命令以及 GUI 虚拟机管理器（Virtual Machine Manager）从命令行演示虚拟机的配置。其他可用工具还包括 `ubuntu-vm-builder`；但这里的重点是 `virt-install` 命令，因为它与 GUI 虚拟机管理器密切相关。

## 从命令行配置虚拟机

`virt-install` 是一个可以从命令行配置基于 KVM 虚拟机的命令脚本。你可以如相关页面所示指定所有功能，也可以让 `virt-install` 命令提示你输入所需信息。当我运行 `virt-install` 命令时，我如下所示输入了所需信息（以粗体显示）：

```
$ virt-install
```

你的虚拟机名称是什么？UbuntuJeOSHHM2

应该分配多少内存（兆字节）？256

你想要使用什么作为磁盘（文件路径）？`/home/michael/UJvm2.img`

你希望磁盘（`/home/michael/UJvm2.img`）有多大（千字节）？2

你是否要启用图形支持？（yes 或 no）yes

## 第 20 章：虚拟机与终端服务器

虚拟 CD 镜像、CD 设备或安装位置是什么？`/home/michael/jeos-8.04-jeos-i386.iso`

开始安装...

libvir: QEMU error :

libvir: QEMU error :

libvir: QEMU error :

正在创建存储文件... 100% |================================== 2.0 GB 00:00

正在创建域... 0 B 00:00

这些项目在我的主目录下配置了一个 2GB 的文件作为虚拟磁盘。图形支持 Ubuntu JeOS ISO 文件，该文件已下载到相同目录。图形支持允许在域创建后，在 20-9 中自动查看虚拟机控制台。

QEMU 查看器方便了在 Send 键下使用控制键。可用选项包括用于重启的 CTRL-ALT-DEL、用于退出 X 窗口的 CTRL-ALT-BACKSPACE、PRINTSCREEN 键以及 CTRL-ALT-FX（其中 x 的范围可以在 1 到 9 之间）。

![](img/28cf881509dedde88f9e34e8cefb7020_541_0.png)

图 20-9. KVM 虚拟机的 QEMU 查看器界面

## 虚拟机管理器

虚拟机管理器为 `virt-install` 命令提供了 GUI 前端。要启动它，在 GUI 中运行 `virt-manager`。如果你熟悉最新的 Red Hat 发行版，你可能认识这个工具，它最初由 Red Hat 开发。然而，在 Ubuntu 系统上，虚拟机管理器并非所有功能都已为 KVM 启用。

在本章中，我在笔记本电脑上完全虚拟化地安装了 Ubuntu JeOS 操作系统。你需要一个开启了虚拟化的 CPU（对于基于 Intel 的系统，还需要 BIOS）的系统。如果满足，你可以按照以下步骤创建 KVM 虚拟机：

1. 首先，打开虚拟机管理器。打开命令行界面并运行 `virt-manager` 命令。
2. 在虚拟机管理器中，高亮 localhost 连接，并选择文件 (File)|打开连接 (Open Connection)。在打开连接窗口中，检查选项。默认是 QEMU 虚拟机程序和本地连接（如果安装并运行了适当的内核，Xen 可能是一个选项）。也可以通过安全 Shell (SSH) 连接进行远程连接。为了本次练习，请接受默认值并点击连接。
3. 回到虚拟机管理器，高亮 localhost 连接并点击新建 (New)。你会看到“创建一个新虚拟机系统”（Create A New Virtual System）窗口，它指定了你在后续步骤中需要添加的信息。阅读描述并下一步 (Forward)。
4. 为基于 KVM 的机器指定一个名称。点击下一步。
5. 选择完全虚拟化（Fully Virtualized）、与本地硬件 CPU 兼容的虚拟 CPU，并保持启用内核/硬件加速（Enable Kernel / Hardware Acceleration）选项被选中。点击下一步。
6. 如果出现错误，当前用户账户可能未确认属于 kvm 组（如前所述）。在这种情况下，你必须重新登录 GUI 并重启过程。
7. 在定位媒体（Locating Media）屏幕上，你可以选择安装源——从本地文件、CD/DVD 或网络。操作系统类型（OS Type）选项包括 Linux、Microsoft 和其他。操作系统变体（OS Variant）选项包括 Windows、Ubuntu。点击下一步。
8. 在分配空间（Assigning Space）屏幕上，你可以选择分配整个磁盘。如果你选择此选项，将在你的主目录下创建一个文件。
9. 在分配内存和 CPU（Allocate Memory And CPU）屏幕上，你将指定分配给的内存和 CPU 数量。确保为主机保留足够的内存。如果 CPU 恰好是双核，KVM 将其识别为两个 CPU，你可以在此屏幕分配。点击下一步。
10. 最后，你将预览配置的虚拟机。点击完成 (Finish) 后，将为新配置的系统打开一个窗口。

![](img/28cf881509dedde88f9e34e8cefb7020_543_0.png)

图 20-10. 配置安装媒体

![](img/28cf881509dedde88f9e34e8cefb7020_542_0.png)

图 20-11. 配置磁盘（图像显示虚拟机创建向导的分配空间步骤）

### Ubuntu 服务器管理

![](img/28cf881509dedde88f9e34e8cefb7020_544_0.png)

如果你想通过虚拟机管理器返回这些已配置虚拟机之一，请重复步骤 1 和 2。已配置的虚拟机应出现在虚拟机管理器中。右键点击所需的虚拟机并选择打开 (Open)。将为所需的虚拟机打开一个窗口，并有一个可以启动虚拟系统的运行 (Run) 按钮。

## Linux 服务器项目 (LTSP)

Linux 是一个多用户、多任务系统。最新的 PC 和网络可以同时处理多个终端的计算需求。通过无盘客户端，你可以使用旧硬件配置终端。网络上的无盘客户端可以从同一个系统运行程序。无盘客户端对管理员来说是一种便利，对组织来说可以大幅节约成本。

如果你认真考虑终端服务器，请考虑 Ubuntu 的 Edubuntu 版本。它预配置了设置终端服务器所需的服务，并包含了一些管理终端服务器客户端的实用工具。本节仅提供了设置 LTSP 基础设施的最基本概述，对于大多数管理员来说是不够的。但它应该让你对在 Ubuntu 上创建终端服务器所需的工具有一个基本的了解。

### 安装 LTSP 包

> 提示：关于 Edubuntu 中 LTSP 实现的说明，请参见 https://wiki.edubuntu.org/ HardyClassroomServer。

无盘客户端并不是“哑终端”；它们需要一些基础设施支持。虽然显示图形用户界面（GUI）需要本地图形硬件（显卡、适当的显示器），但不需要本地硬盘。在网卡和 BIOS 均可配置 PXE 的系统上，可以配置无盘客户端。

无盘客户端的基础设施包含三个部分：首先，DHCP（动态主机配置协议）为每个客户端提供唯一的网络地址，这部分在第 14 章中已经介绍过。其次，TFTP（简易文件传输协议）服务器共享启动无盘客户端所需的文件，或者 TFTP 服务器的配置也比第 17 章中配置的 FTP 服务器更简单。第三，基础的精简目录树可以通过 NFS 服务器进行共享；有关 NFS 的更多信息，请参阅第 16 章。

无盘客户端的一种 Ubuntu 实现方案是基于 Linux 终端服务器项目（Linux Terminal Server Project）的工作。事实上，安装相应 LTSP 服务器的命令也会默认安装 `dhcp-server` 和 `TFTP-server` 包：

```
sudo apt-get install ltsp-server ltsp-server-standalone ltsp-client-core
```

### 动态主机配置协议 (DHCP) 服务

DHCP 服务器的基本配置在第 14 章中介绍过。本节涵盖了支持无盘客户端所需的特殊指令。将 PXE 客户端指向正确的文件取决于你本地网络是否已经存在一个现有的 DHCP 服务器。如果已经有了，你将需要在主 DHCP 服务器配置中添加以下内容。请将 `ipaddress` 替换为 LTSP DHCP 服务器的实际 IP 地址：

```
next-server ipaddress;
```

现在处理 LTSP 系统上的 DHCP 服务器，打开 DHCP 配置文件 `/etc/dhcp.conf`。正如同名指令建议所示，第一条指令表明此配置对于已配置的网络地址范围具有权威性：

```
authoritative;
```

以下指令与特定子网相关联；如果你想配置不同的子网，请进行相应的替换：
