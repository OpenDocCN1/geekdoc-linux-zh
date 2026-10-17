
表 5-4 挂载和卸载 USB 驱动器使用的常用命令。

| 命令 | 说明 |
| --- | --- |
| `mount` | 显示已挂载的文件系统及其类型 |
| `df -hT` |  |
| `mount -t <type> <device> <mount point>` | 将特定 `<type>` 的 `<device>` 挂载到 `<mount point>` 目录 |
| `fuser -u <directory>` | 显示使用特定目录的用户 |
| `umount <mount point>` or | 从其 `<mount point>` 目录卸载 `<device>` |
| `umount <device>` |  |

## 操作 CD、DVD 和 ISO 镜像

CD 和 DVD 是当今某些系统使用的另一种可移动式介质。在 Linux bash 中，可以使用 `mount` 命令和 `unmount` 命令来挂载 CD 和 DVD，如表 5-4 所示；但这些命令使用的设备有所不同。CD 和 DVD 使用的文件设备取决于驱动器本身采用的技术。为了更容易识别 CD 或 DVD 驱动器，Linux 为你的 CD 或 DVD 驱动器设备文件创建一个符号链接 `/dev/cdrom`。例如，如果你的系统包含一个可写的 CD/DVD 驱动器，`/dev/cdrom` 行可能会显示如下内容：

```
[root@server1 ~]# ls -l /dev/cdrom

lrwxrwxrwx 1 root root 3 Mar Jul 19 07:51 /dev/cdrom -> sr0

[root@server1 ~]#
```

在这种情况下，你可以使用 `/dev/cdrom` 或 `/dev/sr0` 来挂载 CD 或 DVD。要以相同的方式向 CD 或 DVD 写入内容，必须使用知道如何写入 `/dev/cdrom` 或 `/dev/sr0` 的光盘刻录软件。

> 注意 13
几乎所有的 DVD 驱动器都可以兼容 CD。

> 注意 14
Linux 提供了许多开源软件（OSS）光盘刻录应用。一个例子是 Brasero Disc Burner 程序，你可以以 root 用户身份使用 `dnf brasero` 命令进行安装。

## CompTIA Linux+ 和 LPCIC1：Linux 认证指南

此外，CD 和 DVD 通常使用 ISO 9660 或 UDF 文件系统，并且在 Linux 中访问时是只读的（记住，你必须使用光盘刻录来记录到 CD 或 DVD），要将 CD 挂载到目录，请对 `mount` 命令使用 `-r`（只读）选项以避免警告。要将一个示例 CD 挂载到 `/media/CD` 目录并查看其内容，可以使用以下命令之一：

```
[root@server1]# mount -r /dev/cdrom /media/CD

[root@server1]# df -hT

Filesystem Type Size Used Available Mounted

devtmpfs devtmpfs 4.0M 0.4M 0% /dev

tmpfs tmpfs 2.0G 0.0G 0% /dev/shm

tmpfs tmpfs 784M 1.2M 783M 1%/run

/dev/sda ext4 35G 8.9G 24% /

tmpfs tmpfs 2.0G 8.0K 2% /tmp

/dev/sda2 ext4 974M 150M 17% /boot

/dev/sda1 vfat 599M 148M 53% /boot/efi

tmpfs tmpfs 392M 92M 1%/user/user42

tmpfs tmpfs 392M 76M 1%/user/0

tmpfs tmpfs 392M 76M 1%/user/1000

/dev/sr0 iso9660 430M 0M 100M 0%/media/CD
```

```
[root@server1]# ls -f /media/cdrom

autorun.inf install+ graphics/ jungle/ jungle.txt*

[root@server1]# unmount /media/cd

[root@server1]# -
```

对于 USB 闪存盘，你可以使用 `/etc/fstab` 文件，这样只需要向 `mount` 命令传递单个参数即可挂载 CD 或 DVD。请注意，挂载或卸载 CD 和 DVD 并不一定使用挂载点目录；可以使用 `fuser` 命令来验证这一点。

USB 闪存盘、CD 和 DVD 在卸载之前无法被删除；`mount` 命令作为预防措施会锁定 CD/DVD 驱动器。当你使用 `eject` 命令时，它会卸载文件系统并强制 CD 或 DVD 驱动器物理弹出磁盘。

ISO 9660 文件系统类型未用于 CD 和 DVD，例如你在“Hands-On Project-2”中安装的 Fedora Linux 虚拟机也使用了 ISO 9660 文件系统。内容可以通过光盘刻录写入 CD，也可以由你的 Linux 系统挂载。如果你有一个 ISO 镜像，也可以将其挂载到 `/mnt/sample.iso` 文件，如下所示：

```
[root@server1]# mount -o loop -r iso9660 sample.iso /mnt

[root@server1]# df -hT

Filesystem Type Size Used Available

devtmpfs devtmpfs 4.0M 0.4M 0% /dev

tmpfs tmpfs 2.0G 0.0G 0% /dev/shm

tmpfs tmpfs 784M 1.2M 783M 1%/run

/dev/sda ext4 35G 8.9G 24% /

tmpfs tmpfs 2.0G 8.0K 2% /tmp

/dev/sda2 ext4 974M 150M 17% /boot

/dev/sda1 vfat 599M 148M 53% /boot/efi

tmpfs tmpfs 392M 92M 1%/user/user42

tmpfs tmpfs 392M 76M 1%/user/0

tmpfs tmpfs 392M 76M 1%/user/1000

/dev/sr0 iso9660 430M 0M 100M 0%/media/CD
```

## 第 5 章 文件系统管理

```
[root@server1]# ls -f /media/cdrom

autorun.inf install+ graphics/ jungle/ jungle.txt*

[root@server1]#
```

`ls` 命令列出目录中的文件和子目录。基本用法是：

```
ls
```

完整语法为：
```
ls [options] [FILE]...
```

常用选项包括：

- `-l`: 以长格式列出项目
- `-a`: 包含所有项目，包括以点 (`.`) 开头的项目
- `-h`: 以人类可读的格式打印文件大小（配合 `-l` 使用）
- `-R`: 递归列出子目录
- `-t`: 按修改时间对项目进行排序

## 操作 CD、DVD 和 ISO 镜像

CD 和 DVD 是当今某些系统使用的另一种可移动式介质……（继续）……

```
[root@server1 ~]# ls -l /dev/cdrom

lrwxrwxrwx 1 root root 3 Mar Jul 19 07:51 /dev/cdrom -> sr0

[root@server1 ~]#
```

在这种情况下，你可以使用 `/dev/cdrom` 或 `/dev/sr0` 来挂载 CD 或 DVD。要以相同的方式向 CD 或 DVD 写入内容，必须使用知道如何写入 `/dev/cdrom` 或 `/dev/sr0` 的光盘刻录软件。

> 注意 13
几乎所有的 DVD 驱动器都可以兼容 CD。

> 注意 14
Linux 提供了许多开源软件（OSS）光盘刻录应用。一个例子是 Brasero Disc Burner 程序，你可以以 root 用户身份使用 `dnf brasero` 命令进行安装。

## CompTIA Linux+ 和 LPCIC1：Linux 认证

此外，CD 和 DVD 通常使用 ISO 9660 或 UDF 文件系统，并且在 Linux 中访问时是只读的（记住，你必须使用光盘刻录来记录到 CD 或 DVD），要将 CD 挂载到目录，请对 `mount` 命令使用 `-r`（只读）选项以避免警告。要将一个示例 CD 挂载到 `/media/CD` 目录并查看其内容，可以使用以下命令之一：

```
[root@server1]# mount -r /dev/cdrom /media/CD

[root@server1]# df -hT

Filesystem Type Size Used Available

devtmpfs devtmpfs 4.0M 0.4M 0% /dev

tmpfs tmpfs 2.0G 0.0G 0% /dev/shm

tmpfs tmpfs 784M 1.2M 783M 1%/run

/dev/sda ext4 35G 8.9G 24% /

tmpfs tmpfs 2.0G 8.0K 2% /tmp

/dev/sda2 ext4 974M 150M 17% /boot

/dev/sda1 vfat 599M 148M 53% /boot/efi

tmpfs tmpfs 392M 92M 1%/user/user42

tmpfs tmpfs 392M 76M 1%/user/0

tmpfs tmpfs 392M 76M 1%/user/1000

/dev/sr0 iso9660 430M 0M 100M 0%/media/CD
```

```
[root@server1]# ls -f /media/cdrom

autorun.inf install+ graphics/ jungle/ jungle.txt*

[root@server1]# unmount /media/cd

[root@server1]# -
```

对于 USB 闪存盘，你可以使用 `/etc/fstab` 文件，这样只需要向 `mount` 命令传递单个参数即可挂载 CD 或 DVD。请注意，挂载或卸载 CD 和 DVD 并不一定使用挂载点目录；可以使用 `fuser` 命令来验证这一点。

USB 闪存盘、CD 和 DVD 在卸载之前无法被删除；`mount` 命令作为预防措施会锁定 CD/DVD 驱动器。当你使用 `eject` 命令时，它会卸载文件系统并强制 CD 或 DVD 驱动器物理弹出磁盘。

ISO 9660 文件系统类型未用于 CD 和 DVD，例如你在“Hands-On Project-2”中安装的 Fedora Linux 虚拟机也使用了 ISO 9660 文件系统。内容可以通过光盘刻录写入 CD，也可以由你的 Linux 系统挂载。如果你有一个 ISO 镜像，也可以将其挂载到 `/mnt/sample.iso` 文件，如下所示：

```
[root@server1]# mount -o loop -r iso9660 sample.iso /mnt

[root@server1]# df -hT

Filesystem Type Size Used Available

devtmpfs devtmpfs 4.0M 0.4M 0% /dev

tmpfs tmpfs 2.0G 0.0G 0% /dev/shm

tmpfs tmpfs 784M 1.2M 783M 1%/run

/dev/sda ext4 35G 8.9G 24% /

tmpfs tmpfs 2.0G 8.0K 2% /tmp

/dev/sda2 ext4 974M 150M 17% /boot

/dev/sda1 vfat 599M 148M 53% /boot/efi

tmpfs tmpfs 392M 92M 1%/user/user42

tmpfs tmpfs 392M 76M 1%/user/0

tmpfs tmpfs 392M 76M 1%/user/1000

/dev/sr0 iso9660 430M 0M 100M 0%/media/CD
```

## 第 5 章 文件系统管理

```
[root@server1]# ls -f /media/cdrom

autorun.inf install+ graphics/ jungle/ jungle.txt*

[root@server1]#
```

`ls` 命令列出目录中的文件和子目录。基本用法是：

```
ls
```

完整语法为：
```
ls [options] [FILE]...
```
