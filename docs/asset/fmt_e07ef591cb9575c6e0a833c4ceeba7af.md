
# 3 Linux 和 FreeBSD 共享交换空间

这会导致错误的设备分配并数据丢失。我的建议是始终将 FreeBSD slice 放在任何 Linux 扩展分区之后，并在安装 FreeBSD 后不要更改任何逻辑分区！

## 3.1 安装并准备 Linux

本节描述了如何让 Linux 和 FreeBSD 共享交换分区。这基于 Red Hat Linux 4.1（Linux 内核 2.0.29 和 2.0.30）和 FreeBSD 2.2。如果你愿意，可以在 Linux 之前安装 FreeBSD，只需注意 FreeBSD slice 中分区的顺序。

第一步是正常安装 Linux。你必须为硬盘上的 FreeBSD slice 留出空间。你不需要创建 Linux 交换分区，但如果你想创建，请将其放在为 FreeBSD 分配的空间。这样以后你可以删除 Linux 交换分区并将该空间供 FreeBSD 使用。

## 3.2 Linux 和 FreeBSD 共享交换空间

当你安装了 Linux 以构建新内核时。如果这对你来说是新的，请阅读 Linux Kernel HOWTO。你必须包含 UFS 文件系统支持（只读）和 BSD disklabel（FreeBSD 分区表）支持。

```
UFS filesystem support (read only) (CONFIG_UFS_FS) [N/y/m]?

BSD disklabel (FreeBSD partition tables) support (CONFIG_BSD_DISKLABEL) [N/y]?

(NEW) y
```

安装新内核并重启。如果你创建了 Linux 交换分区，请从 `/etc/fstab` 文件删除包含 `swap` 单词的行。确保你有一个带有新内核的可运行 Linux 引导磁盘。现在你可以安装 FreeBSD 了。

### 安装 FreeBSD

按照 FreeBSD 文档所述安装 FreeBSD。删除你创建的 Linux 交换分区（你可以使用 FreeBSD 的 `fdisk` 程序）。注意 FreeBSD slice 中分区的顺序。如果你使用默认标记，第二个分区将是交换分区。完成 FreeBSD 安装并使用新的 Linux 引导磁盘重启进入 Linux。

## 3.3 在 Linux 中设置 FreeBSD 交换分区

进入 Linux 后运行 `dmesg`。在输出中你应该看到类似如下的内容：

```
Partition check:

hda: hda1 hda2 hda3 hda4 <hda5 hda6 hda7 hda8 >
```

这意味着 `/dev/hda4` 是你的 FreeBSD slice，而 `/dev/hda5`、`/dev/hda6`、`/dev/hda7` 和 `/dev/hda8` 是 FreeBSD 分区。如果你的 `swap` 是 slice 中的第二个分区，它将是 `/dev/hda6`。你必须将以下行放入 `/etc/fstab` 以启用交换分区：

```
/dev/hda6      none    swap      sw      0 0
```

虽然 FreeBSD 可以使用任何类型的交换分区，但 Linux 需要交换分区中有一个特殊的签名。该签名由 `mkswap` 创建。FreeBSD 在使用交换分区时会运行该签名，因此你每次进入 Linux 都必须运行 `mkswap`。为了自动实现这一点，请找到启动时运行交换的脚本。在 Red Linux 中是 `/etc/rc.d/sysinit`。在该文件中加入以下行：

```
awk '/swap/ && $1 { "mkswap "$1" }' /etc/fstab
```

如果 `/etc/fstab` 中的交换分区被注释掉（以 `#` 为行首），则该命令每次启动时都会对这些分区运行 `mkswap`。

可以重启进入 FreeBSD 以确保一切运行如预期。如果没有运行正常，你可能使用了错误的交换分区。解决该问题的办法是重新安装 FreeBSD 并再次尝试。经验是最好的老师。:-)

## 4 使用 LILO 启动 FreeBSD

你可以轻松地使用 LILO 启动 FreeBSD。如果你想使用 LILO，请勿安装 FreeBSD 启动加载程序（`Bootasy`）。在你的 `/etc/lilo.conf` 文件末尾添加以下行，并运行 `lilo`（假设 FreeBSD 分区位于 `/dev/hda4`）：

```
other=/dev/hda4
table=/dev/hda
label=FreeBSD
```

如果你已将 FreeBSD 安装在第二个 SCSI 驱动器上，请使用如下配置（假设 FreeBSD 分区位于 `/dev/sdb2`）：

```
other=/dev/sdb2
table=/dev/sdb
loader=/boot/chain.b
label=FreeBSD
```

## 5 在 Linux 下挂载 UFS 文件系统

### 5.1 在 Linux 下挂载 UFS 文件系统

遗憾的是，Linux 2.0.xx 内核（以及 2.1.xx 内核；但内核正在开发中）中的 UFS 驱动不支持 FreeBSD。当你尝试挂载 FreeBSD 文件系统时，只会收到一些错误信息（文件系统实际上已经挂载，但你无法从中读取任何内容）。

在 SunSite `<ftp://sunsite.edu.pub/Linux/ALPBH/afs/ufs>` 上有另一个适用于 Linux 2.0.xx 内核（xx <= 30）的 UFS 驱动版本。它被称为 `U2FS`，当前版本为 `u2fs-0.4.3.tar.gz`。一个 适用于于 Linux 2.0.31 及更高版本（2.0.xx）的 U2FS 版本（`ufs-0.4.4.tar.gz`）可以在此站点 `<http://www.math.uni-heidelberg.de/flight/projects/u2fs/>` 找到，那里还有关于 UFS（以及 UFS）的更多信息。

现在你需要编译一个支持 `U2FS` 文件系统和 BSD 磁盘标签的新内核。更多信息请参阅第 3.1 节（安装和准备 Linux）。当内核使用 `U2FS` 时，你可以省略 UFS 文件系统支持。

当你安装了新内核后，可以使用如下命令挂载你的 UFS 文件系统（FreeBSD 分区中除交换分区外的所有分区）：

```
mount -t u2fs /dev/hda8 /mnt
```

UFS 驱动是只读的。也就是说，你可以从 UFS 文件系统读取内容，但不能进行写入。

### 5.2 在 FreeBSD 下挂载 ext2fs 文件系统

要在 FreeBSD 下挂载 `ext2fs` 文件系统，你必须先编译一个支持 `ext2fs` 的内核。请阅读 FreeBSD 文档以学习如何操作。将以下行放入新内核的内核配置文件：

```
"EXT2FS"
```

当使用新内核启动后，可以通过提供如下命令挂载 `ext2fs` 系统：

```
mount -t ext2fs /dev/wd0s3 /mnt
```
