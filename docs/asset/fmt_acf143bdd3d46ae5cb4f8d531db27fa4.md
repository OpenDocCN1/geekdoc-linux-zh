
串口端口和拨出设备。对于每个设备 `tty0`，还有一个设备 `cuax`，用于拨出。这在简单情况下可以避免对协作锁的需求。

`cyclades`

用于 cyclists I/O 串行的拨入和拨出设备。

# 第八部分：管理与特权命令

## 杂项

通用 SCSI 设备。通过 `sg7` 访问设备。这些设备允许向任何 SCSI 设备发送任意命令。这允许查询设备，或控制不在磁盘、磁带或 CD-ROM 上的 SCSI 设备（例如，扫描仪或可写 CD-ROM）。

若要允许任意程序从文件描述符 `x` 读取输入，请使用 `/dev/fd/x` 作为文件名。这还会创建 `8/dev/stdin`、`8/dev/stdout` 和 `8/dev/stderr`。（注意，这些只是指向 `/proc/self/` 的软链接）。

IBS2 仿真所需的设备（和符号）。

用于电源管理的设备。

DCF-77 无线时钟驱动。

内核模块设备演示。参见模块源码。

Linux 曾经在 `/dev` 中用于控制网络设备，但现在不再这样了。要查看内核已知的网络设备，请查看 `/proc/net/dev`。

### 参见

Linux 分配设备，由 H. Peter Anvin (`Peter.Anvin@linux.org`) 维护。

### 作者

Nick Holloway

Linux，8月14日

# mke2fs

`mke2fs`—创建一个 Linux 扩展文件系统。

## 语法

```
mke2fs [-c ] [-l ] [-b block-size ] [-f fragment-size]
[- i bytes-per-inode ] [-m reserved-blocks-percentage ] [- q ] [-v] [-S]
device [ blocks-count ]
```

## 描述

`mke2fs` 用于在设备（通常是磁盘分区）上创建 Linux 扩展文件系统。`device` 是对应设备的特殊文件，例如 `/dev/hdX`。`blocks-count` 是设备上的块数。如果省略，`mke2fs` 将自动创建文件系统的大小。

## 选项

- `-b block-size` 指定以字节为单位的块大小。
- `-c` 在创建文件系统之前，使用只读测试检查设备是否存在坏块。
- `-f fragment-size` 指定以字节为单位的碎片块大小。
- `-i bytes-per-inode` 指定每个 inode 的字节数。`mke2fs` 为磁盘上每隔 `bytes-per-inode` 字节的空间创建一个 inode。此值默认为 4096 字节。`bytes-per-inode` 必须至少 124。
- `-l filename` 读取 `filename` 中的坏块。
- `-m reserved-blocks-percentage` 指定为超级用户保留的块百分比。此值默认为 5%。
- `-q` 静默执行。如果 `mke2fs` 位于脚本中则非常有用。
- `-v` 详细执行。

只写入超级块和组描述符。这在所有超级块和备份超级块都损坏且需要最后的恢复方法时非常有用。它会导致 `mk2fs` 重新初始化超级块和组描述符，而不触碰 inode 表和 inode 位图。在使用此选项后应立即运行 `e2fs` 程序，且无法保证任何数据可以被救。

### 作者

此版本的 `mk2fs` 由 Theodore Tso (`tytsso@mit.edu`) 编写。

### 缺陷

`mk2fs` 接受 `-f` 选项，但目前忽略了它，因为第二个扩展文件系统不支持碎片。可能存在其他缺陷。请向作者报告。

## 可用性

`mke2fs` 可以从 `ftp.lib.fr` 和 `tsx-11.mit.in` 的 `/pub/linux/packages/ext2fs` 通过匿名 FTP 获取。

### 参见

`badblocks(8)`, `dumpefs(8)`, `e2fsck(8)`, `tune2fs(8)`

版本 0.5b，1994年11月

# mk2fs

`mk2fs`—构建 Linux 文件系统。

## 语法

```
mk2fs [ -V ][ -t filesystem ][ -fs-options ] filesystem [ blocks ]
```

## 描述

`mk2fs` 用于在设备（通常是磁盘分区）上构建 Linux 文件系统。`filesystem` 是设备名（如 `/dev/sda1`、`/dev/sdb2`）或文件系统的挂载点（如 `/`、`/home`）。`blocks` 是用于文件系统的块数。

`mk2fs` 返回的退出码：成功为 0，失败为 1。

实际上，`mk2fs` 是 Linux 下各种文件系统构建器（`mk2fs.filesystem`）的前端。特定文件系统的构建器首先在 `/etc/fstab` 中查找，然后是 `/etc`，最后在 `PATH` 环境变量列出的目录中查找。参见特定文件系统的手册。

## 选项

- `-v` 输出详细信息，执行所有特定文件系统的命令。多次指定此选项将抑制特定文件系统命令的执行。
- `-t` 指定构建的文件系统类型。如果未指定，将通过搜索 `/etc/fstab` 中的项来检测类型。如果无法解析类型，则使用默认文件系统类型（`minext`）。
- `-fs-options` 传递给实际文件系统构建器的文件系统特定选项。大多数文件系统构建器支持以下选项：
  - `-c` 在构建文件系统之前检查设备的坏块。
  - `-l` 从 `filename` 读取坏块列表。
  - `-v` 输出详细信息。

# 第八部分：管理与特权命令

## 缺陷

通用选项位于文件系统特定选项之前。某些文件系统程序不支持返回有意义的 `-v`（详细）码。此外，某些文件系统程序不自动检测大小并要求指定。

### 作者

David Engel (`david@dods.com`), Fred N. Kemp (`waltje@uwalt.org`), 以及 Ron Sommeling (`sommel@kun.nl`)。该手册改编自 Remy Card 的 ext2 文件系统版本。

### 参见

`fsck(8)`, `mkfs.minix(8)`, `mkfs.ext(8)`, `mkfs.ext2(8)`, `mkfs.xafs(8)`

版本 1.9，1995年6月

# mkfs

`mkfs`—制作 Linux MINIX 文件系统。

## 语法

```
mkfs [ -c ] [ -namelen [ - inodecount ] device size-in-blocks
mkfs [ -l filename ] device size-in-blocks
```

## 描述

`mkfs` 在设备（通常是分区）上创建 Linux MINIX 文件系统。

设备通常为：

```
/dev/hda[1-8]
/dev/hdb[1-8]
/dev/sda[1-8]
/dev/sdb[1-8]
```

`size-in-blocks` 参数是以块计算的文件系统大小。此信息可以通过 `fdisk(8)` 程序确定。允许大于大于10 且小于 65536 的块。

## 选项

- `-c` 在创建文件系统之前检查设备的坏块。如果有，则打印计数。
- `-n` 指定文件名的长度。`-n` 和 `namelen` 之间不允许空格。允许的值为 14，默认为 30。
- `-inodecount` 指定文件系统的 inode 数量。
- `-l filename` 从 `filename` 读取坏块列表。文件每行一个坏块号。打印读取的坏块计数。

## 退出码

`mkfs.minix` 返回的退出码之一：

- `0` 无错误
- `8` 操作错误
- `16` 用法或语法错误

### 参见

`fsck(8)`, `mkfs(8)`, `reboot(8)`

### 作者

Linus Torvalds (`torvalds@cs.helsinki.fi`)。错误代码值由 Rik Faith (`faith@cs.unc.edu`)。inode 请求功能由 Scott Heavner (`sdpo@cwru.com`)。文件系统有效标志支持 Dr. Wettstein (`greg@wind.uocpl`)。

Daniel Quinlan (`quinlan@yggrasil.com`) 检查以防止对挂载的文件系统执行 `mkfs`。

Linux 0.99，1994年1月

# mklost+found

`mklost+found`—在挂载的扩展文件系统创建 lost+found 目录。

## 语法

`mklost+found`

## 描述

`mklost+found` 用于在 Linux 第二扩展文件系统的当前目录中创建 `lost+found` 目录。`mklost+found` 为该目录预分配磁盘块，使其可被 `e2fsck` 使用。

## 选项

无。

### 作者

`mklost+found` 由 Remy Card (`card@mas.ibp.fr`) 编写，他是 ext 2 fs 的开发者和维护者。

### 缺陷

无。

## 可用性

`mklost+found` 可以从 `ftp.ibp.fr` 和 `tsx-11.mit.edu` 的 `/pub/linux/packages/ext2fs` 通过匿名 FTP 获取。

### 参见

- `e2fsck(8)`, `mke2fs(8)`

版本 0.5b，1994年11月

# mkswap
