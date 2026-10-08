
# 表 30-10：Linux 分区与文件系统工具

| 工具 | 描述 |
|---|---|
| fdisk | 用于创建和删除分区的菜单程序。 |
| cfdisk | `fdisk` 的图形界面。 |
| parted | GNU 分区管理工具。 |
| mkfs | 在分区或软磁盘上创建文件系统。格式化工具的前端。 |
| mke2fs | 在分区上创建 ext2 文件系统；使用 `-j` 选项创建 ext3。 |
| mkfs.ext3 | 在分区上创建 ext3 文件系统。 |
| mkfs.ext2 | 在分区上创建 ext2 文件系统。 |
| mkfs.reiserfs | 在分区上创建 Reiser 日志文件系统（链接 `mkreiserfs`）。 |
| mkfs.jfs | 在分区上创建 JFS 日志文件系统。 |
| mkfs.dos | 在给定分区上创建 DOS 文件系统。 |
| mkfs.vfat | 在给定分区上创建 Windows 16 位文件系统（FAT32）。 |
| mkswap | 在设备或文件中设置交换区的工具。 |
| mkdosfs | Linux 下创建 MS-DOS 文件系统。 |
| mkisofs | 创建 ISO CD-ROM 磁盘镜像。 |
| Gfloppy | GNOME 格式化软磁盘工具（系统工具菜单上的软磁盘格式化器）。 |

分区有不同的类型需要你指定。`Linux fdisk` 是一个命令行程序。它有一组单字符命令，你只需按下即可。然后可能会提示你输入某些信息并按回车。如果在 `fdisk` 过程中遇到问题，可以随时按 `Q`，这将返回上一个界面且不进行任何更改。只有按下 `W` 时，更改才会应用到硬盘上。这会退出 `fdisk` 并返回安装程序。表 30-11 列出了常用的 `fdisk` 命令。执行以下步骤创建 Linux 分区。

# 表 30-11：常用的 fdisk 命令

| 命令 | 动作 |
|---|---|
| a | 切换可引导标记 |
| l | 列出已知的分区类型 |
| m | 列出命令 |
| n | 添加新分区 |
| p | 打印分区表 |
| q | 不保存更改并退出 |
| t | 修改分区的系统 ID |
| w | 写入磁盘并退出 |

当你按下 `N` 定义一个新分区时，系统会询问它是否为主分区。按下 `P` 表示它是一个主分区。Linux 支持多四个分区。输入你正在创建的分区的分区号。输入该分区的磁道数，这是提示符末尾括号中的第一个数字。随后系统会提示你输入最后一个磁道。你可以输入分区的结束磁道，也可以退出。你可以通过在数量前加上 `+` 号将实体大小设置为 `+100M`（代表 1GB）。请记住，大小不能超过你的空闲空间。如果你要指定分区类型，Linux 分区的默认类型为 83。如果你正在创建不同类型的分区（例如交换分区），按下 `T` 指明你需要的类型。输入分区编号，例如交换分区为 82。完成后，按下 `W` 将更改写入硬盘，然后按 `ENTER` 继续。

## parted

作为 **`fdisk`** 的替代方案，你可以使用 **`parted`** (`www.gnu.org/software/parted`)。**`parted`** 让你管理硬盘分区、创建新分区并删除旧分区。与 **`fdisk`** 不同，它还可以调整分区大小。若要在给定硬盘的分区上使用 **`parted`**，你必须以救援模式启动系统，并选择不挂载系统文件。对于未与内核位于同一块硬盘上的其他硬盘，你只需要限制分区并使用 **`swapoff`** 关闭交换空间。然后，你可以通过 **`parted`** 命令和要操作的硬盘设备名称来启动 **`parted`**。以下示例为硬盘 **`/dev/hda`** 启动 **`parted`**。

`/dev/hda`

你使用 **`print`** 命令列出所有分区。每个分区的分区编号将列在 Minor Header（次要头）下的第一列。**`Start`**（起始）和 **`End`**（结束）列列出了使用硬盘的分区的起始和结束位置。这些数字单位是兆字节，从第一个兆字节到总可用容量。要创建一个新分区，请使用 **`mkpart`** 命令并指定 **`primary`**（主）或 **`extended`**（扩展）、文件系统类型以及起始和结束位置。你可以创建最多三个主分区和一个扩展分区（如果没有扩展分区，则可以创建四个主分区）。每个扩展分区可以包含多个逻辑分区。一旦创建了分区，你可以使用 **`mkfs`** 使用文件系统对其进行格式化。要删除分区，请使用 **`rm`** 命令和分区号。要 **`resize`**（调整大小）分区，使用 `resize` 命令、分区号以及起始和结束位置。你可以使用 **`move`** 命令移动分区。**`help`** 命令列出所有命令。

## mkfs

一旦创建了分区，你就必须在上面创建一个文件系统。要实现这一点，使用 **`mkfs`** 命令构建 Linux 文件系统。表 30-12 列出了 `mkfs` 命令的选项。例如，第一块硬盘上的第二个分区设备名称为 `/dev/hdb1`。你现在可以挂载新的磁盘分区，将其附加到文件结构中。下一个示例格式化该分区：

```bash
# mkfs -t ext3 /dev/hdb1
```

`mkfs` 命令实际上只是几个文件系统构建器的前端。文件系统构建器执行创建文件系统的实际任务。红帽支持各种文件系统构建器，包括日志文件系统和 Windows 文件系统。文件系统构建器的名称具有 `mkfs` 前缀和代表文件系统类型的后缀。例如，ext3 文件系统的文件系统构建器是 `mkfs.reiserfs`，而对于 Windows-16 位文件系统（95, 98, ME），它是 `mkfs.vfat`。这些构建器中的某些只是 `mk2fs` ext2 文件系统创建工具的另一种名称，以及 `mkfs` 执行的每个操作的别名。例如，`mkfs.ext2` 构建器只是 `mk2fs` 工具的另一个名称。由于 ext3 是 ext2 的扩展，`mkfs.ext3` 简单地调用了 `mk2fs`（创建 ext2 和 ext3 文件系统的工具）并指向创建 ext3 文件系统（使用 `-j` 选项）。选项列在设备名称之前。任何文件构建器都可以直接用于创建该类型的文件系统。`hdb1` 设备上的 ext3 文件系统：
`mkfs.ext3 /dev/hdb1`

### 表 30-12：Mkfs 选项

| 选项 | 描述 |
|---|---|
| Blocks | 文件系统的块数。1.44MB 软盘有 1440 个块。 |
| `-t file-system-type` | 指定要格式化的文件系统类型。默认是标准的 Linux 文件系统类型 ext3。 |
| file-system-options | 所指定文件系统类型的选项。列在设备名称之前，文件系统类型之后。 |
| `-V` | 详细模式。显示 `mkfs` 执行的每个操作的描述。 |
| `-v` | 指示 `mkfs` 调用的文件系统构建器程序显示其所采取的操作。 |
| `-c` | 在格式化之前检查分区的坏块（检查块）。 |
| `-l` | 在格式化之前检查分区的坏块。 |
| `-T` | 在格式化之前检查分区的坏块（检查块）。 |

`hdb1` 设备上的 ext3 文件系统：
`mkfs.ext3 /dev/hdb1`

也可以切换到该目录并使用 `-o` 来指定目标目录。

如果你在 Linux 上创建一个简单的 CD，你会使用 `mkisofs` 来创建 CD 镜像。这里 `-V` 选项将显示创建过程，而 `-V` 选项用于指定 CD 标签。使用位于 `newscd` 目录中的文件创建一个名为 `songs.iso` 的 CD 镜像：

```
mkisofs -v "Goodsongs" -o songs.iso
```

如果你也想在 Windows 上使用，你会使用 `-r`（标准 RockRidge 支持）和 `-J`（Joliet）选项：

```
mkisofs -v r -J -V "Goodsongs" -o meriso.iso
```

如果你使用的文件名不符合 ISO 标准（例如超过 31 个字符或使用小写字母），你需要包含某些选项。`-U` 选项允许你选择完全不受限制的文件名，而像 `-L` 这样的某些选项则会限制特定内容。以下示例使用 `mdoc` 目录中的文件创建一个名为 `mydoc` 的 CD 镜像，并将 CD 标记为 "doc"：

```
mkisofs -v r -T -J -U "Greatdocs" -o mydocuments.iso
```

## 挂载磁盘镜像

一旦创建了 CD，可以通过将其挂载为 Linux 系统上的文件系统来检查其正确性。为了测试 CD 镜像，必须将其挂载到 loop 设备并像访问文件一样访问它。挂载 CD 镜像需要使用 loop 设备。按照下一个示例指定 loop 设备。`mydoc.iso` 被挂载到 `/mnt/cdrom` 目录，类型为 iso9660 文件系统。完成后请卸载它。

```
mount -t iso9660 -o loop=/dev/loop0 mydocuments.iso /mnt/cdrom
```

## 可引导 CD-ROM

如果你正在创建一个可引导 CD-ROM，你需要使用 `-e` 选项指定引导文件，并通过 `-b` 选项指定引导镜像。引导镜像是一个用于启动安装程序的引导盘。例如，在 Red Hat CD-ROM 上，引导镜是 `isolux/isolux.bin`，引导目录是 `isolux/boot.cat`（你也可以使用 `/boot.img` 和 `boot.cat`）。将这些文件拷贝到硬盘上。以下示例使用 CD-ROM 驱动器上的 Red Hat 发行版文件创建一个可引导 CD-ROM：

```
mkisofs -o dr8-0.iso -b isolinux/isolux.bin -c isolinux/boot.cat \
-no-emul-boot-load-size 4 -boot-info-table \
-v -r -R -T -J "Red8.0" /mnt/cdrom
```

## cdrecord 和 dvdrecord

一旦创建了 CD 镜像，你可以使用 `cdrecord` 或 `dvdrecord` 写入 CD 盘。如果你有多个 CD 刻录设备，应通过指定 SCSI 总线号来指定 CD-R/RW 驱动器（记住在 Linux 上即使是 IDE CD-R/RW 驱动器也被视为设备）。你可以使用 `cdrecord` 配合 `-scansbus` 选项。如示例所示，通过 `-scansbus` 选项，可写 CD-RW 驱动器的设备号为 0,0。`dev` 选项用于指定 DVD-R 刻录机，它是 `cdrecord` 的一个扩展。`cdrecord` 的最后一个参数是 CD 镜像文件名。`dvdrecord` 如：

```
cdrecord dev=0,0 mydocuments.iso
```

如果你正在创建一个音频 CD，使用此处所示的 `-audio` 选项。该选项使用 CD-DA 音频格式：

```
cdrecord dev=/0,0 -audio morengos.iso
```

类似的操作也适用于 `dvdrecord`，只是 `dvdrecord` 会写入 DVD 刻录机上的 DVD-R 光。`cdrecord` 版本的 `dummy` 选项用于测试指定镜像的 CD 写入操作。

### dvd+rw 工具

主要的 `dvd+rw` 工具是 `growisofs`，通过它可以创建 DVD+RW/R 光盘。还包含两个辅助工具：格式化工具 `dvd-rw-format` 和兼容性工具 `dvd-rw-booktype`。详细说明请参见 `/usr/share/doc` 中的 `dvd+rw-tools` 页面。

`growisofs` 工具使用了 `mkisofs` 工具，但它直接写入 DVD+RW/R 光盘而不是镜像。它与 `mkisofs` 名字相同（有少数例外），并且它允许 `mkisofs` 命令有一个友好的结束。它它没有用于指定磁盘镜像的 `-o` 选项，取而代之的是指定 DVD 设备。例如，要将 `news` 目录的内容写入 DVD+RW 光盘，你可以直接使用 `growisofs`：

```
growisofs -v "Goodsongs" -Z /dev/scd0 newsongs
```
