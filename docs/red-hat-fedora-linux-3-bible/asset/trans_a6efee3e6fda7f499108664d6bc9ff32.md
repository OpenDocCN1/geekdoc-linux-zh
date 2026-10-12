

- **ntfs** — 这是 Windows NT 文件系统。它作为只读文件系统受支持（因此你可以挂载并从中复制文件）。虽然存在读写支持，但被认为不可靠（有人甚至称其具有危险性）。
- **affs** — 此文件系统用于 Amiga 计算机。
- **ufs** — 此文件系统在 Sun Microsystems 操作系统（即 Solaris 和 SunOS）中很流行。
- **xenix** — 此项被添加以兼容 Xenix 文件系统（早期 PC 版本的 UNIX 之一）。该系统已过时，最终可能会被移除。
- **xiafs** — 此文件系统支持比 minix 等文件系统更长的文件名和更大的 inode。
- **coherent** — 这是用于 Coherent 或 System V 文件的文件系统类型。与 xenix 文件系统类型一样，它将在未来的某个时候被移除。

## 使用 fstab 文件定义可挂载的文件系统

你本地计算机上的硬盘以及你每天使用的远程文件系统，很可能被设置为在启动 Linux 时自动挂载。关于哪些文件系统被挂载的定义包含在 `/etc/fstab` 文件中。下面是一个 `/etc/fstab` 文件的示例：

```
LABEL=/ / ext3 defaults 1 1
LABEL=/boot /boot ext3 defaults 1 2
none /dev/pts devpts gid=5,mode=620 0 0
none /dev/shm tmpfs defaults 0 0
none /proc proc defaults 0 0
none /sys sysfs defaults 0 0
LABEL=SWAP-hda2 swap swap defaults 0 0
/dev/hdc /media/cdrom_dvdrom auto noauto,user,exec,ro 0 0
/dev/hda1 /mnt/win vfat noauto 0 0
/dev/fd0 /media/floppy auto noauto,owner 0 0
```

该文件中列出的所有文件系统都会在启动时挂载，除非第四字段设置为 `noauto`。在此示例中，根（`/`）和启动（`/boot`）硬盘分区会在启动时挂载，同时还有 `/proc`、`/sys`、`/dev/shm` 和 `/dev/pts` 文件系统（这些文件系统不与特定设备关联）。软盘（`/dev/fd0`）和 CD-ROM 驱动器（`/dev/hdc`）不在启动时挂载。在 `fstab` 文件中为软盘和 CD-ROM 驱动器提供定义，以便将来可以挂载它们（如后文所述）。

我还额外添加了一行针对 `/dev/hda1` 的配置，这允许我挂载计算机上的 Windows (vfat) 分区，这样我就不必每次都启动 Windows 才能访问 Windows 分区中的文件。

> **注意：** 要访问上述描述的 Windows 分区，我必须首先创建挂载点（通过输入 `mkdir /mnt/win`）。然后，我可以通过输入（以 root 身份）`mount /mnt/win` 来选择性地进行挂载。

*fstab* 文件的每个字段中包含以下内容：

- **字段 1** — 代表文件系统的设备名称。对于不与特定设备关联的文件系统（例如 */proc* 和 */dev/pts*），此字段通常填写 *none*。注意，此字段现在可以包括 LABEL 选项。使用 LABEL，你可以指定一个通用唯一标识符 (UUID) 或卷标签，而不是设备名称。这种方法的优势在于，由于分区是通过卷名识别的，你可以将卷移动到不同的设备名称，而不需要更改 *fstab* 文件。
- **字段 2** — 文件系统中的挂载点。除非在其下方的目录树结构中另一文件系统被挂载，否则文件系统包含从挂载点开始向下延伸的所有数据。
- **字段 3** — 文件系统类型。有效的文件系统类型在本章前面“支持的文件系统”一节中有说明。
- **字段 4** — *mount* 命令的选项。在前面的示例中，*noauto* 选项阻止指定的文件系统在启动时挂载。此外，*ro* 表示以只读方式挂载文件系统（这对于 CD-ROM 驱动器是合理的）。选项之间必须用逗号分隔。关于其他支持的选项，请参见 *mount* 命令的手册页（在 *-o* 选项下）。

> **提示：** 通常，只有 root 用户才可以使用 *mount* 命令挂载文件系统。但是，要允许任何用户挂载文件系统（例如软盘上的文件系统），你可以在 */etc/fstab* 的字段 4 中添加 *user* 选项。

- **字段 5** — 此字段中的数字指示指定的文件系统是否需要转储 (dump)。数字 1 假设文件系统需要转储。数字 2 假设文件系统不需要转储。
- **字段 6** — 此字段中的数字指示指定的文件系统是否需要用 *fsck* 检查。数字 1 假设文件系统需要检查。数字 2 假设文件系统不需要检查。

如果你想添加额外的本地磁盘或分区，你可以在 */etc/fstab* 文件中为该磁盘或分区创建条目。有关如何添加 NFS 文件系统条目的说明，请参阅第 18 章。

## 使用 *mount* 命令挂载文件系统

你的 Fedora 或 Red Hat Linux 系统在每次启动时都会自动运行 *mount* -a（挂载所有文件系统）。因此，你通常只在特殊情况下使用 *mount* 命令。具体来说，普通用户或管理员以两种方式使用 *mount*：

- 显示当前已挂载的磁盘、分区和远程文件系统。
- 临时挂载一个文件系统。

任何用户都可以输入 mount 命令（不带选项）来查看本地 Linux 系统当前挂载了哪些文件系统。（以下是一个 mount 命令的示例。它显示了一个包含根（`/`）文件系统的单个硬盘分区（`/dev/hda1`），以及分别挂载在 /proc 和 /dev 上的 proc 和 devpts 文件系统类型。最后一个条目显示了一个软盘，它使用标准的 Linux 文件系统 (ext3) 格式化，并挂载在 /mnt/floppy 目录上。）

```
$ mount
/dev/hda3 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw, gid=5, mode=620)
/dev/hda2 on /boot type ext3 (rw)
none on /dev/shm type tmpfs (rw)
/dev/fd0 on /media/floppy type ext3 (rw)
```

最常见的手动挂载设备是你的软盘和 CD-ROM。不过，取决于你使用的桌面类型，插入 CD-ROM 和软盘时它们可能会自动为你挂载。（在某些情况下，自动运行程序也可能自动执行。例如，自动运行可能启动 CD 音乐播放器或软件包安装程序来处理介质上的数据。）

## 挂载可移动介质

然而，如果你想手动挂载文件系统，/etc/fstab 文件有助于使挂载软盘或 CD-ROM 变得简单。在某些情况下，你可以使用带有一个选项的 mount 命令来指示你想要挂载的内容，并从 /etc/fstab 文件中获取信息以填充其他选项。你的 /etc/fstab 文件中可能已经存在的条目允许你在以下两种情况下进行快速挂载：

- **CD-ROM** — 如果你正在挂载一个采用标准 ISO 9960 格式的 CD-ROM（大多数软件 CD-ROM 都是如此），你可以将 CD-ROM 放入 CD-ROM 驱动器并输入以下内容来挂载该 CD-ROM：

```
# mount /media/cdrom
```

默认情况下，你的 CD-ROM 挂载在 /media/cdrom 目录上。（文件系统类型、设备名称和其他选项会自动填充。）要查看内容，请输入 `cd /media/cdrom`，然后输入 `ls`。将显示 CD-ROM 根目录中的文件。然而，使用新的 /media 目录结构，如果你的光驱是 CD/DVD 组合光驱，其名称将有所不同。例如，带有 DVD 播放器的 CD 刻录机将命名为 /media/cdrom_dvdrom。请检查 /etc/fstab 文件，查看 Linux 为该设备选择的挂载点。

- **软盘** — 如果你正在挂载一个采用标准 Linux 文件系统格式 (ext3) 的软盘，你可以将软盘插入软盘驱动器并输入以下内容来挂载该软盘：

