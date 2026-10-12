

# 参考资源

- [http://www.openoffice.org](http://www.openoffice.org) —— OpenOffice.org 办公套件的首页。
- [http://www.pclinuxonline.com/modules.php?name=News&file=article&sid=3199](http://www.pclinuxonline.com/modules.php?name=News&file=article&sid=3199) —— 一组关于 OpenOffice.org 的技巧、窍门和增强功能的链接。网站上的一个链接指向一个 PDF 文件，解释了如何将 OpenOffice.org 用作 MySQL 的数据库前端。
- [http://www.gnome.org/projects/ooo/](http://www.gnome.org/projects/ooo/) —— GNOME 办公套件网站。
- [http://www.koffice.org](http://www.koffice.org) —— KOffice 套件的首页。
- [http://eri.hancom.com/](http://eri.hancom.com/) —— Hancom Office 套件的首页。
- [http://bulldog.izo.org/webcal/webcal.html](http://bulldog.izo.org/webcal/webcal.html) —— 优秀的基于 Web 的日历和日程安排程序 WebCal 的首页。
- [http://www.codeweavers.com](http://www.codeweavers.com) —— 极度流行的 CodeWeavers CrossOver Office 的网站，它允许你在 Linux 下运行 Windows 程序。

# 第 10 章

## 多媒体应用

### 本章内容

- 在 Fedora Core Linux 中刻录 CD 和 DVD
- 声音和音乐
- 观看电视和视频
- 参考资源

21 世纪已成为数字生活方式的世纪，全球数以百万计的计算机用户正在采用新技术，如数码相机、MP3 播放器以及其他各种多媒体设备。

十年前，你的 Windows 安装中可能散落着一堆 WAV 文件，但如今，你更可能在计算机中拥有数百甚至数千个 MP3 文件，它们分散在各个位置。随着视频片段、动画和其他图形的增加，整理和维护这些庞大库的需求正在推动应用程序的开发。像 iTunes 和 Google 的 Picasa 这样的流行专有应用程序是 Linux 用户梦寐以求的，但开源应用程序开始出现，提供了真正的替代方案，对于某些人来说，这也是他们全天候转向 Linux 的最终理由。

本章概述了随 Fedora 附带的一些基本多媒体工具。你将学习如何制作自己的 CD，观看电视，将音频 CD 刻录（rip）为开源 OGG 音频格式以供播放，以及管理你的媒体库。

> **注意**
>
> 延续始于 Red Hat 9 发布的举措，Fedora 项目维护一种对许多长期用户而言颇具争议的理念。由于对美国版权和专利问题中潜在法律责任的担忧，Red Hat 和 Fedora 项目自愿移除了任何可能侵犯他人知识产权或使 Red Hat 遭受任何处罚的功能。这并不意味着单个用户会违反相同的权利，因此我们为读者提供了资源，说明如何恢复其中一些功能；选择权在于你。

通过安装和使用第 7 章“软件管理”中描述的 xine，你可以轻松地将 Fedora 恢复为完整的多媒体功能。

由于 Fedora 使用 UTF-8 语言编码，某些非 Fedora 应用程序如果不符合 UTF-8 标准，将会出现显示问题。你可以通过在 /etc/bashrc 中放置以下行来修复此问题：

```
export LANG=en_US_SUPPORTED=en_US
LC_MESSAGES=C LC_ALL=C
```

### 在 Fedora Core Linux 中刻录 CD 和 DVD

Linux 通过等待被写入 CD 或 DVD 的 ISO 镜像在互联网上分发。因此，如果你需要下载和安装 Linux 发行版，学习如何刻录光盘是至关重要的。不仅如此，你很可能会使用 CD 以及更常见的 DVD 来备份你的音乐、家庭照片或其他重要文件。由于 DVD 刻录机非常便宜，这种格式真的爆发式增长，越来越多的人使用廉价的 DVD 作为归档方式，仅仅因为可用的存储容量更大。当今的高分辨率数码相机每张照片可能占用 3MB 或更多，而音乐文件大小可以从 1MB 到 10MB+ 不等。这些文件大小使 DVD 成为显而易见的选择，但仍有一些场合你需要写入 CD。你可以使用 CD 和 DVD 来

- 在 CD 或 DVD 上记录和存储多媒体数据，如备份文件、图形图像和音乐。
- 从音乐 CD 中提取音轨（*提取*指的是从音乐 CD 中提取音乐音轨），并为你个人使用编译你自己的音乐 CD。

Linux 音频客户端和程序支持创建和使用许多不同类型的音频格式。本章后面的部分讨论声音格式、声卡、音乐播放器以及更多内容。由于 CD 刻录在 Fedora 中用于许多其他用途，我们首先在本章中介绍该过程的基础知识。要在 CD 上记录多媒体数据，你的系统必须安装了具有 CD 写入能力的光驱。第 4 章“安装后配置”解释了配置并使 CD 刻录机正常工作 rudiments。硬件应该在初始 Fedora 安装期间正确设置，或者在 Kudzu 检测到时正确配置。为了确保你的 CD 刻录机正常工作，使用 `cdrecord -scansbus` 获取在 SCSI（小型计算机系统接口）模拟下使用 CD 驱动器的信息：

```
# cdrecord -scansbus
Cdrecord-Clone 2.01a32-dvd (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling

Linux sg driver version: 3.5.27
Using libsgv version 'schily-0.8'
scsibus0:
0,0,0  0)  'HL-DT-ST'  'RW/DVD GCC-4120B'  '2.01'  Removable CD-ROM
0,1,0  1)  *
0,2,0  2)  *
0,3,0  3)  *
0,4,0  4)  *
0,5,0  5)  *
0,6,0  6)  *
0,7,0  7)  *
```

在这里，我们看到 CD 刻录机（在此示例中，是 CD 刻录机/DVD 读取器）存在，并且被系统识别为设备 0, 0, 0。这些数字代表设备的 scsi/bus/target/lun（逻辑单元号）。在你刻录 CD 时需要知道这个设备号，所以请把它写下来或记住它。

> **提示**
>
> 用于创建 CD 和 DVD 的 IDE 驱动器需要被模拟为 SCSI 驱动器。Fedora 在你首次安装时会自动执行此操作，但如果你需要手动执行，以下是需要配置的几项（假设 CD 驱动器位于 /dev/hdd）：
> - 在 /etc/modules.conf 文件中添加以下行：
>   `probeall ide-scsi`
> - 编辑 /boot/grub/menu.lst 文件，在 kernel 命令中添加以下内容：
>   `hd=ide-scsi`
> - 重新启动你的计算机。
>
> 这些项目加载适当的模块并提供 SCSI 模拟。你不再将 CD 驱动器称为 /dev/hdd，而是称为 /dev/scd0。检查 /dev/cdrom 的符号链接，确保它指向 /dev/scd0。
>
> 然而，由于 Fedora 现在使用 2.6 内核，SCSI 模拟不再是必需的，尽管如果某些功能工作不正确，它是有用的信息。

#### 从命令行创建 CD

在 Linux 中，创建 CD 是一个两步过程。你首先创建 iso9660 格式化的镜像，然后你将镜像刻录或写入 CD。正如你将在第 38 章“文件系统管理”中了解到的，iso9660 是 CD-ROM 的默认文件系统。

使用 `mkisofs` 命令创建 ISO 镜像。`mkisofs` 命令有许多选项（查看 man 页了解完整列表），但对于快速刻录，请使用以下内容：

```
$ mkisofs -r -v -J -l -o /tmp/our_special_1cd.iso /source_directory
```

此示例中使用的选项如下：

- **-r** —— 将文件权限设置为更有用的值。UID 和 GID（个别用户和组用户 ID 要求）设置为零，所有文件全局可读和可搜索，所有文件设置为可执行（针对 Windows 系统）。
- **-v** —— 显示 *详细* 消息（而不是简略消息），以便你可以看到过程中发生的事情；如果发生问题，这些消息可以帮助你解决问题。
- **-J** —— 使用 *joliet* 扩展对 *iso*，以便使用 Windows 的朋友更轻松地读取 CD。*joliet*（用于 Windows）、Rock Ridge（用于 UNIX）和 HFS（用于 Mac）对 *iso9660* 标准的扩展用于适应长文件名，而不是 *iso9660* 标准支持的八字符 DOS 文件名。
- **-l** —— 允许 31 个字符的文件名；DOS 不喜欢，但其他人喜欢。
- **-o** —— 定义镜像写入的目录（即 *输出*）及其名称。*输出* 目录对于此目的很 *方便*，但镜像可以放在你拥有写入权限的任何位置。
- **源目录** —— 指示源目录的路径；即包含你想要包含的文件的目录。有方法添加额外路径并排除指定路径下的目录（和文件）——所有这些在 man 页中都有解释。如果你需要这种复杂程度，我们的简单解决方案是构建一个新的目录树，用我们要复制的文件填充它，然后使用该目录作为源制作镜像。

还有更多可用的选项，包括使 CD 可启动的选项。

创建 ISO 镜像后，你可以使用 `cdrecord` 命令将其写入 CD：

```
$ cdrecord -eject -v speed=12 dev=0,0,0 /tmp/our_special_cd.iso
```

此示例中使用的选项如下：

- ***eject* —— 当写入操作完成时弹出 CD。**
- ***v* —— 显示详细消息。**
- ***speed* —— 设置速度；速率取决于单个驱动器的能力。如果驱动器或可记录介质较差，你可以使用较低的速度来获得良好的刻录效果。**
- ***dev* —— 指定 CD 刻录机的设备号（我稍后让你写下来的那个数字）。**

> **注意**
>
> 你还可以在 `cdrecord` 命令中使用 `blank=` 选项来擦除 CD-RW 磁盘。`cdrecord` 命令比 `mkisofs` 选项少，但它提供了 `-multi` 选项，允许你制作多会话 CD。多会话 CD 允许你写入数据轨道，退出，然后稍后向 CD 添加更多数据。单会话 CD 只能写入一次；任何剩余的 CD 容量都会被浪费。阅读 `cdrecord` man 页了解其他选项。当前 CD 介质的容量为 700MB 数据或 80 分钟音乐。（有 800MB/90 分钟的 CD，但它们很罕见。）一些 CD 可以过烧（overburn）；即记录超过标准的容量。如果 CD-RW 驱动器支持，`cdrecord` 命令能够过烧。你可以在 http://www.cdmediaworld.com/hardware/cdrom/cd_oversize.shtml/ 了解更多关于 CD 过烧的信息。

