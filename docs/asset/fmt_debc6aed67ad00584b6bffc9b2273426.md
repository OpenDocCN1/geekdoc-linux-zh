
# 第 2 章：安装 Fedora

1. 插入 Fedora 7 Desktop Live CD 并重启电脑。

2. 在启动提示处，高亮第一项，按回车。

3. 当现场 CD 启动到 GNOME 桌面时，开始调整硬盘，从顶部面板选择应用程序 -> 系统 -> gParted。`gParted` 图形工具打开，显示你当前的磁盘分区。

4. 选择要调整的分区。`调整/移动`按钮应变为可用。

5. 点击`调整/移动`按钮打开弹出窗口。

6. 拖住滑动条块并移动它，以选择你想调整分区的大小。新大小框显示大小，剩余 MiB 框显示完成后有多少可用空间。在我的示例中，我将 `/dev/sda1` 调整到大约 15GB，留下了大约 5GB 的空闲空间供我安装 Fedora（通常情况下，如果空间允许，Fedora 需要更多空间）。图 2-1 显示了 `gParted` 窗口将一个约 20GB 的分区调整到大约 15GB。

7. 点击`调整/移动`（Resize/Move）开始调整分区大小。完成后，你将看到调整大小后的分区以及一个显示可用空间的新条目。

> 注意：调整操作将在下一步中提交。如果你感到紧张，可以退出且不进行任何更改。在任何情况下，请确保你正在调整大小的分区未挂载。在示例中，我会在运行下一步之前，以 root 身份在 shell 中输入 `unmount /dev/sda1`。

8. 如果新分区的大小看起来正确，点击`应用`（Apply）以提交更改。

9. 此时，你可以关闭 GParted 窗口，并使用刚刚释放的磁盘空间开始 Fedora 或 RHEL 的常规安装。

![](img/74f214fbb2938b570bec5f957507ac66_98_0.png)

图 2-1：使用 GParted 调整你的 Windows 分区大小。

安装完 Fedora 或 RHEL 之后，你可能想做一些有用操作，例如在 Linux 中使用 Windows 分区中的文件。

> 注意：默认情况下，Fedora 和 RHEL 配置为隐藏允许操作系统启动的 GRUB 启动界面。你需要在 Fedora 启动界面倒计时 5 秒时按下回车键才能看到 GRUB 启动界面。你可以考虑修改 `grub.conf` 文件，本章稍后会介绍。我个人删除了 `hiddenmenu` 行并将超时时间从 5 秒增加到 10 秒。

## 在 Linux 中使用 Windows 分区

当磁盘上有可用空间时，在安装 Linux 时，考虑在磁盘上添加一个小的 FAT16 或 FAT32 分区（可能是 2GB）。每个 x86 操作系统（Linux、Windows 95、NT、2000、XP 和 DOS）都支持这些类型。添加后，你就可以在 FAT16 分区上于 Linux 和 Windows 系统之间自由交换文件。

然而，请记住 FAT 分区存在局限性。FAT 的文件大小限制在 2GB 到 4GB 之间。此外，FAT16 不支持长。FAT 文件系统的总分区大小为 32GB。

在通过前面的步骤释放空间安装好 Linux 后，当启动时出现 Fedora 或 RHEL 启动界面时，你应该能够选择 Linux 或 Windows。按任意键进入 GRUB 启动界面。然后移动方向键选择启动 Linux 或 Windows。

第一次启动 Windows 时，你可能会被要求检查磁盘（因为你的 Windows 分区大小与预期不符）。之后，你使用 Windows 系统的方式应该不会有变化。你的磁盘空间会变小。

现在，当你启动 Linux 时，如果你在 Windows 分区上有大量的文档、数字图像、音乐或其他内容，你可能希望从 Linux 中使用这些内容。要做到这一点，你需要：

- 确定哪个分区是你的 Windows 分区。
- 如果在安装期间没有这样做，请为 Linux 添加对 Windows 分区文件类型的支持。由于 VFAT 已经是内置的，这意味着如果文件类型是 NTFS，则需要添加 NTFS 支持。
- 在 Linux 文件系统上挂载 Windows 分区。

下面的步骤描述了如何执行这些操作。

### 1. 检查分区

要确定哪个分区包含你的 Windows 文件系统，请如下所示使用 `fdisk` 命令：

```
# fdisk -l
Disk /dev/sda: 60.0 GB, 6001642880 bytes
16 heads, 63 sectors/track, 116280 cylinders
Units = cylinders of 1008 * 512 = 516096 bytes
```

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/sda | | 1 | 41725 | 21029053+ | 7 | HPFS/NTFS |
| /dev/sda2 | | 106741 | 116280 | 4088160 | 12 | Compaq diagnostics |
| /dev/sda3 | | 41725 | 41932 | 104422+ | 83 | Linux |
| /dev/sda4 | | 41932 | 106734 | 32660145 | 5 | Extended |
| /dev/sda5 | | 41932 | 106718 | 32652081 | 8e | Linux LVM |

在示例中，`/dev/sda` 分区是 NTFS 文件系统。（另一种常见的 Windows 文件系统类型是 VFAT）。

### 2. NTFS 支持

如果你是 VFAT 文件系统，可以跳过此步骤。如果你是 NTFS 文件系统且尚未安装 NTFS 支持，可以通过在终端中以 root 身份运行以下 `yum` 命令来安装必要的驱动程序和工具，以便在 Linux 中挂载并使用你的 NTFS 文件系统：

```
# yum install ntfs-3g
```

假设你已连接到互联网，这将安装你所需的 NTFS 支持，以便从 Linux 访问 NTFS 分区。

### 3. 挂载 Windows 文件系统

你可以使用 `mount` 命令从 Linux 访问你的 Windows 文件系统。假设你的 Windows 分区是 `/dev/sda` 上的 NTFS 文件系统（如上例所示），你可以输入以下内容创建挂载点并挂载文件系统：

```
# mkdir /mnt/win
# chmod 755 /mnt/win
# mount -o -t ntfs /dev/sda /mnt/win
# chmod 755 /mnt/win
# ls /mnt/win
```

`-o ro` 选项将只读模式挂载文件系统。读写支持不被认为是稳定的（如果你移除 `-o` 选项进行读写挂载，风险自担）。如果你的 Windows 分区是 VFAT 文件系统，请将 `ntfs` 替换为 `vfat`。`ls` 命令仅用于确认你是否可以看到 Windows 分区的内容。

你可以通过向 `/etc/fstab` 添加条目来实现持久挂载。以下是在 `fstab` 中添加的行示例，以便在系统启动时自动挂载该分区：

```
/dev/sda /mnt/win ntfs ro 0 0
```

## 磁盘设置说明

- **挂载点/RAID/卷 (Mount Point/Raid/Volume)** — 分区连接到 Linux 文件系统的目录（如果是的话）。继续之前必须将根分区 (`/`) 分配原生 Linux 分区。如果你正在使用 RAID 或 LVM，RAID 设备或 LVM 卷将在此处。
- **类型 (Type)** — 安装在磁盘分区上的文件系统类型。大多数情况下，文件系统是 Linux (`ext3`)、Win FAT (`vfat`) 或 Linux swap（交换）。不过，你也可以使用之前的 Linux 文件系统 (`ext2`)、物理卷 (`LVM`) 或软件 RAID。事实上，在安装 Fedora 或 RHEL 时，根文件系统默认使用 LVM。这允许你在以后需要时为该分区添加更多磁盘空间，而无需创建一个新分区。

![](img/74f214fbb2938b570bec5f957507ac66_102_0.png)

图 2-2：在磁盘设置向导安装期间对磁盘进行分区。

- **格式化 (Format)** — 表示安装过程是否应该格式化硬盘分区（打钩）或不（不打钩）。标记勾选的分区将被擦除！因此，在多引导系统中，请确保你的 Windows 分区以及包含数据的其他分区未被勾选！
- **大小 (MB)** — 分配给分区的磁盘空间量。如果你选择让分区扩展到现有空间，此数字可能远大于请求量。
- **起始/结束 (Start/End)** 代表分区在硬盘上的起始磁道和结束磁道。

# 第一部分：在 Fedora 和 RHEL 中入门

在顶部区域，你可以看到连接到计算机的每块硬盘。首先显示驱动器名称。几何部分 (Geom) 分别显示磁盘上磁道、磁头和扇区的数量。随后是磁盘的型号名称。磁盘空间总量和可用空间以兆字节为单位显示。

## 分区的理由

关于如何划分硬盘，有不同的意见。以下是一些问题：
