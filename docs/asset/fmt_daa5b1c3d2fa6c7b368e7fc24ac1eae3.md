
## CD-ROM 驱动器
ISO960 标准将文件名限制为 32 个字符。大多数 CD-ROM 为了兼容 MS-DOS 使用短文件名。为了支持符号链接和长等某些功能，开发了一套名为 *Rock Ridge* 的扩展，Linux 内核会自动检测并利用它们。CD-ROM 驱动器还支持音频 CD，并有 Linux 程序可以控制 CD-ROM，就像控制 CD 时代一样。Red Hat 的媒体包包含 `xplayed` 程序，可用于播放 CD。要使其工作，你需要将 `/dev/cdrom` 链接指向真实的 CD-ROM 设备。

## 回环设备
回环设备允许将新文件系统存储在普通文件中。你可能想这样做是为了为 DOS 准备硬盘镜像，或者只是在写入 CD 刻机之前尝试新类型的文件系统或 ISO9660 CD-ROM 镜像。

### 在文件上挂载文件系统
在 UNIX 下，更改文件系统结构需要 root 权限；如果你拥有文件以及你想挂载它的挂载点，只有 root 可以这样做，除非用户在 `/etc/fstab` 中拥有该文件系统的选项。

当使用回环驱动挂载文件系统时，文件包含了 `mount` 命令和 `/etc/fstab` 中块设备的角色。内核与回环设备提供的块设备接口通信，驱动程序对文件操作：

```
# mount $(pwd)/rtems.iso -t iso9660 -o loop,mnt/test

# ls -F /mnt/test

INSTALL README SUPPORT c/ doc/ rr_moved/

# mount | grep loop ; fold -s

/home/james/documents/Books/Linux-Unleased-2/ch/tmp/rtems.iso is on

/mnt/test type iso9660(loop=/dev/loop0)

# ummount /mnt/test
```

一旦挂载了回环文件系统，它就是一个普通的文件系统。

## 使用加密文件系统

回环文件系统（Loopback filesystems）提供了更多功能，例如加密。回环文件系统可以配置为从块设备即时解密数据，这样即使人们读取了设备上的数据，对他们也是无用的——除非他们拥有密码。`mount` 命令会在适当的时间提示输入密码。要实现这一功能，你首先必须使用 `mkfs` 在加密的块设备上生成文件系统；`losup` 曾将回环设备和加密与你想要使用的块设备关联（在下面的用例中是一个软驱）：

```
/sbin/losetext -e DES /dev/loop0 /dev/fd1
Password:

Init (up to 16 hex digits):
```

```
/sbin/mkfs -t ext2 -m /dev/loop0
mkfs -i 10, 24-Apr-97 for EXT2 FS 0.5b, 95/08/09

Linux ext2 filesystem format
Filesystem label=
360 inodes, 1440 blocks
blocks (0) reserved for the super user
First data block=1
Block size=1024 (log=0)
Fragment size=1024 (log=0)
1 block group
8192 blocks per group, 8192 fragments per group
360 inodes per group
```

写入索引表：
写入超级块和文件系统计数信息：完成
```
# losup -d /dev/loop0
```

如前所示，`losup -e` 将加密方法和块设备与回环设备关联。`-d` 选项则解除此关联并擦除存储的加密密钥。

在加密设备上创建文件系统后，可以以类似于正常情况的方式挂载：

```
/sbin/losup -d /dev/loop0
# mount /dev/fd1 -t ext2 -o loop /dev/loop0,encryption=DES /mnt/test
Password:

Init (up to 16 hex digits):
# ls /mnt/test

lostfound
```

通常，使用加密文件系统的整个过程可以通过在 `/etc/fstab` 中添加相应的行为普通用户设置：

```bash
$ mount /mnt/test

Password:

Init (up to 16 hex digits):
# ls -ld /mnt/test

drwxrxrwx 3 bytes root 1024 Sep 14 22:04 /mnt/test
```

在这个示例中，通过在 `/etc/fstab` 中包含以下内容，允许用户挂载加密文件系统：

```
/dev/fd1 /mnt/test ext2 user,loop,encryption=DES
```

此外，软驱上顶层目录的所有权已交给用户 `james`，推测这他的他的软驱。如果 `root` 没有这样做，`james` 将能够挂载他的文件系统但无法读取它。这样做是至关重要的，但在本例中，`root` 犯了一个致命的错误。`root` 在更改文件系统根目录所有权的同时，还更改了目录的模式。这意味着，一旦毫无防备的 `james` 提供了他极其秘密的密码，系统上的任何用户都可以读取和写入软驱上的文件！这强调了仅靠加密不足以保证安全的事实。仔细的考虑也是必不可少的。

在在上一个案例中，文件所有权和权限证明阻碍多于帮助。在加密设备上使用 MS-DOS 文件系统可能是更好的，因为所有权会自动授予挂载磁盘的用户，并且文件会被设置好：

```bash
$ ls -ld /mnt/floppy/

drwx-xr-x 2 james 7168 Jan 1 1970 /mnt/floppy/
```

这种策略仍然有两个问题。首先，无法在软驱上创建加密文件系统，因为 `mfsdos` 需要知道创建文件系统时的设备几何结构，而回环驱动程序并没有真正的几何结构。其次，一旦你的加密 `ext2` 文件系统挂载，超级用户仍然可以读取你的数据。

之前列出的加密方法在标准内核中是不可用的，因为大多数有用的加密技术在法律上无法从美国出口。然而，这些技术已经在美国境外可用，地址为 `ftp://ftp.replay.com/pub/linux/all/linux/linux-crypt-kernelpatches.gz`

这些补丁已经就绪了。你需要将这些补丁应用到你的内核并重新编译，以便配合回环设备使用 DES 和 IDE 加密方法。这些补丁是针对 Linux 内核 2.0.11 版本开发的，但它们与 Hat Linux 4.2 提供的内核配合得完美。

总结来说，加密文件系统对于某些类型的数据很有用（例如，以某种方式存储系统二进制文件的数字签名，使其无法被篡改），然而，对于 `root` 以外的其他人员，它们的实用性是有限的。不过当然，普通的文件加密机制对普通用户来说仍然可用且有用。

## 其他块设备

虽然硬盘、软驱器和 CD-ROM 驱动器是最常用的块设备，但还有其他类型的块设备需要考虑。这些包括内存磁盘（ramdisks）和 Zip 驱动

### 内存磁盘

内存磁盘是将数据存储在 RAM 而不是磁盘上的块设备。这意味着它们非常快；尽管如此，内存磁盘在 Linux 中很少使用，Linux 拥有非常

## 硬件与设备

字符设备提供必须顺序读取的数据流。块设备允许寻道到下一个数据块（例如从软驱的一侧跳到另一侧），而字符设备代表不具备这种能力的硬件。一个例子是终端，读取的下一个字符是你在键盘上输入的任何字符。

事实上，设备只有两种类型：块和字符。硬件被表示为其中一种，就像生物分类中的动物界和植物界一样。不可避免的是，这意味着某些设备并不符合这种分类方案。示例包括磁带驱动、通用 SCSI 设备以及 `/dev/port` 和 `/dev/kmem` 等特殊设备。

> 注意
> 网络接口的表示方式不同；参见第 13 章。

### 并行端口

并行端口通常用于与打印机通信，尽管它们足够支持其他事物——例如 Zip 驱动器、CD-ROM 驱动器甚至网络。

硬件本身提供逐字符的通信。并行端口可以提供中断来通知内核它已准备好输出新字符，因为在大多数 PC 上打印机通常不是性能敏感型的，这种中断经常被借用于其他硬件（通常是软硬件）。这产生了一个遗憾的后果：内核需要轮询并行硬件，因此驱动并行打印机中断比所需的更多的 CPU 工作。

好消息是，如果你的并行打印机中断没有被其他硬件占用，可以通过打印机驱动配置程序 `tunelp` 启用。`-i` 选项为每个打印机设备设置 IRQ。你可以这样设置打印端口的 IRQ 为 7：

```
/usr/sbin/tunelp /dev/lp1 -i 7
/dev/lp1 using IRQ 7
```

如果这导致打印机停止工作，回到轮询方法非常简单：

```
/usr/sbin/tunelp /dev/lp1 -i 0
/dev/lp1 using polling
```
