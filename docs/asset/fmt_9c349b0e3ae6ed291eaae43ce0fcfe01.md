
如果你使用的文件名不符合 ISO 标准，例如超过 31 个字符的文件名或使用小写字母的文件名，则需要包含特定选项。`-U` 选项允许使用完全不受限制的文件名，而像 `-l`（无限制长度）这样的特定选项仅解除特定限制。以下示例使用 `mdoc` 目录中的文件和子目录创建名为 `mydoc.iso` 的 CD 映像，并将 CD 映像标记为 "doc"：

```
mkisofs -v -r -T -J -U -V "Greatdocs" -o mydocuments.iso  mydocs
```

### 挂载磁盘映像

创建 CD 映像后，你可以将其挂载为 Linux 系统上的文件系统，以检查其是否正确。实际上，为了测试 CD 映像，你将其挂载到一个目录，然后像访问其他文件系统一样访问它。挂载 CD 映像需要使用回环设备（loop device）。如下一个示例所示，使用 `loop` 选项指定回环设备。这里，`mydoc.iso` 作为 `iso9660` 类型的文件系统挂载到 `/mnt/cdrom` 目录。完成后请务必卸载它。

```
mount -t iso9660 -o ro,loop=/dev/loop0 mydocuments.iso /mnt/cdrom
```

### 可启动 CD-ROM

如果你正在创建一个可启动 CD-ROM，你需要指明要使用的启动映像文件和启动目录。使用 `-c` 选项指定启动目录。使用 `-b` 选项指定启动映像。启动映像是一个启动磁盘映像，类似于用于启动安装过程的映像。例如，在 Red Hat CD-ROM 上，启动映像是 `isolinux/isolinux.bin`，启动目录是 `isolinux/boot.cat`（你也可以使用 `images/boot.img` 和 `boot.cat`）。将这些文件复制到你的硬盘。以下示例使用位于 CD-ROM 驱动器上的 Red Hat 发行版文件创建一个可启动 CD-ROM。

```
mkisofs -o rd8-0.iso -b isolinux/isolinux.bin -c isolinux/boot.cat \
-no-emul-boot -boot-load-size 4 -boot-info-table \
-v -r -R -T -J -V "Red8.0"  /mnt/cdrom
```

### cdrecord 和 dvdrecord

一旦 `mkisofs` 创建了 CD 映像文件，你可以使用 `cdrecord` 或 `cdwrite` 将其写入 CD 写入盘。如果你有一个以上的 CD-R/W 驱动器，你应通过指示其 SCSI 总线编号来指定 CD-R/W 驱动器（请记住，即使在 Linux 上 IDE CD-R/RW 驱动器也被视为 SCSI 设备）。你可以使用带有 `-scanbus` 选项的 `cdrecord` 来查找可重写设备的 SCSI 编号。在此示例中，如前 `-scanbus` 示例所示，可重写 CD-RW 驱动器的设备编号为 0,0。使用 `dev=` 选项来指示此驱动器。`cdrecord` 的最后一个参数是 CD 映像文件的名称。`dvdrecord` 在 DVD-R/RW 写入器上的工作方式相同，实际上它是 `cdrecord` 的扩展。

```
cdrecord dev=0,0 mydocuments.iso
```

如果你正在创建音频 CD，请使用 `-audio` 选项，如下所示。此选项使用 CD-DA 音频格式：

```
cdrecord dev=0,0 -audio moresongs.iso
```

类似的操作也适用于 `dvdrecord`，只是 `dvdrecord` 会将数据写入 DVD-R 驱动器上的 DVD-R 光盘。

`cdrecord` 的虚拟（dummy）选项允许你测试针对给定映像的 CD 刻录操作。

#### dvd+rw 工具

主要的 dvd+rw 工具是 `growisofs`，使用它创建 DVD+RW/R 光盘。另外还包含两个次要的辅助工具：格式化工具 `dvd+rw-format` 和兼容性工具 `dvd+rw-booktype`。详细的说明请参阅 `/usr/share/doc` 目录下的 dvd+rw-tools 页面。

`growisofs` 工具的功能与 `mkisofs` 工具类似，不同之处在于它直接写入 DVD+RW/R 光盘，而不是写入映像文件。它拥有与 `mkisofs` 相同的选项，仅有少数例外，实际上它是 `mkisofs` 命令的前端。当然，它没有指定磁盘映像文件的 `-o` 选项。你需要指定 DVD 设备。例如，要将 newsongs 目录的内容写入 DVD+RW 光盘，你可以直接使用 `growisofs`。

```
growisofs -v -V "Goodsongs" -Z /dev/scd0 newsongs
```

该设备通过其名称指定，通常第一个 SCSI 设备为 `/dev/scd0`。请记住，当系统启动时，`ide-scsi` 模块会将 IDE DVD 写入器配置为 SCSI 设备。`growisofs` 提供了一个特殊的 `-Z` 选项用于烧录初始会话。对于多会话（DVD-RW），你可以使用 `mkisofs -M` 选项。如果你想重用一张 DVD-RW 光盘，只需覆盖它即可。你不需要重新格式化它。

要将 ISO 映像文件烧录到光盘，使用 `-Z` 选项并将 iso 映像文件分配给设备。

```
growisofs -v -V "Goodsongs" -Z /dev/scd0=moresongs.iso
```

尽管 `growisofs` 会自动格式化新的 DVD+RW 磁盘，但 dvd+rw 工具还包含 `dvd+rw-format` 工具，用于明确执行仅格式化操作。你使用 `dvd+rw-format` 工具仅用于明确格式化新的 DVD+RW（读/写）磁盘，为写入做准备。这只需执行一次，且仅针对从未使用过的新 DVD+RW 磁盘。DVD+R 光盘不需要任何格式化。

`dvd+rw-booktype` 工具为可能无法读取 DVD+RW/R 磁盘的较旧的 DVD-ROM 读取器设置兼容性设置。

## 第 31 章：RAID 和 LVM

### 概述

随着廉价、高效且容量非常大的硬盘的出现，即使是专业的系统也会配备多块硬盘。使用多块硬盘为确保障存可靠性以及更轻松地组织对硬盘的访问提供了机会。Linux 提供了两种更好地管理硬盘的方法：独立磁盘冗余阵列（RAID）和逻辑卷管理（LVM）。RAID 是一种在多个硬盘的不同位置存储相同数据的方法。这些多块硬盘被视为单个硬盘。它们包含恢复信息，以便在某个驱动器发生故障时允许你恢复文件。LVM 是一种将所有硬盘组织为逻辑卷的方法，让你将几块硬盘的存储能力池化为单个逻辑卷。你的系统随后看到一个大型存储设备，你不需要微观管理每个底层硬盘及其分区。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_743_0.png)

### 在内核中启用 RAID 和 LVM

Red Hat 在 Linux 安装过程中提供了创建、安装和配置 RAID 及 LVM 设备的方法。如果你希望稍后再添加这些设备，则首先需要在内核中启用 RAID 支持。除非在安装期间安装了 RAID 设备，否则默认情况下未启用 RAID。如第 32 章和第 33 章所述，你需要配置内核模块——在此情况下，是用于 RAID 和 LVM 设备的模块。在内核配置期间，从 Linux 内核配置窗口中选择 Multi-Device Support (RAID and LVM)（多设备支持（RAID 和 LVM））。然后，你可以选择启用 RAID 和 LVM 支持，作为模块或作为内置内核功能（如果你使它们成为内核的一部分，将不得不重新构建整个内核）。对于 RAID 设备，你可以选择想要安装的 Linux 软件 RAID 设备类型。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_744_0.png)

### 配置 RAID 设备

RAID 是一种在多个磁盘上存储数据以提供更高性能和冗余的方法。实际上，你可以让操作系统将多块硬盘视为一块硬盘。然后 RAID 在所有这些磁盘之间高效地存储和检索数据，而不是让操作系统将每个磁盘作为独立的文件系统访问。存储和检索的低级细节不再由操作系统关心。这使得添加或移除硬盘具有更大的灵活性，并在存储系统中实施冗余以提高可靠性。使用 RAID，你可以拥有多块被视为一个虚拟磁盘的硬盘，其中一些磁盘用作实时镜像，复制数据。根据你所需可靠性的程度，可以以多种方式使用 RAID。当你将数据放置在多个磁盘上时，I/O 操作可以平衡地重叠，从而改善性能。由于多个磁盘增加了平均故障间隔时间（MTBF），冗余存储数据也增加了容错能力。
