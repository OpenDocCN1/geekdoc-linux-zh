
| :--- | :--- | :--- | :--- | :--- |
| `/dev/hda7` | `/boot` | `ext3,user_xattr` | `1` | `2` |
| `/dev/hda6` | `/data1` | `auto,user` | `0` | `0` |
| `/dev/hda9` | `/data2` | `auto,user` | `0` | `0` |
| `/dev/hda10` | `/data3` | `auto,user` | `0` | `0` |
| `/dev/hda5` | `/data4` | `auto,user` | `0` | `0` |
| `/dev/hda2` | `/windows` | `ntfs ro,users,gid=users,umask=0002,ls=utf8` | `0` | `0` |
| `/dev/hda8` | `swap` | `swap pri=4` | `0` | `0` |
| `dev/pts` | `/dev/pts` | `mode=0620,gid=5` | `0` | `0` |
| `/proc` | `/proc` | `defaults` | `0` | `0` |
| `/dev` | `/dev` | `defaults` | `0` | `0` |
| `/sys` | `/sys` | `defaults` | `0` | `0` |
| `/dev/cdrom` | `/media/cdrom` | `ro` | `0` | `0` |

## 在文件系统上挂载设备

你在 Linux 中使用的存储设备包含 Linux 文件系统，了解这一点对于日常工作是有益的，但对于考试学习来说是必要的。每个设备都有其自己的本地文件系统，由层次分明的目录结构组成。在访问设备上的文件之前，你必须将设备的目录层次结构挂载到代表整个 Linux 文件系统的树上。

*挂载*（Mounting）是你执行的操作，目的是使物理存储设备（硬盘分区或 CD-ROM 光驱）上的文件系统显示为 Linux 文件系统的一部分。图 3-3 阐释了挂载的概念。

图 3-3 显示了每个以 `/dev` 开头的设备。在图中，`/dev/cdrom` 是第一个 DVD/CD-ROM 驱动器。物理设备挂载在 Linux 文件系统中特定的挂载点上。DVD/CD-ROM 驱动器 `/dev/cdrom` 挂载在文件系统的 `/media/cdrom` 上。在这样挂载 CD-ROM 后，CD-ROM 或 DVD-ROM 上的 Fedora 目录就会出现在 Linux 文件系统中的 `/media/cdrom/Fedora`。

图 3-3：在访问设备之前，你必须在 Linux 文件系统上挂载设备。

![](img/3e16ea99a8df672d45599724c19769ac_419_0.png)

## 管理文件系统

你可以使用 `mount` 命令将设备手动挂载指定的目录 Linux 文件系统。该目录就是*挂载点*（mount point）。要将 DVD/CD-ROM 驱动器挂载到 `/media/cdrom` 目录，请输入以下命令（以 root 登录）：

```
mount /dev/cdrom /media/cdrom
```

如果 DVD/CD-ROM 设备已经挂载或驱动器中没有 CD 或 DVD，`mount` 命令将报告错误。否则，`mount` 操作成功，你可以通过 `/media/cdrom` 目录访问 DVD 或 CD 的内容。

你可以使用任何目录作为挂载点。然而，如果你将设备挂载到一个非空目录，在在使用 `umount` 命令卸载设备之前，你无法访问该目录中的文件。因此，请始终使用空目录作为挂载点。

当你不再需要某个设备时，使用 `umount` 命令卸载它。对于设备名为 `/dev/cdrom` 的 DVD/CD-ROM 设备，输入以下命令卸载设备：

```
umount /dev/cdrom
```

只要没有在使用 DVD/CD-ROM，`umount` 命令就会成功。如果你在尝试卸载 DVD/CD-ROM 时遇到错误，请检查当前工作目录是否在 DVD 或 CD 上。如果你当前正在 DVD/CD-ROM 的某个目录中工作，这也属于正在使用 DVD/CD-ROM。

### 检查 /etc/fstab 文件

`mount` 命令具有以下通用格式：

```
mount device-name mount-point
```

只要 `/etc/fstab` 文件包含 CD-ROM 挂载点的条目，你就可以通过指定 CD-ROM 设备名称或 `mount-point` 名称来进行挂载。该条目指定了 CD-ROM 设备名称和文件系统类型。这就是为什么你可以用较短的 `mount` 命令挂载 CD-ROM。

在 Debian 中，你可以通过输入以下命令之一来挂载 CD-ROM：

```
mount /dev/cdrom
```
```
mount /media/cdrom
```

`/etc/fstab` 文件是一个*配置文件*（configuration file——一个包含 `mount` 和 `umount` 命令用信息的文本文件。`/etc/fstab` 文件中的每一行都提供了关于设备及其在 Linux 文件系统中挂载点的信息。本质上，`/etc/fstab` 文件将文件系统内的各种挂载点与特定设备关联起来，使得 `mount` 命令仅需挂载点或设备作为参数即可从命令行工作。

这是一份来自 SUSE 系统的 `/etc/fstab` 文件。（其他 Linux 发行版中的文件具有类似的格式。）

| device | mount point | options | fs | pass |
| :--- | :--- | :--- | :--- | :--- |
| `/dev/hda7` | `/boot` | `ext3,user_xattr` | `1` | `2` |
| `/dev/hda6` | `/data1` | `auto,user` | `0` | `0` |
| `/dev/hda9` | `/data2` | `auto,user` | `0` | `0` |
| `/dev/hda10` | `/data3` | `auto,user` | `0` | `0` |
| `/dev/hda5` | `/data4` | `auto,user` | `0` | `0` |
| `/dev/hda2` | `/windows` | `ntfs ro,users,gid=users,umask=0002,ls=utf8` | `0` | `0` |
| `/dev/hda8` | `swap` | `swap pri=4` | `0` | `0` |
| `dev/pts` | `/dev/pts` | `mode=0620,gid=5` | `0` | `0` |
| `/proc` | `/proc` | `defaults` | `0` | `0` |
| `/dev` | `/dev` | `defaults` | `0` | `0` |
| `/sys` | `/sys` | `defaults` | `0` | `0` |
| `/dev/cdrom` | `/media/cdrom` | `ro` | `0` | `0` |

---

通过 NFS 共享文件非常简单，涉及两个基本步骤：

- 在 NFS 服务器上，通过在 `/etc/exports` 文件中列出目录并运行 `/usr/sbin/exportfs` 命令来导出一个或多个目录。。
- 在每个客户端系统中，使用 `mount` 命令挂载服务器导出的目录。

如何启动 NFS 服务取决于 Linux 发行版。如果提供了图形界面（GUI）`sysadmin` 工具，你可以从该工具启动 NFS 服务。否则，你可以在终端中输入命令启动 NFS 服务：

- 在 Debian 中，你可以输入 `invoke-rc.d nfs-kernel-server start` 和 `invoke-rc.d nfs-common start` 来启动 NFS 服务。
- 在 Fedora 中，输入 `service nfs start`。
- 在 SUSE 中，你可以使用 YaST 控制中心。从主菜单开始，选择 应用程序启动器➪ YaST➪ 系统➪ 服务（级别）。

使用 NFS 的唯一问题是每个客户端系统必须支持它。大多数 PC 不带 NFS，这意味着如果你想用 NFS 共享文件，就需要单独购买 NFS 软件。然而，如果你局域网（LAN）上的所有系统都运行 Linux 或内置 NFS 支持的 Unix 变体，那么使用 NFS 是合理的。

NFS 存在安全漏洞。因此，不要在直接连接互联网的系统上设置 NFS；务必在它们与互联网之间放置一个防火墙。

接下来的章节将带你完成一次 NFS 设置，并以局域网上的两台 Linux 电脑作为例。

## 使用 NFS 导出文件系统

要使用 NFS 导出文件系统，首先从一个*导出*（即向客户端系统提供）目录内容的服务器系统开始。在服务器上，你必须运行 NFS 服务，并指定一个或多个要导出到客户端系统的文件系统。

你必须在 `/etc/exports` 文件中添加适当的条目。假设你想导出 `/home` 目录，并且你想允许主机 `LNBP75` 挂载该文件系统以进行读写操作。（你可以使用主机的 IP 地址代替主机名）。你可以通过向 `/etc/exports` 文件中添加以下条目来实现：

```
/home LNBP75(rw)
```

如果你使用主机的 IP 地址，该条目可能如下所示：
