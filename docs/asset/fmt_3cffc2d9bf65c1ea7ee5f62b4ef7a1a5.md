
|---|---|---|---|---|---|---|

| `/dev/hda1` | 1 | 1 | 244 | 122944 | 83 | Linux native |

| `/dev/hda2` | 245 | 245 | 375 | 66024 | 82 | Linux swap |

| `/dev/hda3` | 376 | 376 | 1060 | 34520 | 83 | Linux native |

在这种情况下，有三个分区，其中一个是交换分区。

# 磁盘几何

上一节表格中的单位是柱面（cylinders）。分区表为每个分区分配一个连续的柱面块。“柱面”一术本身源于过去可以从 UNIX 机器上取出磁盘盒并指向其各个部分的时代。现在已经无法做到，所以这里有另一种看待方式。

想象硬盘实际上是一组披萨。每块披萨都是盘片（platter），这是一个带有磁性涂层的磁盘形表面，用于存储磁性编码。盘片的两都被使用。它们绕着主轴（唱片机上的轴）旋转。（不要把披萨放在唱片机上！）硬盘有一个活动臂，其中包含几个磁头。每个盘片的每个侧都有一个独立的磁头。如果你在保持手指伸直的同时将其插在披萨之间，这等同于臂上磁头的布局。磁盘旋转一圈时磁头经过的所有盘片部分称为一个柱面。单块盘片旋转一圈经过的部分称为轨道（track）。每条轨道被划分为*扇区*（sectors），就像披萨已经为磁盘切好了一样，它的*几何结构*（geometry）由组成磁盘的柱面、磁头和扇区的数量描述。另一个重要特性是磁盘的旋转速度——通常，速度越快，磁盘读写速度就越快。

你可以使用 `hdparm` 命令发现其中一个硬盘的几何结构，典型的输出可能如下：

```
# /sbin/hdparm -g /dev/hdc
/dev/hdc: geometry = 6232/16/63, sectors = 6281856, start = 0
```

> 带有旧版 BIOS 的 IBM PC 处理大磁盘可能会遇到困难；请参见 Linux-Large mini-HOWTO。

# 软磁盘

软盘是可拆卸的小容量存储介质。作为存储设备，它们远慢于硬盘，但它们的优点是可拆卸的，是传输少量数据的良好介质。

与磁盘对应的块设备以字母 `fd` 开头；`/dev/fd*` 是第一个，任何额外的设备都有递增的数字。软盘有许多可能的格式，内核需要知道磁盘的格式（几何结构）才能正确读取它。Linux 通常可以识别出正确的格式，因此自动设备 `/dev/fd`（加上 `/dev/fd1` 等）通常足够了，但由于某些原因，有必要指定精确格式，因此提供了设备名称来指示这一点。例如，设备 `/dev/fd0H140` 表示 1.44MB 的高密度软盘。还有许多表示晦涩格式的设备，包括旧的低容量格式和非标准的超高容量格式。你可以使用 `serfdpm` 程序创建自己的软磁盘格式。

使用特定格式设备名称的最常见原因是你正在首次格式化软盘。在这种情况下，磁盘是不可读的，因此内核无法自动探测现有格式。例如，你需要使用名称 `/dev/fd0H140` 来表示第一个软驱驱动器中的 3.5 英寸高密度磁盘。关于代表格式的设备名称，请参阅 `fd` 手册页。手册的第 4 节是专门介绍设备的章节。

格式化软盘的过程对其上的数据是完全破坏性的，并且因为它需要实际设备，所以它需要 root 权限。操作方法如下：

```
# mkfs.ext2 /dev/fd0H140
```

格式化后，你可以使用以下命令挂载磁盘：

```
# mount /dev/fd0140 /mnt
```

ISO960 标准规定了 CD-ROM 上数据的布局。为了兼容 MS-DOS，它将文件名限制在 32 个字符以内。为了支持符号链接和长文件名等功能，开发了一种名为 Rock Ridge 的扩展，Linux 内核会自动检测并利用。

# 文件系统、磁盘和其他设备

## 第11 章

CD-ROM 驱动器还支持音频播放，并且有 Linux 程序可以控制 CD-ROM，就像控制唱片机一样。Red Hat 的多媒体包包含 xray，用于播放 CD。为了使其工作，你需要将 `/dev/cdrom` 符号链接指向真实的 ROM 设备。

# 回环设备

回环设备允许将文件系统存储在普通文件中。你可能想为 DOSEMU 准备嵌入硬盘镜像、安装磁盘，或者在写入刻录机之前尝试新类型的文件系统或 ISO960 镜像。

# 在文件上挂载文件系统

在 UNIX 下，更改文件系统结构需要 root 权限；如果你拥有该文件以及挂载点，只有 root 可以这样做，除非 `/etc/fstab` 中为该文件系统指定了用户选项。

当使用回环驱动挂载文件系统时，文件包含了挂载命令和 `/etc/fstab` 中块设备的角色。内核与回环设备提供的块接口通信，驱动程序将操作转发给文件：

```
# mount $(pwd)/rtems.iso -t iso960 -o loop, /mnt/test
# mount | grep loop ; fold -s
/home/james/documents/books/Linux-Unleashed-2/ch/tmp/rtems.iso on
/mnt/test type iso960(loop,loop=/dev/loop0)
# umount /mnt/test
```

一旦挂载回环文件系统，它就是一个正常的文件系统。

## 使用加密文件系统

回环文件系统（Loopback filesystems）提供了更多功能——例如加密。回环文件系统可以配置为即时解密块设备上的数据，这样即使人们读取了设备上的数据，对他们也是无用的——除非他们拥有密码。`mount` 命令会在适当的时候提示输入密码。要使此工作运行，你首先使用 `mkfs` 在加密块设备上生成文件系统；并使用 `losetup` 将回环设备和加密与你想要使用的块设备关联（在例中为软驱）：

```bash
# /sbin/losetup -e DES /dev/loop0 /dev/fd1
Password:
Init (up to 16 hex digits):
# /sbin/mkfs -t ext2 -m /dev/loop0
mkext2 -i 1024 24-Apr-97 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem
Filesystem label=
360 inodes, 1440 blocks
0 blocks reserved for the super user
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
# losetup -d /dev/loop0
```

如前所述，`losetup -e` 将加密方法和块设备关联，而 `-d` 选项则解除这种关联并擦除存储的加密密钥。

在加密设备上创建文件系统后，可以以类似于普通情况的方式进行挂载：

```bash
# /sbin/losetup -d /dev/loop0
# mount /dev/fd1 -t ext2 -o loop=/dev/loop0,encryption=DES /mnt/test
Password:
Init (up to 16 hex digits):
# ls /mnt/test
lost+found
```

通常，通过向 `/etc/fstab` 添加适当的行，可以为普通用户设置使用加密文件系统的整个过程：

```bash
$ mount /mnt/test
Password:
Init (up to 16 hex digits):
$ ls -ld 3 bytes root 1024 Sep 14 22:04 /mnt/test
drwxrwxwx
```

在这个示例中，`root` 通过包含以下内容允许用户挂载加密文件系统：

```text
/dev/fd1 /mnt/test ext2 user,loop,encryption=DES
```

### 第 11 章

在 `/etc/fstab` 中包含。此外，软驱上顶层目录的所有权已交给用户 james，推测这是他的软驱。如果 `root` 没有这样做（赋予权限），`james` 将将能够挂载他的文件系统，但无法读取。这样做是至关重要的，但在本例中，`root` 犯了一个致命的错误。在更改文件系统根目录所有权的同时，`root` 也更改了目录的模式。这意味着一旦毫无防备的 james 提供了了他的秘密密码，系统上的任何用户都可以读取和写入软驱上的文件！这强调了仅凭加密不足以确保安全。仔细的考虑也是必不可少的。

在在上一个案例中，文件所有权和权限证明阻碍多于帮助。在加密设备上使用 MS-DOS 文件系统可能会更好，因为所有权会自动授予挂载磁盘的用户，并且文件模式是预设置好的：
