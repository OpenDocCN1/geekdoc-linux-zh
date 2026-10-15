
我将这个 CD 驱动器的挂载点分配为 `/cdrom`。如果我想用 `/media` 用于 CD 驱动器，我需要为 USB 驱动器准备不同的挂载点。`/etc/fstab` 中的可移动驱动器始终使用 `noauto` 选项，因此缺少 CD 不会影响启动。

### 修复 FAT 文件系统

（此处原文似乎存在重复或错误，已根据上下文维持翻译逻辑）。。。。。。。。。。。。。。。。。。。。。。。。。。

如果你需要创建旧版本的 FAT，请使用 `-F` 参数和 FAT 版本号。FreeBSD 支持三个版本的 FAT：FAT12、FAT16 和 FAT32。

```
### newfs_msdos -F 12 /dev/da451
```

是的，某些网络（开放式电信）的硬件老旧到只支持 FAT12。而且你损坏的服务器也够老旧了！

### 修复 FAT 文件系统

FreeBSD 处理 FAT 的性能相当不错，但并不是每个人都那么小心。如果你有一个 FAT 损坏的设备，`fsk_msdosfs(8)` 可能会修复它。

```
# fsk_msdosfs /dev/da451 ** /dev/da451 ** Phase 1 - Read and Compare FATs ** Phase 2 - Check Cluster Chains ** Phase 3 - Checking Directories ** Phase 4 - Checking for Lost Files 1, 2074816 (64838 clusters)
```

如果 `fsk_msdosfs(8)` 发现错误，你可以选择“修复”它。你最终会得到一个可用的文件系统，但并不一定能恢复你希望恢复的所有 FAT。对于任何文件系统，你恢复具有复杂损坏的 FAT 的能力取决于你对 FAT 的理解。

### MSDOS 和 /etc/fstab

列出 `/etc/fstab` 中的文件系统可以方便地挂载它们。在这里我列出了我的新 FAT 设备，挂载点为 `/media`。

```
/dev/da451 /media msdos rw,noauto 0 0
```

注意我使用了 `noauto` 挂载选项，这样系统就不会在启动时自动挂载它。我不希望我的系统因为我拔掉了 USB 闪盘而导致启动过程中挂起！

### 其他 MSDOS 提示

FreeBSD 的 `mount_msdosfs(8)` 包含了一些很少使用的功能，这些功能在处理旧版 FAT 文件系统时可能会有所帮助，例如管理 Windows 95 的长文件名。当你遇到 FAT 问题时请查看该页面。

虽然 FAT 文件系统不支持 UTF-8 字符集或其他区域设置，但你可以让 FreeBSD 映射 DOS 代码页和这些字符集。你必须加载内核模块 `msdosfs_iconv.ko` 并配置你的区域设置。使用 `-l` 标志设置区域设置，并使用 `-D` 指定 DOS 代码页，如 `mount_msdosfs(8)` 中讨论的那样。

如果你需要处理大量的 FAT 磁盘，请查看 `mtools` 软件包。它包含了几个灵活的工具，可以在不挂载的情况下操作 FAT 文件系统。

# CD：ISO 9660

ISO 9660 是为了支持 CD 而开发的。FreeBSD 支持读取和写入 CD 镜像，以及将镜像刻录到磁盘。大多数 CD 都采用 ISO 9660 格式化，FreeBSD 将其称为 `cd9660`。DVD 和 蓝光盘使用 UDF，将在下一节讨论。

普通 CD 是只读介质。你不能重写 CD。虽然存在可写 CD，但它们寿命很短，且大部分已被更健壮的 USB 闪盘取代，所以我们不再讨论它们。

然而，CD 的只写特性在某些环境中可能是一个优势。你可以确信，刻录到 CD 上的文件（用你那笨拙的“用键盘而不是笔”的手写字标记的）不会被篡改。CD 不会从感染的客户端计算机感染病毒。虽然你可以通过开关将某些 USB 闪盘切换到只读模式，但这留下了人为错误空间，可能会在不方便的时候将开关拨回来。

我们不会涵盖多次刻录光盘（multisession disks）。多次刻录盘允许你在读写光盘的末尾追加数据，而不是覆盖现有的文件系统。使用多次刻录 CD 在很大程度上取决于你的硬件。

创建 CD 分两部分：创建一个 ISO 9660 文件系统的镜像，以及将该镜像刻录到磁盘。我们将分别介绍每个。

## 多个 CD 驱动器

在拥有多个 CD 驱动器的系统中，确定哪个硬件部分对应哪个设备节点会让任何人感到沮丧。如果你有多个 `/dev/cd` 设备，识别哪个设备节点对应哪个驱动器的最简单方法是使用 `cdcontrol(1)`。

关闭所有 CD 托架。对于每个设备节点，运行 `cdcontrol eject` 命令。给设备节点加上 `-f` 标志，如下所示：

```
# cdcontrol -f cd1 eject
```

大搞定！与 `/dev/cd1` 关联的硬件托架打开了。

`cdcontrol(1)` 命令还有一个关闭功能，但并不是所有的 CD 驱动器都支持自动关闭。

我的示例假设你正在使用 CD 驱动器 `/dev/cd0`。

## 读取 CD

要挂载 CD，告诉 `mount(8)` 挂载文件系统 `cd9660`。

```
# mount -t cd9660 /dev/cd0 /media
```

ISO 9660 不需要分区表，但在少数情况下，你可能会发现光盘在刻录时带有分区表。如果你在挂载磁盘时遇到困难，请检查是否有分区表。

CD 驱动器也可以在 `/etc/fstab` 中永久条目。

```
/dev/cd0 /cdrom cd9660 rw,noauto 000
```

我将这个 CD 驱动器的挂载点分配为 `/cdrom`。如果我想用 `/media` 用于 CD 驱动器，我需要为 USB 驱动器准备不同的挂载点。`/etc/fstab` 中的可移动驱动器始终使用 `noauto` 选项，因此缺少 CD 不会影响启动。

### 修复 FAT 文件系统

（此处原文似乎存在重复或错误，已根据上下文维持翻译逻辑）。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。

如果你需要创建旧版本的 FAT，请使用 `-F` 参数和 FAT 版本号。FreeBSD 支持三个版本的 FAT：FAT12、FAT16 和 FAT32。

```
### newfs_msdos -F 12 /dev/da451
```

是的，某些网络（开放式电信）的硬件老旧到只支持 FAT12。而且你损坏的服务器也够老旧了！

### 修复 FAT 文件系统

（此处重复部分已跳过）。

FreeBSD 处理 FAT 的性能相当不错，但并不是每个人都那么小心。如果你有一个 FAT 损坏的设备，`fsk_msdosfs(8)` 可能会修复它。

```
# fsk_msdosfs /dev/da451 ** /dev/da451 ** Phase 1 - Read and Compare FATs ** Phase 2 - Check Cluster Chains ** Phase 3 - Checking Directories ** Phase 4 - Checking for Lost Files 1, 2074816 (64838 clusters)
```

如果 `fsk_msdosfs(8)` 发现错误，你可以选择“修复”它。你最终会得到一个可用的文件系统，但并不一定能恢复你希望恢复的所有 FAT。对于任何文件系统，你恢复具有复杂损坏的 FAT 的能力取决于你对 FAT 的理解。

### MSDOS 和 /etc/fstab

列出 `/etc/fstab` 中的文件系统可以方便地挂载它们。在这里我列出了我的新 FAT 设备，挂载点为 `/media`。

```
/dev/da451 /media msdos rw,noauto 0 0
```

注意我使用了 `noauto` 挂载选项，这样系统就不会在启动时自动挂载它。我不希望我的系统因为我拔掉了 USB 闪盘而导致启动过程中挂起！

### 其他 MSDOS 提示

FreeBSD 的 `mount_msdosfs(8)` 包含了一些很少使用的功能，这些功能在处理旧版 FAT 文件系统时可能会有所帮助，例如管理 Windows 95 的长文件名。当你遇到 FAT 问题时请查看该页面。

虽然 FAT 文件系统不支持 UTF-8 字符集或其他区域设置，但你可以让 FreeBSD 映射 DOS 代码页和这些字符集。你必须加载内核模块 `msdosfs_iconv.ko` 并配置你的区域设置。使用 `-l` 标志设置区域设置，并使用 `-D` 指定 DOS 代码页，如 `mount_msdosfs(8)` 中讨论的那样。

如果你需要处理大量的 FAT 磁盘，请查看 `mtools` 软件包。它包含了几个灵活的工具，可以在不挂载的情况下操作 FAT 文件系统。

# CD：ISO 9660
