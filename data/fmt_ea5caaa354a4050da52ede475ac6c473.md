
- 删除此系统上的所有分区：此选项将在不修改任何 Windows 分区（`FAT`、`VFAT` 和 `NTFS`）的情况下，擦除任何现有的 Linux 分区。如果你正在重新安装 Red Hat Linux（无论是双引导还是单系统配置），请使用此选项。

- 删除此系统上的所有分区：此选项最为危险，因为它会擦除硬盘上的所有内容。只有当你绝对确定磁盘上没有任何内容，或者你不想保存任何内容时，才使用此选项。如果你使用此选项，你的新 Red Hat Linux 安装将是硬盘上唯一的操作系统。

- 保留所有分区并使用现有空空间：如果你在第 2 章中使用了描述的非破坏性分区（例如使用 FIPS、`Norton Ghost` 或 `PartitionMagic`）来缩小你的 Windows 分区，请使用此选项。

你可以使用商业产品（如 `Norton Ghost 2002`）来缩小 `NTFS` 分区。缩小 Windows 分区可以释放磁盘空间，你可以用它安装 Red Hat Linux。如果你的电脑上已经存在 Windows，使用此选项将创建一个双引导配置。

除非你想擦除磁盘上的所有内容，否则永远不要选择“删除此系统上的所有分区”（`Remove All Partitions on This System`）选项！请务必小心，因为此操作会破坏所有已安装的操作系统（Windows 和 Red Hat Linux）和数据。例如，如果你的电脑预装了 Windows，且你想将其转换为仅运行 Red Hat Linux 的工作站，可以使用此选项。

![](img/453364505e32ffec24f7d88ac7824962_59_0.png)

如果你想在硬盘上额外的未使用空间上安装 Red Hat Linux（例如，如果你已经按照第 2 章所述的方法缩小了现有的 `FAT` 或 `NTFS` 分区），请选择标记为“保留所有分区并使用现有空空间”（`Keep All Partitions and Use Existing Free Space`）的选项。

### 4. 选择最适合你的自动分区选项

如果你在第 2 章中划分了 Windows 磁盘以为 Linux 留空间，请点击标记为“保留所有分区并使用现有空空间”的按钮。Red Hat Linux 安装系统将使用磁盘上的额外空间。

可选，如果你要在旧的 Linux 安装上覆盖，点击“删除此系统上的所有 Linux 分区”（`Remove All Linux partitions on This System`）按钮。

可选，如果你想擦除任何现有的操作系统并重新开始，请点击“删除此系统上的所有 Linux 分区”（`Remove All Linux partitions on This System`）按钮（注：此处原文可能有误）。选择标记为“保留所有分区并使用现有空空间”（`Keep All Partitions and Use Existing Free Space`）的选项，如果你想在硬盘上额外的未使用空间上安装 Red Hat Linux（注，此处翻译逻辑遵循原文）。

### 3. 点击“是”（Yes）按钮将创建一个新的分区表

（选择“否”将停止安装过程并重启你的电脑。）

出现“自动分区”窗口。你有三个选项：

- 删除此系统上的所有分区：此选项将在不修改任何 Windows 分区（`FAT`、`VFAT` 和 `NTFS`）的情况下，擦除任何现有的 Linux 分区。如果你正在重新安装 Red Hat Linux（无论是双引导还是单系统配置），请使用此选项。

- 删除此系统上的所有分区：此选项最为危险，因为它会擦除硬盘上的所有内容。只有当你绝对确定磁盘上没有任何内容，或者你不想保存任何内容时，才使用此选项。如果你使用此选项，你的新 Red Hat Linux 安装将是硬盘上唯一的操作系统。

- 保留所有分区并使用现有空空间：如果你在第 2 章中使用了描述的非破坏性分区（例如使用 FIPS、`Norton Ghost` 或 `PartitionMagic`）来缩小你的 Windows 分区，请使用此选项。

你可以使用商业产品（如 `Norton Ghost 2002`）来缩小 `NTFS` 分区。缩小 Windows 分区可以释放磁盘空间，你可以用它安装 Red Hat Linux。如果你的电脑上已经存在 Windows，使用此选项将创建一个双引导配置。

除非你想擦除磁盘上的所有内容，否则永远不要选择“删除此系统上的所有分区”（`Remove All Partitions on This System`）选项！请务必小心，因为此操作会破坏所有已安装的操作系统（Windows 和 Red Hat Linux）和数据。例如，如果你的电脑预装了 Windows，且你想将其转换为仅运行 Red Hat Linux 的工作站，可以使用此选项。

![](img/453364505e32ffec24f7d88ac7824962_59_0.png)

选择标记为“保留所有分区并使用现有空空间”（`Keep All Partitions and Use Existing Free Space`）的选项，如果你想在硬盘上额外的未使用空间上安装 Red Hat Linux（例如，如果你已经按照第 2 章所述的方法缩小了现有的 `FAT` 或 `NTFS` 分区）。

### 4. 选择最适合你的自动分区选项

如果你在第 2 章中划分了 Windows 磁盘以为 Linux 留空间，请点击标记为“保留所有分区并使用现有空空间”的按钮。Red Hat Linux 安装系统将使用磁盘上的额外空间。

可选，如果你要在旧的 Linux 安装上覆盖，点击“删除此系统上的所有 Linux 分区”（`Remove All Linux partitions on This System`）按钮。

可选，如果你想擦除任何现有的操作系统并重新开始，请点击“删除此系统上的所有 Linux 分区”（`Remove All Linux partitions on This System`）按钮（注：此处原文可能有误）。选择标记为“保留所有分区并使用现有空空间”（`Keep All Partitions and Use Existing Free Space`）的选项，如果你想在硬盘上额外的未使用空间上安装 Red Hat Linux。

### 3. 点击“是”（Yes）按钮将创建一个新的分区表

（选择“否”将停止安装过程并重启你的电脑。）

出现“自动分区”窗口。你有三个选项：

- 删除此系统上的所有分区：此选项将在不修改任何 Windows 分区（`FAT`、`VFAT` 和 `NTFS`）的情况下，擦除任何现有的 Linux 分区。如果你正在重新安装 Red Hat Linux（无论是双引导还是单系统配置），请使用此选项。

- 删除此系统上的所有分区：此选项最为危险，因为它会擦除硬盘上的所有内容。只有当你绝对确定磁盘上没有任何内容，或者你不想保存任何内容时，才使用此选项。如果你使用此选项，你的新 Red Hat Linux 安装将是硬盘上唯一的操作系统。

- 保留所有分区并使用现有空空间：如果你在第 2 章中使用了描述的非破坏性分区（例如使用 FIPS、`Norton Ghost` 或 `PartitionMagic`）来缩小你的 Windows 分区，请使用此选项。

你可以使用商业产品（如 `Norton Ghost 2002`）来缩小 `NTFS` 分区。缩小 Windows 分区可以释放磁盘空间，你可以用它安装 Red Hat Linux。如果你的电脑上已经存在 Windows，使用此选项将创建一个双引导配置。

除非你想擦除磁盘上的所有内容，否则永远不要选择“删除此系统上的所有分区”（`Remove All Partitions on This System`）选项！请务必小心，因为此操作会破坏所有已安装的操作系统（Windows 和 Red Hat Linux）和数据。例如，如果你的电脑预装了 Windows，且你想将其转换为仅运行 Red Hat Linux 的工作站，可以使用此选项。

![](img/453364505e32ffec24f7d88ac7824962_59_0.png)

选择标记为“保留所有分区并使用现有空空间”（`Keep All Partitions and Use Existing Free Space`）的选项，如果你想在硬盘上额外的未使用空间上安装 Red Hat Linux（例如，如果你已经按照第 2 章所述的方法缩小了现有的 `FAT` 或 `NTFS` 分区）。

### 4. 选择最适合你的自动分区选项

如果你在第 2 章中划分了 Windows 磁盘以为 Linux 留空间，请点击标记为“保留所有分区并使用现有空空间”的按钮。Red Hat Linux 安装系统将使用磁盘上的额外空间。

可选，如果你要在旧的 Linux 安装上覆盖，点击“删除此系统上的所有 Linux 分区”（`Remove All Linux partitions on This System`）按钮。
