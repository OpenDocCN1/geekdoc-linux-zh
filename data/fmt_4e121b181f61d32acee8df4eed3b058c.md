
`mount -t ntfs-3g /dev/sdb1 /mnt`

挂载 FAT32 分区，使用：

```
mount -t vfat /dev/sdb1 /mnt
```

卸载 Windows 文件系统，使用 `umount` 命令：

```
umount /mnt
```

下面是使用特定选项挂载 NTFS 分区的示例：

```bash
mount -t ntfs-3g -o ro /dev/sdb1 /mnt
```

![](img/85ec3de0d5219d6ca14d5778e16a3338_361_0.png)

# 附录 D：成为专家：管理 Linux 文件系统 341

按钮指示文件系统是否已挂载或卸载。
几秒钟后，按钮将从“卸载”（Unmount）变为“挂载”（Mount），表示已卸载。

- 3. 点击退出按钮关闭该实用程序。

文件系统已挂载。如果该文件系统是可移除类型（如软盘或 CD），你可以将其移除。否则，在将其移除之前，该文件系统将无法直接使用。

![](img/85ec3de0d5219d6ca14d5778e16a3338_362_0.png)

你可以从 bash shell 运行 `eject` 命令来驱出 CD。你必须先卸载 CD，然后输入 `eject` 命令。否则，要弹出 CD，你必须先卸载它，然后按下 CD 驱动器上的弹出按钮。无论哪种情况，在卸载它之前，你都无法弹出 CD。

## 添加磁盘驱动器

早晚生活都会追上你的脚步，你可能需要或想要更大的房子、汽车或牙缝里的钻石，或者任何东西。磁盘空间也是如此，在这种情况下你想添加另一个磁盘驱动器。

增加驱动空间的第一步是添加一个新的存储设备。它可以是硬盘（IDE 或 SCSI），也可以是 USB 或 FireWire 内存棒。这些步骤描述了添加存储设备然后对其格式化并挂载的通用过程：

- 1. 安装硬盘或插入 USB 或 FireWire 设备。

如果设备是 IDE 或 SCSI 硬盘，请关闭电脑和显示器的电源。拔掉电源线并打开电脑机箱。（手伸电脑内部时，不要被尖锐的金属边缘割到）。使用硬盘附带的防电带；按照防电带的说明操作。

大多数 PC 使用 IDE 控制器。基于 SCSI 的 PC 价格较高，在消费领域并不常见；这些类型在商业领域更为常见。基于 IDE 的 PC 有两个 IDE 控制器。每个设备可以控制多两个 IDE 设备。排线连接控制器和设备。

![](img/85ec3de0d5219d6ca14d5778e16a3338_362_1.png)

如果你的新磁盘连接到已经连接了另一个设备（硬盘或 CD-ROM）的排线或 IDE 控制器，你必须配置新磁盘作为从设备设备工作。

如果设备是 USB 或 FireWire 内存棒，请跳到步骤 3。

- 2. 重启电脑并从 GNOME Terminal 窗口中运行 `dmesg` 命令。

如果你添加了 IDE 硬盘，请寻找对 `hdx` 设备的提及，其中 `x` 被替换为字母 `b`、`c`、`d` 或 `e`。此信息告诉你的内核在启动时“看到”了新硬盘：

```
hdb: HITACHI_DK227A-50, 4789MB w/512KB
Cache.CHS-610/255/63
```

如果你添加了 SCSI 硬盘，通用设备类型为 `sdx`。

- 3. 为新磁盘分区。

对于 IDE 硬盘，运行 `fdisk /dev/hdb` 命令。

对于 USB 或 FireWire 内存棒，使用命令 `fdisk /dev/sda`。内存棒显示为 SCSI 设备，例如根据你的电脑配置显示为 `/dev/sda`、`/dev/sdb` 或 `/dev/sdc`。

你可以在 `www.redhat.com/docs/manuals/linux/RHL-9-Manual/install-guide/` 找到更多关于 `fdisk` 的信息。

- 4. 在新分区上创建文件系统（根据情况更改设备名称）。

当你使用 IDE 或 SCSI 硬盘时，输入此命令：

```
mkfs /dev/hdb
```

对于 USB 内存棒，输入此命令：

```
mkfs /dev/sdc
```

- 5. 创建一个新的用于挂载新设备的目录：

```
mkdir /space
```

- 6. 使用适当的命令挂载新格式化的驱动器：

```
mount /dev/hdb /space
```

或者

```
mount /dev/sdc /space
```
