

仅适用于系统管理员（因为它需要对包含待备份数据的底层块设备具有读取访问权限）。要将主目录的全部内容备份到软盘，请输入以下内容：

```
$ find $HOME -print0 | cpio --create -0 --format=crc > /dev/fd0
```

find 和 cpio 的 -print0 和 -0 选项确保待备份文件的文件名由 ASCII 空字符分隔，而不是换行符。这确保了任何包含换行符的文件名都能被正确备份。

> **注意**
> 
> UNIX 文件名中非法的唯一字符是斜杠和 ASCII 空字符。

Linux 的大多数备份工具都是专门为将备份写入任何类型的文件而编写的；事实上，它们是为顺序访问字符设备（如磁带驱动器）设计的。有关 Linux 可用各种备份程序的更多信息，请参见第 22 章“备份和恢复”。

## 文件系统

当您拥有多个数据项时，需要一种方法来组织块设备上的文件。这些方法称为*文件系统*。Linux 允许您选择任何组织方式来管理存储设备上的文件。例如，您可以在软盘上使用 MS-DOS 文件系统，或在硬盘上使用更快的 ext2 文件系统。

Linux 支持许多不同的文件系统；ext2 文件系统使用最为广泛，因为它是专为 Linux 设计的，且效率非常高。其他文件系统用于与其他系统的兼容性；例如，在软盘上使用 msdos 和 vfat 文件系统很常见；这些是 MS-DOS 和 Windows 95 的原生文件系统。在 Red Hat Linux 7 中，一些文件系统内置于内核：

```
$ cat /proc/filesystems
    ext2
nodev proc
    iso9660
nodev devpts
```

一些文件系统可作为可加载模块使用：

```
$ ls -x /lib/modules/`uname -r`/fs
```

autofs.o          binfmt_aout.o     binfmt_java.o     binfmt_misc.o
coda.o            fat.o             hfs.o             hpfs.o
lockd.o          minix.o           msdos.o           ncpfs.o
nfs.o            nfsd.o            nls_cp437.o       nls_cp737.o
nls_cp775.o      nls_cp850.o       nls_cp862.o       nls_cp865.o
nls_cp867.o      nls_cp869.o       nls_cp861.o       nls_cp866.o
nls_cp863.o      nls_cp864.o       nls_cp865.o       nls_cp869.o
nls_cp874.o      nls_cp922.o       nls_cp936.o
nls_cp949.o      nls_cp950.o       nls_iso8859-1.o   nls_iso8859-14.o
nls_iso8859-15.o nls_iso8859-2.o   nls_iso8859-3.o   nls_iso8859-4.o
nls_iso8859-5.o  nls_iso8859-6.o   nls_iso8859-7.o   nls_iso8859-8.o
nls_iso8859-9.o  nls_koi8-r.o      romfs.o           smbfs.o
sysv.o           ufs.o             umsdos.o          vfat.o

其中一些（nfs、ncpfs 和 smbfs）是网络文件系统，不依赖于块设备。网络文件系统在第 16 章“NFS：网络文件系统”和第 17 章“Samba”中进行了介绍。其他文件系统由 Linux 支持，但标准内核未提供。

## mount 命令

使用 mount 命令将块设备挂载到文件系统上。您需要指定包含文件系统的设备、其类型以及在目录层级中挂载它的位置。

mount 命令看起来像这样：

```
mount -t type -o options device mount-point
```

device 应该是一个块设备，或者如果它包含冒号，它可以是另一个机器的名称，从中挂载文件系统（参见第 16 章）。mount-point 应该是一个现有目录（否则会报错）；文件系统将出现在此位置。（该目录中之前存在的内容将被隐藏。）文件系统类型和选项是可选的，选项的多样性和含义取决于正在挂载的文件系统类型。如果要挂载的文件系统指定在 /etc/fstab 文件中，您只需指定挂载点或设备名称；mount 将从 /etc/fstab 中读取其他详细信息。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_618_0.png)

在浏览文件系统时，并不总是很容易快速区分空设备和未挂载任何设备的挂载点。使这种情况更简单的一个好方法是在每个作为挂载点的目录中创建一个名为 "filesystem not mounted" 的文件。这样，您可以立即看到挂载点上是否有设备挂载。

以下是使用 mount 命令的一个示例：

```
# ls /mnt/floppy
filesystem not mounted
# mount -t vfat /dev/fd1 /mnt/floppy
mount: block device /dev/fd1 is write-protected, mounting read-only
# ls /mnt/floppy
grub-0.4.tar.gz
# umount /mnt/floppy
# ls /mnt/floppy
filesystem not mounted
```

在这个示例中，我列出了 /mnt/floppy 挂载点中的文件。我发现没有挂载软盘，因此我在该挂载点挂载了一张包含 vfat 文件系统的软盘。我收到一条信息提示该软盘受写保护；如果软盘未受写保护，则不会出现此消息。目录 /mnt/floppy 已经存在。我使用 ls 查看软盘上的内容，并使用 umount 命令再次卸载它。然后我再次运行 ls，得到的响应只是我留在硬盘 /mnt/floppy 目录中的一个文件的名称，用以提醒我目前那里没有挂载任何内容。这个提示使我能够区分已写入的软盘和挂载的空软盘。您也可以使用 df 命令查看已挂载的文件系统。例如：

```
# mount -t vfat /dev/fd0 /mnt/floppy
# df /mnt/floppy
Filesystem           1k-blocks     Used Available Use% Mounted on
/dev/fd0                1423        0      1423   0% /mnt/floppy
# umount /mnt/floppy
# df /mnt/floppy
Filesystem           1k-blocks     Used Available Use% Mounted on
/dev/hda6              202006   1850753    72493  96% /
```

如您所见，当设备挂载到挂载点上时，df 将输出该设备的统计信息；否则，它将输出该目录所在设备的统计信息。

如前所述，挂载 vfat 软盘会导致 Linux 内核在需要时自动将 vfat 驱动程序加载到内核中。内核模块处理器负责加载这些驱动程序，并且当文件系统卸载后这些驱动程序不再被使用时，它们会被卸载以回收其占用的内存。有关内核模块的更多信息，请参见第 27 章“配置和构建内核”。

### mount 的潜在问题

几种情况都可能导致 mount 命令失败，例如：

- **错误的设备名称**——可能会指定错误的设备名称（即，不存在的设备文件，或内核中没有可用驱动程序的设备，或硬件不存在的设备）。
- **不可读设备**——设备不可读可能是因为设备本身有问题（例如，空的软盘驱动器或损坏的介质），或者是因为您没有足够的权限挂载它们。除管理员通过 /etc/fstab 中的 user 选项列出的文件系统外，普通用户被禁止挂载其他文件系统，并且需要 root 权限才能挂载。
- **错误的挂载点**——尝试在尚未存在的挂载点上挂载设备将不起作用。
- **其他错误**——还可能存在更多但不太可能的错误条件（例如，超过编译时设定的已挂载文件系统数量限制）或不言自明的错误（例如，mount 命令本身的大多数使用错误）。还有一些不太可能的错误消息主要涉及回环设备。

当您挂载文件系统时，挂载点（即文件系统要挂载的位置）必须是一个目录。该目录不必为空，但在文件系统挂载后，其下的任何内容都无法访问。Linux 提供单根文件系统，这与赋予每个文件系统独立驱动器号的操作系统形成对比。这样更灵活，因为块设备（硬盘或其他设备）的数据大小对程序来说是隐藏的，且内容可以移动。例如，如果您有一些软件期望安装在 /opt/umsp，您可以将其安装在 /big-disk/stuff/umsp，并创建 /opt/umsp 作为符号链接。安装新的磁盘驱动器后，也无需编辑大量使用错误驱动器号的配置文件。

许多选项控制已挂载文件系统的行为；例如，可以只读方式挂载。对于 msdos 等没有用户概念的文件系统，也有相应的选项。这些文件系统允许您为每个文件赋予特定的文件模式（出于安全考虑或允许所有人访问）。当您挂载 nfs 文件系统时，灵活性非常高，选项有单独的 man 页面（man nfs），尽管默认值完全合理。nfs 文件系统在第 16 章中有更详细的说明。（注：原文此处写为 nft，根据上下文和常见语境应为 nfs）

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_620_0.png)

