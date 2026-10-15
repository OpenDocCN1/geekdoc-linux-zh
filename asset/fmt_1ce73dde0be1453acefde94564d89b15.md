
$ kword &

```
KWord 随后要求你为会话选择一个文档。如图 9.17 所示，KWord 客户端提供了复杂的编辑能力，包括桌面出版。

![](img/d4ad9a7c85702c925b4288f587284a4f_293_0.png)

图 9.17 KOffice 文字处理组件是一个复杂的基于框架 WYSIWYG 编辑器，适用于轻级桌面出版，支持包括 WordPerfect 在内的多种格式。

KSpread 客户端是一个功能强大的电子表格程序，提供了图表功能。与 KWord 一样，KSpread 也可以从命令行启动。在使用这样的命令后，系统会要求你选择文档类型（新文档或之前的文档）：

```bash
$ kspread &
```

KDE 在其 KOffice 及相关应用集合中包含了其他生产力客户端。这些客户端包括地址录、文件跟踪器、计算器、记事本和调度器。一个流行的客户端是 KOrganizer，它为任务、待办事项列表和计划预约提供每日、每周、工作和每月视图，并带有后台闹钟。

它内部还支持日志功能，你可以与你的 Palm Pilot 同步信息。你可以从 KDE 桌面面板的菜单或从命令行启动此客户端，如下所示：

```bash
$ korganizer &
```

图 9.18 显示了一个典型的 KOrganizer 窗口。

![](img/d4ad9a7c85702c925b4288f58728a4f_294_0.png)

图 9.18 KDE 的 KOrganizer 客户端支持编辑任务和计划，你可以与你的 PDA 同步。这里被添加到地址录中。

## Linux 商业套件

除了已经提到的 StarOffice 之外，Fedora 还有几种商业套件可用。这些商业套件中没有随 Fedora 提供的。Hancom Office 使用与 KDE 桌面相同的 QT 小组件，Hancom 在微软文件格式兼容性方面得分良好。该套件包含一个文字处理器和一个电子表格。

## 为 Linux 编写的生产力应用

除了已经提到的 StarOffice 之外，Fedora 还有几种商业套件可用。这些商业套件中没有随 Fedora 提供的。Hancom Office 使用与 KDE 桌面相同的 QT 小组件，Hancom 在微软文件格式兼容性方面得分良好。该套件包含一个文字处理器和一个电子表格。

## 相关命令

# 参考

- http://www.openoffice.org—OpenOffice.org 套件的主页。
- http://www.pclinonline.com/modules.php?name=News&file=article&sid=3199—OpenOffice.org 技巧、技巧和增强功能的链接集。该网站上的一个链接指向 PDF 文件，解释了如何将 OpenOffice.org 作为 MySQL 的数据库前端。
- http://www.gnome.org/projects/ooo/—GNOME Office 网站。
- http://www.koffice.org—KOffice 套件的主页。
- http://en.hancom.com/—Hancom Office 套件的主页。
- http://bulldog.tzo.org/webcal/webcal.html—优秀的基于 WebCal 的日历和调度程序的主页。
- http://www.codewavers.com—来自 CodeWeavers 的广受欢迎的 CrossOver Office 网站，允许你在 Linux 下运行 Windows 程序。

## 相关命令

以下命令允许你访问 Fedora 中的生产力应用、工具和进程：

- `oowriter`—OpenOffice.org 的 Writer
- `oocalc`—OpenOffice.org 的 Calc
- `oimpress`—OpenOffice.org 的 Impress
- `kshell`—KDE 的 Office 套件
- `kspread`—KDE 的 K 电子表格
- `gimp`—GIMP (GNU 图像处理包)
- `numeric`—GNOME 的电子表格编辑器
- `planner`—GNOME 的项目管理客户端
- `abiword`—GNOME 的图形文字处理器

# 第 10 章

## 多媒体应用

## 本章内容

- 在 Fedora 中刻录 CD 和 DVD
- 声音与音乐
- 观看电视和视频
- 参考

21 世纪已成为数字化生活的世纪，全球数百万计算机用户正在拥抱数码相机、MP3 播放器和其他各种多媒体设备等新技术。10 年前，你的 Windows 安装目录中可能堆积了一些 WAV 文件，而现在，你很可能在不同的计算机上散布着成百甚至上千个 MP3 文件。除了视频剪辑、动画和其他图形，对组织和维护这些庞大库的需求正驱动着应用程序的发展。热门的专有应用程序（如 iTunes 和 Google 的 Picas）深受 Linux 用户青寐以求，但开源应用也开始出现并提供了真正的替代方案，而且对于某些人来说，这些应用是他们决定全面转向 Linux 的终极原因。

本章概述了 Fedora 自带的一些基础多媒体工具。你将看到如何创建自己的 CD、如何看电视、如何将音频 CD 刻取为开源 OGG 音频格式进行播放，以及如何管理你的媒体库。

> 注意
> Fedora 项目延续了从 Red Hat 9 发布开始的趋势，并保持着一种让许多长期用户产生争议的哲学。由于对美国可能因版权和专利问题产生潜在法律责任的担忧，Red Hat 和 Fedora 项目自愿移除了任何违反他人知识产权或导致 Red Hat 遭受惩罚的功能。这并不意味着个人用户会违反这些权利，因此我们为读者提供了相关资源，说明如何恢复部分此类功能；选择权交在你手中。

# 第 10 章 多媒体应用

通过第 7 章“管理软件”介绍的方法安装并使用 `yum`，你可以轻松为 Fedora 恢复完整的多媒体功能。

```bash
# /etc/bashrc
```

由于 Fedora 使用 UTF-8 语言编码，如果某些非 Fedora 应用不符合 UTF-8 标准，将会出现显示问题。你可以通过在 `/etc/bashrc` 中放置以下行来修复此问题

```bash
export LANG=en_US SUPPORTED="en_US"
LC_MESSAGES=LC_ALL=C
```

# 在 Fedora 中刻录 CD 和 DVD

Linux 通过 ISO 镜像分发到网上，这些镜像等待被写入 CD 或 DVD。因此，如果你必须下载并安装 Linux 发行版，学习如何刻录光片至关重要。不仅如此，你可能还会使用 CD 以及更常见的 DVD 来备份你的音乐、家庭照片或其他重要文件。由于 DVD 刻录机价格低廉，这种格式已非常兴盛，仅仅因为可用容量更大，更多的人使用 DVD 进行存档。

今天的高分辨率数码相机每张照片可能占用超过 3MB，而音乐文件从 1MB 到 10MB+ 不等。这些大文件使得 DVD 成为明显的选择，但在某些情况下你仍需要写入 CD。你可以使用 CD 和 DVD：

- 在 CD 或 DVD 上记录和存储多媒体数据，如备份文件、图形图像和音乐。
- 从音乐 CD 中刻取音频轨道（“刻取”是指从音乐 CD 中提取音乐轨道）并为个人使用编译你自己的音乐 CD。

Linux 音频客户端和程序支持创建和使用许多不同类型的音频格式。本章的后续章节将讨论声音格式、声卡、音乐播放器等内容。由于 Fedora 中的许多其他用途都需要刻录功能，因此我们首先涵盖该过程的要点。你必须在系统中安装了具有 CD 刻录能力的驱动器。第 4 章“安装后配置”解释了配置 CD 刻录机并使其正常运行的基础知识。硬件应该在初始安装 Fedora 期间已设置好，或者在被 Kudzu 检测到时已正确配置。请确保你的 CD 刻录工作正常，使用 `cdrecord -status` 获取通过 SCSI（小型计算机系统接口）仿真下的 CD 驱动器的信息：

```bash
# cdrecord -status
Cdrecord-Clone 2.01a32-dvd (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.5.27
Using libscg 'shily-0.8'
scsibus0:
```
