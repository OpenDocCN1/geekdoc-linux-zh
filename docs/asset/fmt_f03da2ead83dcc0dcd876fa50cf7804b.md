
当新驱动器插入镜像时，将开始重新同步。这个将镜像数据复制到新驱动器的过程可能需要一段时间。在复制期间，镜像的性能将大幅降低，因此最好在计算机需求较低时插入新驱动器。

可以使用 `gmirror status` 监控进度，它显示正在同步的驱动器和完成百分比。在重新同步期间，状态将为 `DEGRADED`，在过程完成后将变为 `COMPLETE`。

# RAID3 - 带有专用校验的字节级条带

由 Mark Gladman 和 Daniel Gerzo 编写。

基于 Tom Rhodes 和 Murray Stokely 的文档。

RAID3 是一种用于将多个磁盘驱动器组合为具有专用校验磁盘的单一卷的方法。在 RAID3 系统中，数据被分成若干字节，并写入数组中的所有驱动器，但一个作为专用校验磁盘的磁盘除外。这意味着来自 RAID3 实现的磁盘读取将访问数组中的所有磁盘。通过使用多个磁盘控制器可以增强性能。RAID3 数组提供了 1 块驱动器的容错能力，同时提供驱动器总容量的 1 - 1/n 倍，其中 n 是数组中驱动器的数量。

注意：由于 RAID3 的性质，这种适用于 3, 5, 9 等。

## 19.4. RAID3 - 带有专用校验的字节级条带

### 19.4.1. 创建专用数组

在 FreeBSD 中，RAID3 是用于将多个磁盘驱动器组合到一个具有专用校验磁盘的单一卷的方法。在 RAID3 系统中，数据被分成若干字节，并写入数组中的所有驱动器，但一个作为专用校验磁盘的磁盘除外。这意味着来自 RAID3 实现的磁盘读取将访问数组中的所有磁盘。通过使用多个磁盘控制器可以增强性能。RAID3 数组提供了 1 块驱动器的容错能力，同时提供驱动器总容量的 1 - 1/n 倍，其中 n 是数组中驱动器的数量。

在 FreeBSD 中，RAID3 是通过 `raid3(8)` 类实现的。创建一个专用数组需要以下步骤。

- 首先，通过以下命令加载 `geom_raid3.ko` 模块：
```bash
# raid3
```
或：
```bash
# kldload raid3
```
- 确保存在合适的挂载点。创建一个作为挂载点的目录：
```bash
# mkdir multimedia
```
- 确定添加到数组的磁盘设备名称，并创建设备。此示例使用三个驱动器：`ada1` 和 `ada2` 用于数据，`ada3` 用于校验。
```bash
# raid3 label -v gr0 ada1 /ada2 /ada3
```
- 对新创建的 `gr0` 进行分区并在其上建立FS 系统：
```bash
# gpart create -s GPT /dev/gr0
```
```bash
# gpart add -t freebsd-ufs /dev/gr0
```
```bash
# newfs -j /dev/gr0p1
```

许多数字将扫描屏幕，一段时间后过程将完成。卷已创建并准备好挂载：
```bash
# mount /dev/gr0p1 /multimedia
```

RAID3 数组现在可以使用。跨越重启需要额外的配置。

- 在挂载数组之前必须加载 `geom_raid3.ko` 模块。为了在系统启动期间自动加载内核模块，在 `/boot/loader.conf` 中添加以下行：
```bash
geom_raid3_load="YES"
```
- 必须在 `/etc/fstab` 中添加以下卷信息，以便在系统启动期间自动挂载：
`/dev/gr0p1 /multimedia ufs rw 2 2`

## 19.5. 软件 RAID 设备

原始内容由 Warren Block 提供。

某些主板和扩展卡添加了一些简单的硬件（通常只是一个 ROM），允许计算机从 RAID 数组启动。启动后，对 RAID 数组的访问由在计算机主处理器上软件处理。这种“硬件辅助软件 RAID”提供了不依赖于任何操作系统的 RAID 数组，并且在加载操作系统之前即可运行。

根据使用的硬件，支持多种 RAID级别。完整列表请参见 `raid(8)`。

`graid(8)` 需要 `geom_raid.ko` 内核模块，从 FreeBSD 9.1 开始包含 GENERIC 内核中。如果需要，可以使用 `raid load` 手动加载。

### 19.5.1. 创建数组

软件 RAID 设备通常有一个菜单，可以在计算机启动时通过按特殊键进入。该菜单可以创建和删除 RAID 数组，`graid(8)` 也可以直接从命令行创建数组。

使用 `raid label` 用于创建新数组。此示例用的主板具有 Intel 软件 RAID 芯片组，因此指定了 Intel 元数据格式。新数组被标记为 `gm0`，它是一个镜像（RAID1），并使用驱动器 `ada0` 和 `ada1`。

注意

当驱动器转换为新数组时，磁盘上的某些空间将被覆盖。请先备份现有数据！

```bash
# raid label Intel gm0 RAID1 ada0 ada1
```

`GEOM_RAID`: Intel-a29ea104: Array Intel-a29ea104 已创建。

`GEOM_RAID`: Intel-a29ea104: Disk ada0 状态从 NONE 变为 ACTIVE。

多个卷

`GEOM_RAID`: Intel-a29ea104: Subdisk gm0:0-ada0 状态从 NONE 变为 ACTIVE。

`GEOM_RAID`: Intel-a29ea104: Disk ada1 状态从 NONE 变为 ACTIVE。

`GEOM_RAID`: Intel-a29ea104: Subdisk gm0:1-ada1 状态从 NONE 变为 ACTIVE。

`GEOM_RAID`: Intel-a29ea104: Array 已启动。

`GEOM_RAID`: Intel-a29ea104: Volume gm0 状态从 STARTING 变为 OPTIMAL。

Intel-a29ea104 已创建

`GEOM_RAID`: Intel-a29ea104: 为卷 gm0 创建了 provider raid/r0。

状态检查显示新镜像已准备就绪：
```bash
# raid status
```

| 名称 | 状态 | 组件 |
| :--- | :--- | :--- |
| raid/r0 | OPTIMAL | ada0 (ACTIVE (ACTIVE)) |
| | | ada1 (ACTIVE (ACTIVE)) |

数组设备出现在 `/dev/raid/` 中。该数组名为 `r0`。如果存在额外的数组，它们将是 `r1`、`r2` 等。某些这些设备上的 BIOS 菜单可以创建名称包含特殊字符的数组。为了避免这些特殊字符引起的问题，数组被赋予了简单的数字名称，如 `r0`。要显示实际标签（如上述示例中的 `gm0`），请使用 `sysctl(8)`：
```bash
# sysctl kern.geom.name_format=1
```

### 19.5.2. 多个卷

某些软件 RAID 设备支持在一个数组上创建多个卷。卷的工作类似于分区，允许将物理驱动器上的空间划分并以不同的方式使用。例如，Intel 软件 RAID 设备支持两个卷。此示例创建了一个 40 G 的镜像用于安全地存储操作系统，随后是一个 20 G 的 RAID0（条带）卷，用于快速临时存储：
```bash
# raid label -S 40G Intel gm0 RAID1 ada0 ada1
```
```bash
# raid add -S 20G gm0 RAID0
```

卷以额外的 `rX` 条目形式出现在 `/dev/raid/` 中。具有两个卷的数组将显示 `r0` 和 `r1`。关于不同软件 RAID 设备支持的卷数，请参阅 `raid(8)`。

### 19.5.3. 将单驱动驱动器转换为镜像

在某些特定条件下，可以在不重新格式化的情况下将现有的单驱动器转换为 `raid(8)` 数组。为了避免转换过程中丢失数据，现有驱动器必须满足以下最低要求：

- 驱动器必须使用 MBR 分区方案进行分区。GPT 或其他在磁盘末尾带有元数据的分区方案将被 `raid(8)` 元数据覆盖并损坏。
- 磁盘末尾必须有足够的未分区且未使用的空间来容纳 `raid(8)` 元数据。

这些元数据的大小不一，但最大的占用 64 M，因此建议至少有这么多可用空间。

如果驱动器满足这些要求，首先进行完整备份。然后使用该驱动器创建一个单驱动器镜像：
```bash
# raid label Intel gm0 RAID1 ada0 NONE
```
`raid(8)` 元数据已写入磁盘末尾的空闲空间。现在可以向镜像中插入第二个驱动器：
```bash
# raid insert raid/r0 ada1
```

来自原始驱动器的数据将立即开始复制到第二个驱动器。在复制完成之前，镜像将以降级状态运行。

### 19.5.4. 向数组中插入新驱动器

可以将驱动器插入数组中，以替换故障或缺失的驱动器。如果没有故障或缺失的驱动器，新驱动器将成为备用。例如，向正常的双驱动器镜像中插入新驱动器将产生带有一个备用驱动器的双驱动器镜像，而不是三驱动器镜像。

在示例镜像数组中，数据立即开始复制到新插入的驱动器中。新驱动器上的任何现有信息将被覆盖。
```bash
# raid insert raid/r0 ada1
```

`GEOM_RAID`: Intel-a29ea104: Disk ada1 状态从 NONE 变为 ACTIVE。

`GEOM_RAID`: Intel-a29ea104: Subdisk gm0:1-ada1 状态从 NONE 变为 NEW。

`GEOM_RAID`: Intel-a29ea104: Subdisk gm0:1-ada1 状态从 NEW 变为 REBUILD。

`GEOM_RAID`: Intel-a29ea104: Subdisk gm0:1-ada1 正在重建。

### 19.5.5. 从数组中移除驱动器

可以从数组中永久移除单个驱动器并擦除其元数据：
```bash
# raid remove raid/r0 ada1
```

`GEOM_RAID`: Intel-a29ea104: Disk ada1 状态从 ACTIVE 变为 OFFLINE。

`GEOM_RAID`: Intel-a29ea104: Subdisk gm0:1-ada1 状态从 ACTIVE 变为 NONE。

`GEOM_RAID`: Intel-a29ea104: Volume gm0 状态从 OPTIMAL 变为 DEGRADED。

### 19.5.6. 停止数组

可以在不移除驱动器元数据的情况下停止数组。数组将在启动时重新启动。
```bash
# raid stop raid/r0
```

### 19.5.7. 检查数组状态

可以随时检查数组状态。在驱动器添加到镜像后，数据将复制到原始驱动器：
```bash
# raid status
```

| 名称 | 状态 | 组件 |
| :--- | :--- | :--- |
| raid/r0 | DEGRADED | ada0 (ACTIVE (ACTIVE)) |
| | | ada1 (REBUILD) |

如果磁盘发生故障，某些类型的数组（如 RAID0）可能不会显示在状态中。要查看这些数组，请添加 `-ga`：
```bash
# raid status -ga
```

| 名称 | 状态 | 组件 |
| :--- | :--- | :--- |
| raid/r0 | BROKEN | ada0 (ACTIVE (ACTIVE)) |
| | | ada1 (ACTIVE)) |

### 19.5.8. 删除数组

通过删除所有数组来销毁数组。
```bash
# raid delete raid/r0
```

### 19.5.9. 删除意外数组

驱动器可能会意外包含 `raid(8)`，由于之前的使用。要移除意外的元数据：

1. 启动系统。在启动菜单上，选择 2 进入加载提示符。
2. 备份影响驱动器上的所有数据。
3. 作为变通方法，通过在 `/boot/loader.conf` 中添加 `kern.geom.raid.enable=0` 来禁用 `raid(8)` 检测。
```bash
OK set.geom.raid.enable=0
```

## 19.6. GEOM Gate 网络

GEOM 提供了一种通过使用 GEOM Gate 网络守护程序 `ggated` 远程访问磁盘、CD 和系统的简单机制。带有设备的系统运行服务器守护程序，处理来自 `ggate` 的客户端请求。设备不应包含任何敏感数据，因为客户端与服务器之间的连接没有加密。

类似于第 30.3 节讨论的 NFS（网络文件系统），`ggated` 使用 `exports.le` 进行配置，该文件指定哪些系统允许访问导出的资源以及它们获得什么级别的访问。例如，为了允许客户端 `192.168.1.5` 对 SCSI 磁盘的第四分区具有读写权限，请创建 `/etc/gg.exports` 并写入：
`192.168.1.5 RW /dev/da0s4d`

在导出设备之前，确保它当前未被挂载。然后启动 `ggated`：
```bash
# ggated
```

可以使用多个选项指定替代端口或更改 `exports.le` 的默认位置。详情请参阅 `ggated(8)`。

要在客户端机器上访问导出的设备，使用 `ggatec` 指定服务器的 IP 地址和导出的设备名称。如果成功，此命令将显示要挂载的 `ggate` 设备名称。将指定的设备挂载到空闲挂载点。此示例连接到 `/dev/da0s4d` 分区上的 `192.168.1.1`，然后将 `/dev/ggate0` 挂载到 `/mnt`：
```bash
# ggatec create -o rw 192.168.1.1 /dev/da0s4d
```
`ggate0`
```bash
# mount /dev/ggate0 /mnt
```

现在可以通过客户端上的 `/mnt` 访问服务器上的设备。有关关于 `ggatec` 的更多细节和一些用例示例，请参阅 `ggatec(8)`。

注意

如果设备当前已挂载在服务器或网络上的任何其他客户端上，则挂载将失败。如果需要访问网络资源，请使用 NFS。

当不再需要该设备时，使用 `unmount` 将其卸载，以便该资源供其他客户端使用。

## 19.7. 磁盘设备标记

在系统初始化期间，FreeBSD 内核会在发现设备时创建设备节点。这种探测设备的方法会引发一些问题。例如，如果通过 USB 添加了新的磁盘设备怎么办？新设备可能会被分配设备名 `da0`，而原始的 `da0` 移动到 `da1`。如果这些文件系统列在 `/etc/fstab` 中，这将导致挂载出现问题，并可能阻止系统启动。

一种解决方案是按顺序链接 SCSI 设备，这样添加到 SCSI 卡的新设备将获得未被使用的设备号。但是可能替换主 SCSI 磁盘的 USB 设备呢？这是因为 USB 设备通常在 SCSI 卡之前被探测。一种解决方案是在系统启动后再插入这些设备。另一种方法是仅使用单个 ATA 驱动器，并且永远不在 `/etc/fstab` 中列出 SCSI 设备。

更好的解决方案是使用 `glabel` 标记磁盘设备，并在 `/etc/fstab` 中使用标签。由于 `glabel` 将标签存储在给定提供者的最后一个扇区，因此标签在重启后将保持持久。通过使用此标签作为设备，无论通过哪个设备节点访问，文件系统都可以始终挂载。

注意

`gabel` 可以创建瞬态和永久标签。只有永久标签在重启后是一致的。有关标签之间差异的更多信息，请参阅 `glabel(8)`。

### 19.7.1. 标签类型与示例

永久标签可以是通用标签或文件系统标签。永久性文件系统标签可以使用 `tunefs(8)` 或 `newfs(8)` 创建。这些类型的标签创建在 `/dev` 的子目录下，并根据文件系统类型命名。例如，UFS2 文件系统标签将创建在 `/dev/ufs` 中。通用永久标签可以使用 `glabel label` 创建。这些标签不是特定于系统的，并将创建在 `/dev/label` 中。

临时标签在下次重启时会被销毁。这些标签创建在 `/dev/label` 中，适用于实验。可以使用 `glabel create` 创建临时标签。

要在不破坏任何数据的情况下为 UFS2 系统创建永久性 标签，请执行以下命令：
```bash
# tunefs -L home /dev/da3
```

现在 `/dev/ufs` 中应该存在一个标签，可以将其添加到 `/etc/fstab`：
`/dev/ufs/home /home ufs rw 2 2`

注意

在尝试运行 `tunefs` 时，系统不能处于挂载状态。

现在可以挂载系统了：
```bash
# mount /home
```

从现在起，只要在引导启动时通过 `/boot/loader.conf` 加载了 `geom_label.ko` 内核模块，或者存在 `GEOM_LABEL` 内核选项，设备节点的变化就不会对系统产生任何影响。

可以使用 `-L` 标签使用默认标签创建文件系统。更多信息请参阅 `newfs(8)`。

可以使用以下命令销毁标签：
```bash
# glabel destroy home
```

接面的示例展示了如何对启动磁盘的分区进行标记。

示例 19.1 对启动磁盘上的分区进行标记

通过对启动磁盘上的分区进行永久标记，即使磁盘移动到另一个控制器或传输到不同的系统，系统也能够继续启动。在本示例中，假设使用单个 ATA 磁盘，该磁盘目前被系统识别为 `ad0`。

假设使用了标准的 FreeBSD 分区方案，带有 `/var`、`/usr` 和 `/tmp` 以及一个交换分区。

重启系统，在 `loader(8)` 提示符处，按 4 进入单用户模式。输入以下命令：
```bash
# glabel label rootfs /dev/ad0s1a
```
`GEOM_LABEL`: 提供者 `/dev/ad0s1a` 的标签为 `label/rootfs`
```bash
# glabel label var /dev/ad0s1d
```
`GEOM_LABEL`: 提供者 `/dev/ad0s1d` 的标签为 `label/var`
```bash
# glabel label usr /dev/ad0s1f
```
`GEOM_LABEL`: 提供者 `/dev/ad0s1f` 的标签为 `label/usr`
