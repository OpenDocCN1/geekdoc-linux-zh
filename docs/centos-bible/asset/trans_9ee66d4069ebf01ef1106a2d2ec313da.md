
## 第一部分 入门

- **空闲空间** — 如果你的整个硬盘只包含一个 Windows 分区，你可以调整现有分区的大小，将部分空闲空间分配给 Linux 分区。请注意这里显示的空闲空间数量，并将其与安装 Linux 所需的空间（前文已描述）进行比较。

尽管我已经使用 **GParted** 工具成功调整了多个 NTFS 分区的大小，但我仍建议在继续操作前保持谨慎（并最好为数据做好备份）。如果你更倾向于使用商业产品来调整分区大小，我在下面列出了几款产品。我并未测试过这些产品，之所以提及它们，仅仅是因为我听说过其他用户成功的报告：

- **Norton Partition Magic** — 我听说使用 Partition Magic (www.symantec.com/norton/partitionmagic) 来调整 NTFS 分区大小的用户反馈良好。Partition Magic 还可以帮助你创建新分区并管理它们。它支持 Windows XP 专业版/家庭版、Windows 95b–98SE、Windows Me、Windows 2000 专业版以及 NT 4.0 工作站（SP6a）。

- **Acronis OS Selector** — 这是一款备受好评的分区管理、创建和大小调整产品，现在已包含在 Acronis Disk Director Suite 中。它支持多种文件系统类型，包括 FAT12、FAT16、FAT32、NTFS 以及 Linux 分区类型（ext2、ext3 和 Linux ReiserFS）。它还支持与 Partition Magic 相同的 Windows 平台。

Microsoft Windows Vista 现在附带了用于调整磁盘分区大小的工具。从“开始”菜单中，右键单击“计算机”并选择“管理”。在出现的左侧窗格中，选择“存储”，然后点击“磁盘管理”。然后右键单击你想要调整的卷，并选择“扩展卷”或“压缩卷”以更改其大小。

我在这里描述的用于调整磁盘大小的开源工具称为 **GParted**。它可以用来调整包含各种文件系统类型的分区。

如果你的 Windows 系统已备份且磁盘已碎片整理，你可以开始使用随本书附带的 CentOS Live CD 和 GParted 来调整 NTFS 或 VFAT 磁盘分区。以下是使用该 CD 调整 NTFS 分区大小的步骤：

1. 插入 CentOS Live CD 并重启计算机。
2. 当 CD 启动到 GNOME 桌面时，若要开始调整硬盘，你需要安装提供 NTFS 支持的两个软件包（如果你的分区是 VFAT，则可以跳过安装与 NTFS 相关的软件包）以及来自 RPMForge 仓库的 gparted 软件包（关于启用第三方仓库，参见第 5 章）。假设你拥有互联网连接，请在终端窗口中输入以下命令：

```bash
$ su -
# yum install ntfsprogs fuse-ntfs-3g gparted
```

3. 从“应用程序”菜单中选择“系统工具 ▷ GParted”。GParted 图形化分区工具将打开，显示你当前的磁盘分区。
4. 选择你要调整的磁盘（通常是 /dev/sda）和分区（对于 Windows 分区，通常是 NTFS 或 VFAT）。“调整大小/移动”按钮此时应变为可用状态。
5. 选择*调整大小/移动*按钮以打开“调整大小/移动”弹出窗口。
6. 从右侧拖动滑块条，以选择你希望调整分区的大小。“新大小”框显示分区的新大小。“后面的空闲空间 MiB”框显示完成后你将拥有的空闲空间数量。在我的示例中，在一个小磁盘上，我将 /dev/sda1 调整到约 15 GB，留给我约 5 GB 的空闲空间，以便稍后用于安装 CentOS（通常，如果空间允许，你希望为 CentOS 分配更多空间）。图 2-1 显示了 GParted 窗口将约 20 GB 的分区调整到约 15 GB 的过程。

![](img/2f265415ceec72538dd3c78ffca75c10_82_0.png)

7. 点击*调整大小/移动*以开始调整分区。完成后，你将看到调整后的分区以及一个新条目，显示空闲空间。

> **注意**
> 调整操作将在下一步提交。如果你感到不安，此时可以退出而不做任何更改。无论如何，请确保你正在调整的分区没有被挂载。在此示例中，在运行下一步之前，我会在 shell 中以 root 用户身份输入 `umount /dev/sda1`。

8. 如果新的分区大小看起来正常，点击**应用**以提交更改。
9. 此时，你可以关闭 GParted 窗口，并开始使用刚才释放出的磁盘空间，按照常规流程安装 CentOS。

安装 CentOS 之后，还有一些其他有用的操作你可能希望执行，以便在 Linux 中使用 Windows 分区中的文件。

### 在 Linux 中使用 Windows 分区

> **注** 默认情况下，CentOS 被配置为隐藏 GRUB 启动屏幕，该屏幕允许你选择要启动的操作系统。你需要在 CentOS 启动屏幕倒计时 5 秒期间按任意键，才能看到 GRUB 启动屏幕。你可能需要考虑编辑 `grub.conf` 文件，如本章稍后所述。个人而言，我删除了 `hiddenmenu` 行，并将超时时间从 5 秒增加到 10 秒。

当磁盘上有可用空间时，在安装 Linux 时，考虑在你的磁盘上添加一个小容量的 FAT16 或 FAT32 分区（例如 2 GB）。所有 x86 操作系统（Linux、Windows 95、NT、2000、XP、Vista 和 DOS）都支持这些类型。添加该分区后，你将能够自由地在 Linux 和 Windows 系统之间通过该 FAT16 分区交换文件。

不过，对于 FAT 分区，请记住存在局限性。FAT 的文件大小限制在 2 GB 到 4 GB 之间。此外，FAT16 不支持长文件名。FAT 文件系统的总分区大小为 32 GB。

在通过上述过程释放的空间中安装 Linux 后，当启动过程中出现 CentOS 启动屏幕时，你应该能够在 Linux 和 Windows 之间进行选择。按任意键进入 GRUB 启动屏幕。然后使用方向键选择启动 Linux 或 Windows。

第一次启动 Windows 时，系统可能会要求检查磁盘（因为你的 Windows 分区大小将与预期不同）。在此之后，使用 Windows 系统的方式应该没有变化。你的磁盘空间只是变小了而已。

现在，当你启动 Linux 时，如果你的 Windows 分区上有很多文档、数字图像、音乐或其他内容，你可能希望从 Linux 中使用这些内容。为此，你需要：

- 确定哪个分区是你的 Windows 分区。
- 如果在安装期间未操作，请为你的 Windows 分区文件系统类型添加 Linux 支持。由于 VFAT 已内置，如果这是文件系统类型，这意味着需要添加 NTFS 支持。
- 在 Linux 文件系统中挂载 Windows 分区。

以下过程描述了如何执行这些操作：

**1. 检查分区** — 要确定哪个分区包含你的 Windows 文件系统，请按照以下方式使用 `fdisk` 命令：

```bash
# fdisk -l
Disk /dev/sda: 60.0 GB, 60011642880 bytes
16 heads, 63 sectors/track, 116280 cylinders
Units = cylinders of 1000 * 512 = 516096 bytes
```

| 设备 | 启动 | 起始 | 结束 | 块数 | Id | 系统 |
|---|---|---|---|---|---|---|
| /dev/sda1 | * | 1 | 41725 | 21029053+ | 7 | HPFS/NTFS |
| /dev/sda2 | | 106741 | 116280 | 4808160 | 12 | Compaq diagnostics |
| /dev/sda3 | | 41725 | 41932 | 104422+ | 83 | Linux |
| /dev/sda4 | | 41932 | 106734 | 3260145 | 5 | Extended |
| /dev/sda5 | | 41932 | 106718 | 32652081 | 8e | Linux LVM |

在此示例中，Windows 分区位于设备 /dev/sda1，且为 NTFS 文件系统。（另一种常见的 Windows 文件系统类型是 VFAT。）

**2. 获取 NTFS 支持** — 如果你有 VFAT 文件系统，可以跳过此步骤。如果你有 NTFS 文件系统且尚未安装 NTFS 支持，你可以安装必要的驱动程序和工具，以便在 Linux 中挂载并使用你的 NTFS 文件系统。你需要激活 RPMForge 仓库（参见第 5 章），然后在终端窗口中以 root 用户身份运行以下 yum 命令：

```bash
# yum install ntfsprogs fuse-ntfs-3g
```

假设你拥有活跃的互联网连接，这将安装你从 Linux 访问 NTFS 分区所需的 NTFS 支持。

**3. 挂载 Windows 文件系统** — 你可以使用 mount 命令从 Linux 访问你的 Windows 文件系统。假设你的 Windows 分区是位于 /dev/sda1 上的 NTFS 文件系统（如上述示例），你可以输入以下内容来创建 Windows 挂载点并在那里挂载文件系统：

```bash
# mkdir /mnt/win
# chmod 755 /mnt/win
# mount -t ntfs /dev/sda1 /mnt/win
# chmod 755 /mnt/win
# ls /mnt/win
```

如果你的 Windows 分区是 VFAT 文件系统，请将 ntfs 替换为 vfat。ls 命令仅仅是为了查看你是否能看到 Windows 分区的内容。

你可以通过在 /etc/fstab 文件中添加条目来永久实现挂载。以下是你可以添加到 /etc/fstab 中的一行示例，以便每次系统重启时都挂载该分区：

```
/dev/sda1	/mnt/win	ntfs	ro	0	0
```

此时，你可以像使用系统上的其他文件一样，使用来自 Windows 分区的文件。你可以打开文件夹或将目录更改为 /mnt/win 目录以查看内容。然后使用你选择的任何应用程序来打开你的文档（OpenOffice.org）、音乐（Rhythmbox）、图像（Gimp），或你想从 Windows 分区在 Linux 中使用的任何其他内容类型。

> **注** 如果你的 Linux 系统使用 ext2 或 ext3 文件系统（CentOS 通常如此），你也可以执行相反的操作：从 Windows 访问你的 Linux 分区。关于如何执行此操作的信息，请参阅 Windows 下的 Ext2 可安装文件系统 (www.fs-driver.org)。

