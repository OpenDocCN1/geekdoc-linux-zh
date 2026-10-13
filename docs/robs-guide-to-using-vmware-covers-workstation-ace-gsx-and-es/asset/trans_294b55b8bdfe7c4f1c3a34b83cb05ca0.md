
## Linux 配置

```
vmware-mount.pl [option] <disk> <partition> <mount point>
```

表 7.3：Linux 上 vmware-mount.pl 脚本的可用选项。

| 选项 | 描述 |
|---|---|
| -p | 打印分区表。 |
| disk | 虚拟硬盘文件名称。 |
| partition | 要挂载的分区号。 |
| mount point | 分区将被挂载的目录。 |
| -t type | 分区类型。 |
| -o options | 分区挂载选项。 |

图 7.6 显示了在 Linux 主机上挂载的虚拟磁盘文件的示例。当分区被挂载时，可以使用另一个终端窗口或文件管理器访问挂载点中的文件。当您完成访问虚拟磁盘后，按 Ctrl-C。脚本随后将卸载分区。

![](img/25fe75b93b97a021effaba85db112a52_120_0.png)

图 7.6：挂载虚拟磁盘文件功能现也适用于 Linux。

提示：当您无法卸载磁盘并且出现以下其中一条消息时，磁盘可能仍在使用中。

```
Unable to unmount the Network Block Device on the /mnt/vm mount point. Please make sure that no process uses /mnt/vm as its current directory or is accessing a file under this directory.
```

## DiskMount 限制

使用 VMware Disk Mount Utility 时需要注意以下几点限制：

- 仅当它们使用 FAT (32) 或 NTFS 文件系统格式化时，您才能在 Windows 主机上挂载虚拟磁盘中的卷。
- 如果您挂载具有快照的虚拟磁盘，所有更改在您恢复到快照时将被删除。
- 如果 .vmdk 文件被压缩或标记为只读，则无法挂载虚拟磁盘。
- 如果虚拟磁盘正被正在运行的虚拟机或来自已挂起的虚拟机使用，则无法使用它。

⚠️ 注意：如果您尝试使用 DiskMount Utility 访问已在虚拟机中运行的虚拟磁盘，您将收到类似以下的消息：

```
Unable to mount the virtual disk. The disk
may be in use by a virtual machine or
mounted under another drive letter. If
not, verify that the disk is a virtual
disk file, and that the disk file has not
been corrupted.
```

实际上，如果您使用 .vmx 文件中的参数 disk.locking = "false" 启动虚拟机，您可以访问正在使用的磁盘。然而，这比使用 VMware Dismount Utility 本身的支持程度还要低 ☺。

💡 提示：日本的 Ken Kato 提供了一个实用程序，也可以挂载虚拟硬盘文件。当然它不受支持，但关注他的项目可能会很有趣：chitchat.at.infoseek.co.jp/vmware。

## 7.5 使用原始磁盘分区

虚拟磁盘文件因多种原因非常方便。您可以在主机文件系统上拥有任意数量的它们，并且可以将它们从一台机器复制到另一台机器，等等。那么，为什么使用原始磁盘分区呢？首先让我们看看它是什么。

硬盘至少包含一个分区。操作系统格式化分区后，所有数据都存储在那里。您也可以拥有多个分区。创建多个分区的原因有：分隔数据与操作系统、创建双启动系统，或任何数据不应存储在同一分区中的其他原因。例如，可以压缩或加密一个分区，而让另一个分区不受这些处理的影响。虚拟机可以访问物理硬盘上的分区。这意味着对物理磁盘的所有数据访问都是直接写入和读取的。这不像虚拟磁盘那样将所有内容存储在一个文件中。

可以从添加硬件向导向虚拟机添加分区。

- 1. 通过设置控制面板打开虚拟机配置实用程序，并单击添加按钮以打开向导。您必须做的第一个选择是磁盘类型。选择使用物理磁盘（高级用户）以将现有分区添加到虚拟机。
- 2. 在下一个屏幕中，选择分区所在的物理磁盘，并选择您想要使用整个磁盘还是单独分区。选择使用单独分区将打开下一个屏幕，其中列出分区。
- 3. 在图 7.7 中，从 Linux 安装中选择了两个分区，该安装也在该计算机上作为双启动配置可用。

![](img/25fe75b93b97a021effaba85db112a52_122_0.png)

图 7.7：可以将单独的分区分配给虚拟机。

- 4. 单击下一步进入此配置的最后一步。为此物理磁盘创建的控制文件提供一个名称。

## 7.6 更改 SCSI 总线适配器类型

VMware Workstation 支持两种类型的 SCSI 适配器：LSI Logic 和 Buslogic。一旦您为其中一种适配器配置了机器，所有后续磁盘都将为此类型的适配器创建。

在 VMware Workstation 和 VMware GSX Server 中，SCSI 总线类型可以在虚拟机的 .VMX 配置文件中更改。如果机器配置了 SCSI 适配器，则文件内部可以找到以下其中一行：

```
scsi0.virtualDev = "lsilogic"
```

或

```
scsi0.virtualDev = "buslogic"
```

当您将虚拟机的总线类型从 LSI Logic 更改为 Buslogic 或反之时，虚拟磁盘文件也必须进行修改。VMware Workstation 和 VMware GSX Server 都会自动检测此类更改。如图 7.8 所示，它会询问您是否要更改虚拟磁盘的磁盘类型。

![](img/25fe75b93b97a021effaba85db112a52_123_0.png)

图 7.8：当适配器类型更改时，VMware Workstation 和 VMware GSX Server 可以自动更新虚拟磁盘。

## 7.7 使用 CD-ROM 和 DVD 映像文件

你是否有时感觉自己像个“唱片骑师”？或者，你是否随身携带一个装有所有可能 someday 在某个客户现场需要的 CD 和 DVD 的活页夹？你是否担心在需要时没有随身携带那张 Windows NT Workstation 4 可启动 CD？

那么请考虑使用 CD-ROM ISO 文件。它们不仅可以直接与虚拟机一起使用，还可以在需要时刻录到 CD 上。一个装在小型 USB 2 外壳中的 60 GB 外部笔记本硬盘大约花费你 200 美元。它可以容纳大约 50 到 80 个操作系统 CD-ROM 或 DVD ISO 文件，具体取决于操作系统和文件大小。

许多操作系统制造商通过互联网提供其操作系统 CD-ROM 的下载，有时带有集成服务包。这些所谓的覆盖 CD 将使安装新机器变得更加简单，因为它们包含了服务包。这样做是为了您不必在安装后立即更新服务器。

您也可以为归档或用于 VMware 创建自己的 ISO 文件。最简单的方法是直接从原始 CD-ROM 或 DVD 创建 ISO 文件。这可以使用任何流行的 CD/DVD 软件（如 Nero 和 EasyCD Creator）或互联网上可用的许多 ISO 实用程序来完成。此软件类别还允许您为虚拟机创建自己的 ISO 文件。

请查看以下用于 ISO 实用程序的网站：

- IsoBuster www.isobuster.com
- WinISO www.winiso.com
- Turtleblast ISO Commander www.turtleblast.com
- Undisker www.undisker.com
- Alex Feinman ISO Recorder isorecorder.alexfeinman.com
- Daemon Tools www.daemon-tools.cc

## 7.8 我的虚拟机无法从 CD-ROM 启动

安装操作系统后，当您的虚拟机使用空硬盘启动时，您可能会遇到此错误消息：未检测到可启动 CD。软盘或硬盘已被检测到。

如果您确实分配了用于安装的操作 CD-ROM，请检查虚拟机的 BIOS。很可能您的 CD-ROM 在启动顺序中未列在硬盘驱动器之前。在启动虚拟机时按 F2 进入设置。在 BIOS 中，进入启动菜单选项，并使用 + 和 – 键更改 CD-ROM 设备的启动顺序。

![](img/25fe75b93b97a021effaba85db112a52_125_0.png)

图 7.9：将 CD-ROM 驱动器在 BIOS 中设置为第一个启动设备。

![](img/25fe75b93b97a021effaba85db112a52_125_1.png)

另一种方法是在启动序列期间按 Escape 键进入启动菜单。这会打开一个一次性菜单，您可以在其中选择要从中启动的设备。

图 7.10：通过按 Esc 在系统启动时选择 CD-ROM 作为启动设备。
