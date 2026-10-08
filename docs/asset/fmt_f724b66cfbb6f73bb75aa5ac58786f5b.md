
> **提示**：`redhat-config-packages` 工具不支持内核包安装。您必须在终端窗口中使用 `rpm` 命令手动安装内核包。

如果您正在自定义内核，安装内核的源码和头文件也是至关重要的。您需要源码来生成模块并根据您自己的需求定制内核。例如，您可以使用源码来生成包含您可能已安装的任何不常见设备驱动程序的模块，如下所示：

```
# rpm -Uvh kernel-source-2.4.22-1.2115.npt.i386.rpm
```

在大多数发行版中，内核安装在 `/boot` 目录中。对该目录执行 `-l` 操作会列出所有当前安装的内核。您有一个旧内核文件和一个新内核文件，还有一个名为 `vmlinuz` 的文件，它链接到新内核文件。如果您遵循了上一节的说明，您可能已经重命名了旧内核。如果您正在使用如 GRUB 等启动加载程序，无需更改其配置文件 (`grub.conf`)，因为调用内核的条目仍然引用 `/boot/vmlinuz` 链接，该链接指向新内核。内核通过 `/boot/vmlinuz` 链接到内核文件启动。在您的 `grub.conf` 中，内核文件的内核行引用了此链接。您还需要包含一行用于 RAM 磁盘的 `initrd`。

```
kernel /boot/vmlinuz-2.4.22-1.2115.npt root=/
initrd /boot/initrd-2.4.22-1.2115
```

> **提示**：`redhat-config-packages` 工具不支持内核包安装。你必须在终端窗口中使用 `rpm` 命令手动安装内核包。

## 修改内核的预防措施

如果您正在创建相同内核的修改版本，内核文件（此处称为 `vmlinux-2.4.22-1`）将被新内核覆盖，以及 `System.map` 和 `module-info` 文件。为了保留您工作的内核，必须对这些文件进行备份。您将拷贝 `/boot/vmlinux-2.4.22-1`，给它另一个名称，如下所示：

```bash
cp /boot/vmlinux-2.4.22-1 /boot/vmlinux-2.4.22-1.old
```

## 启动加载程序

如果您使用启动加载程序，您应该在启动加载程序配置文件中为旧内核创建一个新条目。然后您可以为新内核创建一个条目。保留旧内核条目是明智的。

出现问题通常是使用未注册版本的 CHM2PDF Pilot 创建的。通过它，你可以恢复并选择旧内核。例如，在 `grub conf` 中，在旧内核项旁边添加一个新项，并在 `kernel` 语句中引用新内核。grub 条目将如下代码所示。你可以在 GRUB 菜单中选择“Old Linux (2.4.22-1old)”项来启动旧内核。

```
title old Linux (2.4.22-1old)
root (hd0,2)
kernel /boot/vmlinuz-2.4.22-1old root=/dev/hda3
initrd /boot/initrd-2.4.22-1old.img
```

如果你为启动分区使用了标签（label），那么内核语句中的 `root` 选项对于标签为 / 的启动分区看起来如下：

`kernel /boot/vmlinuz-2.4.22-1old root=LABEL=/`

## 启动盘

你还应该准备一个启动盘，以防安装过程中出现问题（通常是在安装过程中创建的）。有了启动盘，你可以在不使用引导程序的情况下启动系统。你可以使用 `mkbootdisk` 实用创建启动盘。要创建启动盘，你需要知道内核的完整版本号。事实上，你可以安装多个内核，并为每个内核创建启动盘（你的 `grub conf` 文件会对应到你的内核版本号）。如果内核版本是 `2.4.22-1`，请使用它作为 `mkbootdisk` 命令的参数为你的系统创建启动盘：

```
mkbootdisk 2.4.22-1
```

如果你想制作启动 CD-ROM，可以使用 `--iso` 选项配合 `--device` 选项来指定 CD 镜像文件。你可以将镜像文件刻录到 CD-ROM 磁盘。在本示例中，用户创建了一个名为 `myimage.iso` 的 CD-ROM 镜像文件，用于 `2.4.22-1` 内核的启动 CD-ROM：

```
mkbootdisk --iso --device myimage.iso 2.4.22-1
```

## 从源码编译内核

与其安装已经编译好的内核二进制版本，不如在你的系统中安装内核源码，并自己创建内核二进制文件。内核源码文件使用 `gcc` 编译器进行编译，就像其他任何源码文件一样。编译内核的一个优势是你可以增强它的配置，添加对某些类型设备（如蓝牙设备）的支持。这里描述的是 2.4 内核。

### 安装内核源码：内核存档和补丁

你可以从你的发行版中获取最新版本的内核源码。它的名称为 `kernel-source`。新版本可以通过你的发行版更新代理下载，也可以通过直接访问发行版的 FTP 站点下载。如果你只是安装了它，那么使用任何 RPM 包即可。

```
rpm -ivh kernel-source-2.42-2.1115.npt1.i386.rpm
```

源文件被放置在 `/usr/src` 目录下，位于具有 `linux` 前缀并以内核作为后缀的子目录中。当你下载并安装新内核时，对于内核 2.4、版本 20、补丁 8，即 `linux-2.42-2.422-1`，完整的目录将是 `/usr/src/linux-2.42-2.422-1`。系统会为其创建一个独立的子目录。例如，2.42-1 内核被放置在 `/usr/src/linux-2.422-1`。系统会创建一个链接 `/usr/src/linux-2.4` 指你安装的最新的内核源码。你可以使用此链接来访问你最新的内核源码。最初，它将指向 `/usr/src/linux-2.4.222-1`。如果你之后安装了 2.5.67 内核，它将指向 `/usr/src/linux-2.5.67`。

你也可以从 `www.kernel.org` 获取最新版本的源码。这些版本通常比发行版站点提供的版本新得多。

```
cd /usr/src
tar -xzpf linux-2.4.22-1.tar.gz
```

务必在 `/usr/src` 目录下解压存档。存档会提取出一个名为 `linux` 的目录，其中包含源码文件。这样，文件就位于 `/usr/src/linux` 目录。你应该重命名这个目录并加上内核版本，就像 Red Hat 做的那样，改为 `/usr/src/linux-2.4.22-1`。

> 提示

> 如果你在使用原始内核源码，还应该检查是否有任何补丁。

### 配置内核

一旦安装了源码，你就必须配置内核。配置包括确定你希望为内核提供内核级支持的功能。这些包括用于不同设备的驱动程序，例如声卡和 SCSI 设备。你可以根据需要配置功能直接包含在内核中，或作为模块包含。你可以特意排除某些功能。直接包含在内核中的功能会使内核程序变大。设置为独立模块的功能也可以容易地更新。许多提供音频、视频或网络支持的设备文档可以在 `/usr/kernel/doc` 中找到。

### 内核工具

你可以使用多个工具之一来配置内核：`config`、`menuconfig` 和 `xconfig`。

`xconfig` 会打开一个列出 2.4 内核不同类别的窗口。`xconfig` 工具显示类别并允许你选择直接包含在内核中的功能。直接包含在内核中的功能会使内核程序变大。设置为独立模块的功能也可以容易地更新。许多提供音频、视频或网络支持的设备文档可以在 `/usr/kernel/doc` 中找到。

`menuconfig` 会打开一个列出 2.6 内核不同类别的窗口。`menuconfig` 工具提供了一个更具交互性的界面来配置内核。

`config` 会打开一个列出 2.6 内核不同功能的窗口。`config` 工具是一个用于配置内核的文本界面。

## 重要的内核配置功能

`xconfig`、`menuconfig` 和 `geconfig` 工具为每个条目提供了极佳的上下文帮助。每个条目的右侧都有一个帮助（Help）按钮。点击它可以查看详细说明该功能的作用，以及你应该将其直接包含、作为模块包含，还是排除它。当你对某个功能产生疑问时，请务必使用“帮助”来了解它的确切功能以及你想要使用它的原因。这里描述了许多关键功能。2.6 内核的对应条目列在括号中。

- **可加载模块支持 (Loadable Module Support)**：在大多数情况下，你应该确保你的内核可以加载模块。点击“Loadable Module Support”按钮显示多个模块管理选项列表。确保“Loadable Module Support”标记为 Yes。此功能允许你的内核根据需要加载模块。内核加载器（Kernel Module Loader）也应该设置为 Yes，因为这允许你的守护进程（例如你的 Web 服务器）加载它们可能需要的任何模块。

- **处理器类型和特性 (Processor Type And Features)**：“Processor Type And Features”允许你为你的系统设置支持。在这里，选择你拥有的处理器类型（486, 586, 686, Pentium III, Pentium IV 等），以及你的系统支持的最大内存量（2.4 内核最高支持 64GB）。

- **通用设置 (General Setup)**：“General Setup”窗口允许你选择通用功能，如网络、PCI BIOS 支持和电源管理，以及对 ELF 和二进制文件的支持。还支持通过 `sysctl` 动态更改在 `/proc` 文件中指定的内核参数。你可以使用 `redhat-config-proc`（系统工具菜单中的内核调整）来对内核进行这些更改。在额外的设备驱动程序支持中，你可以启用特殊功能，如加密 IP 封装 (CIPE) 和加速 SSL。

- **块设备（设备驱动程序）(Block Devices (Device Drivers))**：“Block Devices”窗口列出了支持你的 IDE、软磁盘驱动器并行设备的条目。那里还有特殊功能，例如 RAM disk 支持和用于挂载 CD-ROM 镜像文件的循环设备（loopback device）。

- **多设备支持（RAID 和 LVM）（设备驱动程序）(Multi-Device Support (RAID and LVM) (Device Drivers))**：“Multi-Device Support”窗口列出了启用使用 RAID 设备的条目。你可以选择你需要的 RAID 支持级别。在这里，你还可以启用逻辑卷管理（LVM）支持，它允许你将分区组合成可以进行动态管理的逻辑卷。

- **网络选项（文件系统和设备驱动程序）(Networking Options (Filesystems and Device Drivers))**：“Networking Options”窗口列出了一系列广泛的网络能力。“TCP/IP Networking”条目必须设置为启用以支持任何类型的互联网网络。在这里，你可以指定允许你的系统作为网关、防火墙或路由器运行的功能。网络别名（Network Aliasing）允许对 IP 别名的支持。其他类型的网络也存在别名，包括 AppleTalk 和 IPX。如果你想使用 NetTalk 连接网络上的 Macintosh 系统（文件系统），则必须启用 AppleTalk。

### ATA/IDE/MFM/RLL 支持（设备驱动程序）[ATA/IDE/MFM/RLL Support]

在 ATA/IDE/MFM/RLL Support窗口中，你可以点击“IDE, ATA, and ATAPI Block Device”打开一个窗口，你可以在其中选择对 IDE 硬盘和 ATAPI CD-ROM 支持。

### SCSI 支持（设备驱动程序）[SCSI Support]

如果你的系统上有任何 SCSI 设备，请确保 SCSI Support 窗口中的条目设置为 Yes。在这里，你可以启用对 SCSI 设备、磁带设备和 CD-ROM 的支持。SCSI Low-Level Drivers 窗口显示 Linux 目前支持的广泛 SCSI 设备列表。从那里选择你选中的设备。

### 网络设备支持（设备驱动程序/网络支持）[Network Device Support]

Network Device Support 窗口列出了网络设备的通用功能。有特定的窗口列出特定类型网络设备的支持列表，包括以太网（10 或 100MB）设备、令牌环网设备、WAN 接口和 AppleTalk。其中许多功能被创建为模块，你可以根据需要加载。你可以选择重新编译你的内核，并将这些设备中的任何一个支持支持直接构建到内核中。

### 多媒体设备（设备驱动程序）[Multimedia Devices]

多媒体设备为各种多媒体卡以及 Video4Linux 提供支持。

### 文件系统（文件系统）[File Systems]

File Systems 窗口列出了 Linux 支持的不同类型文件系统。这些包括 Windows 文件系统，如 DOS、VFAT (Windows 95/98) 和 NTFS，以及 CD-ROM 文件系统，如 ISO 和 UDF。还包括网络文件系统，如 NFS、SMB (Samba) 和 NCP (NetWare)，以及各种杂文件系统，如 HFS (Macintosh)。

### 字符设备（设备驱动程序）[Character Devices]

Character Devices 窗口列出了键盘、鼠标和串口端口等设备的功能。对串口鼠标和总线鼠标都有支持。

### 音频（设备驱动程序）[Sound]

对于 2.4 内核，Sound 窗口列出了内核支持的不同声卡。选择你系统上的那一个。对于较旧的系统，你可能选择提供声卡使用的 IRQ、DMA 和基础 I/O。这些被编译为单独的模块，如果你愿意，可以将其中一些直接包含内核。对于 2.6 内核，你可以选择高级 Linux 架构（Advanced Linux Architecture）音频支持，将其扩展到特定音频设备的驱动程序（也包含了 Open Sound System，尽管已弃用）。

- 蓝牙设备（设备驱动程序/网络）[Bluetooth Devices]：此处支持支持蓝牙的外围设备、USB、串口和 PC 接口。

- **内核黑客 (Kernel Hacking)**：Kernel hacking 窗口列出了对在内核级工作并需要修改内核的开发者感兴趣的功能。Save And Exit 选项会覆盖你的配置。Store To Configuration 选项允许你保存你的配置。

## 编译并安装内核

现在配置已经就绪，你可以编译内核了。你首先需要生成依赖树，以根据你的配置确定要编译内核的部分。在 `/usr/src` 使用以下命令：

```bash
make dep
```

你还需要清理之前编译留下的任何对象文件和依赖。使用以下命令删除此类文件：

```bash
make clean
```

你可以使用多个选项来编译内核（参见表 33-1）。`bzImage` 生成一个名为 `bzImage` 的内核并将其放在 `arch` 目录。对于 Intel 和 AMD 系统，你可以在 `i86` 子目录找到它。

```bash
make bzImage
```

表 33-1 中的选项创建的是内核，而不是编译成独立模块的内核特性。要编译你的模块，请使用带有 `modules` 参数的 `make` 命令。

```bash
make modules
```

表 33-1：`make Kernel` 的编译选项

| 选项 | 描述 |
| --- | --- |
| `bzImage` | 创建名为 `bzImage` 的内核文件，位于 `/usr/src/linux/arch` 或 `arch/i86/boot` 目录。 |
| `install` | 创建内核并安装到你的系统。 |
| `zdisk` | 创建内核并安装到软磁盘（创建启动磁盘）。 |
| `bzImage` | 创建压缩的内核文件并命名为 `bzImage`。 |
| `bzdisk` | 创建内核并安装到软磁盘（创建启动磁盘）。 |

```bash
make modules_install
```

要安装模块，请使用带有 `modules_install` 选项的 `make` 命令。这将模块安装在 `/lib/modules/version-num` 目录下，其中 `version-num` 是内核的版本号。在安装新模块之前，你应该对旧模块进行备份复制。

`install` 选项既生成内核文件，又将其作为 `vmlinuz` 安装到你的系统中，并结合了 `make bImage` 关。此操作会将像 `bImage` 文件之类的内核文件放在 `/boot` 目录下，并赋予它们适当的名称和内核版本。

```
make install
```

如果你是使用 `loadlin` 启动 Linux，则需要将 `bImage` 文件拷贝到启动 Linux 的 DOS 分区上的 `loadlin` 目录中。

这里是简单编译和安装的命令：

```
make dep
make clean
make bImage
make modules
make modules_install
make install
```

如果你愿意，你可以在更少的行数内输入所有内容，并用分号分隔命令，如下所示：

`make dep; make clean; make bImage; make modules`

`make modules_install; make install`

在单行上执行这些操作更安全的方法是让它们相互产生条件依赖关系，使用 `&&`。在一种方法中，如果某个操作发生错误，下一个操作仍会执行。通过使操作具有条件性，只有在前一个操作成功时才会运行下一个操作。

`make dep && make clean && make bImage`

`make modules`

`make modules_install && make install`

## 手动安装内核镜像
