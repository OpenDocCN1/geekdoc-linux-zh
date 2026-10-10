
然而，如果你使用的是 SATA 或 SCSI 光盘或 DVD 驱动器，Linux 可能会根据你的实际光盘或 DVD 驱动器使用许多不同的名称：

- 第一个 SATA/SCSI 驱动器（`/dev/sda`、`/dev/scd0`、`/dev/sr0` 和 `/dev/sdg0`）
- 第二个 SATA/SCSI 驱动器（`/dev/sdb`、`/dev/scd1`、`/dev/sr1` 和 `/dev/sd1`）
- 第三个 SATA/SCSI 驱动器（`/dev/sdc`、`/dev/sed2`、`/dev/sr2` 和 `/dev/sdg2`）
- 以此类推

为了更轻松地识别你的光盘或 DVD 驱动器，Fedora Linux 创建了一个名为 `/dev/cdrom` 的文件，它只是指向你的第一个光盘或 DVD 驱动器正确设备文件的符号链接。例如，如果你的系统包含一个 SATA CD/DVD 驱动器，`/dev/cdrom` 的长列表显示可能如下：

```
[root@server1 ~]# ls -l /dev/cdrom
lrwxrwxrwx 1 root root 3 Aug 10 12:39 /dev/cdrom -> sr0
[root@server1 ~]#_
```

在这种情况下，你可以使用 `/dev/cdrom` 或 `/dev/sr0` 来挂载 CD 或 DVD。但是，要向同一驱动器中的 CD 或 DVD 写入数据，你必须使用知道如何向 `/dev/cdrom` 或 `/dev/sr0` 写入数据的刻录软件。

![](img/c27875544958897d817484d558c208c8_232_0.png)

Linux 有许多可用的开源（OSS）光盘刻录软件应用程序。其中一个示例是图形化的 Brasero Disc Burner 程序，你可以以 root 用户身份运行命令 `yum install brasero` 来安装它。

此外，CD 和 DVD 通常使用 `iso9660` 文件系统类型，并且在使用 Linux 访问时是只读的（请记住，你必须使用光盘刻录软件来向 CD 或 DVD 记录数据）。因此，要将 CD 或 DVD 挂载到目录，你应该使用 `iso9660` 文件系统类型，并在 mount 命令中添加 `-r`（只读）选项。要将示例 CD 挂载到 `/media/cd` 目录并查看其内容，可以使用以下命令：

```
[root@server1 ~]# mount -r -t iso9660 /dev/cdrom /media/cd
[root@server1 ~]# mount
/ on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/cdrom on /media/cd type iso9660 (ro)
[root@server1 ~]# ls -l /media/cdrom
autorun.inf* install* graphics/ jingle/ jingle.txt*
joystick/
[root@server1 ~]# umount /media/cdrom
[root@server1 ~]#_
```

![](img/c27875544958897d817484d558c208c8_233_0.png)

在上面的示例中，`/media/cd` 目录必须存在，`mount` 命令才能成功。

与软盘一样，你可以修改 `/etc/fstab` 文件，以便只需向 `mount` 命令指定单个参数即可挂载 CD 或 DVD。请记住，要成功挂载或卸载 CD 和 DVD，挂载点目录必须未被使用；可以使用 `fuser` 命令来验证这一点。

与软盘不同，直到 CD 和 DVD 正确卸载之前，无法从驱动器中弹出它们，因为 `mount` 命令作为预防措施会锁定 CD/DVD 驱动器。

当你在图形用户界面（GUI）环境中插入 CD 或 DVD 时，系统会自动将其挂载到 `/run/media/username` 目录下的一个目录（其中 `username` 是登录到 GUI 环境的用户名称），该目录的名称是根据 CD 或 DVD 上的标签命名的（由光盘刻录软件指定）。例如，如果你以 `user1` 身份登录到 GUI 环境时，向系统中插入一个标签为 "Cafe_Scientifique" 的 DVD，系统将自动创建一个 `/run/media/user1/Cafe_Scientifique` 目录并将设备挂载到该目录，如下所示：

```text
[root@server1 ~]# mount
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
gvfs-fuse-daemon on /home/bob/.gvfs type fuse.gvfs-fuse-daemon (rw,nosuid,nodev,user=bob)
/dev/sr0 on /run/media/user1/Cafe_Scientifique type iso9660 (ro,nosuid,nodev,rhelper=udisks,uid=501,gid=501,iocharset=utf8,mode=0400,dmode=0500)
[root@server1 ~]#_
```

此外，系统还会在 GUI 环境中的“文件”应用程序中放置一个指向 `/run/media/user1/Cafe_Scientifique` 目录的快捷方式，以便你可以轻松访问 DVD 的内容，如图 5-3 所示。

当你访问完 DVD 上的文件后，可以单击 Cafe_Scientifique 旁边的弹出图标（如图 5-3 所示），从 `/run/media/user1/Cafe_Scientifique` 目录卸载 DVD 并强制 DVD 驱动器弹出 DVD。

`iso9660` 文件系统类型不仅限于 CD 和 DVD。你还可以创建包含其他文件的映像文件，称为 ISO 映像。回想第 2 章中提到的，大多数可从 Internet 下载的操作系统软件，如 Linux 发行版，都提供为 ISO 映像文件。下载后，可以使用光盘刻录软件将 ISO 映像轻松写入 CD 或 DVD，或者由你的 Linux 系统挂载和访问。如果你下载了一个名为 `sample.iso` 的 ISO 映像，你可以将其作为环回设备挂载到 `/mnt` 目录，

![](img/c27875544958897d817484d558c208c8_234_0.png)

**图 5-3** 在 GNOME 桌面中访问 DVD

允许你的系统使用以下命令访问 *sample.iso* 文件的内容：

```
[root@server1 ~]# mount
[root@server1 ~]# mount -o loop -r -t iso9660 lala.iso /mnt
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/loop0 on /mnt type iso9660 (ro)
[root@localhost ~]# ls /mnt
setup.exe tools binares
[root@server1 ~]#_
```

然后，你可以操作、执行或编辑 /mnt 目录内的文件，或将文件从 /mnt 目录复制到另一个目录，以提取 ISO 映像文件的内容。

要从文件目录创建 ISO 映像，只需使用 **mkisofs** 命令即可。以下命令从 /data 目录中的所有信息创建一个名为 *newimage.iso* 的 ISO 映像，并额外支持 Joliet（-J）和 Rock Ridge（-R）标准：

```
[root@localhost ~]# mkisofs -R -o newimage.iso /data
[root@localhost ~]# mount -o loop -r -t iso9660 lala.iso /mnt
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
nfsrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/loop0 on /mnt type iso9660 (ro)
[root@server1 ~]#_
```

![](img/c27875544958897d817484d558c208c8_235_0.png)

在 Fedora 20 上运行 **mkisofs** 命令之前，你必须首先以 root 用户身份运行 **yum install genisoimage** 命令来安装 ISO 映像工具。

## 使用硬盘和 SSD

硬盘通常有三种类型：PATA、SATA 和 SCSI。PATA 硬盘必须设置为四种配置之一，每种配置都有不同的设备文件：

- 主盘主设备 (/dev/hda)
- 主盘从设备 (/dev/hdb)
- 副盘主设备 (/dev/hdc)
- 副盘从设备 (/dev/hdd)

SATA 和 SCSI 硬盘通常比 PATA 硬盘具有更快的数据传输速度，并且大多数系统允许连接超过四个 SATA 或 SCSI 硬盘。由于这些优势，SATA 和 SCSI 硬盘非常适合需要大量存储空间来存放程序和用户文件的 Linux 服务器。然而，SATA 和 SCSI 硬盘具有不同的关联设备文件：

- 第一个 SCSI 硬盘驱动器 (/dev/sda)
- 第二个 SCSI 硬盘驱动器 (/dev/sdb)
- 第三个 SCSI 硬盘驱动器 (/dev/sdc)
- 第四个 SCSI 硬盘驱动器 (/dev/sdd)
- 第五个 SCSI 硬盘驱动器 (/dev/sde)
- 第六个 SCSI 硬盘驱动器 (/dev/sdf)
- 以此类推

SSD 是一种较新的技术，它使用速度更快的 NAND 闪存存储，但提供了与硬盘兼容的接口，因此可以作为硬盘的即插即用替代品。市场上大多数 SSD 都是 SATA 接口，并被 Linux 操作系统视为 SATA 硬盘。因此，/dev/sda 可以指第一个 SATA 硬盘或第一个 SATA SSD，/dev/sdb 可以指第二个 SATA 硬盘或第二个 SATA SSD，等等。

![](img/c27875544958897d817484d558c208c8_235_1.png)

为了简单起见，在本书余下的部分讨论永久存储时，我们主要指的是硬盘驱动器。然而，与硬盘驱动器相关的所有概念同样适用于 SSD。

