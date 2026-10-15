
| 1 | 列出已知分区类型 |
| m | 列出命令 |
| n | 添加新分区 |
| p | 打印分区表 |
| q | 不保存更改退出 |
| t | 更改分区的系统 ID |
| w | 将表写入磁盘并退出 |

# 第 32 章：文件系统管理 651

数字以兆字节为单位，从第一个兆字节开始到可用总量。要创建一个新分区，使用 `mkpart` 命令指定主分区或扩展分区、文件系统类型以及起始和结束位置。你可以最多创建三个主分区和一个扩展分区（如果没有扩展分区，则可以创建四个分区）。扩展分区反过来包含多个逻辑分区。一旦创建了分区，你可以使用 `mkfs` 将其格式化为文件系统。要删除分区，请使用 `rm` 命令和分区号。要调整分区大小，请使用 `resize` 命令配合分区号以及起始和结束位置。你甚至可以使用 `move` 命令移动分区。`help` 命令列出了所有命令。

## mkfs

一旦创建了分区，你就必须在上面创建一个文件系统。要做到这一点，请使用 `mkfs` 命令构建 Linux 文件系统，并将硬盘分区的名称作为参数。你必须使用 `mkfs` 命令指定其完整路径。表 32-12 列出了 `mkfs` 命令的选项。例如，第一块硬盘设备上的第二个分区名称为 `/dev/hdb1`。你现在可以挂载硬盘分区，将其附加到你的文件结构中。下一个示例格式化了该分区：

```
# mkfs -t ext3 /dev/hdb1
```

`mkfs` 命令实际上只是几个不同文件系统构建器的前台。文件系统构建器执行创建文件系统的实际任务。Fedora Core 4 支持各种文件系统构建器，包括以 `mkfs` 为前缀并以文件系统类型为后缀的文件系统构建器。ext3 文件系统的构建器是 `mkfs.ext3`。对于 Reiser 文件系统，它是 `mkfs.reiser`，而对于 Windows 16 位文件系统（95, 98, ME），它是 `mkfs.vfat`。这些构建器中的某些仅仅只是传统文件系统创建工具的其他名称。例如，`mkfs.ext2` 文件构建器只是 `mk2fs` ext2 文件系统创建工具的另一个名称，而 `mkfs.msdos` 就是 `mkdosfs` 命令。

| 选项 | 说明 |
|---|---|
| Blocks | 文件系统的块数。1.44MB 软盘有 1,440 个块。 |
| -t file-system-type | 指定要格式化的文件系统类型。默认是标准的 Linux 文件系统类型 ext3。 |
| file-system-options | 指定的文件系统类型的选项。列在设备名称之前，文件系统之后。 |
| -V | 冗余模式。显示 `mkfs` 执行的每个操作的描述。 |
| -v | 指示 `mkfs` 调用的构建器程序显示其采取的操作。 |
| -c | 在格式化分区之前检查其坏块（这可能需要一些时间）。 |
| -1 filename | 读取坏块列表。 |

表 32-12 mkfs 选项

ext3 是 ext2 的扩展，`mkfs.ext3` 简单地调用了 `mke2fs`（创建 ext2 和 ext3 文件系统的工具），并引导其创建 ext3 文件系统（使用 `-j` 选项）。可以直接使用任何一个文件系统构建器来创建该类型的文件系统。选项列在设备名称之前。下一个示例与前一个示例等效，即在 `hdb1` 设备上创建 ext3 文件系统。

```
mkfs.ext3 /dev/hdb1
```

`mkfs` 命令的语法如下。你可以在类型之后、设备之前添加特定文件系统的选项。块大小用于不检测磁盘的文件构建器。

```
mkfs options [-t type] file-sysoptions device size
```

> 一旦你格式化了磁盘，就可以按照本早些描述的 `e2llabel` 命令对其进行标记。

相同的步骤也适用于软盘。在这种情况下，`mkfs` 命令将设备名称作为参数。它使用 ext2 文件系统（`mkfs` 的默认值），因为软盘太小，不支持日志文件系统。

```
mkfs /dev/fd0
```

> 在桌面上，你可以使用“系统工具”中列出的“软盘格式化器”来格式化你的软盘。格式化器允许你选择 MS-DOS 或 Linux 文件系统。

## mkswap

如果你想创建一个分区，请使用 `fdisk` 或 `parted` 创建分区（如果它还不存在），然后使用 `mkswap` 命令将其格式化为交换分区。除非另有说明，否则 `mkswap` 会格式化整个分区。它接受交换分区的设备名称作为参数。

```
mkswap /dev/hdb2
```

你需要在 `/etc/fstab` 文件中创建一个条目，以便在系统启动时自动挂载。

## CD-ROM 和 DVD-ROM 记录

在 Linux 上向 CD-ROM 磁盘记录数据涉及创建 CD-ROM 的 CD 镜像文件，并将该镜像写入 CD-R/RW Drive中的 CD-R 或 CD-RW 光盘。通过 `mkisofs` 命令，你可以创建一个 CD 镜像文件，然后将其写入 CD-R/RW 写设备。一旦有了 CD 镜像文件，可以使用 `ddrecord` 和 `cdwrite` 将其写入 CD-RW 设备。

## 创建磁盘镜像

最后一个参数是包含你要制作 CD 镜像文件的目录。为此，你可以指定一个目录。例如，如果你正在创建一个包含 `mydocs` 目录数据文件的 CD-ROM，你就指定该目录。该目录本身不会被包含，只包含其中的文件和子目录。你也可以将其改为目录并使用 `.` 表示当前目录。

# 654 第六部分：系统管理

使用 mydocs 目录下的文件和子目录创建一个名为 `mydocs.iso` 的 CD 镜像，并将该 CD 镜像标记标记为 "Greatdocs"：

```
mkisofs -v r -T -J -U -V "Greatdocs" -o mydocs.iso  mydocs own
```

## 挂载磁盘镜像

一旦创建了 CD 镜像，你就可以将其挂载到 Linux 系统的文件系统上，以检查其是否正确。实际上，为了测试 CD 镜像，你将其挂载到目录中，并像访问另一个文件系统一样访问它。挂载 CD 镜像需要使用循环设备（loop device）。如下例所示，使用 `loop` 选项指定设备。在此示例中，`mydocs.iso` 被挂载到 `/media/cdrom` 目录，类型为 `iso9660` 的文件系统。完成后，请务必卸载它。

```
mount -t iso9660 -o ro,loop=/dev/loop0 mydocs.iso /media/cdrom
```

## 可启动 CD-ROM

如果你正在创建一个可启动的 CD-ROM，你需要指定要使用的启动镜像文件和启动目录（boot catalog）。使用 `-c` 选项指定启动目录。使用 `-b` 选项指定启动镜像。启动镜像是一个启动磁盘，用于启动安装程序。例如，在 Fedora Core CD-ROM 上，启动镜像是 `isolinux/linux.bin`，启动目录是 `isolinux/boot.cat`（你也可以使用 `images/boot.img` 和 `boot.cat`）。将这些文件复制到你的硬盘。以下示例使用位于 CD-ROM 驱动上的 Fedora Core 4 发行文件创建一个可启动的 CD-ROM。

```
mkisofs -o rd8-0.iso -b isolinux/linux.bin -c isolinux/boot.cat \
no-emul-boot -boot-load-size 4 --boot-info-table \
-v r -R -T J -V "Fed4" /media/cdrom
```

## cdrecord

一旦 mydocs 创建了 CD 镜像文件，你就可以使用 `cdrecord` 或 `cdwrite` 将其写入 CD 光盘。如果你有多个 CD 刻录设备，应该通过指定其设备名称来确定 CD-R/RW 设备。在此示例中，设备是位于 `/dev/hdc` 的 IDE CD-R。使用 `dev=` 选项指示此驱动器。`cdrecord` 的最后一个参数是 CD 镜像文件名。`cdrecord` 在 DVD-R/RW 刻录机上的工作原理相同。

```
cdrecord dev=/dev/hdc mydocs.iso
```

在此示例中，使用了设备为 `/dev/scd0` 的 SCSI 可写 CD-RW 设备。

```
cdrecord dev=/dev/scd0 mydocs.iso
```

如果你正在创建音频 CD，请如下所示使用 `-audio` 选项。该选项使用 CD-DA 音频格式：

```
cdrecord dev=/dev/hdc -audio moresong.iso
```

提示：`cdrecord` 的 `dummy` 选项用于测试给定镜像的 CD 刻录操作。

## dvd+rw 工具
