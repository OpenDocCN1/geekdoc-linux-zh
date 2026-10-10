
## 验证磁带驱动器加载

要验证您的系统是否已加载磁带驱动器，请在启动计算机后不久输入以下命令：

```
dmesg | grep ftape
```

此操作将在最近的内核消息中搜索包含单词 `ftape` 的行。如果 `ftape` 模块已加载，您应该看到类似以下的内容：

```
ftape v4.04 24/07/00
[000] ftape-init.c (ftape_init) - installing QIC-117 floppy tape
hardware drive...
[001] ftape-init.c (ftape_init) - ftape_init @ 0x00b0060.
[002] ftape-buffer.c (add one buffer) - buffer nr #1 @ c1503914, dma area @ c02c0000.
[003] ftape-buffer.c (add one buffer) - buffer nr #2 @ c1503c44, dma area @ c0298000.
[004] ftape-buffer.c (add one buffer) - buffer nr #3 @ c50aabc, dma area @ c0328000.
[005] ftape-calibr.c (time_inb) - inb() duration: 1109 nsec.
[006] ftape-calibr.c (ftape_calibrate) - TC for `ftape_udelay()' = 310 nsec (at 20479 counts).
[007] ftape-calibr.c (ftape_calibrate) - TC for `fdc_wait()' = 2208 nsec (at 2559 counts).
```

如果模块未加载，请检查您的内核是否编译了 `ftape` 模块支持以及您的特定磁带驱动器支持。它应该可用并准备作为可加载模块包含。

在大多数情况下，`ftape` 设备可以像 SCSI 设备一样访问。主要区别在于，`ftape` 设备文件包含字母 `qft`（代表 QIK Floppy Tape），而 SCSI 磁带包含 `st`。例如，系统中第一个 SCSI 磁带的设备文件可能是 `/dev/st0`；第一个软盘磁带的设备文件很可能是 `/dev/qft0`。

所有标准的磁带和归档相关程序在两种类型的硬件上都应该运行良好。然而，在使用软盘磁带驱动器时，您可能会发现有一些额外的程序有用。这些程序可以在 Fedora 中的 `mt-st` 包中找到。`mt` 命令用于控制磁性磁带操作。`stininit` 命令可以初始化 SCSI 磁性磁带驱动器。

## 测试磁性磁带驱动器

安装了 `mt-st` 包后，您现在应该可以测试磁带驱动器了。将一盘空白磁带插入磁带驱动器，并输入以下命令：

```
$ mt -f /dev/qft0 status
$ mt -f /dev/qft0 rewind
```

第一个命令将显示磁带驱动器的状态。在第二个命令之后，您应该听到磁带旋转的声音，因为系统正在倒带。如果磁带已经倒回，这将是一个非常短暂的过程。`mt-st` 包提供的 `mt` 命令用于在磁带驱动器中扫描、倒带和弹出磁性磁带。

## 可写 CD 驱动器

另一种日益流行的备份介质是可写 CD 驱动器。与磁带相比，可写 CD 驱动器有几个优势，主要的一个是 CD 是随机访问介质。这意味着 CD 驱动器可以快速定位 CD 上的特定文件，而无需顺序扫描整个磁盘。当您需要保持经常变化的数据文件（如软件项目的源代码或法律文件草稿）的版本历史时，这非常有用。

尽管人们过去认为 CD 有很长的使用寿命，但这种信念最近受到了质疑。即使您 1984 年的 Robyn Hitchcock CD 听起来仍然很好，如果备份需要在两年或更短的时间内使用，CD 可能仍然是一个不错的选择。对于更长的时间段，磁带备份通常比可写 CD 更持久。如果您的备份用于短期存储，您可能应该考虑可重写或 CD-RW CD 驱动器。可重写 CD（与普通可写 CD 不同）可以重新格式化并用于存储新的备份。

最大的缺点是，CD 最多只能存储约 700MB 的数据。相比之下，DVD 可以存储 4.7GB 的数据（双层 CD 约为 8.5GB），许多磁带驱动器可以存储数 GB 的数据。例如，DAT DDS-3 磁带最多可容纳 24GB 的压缩数据，而 8mm AIT-2 磁带最多可容纳 100GB 的压缩数据。

## 获取可写 CD 的 cdrecord

要在 Fedora 中写入 CD，您可以使用 wodim、cdparanoia 和 genisoimage 包，这些包是默认安装的。这些包包含诸如 `cdrecord`、`devdump`、`isodump`、`isoinfo`、`isofy` 和 `readcd` 等组件。

> **注意：** 如果您想交互式地创建 CD，请使用前面介绍的 CD/DVD 创建器或 Brasher Disc Burner 应用程序（在第 7 章中介绍）。本节讨论旧的命令行工具，因为这是运行自动备份所需的内容。

## 写入 CD

因为写入 CD-R 或 CD-R 磁盘的数据一旦写入就成为永久的，所以您需要将格式化和将文件复制到磁盘作为一个步骤完成。如果先格式化，您最终会在一个无法再写入的 CD 上拥有一个空的文件系统。

> **注意：** 使用名为 `growisofs` 的命令（在本章后面介绍），您可以以不关闭会话的方式写入 CD。稍后，您可以在最终关闭 CD 之前添加更多数据，跨越多个会话。`cdrecord` 命令本身现在也支持 `-multi` 选项，这可以保持会话打开以进行进一步写入。并非所有 CD 驱动器都支持多会话写入（这需要硬件支持 CD-ROM XA 模式 2 形式 1）。

第一步是在计算机上创建 CD 文件系统的镜像文件。您使用 `mkisofs` 命令完成此操作。第二步是使用诸如 `cdrecord` 命令这样的工具将镜像刻录到 CD 或 DVD。

> **注意：** 在 Fedora 的近期版本中，`cdrecord` 命令已被 CDR Kit 项目的一个名为 `wodim` 的命令所取代（<http://cdrrkit.org>）。Fedora 和其他 Linux 发行版转向 CDR Kit 项目，是因为 `cdrecord` 的许可证更改为 Sun CDDL 许可证，该许可证被认为与 GPL 不兼容。由于 `wodim` 与 `cdrecord` 向后兼容，且该命令链接到 `cdrecord`，您仍然可以使用 `cdrecord` 命令。

作为一个例子，假设您想备份用户 mary 的主目录。您将调用 `mkisofs` 命令并传入要创建的文件系统镜像文件名称，然后是作为基础的目录：

```
$ mkisofs -R -O /var/tmp/mary.iso /home/mary
```

这在一个名为 `mary.iso` 的文件中创建 ISO9660 文件系统镜像，位于 `/var/tmp` 目录中。-`R` 选项导致使用 Linux 特定的文件所有权和长文件名。如果您的 `/var` 分区没有足够的空间存放镜像，请选择其他位置。

> **提示：** 默认情况下，`mkisofs` 在创建文件系统镜像时保留文件和目录的所有权及访问权限。这在制作备份时是合适的，但在创建软件分发 CD 时则不然。在这种情况下，请将 `-r` 选项代替 `-R` 作为 `mkisofs` 的第一个参数。这样，所有文件将存储为公开可读，并酌情设置为可执行。

如果您有 ATAPI CD 驱动器，您不再需要该驱动器的 SCSI ID 即可向其记录数据。您可以输入设备名称代替 SCSI ID（例如 `dev=/dev/cdrom`）。但是，如果您有 SCSI CD 驱动器，在将镜像文件写入 CD 之前，您必须首先发现 CD 驱动器的 SCSI 总线号、设备 ID 号和逻辑单元号（LUN）。您可以找出 CD 驱动器使用的是哪个 SCSI 设备 ID。调用带有单个参数 `-scanbus` 的 `cdrecord` 命令：

```
# cdrecord -scanbus
```

您应该看到类似以下的响应：

```
scsibus0:
  0,0,0     0) 'IcE-CBD ' 'R/W 4x4x24  ' '1.04' Removable CD-ROM
  0,0,1     1) *  
  0,0,2     2) *  
  0,0,3  3)  *
  0,0,4  4)  *
  0,0,5  5)  *
  0,0,6  6)  *
  0,0,7  7)  *
```

这告诉您 CD 驱动器使用的是 SCSI ID 零。在这种情况下，逻辑单元号应该总是零，因此您现在有了这三个数字。您将它们作为 `dev` 参数的一部分提供给 `cdrecord`。在具有可写 DVD 驱动器的系统上，您可能会看到类似于以下内容：

```
scsibus0:
  0,0,0  0)  *
  0,0,1  1)  'TSTSTCorp'  'DVD+RW  TS-H653G'  'D200'  Removable  CD-ROM
  0,0,2  2)  *
  0,0,3  3)  *
  0,0,4  4)  *
  0,0,5  5)  *
  0,0,6  6)  *
  0,0,7  7)  *
```

首先列出 SCSI 总线号；随后是 ID 号，然后是 LUN。写入第一个示例中 CD 的完整命令应该类似于以下内容：

```
# cdrecord -v speed=2 dev=0,0,0 -data /var/tmp/mary.iso
```

> **注意：** `wodim` 命令（在此例中为向后兼容称为 `cdrecord`）会警告您，`dev=0,0,0` 伪 SCSI 语法可能在未来的版本中不再受支持。

对于 ATAPI CD 驱动器，如果 CD 驱动器为 `/dev/cdrom`，您的命令行可能如下所示：

```
# cdrecord -v speed=2 dev=/dev/cdrom -data /var/tmp/mary.iso
```

命令中包含几个额外的参数。`-v` 参数告诉 `cdrecord` 向屏幕提供详细输出。`speed` 参数告诉 `cdrecord` 以什么速度记录（在此为 X2）。（您可能选择省略 `speed=2`，让 `cdrecord` 自动检测 CD 刻录机的记录速度。）`-data` 参数告诉 `cdrecord` 将 WAV 或 AU 文件作为数据刻录，而不是作为音轨。（没有该选项，这些文件类型将作为音轨刻录，而所有其他文件则作为数据刻录。）

在实际运行 `cdrecord` 之前，您可以考虑添加 `-dummy` 选项，该选项模拟 CD 刻录过程而不实际打开激光。您可以添加 `-eject` 参数，以便在完成后弹出 CD。工作时，`cdrecord` 应显示状态消息，如下所示：

```
wodim: No write mode specified.
wodim: Assuming -two mode.
wodim: Future versions of wodim may have drive dependent defaults.
```
