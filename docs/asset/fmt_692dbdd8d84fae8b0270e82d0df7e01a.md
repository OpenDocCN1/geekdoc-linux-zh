
如果您在安装期间未创建 RAID 磁盘，而是在之后创建并且想要从中启动，您将必须确保您的系统配置正确。RAID 设备需要使用持久超级块创建。内核中必须启用对 RAID 设备的支持。在 Red Hat 上，此支持作为模块启用。困难出现在您对 `/`（根）分区使用 RAID 5 时。此分区包含 RAID 5 模块，但要访问该分区，您必须先加载 RAID 5 模块。为了解决此限制，您可以在 `/boot` 分区中创建一个包含 RAID 5 模块的 RAM 磁盘。使用 `mkinitrd` 命令创建 RAM 磁盘并使用 `--with` 选项指定要包含的模块。

```
mkinitrd --preload raid5 --with=raid5 raid-ramdisk 2.4.20-8
```

## Automatic Detection: Persistent Superblocks

Linux 软件 RAID 现在支持 RAID 设备的自动检测。这允许您的 RAID 设备在系统每次启动时自动被检测到，就像标准分区一样。然后您可以使用任何 RAID 设备 `md` 就像使用硬盘分区 `hd` 或 `sd` 一样，在 `/etc/fstab` 文件中使用它们（参见第 30 章）。自动检测是通过在每个 RAID 磁盘上放置的持久超级块来实现的，以保存配置信息。持久超级块需要在您使用 `mkraid` 创建 RAID 设备时创建。要指示 `mkraid` 创建持久超级块，您需要在 `/etc/raidtab` 文件中指定 `persistent-superblock` 选项，这是 RAID 配置文件。如果没有持久超级块选项，您将必须使用 `raidstart` 命令手动启动您的 RAID 设备。`raidstart -a` 启动所有您的设备。

## RAID Tools

RAID 工具对于在 Linux 上管理软件 RAID 设备很有用。`mkraid` 创建 RAID 设备，`raidstop` 停止设备，而 `raidstart` 打开它（参见表 31-2）。这些将在下一节中详细讨论。

## Creating and Installing RAID Devices

如果您在安装过程中创建了 RAID 设备及其分区，您应该已经拥有可工作的 RAID 设备。您的 RAID 设备将配置在 `/etc/raidtab` 文件中，并且您的 RAID 设备的状态将列在 `/proc/mdstat` 文件中。您可以使用 `raidstart` 和 `raidstop` 命令手动启动或停止您的 RAID 设备。`-a` 选项对它们全部操作，不过您也可以指定特定设备如果您想要。

要为已安装的系统手动创建一个新的 RAID 设备，请按照以下步骤操作：

- 1. 确保您的内核支持您要为正在创建的设备使用的 RAID 级别。要在内核中启用对 RAID 级别的支持，请使用内核配置工具为其创建一个模块，如前所述。
- 2. 如果您尚未这样做，请创建您将用于 RAID 设备的 RAID 磁盘（分区）。
- 3. 在 `/etc/raidtab` 文件中配置您的 RAID 设备（`/dev/md n`），指定要使用的 RAID 磁盘。务必指定持久超级块选项以便在启动时自动检测您的 RAID 设备。
- 4. 使用 `mkraid` 创建您的 RAID 设备。
- 5. 使用 `raidstart` 激活 RAID 设备。
- 6. 在 RAID 设备上创建文件系统（`mkfs`）然后挂载它。

### TABLE 31-2

RAID Tools

| Tool | Description |
|------|-------------|
| `mkraid` | 从一组块设备创建（配置）RAID 设备，并对其进行初始化。 |
| `raidstart` | 激活 RAID 设备。 |
| `raid0start` | 激活旧的非持久线性 RAID 和 RAID 0 RAID 设备。 |
| `raidstop` | 关闭一个 RAID 设备。 |

## 创建硬盘分区：fd

要添加新的 RAID 设备或首先创建它们，您需要手动创建它们将使用的硬盘分区，然后配置 RAID 设备以使用这些分区。要为 RAID 阵列创建硬盘分区，请使用 `fdisk` 或 `parted` 并将文件系统类型指定为 `fd`。您使用要创建分区的硬盘的设备名称调用 `fdisk` 或 `parted`。务必将 `fd` 指定为分区类型。以下示例为硬盘 `/dev/hdb`（主 IDE 连接上的第二个硬盘）调用 `fdisk`：

```
fdisk /dev/hdb
```

尽管从技术上讲是分区，但在 RAID 配置文档和文件中，这些硬盘设备被称为磁盘。

## 配置 RAID：/etc/raidtab

一旦有了磁盘，就需要将它们配置为 RAID 设备。RAID 设备在 `/etc/raidtab` 文件中进行配置。此文件将由 `mkraid` 命令用于创建 RAID 设备。在 `/etc/raidtab` 文件中，您为每个 RAID 设备创建一个 `raiddev` 条目，并指定它们将使用的磁盘以及任何 RAID 选项。对于 `raiddev` 条目，您指定正在配置的 RAID 设备的名称，例如 `/dev/md0` 表示第一个 RAID 设备。

```
raiddev /dev/md0
```

然后您使用 `raid-level` 关键字后跟 RAID 级别数字指定 RAID 设备的级别，例如 0、1 或 5。然后添加您可能需要的任何选项以及构成 RAID 阵列的磁盘列表。磁盘使用 `device` 条目定义，并使用 `raid-disk` 选项指定其在 RAID 阵列中的位置。配置指令和选项列在表 31-3 中。以下是 `/etc/raidtab` 文件的示例条目：

```
raiddev /dev/md0
  raid-level       5
  nr-raid-disks    3
  nr-spare-disks   1
  persistent-superblock 1
  chunk-size       4
  parity-algorithm left-symmetric
  device           /dev/hdb1
    raid-disk       0
  device           /dev/hdc1
    raid-disk       1
  device           /dev/hdd1
    raid-disk       0
```

前面的示例将 RAID 设备 `/dev/md0` 配置为 RAID 5（`raid-level 5`）设备。构成此 RAID 阵列的有三个磁盘（分区），`/dev/hdb1`、`/dev/hdc1` 和 `/dev/hdd1`，其中 `/dev/hdb1` 为第一个，`/dev/hdc1` 为第二个。有 一个备用磁盘 `/dev/hdd1`。总共有三个 RAID 磁盘（`nr-raid-disks`）和一个备用分区（`nr-spare-disks`）。RAID 文件系统使用持久超级块（`persistent-superblock`）来保存文件系统配置信息，从而允许自动检测您的设备。`parity-algorithm` 选项用于 RAID 5 设备，以指定用于奇偶校验恢复的奇偶校验算法类型，在此示例中为 `left-symmetric`。

| 指令和选项 | 描述 |
|---|---|
| `raiddev device` | 为特定 RAID 设备开始一个配置段。 |
| `raid-level num` | RAID 设备的 RAID 级别，例如 0、1、4、5 和 -1（线性）。 |
| `device disk-device` | 要添加到 RAID 阵列的磁盘设备（分区）。为 RAID 设备指定的 `device` 条目数量必须与 `nr-raid-disks` 指定的数量相匹配。 |
| `nr-raid-disks count` | 阵列中的 RAID 设备数量。每个 RAID 设备段必须有此指令。最大值为 12。 |
| `nr-spare-disks count` | 阵列中的备用设备数量。仅用于 RAID 4 和 RAID 5。内核必须配置为允许根据需要自动添加新的 RAID 磁盘。您可以使用 `raidhotadd` 和 `raidhotremove` 添加和删除备用磁盘。 |
| `persistent-superblock 0/1` | 指定新创建的 RAID 阵列是否应使用持久超级块。用于帮助内核自动检测 RAID 阵列。RAID 阵列信息保存在每个 RAID 成员的超级块中。 |
| `chunk-size size` | 将条带大小设置为 `size` 字节，以 2 的幂为单位。 |
| `device devpath` | 将最近定义的设备添加到构成 RAID 系统的设备列表中。 |
| `raid-disk index` | 将最近定义的 RAID 设备插入 RAID 阵列中指定位置。 |
| `spare-disk index` | 将最近定义的 RAID 设备作为备用设备插入 RAID 阵列中指定位置。 |
| `parity-disk index` | 最近定义的设备用作奇偶校验设备，将其放置在 RAID 阵列的末尾。 |
