
## 磁盘工具中的信息

左侧显示了系统当前检测到的所有可用存储设备。

在左侧窗格中选择任何一个设备，会在右侧窗格中显示设备属性信息。

这些信息包含了设备的存储容量以及访问该数据所需的 Linux 设备节点。一旦选择了某个设备，点击“分区”（Partitions）选项卡，将显示该设备当前分区情况的摘要，如图 23.17 所示。

**磁盘工具中的信息**

![](img/e88880e40d650bfe19d5b6927bd86568_723_0.png)
![](img/e88880e40d650bfe19d5b6927bd86568_723_1.png)

要查看特定分区的信息，请从右侧窗格列表中选择其名称。例如，图 23.17 显示了分区 `/dev/sda2` 的信息，识别出其当前处于未格式化状态。要格式化选定的分区，点击“格式化”（Format）。将显示类似于图 23.18 所示对话框。

**在磁盘工具中格式化分区**

图 23.18 中所示的对话框允许您指定关于分区的几种不同类型的信息：

- **格式化类型（Format Type）：** 您想在所选分区上创建的文件系统类型。可选 Extended 2、Extended 3、JFS、Memory Swap、ReiserFS、Windows Virtual FAT 和 XFS。
- **访问路径（Access Path）：** 格式化后的分区在系统上的挂载点。此信息在格式化分区时存储，但除非您点击图 23.17 所示对话框中的“启用”（Enable），否则实际上不会生效。

在进行格式化时，点击图 23.18 所示对话框中的“格式化”（Format）。如果您确定要格式化该分区，将显示此警告。点击“是”（Yes）继续，或点击“否”（No）取消。

当您完成对系统存储设备的检查或格式化后，点击对话框 23.16 或 23.17 中的“确定”（OK）以退出磁盘工具。

## 识别驱动器和分区的命令行工具

`fdisk` provides an easy way to examine all of the disk partitions and associated filesystems that are mounted and in use on your system. Unfortunately, commands such as `df` don’t provide information about devices that are newly attached to your system (and therefore may not contain partitions) or devices that are attached to your system but whose filesystems are not mounted. Luckily, Linux provides easy ways of finding all of the storage devices on your system, regardless of whether they’re formatted, mounted, or not. You’ll have to put up with a small bit of cryptic command-line magic, but you’re already at least an apprentice Linux wizard, right? You just put a new drive in your system!

A way to determine the device nodes associated with the storage devices in your system is to look at kernel boot messages for patterns that match the strings discussed earlier in this chapter in the section titled “Troubleshooting Automatic Device Detection.” That section suggested looking through the `dmesg` files for messages associated with hotplug events, which are the device detection and removal processes processed by the kernel when a system is running. Luckily, you can also look through the information of this message log using a command called `dmesg`. Because you know that IDE devices have names that begin with `hd` and are followed by some other letter, and that SATA and SCSI devices have names that begin with `sd` and are followed by some other letter, you can use a pattern such as `[hs]d[a-z]:`.

![](img/e88880e40d650bfe19d5b6927bd86568_724_0.png)

If you don’t speak Linux regular expressions fluently, the `[hs]d[a-z]:` means, “match any sequence of characters that begins with an ‘h’ or an ‘s’, followed by any single letter ‘d’, followed by any character between ‘a’ and ‘z’ (inclusive), followed by a colon, followed by space.” That was easy, wasn’t it?

Searching for this string in the output of the `dmesg` command on a sample Ubuntu system is exactly what you’d hope for, as the following example shows:

```
dmesg | grep '[hs]d[a-z]:'
[846.564436] SCSI device sda: 234441648 512-byte hdwr sectors (120034)
[846.564453] SCSI device sda: drive cache: write back
[846.564514] SCSI device sda: 234441648 512-byte hdwr sectors (120034)
[846.564526] SCSI device sda: drive cache: write back
[846.564531] sda: sda1 sda2
[846.575071] SCSI device sdb: 156299375 512-byte hdwr sectors (80025)
[846.575086] SCSI device sdb: drive cache: write back
[846.578550] SCSI device sdb: 156299375 512-byte hdwr sectors (80025)
```
