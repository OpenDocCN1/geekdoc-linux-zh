
`live-build` 提供了可在构建过程的不同步骤中执行的钩子。Chroot 钩子是作为 `hooks/live/*.chroot` 文件安装在你的配置树中的可执行脚本，并在 chroot 内执行。虽然 chroot 是让你临时更改操作系统根目录到你选择的目录的命令，但它也被引申用来指代托管完整（替代）文件系统树的目录。在这里使用 live-build 时也是如此，chroot 目录是正在准备实时文件系统的目录。由于在 chroot 中启动的应用程序无法看到该目录之外的内容，因此对于 chroot 钩子也是如此：你只能使用和修改在该 chroot 环境中可用的任何内容。我们依赖这些钩子来执行多个 Kali 特定的自定义（参见 `kali-config/common/hooks/live/kali-hacks.chroot`）。

二进制钩子（`hooks/live/*.binary`）在过程的末尾执行，且在构建过程的上下文中（不在任何 chroot 中）。你可以修改构建的 ISO 镜像的内容，但不能修改实时文件系统，因为此时它已经生成完毕。我们在 Kali 中使用此功能来对 `live-build` 生成的默认 isolinux 配置进行一些更改。例如，参见 `kali-config/common/hooks/live/persistence.binary`，我们在其中添加了启用持久性的启动菜单项。

### 9.3.5. 在 ISO 镜像或实时文件系统中添加文件

另一个非常常见的自定义是在实时文件系统或 ISO 镜像中添加文件。

你可以通过将文件放在 `includes.chroot` 配置目录下的预期位置来向实时文件系统添加文件。例如，我们提供 `kali-config/common/includes.chroot/usr/lib/live/config/0031-root-password`，它最终成为实时文件系统中的 `/usr/lib/live/config/0031-root-password`。

**Live-Boot 钩子**

安装为 `/lib/live/config/XXXX-name` 的脚本由 live-boot 包的 init 脚本执行。它们重新配置系统的许多方面，使其适合实时系统。你可以添加自己的脚本来在运行时自定义你的实时系统：例如，这被用来实现自定义启动参数。

你可以通过将文件放在 `includes.binary` 配置目录下的预期位置来向 ISO 镜像添加文件。例如，我们提供 `kali-config/common/includes.binary/isolinux/splash.png` 以覆盖 Isolinux 引导加载程序使用的背景图像（该图像存储在 ISO 镜像文件系统的 `/isolinux/splash.png` 中）。

## 9.4. 使用 USB 键为 Live ISO 添加持久性

### 9.4.1. 持久性功能：解释

接下来，我们将讨论为 Kali USB 键添加持久性所需的步骤。实时系统的本质是短暂的。存储在实时系统上的所有数据以及所做的所有更改在重启时都会丢失。为了解决这个问题，你可以使用 `live-boot` 的一个称为持久性的功能，当启动参数包含 `persistence` 关键字时启用。

由于修改启动菜单是一项非平凡的任务，Kali 默认包含两个启用持久性的菜单项：Live USB Persistence（USB 持久性）和 Live USB Encrypted Persistence（加密 USB 持久性），如图 9.1“持久性菜单项”[第 240 页]所示。

![](img/46e3313ea1bb2892f3146304f0677b8_266_0.png)

*图 9.1 持久性菜单项*

当启用此功能时，*live-boot* 将扫描所有分区，寻找标记为 *persistence*（持久性）的文件系统（可以通过启动参数 *persistence-label=value* 覆盖该标签），并且安装程序将设置在该分区的 *persistence.conf* 文件中列出的目录（每行一个目录）的持久性。特殊值“/ union”启用所有目录的完全持久性，使用 *union mount*（联合挂载），这是一种仅存储与底层文件系统相比发生变化的覆盖层。持久目录的数据存储在与相应 *persistence.conf* 文件所在相同的文件系统中。

### 9.4.2. 在 USB 键上设置未加密持久性

在本节中，我们假设您已按照 2.1.4 节“将镜像复制到 DVD 或 USB 键”[第 19 页]的说明准备好了 Kali Live USB 键，并且您使用了足够大的 USB 键来容纳 ISO 镜像（大约 3 GB）以及您想要持久化的目录数据。我们还假设 Linux 识别该 USB 键为 `/dev/sdb`，并且它仅包含默认 ISO 镜像中的两个分区（`/dev/sdb1` 和 `/dev/sdb2`）。在执行此过程时请非常小心。如果您重新分区错误的磁盘，可能会轻易销毁重要数据。

要添加新分区，您需要知道所复制镜像的大小，以便使新分区在 live 镜像之后开始。然后使用 `parted` 实际创建该分区。以下命令分析了名为 `kali-linux-2016.1-amd64.iso` 的 ISO 镜像，假设该镜像也存在于 USB 键上：

```
#### parted /dev/sdb print
Model: SanDisk Cruzer Edge (scsi)
Disk /dev/sdb: 32,0GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start   End     Size    Type  File system  Flags
 1      32,8kB  2852MB  2852MB  primary        boot, hidden
 2      2852MB  2945MB  93,4MB  primary
#### start=$(du -b --block-size=1MB kali-linux-2016.1-amd64.iso | awk '{print $1}')
#### echo "Size of image is $start MB"
Size of image is 2946 MB
#### parted -a optimal /dev/sdb mkpart primary "${start}MB" 100%
Information: You may need to update /etc/fstab.
```

```
#### parted /dev/sdb print
Model: SanDisk Cruzer Edge (scsi)
Disk /dev/sdb: 32,0GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start   End     Size    Type  File system  Flags
 1      32,8kB  2852MB  2852MB  primary        boot, hidden
 2      2852MB  2945MB  93,4MB  primary
 3      2946MB  32,0GB  29,1GB  primary
```

在新的 `/dev/sdb3` 分区就位后，使用 `mkfs.ext4` 命令将其格式化为标记为 "persistence" 的 ext4 文件系统（并使用其 `-L` 选项设置标签）。然后该分区被挂载到 `/mnt` 目录，您添加所需的 `persistence.conf` 配置文件。一如既往，格式化任何磁盘时都要谨慎。如果格式化了错误的磁盘或分区，您可能会丢失宝贵信息。
