
过程的下一步是为每个 RAID 阵列创建多磁盘（MD）设备。在我的案例中，我想创建三个 MD 设备，一个用于 RAID 1 `/boot`，一个用于 RAID 5 `swap`，另一个用于 RAID 5 `/`。对于这些 MD 设备中的每一个，选择“创建 MD”（Create MD），然后选择阵列的 RAID 级别。然后选择阵列中的活动设备和备用设备数量。在我的案例中，我没有备用设备，所以我每个阵列选择三个活动设备和零备用设备。最后，我选择在特定 MD 设备中使用哪些分区。如果你是按照驱动器的顺序创建每个分区的，这将非常简单，因为 `/dev/sda1`、`dev/sdb1` 和 `/dev/sdc1`（在我的案例中）属于同一个 MD 设备。重复此过程直到创建了所有 MD 设备并选择“完成”。

完成后，分区屏幕将显示你的 RAID 设备，如图 10-3 所示。你会注意到每个 SCSI 驱动器

## 第 10 章 ■ 容错

![](img/4615e4cf343951e4c386edd77976762d_381_0.png)

**图 10-3** 显示了已创建 RAID 设备的分区菜单

显示方式与之前相同，但在它们上方显示了 RAID 设备。这些设备将会被编号，并显示它们的 RAID 级别以及 RAID 设备的总体大小。

下一步是配置分区如何使用这些新的 RAID 设备中的。选择每个 RAID 设备下方行中的未标记分区并按回车（Enter）。从那里开始，如果是普通分区，你就可以配置文件系统、挂载点和其他选项。参见图 10-4，这是我完成后最终分区的示例。完成后，选择“完成分区”（Finish partitioning）并将更改写入磁盘。如果出现提示询问你是否在阵列降级（degraded）时启动，请仔细阅读这样做的风险描述，并选择“是”（Yes）或“否”（No）。安装程序将继续完成剩余的安装过程。跳转到“软件 RAID 管理”部分，学习如何使用 `mdadm` 包的功能来管理你的软件 RAID。

## 安装后配置 RAID

你可以在初始安装后为服务器添加 RAID 存储。在本章的稍后部分中，我将讨论如何从单磁盘迁移到 RAID 阵列，以及如何从一种 RAID 类型迁移到另一种，但现在我假设你只是想向现有服务器添加一个 RAID 阵列。

![](img/4615e4cf343951e4c386edd77976762d_382_0.png)

10-4 完成的 RAID 分区

在此示例中，我添加了三个新硬盘：`/dev/sdb`、`/dev/sdc` 和 `/dev/sdd`，我想对这些硬盘进行分区，并在三个分区上创建一个 RAID 5 阵列，将其挂载到 `/mnt/storage`。

在 Ubuntu 中，软件阵列使用 `mdadm` 工具进行创建和管理。该工具可能没有默认安装；如果没有，运行 `sudo apt-get install mdadm` 来安装该包。下一步是为这些硬盘中的每一个分区。在我的情况下，我创建了一个跨越整个硬盘的单一分区。就像你创建任何其他分区一样，使用你偏喜的分区工具（如 `fdisk` 或 `cfdisk`）。唯一的区别是将分区类型从 `de` 更改为 `fd`。`fd` 分区类型预留给 Linux RAID 自动检测。如果分区设置为该类型，它会告诉 Linux 它是软件 RAID 阵列的一部分。

一旦设置好分区，你就可以在命令行中使用 `mdadm` 来创建 MD 设备。在 RAID 1 阵列的情况下，你会输入：

```bash
$ sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
md array /dev/md0 started.
```

这里的大部分参数都是自言自明的。`--create` 选项告诉 `mdadm` 我想在 `/dev/md0` 创建一个新的 MD 设备。如果我已经在 `/dev/md0` 有了一个 RAID 阵列，我将只会选择下一个数字，例如 `/dev/md1`。`--level=1` 设置用于此阵列的 RAID 级别，`--raid-devices` 设置活动设备的数量，最后指定你想要用于阵列的每个分区。

如果我想在 `/dev/sdb1`、`/dev/sdc1` 和 `/dev/sdd1` 上设置 RAID 5 阵列，我会输入：

```bash
$ sudo mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdb1 /dev/sdc1 /dev/sdd1
array /dev/md0 started.
```

一旦我创建了阵列，我可以在 `/proc/mdstat` 中检查当前的健康状况：

```
Personalities : [raid6] [raid5] [raid4]
md0 : active raid5 sdd1[2] sdc1[0]
167/1584 blocks level 5, 64k chunk, algorithm 2 [3/3] [UUU]
unused devices: <none>
```

现在我可以像创建任何分区一样创建 `/dev/md0`，用我选择的文件系统对其进行格式化，并挂载它：

```bash
$ sudo mkfs -t ext3 /dev/md0
$ sudo mkdir /mnt/storage
$ sudo mount /dev/md0 /mnt/storage
```

现在这个阵列已经启动并正常运行；但是，它还没有设置为在引导启动时自动启动并挂载。如果不设置此项，你每次启动系统都必须运行 `mdadm` 命令来组装阵列并运行挂载命令。要在启动时启动阵列，你需要配置 `/etc/mdadm/mdadm.conf` 并包含有关你阵列的详细信息。你完全可以手动这样做，但 `mdadm` 提供了一种更简单的方法。`mdadm --detail` 命令将为每个阵列输出一个与 `mdadm.conf` 兼容的字符串，因此你只需要重定向剩余分区即可。确定 `/etc/mdadm/mdadm.conf` 文件：

```bash
$ sudo sh -c 'mdadm --detail --scan >> /etc/mdadm/mdadm.conf'
```

现在编辑你的 `/etc/fstab` 并为 `/dev/md0` 添加条目，就像它是任何其他挂载点一样。在我的情况下，我会添加：

```
/dev/md0 /mnt/storage ext3 defaults 0 0
```

或者，你可以通过以下命令指定 UUID：

```bash
$ sudo blkid /dev/md0
```

现在你可以将旧硬盘更换为新硬盘并对其进行分区。请确保你用于创建新分区的硬盘，其大小大于或等于 RAID 阵列中其他分区的大小。一旦新分区准备就绪，使用 `--add` 命令将其添加到阵列：

```
$ sudo mdadm /dev/md0 --add /dev/sd1
```

现在 `mdadm` 将开始数据重同步过程。这可能需要一些时间，取决于你磁盘的读和大小。你可以通过 `/proc/mdstat` 监控同步进度：

```
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
md0 : active sda(1) sdb(1) sdc(1)
16777184 blocks level 5, 6k chunk, algorithm 2 [3/2] [.]
[......] recovery 2.0% (170112/8385792)
finish=1.6min speed=8056K/sec
```

unused devices: <none>

除了这些基本的 RAID 管理之外，你还可以对 RAID 阵列进行许多不同的调整和自定义，特别是在创建它们时。要查看完整的选项和设置列表，请参考 `mdadm` 手册 (`man mdadm`)。

## 将非 RAID 迁移到软件 RAID

如果你在构建系统时没有考虑到 RAID，你可能会发现自己处于想要将单盘系统迁移到软件 RAID 的情况。我曾遇到过这种情况：我有一个 RAID 1 阵列，想将其迁移到 RAID 5 以增加存储空间。在本节中，我将讨论如何执行这两种迁移，以及如何向 RAID 5 添加磁盘。

在示例中，我将假设已经在 `/dev/sda` 上安装了系统。这是一个基础的 Ubuntu 安装，根分区位于 `/dev/sda`，交换分区位于 `/dev/sda5`。我已经在系统上添加了第二块磁盘 `/dev/sdb1`，并且我想为根分区和交换分区都创建一个 RAID 1 阵列。在执行任何额外步骤之前，我想确保服务器上安装了 `mdadm` 软件包，因此我运行：

```
$ sudo apt-get install mdadm
```

由于我需要能够将旧系统的所有文件复制到新的 RAID 阵列，因此我无法在运行中的系统中执行所有这些步骤。相反，我需要某种启动 CD 或救援光盘，以便确保没有分区被写入。Ubuntu 服务器安装 CD 适用于此；只需启动它并选择“救援损坏的系统 (Rescue a broken system)”选项。在回答完基本的键盘和布局问题后，你将进入一个带有几个恢复选项的菜单。在这里选择“在安装程序环境中执行 (Execute in the installer environment)”。

进入安装程序环境后，第一步是使用 `fdisk` 对 `/dev/sdb` 进行分区，并至少创建一个与 `/dev/sda` 大小相同或更大的 `/dev/sdb1`。如果硬盘大小相同，操作会更简单，因为你只需要重新创建 `/dev/sda` 上的分区（包括交换分区）。在创建分区时，请记住将分区类型设为 `fd`。

> 注意：此示例适用于 RAID 1 阵列，但如果你想从单盘迁移到 RAID 5 阵列，请记住 GRUB 无法从 RAID 5 阵列读取，因此你必须创建一个独立的 `/boot` 分区并让它不参与 RAID，或者为它创建一个 RAID 1 阵列。

分区创建完成后，你就可以准备创建阵列了。由于我们目前在系统在使用 `/dev/sda1` 和 `/dev/sdb`，我们以降级模式（degraded mode）创建阵列，对其格式化，将所有数据复制到新的 RAID 阵列，从降级模式启动阵列，最后热添加原始分区。这样，我们在每一步中都拥有数据的安全副本。降级阵列的创建与普通阵列类似，只是在缺失硬盘的地方使用 `missing` 关键字：

```
# mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 missing
mdadm: array /dev/md0 started
# mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/sdb5 missing
mdadm: array /dev/md1 started
```

## 第 10 章：容错性

分区创建完成后，现在用 ext4 格式化 `/dev/md0`，用交换系统格式化 `/dev/md1`：

```
# mkfs.ext4 /dev/md0
# mkswap /dev/md1
```

现在你可以为 `/dev/md0` 创建一个临时挂载点，并将根分区的所有文件迁移到这个新分区。Ubuntu 救援模式默认会将根分区挂载在 `/target` 下，但如果你使用了其他救援光盘，或者需要将分区迁移到多个阵列，你将必须单独挂载这些分区。遗憾的是，Ubuntu 服务器救援模式不包含 `cpio` 等工具，即使 `find` 的版本也不全全，因此我使用服务器根分区的 `find` 命令：

```
# mkdir /mnt/temp
# mount /dev/md0 /mnt/temp
# cd /target
# ./usr/bin/find -xdev -print | cpio -padmvd /mnt/temp
```

当然，如果你将根分区挂载在 `/target` 以外的地方，请切换到该目录。此命令的运行可能需要一些时间，因为它需要从系统复制所有文件。现在系统已经迁移到 `/dev/md0`，你需要设置阵列在启动时自动加载。首先，我们将阵列添加到 `/etc/mdadm/mdadm.conf`（即 `/dev/md0` 挂载所在），然后更新其 initramfs，以便在启动时创建这些设备：

```
# mdadm --detail --scan >> /mnt/temp/etc/mdadm/mdadm.conf
# chroot /mnt/temp update-initramfs -2.6.32-19-generic
initramfs: Generating /boot/initrd.img-2.6.32-19-generic
```

确保更改 `update-initramfs` 参数指向你的 initrd 文件（检查 `/mnt/temp/boot/`）。接下来，我需要编辑 RAID 阵列中的 `/etc/fstab` 文件，使其指向 RAID 阵列而不是 `/dev/sda` 上的分区。由于我们在救援光盘上的工具有限，这意味着需要使用 `nano` 编辑器。首先编辑 `/mnt/temp/etc/fstab`...

# RAID 351

`sudo grub-install /dev/sdb`。如果你的第二个 RAID 设备不同，请将 `/dev/sdb` 更改为相应的设备路径。如果你有第三个 RAID 设备，请也为该设备运行 `grub-install`。

最后一步是在 `/dev/sda` 上使用分区工具，并将两个分区的分区类型都设置为 `fd`，这样它们会被自动识别为 RAID 设备。最后重启一次系统，以确保它能够从你的 RAID 阵列启动。现在，你的系统已具备容错能力并准备可以使用。

## 从 RAID 1 迁移到 RAID 5

在某个时刻，你可能决定某个系统需要从 RAID 1 扩展到 RAID 5。大多数情况下，这是因为 RAID 阵列需要更多存储空间。如果你增加额外的硬盘并迁移到 RAID 5，你可以在保持冗余的同时将可用存储空间翻倍。

在这个示例中，我将我上面提到的 RAID 1 系统迁移到 RAID 5 系统。目前它有两个 RAID 阵列：由 `/dev/sda1` 和 `/dev/sdb1` 组成的 `/dev/md0`（用于 `/` 分区），以及由 `/dev/sda5` 和 `/dev/sdb5` 组成的 `/dev/md1`。我将使用第三块硬盘 `/dev/sdc`，并将系统迁移到 RAID 5 阵列。

当你的根分区位于 RAID 5 上时，有一些特殊考虑，因为 GRUB 无法直接从其启动。你需要设置一个不是 RAID 5 的小型 `/boot` 分区供 GRUB 启动。在这里仍然拥有容错能力；你必须将 `/boot` 分区设置为 RAID 1。

就像我从单硬盘迁移到 RAID 1 一样，为了迁移到 RAID 5 阵列，我需要使用救援盘。在这种情况下请使用 Ubuntu Server 救援模式，从 Ubuntu Server 安装光盘启动并在启动菜单中选择“修复损坏的系统（Rescue a broken system）”。当你进入选择根文件系统的部分时，务必选择正确的 MD 设备（在我的情况下为 `/dev/md0`）。在主操作菜单中选择“在安装程序环境中执行 shell（Execute a shell in the installer environment）”。

这种迁移的通用步骤与将单盘迁移到 RAID 1 非常相似。我们按照希望的新阵列布局对 `/dev/sdc` 进行分区，从两个 RAID 1 阵列中移除 `/dev/sdb`，对其重新分区，然后创建

# 第 10 章 ● 容错

我们的降降级 RAID 阵列，并设置它们以便系统可以从它们启动。一旦我们成功从新阵列启动，就会销毁旧阵列，对最后一块硬盘进行重新分区并对其进行热添加。

因此，我对 `/dev/sdc` 进行分区。我在 `/dev/sdc1` 上创建了一个 100MB 的 `/boot` 分区，然后用剩余空间创建根分区和交换分区。由于 RAID 5 阵列无论如何都会更大，所以我不需要担心没有从根分区中扣除 100MB。记得将每个分区创建为类型 `fd`。我的最终磁盘看起来如下：

| 设备 (Device) | 结束 (End) | 块 (Blocks) | Id | 系统 (System) |
| :--- | :--- | :--- | :--- | :--- |
| `/dev/sdc1` | 1 | 104391 | fd | Linux 自动检测 |
| `/dev/sdc2` | 14 | 1033893150 | fd | Linux 自动检测 |
| `/dev/sdc3` | 13 | 104488357* | 5 | 扩展 |
| `/dev/sdc5` | 14 | 104488326 | fd | Linux 自动检测 |

现在我使用 `mdadm` 从 RAID 阵列中移除 `/dev/sdb` 分区：

```
# mdadm /dev/md0 --fail /dev/sdb1
# mdadm: 在 /dev/md0 中设置 /dev/sdb1 为故障
# mdadm /dev/md0 --remove /dev/sdb1
# mdadm /dev/md1 --fail /dev/sdb5
# mdadm: 在 /dev/md1 中设置 /dev/sdb5 为故障
# mdadm /dev/md1 --remove /dev/sdb5
```

现在我使用 `mdadm` 从 RAID 阵列中移除

修改 `/dev/sdb` 的分区表，使其与 `/dev/sdc` 一致，然后创建

我们的降级 RAID 阵列，并设置它们以便系统可以从它们启动。一旦我们成功从新阵列启动，就会销毁旧阵列，对最后一块硬盘进行重新分区并对其进行热添加。

现在，我使用 `mdadm` 从 RAID 阵列中移除 `/dev/sdb` 分区：
