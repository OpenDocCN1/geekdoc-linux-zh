
虽然 Novell Network 主要是一个网络软件包，但它自带了一套设备驱动程序（特别是针对网卡的）。这些特殊的驱动程序可以在 `VMware Workstation` 下运行，尽管在本书时，`VMware` 对 `Netware` 的支持仍处于实验阶段。（`Netware` 原本是 `DOS`，但随着每次发布，它离 `DOS` 越来越远。）我们将在本节中讨论 `Server 4` 和 `5`。

### 8.3.1 配置你的虚拟机并安装 Netware

在虚拟机上安装每个版本的 `Netware` 都相当简单，因为 `CD` 安装过程是通行的。为此，首先要配置你的虚拟机，包括所有的串口和并行口。对于 `Server 4`，将客机系统内存大小设置为 `48 MB`。对于 `Server 5`，所需的数量是 `128 MB`，尽管你可能用 `64 MB` 也能运行。请使用容量为 `2 GB` 的虚拟磁盘。

对于 `Server` 而言，你可能也希望你的虚拟机与真实网络上的设备通信。因此，你将希望使用 `VMware` 的桥接网络，而不是主机 `only` 或 `NAT` 网络（除非，你正在使用其他 `VMware` 客机系统上的客户端来测试服务器）。

### 创建分区

`Netware` 需要一个小的 `DOS` 分区来启动。`Server 5` 版本带有 `DOS 7`，因此你只需要从 `CD` 启动你的虚拟机即可。对于 `Server 4`，你需要自己创建分区（见第 5.3.3 节；不要使用 `FreeDOS`。）

此启动分区的大小应分配在 `50` 到 `60 MB` 之间；将磁盘其余部分留为空。安装 `Netware 4` 时安装 `DOS` 的重要部分是，你需要 `CD-ROM` 驱动器，以便在 `Server 4` 安装程序上运行安装程序。

提示：一旦完成分区，请立即为虚拟磁盘创建一个副本，这样如果你搞砸了网络安装，你还有一个备份。你可以使用如 `FIPS` 等程序在副本上以后调整 `DOS` 分区的大小，如果你需要将该 `DOS` 分区用于其他用途的话。

### 安装软件

现在你需要安装软件并针对 `VMware` 进行一些自定义。特别是，你需要安装一个名为 `DOSIDLE` 的 `CPU` 空闲程序（如第 5.6.1 节所述），否则你的虚拟机将耗尽主机系统允许的所有 `CPU` 时间，从而损害主机和客机的性能。你可以从 `VMware` 网站获取这些程序；使用 `nw4-idle.nlm` 和 `nw5-idle.nlm` 上的搜索功能查找它们。

### Server 5

如前所述，首先从 `CD-ROM` 启动你的虚拟机。

注意：图形控制台有一个小问题；除非你在控制台启动期间必须移动鼠标，否则它无法看到鼠标。目前，只需使用键盘安装系统；稍后我们会禁用图形控制台。

当安装程序询问你网卡时，选择 `AMD PCnet PCI` 卡；然后完成安装。完成服务器完成后，进入控制台并执行以下操作：

1. 从 `VMware` 网站将 `nw5–idle.nml` `CPU` 空闲模块复制到 `C:\NWSERVER` 目录。
2. 使用类似 `edit sys:\system\autoexec.ncf` 的命令编辑你的 `AUTOEXEC.NCF` 文件。首先，删除 `startnx.exe` 以禁用图形控制台（解决鼠标问题）。在底部添加以下内容以启用你在第 1 步中安装的 `CPU` 空闲模块：

```
LOAD C:\NWSERVER\NW5-IDLE
```

### Server 4

一旦你设置了带有 `CD-ROM` 支持的 `DOS` 分区（如之前讨论），插入 `Netware 4` 安装 `CD` 驱动器，确保驱动器已连接到你的虚拟机，使用 `cd` 命令进入驱动器，并运行安装服务器。

完全按照你常的方式安装 `Netware`，但网卡除外。当你到达该部分时，按 `F10` 跳过驱动程序安装。完成后，按如下步骤完成最后工作：

1. 进入服务器控制台，从 `VMware` 网站将 `nw4–idle.nml` 模块复制到 `C:\NWSERVER`。
2. 仍在服务器控制台时，使用 `edit sys:\system\autoexec.ncf` 编辑服务器启动文件。移动到最后并添加此处显示的用于 `VMware` 网络虚拟卡的两行。第一行加载 `PCNTNW` 驱动，第二行将 `IPX` 协议栈绑定到驱动程序：

```
LOAD PCNTNW PCI SLOT=2 FRAME=802.2,
BIND IPX TO PCNTNW NET=address
```

在这里，*type* 是你的帧类型（`Ethernet_802.2`、`Ethernet_802.3`、`Ethernet_II` 或其他），而 *address* 是你的网络地址号。

注意：如果你使用公司网站上的 `AMD` 驱动，驱动程序名称是 `CPCNTNW` 而不是 `PCNTNW`。

3. 仍在编辑器中时，添加

```
LOAD C:\NWSERVER\NW4-IDLE
```

到最底部。

4. 重启系统使更改生效。

### 8.3.2 杂记说明

由于你使用公司网站上的 `AMD` 驱动，驱动程序名称是 `CPCNTNW` 而不是 `PCNTNW`。

## 8.4.3 启动 Solaris

`Solaris` `Intel Platform` 版通过两步过程进行启动。它首先从 `DOS` 分区加载一个 (`DOS`) 配置助手。

如果你在交互模式下进入助手（如首次安装时那样），你可以从备设备启动并探测新添加的硬件。你也可以扫描特定的硬件，但要小心！如果你在扫描时漏掉了某个设备，`Solaris` 内核将无法找到它（对于键盘等小型设备来说，这可能会是一个大问题）。

注意：在 `VMware Workstation` 下，你通常不需要过多配置助手；内核应该会在重新配置启动期间自动检测大多数新设备。

## 8.4.4 与 VMware Workstation 的设备

以下是与 `VMware Workstation` 相关的设备指南。

注意：有关完整的设备列表，请参考 `AnswerBook2`（`Sun` 文档）中的 `Solaris 7` 或 `8`（`Intel Platform` 版）设备配置指南，地址位于 `http://docs.sun.com/` 以及一些镜像站点。

### IDE 磁盘

`/dev/` 下有两个目录：用于普通设备的 `/dev/dsk` 和用于直接访问磁盘的原始设备 `/dev/rdsk`。

第一个 `VMware` 设备显示为 `/dev/dsk/c0d0`，与 `BSD` 系统一样，它是被切片的（sliced）。例如，第一块磁盘 `/dev/dsk/c0d0` 是 `Solaris` 切片上的 `Unix` 分区；`/dev/dsk/c0d1` 分区是 `PC` 风格分区。`/dev/dsk` 中的每个文件在 `/dev/rdsk` 中都有同名的原始磁盘。以下是 `VMware Workstation` 下可能的名称分配完整列表：

| c0d0 | 主主 (Primary Master) |

|---|---|

| c0d1 | 主从 (Primary Slave) |

| c1d0 | 从主 (Secondary Master) |

| c1d1 | 从从 (Secondary Slave) |

要对磁盘进行分区并在上面建立文件系统，你必须对原始设备进行操作。例如，要操作主接口上的从盘，应使用 `/dev/rdsk/c0d1p0`，而不是 `/dev/dsk/c0d1p0`。

要对磁盘进行分区，请在 `Solaris Slice` 上使用 `format` 命令，例如：

```
format /dev/rdsk/c0d1p0
```

在这里，如果磁盘是空的，或者没有 `PC` 风格的分区表（如新的 `VMware` 虚拟磁盘），你必须运行 `fdisk` 来创建一个。如果 `format` 命令在磁盘上找不到分区表，它会为你运行 `fdisk`。当磁盘上有 `PC` 分区表时，在 `format` 内部运行 `partition` 命令在磁盘上创建分区。确保你已经连接了磁盘。

完成 `format` 后，你必须在分区上建立文件系统。使用 `newufs /dev/rdsk/devname`，其中 `devname` 是磁盘设备。

## 第8章：其他客户操作系统

`Solaris` 使用 `/etc/vfstab` 作为启动时挂载的文件系统列表。如果你习惯其他 `Unix`，在添加条目时要小心，确保在该文件的前两个字段中正确指定设备名称。

注意：对于 `SCSI` 磁盘，`VMware Workstation` 不支持 `BusLogic 24` 位指令集，遗憾的是，`Solaris` 使用了这些命令。因此，`SCSI` 磁盘无法 `Solaris` 虚拟机上工作。

### CD–ROM 驱动器

`VMware` 的 `ATAPI CD–ROM` 驱动器与硬盘设备一起显示在 `/dev/disk` 中，并带有一个额外的组件：目标（例如 `l0`）。如果你习惯在 `Solaris` 下操作 `SCSI` 磁盘，你会熟悉这些名称。

通常情况下，守护进程 `void` 将 `CD–ROM` 挂载到系统 `/cdrom` 下的目录中。然而，如果你出于某种原因需要设备名称（例如，想用 `dd` 复制其中的内容），请使用第一个分区。例如，`/dev/disk/c1t0d00` 适用于位于辅助接口的 `CD–ROM`。

注意：当你尝试正常访问驱动器时，`VMware` 可能会为 `CD-ROM` 驱动器标记几个未实现的致命命令。弹出消息时点击 `OK` 即可；这不会导致你的虚拟机崩溃。
