
表 5-4 列出了挂载和卸载软盘时实用的命令。

## 使用 CD、DVD 和 ISO 镜像

大多数软件不会从 CD 和 DVD 下载，因为它们的存储容量比软盘大；一张 DVD 存储的数据是软盘的 3000 多倍。与软盘一样，CD 和 DVD 可以使用 `mount` 和 `unmount` 命令进行挂载和卸载，如表 5-4 所示；但这些命令使用的设备文件是不同的。CD-ROM、DVD-ROM 以及 CD-RW 和 DVD-RW（可以刻录空白 CD 或 DVD）使用的设备文件取决于驱动器本身使用的技术。如果你的电脑带有 PATA CD-RW、DVD-ROM 或 DVD-RW 驱动器，你可以参考以下标准 PATA 硬盘配置（在第 2 章讨论过）：

- 主主设备 (`/dev/hda`)
- 主从设备 (`/dev/hdb`)
- 从主设备 (`/dev/hdc`)
- 从从从设备 (`/dev/hdd`)

然而，如果你有 SATA 或 SCSI CD-ROM、CD-RW、DVD-ROM 或 DVD-RW 驱动器，Linux 可能根据你的 CD 或 DVD 驱动器使用不同的名称：

- 第一个 SATA/SCSI 驱动器 (`/dev/sda`, `/dev/sd0`, `/dev/sr0`, `/dev/sg0`)
- 第二 SATA/SCSI 驱动器 (`/dev/sdb`, `/dev/sd1`, `/dev/sr1`, `/dev/sg1`)
- 第三个 SATA/SCSI 驱动器 (`/dev/sdc`, `/dev/sd2`, `/dev/sr2`, `/dev/sg2`)
- 以此类推

例如，如果你的系统有 SATA 或 SCSI CD-ROM 或 CD-RW 驱动器，通常使用 `/dev/sda` 或 `/dev/sd0` 读取 CD。然而，如果你的系统有 SCSI DVD-ROM 或 DVD-RW，通常会使用 `/dev/sr0` 读取 CD 和 DVD。如果你使用刻录软件写入 CD-RW 或 DVD-RW 驱动器，刻录软件通常使用 `/dev/sg0` ![](img/bafa5678973f896b93838a140b8f7840_232_0)

- 几乎所有的 DVD-ROM 和 DVD-RW 驱动器也可以配合 CD 使用。Linux 有许多刻录软件。Fedora 自带 `Brasero` 程序。你可以通过导航到 GNOME 环境中的应用程序>声音和视频>`Brasero` 来访问该程序。为了方便识别 CD、CD-RW、DVD-ROM 或 DVD-RW 驱动器，Linux 在 `/dev/` 中创建符号链接：
  - `/dev/cdrom` 指向 CD-ROM 驱动器的设备文件
  - `/dev/cdrw` 指向 CD-RW 驱动器的设备文件
  - `/dev/dvd` 指向 DVD 的设备文件
  - `/dev/dvdrw` 指向 DVD-RW 驱动器的设备文件

例如，如果你的系统有一个配置为从设备的 PATA CD-ROM 驱动器，`/dev/cdrom` 的长列表显示如下：

```
[root@server1 ~]# ls -l /dev/cdrom
lrwxr-x 1 root Aug 10 19 /dev/cdrom -> /dev/hdd
[root@server1 ~]#
```

然而，如果你的系统有 DVD-RW 驱动器，符号链接将指向 `/dev/sr0`，如下所示：

```
[root@server1 ~]# ls -l /dev/cdrw
lrwxr-x 1 root Aug 10 29 /dev/cdrw -> sr0
[root@server1 ~]# ls -l /dev/dvd
lrwxr-x 1 root Aug 10 29 /dev/dvd -> sr0
[root@server1 ~]# ls -l /dev/dvdrw
lrwxr-x 1 root Aug 10 29 /dev/dvdrw -> sr0
[root@server1 ~]#
```

此外，CD 和 DVD 通常使用 `iso9660` 文件系统类型，并且在 Linux 下访问时是只读的（记住你必须使用刻录软件写入 CD 或 DVD）。要将 CD 或 DVD 挂载到目录，应使用 `iso9660` 文件系统类型并在 `mount` 命令中添加 `-r`（只读）选项。要将示例 CD 挂载到 `/media/cd` 目录并查看其内容，可以使用以下命令：

```
[root@server1 ~]# mount -r -t iso9660 /dev/cdrom /media/cd
[root@server1 ~]# mount
/dev/sda1 / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/ptpts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunprpc on /var/lib/rpc/rpc_pipe type (rw)
/dev/cdrom on /media/cd type iso9660 (ro)
[root@server1 ~]# mount -l /media/cd
autofun.inf* generics/ jingle/ jungle.txt* joystick/
[root@server1 ~]# umount /media/cd
[root@server1 ~]#
```

> 在示例中，`/media/cd` 目录必须存在，`mount` 命令才能成功。

![](img/bafa5678973f896b93838a140b8f7840_233_0.png)

与软盘一样，你可以修改 `/etc/fstab` 文件，使得对于 CD 或 DVD 只需为 `mount` 命令指定单个参数。还要记住挂载点目录不能用于成功挂载或卸载 CD 和 DVD；必须使用 `fuser` 命令进行验证。

与软盘不同，CD 和 DVD 在正确卸载之前无法从驱动器中弹出，`mount` 命令作为预防措施锁定 CD-ROM、CD-RW、DVD-ROM 或 DVD-RW 驱动器。当你登录 GUI 环境并向系统插入标签为 `Pictures` 的 CD 或 DVD 时，系统会自动创建一个 `/media/Pictures` 目录并将设备挂载到该目录，如下：

```
[root@server1 ~]# mount
/dev/sda1 / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/ptpts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunprpc on /var/lib/rpc/rpc_pipe type (rw)
/dev/cdrom on /media/cd type iso9660 (ro)
sunrpc on /var/lib/nfs/rpc_pipes type rpc_pipes (rw)
gvfs-fuse-daemon on /home/bob/.gvfs type gfs-fuse-daemon (rw, nosuid, nodev, user=bob)
/dev/sr0 /media/Pictures type iso9660 (ro,nosuid, nodev, uhelper= disks,uid=501,gid=501,ioctl-utf8,mode=0400,dmode=0500)
```

此外，系统会在桌面上创建一个指向 `/media/Pictures` 目录的快捷方式，并带有一个 DVD 图标，你可以轻松地访问 DVD 的内容，如图 5-3 所示。

你可以右键点击图 5-3 所示的 DVD 并选择“弹出”（`Eject`），以从 `/media/Pictures` 目录中卸载 DVD，并强制 DVD 驱器弹出 DVD。

`iso9660` 文件系统不仅限于 CD 和 DVD。你还可以创建包含其他文件的镜像文件，称为 `ISO`。从网上获取的大多数软件（如 Linux 发行版和 BSD UNIX）都以 `ISO` 镜像的形式提供。下载后，可以使用光刻录软件将 `ISO` 镜像写入 CD 或 DVD，或者由你的 Linux 系统挂载并访问。如果你下载了一个名为 `sample` 的 `ISO` 镜像，可以将其作为回环设备挂载到 `/mnt` 目录，通过以下命令访问 `sample.iso` 文件的内容：

```bash
[root@server1] # mount
```
