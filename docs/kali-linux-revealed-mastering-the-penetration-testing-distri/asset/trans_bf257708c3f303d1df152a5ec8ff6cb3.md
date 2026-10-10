

由于修改启动菜单是一项非平凡的任务，Kali 默认包含两个启用持久性的菜单项：Live USB Persistence（USB 持久性）和 Live USB Encrypted Persistence（加密 USB 持久性），如图 9.1“持久性菜单项”[第 240 页]所示。

![](img/46e3313ea1bb2892f3146304f0677b8_266_0.png)

*图 9.1 持久性菜单项*

当启用此功能时，*live-boot* 将扫描所有分区，寻找标记为 *persistence*（持久性）的文件系统（可以通过启动参数 *persistence-label=value* 覆盖该标签），并且安装程序将设置在该分区的 *persistence.conf* 文件中列出的目录（每行一个目录）的持久性。特殊值“/ union”启用所有目录的完全持久性，使用 *union mount*（联合挂载），这是一种仅存储与底层文件系统相比发生变化的覆盖层。持久目录的数据存储在与相应 *persistence.conf* 文件所在相同的文件系统中。

## 9.4.2. 在 USB 键上设置未加密持久性

在本节中，我们假设您已按照 2.1.4 节“将镜像复制到 DVD 或 USB 键”[第 19 页]的说明准备好了 Kali Live USB 键，并且您使用了足够大的 USB 键来容纳 ISO 镜像（大约 3 GB）以及您想要持久化的目录数据。我们还假设 Linux 识别该 USB 键为 /dev/sdb，并且它仅包含默认 ISO 镜像中的两个分区（/dev/sdb1 和 /dev/sdb2）。在执行此过程时请非常小心。如果您重新分区错误的磁盘，可能会轻易销毁重要数据。

要添加新分区，您需要知道所复制镜像的大小，以便使新分区在 live 镜像之后开始。然后使用 parted 实际创建该分区。以下命令分析了名为 kali-linux-2016.1-amd64.iso 的 ISO 镜像，假设该镜像也存在于 USB 键上：

```
# parted /dev/sdb print
Model: SanDisk Cruzer Edge (scsi)
Disk /dev/sdb: 32,0GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start   End     Size    Type  File system  Flags
 1      32,8kB  2852MB  2852MB  primary        boot, hidden
 2      2852MB  2945MB  93,4MB  primary
# start=$(du -b --block-size=1MB kali-linux-2016.1-amd64.iso | awk '{print $1}')
# echo "Size of image is $start MB"
Size of image is 2946 MB
# parted -a optimal /dev/sdb mkpart primary "${start}MB" 100%
Information: You may need to update /etc/fstab.

```

```
# parted /dev/sdb print
Model: SanDisk Cruzer Edge (scsi)
Disk /dev/sdb: 32,0GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start   End     Size    Type  File system  Flags
 1      32,8kB  2852MB  2852MB  primary        boot, hidden
 2      2852MB  2945MB  93,4MB  primary
 3      2946MB  32,0GB  29,1GB  primary

```

在新的 /dev/sdb3 分区就位后，使用 mkfs.ext4 命令将其格式化为标记为 "persistence" 的 ext4 文件系统（并使用其 -L 选项设置标签）。然后该分区被挂载到 /mnt 目录，您添加所需的 persistence.conf 配置文件。一如既往，格式化任何磁盘时都要谨慎。如果格式化了错误的磁盘或分区，您可能会丢失宝贵信息。

```
# mkfs.ext4 -L persistence /dev/sdb3
mke2fs 1.43-WIP (15-Mar-2016)
Creating filesystem with 7096832 4k blocks and 1777664 inodes
Filesystem UUID: dede20c4-5239-479a-b115-96561ac857b6
Superblock backups stored on blocks:
		32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
		4096000

Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
# mount /dev/sdb3 /mnt
# echo " / union" >/mnt/persistence.conf
# ls -l /mnt
total 20
drwx------ 2 root root 16384 May 10 13:31 lost+found
-rw-r--r-- 1 root root     8 May 10 13:34 persistence.conf
# umount /mnt
```

USB 键现在已准备就绪，可以使用“Live USB Persistence”启动菜单项进行启动。

## 9.4.3. 在 USB 键上设置加密持久性

Live-boot 也能够处理加密分区上的持久性文件系统。因此，您可以通过创建保存持久性数据的 LUKS 加密分区来保护持久目录数据的机密性。

初始步骤直到创建分区为止都相同，但不要使用 ext4 文件系统格式化它，而是使用 cryptsetup 将其初始化为 LUKS 容器。然后打开该容器，并以与非加密设置相同的方式在内部设置 ext4 文件系统，但要使用 cryptsetup 创建的虚拟分区，而不是使用 /dev/sdb3 分区。此虚拟分区代表加密分区的解密内容，它在 /dev/mapper 下以您分配的名称可用。在下方的示例中，我们将使用名称 kali_persistence。再次确保您使用的是正确的磁盘和分区。

```
# cryptsetup --verbose --verify-passphrase luksFormat /dev/sdb3

WARNING!
=========
This will overwrite data on /dev/sdb3 irrevocably.

Are you sure? (Type uppercase yes): YES
Enter passphrase:
Verify passphrase:
Command successful.
# cryptsetup luksOpen /dev/sdb3 kali_persistence
Enter passphrase for /dev/sdb3:
# mkfs.ext4 -L persistence /dev/mapper/kali_persistence
mke2fs 1.43-WIP (15-Mar-2016)
Creating filesystem with 7096320 4k blocks and 1774192 inodes
Filesystem UUID: 287892c1-00b6-43cb-b513-81cc9e6fa72b
Superblock backups stored on blocks:
		32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
		4096000

Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
# mount /dev/mapper/kali_persistence /mnt
# echo "/ union" >/mnt/persistence.conf
# umount /mnt
# cryptsetup luksClose /dev/mapper/kali_persistence
```

## 9.4.4. 使用多个持久性存储

如果您的 Kali live 系统有多种用例，您可以使用带有不同标签的多个文件系统，并在启动命令行上指明用于持久性功能的（一组）文件系统：这可以通过启动参数 persistence-label=*label* 来完成。

假设您是一名专业的渗透测试人员。当您为客户工作时，您使用加密持久性分区来保护数据的机密性，以防 USB 键被盗或受损。同时，您希望能够展示 Kali 以及存储在同一个 USB 键未加密分区中的一些宣传材料。由于您不想在每次启动时手动编辑启动参数，您希望构建一个带有专用启动菜单项的自定义 live 镜像。

第一步是构建自定义 live ISO（遵循 9.3 节“构建自定义 Kali Live ISO 镜像”[第 236 页]，特别是 9.3.4 节“使用钩子调整镜像内容”[第 238 页]）。主要的自定义是修改 kali-config/common/hooks/live/persistence-menu.binary，使其看起来像这样（注意 persistence-label 参数）：

```
#!/bin/sh

if [ ! -d isolinux ]; then
	cd binary
fi
cat >>isolinux/live.cfg <<END

label live-demo
menu label ^Live USB with Demo Data
linux /live/vmlinuz
initrd /live/initrd.img
append boot=live username=root hostname=kali persistence-label=demo persistence

label live-work
menu label ^Live USB with Work Data
linux /live/vmlinuz
initrd /live/initrd.img
append boot=live username=root hostname=kali persistence-label=work persistence-encryption=luks persistence

END
```

接下来，我们将构建自定义 ISO 并将其复制到 USB 键。然后我们将创建并初始化两个将用于持久性的分区和文件系统。第一个分区未加密（标签为“demo”），第二个分区加密（标签为“work”）。假设 /dev/sdb 是我们的 USB 键，且自定义 ISO 镜像的大小为 3000 MB，它看起来会像这样：

```
# parted /dev/sdb mkpart primary 3000 MB 55%
# parted /dev/sdb mkpart primary 55% 100%
# mkfs.ext4 -L demo /dev/sdb3
[...]
# mount /dev/sdb3 /mnt
# echo "/ union" >/mnt/persistence.conf
# umount /mnt
# cryptsetup --verbose --verify-passphrase luksFormat /dev/sdb4
[...]
# cryptsetup luksOpen /dev/sdb4 kali_persistence
# mkfs.ext4 -L work /dev/mapper/kali_persistence
[...]
# mount /dev/mapper/kali_persistence /mnt
# echo "/ union" >/mnt/persistence.conf
# umount /mnt
# cryptsetup luksClose /dev/mapper/kali_persistence
```

就这样了。现在您可以启动 USB 键，并根据需要从新的启动菜单项中进行选择！

