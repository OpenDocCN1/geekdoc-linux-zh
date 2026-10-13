
```
# grub2-editenv list
saved_entry=f86218lbe19a40ae921f10fc572174d3-5.14.0-162.23.1.el9_1.x86_64
menu_auto_hide=1
boot_success=1
boot_indeterminate=0
save_default=true
```

请注意，`saved_entry`值现在已设置为 Linux 启动分区。更改默认值后，按如下方式重新生成启动配置文件：

```
# grub2-mkconfig --output=/boot/grub2/grub.cfg
```

重新启动系统并验证启动菜单是否默认为 Windows 选项，并且在超时到期后 Windows 加载。

### 4.3 从 RHEL 9 访问 Windows 分区

在双启动配置中运行 RHEL 时，可以通过从命令行手动挂载分区来访问位于 Windows 分区上的文件。但是，在这样做之前，需要在系统上安装一些额外的软件包。首先，需要下载并安装 fuse 内核模块：

```
# dnf install fuse
# modprobe fuse
```

接下来，需要安装 Fuse NTFS 驱动程序。不幸的是，此软件包未包含在标准 RHEL 9 仓库中，因此需要按如下方式将企业版 Linux 额外软件包（EPEL）仓库添加到系统中：

```
# subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
# dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
```

添加 EPEL 仓库后，现在可以安装驱动程序：

```
# dnf install ntfs-3g
```

安装所需软件包后，下一步是创建一个目录用作 Windows 分区的挂载点。在此示例中，我们将创建一个名为`/mnt/windows`的目录：

```
# mkdir /mnt/windows
```

要识别分配给 Windows 分区的设备名称，请按如下方式使用`fdisk`命令：

```
# fdisk -l
```

| 设备 | 起始 | 结束 | 扇区 | 大小 | 类型 |
|---|---|---|---|---|---|
| `/dev/nvme0n1p1` | 2048 | 206847 | 204800 | 100M | EFI 系统 |
| `/dev/nvme0n1p2` | 206848 | 239615 | 32768 | 16M | Microsoft 保留 |
| `/dev/nvme0n1p3` | 239616 | 49362943 | 49123328 | 23.4G | Microsoft 基本数据 |
| `/dev/nvme0n1p4` | 132933632 | 134213631 | 1280000 | 625M | Windows 恢复环境 |
| `/dev/nvme0n1p5` | 49362944 | 51460095 | 2097152 | 1G | Linux 文件系统 |
| `/dev/nvme0n1p6` | 51460096 | 132933631 | 81473536 | 38.8G | Linux LVM |

在上述输出中，包含我们需要访问的文件的主要 Windows 分区由`/dev/nvme0n1p3`表示。接下来，我们需要按如下方式运行`mount`命令（假设 Windows 分区为`/dev/nvme0n1p3`）：

```
# mount /dev/nvme0n1p3 /mnt/windows
```

通过列出挂载点的顶级目录内容来检查挂载是否成功：

```
# ls /mnt/windows
'$Recycle.Bin' ProgramData swapfile.sys
'Documents and Settings' 'Program Files' 'System Volume Information'
pagefile.sys 'Program Files (x86)' Users
PerfLogs Recovery Windows
```

要使系统每次启动时自动挂载，请将适当的挂载行添加到`/etc/fstab`文件中：

```
/dev/nvme0n1p3 /mnt/windows ntfs defaults 0 0
```

要随时卸载 Windows 文件系统：

```
# umount /mnt/windows
```

### 4.4 摘要

通过创建双启动环境，RHEL 9 可以与 Windows 操作系统安全地共存于同一磁盘驱动器上。这涉及在执行安装之前缩小 Windows 系统的空间以腾出空间供 RHEL 9 使用。安装 RHEL 后，必须修改启动菜单配置以包含从 Windows 启动的选项。要从 RHEL 访问 Windows 文件系统，需要安装 Fuse NTFS 驱动程序并使用它来挂载 Windows 分区。

## 5. 将 Windows 磁盘分区分配给 RHEL 9

在上一章中，我们研究了在与 Windows 相同的磁盘上安装 Red Hat Enterprise Linux 9。此所谓的“双启动”配置允许用户在单个磁盘驱动器上同时安装两个操作系统，并在系统通电时选择启动其中一个。

本章适用于决定喜欢 RHEL 9 足够以从磁盘中完全删除 Windows 并将所得空间用于 Linux 的用户。在以下各节中，我们将逐步完成此过程。

### 5.1 卸载 Windows 分区

如果按照“使用 Windows 双启动 RHEL 9”章节中的步骤从 RHEL 9 中挂载 Windows 分区，则在继续本章之前应采取步骤卸载该分区。假设 Windows 分区已挂载为`/mnt/windows`，可以按如下方式卸载：

```
# umount /mnt/windows
```

还应编辑`/etc/fstab`文件以删除之前添加的`/mnt/windows`自动挂载。

### 5.2 从磁盘删除 Windows 分区

释放 Windows 分区供 RHEL 使用的第一步是删除该分区。但是，在这样做之前，必须从 Windows 和 RHEL 分区备份您需要保留的任何数据。完成此操作后，可以安全地继续本章。

要删除 Windows 分区，我们首先需要使用`fdisk`工具识别它们所在的磁盘：

```
# fdisk -l
Disk /dev/nvme0n1: 64 GiB, 68719476736 bytes, 134217728 sectors
Disk model: VMware Virtual NVMe Disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimum): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 7A38CD86-091E-4781-BFB0-928FD383C935
```

| 设备 | 起始 | 结束 | 扇区 | 大小 | 类型 |
|---|---|---|---|---|---|
| `/dev/nvme0n1p1` | 2048 | 206847 | 204800 | 100M | EFI 系统 |
| `/dev/nvme0n1p2` | 206848 | 239615 | 32768 | 16M | Microsoft 保留 |
| `/dev/nvme0n1p3` | 239616 | 49362943 | 49123328 | 23.4G | Microsoft 基本数据 |
| `/dev/nvme0n1p4` | 132933632 | 134213631 | 1280000 | 625M | Windows 恢复环境 |
| `/dev/nvme0n1p5` | 49362944 | 51460095 | 2097152 | 1G | Linux 文件系统 |
| `/dev/nvme0n1p6` | 51460096 | 132933631 | 81473536 | 38.8G | Linux LVM |

在上述示例输出中，系统包含一个物理磁盘驱动器，其设备名为`/dev/nvme0n1`。在该磁盘驱动器上，有六个分区，其设备名分别为`/dev/nvme0n1p1`至`/dev/nvme0n1p6`。基于类型列中的值，存在三个与 Windows 相关的分区。第一个是 Windows 系统分区，而第二个、更大的分区是包含 Windows 操作系统和用户数据的 Windows 启动分区，其后是 Windows 恢复分区。

要删除分区，请使用包含分区的磁盘的设备名称（本例中为`/dev/nvme0n1`）启动`fdisk`工具，然后按照说明再次显示分区和扇区信息：

```
# fdisk /dev/nvme0n1
```
