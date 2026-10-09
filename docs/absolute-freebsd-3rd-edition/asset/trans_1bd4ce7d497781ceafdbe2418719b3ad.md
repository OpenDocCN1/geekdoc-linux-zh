
交换分区（类型 *freebsd-swap*）。其他分区类型为 *freebsd-ufs*：root 为 5GB，*/tmp* 为 5GB，*/var* 为 100GB，剩余空间分配给 */usr*。我将为每个分区标记其预期用途。

使用 `gpart(8)` 创建分区。使用 `-t` 标志指定分区类型，`-s` 指定大小，`-l` 为新区分配置 GPT 标签。我们从引导分区开始。

```
# gpart add -t freebsd-boot -l boot -s 512k da3
da3p1 added
```

使用 `gpart show` 检查结果。添加 `-l` 标志以查看 GPT 标签。

```
# gpart show -l da3
=>   40 1935325088 da3 GPT (932G)
    40 1024 1 boot (512K)
  1064 1935324064 - free - (932G)
```

此磁盘有一个分区，即一个标签为 *boot* 的 512K 分区。命令执行成功。现在添加交换空间。

```
# gpart add -a 1m -t freebsd-swap -s 8g -l swap da3
da3p2 added
```

该命令与添加引导分区的命令类似：我们指定了分区类型、大小和标签。

不过，慢着——这个 `-a 1m` 是什么？`-a` 标志允许你设置分区对齐，从而可以设置分区相对于磁盘起点的开始和结束位置。回想一下本章开头我讨论过的内容，在 4K 磁盘上，如果文件系统与物理扇区未对齐可能会导致问题。`-a 1m` 告诉 `gpart` 从磁盘起点开始，在 1MB 的整数倍位置创建分区。如我们在本章第 215 页“查看分区”中看到的，分区 1 和分区 2 之间会有一些空白空间，但这是正常的。这为你留出空间，以便在必要时将该分区更改以支持 UEFI（参见本章稍后第 222 页的“统一可扩展固件接口和 GPT”）。

在创建 5GB 的 root 和 */tmp* 分区以及 100GB 的 */var* 分区时，请保留 1MB 对齐设置。

```
# gpart add -a 1m -t freebsd-ufs -s 5g -l root da3
da3p3 added
# gpart add -a 1m -t freebsd-ufs -s 5g -l tmp da3
da3p4 added
# gpart add -a 1m -t freebsd-ufs -s 100g -l var da3
da3p5 added
```

创建最后一个分区时，不要指定大小。这将告诉 `gpart` 将分区尽可能做大。

```
# gpart add -a 1m -t freebsd-ufs -l usr da3
da3p6 added
```

你已完成磁盘分区，安装准备就绪。

### 调整 GPT 分区大小

再想想，也许拥有巨大的 /usr 分区并不明智。大约 100GB 的 /usr 分区可能已包含你可能期望的所有操作系统文件空间，同时留下数百 GB 用于独立的 /home 分区。我信任我的大多数用户，但有少数人正是那种会把 /dev/random 倾倒到文件中直到耗尽所有可用空间的人。在这里，我将调整 /usr 的大小，以为 /home 腾出空间。

使用 `gpart resize` 更改分区大小。你必须知道目标分区的分区编号。运行 `gpart show da3` 可知 /usr 是分区 6。使用 `-i` 标志和分区编号来调整分区大小。

```
# gpart resize -i 6 -s 100g -a 1m da3
da3p6 resized
```

运行 `gpart show` 查看新的磁盘布局。

```
# gpart show da3
--snip--
 247465984   209715200     6  freebsd-ufs   (100G)
 457181184   1496343944     -  free    -   (714G)
```

此磁盘末尾有 714GB 空闲空间。我们现在可以创建一个宽敞的 /home，以容纳所有那些给用户带来麻烦的用户。

每个分区在磁盘上被分配了特定的扇区。如果分区两侧没有空闲空间，你就无法增加分区的大小。虽然示例磁盘在分区 6 之后有很多空闲空间，但你不能利用它来增加分区 1 到分区 5 的大小。你必须删除并重新创建这些分区。

更改分区大小不会更改该分区上文件系统的大小。缩小带有文件系统的分区会切断文件系统的一部分。增加分区大小也不会扩展文件系统。UFS 和 ZFS 都有处理分区大小增加的工具，但你必须将其作为单独的过程来处理。

## 更改标签和类型

你可以使用 `gpart modify` 命令修改 GPT 分区的类型或 GPT 标签。使用 `-i` 指定分区编号。使用 `-l` 指定新标签。这里，我更改了磁盘 vtd0 上分区 2 的 GPT 标签：

```
# gpart modify -i 2 -l rootfs vtd0
```

类似地，使用 `-t` 更改分区类型：

```
# gpart modify -i 2 -t freebsd-zfs vtd0
```

现在磁盘的 GPT 表声明分区 2 的标签为 rootfs，类型为 freebsd-zfs。

## 在旧式硬件上引导

旧式硬件期望在磁盘开头看到主引导记录（MBR），并且无法识别 GPT 分区表。FreeBSD 使用保护性 MBR（PMBR）为旧式硬件提供可识别的分区表，并帮助该硬件引导 GPT 分区磁盘。格式化为 GPT 的可引导磁盘需要保护性 MBR 和 GPT 引导加载程序两者。

使用 `gpart bootcode` 命令和 `-b` 标志安装 PMBR。FreeBSD 提供 PMBR 作为 /boot/pmbrr。

```
# gpart bootcode -b /boot/pmbrr da3
bootcode written to da3
```

此磁盘将不再困扰那些寻找 MBR 的主机。

你还需要引导加载程序。UFS 主机需要 gptboot 引导加载程序，而 ZFS 主机需要 gptzfsboot。为了方便，FreeBSD 在 /boot 目录中提供了每个引导加载程序的副本。这些副本不是磁盘上的引导加载程序，而是该版本 FreeBSD 所需的引导加载程序版本。使用 `gpart bootcode` 的 `-p` 标志安装选定的引导加载程序。使用 `-i` 选项告诉 `gpart(8)` 将引导加载程序复制到哪个分区。上一节使用的示例磁盘将分区 1 设为 freebsd-boot 类型，因此我们将使用它。

```
# gpart bootcode -p /boot/gptboot -i 1 da3
partcode written to da3p1
```

你可以将 `-p` 和 `-b` 合并为一条命令。

## 统一可扩展固件接口（UEFI）和 GPT

统一可扩展固件接口（UEFI）是一种较新的标准，用于在不使用 BIOS 模拟的情况下引导 amd64 硬件。FreeBSD 10 及更高版本早期支持通过 UEFI 引导 UFS，而 FreeBSD 11 可以通过 UEFI 引导 ZFS。

UEFI 使用类型为 efi 的分区，其大小必须至少为 800KB。使用 `gpart create` 在新磁盘上创建 efi 分区。

```
# gpart create -s gpt da0
# gpart add -t efi -s 800K da0
```

FreeBSD 将 efi 分区提供为 /boot/boot1.efifat。使用 `dd(1)` 将其复制到新的引导分区。

```
# dd if=/boot/boot1.efifat of=/dev/da0p1
```

按你的意愿对磁盘的其余部分进行分区。

efi 分区实际上是一个具有非常特定目录层次结构的 FAT 文件系统。你可以放心地挂载 boot1.efifat 文件并探索其内容。

## 扩展 GPT 磁盘

我们已经了解了如何扩展分区，那么磁盘呢？扩展磁盘在虚拟主机中很常见。扩展虚拟磁盘时，`gpart(8)` 会抱怨磁盘的 GPT 无效。GPT 和 GEOM 在磁盘的第一个和最后一个扇区中存储信息。扩展虚拟磁盘意味着添加扇区。新的最后一个扇区将是空的。使用 `gpart recover` 为最后一个扇区创建新的元数据块。

```
gpart recover vtbd0
```

现在你可以在扩展后的虚拟磁盘上创建或扩展分区。

既然你掌握了 GPT 分区，让我们看看 MBR，并了解为什么 GPT 看起来像是一个巨大的改进。

## MBR 分区方案

旧硬件，或新型但小容量的硬件，其磁盘可能需要主引导记录分区。英特尔风格的硬件几十年来一直使用 MBR 分区，数百万运行各种操作系统设备都使用它。MBR 方案仅适用于 2TB 或更小的磁盘。更大的磁盘必须使用 GPT 分区。

## 什么是主引导记录？

主引导记录（MBR）是一个占用传统磁盘前 512 字节（也称为扇区 0）的文件。MBR 包含分区信息和引导加载程序，以便 BIOS 找到操作系统。术语 MBR 可能指磁盘上的实际第一个扇区，或指该格式使用的分区方案。

主引导记录描述四个主要分区，在 BSD 社区中称为切片（slices）。每个切片描述包括包含在分区中的磁盘扇区以及该切片上预期的文件系统类型。即使磁盘只有一个切片，MBR 仍会列出四个切片，但是
