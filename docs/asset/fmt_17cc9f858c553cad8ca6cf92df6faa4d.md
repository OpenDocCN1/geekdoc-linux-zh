
沙箱系统将位于用户空间的一个 `chroot` 内部。内核与主机系统共享，因此沙箱不允许对内核进行实验。此外，我不应该错过警告 `chroot`s 安全影响的机会。许多来源认为运行在 `chroot` 中的软件具有更高的安全性，因为它被限制在沙箱内，无法触碰主机系统。然而，在 Linux 中，如果在 `chroot` 内部没有获得 `root` 权限的情况下，跳出 `chroot` 是至关重要的。虽然 `chroot`s 提供了逻辑隔离并可以简化管理，但它们并不构成安全围栏，充其量是一个屏障。对于我们的目的，`chroot` 并不打算提供安全监狱，因此我们不需要担心安全问题。

> http://www.bpf.net/imes/computing/chroot-break.html

`chroot` 程序为我们的目的启动一个具有不同根目录的命令。因此，第一步是为我们的目的创建一个新的指定根目录。注意，`chroot` 的使用为 `root` 用户保留，没有实际的理由让 `chroot` 存在于用户的家目录下。在下文中，我们将 `/home/chroots/sarge` 指定为沙箱。如果你需要为用户提供自己的沙箱，User-Mode Linux 是你正在寻找的。然而，User-Mode Linux 有许多 bug，可能不适用于所有应用程序。替代方案是 Xen，一种用于 Intel 架构的高性能虚拟机。`xen` 包提供了它，并且可以在线找到相关文档。

`bootstrap` 工具安装 Debian 基础系统，并为你留存了一套软件包，这与从可启动介质进行常规安装相同。必要的包可以通过两种方式获得：最简单的方法是使用 `bootstrap` 连接到 Debian 镜像服务器并让它发挥作用。另一种方法是使用 `basedebs`，这是一个包含基础系统所需包的文件。这一程序是引导软盘时代的遗迹，`bootstrap` 仍然支持它。对于 sarge 及其此后的版本，你必须自己创建该文件。

以下命令安装沙箱。请确保你使用的是最近的镜像，而不是示例中引用的：

```
# cd /home/chroots
# MIRROR=http://ftp.debian.org
# bootstrap sarge /sarge $MIRROR
# cd:
# bootstrap --arch i386 --download-only sarge $MIRROR
# tar cz -f basedebs.tgz var
# bootstrap --unpack-tarball 'pwd'/basedebs.tgz sarge /sarge
```

当 `bootstrap` 完成后，你可以进入新的沙箱并配置基础系统。我们不需要担心分区、网络、内核和引导加载程序或键盘配置，因为所有都由主机处理。`chroot` 仅仅是它的名称，带有一套不同的已安装包、一个独立的 `/etc` 层次结构和一个干净的数据库。它不是一个独立的安装。`base-config` 程序将询问几个问题来配置基础系统的基本方面。

```
# rm sarge/etc/resolv.conf
# cp /etc/resolv.conf sarge/etc
```

要找到最近的镜像，请使用 http://www.debian.org/mirror/ 上的官方列表，或运行 `apt-cache` 工具（见第 5.4 章）。

> 6 http://www.debian.org/doc/manual/user-guide/usermode-linux

> 7 http://www.debian.org/mirror/

> 8 http://www.debian.org/mirror/

在 `/etc/fstab` 中，必须列出新磁盘的分区。下面包含了适用于上述配置的最终且有效的 `fstab`。请注意可移动介质的挂载点选择。FHS（文件系统层次结构）定义 `/media` 作为 `/cdrom`、`/floppy` 或 `/mnt` 下子目录的替代。

```
# cat /etc/fstab
# /etc/fstab: static file system information.
#
# <fs>            <mount point> <type>  <options>               <dump> <pass>
proc             proc          defaults                               0       0
/dev/hda2        xfs           swap                               0       0
/dev/sda1        boot          xfs       noatime,nodev,nosuid,noexec 0       2
/dev/sda5        xfs           noatime                               0       2
/dev/hda6        /usr          xfs       noatime,nodev                         0       2
/dev/hda7        /local        xfs       noatime,nodev,nosuid                  0       2
/dev/hda8        /var          xfs       nodev,nosuid                          0       2
/dev/hda9        home          xfs       nodev,nosuid                          0       2
/dev/sda10       /tmp          xfs       iso9660  ro,user,autounct     0       2
/dev/hdc        /media/cdrom xfs       nodev,autounct                     0       0
/dev/fd0         /media/floppy auto        rw,noatime,nosync     0       0
```

第四列中的挂载选项非常优越，有助于提高安全性，特别是在用户访问机器时。`nodev`、`nosuid` 和 `noexec` 分别防止创建设备节点、防止设置 `setuid` 位的二进制文件以及防止执行脚本和程序。`noatime` 选项通过防止更新文件访问时间来略微提升性能。我还通过 `sync` 选项挂载了软驱器进行同步访问，以防止数据丢失。

文件所引用的空间在使用之前必须初始化。请务必小心以下命令，一个拼写错误可能会破坏你刚刚创建的 `chroot`（或整个硬盘）：

```
# mkswap /dev/hda2
```

## 安装内核

为了让系统启动，需要安装内核。虽然可以遵循标准的内核安装程序，但你会在 Debian 归档中发现各种版本和优化的 Linux 内核以普通的 `DEB` 文件存在。内核包的安装过程必须与运行中的内核通信，并需要访问 `/proc` 文件系统，该文件系统是由运行的内核提供的虚拟文件系统（见第 8.3.1 节）。因此，在使用 `apt-get` 安装 Debian 内核之前，必须挂载 `/proc`：

```
# mount /proc
# apt-get install kernel-image-2.6.8-1-k7
[...]
```

## 8 高级概念

如果 `chroot` 中安装的内核与运行中的内核不同，在 `chroot` 内部工作时可能会遇到问题。例如，`depmod` 将无法找到运行内核的模块树。然而，这些错误通常不会引起严重问题。
