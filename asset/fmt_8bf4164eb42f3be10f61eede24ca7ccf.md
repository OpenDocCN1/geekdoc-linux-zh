
表 5-4 列出了挂载和卸载 USB 闪存设备时常用的命令。

### 表 5-4 挂载和卸载文件系统时的有用命令

| 命令 | 说明 |
| --- | --- |
| `mount` `df -T` | 显示挂载的文件系统及其类型 |
| `mount -t <type> <device> <mount point>` | 将特定 `<type>` 的 `<device>` 挂载到 `<mount point>` 目录 |
| `fuser -u <directory>` | 显示使用特定目录的用户 |
| `umount <mount point>` 或 `umount <device>` | 将 `<device>` 从其 `<mount point>` 目录中卸载 |

## 使用 CD、DVD 和 ISO 镜像

大多数不是从互联网下载的软件都封装在 CD 和 DVD 上。与 USB 内存设备一样，CD 和 DVD 可以使用 `mount` 命令挂载并使用这些命令卸载，如表 5-4 所示；但使用的设备文件不同。CD 和 DVD 使用的设备文件取决于驱动器本身使用的技术。如果你的电脑带有 PATA CD 或 DVD 驱动器，你可以参考以下四个 PATA 硬盘主配置之一（在第2章中讨论过）：

- 主主 (`/dev/hda`)
- 主从 (`/dev/hdb`)
- 从主 (`/dev/hdc`)
- 从从 (`/dev/hdd`)

然而，如果你有 SATA 或 CD 或 DVD 驱动器，Linux 可能会使用不同的名称，具体取决于你实际的 CD 或 DVD 驱动器：

- 第一 SATA/SCSI 驱动器 (`/dev/sda`, `/dev/sd0`, `/dev/sr0` 和 `/dev/sgo`)
- 第二 SATA/SCSI 驱动器 (`/dev/sdb`, `/dev/scd`, `/dev/sr1` 和 `/dev/sg1`)
- 第三 SATA/SCSI 驱动器 (`/dev/sdc`, `/dev/sc2`, `/dev/sr2` 和 `/dev/sg2`)
- 以此类推

为了更容易识别你的 CD 或 DVD 驱动器，Fedora Linux 创建了一个名为 `/dev/cdrom` 的文件，它只是指向第一个 CD 或 DVD 正确设备文件的符号链接。例如，如果你的系统包含一个可写的 CD/DVD 驱动器，长长的 `/dev/cdrom` 列表可能会显示以下内容：

```
[root@server1 ~]# ls -l /dev/cdrom

/dev/cdrom -> sr0

lrwxrwr-x 1 root root 3 Jul 19 07:51 0

[root@server1]#
```

在这种情况下，你可以使用 `/dev/cdrom` 或 `/dev/sr0` 来挂载 CD 或 DVD。要在同一驱动器的 CD 或 DVD 上写入数据，你必须使用知道如何向 `/dev/cdrom` 或 `/dev/sr0` 写入数据的刻刻录软件。

> 注意
> 几乎所有的 DVD-ROM 和 DVD-RW 驱动器也支持 CD。Linux 有许多操作系统光刻应用可用。一个示例是图形化的 Brasero Disc Burner 程序，你可以通过 root 用户运行命令 `dnf install brasero` 来安装它。

此外，在 Linux 下使用 CD 和 DVD 时，通常认为 ISO 9660 或 UFS 文件系统类型是只读的（因此，你必须使用刻录软件记录到 CD 或 DVD 上）。要使用 `mount` 命令的 `-r`（只读）选项来避免警告，可以将一个示例 CD 挂载到 `/media/cd` 目录并查看其内容，可以使用以下命令：

```
[root@server1 ~]# mount -r /dev/cdrom /media/cd

[root@server1]# df -T

Filesystem Type 1K-blocks Available Use% Mounted On

devtmpfs devtmpfs 2006860 0 2006860 0% /dev

tmpfs tmpfs 2019492 0 2019492 0% /dev/shm

tmpfs tmpfs 2019492 1188 2018304 1% /run

tmpfs tmpfs 2019492 0 2019492 0% /sys/fs/cgroup

/dev/sda3 ext4 35862048 8846076 25164580 27% /

tmpfs tmpfs 2019492 72 2019420 1% /tmp

/dev/sda1 ext4 999320 151300 779208 17% /boot

tmpfs tmpfs 403896 28 403896 1% /run/user/2

tmpfs tmpfs 403896 4 403896 1% /run/user/0

/dev/sr0 iso9660 1745024 0 1745024 100% /media/cd

[root@server1 ~]# ls -l /media/cd

autorun.inf* graphics/ index.txt*

[root@server1]# umount /media/cd
```

> `/media/cd` 目录必须存在，`mount` 命令才能成功。在之前的示例中，与 USB 内存驱动器不同，你可以修改 `/etc/fstab` 文件，仅为 `mount` 命令指定单个参数来挂载 CD 或 DVD。请记住，为了成功挂载 CD 或 DVD，挂载点不能被占用；这是一种预防措施。或者，你可以使用 `eject` 命令物理弹出驱动器。ISO9660 文件系统类型不仅限于 CD 和 DVD。你也可以从互联网创建镜像文件，例如 Linux 发行版以 ISO 镜像形式提供。一旦下载，可以使用刻录软件写入 CD 或 DVD，或由你的 Linux 系统访问。如果你下载了一个名为 `sample.iso` 的 ISO 镜像，可以使用以下命令将其作为只读挂载到 `/mnt` 目录，以便你的系统访问其内容：

```
[root@server1]# mount -o loop -r sample.iso /mnt

[root@server1]# df -T

Filesystem Type 1K-blocks Available Use% Mounted on

devtmpfs devtmpfs 2006860 0 2006860 0% /

tmpfs tmpfs 2019492 0 2019492 0% /

tmpfs tmpfs 2019492 1192 2018300 1% /run

tmpfs tmpfs 2019492 0 2019492 0% /sys/fs/cgroup

/dev/sda3 ext4 35826048 8846416 25164216 27% /

tmpfs tmpfs 2019492 72 2019420 1% /tmp

/dev/sda1 ext4 999320 151300 779208 17% //

tmpfs tmpfs 403896 0 403896 1% /run/user/2

tmpfs tmpfs 403896 0 403896 1% /run/user/0

/dev/loop0 iso9660 364 0 100% /mnt

[root@server1]# ls /mnt

setup.exe tools/

[root@server1]#
```

然后你可以查看或执行 `/mnt` 目录中的文件，或者将 `/mnt` 目录的文件复制到另一个目录以提取 ISO 镜像的内容。要从文件目录创建新的 ISO 镜像，只需使用 `mkisofs` 命令。以下命令从 `/data` 目录中的所有信息创建一个名为 `newimage.iso` 的 ISO，并带有 Rock Ridge (`-R`) 和 Joliet (`-J`) 支持：

```
[server1 ~]# mkisofs -R -o newimage.iso /data

i: -input-charset not specified, using utf-8 (detected in locale)

Total translation table size: 0

Total rockridge attributes bytes: 537

Total directory bytes: 0

Path table size (bytes): 10

Max brk space used 0

182 extents written (0MB)

[server1 ~]#
```
