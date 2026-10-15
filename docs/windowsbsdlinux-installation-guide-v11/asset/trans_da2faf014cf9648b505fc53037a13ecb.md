

每个分配在硬盘上的空间（主分区、扩展分区或逻辑驱动器）都会被分配一个驱动器号。磁盘 1 可能包含一个扩展分区，而第二块硬盘可能包含主分区或扩展分区。扩展分区可包含一个或多个逻辑 MS-DOS 驱动器。

使用 Fdisk 工具对硬盘进行分区后，您可以使用 Format 工具使用文件系统格式化这些分区。文件系统 File Allocation Table（FAT）允许硬盘接收、存储和检索数据。Windows 95、Windows 98（SE）、Windows Millennium（ME）和 Windows 2000 支持 FAT16 和 FAT32 文件系统。当您在大于 512 兆字节（MB）的硬盘上运行 Fdisk 工具时，会提示您选择以下文件系统之一：FAT16 或 FAT32。FAT16 文件系统每个分配的空间或驱动器号的最大容量为 2 千兆字节（GB）。例如，如果您使用 FAT16 文件系统并且拥有一块 6 GB 的硬盘，您可以拥有三个驱动器号（C、D 和 E），每个分配的空间为 2 GB。至于 FAT32 文件系统，它支持最大为 2 太字节的驱动器，并且将文件存储在比 FAT16 文件系统更小的硬盘区域中。这导致硬盘上有更多的可用空间。请注意，FAT32 文件系统不支持小于 512 MB 的驱动器。当您运行 “fdisk” 和 “format” 命令时，会创建主引导记录（MBR）和文件分配表。MBR 和文件分配表存储必要的磁盘几何结构，允许硬盘接收、存储和检索数据。

请注意，我假设您拥有一台可以无故障运行的计算机系统，并且您可以使用可启动的 Microsoft Windows CD-ROM。如果您在从 CD-ROM 启动或使用启动磁盘时遇到问题，请咨询您的硬件制造商以获取 CD-ROM 设备驱动程序。对于分区主硬盘，您必须运行 fdisk 命令。首先将启动磁盘插入软盘驱动器，重新启动计算机，然后根据您的操作系统使用以下方法之一。

## For a Windows 95/98/ME Startup disk:
在命令提示符下，键入 fdisk，然后按 enter。如果您的硬盘大于 512 MB，您会收到以下消息：

> *Your computer has a disk larger than 512 MB. This version of Windows includes improved support for large disks, resulting in more efficient use of disk space on large drives, and allowing disks over 2 GB to be formatted as a single drive.*

如果您启用大磁盘支持并在此磁盘上创建任何新驱动器，您将**无法**使用其他操作系统访问新驱动器，包括某些版本的 Windows 95 和 Windows NT，以及更早版本的 Windows 和 MS-DOS。此外，未明确指定用于 FAT32 文件系统的磁盘实用程序将无法与此磁盘一起使用。如果您需要使用其他操作系统或旧的磁盘实用程序访问此磁盘，请勿启用大驱动器支持。

Do you wish to enable large disk support?

如果您想使用 FAT32 文件系统，请按 Y 然后按 enter。如果您想使用 FAT16 文件系统，请按 N，然后按 enter。按 enter 后，会显示以下 Fdisk Options 菜单：

- 1. Create DOS partition or Logical DOS Drive
- 2. Set active partition
- 3. Delete partition or Logical DOS Drive
- 4. Display partition information
- 5. Change current fixed disk drive

**请注意，只有在计算机中有两块物理硬盘时，选项 5 才可用。**

按 1 选择 Create DOS partition or Logical DOS Drive 菜单选项，然后按 enter。按 1 选择 Create Primary DOS Partition 菜单选项，然后按 enter。按 enter 后，您会收到以下消息：

Do you wish to use the maximum available size for primary DOS partition?

收到此消息后，根据您选择的文件系统使用以下方法之一。

### For a FAT32 File System:
如果您在步骤 2 中为 FAT32 文件系统按 Y，并且希望将硬盘上的所有空间分配给驱动器 C，请按 Y，然后按 enter。按 ESC，然后按 ESC 退出 Fdisk 工具并返回命令提示符。

### For a FAT16 File System:
如果您在步骤 2 中为 FAT16 文件系统按 N，您可以接受分区大小的默认 2 GB 大小，也可以自定义分区大小。

如果您想自定义硬盘上分区（驱动器号）的大小，请按 N，然后按 enter。会显示一个对话框，您可以在其中键入您希望主分区大小的 MB 或磁盘空间百分比。请注意，对于运行 Windows 98（SE）或 Windows ME 的计算机，Microsoft 建议您将主分区大小至少设为 500 MB。键入您想要创建的分区的大小，然后按 enter。按 ESC 返回 Options 菜单。要为硬盘上的额外空间分配驱动器号，请按 1，然后按 enter。按 2 选择 Create Extended DOS Partition 菜单选项，然后按 enter。您会收到一个对话框，显示扩展分区可用的最大空间。您可以调整分区大小或使用默认大小。请注意，默认最大空间是推荐的，但您可以将空间分配给多个驱动器号。键入您想要的空间量，按 enter，然后按 ESC。会显示 Create Logical DOS Drive(s) in the Extended DOS Partition 菜单。这是您可以使用该菜单将剩余硬盘空间分配给额外驱动器号的菜单。在 Enter logical drive size in Mbytes or percent of disk space (%) 框中键入您想要分配给下一个驱动器号的空间量，然后按 enter。之后，您必须激活计划从中启动的分区。这通常是驱动器 C。因此，按 2 选择 Set active partition 菜单选项，然后输入您想要设为活动状态的分区的编号。

创建分区后，您必须格式化分区以便访问和使用它们。如果您使用的是 Windows 95 启动磁盘，会显示命令提示符，您可以跳到步骤 2。如果您使用的是 Windows 98 第二版或 Windows ME 启动磁盘，请在显示 Windows 98 启动菜单时选择 Start computer without CD-ROM support 菜单选项。当显示命令提示符时，键入 "format c:"，然后按 enter。此命令格式化驱动器 C（或您的“活动”驱动器）。对于所有其他分区，键入 format drive:（其中 drive 是您想要格式化的分区的字母）。

