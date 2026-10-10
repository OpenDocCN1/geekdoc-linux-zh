
`OCR`在`/proc/mtd`中有`ppcboot`。我将保留它还是改为`ppboot`？表格有`ppboot`。日志有`ppboot`。除非`ppcboot`是特定术语，否则我将标准化为`ppboot`。“ppc”通常意味着PowerPC。这是`TQM860L`（基于PowerPC？`TQM8xxL`模块通常是PowerPC）。所以`ppcboot`可能是正确的。然而，表格说`ppboot`。我将在表格中保留`ppboot`，在`/proc/mtd`中保留`ppcboot`，按照`OCR`，或者只是更正明显的拼写错误。`inixd`->`initrd`和`jifs2`->`jffs2`是主要的。

请注意，分区位于擦除大小边界上。由于闪存芯片是按块而不是按字节擦除的，因此创建分区时必须考虑擦除块的大小。在这种情况下，擦除块的大小为`128 KB`，所有分区都按`128 KB (0x20000)`边界对齐。

某些类型的引导固件，如`RedBoot`、`AFS`和`TI AR7`，确实会在闪存本身存储关于其如何划分为单独映像或区域的信息。当适当配置时，`MTD`子系统能够解释此类信息，从而提供闪存的自动分区。

正如你所见，`MTD`分区化的概念并不像块设备上的分区那样暴露给用户空间。单个闪存芯片的独立分区在用户空间中表现为完全独立的`MTD`设备（`mtd0`, `mtd1`, 等）。

## 另一种提供 MTD 分区信息的方式

自前段时期以来，`MTD`子系统一直能够接受分区信息作为内核启动选项的一部分。`iPAQ`的`Familiar`发行版利用此功能向`iPAQ`的内核提供设备`CFI`闪存芯片的分区信息。

下面是一个启动选项行的示例，用于向内核提供与前一节中`TQM8xxL`板相同的信息（必须写成单行）：

```
mtdparts=0:256k(ppcboot),ro,768k(kernel),,1m(user),-(initrd),1:2m(cramfs),-(jffs2)
```

（注：如果`mtdparts`行中出现，更正"im"为"1m"，"jifs2"为"jffs2"？`OCR`行是`mtdparts=0:256k(ppcboot),ro,768k(kernel),,im(user),-(initrd),1:2m(cramfs),-(jffs2)`。`im`可能是`1m`。`jffs2`在`OCR`中是正确的吗？不，`OCR`在表格中有`jifs2`。`OCR`文本中的`mtdparts`行有`jffs2`? 让我们检查：`...-(jffs2)`。是的，`mtdparts`行中看起来像是`jffs2`。我将确保它是`jffs2`。）

## 所需的 /dev 条目

你需要为`MTD`字符设备创建`/dev`条目，并且可能还需要为块设备`MTD`用户模块创建条目，以访问你的`CFI`闪存设备。对于每种类型的用户模块，创建与你设备上的分区数量相同数量的条目。例如，以下命令为我的`TQM860L`板的六个分区创建根文件系统条目：

```
$ cd ${PRJROOT}/rootfs/dev
$ su -m
Password:
# for i in $(seq 0 5)
> do
> mknod mtd$i c 90 $(expr $i + 1)
> mknod mtdblock$i b 31 $i
> done
# exit
```

以下是生成的条目：

```
$ ls -al mtd*
crw-rw-rw-  1 root    root      90,   0 Aug 23 17:19 mtd0
crw-rw-rw-  1 root    root      90,   2 Aug 23 17:20 mtd1
crw-rw-rw-  1 root    root      90,   4 Aug 23 17:20 mtd2
crw-rw-rw-  1 root    root      90,   6 Aug 23 17:20 mtd3
crw-rw-rw-  1 root    root      90,   8 Aug 23 17:20 mtd4
crw-rw-rw-  1 root    root      90,  10 Aug 23 17:20 mtd5
brw-rw-rw-  1 root    root      31,   0 Aug 23 17:17 mtdblock0
brw-rw-rw-  1 root    root      31,   1 Aug 23 17:17 mtdblock1
brw-rw-rw-  1 root    root      31,   2 Aug 23 17:17 mtdblock2
brw-rw-rw-  1 root    root      31,   3 Aug 23 17:17 mtdblock3
brw-rw-rw-  1 root    root      31,   4 Aug 23 17:17 mtdblock4
brw-rw-rw-  1 root    root      31,   5 Aug 23 17:17 mtdblock5
```

（注：`OCR`中有`cfw-rw-x-`，这对字符设备`c`和权限`rwx`来说是错误的。标准是`crw-rw-rw-`或类似。`cfw`很可能是`crw`的`OCR`错误。`x`很可能是`-`。我将更正为标准的`crw-rw-rw-`和`brw-rw-rw-`。）

## 擦除

在可以写入`CFI`闪存设备之前，你需要擦除其内容。你可以使用`MTD`实用程序中的两个擦除命令之一来执行此操作：`flash_erase`和`flash_eraseall`。

例如，在更新我的控制模块上的初始`RAM`盘之前，我需要擦除"initrd"分区：

```
# eraseall /dev/mtd3
Erased 2048 Kibyte @ 0 -- 100% complete.
```

## 写入和读取

虽然像`JFFS2`这样的闪存文件系统利用其继续将擦除块中的位清除为`0`的能力，以允许透明的读写访问，但你通常不能使用用户级工具向`MTD`设备写入超过一次。这主要是因为这些工具通常希望整体替换映像，因此会希望将某些位从`0`设置为`1`，而这在擦除时是不可能的。如果你想使用原始字符`/dev`条目更新`MTD`设备或分区的内容，例如，通常必须在写入新数据之前擦除该设备或分区。

虽然可以使用传统的文件系统命令（如`cat`和`dd`）来写入原始闪存设备，但最好使用`MTD`实用程序——对于`NOR`闪存使用`flashcp`，对于`NAND`使用`nandwrite`——因为它们更适合这些任务。`flashcp`命令会在写入前擦除闪存，并在之后读回内容以验证正确编程。`nandwrite`命令会检测`NAND`闪存设备上的坏块，并适当地跳过它们。例如，为了将新的初始`RAM`盘映像写入我控制模块上的"initrd"分区，我使用以下命令：

```
# flashcp /tmp/initrd.bin /dev/mtd3
```

在这种情况下，我的目标根文件系统通过`NFS`挂载，我在目标上运行`MTD`命令。

从`CFI MTD`分区读取与从任何其他设备读取没有区别。例如，在我的控制模块上，以下命令会将引导加载程序分区的二进制映像复制到文件中：

```
# dd if=/dev/mtd0 of=/tmp/ppcboot.img
```

（注：`OCR`中有`$\ tt\ dd\ if=/dev/mtd0\ of=/tmp/ppcboot.img$`。这是垃圾。更正为标准shell命令。）

由于引导加载程序映像本身可能没有填满整个分区，因此`ppcboot.img`文件除了引导加载程序映像外可能还包含一些额外的无关数据。

## DiskOnChip

在基于`x86`的嵌入式`Linux`系统中，`DiskOnChip`设备曾经非常流行，而`MTD`子系统在很大程度上为它们提供了支持。例如，我在我的`DAQ`模块中使用了它。但必须指出，`DiskOnChip`是一种特殊的野兽，需要精通的主人。做出这种陈述的原因很快就会显而易见。

`DiskOnChip`只是一个带有用户`ASIC`的`NAND`闪存设备，该`ASIC`在硬件中执行`ECC`计算。在该`NAND`闪存上，我们使用一种称为`NFTL`的特殊"转换层"，它作为某种伪文件系统运行，用于模拟正常的硬盘。底层的原始闪存设备作为`/dev/mtdN`设备暴露，而模拟的磁盘作为`/dev/nftlX`暴露。正是这种二元性经常导致困惑。

与所有`NAND`闪存设备一样，`DiskOnChip`设备可能包含一定数量的制造缺陷，从而导致坏块。在`DiskOnChip`从工厂出货之前，会在上面写入坏块表（`BBT`）。虽然该表不是写保护的，但对于所有读写该设备的软件操作都是至关重要的。因此，`M-Systems`的`DiskOnChip`软件能够读取此表并将其存储到文件中。`Linux`应该能够保留此表，但这些工具并没有得到特别完善的测试。

在`DiskOnChip (DOC)`上安装引导加载程序并为其格式化为`NFTL`有两种方法。第一种，由于`MTD`维护者推荐它保证能保留坏块表，是最受推荐的，即使用`M-Systems`的`DOS`实用程序。第二种，允许你在`Linux`内部对你的`DOC`设备进行最大程度的控制，即使用`doc_loadbios`和`nftl_format MTD`实用程序。

`M-Systems`的`DOS DOC`工具及相关文档曾经可以从该公司的网站`http://www.m-sys.com`获取。然而，`Sandisk`收购了`M-Systems`，该网站现在重定向到母公司。我在新网站上无法找到`DiskOnChip`工具。

在尝试`DiskOnChip`时，在破坏坏块表之前保存它是有用的。你可以使用`DOS`格式化工具来做到这一点：

```
A:\>dformat /win:d000 /noformat /log:docbbt.txt

DFORMAT Version 5.1.0.25 for DOS

Copyright (C) M-Systems, 1992-2002

DiskOnChip 2000 found in 0xD0000.

32M media, 16K unit

OK
```

`dformat`命令通常用于格式化`DOC`以便在`DOS`下使用。在这种情况下，我们使用`/noformat`选项指示`dformat`不格式化该设备。此外，我们指示它将起始于段`0xD000T`的设备`BBT`记录到`docbbt.txt`文件中。`dformat`完成`BBT`检索后，请将`docbbt.txt`的副本存储在安全的地方，因为如果您在`Linux`中擦除了整个`DOC`设备，可能需要恢复它。请查阅`M-Systems`的`dformat`文档以了解如何丢失的`BBT`。

请注意，您的`DOC`设备可能没有坏块。在这种情况下，`docbbt.txt`将为空，如果完全擦除设备，您就不必担心恢复`BBT`了。

## 内核配置

要使用您的`DiskOnChip`设备，您需要启用内核对以下选项的支持：

- `MTD`支持
- 如果您希望对闪存设备进行分区，则需支持`MTD`分区
- 直接字符设备访问`MTD`设备
- `NAFT (NAND Flash Translation Layer)`支持
- `NFTL (BETA)`的写支持
- `NAND`设备支持
- `DiskOnChip 2000, Millennium 和 Millennium Plus (NAND 重新实现) (实验性)`

虽然`DiskOnChip`设备过去曾使用专用驱动，但现在我们利用通用的`NAND`闪存基础设施来支持`DiskOnChip`。甚至可以在`DiskOnChip`上使用`JFFS2`代替`NFTL`，尽管这样启动会更具挑战性。

与`CFI`闪存一样，您可以选择启用其他选项。如果将上述选项编译为模块，`DiskOnChip`支持将需要多个模块。执行`modprobe diskonchip`命令应自动加载所有必要的模块。无论它是内核的一部分还是作为模块加载，`DiskOnChip`驱动程序都会探测所有潜在的`DOC`设备内存地址。以下是我的`DAQ`模块上驱动程序输出的示例：

```
DiskOnChip found at 0xd0000
DiskOnChip 2000 responds to DWORD access
NAND device:  Manufacturer ID: 0x98,  Chip ID: 0x73 (Toshiba NAND 16MiB, 3,v 8-bit)
Found DiskOnChip NAND Media Header at 0x10000
Found DiskOnChip NAND Media Header at 0x18000
```

### PC 上的“实模式”地址通过段和偏移量组合来表示，方式如下：`segment:offset`。当偏移量为零时，通常提供段值即可。在此例中，例如，段`0xD000`起始于地址`0xD0000`，这在`dformat`的输出中有所显示。

## M-Systems DOC 驱动程序

`M-Systems`在其`Linux`工具包中提供用于`Linux`的`DOC`驱动程序。然而，该驱动不属于`GPL`，只能作为可加载的内核模块使用。分发包含此驱动编译在内的内核，或由该模块和`Linux`内核组成的任何组合或集体作品，均违反`GPL`。因此，如果您希望使用`M-Systems`驱动的内核从`DOC`启动，您需要使用初始`RAM`磁盘（`initramfs`）来加载二进制驱动，并使其与内核分开分发。此外，`MTD`邮件列表上的帖子表明，该驱动程序消耗大量系统资源，有时还会导致串口数据丢失。基于这些原因，我建议避免使用`M-Systems Linux DOC`驱动。相反，请使用此处介绍的`GPL MTD`驱动。

### 必需的 /dev 条目

为了访问您的`DOC`设备，您需要为字符设备和`NFTL MTD`用户模块创建`/dev`条目。为您的系统中所有的`DOC`设备创建相应数量的字符设备条目和`NFTL`条目集。对于每个`NFTL`集，创建您将在设备上建立的分区数量的条目。例如，对于我的`DAQ`模块，我有一个`DOC`设备，只有一个主分区。我使用以下命令创建相关条目：

```
$ cd $(PRJROOT)/rootfs/dev
$ su -m
Password:
# mknod mtd0 c 90 0
# mknod nftla b 93 0
# mknod nftla1 b 93 1
# exit
```

生成的条目如下：

```
$ ls -al mtd* nftl*
crw-------    1 root    root        90,   0 Aug 29 12:48 mtd0
crw-------    1 root    root        93,   0 Aug 29 12:48 nftla
crw-------    1 root    root        93,   1 Aug 29 12:48 nftla1
```

### 擦除

擦除`DOC`设备与其他`MTD`设备非常相似，使用`erase`和`eraseall`命令。在对`DOC`设备使用此类命令之前，请确保您已备份`BBT`，因为擦除设备将清除其中包含的`BBT`。

例如，要擦除我`DAQ`模块中的整个`DOC`设备，我使用以下命令：

```bash
# eraseall /dev/mtd
Erased 32768 Kibyte @ 0 -- 100% complete.
```

通常，只有当您想要擦除引导加载程序和设备上的当前格式时，才需要擦除`DOC`设备。例如，如果您安装了`Linux`引导加载程序并希望恢复到`M-Systems SPL`，您需要在使用`M-Systems`工具安装`M-Systems SPL`之前使用`eraseall`命令。但是，每次擦除整个设备时，都需要使用`M-Systems`工具恢复`BBT`。

## 安装引导加载程序映像

如果您的目标系统不从其`DOC`设备启动，可以跳过此步骤。否则，您需要先构建第9章中描述的引导加载程序，然后再继续。但首先，让我们看看系统如何从`DOC`启动。

在`x86`系统启动过程中，`BIOS`会扫描内存中的`BIOS`扩展。当找到此类扩展时，`BIOS`会执行它。`DOC`设备包含一个称为初始程序加载器（`IPL`）的`ROM`程序，它利用这一特性安装另一个称为次级程序加载器（`SPL`）的程序，该程序在系统启动过程中充当引导加载程序。默认情况下，`SPL`由`M-Systems`自己的固件提供。然而，要从`DOC`设备启动`Linux`，必须用能够识别`Linux`在`DOC`上使用的格式的引导加载程序替换`SPL`。我们将在第9章中讨论各种支持`DOC`的`Linux`引导加载程序。现在，让我们看看如何在`DOC`上安装我们自己的`SPL`。

以下是我在`Linux`中用于在`DOC`上安装`GRUB`引导加载程序映像`grub_firmware`的命令：

```bash
# doc_loadbios /dev/mtd0 grub firmware
Performing Flash Erase of length 16384 at offset 0
Performing Flash Erase of length 16384 at offset 16384
Performing Flash Erase of length 16384 at offset 32768
Performing Flash Erase of length 16384 at offset 49152
Performing Flash Erase of length 16384 at offset 65536
Performing Flash Erase of length 16384 at offset 81920
Writing the firmware of length 92752 at 0... Done.
```

以下是我在`DOS`中用于在`DOC`上安装`GRUB`引导加载程序映像的命令：
