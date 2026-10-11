
| Device | Start | |
| :--- | :--- | :--- |
| `/sdb` | 1 |

## 注意

如果下一步的 `pvcreate` 命令不起工作，很可能是没有安装 LVM2 包。要安装包，请参阅第 9 章。

下一步是使用分区创建实际卷。这是通过 `pvcreate` 命令完成的。`pvcreate` 命令将分区标记为 PV：

```
$ sudo pvcreate /dev/sdb1

Physical volume "/dev/sdb1" created
```

## 注意

不要被 `mpath: failed to get device for 8:17` 消息吓到。只要你收到成功创建的消息，一切正常。可以使用 `pvdisplay` 命令显示你创建的物理卷列表，以查看过程中的进度：

```
$ sudo pvdisplay /dev/sdb1

"/dev/sdb1" is a new physical volume of "2.01 GiB"

- NEW Physical volume

PV Name /dev/sdb1

VG Name

PV Size 2.01 GiB

Allocable NO

PE Size 0

Total PE 0

Free PE 0

Allocated PE 0
```

`pvdisplay` 命令显示 `/dev/sdb1` 现在已标记为 PV。然而，在输出中，PV 名称是空的。该 PV 不属于任何卷组。

## 创建卷组（Volume Groups）

过程的下一步是从物理卷创建一个或多个卷组。对于你的系统需要多少个卷组没有固定规则——你可以将所有可用物理卷添加到单个卷组，也可以通过组合不同的物理卷创建多个卷组。

```
$ sudo vgcreate Vol1 /dev/sdb1

Volume group "Vol1" successfully created
```

这并不是全部的有趣输出！如果你想查看有关新创建卷组的细节，请使用 `vgdisplay` 命令：

```
$ sudo vgdisplay Vol1

- Volume group - Vol1

- VG Name

System ID

Format lvm2

Metadata Areas 1

Metadata Sequence 1
```

```
VG Access read/write

VG Status resizable

MAX LV 0

Cur LV 0

Open LV 0

Max PV 0

Cur PV 1

Act PV 1

VG Size 2.00 GiB

PE Size 4.00 MiB

Total PE 513

Alloc PE / Size 0 / 0

Free PE / Size 513 / 2.00 GiB

VG UUID oe4I7e-5RA9-G9ti-AnoI-QKLz-qX4-58Wj6e
```

此示例创建了一个名为 `vol1` 的卷组，它使用了在 `/dev/sdb1` 分区上创建的物理卷。

现在，你已经创建了一个或多个卷组，准备好创建逻辑卷了。

# 创建逻辑卷

逻辑卷是 Linux 系统用于模拟物理分区的内容，并承载文件系统。Linux 系统像处理物理分区一样处理逻辑卷，允许你在逻辑卷中定义文件系统，然后将文件系统挂载到虚拟目录中。

要创建逻辑卷，请使用 `lvcreate` 命令。虽然在其他 Linux LVM 命令中你通常可以不使用命令行选项，但 `lvcreate` 命令至少需要输入选项。表 8.5 显示了可用的命令选项。

表 8.5 `lvcreate` 选项

| 选项 | 长选项名称 | 描述 |
|---|---|---|
| `-c` | `--chunksize` | 指定快照逻辑卷的块大小 |
| `-C` | `contiguous` | 设置或重置连续分配策略 |
| `-i` | `--stripes` | 指定条带（stripes）的数量 |
| `-I` | `--stripsize` | 指定每个条带的大小 |
| `-1` | `--extents` | 指定分配给新逻辑卷的逻辑区（extents）数量，或要使用的逻辑区百分比 |
| `-L` | `--size` | 指定分配给新逻辑卷的磁盘大小 |
| | `--minor` | 指定设备的次设备号 |
| `-m` | `--mirrors` | 创建镜像逻辑卷 |

# 使次设备号持久化

| 选项 | 长选项名称 | 描述 |
|---|---|---|
| `-M` | `persistent` | |
| `-n` | `--name` | 指定新逻辑卷的名称 |
| `-p` | `permission` | 为逻辑卷设置读写权限 |
| `-r` | `--reahead` | 设置预读扇数 |
| `-R` | `regionsize` | 指定将镜像区域划分的大小 |
| `-s` | `--snapshot` | 创建快照逻辑卷 |
| `-Z` | `--zero` | 将新逻辑卷前 1KB 的数据置零 |

尽管命令行选项看起来可能令人生而畏，但在大多数情况下，你只需要少量的选项即可完成：

```
$ sudo lvcreate -l 100%FREE -n lvtest Vol1

Logical volume "lvtest" created

$
```

如果你想查看所创建内容的详情，请使用 `lvdplay` 命令：

```
$ sudo lvdplay Vol1

- Logical volume /dev/Vol1/lvtest

- LV Name lvtest

- VG Name Vol1

- LV UUID 4W2369-pLXy-jWmb-lIFN-SMNX-xZnN-3KN208

- LV Write Access read/write

- LV Creation host, time ... -0400

- LV Status 0

- LV Size 2.00 GIB

- Current LE 513

- Segments 1 inherit

- Allocation auto

- Read ahead sectors

- currently set to 256

- Block device 253:2$
```

现在你可以看到你刚刚创建的内容了！注意，卷组名称（`vol1`）用于在创建新逻辑卷时标识要使用的卷组。

`-l` 参数定义了指定卷组中可用空间的使用比例，你可以将值指定为卷组中可用空间的百分比。此示例使用了所有（100%）的可用空间来创建新逻辑卷。

你可以使用 `-l` 参数按可用空间的百分比来指定大小，或者使用 `-L` 参数按字节、千字节（KB）、兆字节（MB）或字节（GB）指定实际大小。`-n` 参数允许你为逻辑卷提供名称（在本示例中称为 `lvtest`）。

# 创建文件系统

运行 `lvcreate` 命令后，逻辑卷已存在，但还没有文件系统。要创建它，你需要针对要创建的文件系统使用相应的命令行程序：

```
$ sudo mkfs.ext4 /dev/Vol1/lvetest

mke2fs 1.41.12 (17-May-2010)

Filesystem label=

OS type: Linux

Block size=4096 (log=2)

Fragment size=4096 (log=2)

Stride=0 blocks, Stripe width=0 blocks

131736 inodes, 525312 blocks

26265 blocks (5.00%) reserved for the super user

First data block=0

Maximum filesystem blocks=541065216

17 block groups

32768 blocks per group, 32768 fragments per group

7728 inodes per group

Superblock stored on blocks:

32768, 98304, 163840
```
