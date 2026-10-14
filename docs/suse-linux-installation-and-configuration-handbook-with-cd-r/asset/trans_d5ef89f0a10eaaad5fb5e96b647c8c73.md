

正如你所见，这非常简单且有条理。作为示例，要在 A 驱动器中挂载软盘，输入以下命令：

```
# mount /dev/fd0 /mnt/floppy -t vfat
```

这指示操作系统将驱动器 a 中的磁盘（/dev/fd0）挂载到 /mnt/floppy 目录下，使用 Windows VFAT 作为文件系统（使用 Virtual FAT 以确保长文件名正确显示）。要查看磁盘的内容，请进入 /mnt/floppy。

如果你要挂载 CD-ROM，其过程与挂载软盘相同。你只需要知道 CD-ROM 在你的 IDE 上连接在哪里。你可以通过物理查看硬件或观察内核的启动信息来做到这一点。当内核启动时，它会显示找到的硬件及其对应的 /dev/ 文件。如果你错过了内核启动时的信息，输入 dmesg 即可再次查看。你要找的行看起来会像这样：

```
hda: WDC AC2400B, ATA DISK drive
hdb: Maxtor 9136BD6, ATA DISK drive
hdc: TOSHIBA DVD-ROM SD-M1212, ATAPI CDROM drive
hdd: ZIPCD 4x650, ATAPI CDROM drive
```

该系统有两个 CD-ROM 驱动器——Toshiba DVD-ROM，即 /dev/hdc，以及位于 /dev/hdd 的 ZIPCD 4x650。要挂载其中任意一个，使用其设备名：

```
# mount /dev/hdd /mnt/
```

这会将 ZIPCD 驱动器中的 CD 挂载到 /mnt/ 下。注意你没有使用 -t 选项。这是因为 mount 会正确猜测文件系统是 iso9660。

当你想要挂载其他分区或硬盘时，你必须指定要挂载的分区号。例如，如果你的硬盘上有 MS Windows 分区，你在挂载时必须指定其位置。要指定要挂载的分区，将其编号插入设备名之后。例如，第一个驱动器的第一个分区为 /dev/hda1，第二个为 /dev/hda2，以此类推。如果你不确定 MS Windows 安装在哪个分区上，你始终可以使用 fdisk 命令查看分区表。按以下步骤操作：

- 1. 以 root 身份运行 fdisk，并指定要查看的驱动器：
- # fdisk /dev/hda
- 2. fdisk 启动并显示命令提示符。输入 p 以显示分区表：
- Command (m for help): p
- 3. fdisk 将显示该驱动器上找到的所有分区：
- Disk /dev/hda: 255 heads, 63 sectors, 784 cylinders
- Units = cylinders of 16065 * 512 bytes

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/hda1 | * | 1 | 530 | 4257193 | 83 | Linux native |
| /dev/hda2 |  | 531 | 547 | 136552 | 82 | Linux swap |
| /dev/hda3 | * | 548 | 775 | 1831410 | c | Win95 FAT32 |

- 4. 查找系统字段中具有 Win95 的分区。
- 5. /dev/hda3 的系统字段为 Win95 FAT32。
- 6. 输入 q 退出 fdisk。

现在你知道 MS Windows 安装在 /dev/hda3 上。要挂载它，输入以下内容：

```
# mount /dev/hda3 /mnt/ -t vfat
```

再次，所有该分区的内容都将显示在 /mnt 下。

现在你知道如何挂载另一个文件系统，但如何卸载它呢？很简单；你使用 umount 命令如下：

```
# umount /mnt
```

umount 命令接受设备名或挂载点作为参数。在尝试从已挂载驱动器中取出介质之前，你必须发出此命令。在大多数情况下，除非你先卸载它，否则你甚至无法取出介质（CD-ROM 就是一个例子）。umount 命令可确保已将对已挂载介质上文件所做的所有更改保存。

## 理解 /etc/fstab

挂载和卸载文件系统可能会变得相当繁琐，尤其是在经常使用的驱动器或分区上。Linux 有一个特殊配置文件用于挂载文件系统，即 /etc/fstab。fstab 代表 Filesystem Table，即维护系统上最常见挂载配置的文件。为了进一步理解此文件，让我们看一个示例 /etc/fstab 文件：

/dev/hda1   /boot   ext2    defaults 1
/dev/hda2   swap    swap    defaults 0
/dev/hda3   /       ext2    defaults 1
proc        /proc   proc    defaults 0

此文件被系统上需要了解各种文件系统挂载点的多个程序读取。当系统启动时，它会从此文件识别系统的根分区，在本例中为 /dev/hda3。让我们来看一下此文件的格式。

此文件以单行定义每个分区或驱动器。字段使用空白分隔。第一个字段是设备字段，你在此处放置要挂载的设备名。例如，对于 CD-ROM，第一个字段将为 /dev/cdrom。

第二个字段是该设备的挂载点。这是你希望设备在本地文件系统上挂载的位置。因此对于 CD-ROM，第二个字段将为 /cdrom。

第三个字段是你希望挂载此设备的<|message|> 文件系统类型。你可以使用 mount 命令提供的任何类型：minix、ext、ext2、xiafs、msdos、vfat、hpfs、iso9660、nfs、swap 和 auto。使用 auto 会告诉 mount 尝试自动确定文件系统类型。对于 CD-ROM，第三个字段将为 iso9660。Auto 也可用，但当我们已知其类型时，无需让 mount 去猜测。

第四个字段是你希望传递给 mount 命令的选项。同样，你可以使用 mount 接受的任何选项。有关这些选项的详细列表，请查看 man mount。以下是最常见的选项：

- - defaults—默认选项为：rw、suid、dev、exec、auto、nouser 和 async。
- - auto—在系统启动时自动挂载此文件系统。
- - noauto—在启动时不要自动挂载此文件系统。
- - noexec—不允许执行二进制文件。
- - exec—允许从此文件系统执行二进制文件。
- - user—允许普通用户随意挂载此文件系统。
- - nouser—不允许用户挂载此文件系统。
- - ro—以只读方式挂载文件系统。
- - rw—以读写方式挂载文件系统。

对于 CD-ROM，你可能希望普通用户能够挂载它并从中执行二进制文件。因此，选项为 user、exec 和 noauto。请注意，如果你不希望系统在启动时尝试挂载 CD-ROM 驱动器，应使用 noauto 选项。

第五个字段特定于 dump 命令。此命令备份第二扩展文件系统。如果你想使用此命令，应在此字段输入 1；否则输入 0。请注意，dump 仅适用于 ext2 类型的文件系统。对于 CD-ROM，你将输入 0。

第六个也是最后一个字段由 fsck 命令读取。此命令检查文件系统的完整性。如果你在此字段输入 1，fsck 理解为在必要时应检查此文件系统是否有错误；如果你输入 0，则不会。对于 ext2 文件系统，尤其是根文件系统，输入 1。对于 CD-ROM，输入 0。

因此，现在你了解了 /etc/fstab 的格式。你也学会了如何为 CD-ROM 添加新条目。其最终形式如下：

/dev/cdrom /cdrom iso9660 user,noauto,exec 0

现在任何用户都可以通过输入以下任一命令轻松挂载 CD-ROM：

```
$mount /dev/cdrom
$mount /cdrom
```

mount 命令将读取 fstab 文件并自动理解该做什么。非常方便，不是吗？

> **CAUTION**
> 请注意，/etc/fstab 被系统上的多个程序使用。这意味着其格式必须正确。你应确保不更改此文件的权限。此文件应可被系统上所有人读取，但只有 root 可写。YaST 最终会在文件权限不正确时警告你。

## 创建和格式化文件系统

不可避免的是，在某个时候你需要创建或格式化文件系统。这可能是因为你获得了一个新硬盘或由于空间有限而释放了另一个分区。为了能够使用该新空间，你必须对其进行格式化。你应将此新空间格式化为使用第二扩展文件系统，因为这是 Linux 使用的默认文件系统。

你需要遵循的格式化新分区或驱动器的方法取决于该空间之前有什么内容。在大多数情况下，这将是一个空白的新硬盘。在其他情况下，它可能是安装了另一个操作系统的硬盘或分区。在第一种情况下，你需要对新驱动器进行分区。在第二种情况下，你需要修改驱动器的分区。让我们看看如何做到两者。

### 格式化新驱动器或分区

假设你计划通过添加一个额外的硬盘或分区来为你的 SuSE Linux 系统增加更多空间。如果是新硬盘，你首先要做的是在其上创建新的分区表。

要为新硬盘创建新的分区表，你将使用 YaST。这是一个相当安全的程序，因为 YaST 在你确认之前不会应用任何更改。要创建新的分区表，请按以下步骤操作：

- 1. 运行 YaST。
- 2. 导航到 Adjustment of Installation，Configure Hard Disk Partitions。按 Enter。
- 3. YaST 会要求你选择要分区的硬盘。选择你的新硬盘。
- 4. 选择 Partitioning 并按 Enter。
- 5. YaST 显示你的新硬盘。它应显示 No Partitions Available，因为这是一个新硬盘。
- 6. 你要在该驱动器上创建一个或多个分区，因此按 F5。
- 7. YaST 询问你是否要创建主分区或扩展分区。选择 Primary Partition。

