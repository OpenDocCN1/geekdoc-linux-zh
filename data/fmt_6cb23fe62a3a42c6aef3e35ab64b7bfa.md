
要添加新的 RAID 设备或从头创建它们，你将创建将使用的硬盘磁盘分区。要为 RAID 阵列创建硬盘磁盘分区，请使用 `fdisk` 或 `parted` 并使用 `-f` 指定文件系统类型。你通过要创建分区的硬盘设备名称调用 `fdisk` 或 `parted`。请务必指定 `-f` 为分区类型。以下示例为硬盘 `/dev/hdc`（次级 IDE 连接上的第一个硬盘）调用 `fdisk`：

```bash
fdisk /dev/hdc
```

虽然技术上是分区，但这些硬盘设备在 RAID 配置文档和文件中被称为磁盘（disk）。

![](img/70a65fc8f3408711ddea7ea368f31720_704_0.png)

# 配置 RAID：`/etc/mdadm.conf`

一旦你有了磁盘，就需要将它们配置为 RAID 设备。RAID 设备在 `/etc/mdadm.conf` 文件中配置，选项如表 33-3 所示。此文件将由 `create` 模式下的 `mdadm` 命令用于创建 RAID 设备。在 `/etc/mdadm.conf` 文件中，你同时创建了 `DEVICE` 和 `ARRAY` 条目。`DEVICE` 条目列出 RAID 设备。`ARRAY` 条目列出 RAID 阵列及其选项。

- `/dev/hda1`
- `/dev/hda2`
- `/dev/hdc1`

你可以在 `DEVICE` 条目中列出多个设备，也可以有多个独立的 `DEVICE` 条目。你还可以使用匹配符号 `*`、`?` 或 `[]` 来指定多个设备。以下将把 hda 驱动器上的所有分区指定为 RAID 设备：

- `DEVICE /dev/hda*`
- `/dev/hdc1`

对于 `ARRAY` 条目，你指定你正在配置的 RAID 设备名称，例如第一个 RAID 设备为 `/dev/md0`。然后你添加配置选项，作为 `devices` 来列出组成阵列的分区、作为 RAID 级别的 `level`，以及作为设备数量的 `num-devices`。

```
ARRAY /dev/md0 devices=/dev/hdb,/dev/hdc1 level=5 num-devices=3
```

前面的示例将 RAID 阵列 `/dev/md0` 配置为 RAID 5 (`level=5`) 设备。两个磁盘（分区）构成了这个 RAID 阵列：`/dev/hdb1` 和 `/dev/hdc1`。

| 指令或选项 | 描述 |
|---|---|
| `DEVICE devices-list` | 用于 RAID 设备的分区和驱动器。 |
| `ARRAY` | 特定 RAID 设备的 ARRAY 配置部分。 |
| `level=num` | RAID 设备的级别，例如 0, 1, 4, 5 和 -1（线性）。 |
| `devices=disk-list` | 组成 RAID 阵列的磁盘设备（分区）。 |
| `num-devices=count` | 阵列中 RAID 设备的数量。每个 RAID 设备部分必须包含此指令。最大值为 12。 |
| `spare-group=name` | 备用组的文本名称，其设备可用于其他阵列。 |
| `auto=option` | 如果不存在，则自动创建非分区设备。你可以创建传统的非分区设备（yes 或 md 选项）或较新的可分区阵列（adp 或 part 选项）。对于可分区阵列，默认值为 4，你可以更改它。 |
| `super-minor` | 阵列超级块的次序号，与 md 设备号相同。 |
| `uuid=UUID-number` | 存储在阵列超级块中的 标识符，用于识别 RAID 阵列。可用于命令中引用阵列。 |
| `MAILADDR` | 监控模式，发送警报的邮件地址。 |
| `PROGRAM` | 监控模式，在发生事件时运行。 |

表 33-3 mdadm.conf 选项

# 创建 RAID 阵列

你可以创建一个 RAID 阵列。你可以使用 `create` 模式创建 RAID 设备，列在在在过程中 RAID RAID，你已经已经拥有可以的 RAID 设备。你的 RAID 设备将配置在 `/etc/mdadm.conf` 文件中。在 `/etc/mdadm.conf` 文件中，你创建了 `DEVICE` 和 `ARRAY` 条目。`DEVICE` 条目列出 RAID 设备。`ARRAY` 条目列出 RAID 阵列及其选项。

- 
RAIDdev/md，，，////
/ /dev/
 /dev/hda1 /dev/hdc1

```
/
```

`ARRAY /dev/md0 devices=/dev/hdb,/dev/hdc1 level=5 num-devices=3`

```
```

/dev/md0 devicesdevdev/111dev/ 1
