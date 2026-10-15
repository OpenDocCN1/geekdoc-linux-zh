
Purpose: `gpart` 实用程序用于对 GEOM 提供者，通常是磁盘，进行分区。
常用选项/功能：

- `gpart create -s GPT ada0` 在 `ada0` 上创建 GPT 方案。
- `gpart add -s 512M -t freebsd-zfs ada1` 创建一个 512 MB 的 freebsd-ufs 分区以包含一个 ZFS 文件系统，系统可以从中启动。
- `gpart add -s 15G -t freebsd-ufs -a 4k da0` 创建一个 15 GB 的 freebsd-ufs 分区以包含一个 ZFS 文件系统并在 4KB 边界上对齐。
- `gpart add -t freebsd-zfs -l zfs1 ada1` 在 `ada1` 上的所有空闲空间上创建 ZFS 分区。
- `gpart show` 显示系统上磁盘的状态。
- `gpart delete -i 1 da0` 删除 `da0` 上的分区 1。
- `gpart destroy -F da0` 删除 `da0` 上的分区表。

你可以使用 `gpart` 对添加到系统的新磁盘驱动器进行分区和格式化。有关其子命令、选项、选项参数和命令参数的更多描述，请参阅系统上 `gpart` 的手册页。

## Example 23.3: 在 Solaris 中添加新磁盘并使用 Gparted 对磁盘进行切片

- 1. 从应用程序菜单>系统工具中，选择 Gparted 分区编辑器。如果需要，在终端窗口中以超级用户身份输入 `gparted`。
- 2. Gparted 屏幕出现，如图 23.6 所示。

![](img/02e070097d401d3bf7de4bf1c470b267_1131_0.png)

FIGURE 23.6 Gparted 主屏幕显示。

3. 当前连接到系统的磁盘出现在右上角的菜单栏中。记下所有当前磁盘的完整路径。例如，启动或根磁盘可能被指定为 `/dev/dsk/c1t0d0p0`，如图 23.6 所示。

4. 如有必要，关闭系统电源，并添加新磁盘。重新启动系统。

5. 重新启动 Gparted。

6. 当 Gparted 屏幕重新出现时，你的新磁盘驱动器应该显示在 Gparted 屏幕右上角的菜单栏中。如果刚添加的磁盘驱动器没有出现在 Gparted 列表中，你就不能使用该磁盘驱动器。如果它出现了，请继续下一步。

7. 在该栏中滚动，直到到达你刚添加到系统的磁盘。

8. 在菜单栏中选择该新磁盘。它显示在主 Gparted 窗格中。单击主 Gparted 窗格中的该磁盘。现在你可以对该新磁盘进行分区和格式化。在我们的示例中它显示为 `/dev/dsk/c1t0d0p0`，是我们在步骤 4 插入的新磁盘。它上面有一个 FAT32 文件系统，大小为 29.95 GB。参见图 23.7。

9. 从 Gparted 窗口顶部的下拉菜单中，选择 Partition>Delete。这将删除该磁盘上的分区信息。它现在是一个待处理操作。

10. 为了执行待处理操作，选择下拉菜单 Edit>Apply All Operations。在警告窗口中，单击 Apply。会出现一个窗口，显示待处理操作的进度，以及 hopefully 成功应用。操作完成后在该窗口中单击 close。

11. 新磁盘现在应该未分配。单击主 Gparted 窗格中的其列表。选择下拉菜单 Device>Create Partition Table。在警告窗口中单击 Create。该磁盘上的所有内容将被擦除！当 Gparted 创建了新的分区表后，再次单击主 Gparted 窗格中的该磁盘。

12. 选择下拉菜单 Partition>New。屏幕上会出现创建新分区窗口，如图 23.8 所示。默认值

![](img/02e070097d401d3bf7de4bf1c470b267_1132_0.png)

FIGURE 23.8 Gparted 创建新分区窗口。

![](img/02e070097d401d3bf7de4bf1c470b267_1133_0.png)

FIGURE 23.9 显示已完成分区的 Gparted 主窗口。

![](img/02e070097d401d3bf7de4bf1c470b267_1133_1.png)

对于如图 23.8 所示的新分区，是用整个磁盘来创建此分区，将其创建为主要分区（ZFS 文件系统允许的唯一分区），并将文件系统设置为 ntfs。

- 13. 在 Label 字段中添加你选择的标签 designation。保持所有其他默认值不变。单击 Add 按钮。选择下拉菜单 Edit>Apply All Operations，并按照步骤 10 的方式跟进此选择。
- 14. 你现在有一个已分区并格式化的磁盘可在系统上使用，对我们的系统而言如图 23.9 所示。
- 15. 通过选择下拉菜单 Gparted>Quit 退出 Gparted。

## Example 23.4: 在 PC-BSD 中添加新磁盘并对其进行分区

以下说明假设你的系统开始时只有一个硬盘；在我们的系统上它列为 `ada0`。你应该部署第 23.4.2 节中所示的方法来找出新磁盘的逻辑名称。当你到达步骤 4 时，你可以通过它上面已经有一个名为 `tank` 的 `zpool` 来识别系统上的原始磁盘。`tank` `zpool` 是安装系统时创建的默认池，它包含启动切片、交换空间和操作系统。

这些说明适用于内部添加 SATA 硬盘。USB 外部硬盘在下一个示例中介绍。如果你在步骤 4 中添加的磁盘没有作为新磁盘出现在列表中，你就不能在没有为其获取设备驱动程序的情况下轻松地在系统上使用它。

在开始此示例之前，值得注意的是，你也可以在命令行上使用 `gpart` 命令来实现所示的相同操作。请参阅手册页

for `gpart` 在你的系统上查看命令选项和参数，以及如何分区和格式化磁盘的示例。`gpart` 确实允许格式化为 `freebsd-zfs`。此外，了解你要添加的磁盘的逻辑设备名称也很重要，这样你就可以将该逻辑设备名称作为 geom 参数提供给 `gpart` 命令。

- 1. 关闭系统电源，并添加新的磁盘驱动器。重新启动系统。
- 2. 从 KDE4 桌面左下角极端的 Kickoff 应用程序启动器菜单中，选择 Applications>Utilities>Root Terminal。提示时提供 root 密码。
- 3. 一个 root 终端窗口在你的屏幕上打开。在其中输入 `pc-zmanager`。PC-BSD 磁盘管理器屏幕打开，如图 23.10 所示。
- 4. 点击 PC-BSD 磁盘管理器窗口顶部的 Disks 选项卡。你的新添加磁盘的标识和列表应出现在磁盘窗格底部附近，类似于图 23.11。图中所显示的我们系统上新磁盘的标识显示为 `ada1 (931.51 GB) ST3100033AS`，并且被列为 Available (sic)。在我们的系统上，`cd0` 磁盘在安装时已存在，`ada0`（包含 `tank` 的切片的磁盘）也是如此。你的新磁盘可能有不同的标识，具体取决于系统上有多少磁盘。

![](img/02e070097d401d3bf7de4bf1c470b267_1134_0.png)

FIGURE 23.10 Disk Manager window.

![](img/02e070097d401d3bf7de4bf1c470b267_1134_1.png)

FIGURE 23.11 Disk Manager disks tab display.

- 5. 要在磁盘上创建切片（分区）表，右键单击它并选择 Create GPT Partition Table。该磁盘的标识显示现在后面跟着 `[GPT]`。其上的任何内容现在都被擦除。
- 6. 右键单击新磁盘，并选择 Add a new slice。Add Partition 窗口出现在屏幕上，如图 23.12 所示。仅将分区类型更改为 `freebsd-zfs`，然后点击 OK。
- 7. 你刚刚使用整个磁盘创建了一个新的分区表和切片，其上有一个名为 ZFS 的 FreeBSD 文件系统，并且知道其在 `/dev` 中的路径。该路径信息对于执行 `zpool` 创建至关重要。参见图 23.13。

当你执行 ZFS 文件系统维护操作时使用该路径，例如在这些池上创建 `zpools` 和文件系统，并将它们与虚拟设备（`vdevs`）关联。此新磁盘现在是系统上的一个 `vdev`。Vdevs 在第 24 章中有详细解释。

- 8. 你现在可以选择使用 ZFS Pools 选项卡或 ZFS File systems 选项卡以图形方式创建和操作 `zpools` 及其上的文件系统。你也可以在命令行键入 ZFS 命令来实现磁盘管理器中所有可用的功能，以及更多功能。两种功能都是互操作的，并设计为适合你最舒适的交互方式。

![](img/02e070097d401d3bf7de4bf1c470b267_1135_0.png)

FIGURE 23.12 Disk Manager add partition display.

![](img/02e070097d401d3bf7de4bf1c470b267_1135_1.png)

FIGURE 23.13 Disk Manager with added partition.

- 9. 准备就绪后，你可以通过点击窗口右上角的 destroy 按钮退出 PC-BSD 磁盘管理器，并且也可以退出你在步骤 2 中启动的 root 终端。

## Example 23.5: Adding an External USB Hard Drive and Partitioning It in PC-BSD

PC-BSD 系统常见的安装后添加是需要格式化和分区后才能在系统上挂载和使用的外部 USB 硬盘。

以下说明假设你系统上已经有一个内部挂载的硬盘作为起点；在我们的系统上它被列为 `ada0`。你应该部署第 23.4.2 节中所示的方法来找出你要添加的新磁盘的逻辑名称。USB 驱动器通常被指定为 `daXpY`，其中 X 是从 0 开始的数字，Y 是从 1 开始的数字。

说明适用于添加外部 USB 硬盘、SATA 或 IDE，通常安装在带电外壳中。它们还显示了如何将该驱动器从系统分离。第一步之后，它们还假设它以与 PC-BSD 系统不兼容的方式进行分区和格式化。如果你要添加的磁盘未作为新磁盘出现在 `/dev` 列表中，你在没有获得其设备驱动程序的情况下就无法轻松地在系统上使用它。

此外，从 KDE4 Kickoff 应用程序启动器，你可以做出 System Settings 菜单选择来影响 USB 可移动媒体的自动挂载过程。System Settings 图标之一是 Removable Devices。当你点击此图标时，你可以打开或关闭自动挂载，并为可移动媒体配置其他设置。默认情况下，自动挂载是关闭的。Mount Tray，一个 KDE4 桌面图标，作为项目 F 显示在 Panel 中，如表 22.4 所示，并在第 22 章图 22.12 “KDE4 Panel components”中说明。它允许对你添加到系统或从系统移除的可移动媒体进行简单、基于 GUI 的管理。

- 1. 打开外部硬盘外壳电源，并将外壳的 USB 电缆连接到计算机上的 USB 端口。此时你可以使用第 23.5.2 节中所示的方法确定新添加的外部 USB 驱动器的逻辑设备名称。但我们将在以下步骤中使用磁盘管理器来演示如何执行此操作。

2. 启动一个命令行控制台窗口并成为超级用户。

3. 在控制台窗口中，输入 `pc-zmanager` 并按 `<Enter>`。PC-BSD 磁盘管理器屏幕打开。

4. 单击 PCBSD 磁盘管理器窗口顶部的 Disks 选项卡。您新添加的磁盘的标识和列表应出现在磁盘窗格底部附近。

我们系统上新的外部 USB 硬盘的逻辑设备名称的标识显示为 `da0 (38.29 GB)`，`Maxtor 6 E040L0`，并且它被列为 Sliced（表示已分区）。它在磁盘管理器的磁盘窗格中也显示为已有一个分区，名为 `da0s1`。您的新磁盘可能有不同的标识，具体取决于系统上有多少磁盘。

5. 此步骤允许您销毁磁盘上的所有分区和分区表，并允许您在上面创建 GPT 分区表。右键单击已存在的任何分区并对所有分区做出 Destroy this slice 选择。当所有现有分区都被销毁后，右键单击 `da0`，并做出 Delete partition table 的选择。然后，右键单击 `da0` 并做出 Create GPT partition table 的选择。该磁盘的标识显示现在后面跟着 `[GPT]`。其上的任何内容现在都被擦除。它显示为 Available。

6. 右键单击新磁盘，并做出 Add a new slice 的选择。Add Partition 窗口出现在屏幕上。将分区类型更改为 `freebsd-zfs`，并在标记为 Create and initialize a new file system 的框中打上复选标记。我们系统上的新分区在磁盘管理器的磁盘窗格中显示为 `da0p1`。然后单击 OK。您现在可以通过使用窗口右上角的 destroy 按钮退出磁盘管理器。

您也可以从 Add Partition 窗口更改分区的大小，并向此驱动器添加多个分区。如果您愿意，可以这样做。对于我们此处的用途，我们只展示了如何创建占用整个磁盘的单个主分区。

7. 您现在可以使用 `zpool create` 和 `zfs create` 命令在此磁盘上创建 ZFS `zpools` 和 ZFS datasets。例如，要在其上创建一个名为 `testing` 的 ZFS `zpool`，输入：

```
#zpool create testing /dev/da0p1
```

8. 为了拥有您复制到新外部 USB 驱动器以及从其复制的文件，您可能需要使用 `chown` 和 `chgrp` 命令对 `zpool create` 命令挂载文件系统的目录执行操作。

9. 您刚刚在外部 USB 硬盘上创建了新的分区表和占用整个磁盘的 slice，并在其上使用 ZFS 文件系统。您也知道它在 `/dev` 中的逻辑设备名称，并且在您在此上创建 ZFS `zpool` 后知道其在系统上的挂载点。

10. 要分离 USB 外部硬盘并销毁其上的 `zpool`、分区和数据，请使用命令 `zpool destroy testing` 销毁其上的 `zpool`，并对它重复步骤 5。然后您可以安全地将 USB 外部硬盘从计算机中移除。

## EXERCISE 23.10

- 1. 使用 PC-BSD 中的 `gpart` 命令对主分区进行分区，格式化为 `freebsd-zfs`，并将新的内部 SATA 总线硬盘添加到您的系统。
- 2. 如果您尚未这样做，请使用示例 23.5 的 GUI 方法，将外部 USB 硬盘添加到您的 PC-BSD 系统。
- 3. 根据示例 23.5 的方法，要执行磁盘管理器 GUI 在添加外部 USB 硬盘时所做的事情，需要执行哪些 `gpart` 命令？为了按顺序测试这些命令，请仅使用 `gpart` 命令重新执行示例 23.5。The

代替信息步骤 7，使用以下命令在外部 USB 驱动器上创建一个 `zpool`：

```
```
