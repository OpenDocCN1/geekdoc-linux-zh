
- `kamera`—KDE 数字相机工具

- `dvgrab`—使用 FireWire（火线）连接的视频摄像头捕捉工具

### 扫描仪

- `kooka`—KDE 扫描仪应用程序

- `xsane`—扫描仪应用程序

### 图形

- `eog`—Eye of GNOME 图像查看器

- `ImageMagick`—图像处理应用程序

- `gimp`—GNU 图像处理程序

- `qview`—GNOME 图像查看器

- `koloredit`—KDE 调色板编辑器

- `kiconedit`—KDE 图标编辑器

- `kpaint`—一个图形应用程序

- `kuickshow`—KDE 图像查看应用程序

- `view`—KDE 嵌入式图像查看器

- `tpbm-progs`—处理 netpbm 格式图形的工具

- `xfig`—一个矢量图形应用程序

## 参考

- `http://www.gimp.org`—The GIMP (GNU 图像处理程序) 主页。

- `http://www.gnome.org/projects/f-spot/`—F-Spot 项目主页。

- `http://www.linuxformat.co.uk`—Linux Format 网站，Michael J. Hammel 编写的长期 GIMP 教程的发布地。

- `http://www.exif.org`—关于 EXIF 及其在数字相机中使用的更多信息。

- `http://www.sane-project.org`—SANE (Scanner Access Now Easy) 项目主页。

- `http://www.imagemagick.org`—ImageMagick 主页。

- `http://www.codeweavers.com`—流行的 crossover 办公；如果你想尝试在 Linux 下运行 Photoshop，则需要。

- `http://gimp.net/tutorials/`—The GIMP 官方教程。

# 第 12 章 使用 Fedora 打印

## 本章内容

## 使用 Fedora 打印

- Fedora 打印概述

- 配置和管理打印服务

- 创建和配置本地打印机

- 参考

从一开始，Fedora 就支持来自许多不同制造商的大量打印机。在本章中，我们将查看如何让打印机连接并与 Fedora 通信，以及 Fedora 用于管理打印机和打印作业的软件。

与大多数其他 Linux 发行版一样，Fedora 使用 CUPS（通用 UNIX 打印系统）来处理。也支持其他系统，如 LPRng，但你无法使用 Fedora 内部的一些图形管理工具。

## 互联网打印协议

CUPS 支持被称为 IPP 的互联网打印协议，提供了许多独特功能，例如网络打印机目录（打印机浏览）服务、对加密的支持以及对 PostScript 打印机描述 `.ppd` 文件的支持。

根据互联网工程任务组 (IETF) 的规定，IPP 源于 Novell 在 1996 年提出的提案，旨在创建一个用于互联网的打印协议。

## Fedora 打印概述

Fedora 打印系统可以打印到本地（连接）或远程（网络）打印机。如果你使用本地打印机，它由 `/dev/lp0` 表示（如果你有 USB 打印机）。本地和远程打印机使用系统数据库 `/etc/printcap` 中定义的打印队列。正在打印的文档被称为打印作业，你可以在池目录 `/var/local/cups/` 中查看打印作业列表（队列）。注意，你只能控制自己的打印作业。

要向系统添加打印机，你使用 `system-config-printer` 客户端创建、配置并保存打印机定义。该客户端将定义保存为系统数据库 `/etc/printcap` 中的条目。每个定义包含包含打印机名称、主机和队列的文本字段。打印文档将池化到 `/var/local/cups/`。

CUPS 在 `/etc/cups` 目录下通过名为 `printers.conf` 的文件维护自己的打印机数据库。例如，之前在 `/etc/printcap` 中定义的关联打印机在 `/etc/cups/printers.conf` 中可能有以下条目：

```
# 此文件由 cupsd(8) 从
# /etc/cups/printers.conf 文件自动生成。对此文件的更改将丢失。
lp1|lp:rm=stinky;rp=lp:-
```

<DefaultPrinter lp1>

Info Created by redhat-config-printer 0.6.x

DeviceURI parallel:/dev/lp0

Location HP 648 local printer

State Idle

Accepting Yes

JobSheets none none

QuotaPeriod 0

PageLimit 0

KLimit 0

</Printer>

CUPS 使用一个名为 `cups` 的打印服务器（守护进程），在 CUPS 文档中也称为调度器。该服务器像其他 Fedora 服务一样通过 `service` 命令或 `system-config-services` 客户端进行控制。服务器在系统上的运行方式由 `/etc/cups` 目录下的配置文件 `cupsd.conf` 设置决定。CUPS 可执行文件位于 `/usr/lib/cups` 目录。

## 配置与管理打印服务

`cupsd.conf` 手页记录了服务器的 80 种不同设置，你可以根据你的系统、网络或打印环境对其进行配置。默认的 CUPS 相关文件和目录存储在 `/usr/share/cups` 目录下。日志可以设置为七种不同的级别，有关访问和错误的信息存储在 `/var/log/cups` 目录下的日志文件中。

可以通过其他设置来定制资源需求，例如 `MaxCopies` 用于设置用户打印任务的最大复印份数，`MaxJobs` 用于设置每个用户活动打印任务的数量限制。`RIPCache` 设置（默认为 8MB）控制打印期间用于图形缓存的内存量。

例如，如果你想限制每次打印的文档或页数为 20 份，且每个用户同时仅允许 10 个并发打印任务，可以使用以下设置：

- MaxCopies 20

- MaxJobsUser 10

> 提示：在修改配置文件后，不要忘记重启 CUPS 服务。更改只有在服务重启时（当守护进程重新加载配置文件时）才会生效。请参阅本章节后部分的“基于 GUI 的打印机配置快速上手”。

由于 CUPS 不使用传统的 Berkeley 风格后台打印系统 `lpd`，你可以更改默认的 `/etc/printcap` 打印机能力数据库的名称。打印可以使用加密，安全访问行为由 `/etc/cups/client.conf` 中的设置决定。网络访问设置包括端口、连接、IP 地址、域名以及对客户端请求数量和大小的限制。

## 配置与管理打印服务

作为系统管理员（或你工作站的 root 操作员），你的任务是正确定义本地或远程打印机，并确保打印服务已启用且正常运行。幸运的是，Fedora 包含了 Red Hat 的图形打印配置工具，这使得这项工作变得简单。在你学习本章相应节时，应该使用这些工具来配置打印。但首先，请花一点时间阅读配置过程的快速概述。

> 注意：不要手动编辑你的 `/etc/printcap`。当打印服务重启或系统重启时，任何更改都会丢失。如果你需要创建自定义打印机条目，请将条目保存在 `/etc/printcap.local` 并重启打印服务。

你可以使用命令行系统 `system-config-printer-tui` 程序或图形界面 `system-config-printer-gui` 来配置打印服务。本章中的大部分详细信息在使用 GUI 的使用。然而，接下来的概述部分将为你两种配置方法提供坚实的基础。你将在章节的后续部分学习这些过程的细节。

# 第 12 章 使用 Fedora 打印

### 基于 GUI 的打印机配置快速上手

为 Fedora 配置打印机非常简单，但必须使用 root 权限进行。请确保 `cups` 守护进程已安装并运行。如果你在安装 Fedora 时选择了使用打印支持，则会安装该守护进程及软件。如果你不确定 cups 是否正在运行，可以使用带有服务名称和状态关键字的 `service` 命令，如下：

```
# service cups status
```

你将看到：

cupsd is stopped

或者，如果 cupsd 正在运行，会显示确认信息及其进程 ID，例如 `cupsd (pid 2378) is running...`

如果 cupsd 已安装但未运行，请如下所示启动守护进程：

```
# /etc/rc.d/init.d/cups start
```

你也可以如下使用 `service` 命令启动守护进程：

```
# service cups start
```

如果你正在使用桌面，请选择系统、管理、打印。系统会要求你输入 root 密码。如果不是，说明你是以 root 身份运行 X，这是一个坏主意。请注销并以普通用户身份重新登录！输入 root 密码后，会弹出打印机配置对话框。
