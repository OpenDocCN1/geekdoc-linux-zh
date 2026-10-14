

在本节中，我们选择将用于安装根目录（/）的硬盘。默认情况下，它安装在驱动器的“a”分区上。我们还选择使用 AdvFS 作为根目录（/）所使用的文件系统。

选择根文件系统的磁盘。根文件系统将被放置在您选择的磁盘的“a”分区上。

要目视定位磁盘，输入 ‘ping <disk>’，其中 <disk> 是您要定位的磁盘的设备名称（例如，dsk0）。如果该磁盘具有可见指示灯，它将闪烁直到您准备好继续。

| Device Name | Size (GB) | Controller Type | Disk Model | Location |
|---|---|---|---|---|
| 1) dsk0 | 18.2 | SCSI | BD018635C4 | bus-5-targ-0-lun-0 |

Enter your choice: 1

选择根文件系统的文件系统类型：

1) UFS -- UNIX File System
2) AdvFS -- Advanced File System

Enter your choice: 2

对于 /usr 文件系统，我们选择与根目录（/）安装在同一设备上的“g”分区。我们对 /usr 使用 AdvFS 作为文件系统类型。

选择 /usr 文件系统所在的磁盘，或输入 ‘ping <disk>’，其中 <disk> 是设备名称（例如 dsk0）以物理识别特定磁盘。

| Device Name | Size (GB) | Controller Type | Disk Model | Location |
|---|---|---|---|---|
| 1) dsk0 | 18.2 | SCSI | BD018635C4 | bus-5-targ-0-lun-0 |

Enter your choice: 1

选择 dsk0 分区以存放 /usr 文件系统。该分区必须至少为 4GB 才能容纳您选择的软件。然而，建议大小为 700 MB 或更大，以便为额外的分层软件和未来的升级考虑留出空间。

| Partition | Size (GB) | Start Block | End Block | Overlaps |
|---|---|---|---|---|
| 1) b | 4.5GB | 1048576 | 10485760 | c |
| 2) e | 3.9GB | 10485760 | 18787864 | c |
| 3) f | 2.0GB | 18787864 | 22982168 | c |
| 4) g | 4.0GB | 22982168 | 31370776 | c |
| 5) h | 2.0GB | 31370776 | 35565080 | c |

Enter your choice: 4

选择 /usr 文件系统的文件系统类型：

1) UFS -- Unix File System
2) AdvFS -- Advanced File System

Enter your choice: 2

交换分区也将位于与根目录（/）相同的设备上。这次我们将使用“b”分区作为交换分区，因为其大小大约是内存的三倍。

选择第一个交换区（swap1）所在的磁盘，或输入 "ping <disk>" 其中 <disk> 是设备名称（例如 dsk0）以物理识别特定磁盘。

| Device Name | Size (GB) | Controller Type | Disk Model | Location |
|---|---|---|---|---|
| 1) dsk0 | 18.2 | SCSI | BD018635C4 | bus-5-targ-0-lun-0 |

...

Enter your choice: 1

选择 dsk0 分区以存放第一个交换区（swap1）。

| Partition | Size (GB) | Start Block | End Block | Overlaps |
|---|---|---|---|---|
| 1) b | 4.5GB | 1048576 | 10485760 | c |
| 2) e | 3.9GB | 10485760 | 18787864 | c |
| 3) f | 2.0GB | 18787864 | 22982168 | c |
| 4) h | 2.0GB | 31370776 | 35565080 | c |

Enter your choice: 1

由于我们选择不设置第二个交换分区，因此在提示时回答 "no"。

您可以选择设置第二个交换区（swap2）。  
Do you want a second swapping area [y/n] ? n

在本节中，我们会被提示是否要将 /var 与 /usr 分开。在我们的例子中，我们通常会将 /usr 和 /var 保持为单独的文件系统。按照传统，我们将 /var 放在 "h" 分区上。/var 文件系统也使用 AdvFS 文件系统。

您可以使 /var 成为单独的文件系统，也可以让它与 /usr 文件系统共享空间。

Should /var be a separate file system (y/n) ? y

选择 /var 文件系统所在的磁盘，或输入 "ping <disk>" 其中 <disk> 是设备名称（例如 dsk0）以物理识别特定磁盘。

| Device Name | Size (GB) | Controller Type | Disk Model | Location |
|---|---|---|---|---|
| 1) dsk0 | 18.2 | SCSI | BD018635C4 | bus-5-targ-0-lun-0 |

...

Enter your choice: 1

选择 dsk0 分区以存放 /var 文件系统。

| Partition | Size (GB) | Start Block | End Block | Overlaps |
|---|---|---|---|---|
| 1) e | 3.9GB | 10485760 | 18787864 | c |
| 2) f | 2.0GB | 18787864 | 22982168 | c |
| 3) h | 2.0GB | 31370776 | 35565080 | c |

Enter your choice: 3

