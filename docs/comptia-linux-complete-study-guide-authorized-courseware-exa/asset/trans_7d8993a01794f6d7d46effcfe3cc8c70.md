

## 挂载支持的一些常见参数具备多种功能：

- **挂载所有文件系统**：`-a` 参数会让 mount 命令挂载 `/etc/fstab` 文件中列出的所有文件系统，该文件指定了最常用的分区和设备。接下来的“永久挂载文件系统”部分将描述该文件的格式。
- **以只读方式挂载**：`-r` 参数会导致 Linux 以只读方式挂载文件系统，即使它通常是一个读/写文件系统。
- **显示详细输出**：与许多命令一样，`-v` 会生成详细输出——程序会在操作发生时提供注释。
- **以读写方式挂载**：`-w` 参数会导致 Linux 尝试以读和写操作的方式挂载文件系统。这是大多数文件系统的默认设置，但一些实验性驱动默认采用只读操作。`-o rw` 选项具有相同的效果。
- **指定文件系统类型**：使用 `-t fstype` 参数来指定文件系统类型。常见的文件系统类型包括 ext2（用于 ext2fs）、ext3（用于 ext3fs）、ext4（用于 ext4fs）、reiserfs（用于 ReiserFS）、jfs（用于 JFS）、xfs（用于 XFS）、vfat（用于具有 VFAT 长文件名的 FAT）、msdos（用于仅使用短 DOS 文件名的 FAT）、iso9660（用于 CD-ROM 文件系统）、udf（用于 DVD 和某些 CD-ROM 文件系统）、nfs（用于 NFS 网络挂载）、smbfs（用于 SMB/CIFS 网络共享）以及 cifs（用于 SMB/CIFS 网络共享的新驱动）。Linux 支持许多其他类型。如果省略此参数，Linux 将尝试自动检测文件系统类型。

![](img/f339a9f48c4b443e61c74acb4c9c3da4_218_0.png)

Linux 需要内核支持或作为内核模块来挂载给定类型的文件系统。如果缺少这种支持，Linux 将拒绝挂载相应的文件系统。

- **按标签或 UUID 挂载**：`-L label` 和 `-U uuid` 选项分别告知 mount 命令挂载具有指定标签或 UUID 的文件系统。
- **其他选项**：您可以使用 `-o` 参数添加许多选项。其中许多是特定于文件系统的。
- **设备**：*device* 是与分区或磁盘设备关联的设备文件名，例如 /dev/hda4、/dev/fd0 或 /dev/cdrom。此参数通常是必需的，但在某些情况下可以省略，详见下文。
- **挂载点**：*mountpoint* 是将设备内容附加到的目录。与 *device* 一样，它通常是必需的，但在某些情况下可以省略。

前述的挂载参数列表并非详尽无遗；请参阅 mount 手册页以了解更晦涩的选项。mount 的常见应用使用很少的参数，因为 Linux 通常能很好地检测文件系统类型，且默认参数运行良好。例如，考虑以下示例：

```
# mount /dev/sdb7 /mnt/shared
```

此命令将 /dev/sdb7 的内容挂载到 /mnt/shared，自动检测文件系统类型并使用默认选项。通常，只有 root 才能发出 mount 命令；但是，如果 /etc/fstab 指定了 user、users 或 owner 选项，普通用户可以使用简化的语法挂载文件系统，其中仅指定设备或挂载点，而非两者都指定。例如，如果 /etc/fstab 指定 /mnt/cdrom 为挂载点并使用 user、users 或 owner 选项，用户就可以输入 mount /mnt/cdrom 来挂载 CD-ROM。

> 大多数 Linux 发行版都附带自动挂载支持，这使得操作系统在插入可移动介质时自动挂载它们。在 GUI 环境中，文件浏览器也可能在插入磁盘时打开。为了弹出磁盘，用户需要使用稍后描述的 umount 卸载文件系统，或者通过选择桌面环境中的选项来卸载。

当 Linux 挂载文件系统时，它通常会在 /etc/mtab 中记录这一事实。该文件的格式与 /etc/fstab 类似，并存储在 /etc 中，但它不是您应该编辑的配置文件。不过，您可以检查此文件以确定哪些文件系统已挂载。（df 命令，在“监控分区的磁盘使用情况”中有更详细的描述，是了解已挂载文件系统的另一种方法。）

### 挂载选项

当你确实需要使用特殊参数（通过 -o 或在 /etc/fstab 中）时，通常是为了添加特定于文件系统的选项。表 3.5 总结了最重要的文件系统选项。其中一些仅在 /etc/fstab 文件中才有意义。

#### 表 3.5 mount 命令的重要文件系统选项

| 选项 | 支持的文件系统 | 描述 |
|---|---|---|
| defaults | 所有 | 导致使用该文件系统的默认选项。它主要用于 /etc/fstab 文件中，以确保文件包含选项列。 |
| loop | 所有 | 导致使用该挂载的回环设备。允许你将文件作为磁盘分区进行挂载。例如，mount -t vfat -o loop image.img /mnt/image 将文件 image.img 作为磁盘进行挂载。 |
| auto 或 noauto | 所有 | 在启动时或当 root 发出 **mount -a** 命令时挂载或不挂载文件系统。默认是 auto，但可移动介质适合使用 noauto。用于 `/etc/fstab`。 |
| user 或 nouser | 所有 | 允许或禁止普通用户挂载文件系统。默认是 nouser，但可移动介质通常适合使用 user。用于 `/etc/fstab`。当包含在此文件中时，user 允许用户输入 **mount /mountpoint**（其中 /mountpoint 是指定的挂载点）来挂载磁盘。只有挂载了该文件系统的用户才能卸载它。 |
| users | 所有 | 与 user 类似，除了任何用户都可以在文件系统挂载后卸载它。 |
| owner | 所有 | 与 user 类似，除了用户必须拥有该设备文件。某些发行版，如 Red Hat，将某些设备文件（如软盘驱动的 `/dev/fd0`）的所有权分配给控制台用户，因此这是一个有用的选项。 |
| remount | 所有 | 在不显式卸载分区的更改一个或多个挂载选项。要使用此选项，你需要在已挂载的文件系统上发出 mount 命令，并带有 remount 以及你想要更改的任何选项。例如，此功能可用于启用或禁用分区的写访问。 |
| ro | 所有 | 指定以只读方式挂载文件系统。对于没有写访问权限的文件系统以及一些写支持特别不可靠的文件系统，这是默认设置。 |
| rw | 所有读写文件系统 | 指定以读写方式挂载文件系统。对于大多数读写文件系统，这是默认设置。 |
| `uid=value` | 大多数不支持 Unix 风格权限的文件系统，如 vfat, hpfs, ntfs 和 hfs | 设置所有文件的所有者。例如，`uid=500` 将所有者设置为拥有 Linux 用户 ID 500 的人。（在 `/etc/passwd` 文件中检查 Linux 用户 ID。） |
| `gid=value` | 大多数不支持 Unix 风格权限的文件系统，如 vfat, hpfs, ntfs 和 hfs | 工作方式与 `uid=value` 类似，但设置文件系统中所有文件的组。你可以在 `/etc/group` 文件中找到组 ID。 |
| `umask=value` | 大多数不支持 Unix 风格权限的文件系统，如 vfat, hpfs, ntfs 和 hfs | 设置文件权限的 umask。value 被解释为从文件权限中移除位的二进制值。例如，`umask=027` 产生 750 的权限，即 `-rwxr-x---`。与 `uid=value` 和 `gid=value` 结合使用，此选项让你控制谁可以访问 FAT、HPFS 和许多其他外部文件系统上的文件。 |
| `dmask=value` | 大多数不支持 Unix 风格权限的文件系统，如 vfat, hpfs, ntfs 和 hfs | 类似于 umask，但仅设置目录的 umask，而不设置文件的。 |
| `fmask=value` | 大多数不支持 Unix 风格权限的文件系统，如 vfat, hpfs, ntfs 和 hfs | 类似于 umask，但仅设置文件的 umask，而不设置目录的。 |
| `conv=code` | 大多数用于 Microsoft 和 Apple 操作系统上的文件系统：msdos, umsdos, vfat, hpfs 和 hfs | 如果 `code` 是 `b` 或 `binary`，Linux 不会修改文件的内容。如果 `code` 是 `t` 或 `text`，Linux 自动在 Linux 风格和 DOS 或 Macintosh 风格的行结束字符之间转换文件。如果 `code` 是 `a` 或 `auto`，除非文件是已知的二进制文件格式，否则 Linux 会应用转换。通常最好将其保留为默认值 `binary`，因为文件转换可能会对某些应用程序和文件类型造成严重问题。 |
| `norock` | iso9660 | 禁用 ISO-9660 CD-ROM 的 Rock Ridge 扩展。 |
| `nojoliet` | iso9660 | 禁用 ISO-9660 CD-ROM 的 Joliet 扩展。 |

