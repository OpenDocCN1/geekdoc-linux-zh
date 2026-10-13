
对于 `iso9660` 文件系统，有趣的选项是 `unhide`，它可以显示隐藏和关联文件。

`fstab` 手帮助页包含 `fstab` 及其字段的详细描述。

`/etc/fstab` 的第五个字段用于 `dump`（一个传统的 UNIX 备份程序），以确定文件系统是否应该被 dump（备份）；1 表示是，0 表示否。初始安装时设置了默认值。如果你确实使用 `dump`，这些值就是需要关注的；届时为你想要备份的文件系统将该值设置为 1。

第六个字段用于 `fsck`，以确定 `fsck` 如何与文件系统交互——0 表示 `fsck` 永远不会在文件系统上运行（例如 FAT32 文件系统）；1 表示 `fsck` 将在预定时间在驱动上运行。对于非根文件系统建议使用 2，以免 `fsck` 运行得过于频繁。

以下是一个具有 RAID0 ext3 根分区并与 MS Windows 双启动的系统的简单 `/etc/fstab` 文件：

| LABEL=/1 | | ext3 | defaults | 1 1 |

| none | /dev/pts | devpts gid=5,mode=620 | 0 0 |

| none | /proc | proc defaults | 0 0 |

| none | /dev/shm | tmpfs defaults | 0 0 |

| /dev/hda1 | swap | defaults | 0 0 |

| /dev/cdrom | /mnt/cdrom | iso9660 noauto,owner,kudzu | 0 0 |

| /dev/fd0 | /mnt/floppy | auto noauto,owner,kudzu | |

| /dev/hda1 | /mnt/win_c | vfat auto,quiet,exec | 0 0 |

注意标记有 `kudzu` 选项的条目。这是 `ufstab` 操作的结果，它保持 `fstab` 与系统上可移动设备的状态同步，如 CD-ROM、软盘驱动器、Zip 和 Jaz 驱动器、LS-120 驱动器以及数字相机。Windows 分区的 `quiet` 选项将抑制错误信息，如果你使用 Wine 程序，建议使用它。

> 注意
>
> 设备非常有用。你可以使用 `/etc/fstab` 中的标签（label），如果你有很多设备，它们的标签可能比设备名称更容易记忆和跟踪。你也可以在不编辑 `fstab` 的情况下调整分区，只需通过更改它们的标签即可。`e22label` 命令比类似的 `tune2fs` 命令更容易记忆。

`e22label` 命令可以显示或更改设备的标签。（你也可以使用 `-L` 更改设备标签）。例如，要将 `/dev/hda4` 的标签改为 `archives`：

```bash
# e22label /dev/hda4 archives
```

如前所述，你在安装期间会在 `/etc/fstab` 中记录挂载偏好。只有当你对挂载进行更改，或者希望更改默认设置以满足特定需求时，才需要修改 `/etc/fstab`。

# 管理文件系统

## 自动挂载文件系统

设备非常有用。你可以使用 `/etc/fstab` 中的标签（label），如果你有很多设备，它们的标签可能比设备名称更容易记忆和跟踪。你也可以在不编辑 `fstab` 的情况下调整分区，只需通过更改它们的标签即可。`e22label` 命令比类似的 `tune2fs` 命令更容易记忆。

`e22label` 命令可以显示或更改设备的标签。（你也可以使用 `-L` 更改设备标签）。例如，要将 `/dev/hda4` 的标签改为 `archives`：

```bash
# e22label /dev/hda4 archives
```

如前所述，你在安装期间会在 `/etc/fstab` 中记录挂载偏好。只有当你对挂载进行更改，或者希望更改默认设置以满足特定需求时，才需要修改 `/etc/fstab`。

## 挂载文件系统 (NFS) 卷

```
# mount -t nfs remote_host:/dir mount_point
```

存在许多挂载选项。这些选项主要用于 `/etc/fstab` 文件。你可以通过在 `-o` 切换之前加上挂载选项（或一组用逗号分隔的选项字符串）来调用挂载选项。挂载选项列在本章的 fstab 部分。

## umount 命令

要卸载文件系统，请使用具有以下语法格式的 `umount` 命令：

```
umount mount_point
```

你也可以通过设备名称进行卸载：

```
umount device_name
```

> 注意事项
>
> 不要使用 `umount` 卸载系统运行不需要的所有内容（或正在使用的任何内容）。在多用户网络系统中，卸载所有内容是一个特别糟糕的主主意，因为你的用户无疑会失去对某些或所有文件的访问权限。因此，正如任何出色的系统管理员会告诉你说的那样，不要这样做。

## 通过 /etc/fstab 自动挂载

存在一个特殊文件 `/etc/fstab`，用于为系统提供预定义的选项和挂载点，以便能够以最少的输入量自动或手动挂载文件系统，而无需记忆那些晦涩的 Linux 语法。

`/etc/fstab` 文件仅允许超级用户写入。`fsck`、`mount` 以及所有读取命令都会从 `/etc/fstab` 读取信息。每个文件系统都有其独立的一行，信息之间用制表符分隔。

在 `fstab` 的每行中，第一个字段标识将要挂载的块设备或远程文件系统。第二个字段标识本地系统上挂载文件系统的挂载点。第三个字段是文件系统类型，第四个字段是逗号分隔的挂载选项列表。选项包括：

- `exec`—如果指定了此选项，可以从该文件系统执行二进制文件。
- `auto`—这意味着该选项不会导致文件系统被立即挂载，而它将在启动时挂载。
- `noexec`—如果指定了此选项，则无法从该文件系统执行二进制文件。
- `nosuid`—此选项不设置用户标识符或设置组标识符位以生效。
- `ro`—此选项将文件系统以只读模式挂载。
- `rw`—此选项将文件系统以读/写模式挂载。
- `sync`—对文件的读取和写入将同步完成。
- `user`—此选项允许普通用户（不仅仅是 root）挂载文件系统，但默认情况下包含了 `noexec`、`nosuid` 和 `nodev` 选项，除非它们被 `exec`、`dev` 和 `suid` 覆盖。

对于 `iso9660` 文件系统，有趣的选项是 `unhide`，它可以显示隐藏和关联文件。

`fstab` 手帮助页包含 `fstab` 及其字段的详细描述。

`/etc/fstab` 的第五个字段用于 `dump`（一个传统的 UNIX 备份程序），以确定文件系统是否应该被 dump（备份）；1 表示是，0 表示否。初始安装时设置了默认值。如果你确实使用 `dump`，这些值就是需要关注的；届时为你想要备份的文件系统将该值设置为 1。

第六个字段用于 `fsck`，以确定 `fsck` 如何与文件系统交互——0 表示 `fsck` 永远不会在文件系统上运行（例如 FAT32 文件系统）；1 表示 `fsck` 将在预定时间在驱动上运行。对于非根文件系统建议使用 2，以免 `fsck` 运行得过于频繁。

以下是一个具有 RAID0 ext3 根分区并与 MS Windows 双启动的系统的简单 `/etc/fstab` 文件：

| LABEL=/1 | | ext3 | defaults | 1 1 |

| none | /dev/pts | devpts gid=5,mode=620 | 0 0 |

| none | /proc | proc defaults | 0 0 |

| none | /dev/shm | tmpfs defaults | 0 0 |

| /dev/hda1 | swap | defaults | 0 0 |

| /dev/cdrom | /mnt/cdrom | iso9660 noauto,owner,kudzu | 0 0 |

| /dev/fd0 | /mnt/floppy | auto noauto,owner,kudzu | |

| /dev/hda1 | /mnt/win_c | vfat auto,quiet,exec | 0 0 |

注意标记有 `kudzu` 选项的条目。这是 `ufstab` 操作的结果，它保持 `fstab` 与系统上可移动设备的状态同步，如 CD-ROM、软盘驱动器、Zip 和 Jaz 驱动器、LS-120 驱动器以及数字相机。Windows 分区的 `quiet` 选项将抑制错误信息，如果你使用 Wine 程序，建议使用它。

> 注意
>
> 设备非常有用。你可以使用 `/etc/fstab` 中的标签（label），如果你有很多设备，它们的标签可能比设备名称更容易记忆和跟踪。你也可以在不编辑 `fstab` 的情况下调整分区，只需通过更改它们的标签即可。`e22label` 命令比类似的 `tune2fs` 命令更容易记忆。
