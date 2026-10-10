
## RAID 管理：mpathd

Red Hat Enterprise Linux 和 Fedora 使用 `mpathd` 工具来管理和监控 RAID 设备。它取代了以前版本的 Red Hat Enterprise Linux 和 Fedora 中使用的较旧的 raid 工具。`mpathd` 工具是一种通用的创建、监控和管理

## 创建和安装 RAID 设备

如果在安装过程中已经创建了 RAID 设备及其分区，那么你应该已经有了可用的 RAID 设备。你的 RAID 设备配置在 `/etc/mdadm.conf` 文件中，而 RAID 设备的状态则列在 `/proc/mdstat` 文件中。你可以使用 `raidstart` 和 `mdadm` 命令手动启动或停止 RAID 设备。`-a` 选项可操作所有设备，但如果需要，你也可以指定特定的设备。要为已安装的系统手动创建新的 RAID 设备，请遵循以下步骤：

- 确保内核支持你要为正在创建的设备所需的 RAID 级别。
- 如果尚未这样做，请创建用于 RAID 设备的 RAID 磁盘（分区）。
- 使用 `mdadm` 命令的构建（build）或创建（create）模式创建你的 RAID 设备。该阵列也将被激活。
- 或者，你可以配置 `/etc/mdadm.conf` 文件中的 RAID 设备（`/dev/mdn`），指定要使用的 RAID 磁盘，然后使用指定了要创建的 RAID 设备的 `mdadm` 命令。
- 在 RAID 设备上创建文件系统（`mkfs`），然后将其挂载。

## 添加独立的 RAID 文件系统

如果你只是想向一个已有标准引导分区的系统添加 RAID 文件系统，你可以省略第一个 RAID 1 分区。假设使用两个硬盘用于 RAID 文件系统，你只需要两个分区，每个硬盘各一个，即 `/dev/sda1` 和 `/dev/sdb1`。

```
ARRAY /dev/md0 devices=/dev/sda1,/dev/sdb1 level=5 num-devices=2
```

**表 31-2 mdadm 模式**

| 模式 | 描述 |
| --- | --- |
| assemble | 从设备组装 RAID 阵列。 |
| build | 在没有每设备超块的情况下构建阵列。 |
| create | 在具有每设备超块的情况下构建阵列。 |
| manage | 管理阵列设备，添加或移除磁盘。 |
| misc | 对设备的特定操作，例如将其设为只读。 |
| monitor | 监控阵列的变化并采取措施（用于 RAID 1, 4, 5, 6）。 |
| grow | 更改阵列大小，例如用较大的设备替换较小的设备时。 |

然后你可以使用以下命令创建阵列：

```
mdadm -C /dev/md0 -n2 /dev/sda1 /dev/sdb1 -l5
```

然后你可以格式化和挂载你的 RAID 设备。

## 创建硬盘分区：raid

若要添加新的 RAID 设备或首次创建它们，你需要手动创建它们将使用的硬盘分区，然后配置 RAID 设备以使用这些分区。要为 RAID 阵列创建硬盘分区，请使用 `fdisk` 或 `parted`，并指定 `raid` 作为文件系统类型。使用你想要创建分区的硬盘的设备名称调用 `fdisk` 或 `parted`。请务必指定 `raid` 作为分区类型。以下示例针对硬盘 `/dev/hdc`（次要 IDE 连接上的第一个硬盘）调用 `fdisk`：

```
fdisk /dev/hdc
```

虽然从技术上讲这些是分区，但在 RAID 配置文档和文件中，这些硬盘设备被称为磁盘。

> **注意** *你也可以使用 parted 或 qparted 来创建硬盘分区。这些工具为 parted 提供了图形用户界面（应用程序 | 系统工具菜单）。*

## 配置 RAID：/etc/mdadm.conf

一旦你有了磁盘，就需要将它们配置为 RAID 设备。RAID 设备在 `/etc/mdadm.conf` 文件中配置，选项如表 31-3 所示。此文件将被 `mdadm` 命令在创建模式下用于创建 RAID 设备。在 `/etc/mdadm.conf` 文件中，你创建 `DEVICE` 和 `ARRAY` 条目。`DEVICE` 条目列出 RAID 设备。`ARRAY` 条目列出 RAID 阵列及其选项。此示例在两个磁盘上实现了一个简单的阵列。使用的串行 ATA 硬盘驱动器使用 `sd` 而不是 `hd` 作为设备名称前缀。

```
DEVICE /dev/sda1 /dev/sdb1
```

你可以为一个 DEVICE 条目列出多个设备，也可以拥有单独的 DEVICE 条目。你还可以使用文件匹配符号（如 `*`、`?` 或 `[]`）来指定多个设备。以下操作将指定 `sda` 驱动器上的所有分区作为 RAID 设备：

```
DEVICE /dev/sda* /dev/sdb1
```

对于 `ARRAY` 条目，你指定正在配置的 RAID 设备的名称，例如第一个 RAID 设备为 `/dev/md0`。然后你添加配置选项，例如使用 `devices` 来列出组成阵列的分区，使用 `level` 指定 RAID 级别，使用 `num-devices` 指定设备数量。第一个阵列仅包含引导分区并使用 RAID 级别 1，而第二个阵列使用两个分区并设置为 RAID 级别 5。

```
ARRAY /dev/md0 devices=/dev/sda2, /dev/sdb1 level=5 num-devices=2
```

**表 31-3 mdadm.conf 选项**

| 指令或选项 | 描述 |
|---|---|
| DEVICE devices-list | 用于 RAID 设备的分区和驱动器。 |
| ARRAY | 特定 RAID 设备的 ARRAY 配置部分。 |
| level=num | RAID 设备的 RAID 级别，例如 0, 1, 4, 5 和 –1（线性）。 |
| devices=disk-device-list | 组成 RAID 阵列的磁盘设备（分区）。 |
| num-devices=count | 阵列中的 RAID 设备数量。每个 RAID 设备部分都必须有此指令。最大值为 12。 |
| spare-group=name | 备用组的文本名称，其设备可用于其他阵列。 |
| auto=option | 如果指定的设备不存在，则自动创建。你可以创建传统的非分区阵列（yes 或 md 选项）或较新的可分区阵列（mdp 或 part 选项）。对于可分区阵列，默认为 4，你可以更改此设置。 |
| super-minor | 阵列超块的主设备号，与 md 设备号相同。 |
| uuid=UUID-number | 存储在阵列超块中的 UUID 标识符，用于识别 RAID 阵列。可用于在命令中引用阵列。 |
| MAILADDR | 监控模式，接收警报的邮件地址。 |
| PROGRAM | 监控模式，当事件发生时运行的程序。 |

上述示例将 RAID 阵列 `/dev/md0` 配置为使用 `/dev/sda1` 和 `/dev/sdb1` 的两个磁盘（分区），并配置为 RAID 5（level=5）。

## 创建 RAID 阵列

你可以使用 `mdadm` 命令指定的选项或使用 `/etc/mdadm.conf` 文件中列出的配置来创建 RAID 阵列。使用 `/etc/mdadm.conf` 文件并非必需，但它使 RAID 创建更易于管理，特别是对于大型或复杂的阵列。一旦你创建了 RAID 设备，你的 RAID 设备将被自动激活。以下命令在级别 5 上使用两个设备 `/dev/sda2` 和 `/dev/sdb1` 创建 RAID 阵列 `/dev/md1`。

```
mdadm --create /dev/md1 --raid-devices=2 /dev/sda1 /dev/sdb1 --level=5
```

每个选项都有对应的短版本，如表 31-4 所示。此处显示了使用单字母选项的相同命令。

```
mdadm -C /dev/md1 -n2 /dev/sda1 /dev/sdb1 -l5
```

如果你已在 `/etc/mdadm.conf` 文件中配置了 RAID 设备，则接下来使用 `mdadm` 命令的创建模式来创建你的 RAID 设备。`mdadm` 接受 RAID 设备的名称作为参数，例如第一个 RAID 设备为 `/dev/md0`。然后它在 `/etc/mdadm.conf` 文件中定位该设备的条目，并使用该配置信息在该设备上创建 RAID 文件系统。如果需要，你可以使用 `-c` 选项指定备用配置文件。`mdadm` 作为 RAID 设备的一种 `mkfs` 命令运行，初始化分区并创建 RAID 文件系统。组成 RAID 阵列的分区上的任何数据都将被擦除。

```
mdadm --create /dev/md0
```
