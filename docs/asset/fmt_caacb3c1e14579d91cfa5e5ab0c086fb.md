
## 第 5 章 文件系统管理

创建文件系统最常用的命令是 `mkfs`，你可以使用该命令的其他变体和快捷方式。例如，要创建一个 `ext2` 文件系统，可以输入 `mkfs /dev/sdb1`。`mkfs` 命令的替代方案列在表 5-3 中。

### 5-3 创建文件系统的命令

| 命令 | 创建的文件系统 |
|---|---|
| `mkfs` | |
| `mkfs.msdos` | FAT (12, 16 或 32 位，取决于文件系统的大小) |
| `mkfs.fat` | |
| `mkfs.vfat` | |
| `mkfs.ext2` | `ext2` |
| `mk2fs` | |
| `mkfs.ext3` | `ext3` |
| `mkfs.ext4` | |
| `mk2fs -t ext4` | `ext4` |
| `mkofs` | ISO |
| `mkfs.xfs` | XFS |
| `mkfs.udfs` | UDF |
| `mkfs.udf` | |
| `mkfs.ntfs` | |
| `mkfs.ntfs` | |
| `mkfs.exfat` | exFAT |

在闪盘被格式化为文件系统后，必须将其挂载到目录才能使用。可以通过不带任何选项或参数的 `mount` 命令获取当前挂载的文件系统列表，它会读取 `/etc/mtab` 文件。在现代系统中，此命令的输出非常长，因为它包含了许多文件系统和系统参数。因此，使用 `lsblk` 命令或 `df` 命令查找当前挂载的文件系统要容易得多。`df` 命令的 `-T` 选项将显示文件系统类型，`-h` 选项显示易于阅读的格式，如下：

```
[root@server1 ~]# df -ht

Filesystem Size Avail Mounted On

tmpfs 4.0M 0.4M /dev/
```

| | Type | Size | Avail | % | Mounted on |
| --- | --- | --- | --- | --- | --- |
| tmpfs | tmpfs | 2.0G | 0 | 0% | /dev/shm |
| tmpfs | tmpfs | 784M | 1.2M | 783M | 1% | / |
| /dev/sda3 | ext4 | 35G | 8.9G | 24G | 28% | / |
| tmpfs | tmpfs | 2.0G | 8.0K | 2K | 1% | /tmp |
| /dev/sda2 | ext4 | 974M | 150M | 757M | 17% | /boot |
| /dev/sda1 | vfat | 599M | 14M | 585M | 3% | /boot/efi |
| tmpfs | tmpfs | 392M | 76K | 392M | 1% | /run/user/42 |
| tmpfs | tmpfs | 392M | 76K | 392M | 1% | /run/user/1000 |

从示例输出中你可以看到 `/dev/sda3` 上的文件系统挂载到了目录 `/`，`/dev/sda2` 上的 `ext4` 文件系统挂载到了 `/boot/efi`。列出的其他文件系统是由系统列出的：这些虚拟文件系统和伪文件系统将在书中后续部分讨论。

要挂载目录树，你可以使用带有选项和参数的 `mount` 命令来指定文件系统、要挂载的设备以及挂载它的目录。确保没有用户正在使用挂载点目录非常重要；否则系统会报错且不会操作设备。要检查 `/media/USBdrive` 目录是否被任何用户使用，你可以使用带有 `-u` 选项的 `fuser` 命令，如下所示：

```
[root@server1 ~]# fuser -u /media/USBdrive

[root@server1 ~]#
```

以下输出表示 `/media/USBdrive` 没有被任何进程使用；要将带有 `ext2` 文件系统的闪盘（`/dev/sda1`）挂载到此目录，你可以运行以下命令：

```
[root@server1 ~]# mount -t ext2 /dev/sda1 /media/USBdrive

[root@server1 ~]#
```

### Note

如果你在 `mount` 命令中省略 `-t` 选项，它将自动检测设备上的文件系统。`mount /dev/sda1 media/USBdrive` 命令执行的操作与上述输出所示的 `mount` 命令相同。

## Linux 文件系统管理

注意，在 `mount` 命令的前面输出中，`/dev/sdb1` 已挂载到 `/media/USBdrive`。要在 USB 闪盘上访问和存储文件，你现在可以将 `/media/USBdrive` USB 闪盘的根目录。在设备上创建 `ext2`、`ext3` 或 `ext4` 文件系统时，会创建一个名为 `lost-found` 的目录，该目录供本章后面讨论的 `fsck` 命令使用。要探索挂载的文件系统，可以使用以下命令：

```
[root@server1 ~]# cd /media/USBdrive

[root@server1 USBdrive]# pwd

/media/USBdrive

[root@server1 USBdrive]# ls -F

lost-found/
```

要将文件拷贝到 USB 闪盘，请将 `/media/USBdrive` 目录指定为 `cp` 命令的目标，如下：

```
[root@server1 USBdrive]# cd /etc

[root@server1 etc]# cat issue

Linux 5.4.0-generic

[root@server1 etc]# cp issue /media/USBdrive

[root@server1 USBdrive]# cd /media/USBdrive

[root@server1 USBdrive]# ls -F

issue lost-found/

[root@server1 USBdrive]# cat issue

Linux 5.4.0-generic
```

同样，你可以在 USB 闪盘下创建子目录来存储文件；这些子目录在挂载点目录下引用。要使上一个示例中的目录生效并使用 `/etc/inittab` 为其工作，可以使用以下命令：

```
[root@server1 USBdrive]# pwd

/media/USBdrive

[root@server1 USBdrive]# ls -F

issue lost-found/

[root@server1 USBdrive]# mkdir workfiles

[root@server1 USBdrive]# ls -F

issue lost-found/

[root@server1 USBdrive]# cd workfiles

[root@server1 workfiles]# pwd

/media/workfiles

[root@server1 workfiles]# cp /etc/inittab .

[root@server1 workfiles]# ls

inittab
```

即使你在没有断开系统的情况下拔除了 USB 闪盘，终端屏幕上也可能出现错误信息。在移除 USB 闪盘之前，必须使用 `umount` 命令正确卸载。`umount` 命令可以接受设备名称或挂载点作为参数。同样，如果你尝试在 USB 闪盘正在被挂载到 `/media/USBdrive` 时卸载一个没有使用的挂载点的设备，你会收到类似下面示例中的错误消息：

```
[root@server1]# cd /media/USBdrive

[root@server1]# umount /media/USBdrive

mount: /media/USBdrive: target is busy.

[root@server1]# fuser -u /media/USBdrive

/media/USBdrive:

17368(root)

[root@server1]# cd /root

[root@server1]# umount /media/USBdrive

[root@server1]# df -HT

Filesystem Type Size Used Avail% Mounted

devtmpfs 4.0M 0 4.0M 0% /dev

tmpfs 2.0G 0 2.0G 0% /dev/shm

tmpfs 784M 1.2M 783M 1% /run

/dev/sda3 ext4 35G 8.9G 24G /

tmpfs 2.0G 8.0K 2.0G 1% /tmp

/dev/sda2 ext4 974M 150M 757M 17% /boot

/dev/sda1 vfat 599M 32M 585M 3% /boot/efi

tmpfs 392M 92K 376M 19% /run/user

tmpfs 392M 76K 392M 1% /run/user/1000
```

注意前面的错误，你之所以正在使用 `/media/USBdrive` 是因为它是工作目录。`fuser` 命令也表明 root 用户有一个进程正在该目录。在更改工作目录后，`umount` 命令能够从 `/media/USBdrive` 目录卸载 USB 闪盘，命令的输出表明它不再被挂载。

回想，挂载是将设备连接到 Linux 目录树，这样你可以将设备视为充满文件和子目录的目录。可以挂载设备以访问其数据；但是，如果目录包含文件，当设备被卸载时，这些文件将无法访问。例如，如果你创建了一个名为 `/USBdrive` 的目录用于挂载 USB 闪盘，并在内部创建一个名为 `sample` 的文件，如下：

```
[root@server1]# mkdir /USBdrive

[root@server1]# touch /USBdrive/samplefile

[root@server1]# ls /USBdrive

samplefile
```

如果 USB 闪盘之前挂载到 `/USBdrive` 目录，使用 `/USBdrive` 目录的用户将使用驱动器上的文件系统；然而，当未挂载到 `/USBdrive` 目录时，以下内容是可用：

```
[root@server1]# mount /dev/sdb1 /USBdrive

[root@server1]# df -HT

Filesystem Type Size Used Avail% Mounted

devtmpfs 4.0M 0 4.0M 0% /dev

tmpfs 2.0G 0 2.0G 0% /dev/shm

tmpfs 784M 1.2M 783M 1% /run

/dev/sda3 ext4 35G 8.9G 24G /

tmpfs 2.0G 8.0K 2.0G 1% /tmp

/dev/sda2 ext4 974M 150M 757M 17% /boot

/dev/sda1 vfat 599M 32M 585M 3% /boot/efi

tmpfs 392M 92K 376M 19% /run/user

tmpfs 392M 76K 392M 1% /run/user/1000
```

| Filesystem | Type | Size | Used | Avail% | Mounted |
| :--- | :--- | :--- | :--- | :--- | :--- |
| devtmpfs | devtmpfs | 4.0M | 0 | 4.0M | 0% | /dev |
| tmpfs | tmpfs | 2.0G | 0 | 2.0G | 0% | /dev/shm |
| tmpfs | tmpfs | 784M | 1.2M | 783M | 1% | /run |
| /dev/sda3 | ext4 | 35G | 8.9G | 24G | / |
| tmpfs | tmpfs | 2.0G | 8.0K | 2.0G | 1% | /tmp |
| /dev/sda2 | ext4 | 974M | 150M | 757M | 17% | /boot |
| /dev/sda1 | vfat | 599M | 32M | 585M | 3% | /boot/efi |
| tmpfs | tmpfs | 392M | 92K | 376M | 19% | /run/user |
| tmpfs | tmpfs | 392M | 76K | 392M | 1% | /run/user/1000 |
| /dev/sdb1 | ext2 | 9M | 24K | 5G | /USBdrive |

前面使用的 `mount` 命令输出了文件系统类型、要挂载设备和挂载点目录。为了在命令行中减少输入，你可以指定一个参数并让系统在 `/etc/stab` 中查找剩余信息。`/etc/stab` 文件具有双重目的：它用于在启动时挂载设备以及当用户没有向 `mount` 命令提供足够参数时使用。`/etc/stab` 文件包含：

- `<device>`
- `<mountpoint>`
- `<options>`
- `<dump>`
- `<fsck>`

要挂载设备可以是文件路径（例如 `/dev/sda`）、文件系统 UUID（例如 `UUID=0b54f1cd-d2ee-4bc3-a614bd0`）、分区 UUID（例如 `PARTUUID=ed8358-1`）或文件系统标签（例如 `LABEL=Disk`）。挂载点指向设备应该挂载的目录。设备可以是特定类型（例如 `ext4`）或可以自动检测。挂载选项接受如 `volume`、检查次数或 `no`。任何带有 `auto` 挂载选项的文件系统在启动时自动挂载；可以通过查看 `mount` 命令的手页来找到该命令。

`dump` 字段供 `dump` 命令（第 11 章讨论）在备份文件系统时使用；`1` 表示应该备份该文件系统，而 `0` 表示不需要备份。`fsck` 字段供本章后面讨论的 `fsck` 命令在检查文件系统时使用；`1` 在数字为 2 的文件系统之前检查，数字为 0 的文件系统不检查。

**注意 9**：你可以使用 `blkid` 命令显示系统上的分区和文件系统 UUID。你也可以使用 `lsblk --fs` 显示文件系统 UUID 和标签。

**注意 10**：文件系统标签是可选的；要为文件系统设置标签，必须使用对应文件类型的命令。例如，可以使用 `e2label` 命令为 `ext2`/`ext3`/`ext4` 文件系统设置标签，可以使用 `fatlabel` 命令为 FAT 文件系统设置标签，可以使用 `xfs_admin` 命令为 XFS 文件系统设置标签。

为了将文件系统 UUID 与其标签关联，udev 为每个 UUID 和 `/dev/disk` 下的子目录创建符号链接指向正确的文件（例如 `/dev/sdb1`）；`/dev/disk-by-uuid` 符号链接、`/dev/disk-by-partuuid` 分区 UUID 符号链接以及 `/dev/disk-by-label` 符号链接。你也可以通过内核标识符（在 `/dev/disk/by-id 和 PCI id 下）找到磁盘的符号链接。

**注意 12**：要挂载 `/etc/fstab` 中所有旨在启动时挂载的文件系统，可以使用 `mount -a` 命令。

以下输出显示了示例 `/etc/fstab` 文件的内容：

```
[root@server1]# cat /etc/fstab

# 可访问文件系统通过引用维护在

# '/dev/disk/' 下。参见 fstab(5), find(8) 和/或

# blkid(8) 获取更多信息。

# 编辑此文件后，运行 systemctl daemon-reload 更新

# 由此文件生成的系统单元。

UUID=e8ffccfc-841a-b879-d7adb1fd1de94 / ext4 defaults 1 1

UUID=c203a16-e9b2-4577-aab5-5f35f0274 / / ext4 defaults 1 2

UUID=f4d6-9857 /boot/efi vfat umask=022 0 2

/dev/sdb /USBdrive auto mount 0 0
```

要将 USB 闪盘 (`/dev/sdb`) 挂载到 `USBdrive` 目录并自动检测设备的文件类型，请指定足够的信息让 `mount` 命令在 `/etc/fstab` 文件中找到相应的行：

```
[root@server1]# mount /USBdrive

[root@server1]# df -hT
```

```
/dev/sda vfat 599M 14M 585M 3% /boot/efi

tmpfs tmpfs 392M 92K 392M 1% /run/user/42

tmpfs tmpfs 392M 76K 392M 1% /run/user/0

tmpfs tmpfs 392M 76K 392M 1% /run/user/1000

/dev/sdb1 ext2 7.9G 24K 7.5G 1% /USBDrive

[root@server1 ~]# mount /USBDrive

[root@server1 ~]#
```
