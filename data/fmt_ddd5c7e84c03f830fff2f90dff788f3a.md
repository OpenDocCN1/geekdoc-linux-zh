
| 线性 (Linear) | 追加 | 简单将硬盘视为一个驱动器，没有条带、镜像或校验。 |
| 0 | 条列 (Striping) | 跨驱动实现条列，无冗余。 |
| 1 | 镜像 (Mirroring) | 实现高水平冗余。每块磁盘都被视为所有数据的镜像。 |
| 4 | 校验 (Parity) | 使用校验信息进行数据重建，保留在单独的磁盘上。 |
| 5 | 分布式校验 (Distributed parity) | 使用校验信息进行数据重建。校验信息分布在所有驱动上。 |
| 6 | 分布式校验 (Distributed parity) | 使用分布在所有驱动上的双重校验信息进行数据重建。 |
| 10 | 条列与镜像 (Striping and Mirroring) | 实现条带的高水平冗余。也称为 RAID 1+0。 |
| 多路径 (Multipath) | 多路访问 | 支持对同一设备的多路访问 |

# 第 16 章：RAID 和 LVM

注意：对于 RAID 1，需要相同大小的磁盘；对于 RAID 5，建议使用相同磁盘。

## 线性 (Linear)

线性级别允许你将几块硬盘合并为一个，提供一个连续存储池。你不再被强制在每个驱动器上设置单独的分区，实际上你只有一个驱动器。当一个磁盘填满时，将使用下一块。如果你有一个包含两块硬盘的硬盘阵列，在使用其中一块后，会自动开始下一块。此级别不提供恢复功能。

## RAID 0：条列 (Striping)

为了效率，RAID 使用条列存储数据，其中数据组织成条带并存储在 RAID 驱动器上，以便快速访问（级别 0）。RAID 0 也会组织你的硬盘，但将它们视为单盘。如果你有一个包含两块硬盘的硬盘阵列，你可以像访问设备一样访问它们。

提示：请记住，许多“硬件” RAID 设备实际上是软件 RAID。尽管你在 BIOS 中配置了它们，但驱动程序像其他程序一样是以软件形式运行的。在这方面，它们被认为比 Linux RAID 解决方案灵活性低，并且直接取决于供应商的更新。

## RAID 1：镜像 (Mirroring)

RAID 级别 1 通过镜像实现冗余。在镜像中，相同的数据被写入每个 RAID 驱动器。每块磁盘都有所有数据的完整副本，因此当一个或多个磁盘故障时，其他磁盘仍然保留其数据。尽管极其安全，但冗余可能会导致效率低下且存储成本较高。例如，在由两个磁盘组成的 RAID 阵列中，一块用于标准存储，另一块用于实时备份。这导致你的系统只剩一块磁盘可用。写入操作也必须复制，因为 RAID 阵列使用了多个镜像磁盘，这会减慢操作速度。

## RAID 5 和 6：分布式校验 (Distributed Parity)

作为镜像的替代方案，可以使用校验信息进行数据重建，而不是完全复制数据。校验信息占用的空间相当于一块磁盘，留下了大部分 RAID 驱动器的空间。RAID 5 结合了条列和校验（参见 RAID 4），其中校验信息分布在硬盘上，而不是在一个专门用于此目的的磁盘上。这允许使用更高效的访问方法——条列。RAID 5 同时提供了快速访问和恢复能力，是最受欢迎的级别。例如，由四块 80GB 硬盘组成的阵列将被视为一个 320GB 的驱动器，其中部分空间（80GB）用于存储校验信息，提供 240GB 可用空间。RAID 5 至少需要三块硬盘。

RAID 6 的运行方式与 RAID 5 相同，但它对数据使用双重校验信息，提供了更大的恢复能力。

# 第 3 部分：设备与文件系统

## RAID 4：校验 (Parity)

虽然由于开销成本，Red Hat Enterprise Linux 和 Fedora 不支持 RAID 4，但它像 RAID 5 一样支持使用校验信息而非镜像数据的更紧凑的恢复形式。在 RAID 4 中，校验信息保留在单独的磁盘上，而其他磁盘用于数据存储，类似于线性模型。

提示：Red Hat Enterprise Linux 和 Fedora 还允许你在安装期间创建并格式化 Linux 软件 RAID 设备。此时，你可以创建你的 RAID 分区和设备。

## RAID 10：条列与镜像 (Striping and Mirroring)

RAID 10 也称为 1+0，结合了条列和镜像（RAID 0 和 1）。这同时提供了冗余和快速访问。

## 多路径 (Multipath)

虽然它不是真正的 RAID 级别，但多路径允许对同一设备进行多路访问。如果一个控制器故障，可以使用另一个访问设备。实际上，你拥有控制器的冗余。在 Red Hat Enterprise Linux 和 Fedora 上使用 `mdadm` 实现这种支持。它通过 `mdadm` 服务脚本启动。

```
mdadm start
```

## RAID 设备与分区：md 和 fd

设备被命名为 `md` 并使用 MD 驱动程序。这些设备已定义在 Linux 系统的 `/dev` 目录下，从 `md0` 开始；`/dev/md0` 是第一个 RAID 设备，`/dev/md1` 是第二个，以此此类推。每个 RAID 设备使用分区，每个分区包含整个磁盘。在创建 RAID 分区时，你应该将分区类型设置为 `fd`，而不是标准的 Linux 分区 `83`。`fd` 类型用于 RAID 的自动检测。这些分区通常被称为 RAID 磁盘，而 RAID 设备则是它使用的 RAID 磁盘的阵列。

## 从 RAID 设备启动

在安装过程中，Fedora 允许你创建可以从其启动系统的 RAID 设备。你的 Linux 系统将配置为加载 RAID 内支持并自动检测你的设备。引导程序将安装在你的 RAID 设备，意味着安装在组成该设备的所有磁盘上。

Fedora 不支持从 RAID 5 启动，仅支持 RAID 1。这意味着如果你想使用 RAID 5 且从 RAID 磁盘启动，你需要至少创建两个（或更多）RAID 设备，并在每个设备中使用对应分区。其中一个设备将包含 `/boot` 分区并安装为 RAID 1 设备。这个 RAID 1 设备将是 RAID 设备 `md0`，由每块硬盘的第一个分区组成。第二个 RAID 设备 `md1` 可以是 RAID 5 设备。它由其他硬盘上的对应分区组成。你的系统可以从 RAID 1 设备启动，但使用 RAID 5 设备。

如果你在安装过程中没有创建 RAID 磁盘，而是在之后才创建并希望从它们启动，那么你必须确保系统配置正确。RAID 设备需要使用具有持久性超级块（superblocks）的方式来创建。如果你在 `/`（根分区）上使用 RAID 5，将会遇到困难。因为该分区包含了 RAID 5 模块；要访问该分区，你必须已经加载了 RAID 5 模块。为了规避这一限制，你可以在 `/boot` 分区创建一个包含 RAID 5 模块的 RAM 磁盘（RAM disk）。使用 `mkinitrd` 命令创建 RAM 磁盘，并使用 `--with` 选项指定要包含的模块。

```
mkinitrd --preload raid5 --with=raid-ramdisk 2.6.29.5-159
```

### RAID 管理：mdadm

Red Hat Enterprise Linux 和 Fedora 使用 `mdadm` 工具来管理和监控 RAID 设备。它取代了以前版本 Red Hat Enterprise Linux 和 Fedora 中旧的 `ertools`。`mdadm` 是一个用于创建、监控、管理和修复 RAID 设备的通用工具。你可以直接运行命令来创建和格式化 RAID 磁盘。它还可以作为守护进程运行，以监控和检测设备问题。具有几种不同的运行模式，每种模式都有自己的一套选项，例如使用 `-f` 选项进行监控以作为守护进程运行，或使用 `-l` 选项进行创建以为磁盘设置 RAID 级别。表 16-2 列出了不同的运行模式。查阅 `mdadm` 手页（Man page）获取每种模式选项的详细列表。

| 模式 | 说明 |
| --- | --- |
| assemble | 从设备组装 RAID 阵。 |
| build | 构建不带每个设备超级块的阵。 |
| create | 构建带每个设备超级块的阵。 |
| manage | 管理阵设备，添加或删除磁盘。 |
| misc | 对设备进行特定操作，例如将其设置为只读。 |
| monitor | 监控阵的变化并采取行动（用于 RAID 1, 4, 5, 6）。 |
| grow | 更改阵的大小，当用较大的设备替换较小的设备时。 |

**表 16-2：mdadm 模式**

### 创建和安装 RAID 设备

如果你在安装过程中创建了 RAID 设备及其分区，那么你应该已经有了可以工作的 RAID 设备。你的 RAID 设备将配置在 `/etc/mdadm.conf` 文件中，你的 RAID 设备状态则可以在 `/proc/mdstat` 文件中读取。你可以使用 `raidstart` 和 `mdadm` 命令手动启动或停止 RAID 设备。`-a` 选项作用于所有设备，尽管你也可以根据指定特定的设备。

要为已安装的系统手动创建一个新的 RAID 设备，请遵循以下步骤：

- 确保你的内核支持你为要创建的设备选择的 RAID 级别。
- 如果你还没有这样做，请创建你将为 RAID 设备使用的 RAID 磁盘（分区）。
- 使用 `mdadm` 命令在 `build` 模式或 `create` 模式下创建你的 RAID 设备。该阵也将被激活。
- 或者，你可以在 `/etc/mdadm.conf` 文件中配置你的 RAID 设备 (`/dev/mdn`)，指定要使用的 RAID 磁盘，然后使用 `mdadm` 命令指定要创建的 RAID 设备。
- 在 RAID 设备上创建文件系统 (`mkfs`) 并将其挂载。

#### 添加独立的 RAID 文件系统

如果你只是只想为一个已经有启动分区的系统添加 RAID 文件系统，可以跳过第一个 RAID 1 分区。用于 RAID 文件系统需要两个块硬盘，对于每个磁盘，你需要两个分区，`/dev/sdb1`、`dev/sdc1` 和 `/dev/sdd1`。

```
ARRAY /dev/md0 devices=/dev/sdb1,/dev/sdc1,/dev/sdd1 level=5 num-devices=3
```

然后你使用以下命令创建阵：

```
mdadm -C /dev/md0 -n2 /dev/sdb1 /dev/sdc1 /dev/sdd1 -l15
```

你可以格式化并挂载你的 RAID 设备。

#### 创建硬盘分区：fdisk

要添加新的 RAID 设备或从一开始创建它们，你需要手动创建它们将使用的硬盘分区，然后配置 RAID 设备使用这些分区。要为 RAID 阵创建硬盘分区，请使用 `fdisk` 或 `parted` 并指定 `fdisk` 为文件类型。你通过想要创建的硬盘名称来调用 `fdisk` 或 `parted`。

注意：要为 RAID 阵创建硬盘分区，请使用 `fdisk` 或 `parted` 并指定 `fdisk` 为文件类型。你通过想要创建的硬盘名称来调用 `fdisk` 或 `parted`。

#### 配置 RAID：mdadm

一旦你有了 RAID 设备，你就可以在 `/etc/mdadm.conf` 文件中配置它们。你的 RAID 设备状态可以在 `/proc/mdstat` 文件中读取。你可以使用 `raidstart` 和 `mdadm` 命令手动启动或停止 RAID 设备。`-a` 选项作用于所有设备，尽管你也可以指定特定的设备。

RAID 设备需要使用具有持久性超级块的方式来创建。如果你在 `/`（根分区）上使用 RAID 5，将会遇到困难。因为该分区包含了 RAID 5 模块；要访问该分区，你必须已经加载了 RAID 5 模块。为了规避这一限制，你可以在 `/boot` 分区创建一个包含 RAID 5 模块的 RAM 磁盘。使用 `mkinitrd` 命令创建 RAM 磁盘，并使用 `--with` 选项指定要包含的模块。

```
mkinitrd --preload raid5 --with=raid-ramdisk 2.6.29.5-159
```

## 第 3 部分：设备和文件系统

## 第 16 章：RAID 和 LVM

RAID 设备需要使用具有持久性超级块的方式来创建。如果你在 `/`（根分区）上使用 RAID 5，将会遇到困难。因为该分区包含了 RAID 5 模块；要访问该分区，你必须已经加载了 RAID 5 模块。为了规避这一限制，你可以在 `/boot` 分区创建一个包含 RAID 5 模块的 RAM 磁盘。使用 `mkinitrd` 命令创建 RAM 磁盘，并使用 `--with` 选项指定要包含的模块。

```
mkinitrd --preload raid5 --with=raid-ramdisk 2.6.29.5-159
```

```
mdadm -C /dev/md1 -n3 /dev/sdb1 /dev/sdd1 /dev/mdadm.conf -15
```

如果您已经在 `/etc/mdadm.conf` 文件中配置了你的 RAID 设备，那么您可以使用 `mdadm` 命令的创建模式来创建您的 RAID 设备。`mdadm` 的参数是 RAID 设备名称，例如第一个 RAID 设备的名称为 `/dev/md0`。它会在 `/etc/mdadm.conf` 文件中查找该设备的条目，并使用该信息在相应设备上创建 RAID 文件系统。如果您需要，可以使用 `-c` 选项指定备用配置。`mdadm` 的操作类似于 RAID 设备的 `mkfs` 命令，用于初始化分区并创建 RAID 文件系统。组成 RAID 阵的分区上的任何数据都将被删除。

```
mdadm --create /dev/md0
```

| 选项 | 描述 |
|---|---|
| -n --raid-devices | RAID 设备数量 |
| -l --level | RAID 级别 |
| -C --create | 创建模式 |
| -c --chunk | 以 2 的幂次方指定块（条带）大小，默认为 64KB |
| -x --spare-devices | 阵列中的备用设备数量 |
| -z --size | 设备中使用的块大小，默认设置为最小的相同大小 |
| -p --parity | 指定奇偶校验算法；默认使用左对称（left-symmetric） |

**表 16-4：mdadm --create 选项**

### 创建备用组

Linux RAID 现在允许 RAID 阵列共享它们的备用设备。这意味着如果多个阵列属于同一个备用组，那么当一个阵列中的设备发生故障时，它可以自动使用另一个阵列中的备用设备。任何阵列的备用设备都可以根据需要用于另一个阵列。您可以使用 `--spare-group` 选项设置阵列所属的备用组。`mdadm` 监控模式会检测阵列中的故障设备，并自动用同一备用组中的备用设备替换它。以下示例中的第一个命令为 `/dev/md0` 阵列创建一个名为 `/dev/sd` 的备用驱动器，并将其标记为组。在第二个命令中，阵列 `/dev/md1` 没有备用设备，但与 `/dev/md0` 属于同一个备用组。如果 `/dev/md1` 中的设备发生故障，它可以自动使用来自 `/dev/md0` 的备用设备 `/dev/sde1`。以下代码行实际上是单行，每行都以 `mdadm` 开始。

```
mdadm --create /dev/md0 --raid-devices=4 /dev/sda1 /dev/sdc1 /dev/sdd1 -x /dev/sdel --level=5 --spare-group=mygroup
mdadm --create /dev/md1 --raid-devices=2 /dev/sdf1 /dev/sdg1 --level=1 --spare-group=mygroup
```

## 创建文件系统

一旦激活 RAID 设备，您就可以在 RAID 设备上创建文件系统并挂载这些文件系统。以下示例在 `/dev/md0` 设备上创建一个标准的 Linux 文件系统：

```
mkfs.ext3 /dev/md0
```

在接下来的示例中，用户随后创建一个名为 `/myraid` 的目录并将 RAID 设备挂载到那里：

```
mkdir /myraid
mount /dev/md0 /myraid
```

如果您计划使用 RAID 设备来维护您的用户目录和文件，则可以将 RAID 设备挂载为您的 `/home` 分区。如果您在安装系统时就创建了 RAID 设备，通常会使用此类挂载点。要将您当前的家目录传输到 RAID 设备，首先在另一个分区上进行备份，然后挂载 RAID 设备，并将您的家目录复制到：

### 管理 RAID 阵列

您可以使用 `mdadm` 管理操作来管理 RAID 阵列。在此模式下，您可以添加或删除阵列中的设备，还可以将它们标记为故障。`--add` 选项允许您将设备添加到活动阵列中，这本质上是一个热插拔操作。

```
mdadm /dev/md0 --add /dev/sde
```

要从活动阵列中删除设备，您必须先使用 `--fail` 选项将其标记为故障，然后使用 `--remove` 将其移除：

```
mdadm /dev/md0 --fail /dev/sdb1 --remove /dev/sdb1
```

### 启动和停止 RAID 阵列

要启动现有 RAID 阵列，您可以使用组装模式的 `mdadm`（新创建的阵列会自动组装）。

在接下来的示例中，用户随后创建一个名为 `/myraid` 的目录并将 RAID 设备挂载到那里：

```
mkdir /myraid
mount /dev/md0 /myraid
```

要启动现有 RAID 阵列，您可以使用组装模式的 `mdadm`。要停止 RAID 阵列，您可以使用 `--stop` 命令：

```
mdadm --assemble /dev/md0
```

要停止 RAID 阵列，您可以使用：

```
mdadm --stop /dev/md0
```

### 监控 RAID 阵列
