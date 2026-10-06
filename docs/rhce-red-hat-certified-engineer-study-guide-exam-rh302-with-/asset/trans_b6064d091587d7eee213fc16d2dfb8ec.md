

如果你必须先安装 Linux 再安装 Microsoft Windows，请务必为 Windows 分区留出空间，该分区必须位于硬盘的可启动区域（通常是第 1024 磁道）。此外，请务必创建一个 Linux 启动盘，因为 Windows 安装程序会覆盖 MBR，从而破坏 LILO。在 Windows 安装完成后，使用启动盘启动 Linux，修改 LILO 配置以包含 `/sbin/l11o` 并重新安装 LILO。

> 你可能会发现使用 BIOS 关闭 ISA 插槽的即插即用功能对你有所帮助。否则，Windows 可能会使用即插即用更改与设备相关的系统资源，导致该设备在 Linux 中无法使用，直到你重新配置该设备。

查看练习 8.3 以确认你是否理解了如何配置一个可以启动 Linux 和 Windows 9x 的多引导系统。

| 练习 8.3 |
| 配置系统以启动 Linux 和 Windows 9x |
| 1. 使用 Windows 9x 和 Linux 配置用于多引导运行的系统。 |
| 2. 如果你有一台的 Windows 9x 笔记本，请在笔记本上安装 Linux 并将其配置为多引导运行。务必尝试安装并配置 XFree86。 |

## Windows NT

配置一个启动 Windows NT 和 Linux 的多引导系统比配置一个启动 Windows 9x 和 Linux 的多引导系统稍微困难一些。同样，如果你在安装 Linux 之前安装 Windows NT，你会发现任务变得更简单。然而，安装程序不会像对待 Windows 9x 那样自动配置系统启动 Windows NT。

你可以使用 Windows NT 加器启动 Linux。Windows NT 加器的配置存储在隐藏文件 `:\boot.ini` 中。以下是 NT 加器配置文件的示例：

```
[boot loader]
timeout=60
default=multi(0)disk(0)disk(1)partition(1)\WINNT
```

## 执行多引导安装 183

[operating systems]
multi(0)disk(0)disk(1)\WINNT="Windows NT
➥ Workstation Version 4.00
multi(0)disk(0)disk(1)\WINNT="Windows NT
➥ Workstation Version 4.00 [VGA mode] /basevideo/sos
c=\Microsoft Windows 95"

此配置包含两个由方括号标题定义的节。第一个节的标题为 `[boot loader]`。它包含两行：一行指定超时时间，另一行指定默认启动镜像。超时工作原理与 LILO 类似。如果 NT 在指定时间范围内没有收到对其提示的响应，它将自动启动启动镜像。默认启动镜像由磁盘 (rd) 和分区 (partition) 数字指定，这两个数字都是相对于 0 编号的。示例配置中的默认启动镜像位于该分区文件系统的 `\WINNT` 目录。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_205_0.png)

`.ini` 文件中的 `multi` 和 `disk` 参数用于 SCSI 磁盘。为了准备 RHCE 考试，你不需要学习这些 NT 细节。

第二个节标题为 `[operating systems]`。第二个节的每行都指定了一个启动镜像和一个关联标签，标签包含在双引号中。出现了两种指定形式：一种用于指定 NT 启动镜像，另一种用于指定非 NT 启动镜像。在示例配置中，前两行指定了 NT 启动镜像，第三行指定了非 NT 启动镜像。

要配置 NT 启动 Linux，请使用 LILO 作为次级加载器安装 Linux。务必创建一个启动盘，以便在重新配置 NT加载器之前启动 Linux。

假设 `/dev/hda3` 分区是 Linux 挂载为 `/boot` 的分区。启动并执行以下命令：

```
dd if=/dev/hda3 of=/boot/linux.ldr bs512 count=1
```

此命令将 `/boot` 分区的引导扇复制到文件 `/boot/linux.ldr`。

插入 MS-DOS 格式的软盘，并执行命令：

```
mount -t msdos /dev/fd0 /mnt/floppy
umount /boot/linux.ldr
unmount /dev/fd0
```
所有所有 ©2000 SYBEX, Inc., Alameda, CA

## 第 8 章 高级安装

移除软盘并启动 NT。插入软盘，将 `linux.ldr` 文件复制到 `c:\` 目录。使用文本编辑器在 `boot.ini` 文件中添加以下行：

```
c:\linux.ldr='Linux'
```

当你启动 NT 时，NT加载器会显示标记为 Linux 的新行。只需突出该行并按回车即可启动 Linux。

注意，如果 Windows NT 系统使用 FAT 而不是 NTFS，可以在不使用软盘的情况下将 `/boot/linux.ldr` 复制到 Windows NT 系统。挂载文件，复制文件，然后卸载文件。此外，如果你愿意，可以通过 LILO 启动 NT。只需在 LILO 配置中指定 `other` 和 `label` 指令。然后运行 `/sbin/lilo` 更新引导扇。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_0.png)

如果你重新编译 Linux 内核，必须运行 `/sbin/lilo` 并重复引导扇程序。否则，NT加载器将无法找到并加载新内核。

查看练习 8.4 以检查你现在是否理解如何配置一个同时启动 Linux 和 Windows NT 的引导系统。

## 练习 8.4

配置系统以启动 Linux 和 Windows NT

使用 Windows NT 和 Linux 配置多引导运行的系统。

## 其他操作系统

你可以配置 Linux 启动或由其他操作系统（包括 OS/2, FreeBSD 和 NetBSD）启动。配置方法通常类似于 Windows NT 或 Windows 9x 的配置，取决于你喜欢将 LILO 作为主引导还是还是次引导引导。咨询操作系统文档以确定如何进行。你可能会发现 USENET 新组有助于解决你的问题。

## 特殊安装

本节介绍了如何执行几种特殊类型的安装：

**PCMCIA 安装**：必须访问 PCMCIA
**网络安装**：访问发行版文件
**Kickstart 安装**：更自动地

### 执行 PCMCIA 安装

如果你在安装期间需要访问 PCMCIA，请使用启动盘。通过 PCMCIA 安装 Red Hat Linux 请参考第 6 章“安装”中的描述。

> 安装之前的版本的 Red Hat 请使用启动盘。某些 Red Hat 文档已经更新。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_0.png)

> 某些 Red Hat CD-ROM 包含镜像。在使用 PCMCIA 时遇到安装问题，请检查 Red Hat 服务器是否有更新的镜像。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_0.1.png)

现在尝试练习 8.5 执行 PCMCIA。

| 练习 8.5 |
| 执行 PCMCIA 安装 |
| 如果你有 PCMCIA CD-ROM，请使用它安装 Linux。 |

## 执行网络安装

安装 Red Hat Linux 的常用方法是通过发行版 CD-ROM。然而，你可以从位于 FTP、HTTP (Web) 或 NFS 服务器上的发行媒体安装 Red Hat Linux。这被称为网络安装。

曾经，Red Hat Linux 支持通过 Samba (SMB) 网络安装。现在不再支持。

在 Red Hat Linux 6.2 之前，解析包含服务器域名的 DNS 服务器必须能够为服务器提供反向查找。服务器必须将其 IP 地址映射到服务器的主机。在 Red Hat Linux 6.2 下，这不再需要了。

如果服务器通过多种服务访问发行媒体，那么只存储介质是有用的。以下命令序列创建了可以通过 FTP 和 HTTP 访问的发行媒体副本：

```
cp -a /mnt/cdrom/RedHat /home/ftp/pub
ln -s /home/ftp/pub/RedHat /home/httpd/html/RedHat
```

要通过 NFS 提供媒体访问，通过在 `/etc/exports` 文件中包含以下行来导出 `/home/ftp/pub/RedHat` 目录：

```
/home/ftp/pub/RedHat (ro)
```

有关设置 FTP、HTTP 和 NFS 服务的更多信息，请参见第 21 章“安装和配置主网络服务”。

你可以通过 NFS 执行图形安装，但不能通过 FTP 或 HTTP 执行。要要通过网络服务器安装 Red Hat Linux，从发行版 CD-ROM 中 images 目录下的镜像文件 `bootnet.img` 创建启动盘。然后通过启动此磁盘开始安装程序。注意，网络安装使用文本模式而不是图形模式，因此安装菜单不会提供执行图形安装的选项。在选择语言和键盘后，将显示如图 8.1 所示的安装方法屏幕。选择提供安装媒体的服务并点击确定。

