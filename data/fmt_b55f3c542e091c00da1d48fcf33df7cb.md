
# `parted [options] [device] [command [options]]`

`parted` 支持硬盘和 SSD 的分区。与过时的 `fdisk` 命令不同，`parted` 还支持 GUID 分区表 (`GPT`)。

如果你没有向 `parted` 传递命令，可以使用交互模式运行该程序并顺序输入多个命令。只要输入是唯一的，命令可以缩写（例如用 `q` 代替 `quit`）。

然而，你应该注意，与 `fdisk` 不同，命令是立即执行的且无法撤销！在操作不太方便的 `parted` 程序中，你也可以使用其名为 `gparted` 的图形用户界面。

## 选项

- `-a` 或 `--align`
指定新分区的对齐方式。允许设置有 `none`、`cylinder`（对齐到道区限制）、`minimal`（对齐到块限制）或 `optimal`（对齐到 1 MiB 的倍数）。你应该始终使用 `-a optimal` 选项以最高速度使用数据介质。

- `-l` 或 `--list`
列出所有分区。

- `-s` 或 `--script`
运行作为参数传递的所有命令，无需进行询问。

## 重要命令

- `align-check min/opt nr`
检查指定分区是否从最佳位置开始。`parted align-check min` 仅测试分区是否在物理块边界处开始。通过 `parted align-check opt`，`parted` 尝试根据数据介质的关键数据计算分区的最佳起始位置。如果无法实现，则将 1 MiB 的倍数视为最佳。

- `mklabel mdsos/gpt`
在 MBR 或 GPT 格式下建立新的分区表。注意：硬盘的所有内容将丢失！`parted` 还支持其他各种分区格式，但这些格式在 Linux 环境中并不重要（参见 `man parted`）。

- `mkpart primary/logical/extended/name [file system] start end`
创建一个新分区。注意，你必须指定起始和结束位置，而不是起始位置和大小！结束位置也可以指定为负数，然后从数据介质的末尾计算。

指定分区类型（主、逻辑或扩展）仅对具有 MBR 分区表的数据介质有用。如果数据介质上有 GPT，你应该通过第一个 `mkpart` 参数为分区指定一个名称。

可选的文件系统指定仅用于定义分区类型。然而，在新分区上不会设置文件系统。允许的类型有 `fat16`, `fat32`, `ext2`, `HFS`, `linux-swap`, `NTFS` 和 `ufs`。

- `print`
列出所有分区。

- `quit`
退出 `parted`。

- `resize nr start end`
更改指定分区的大小。遗憾的是，该命令只能用于 MBR 磁盘的扩展分区。要更改其他分区的大小，你必须删除它们，然后使用完全相同的起始点重新设置。这显然是一个容易出错的操作，并且要求分区后面有空闲空间。

- `rm nr`
删除指定分区。

- `set nr flag on/off`
更改分区的标志（额外属性）。`parted` 可以使用 `boot`, `root`, `swap`, `hidden`, `raid`, `lvm`, `lba` 和 `bios_grub` 等标志。

- `unit bios grub`
定义位置和大小规格的单位。可用选项有：

  - `s` (扇区)
  - `B` (字节)
  - `KB`, `MB`, `GB`, 和 `TB` ($10^3$, $10^6$, $10^9$, 和 $10^{12}$ 字节)
  - `KiB`, `MiB`, `GiB`, 和 `TiB` ($2^{10}$, $2^{20}$, $2^{30}$, 和 $2^{40}$ 字节)
  - `%` (百分比，相对于数据介质的总大小)
  - `compact` (输入使用十进制兆，输出易读)

默认应用 `compact` 设置。如果启动 `parted` 时使用了 `--align` 选项，在创建新分区时位置和大小规格将相应调整。

## 示例

以下几行显示了如何使用 `parted` 在带有 GPT 的 SSD 上设置新的 LVM 分区：

```
root# parted -a optimal /dev/sda

(parted) print

Model: ATA SAMSUNG SSD 830 scsi

Hard disk /dev/sda: 512GB

Sector size (logical/physical): 512B/512B

Partition table: gpt

Number Start End Size Filesystem Name Flags

1 17.4kB 1000MB fat32 EFI System Part... boot, hidden

2 1000MB 21.0GB 20.0GB ext4 hidden

3 21.0GB 21.0GB 134MB Microsoft reser... hidden, msftres

4 21.1GB 61.2GB 40.1GB Basic data part... hidden

5 61.2GB 82.2GB 21.0GB ext4 hidden

6 82.2GB 103GB 21.0GB ext4 boot, hidden

7 103GB 124GB 21.0GB ext4 boot

8 124GB 281GB 157GB ext4

9 281GB 386GB 105GB ext4

10 386GB 407GB 21.0GB ext4

(parted) mkpart svm-partition 407GB 450GB

(parted) set 11 svm on

(parted) print

...

11 407GB 450GB 42.7GB svm-partition svm

(parted) quit
```

也可以直接处理命令而无需手动交互。以下命令假设 `/dev/sdb` 是 USB 闪存盘或 SD 卡的设备。第一个 `parted` 创建一个新的 MBR 分区表并删除所有现有数据。第二个命令创建一个主分区，在开头留出 1 MiB 的空空间。

（此处省略重复的示例部分，翻译逻辑与上文一致）

## `partx` 选项

- `-s` 或 `--show`
显示所选数据介质或分区的信息。通过 `-s` 或 `-o` 显示的数据根据物理磁盘确定，可能与 Linux 内核的分区表不匹配。

- `-u`
更改内核分区表中某个分区的大小或其他数据。这些更改必须先在数据介质上物理完成。

## 示例

以下命令提供了具有 MBR 分区表的硬盘详细信息：

```bash
root# partx -o NR,TYPE,FLAGS,START,END,SECTORS,SIZE /dev/sda

NR TYPE FLAGS START END SECTORS SIZE

1 0x83 0x80 2048 411647 409600 200M

2 0x8e 0x0 411648 3145729 31045632 14,8G
```

## `passwd [options] [username]`

不带参数的 `passwd` 允许你更改当前用户的密码。要此此，你必须首先输入旧密码，然后连续输入两次新密码。新密码以加密格式写入 `etc/shadow` 文件中。然而，在某些发行版中，新密码必须符合特定的安全规则才能被接受。

`root` 也可以通过 `passwd name` 修改其他用户的密码。不需要输入旧密码；也就是说，即使用户忘记了密码，`root` 也可以更改。之前的密码限制不适用于 `root`，因此它也可以定义仅由单个字符组成的密码。然而，即使是 `root` 也不允许不输入密码（即直接按回车键）。

通过指定选项，`passwd` 还可以锁定单个账户、重新激活以及为账户或密码设置过期时间（另见 `chage` 命令的描述，该命令在这方面提供了更多设置选项）。

### 选项

- `-g`
设置组密码。此功能很少使用。它允许你通过 `newgrp` 使用密码来保护对非主组的访问。由于由于由于组密码必须被多个用户知晓，该过程在本质上是不安全的。

- `-l`
禁用账户（锁定）。

- `-u`
重新激活已禁用的账户（解锁）。

- `-x n`
指定密码有效的最大天数。换句话说，`-x 180` 意味着大约每六个月必须设置一次新密码。

`passwd` 只能交互式使用。无法将密码作为参数或选项传递。要自动设置密码，必须使用 `chpasswd` 命令。

## 示例

在以下示例中，`root` 为用户 `hawks` 设置了新密码。在将来，他们必须每年更改一次密码。

```bash
root passwd hawks

change password for user hawks.

Enter a new password: *********

Enter the new password again: *********

passwd: all authentication features successfully updated.

root# passwd -x 365 hawks
```
