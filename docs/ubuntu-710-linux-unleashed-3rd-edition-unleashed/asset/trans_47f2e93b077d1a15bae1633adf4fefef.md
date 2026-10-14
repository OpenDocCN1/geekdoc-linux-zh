

![](img/7aaa8e4f2209bf9f2fb443905096e94c_770_0.png)

FIGURE B.1 To boot to an install using your Ubuntu CD-ROM or DVD, set your BIOS to have your computer boot using its CD drive.

## 安装前和安装期间的分区

为 Linux 分区可以在安装前或安装期间进行。

如果您计划在安装 Linux 之前准备分区，您将需要使用商业分区软件。一些流行的商业软件工具可用于创建 Linux 分区是 Symantec 的 PartitionMagic 或 VCOM Products 的 Partition Commander。或者，也可以使用免费的 FIPS.EXE 命令在安装 Ubuntu 之前准备分区。

如果您想使用现有的 Linux 系统对硬盘进行分区，您可以将硬盘连接到备用 IDE 通道，然后使用 Linux fdisk 或 GNU parted 分区工具。两种工具都提供交互式分区和准备存储介质的方式。Linux 使用诸如 /dev/sda（IDE 通道 0 上的主设备）、/dev/sdb（IDE 通道 0 上的从设备）、/dev/sdc（IDE 通道 1 上的主设备）和 /dev/sdd（IDE 通道 1 上的从设备）之类的设备名称来识别 IDE 硬盘。对于使用 SATA 接口的更现代的计算机，Linux 将把驱动器称为 /dev/sda（通道 0 上的主设备）、/dev/sdb（通道 0 上的从设备），依此类推。

如果新硬盘正确连接到您的 PC，然后您启动 Linux，您可以通过查看 dmesg 命令的输出来查看内核是否识别该设备。然后您可以使用设备名称使用 fdisk 开始分区，如下所示：

```
$ sudo fdisk /dev/sdb
```

请注意，您需要 root 权限，在此示例中，新驱动器作为 IDE 通道 0 上的从设备连接。不要更改您的根设备的分区，否则您会搞坏系统！fdisk 命令是交互式的，您在使用该工具时可以按 M 获取帮助。如果您在命令行上指定 i 或交互选项，您也可以以类似的方式使用 parted，如下所示：

```
$ sudo parted -i /dev/sdb
```

在使用 parted 交互时，按 ? 或输入 help 后跟命令关键字以获取帮助。parted 命令具有其他有用的功能，例如能够直接从一个分区复制文件系统到另一个分区。

最后，您可以通过使用可启动的 Linux 发行版（例如 LNX Bootable Business Card，可在 http://www.lnx-bbc.org/ 获取）启动系统，然后使用 fdisk 等原生 Linux 工具对驱动器进行分区，从而在安装前准备分区。

### TIP

您可以使用第一张 Ubuntu CD 或 DVD 执行除安装 Linux 之外的其他任务。CD-ROM/DVD 具有救援模式，也可用于使用上述描述的 fdisk 对硬盘进行分区并为 Linux 做准备。

### NOTE

可以创建双启动配置，这允许选择启动 Ubuntu 和另一个操作系统，例如 Windows XP。要将系统配置为双启动，您必须先安装 Windows，然后安装 Linux。请注意，许多 Windows 系统还原 CD-ROM 会清除硬盘上的所有数据，包括 Linux。在安装 Ubuntu 期间，您会自动将 GRUB Linux 启动加载程序安装到主驱动器的主引导记录或 MBR 中。当配置正确时，GRUB 允许您的系统重新启动到 Windows 或 Linux。浏览至 http://www.gnu.org/software/grub/manual/ 以在线阅读 GRUB 手册。

### CAUTION

在开始分区驱动器之前，请做好安全保障。首先，备份所有关键数据！对系统硬盘或操作系统的任何更改都会使现有数据面临风险。为了防止数据丢失后不可避免的时间和资源损失，请在对系统进行任何更改之前进行完整备份。在安装过程中创建启动盘（在安装完成前会提示您），这样如果出现问题，您至少能够启动 Linux。

