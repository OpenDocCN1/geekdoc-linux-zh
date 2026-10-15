

2. 启动一个命令行控制台窗口并成为超级用户。

3. 在控制台窗口中，输入 pc-zmanager 并按 <Enter>。PC-BSD 磁盘管理器屏幕打开。

4. 单击 PCBSD 磁盘管理器窗口顶部的 Disks 选项卡。您新添加的磁盘的标识和列表应出现在磁盘窗格底部附近。

我们系统上新的外部 USB 硬盘的逻辑设备名称的标识显示为 da0 (38.29 GB)，Maxtor 6 E040L0，并且它被列为 Sliced（表示已分区）。它在磁盘管理器的磁盘窗格中也显示为已有一个分区，名为 da0s1。您的新磁盘可能有不同的标识，具体取决于系统上有多少磁盘。

5. 此步骤允许您销毁磁盘上的所有分区和分区表，并允许您在上面创建 GPT 分区表。右键单击已存在的任何分区并对所有分区做出 Destroy this slice 选择。当所有现有分区都被销毁后，右键单击 da0，并做出 Delete partition table 的选择。然后，右键单击 da0 并做出 Create GPT partition table 的选择。该磁盘的标识显示现在后面跟着 [GPT]。其上的任何内容现在都被擦除。它显示为 Available。

6. 右键单击新磁盘，并做出 Add a new slice 的选择。Add Partition 窗口出现在屏幕上。将分区类型更改为 freebsd-zfs，并在标记为 Create and initialize a new file system 的框中打上复选标记。我们系统上的新分区在磁盘管理器的磁盘窗格中显示为 da0p1。然后单击 OK。您现在可以通过使用窗口右上角的 destroy 按钮退出磁盘管理器。

您也可以从 Add Partition 窗口更改分区的大小，并向此驱动器添加多个分区。如果您愿意，可以这样做。对于我们此处的用途，我们只展示了如何创建占用整个磁盘的单个主分区。

7. 您现在可以使用 zpool create 和 zfs create 命令在此磁盘上创建 ZFS zpools 和 ZFS datasets。例如，要在其上创建一个名为 testing 的 ZFS zpool，输入：

#zpool create testing /dev/da0p1

8. 为了拥有您复制到新外部 USB 驱动器以及从其复制的文件，您可能需要使用 chown 和 chgrp 命令对 zpool create 命令挂载文件系统的目录执行操作。

9. 您刚刚在外部 USB 硬盘上创建了新的分区表和占用整个磁盘的 slice，并在其上使用 ZFS 文件系统。您也知道它在 /dev 中的逻辑设备名称，并且在您在此上创建 ZFS zpool 后知道其在系统上的挂载点。

10. 要分离 USB 外部硬盘并销毁其上的 zpool、分区和数据，请使用命令 zpool destroy testing 销毁其上的 zpool，并对它重复步骤 5。然后您可以安全地将 USB 外部硬盘从计算机中移除。

## EXERCISE 23.10

- 1. 使用 PC-BSD 中的 gpart 命令对主分区进行分区，格式化为 freebsd-zfs，并将新的内部 SATA 总线硬盘添加到您的系统。
- 2. 如果您尚未这样做，请使用示例 23.5 的 GUI 方法，将外部 USB 硬盘添加到您的 PC-BSD 系统。
- 3. 根据示例 23.5 的方法，要执行磁盘管理器 GUI 在添加外部 USB 硬盘时所做的事情，需要执行哪些 gpart 命令？为了按顺序测试这些命令，请仅使用 gpart 命令重新执行示例 23.5。The

代替信息步骤 7，使用以下命令在外部 USB 驱动器上创建一个 zpool：

```
zpool create test7 /dev/da0p1
```

USB 外部硬盘将挂载在 /test7。 这是您可以复制文件到 USB 外部硬盘以及从其复制文件的路径名。

## 23.5 ADDING A PRINTER TO THE SYSTEM

打印机是任何计算机系统的常见外设添加。

PC-BSD 使用 Common UNIX Printing System (CUPS) 来处理打印。PC-BSD 控制面板为添加和管理打印机提供了一个图形前端。您可以从其桌面图标启动 PC-BSD 控制面板，或作为超级用户在控制台或终端窗口中输入 pc-controlpanel 来启动。在控制面板中，打印机控制位于硬件组中，并命名为 Printing。

虽然控制面板图形实用程序易于使用，但它可能无法自动检测您的打印机，具体取决于您的打印机是否得到开源打印驱动程序的良好支持。您的打印机连同其驱动程序可能被快速轻松地找到，从而允许您轻松完成配置操作。如果您的打印机配置无法工作，请阅读以下部分以获取有关如何为您的打印机找到正确驱动程序的建议。

### 23.5.1 Researching Your Printer

在配置打印机之前，您必须查明是否存在适用于您特定型号的打印驱动程序，如果存在，推荐使用哪个驱动程序。如果您计划购买打印机，这绝对是事先了解的好信息。您可以在 Open Printing Database 中查找打印机的厂商和型号，该数据库位于 www.openprinting。

