
你可以在主页面以及 Efax 主页 `http://www.ce.com/efax/documentation` 找到更多关于传真和 Efax 工作原理的信息。

Efax 真正的设计是用于……（注：原文此处似乎不完整或存在重复，根据语境翻译如下）[此处由于原文存在重复导致逻辑混乱]（注：由于用户提供的原文在后半部分出现了大量重复内容，翻译时已根据指令“不要重复输出原文”的原则进行了去重处理，仅保留核心逻辑部分。）

# 第 25 章 效率应用

此外，还有其他使用微软效率应用的解决方案，主要是 Codweaver 的 Crossover 和 Transgaming 对 Wine 的实现。这些将在第 27 章中结合 Wine 进行详细讨论。

## 相关的 FEDORA CORE LINUX 命令

以下命令允许你访问 Fedora Core Linux 中的效率应用、工具和进程：

```
fax—一个作为 Efax 应用程序前端端的脚本
gimp—一个用于 X 的图形图像编辑器
koshell—KDE 的 KOffice 办公套件
kpread—KDE 的 KSpread 电子表格程序
owriter—OpenOffice.org 中的文字处理器
numeric—一个用于 GNOME 的电子表格编辑器
mproject—一个用于 GNOME 的项目客户端
abioward—一个用于 GNOME 的图形文字处理器
pilot-xfer—一个用于 Palmos PDA 用户的全面命令行工具
```

## 参考资料

`http://www.openoffice.org`—OpenOffice.org 套件的主页。

`http://www.pclinuxonline.com/modules.phpname=News&file=article&sid=3199`—一组指向 OpenOffice 技巧和增强的链接。网站上的一个链接是 PDF 文件，解释了如何将 OpenOffice 作为 MySQL 的数据库前端。

`http://www.gnome.org/gnome-office/`—GNOME Office 网站。

`http://www.koffice.org`—KOffice 套件的主页。

`http://en.hancom.com/`—Hancom Office 套件的主页。

`http://www.sun.com/software/staroffice/6.0/`—StarOffice 6.0 网站。

`ftp://corp.devel/pub/linux/OpenOffice2000/updates/installscript`—一个改进的安装脚本下载，它能够在 Red Hat Core Linux 和其他发行版上对 Core WordPerfect Office 2000 进行更不易出错的安装。

`http://bulldog.torg/webcal/webcal.html`—优秀的 WebCal 基于 Web 的日历和调度程序的主页。

`http://www.quanta.sourceforge.org`—用于 KDE 的 Quanta Plus 开发工具。

`http://www.kronos.com/products/TKC.html`—一种基于 Linux 的计时系统，支持开放标准且比竞争产品更具价格。

`http://www.hriggs.com/palm.html`—关于在 Linux 上获取 Palm Pilot 设备及其若干实用应用程序的教程和说明。

## 多媒体应用

电影、音乐、动画、实时视频会议和其他媒体功能已成为许多家庭和商业计算环境的基本能力。毫无疑问，多媒体对互联网增长和计算机硬件进步的推动作用，与邮件、新闻等其他相关服务的传统服务不上下。

Fedora Core Linux 包含了几个不同的程序，你可以使用它们来执行“魔术”，包括在其他功能较弱的操作系统上使用的图形、视频和音频格式。

本章概述了 Fedora Core Linux 包含的基本多媒体工具。你将看到如何创建自己的 CD、看电视、将音频 CD 刻录为开源 OGG 音频格式进行播放、扫描并处理图形图像，以及执行其他高效且令人快乐的任务。

- 在 Fedora Core Linux 中刻录 CD 和 DVD
- 声音与音乐
- 查看电视和视频
- 在 Fedora Core Linux 中使用照相机
- 在 Fedora Core Linux 中使用扫描仪
- 图形处理
- Linux 游戏
- 参考资料

> 从 Red Hat 9 发布开始，Fedora 维持了一种引起许多长期用户争议的哲学。由于对美国版权和专利问题可能引发潜在责任的担忧，Red Hat 和 Fedora 自愿移除了任何可能侵犯他人知识产权或导致 Red Hat 遭受任何惩罚的功能。这并不意味着个人用户会侵犯同样的权利，因此我们为读者提供了资源，说明如何恢复这些功能；选择权交由你。

通过按照第 8 章“管理软件和系统资源”中描述安装并使用 APT 或 YUM，你可以轻松地恢复 Fedora 的完整多媒体功能。

# 第 26 章 多媒体应用

由于 Fedora Core 使用 UTF-8 语言编码，如果非 Fedora 应用不符合 UTF-8 标准，将出现显示问题。你可以通过在 `/etc/bashrc` 中放置以下行来修复此：

```
export LANG=en_US SUPPORTED="en_US"
LC_MESSAGES=C LC_ALL=C
```

## 在 Fedora Core Linux 中刻录 CD 和 DVD

刻录（或创建）自己的 CD 是 Linux 多媒体爱好者的基本技能。由于典型媒体文件变得越来越大，单曲（即使在压缩音频格式下）通常需要几兆字节的存储空间，CD 和 DVD（数字视频磁盘）已成为多媒体内容的标准媒介。你可以使用 CD 来：

- 在 CD 上记录和存储多媒体数据，如备份文件、图形图像和音乐。
- 从音乐 CD 刻录音频轨道（刻录是指从音乐 CD 中提取音乐轨道）并为你的个人使用汇成你自己的 CD。

Linux 音频客户端支持创建和使用许多不同类型的音频格式。本章的后续部分将讨论声音格式、声卡、音乐播放器等内容。因为 CD 刻录在 Fedora Core Linux 中有许多其他用途，你必须在本章中首先涵盖该过程的要点。若要在 CD 上记录多媒体数据，你必须在系统中安装了具有 CD 刻录能力的驱动器。第 4 章“安装后配置”解释了配置并让 CD 驱动程序正常运行的基础知识。硬件应该已经设置好了。

### 设备识别

在这里，我们看到 CD 刻录机（在本例中为 DVD 阅读器）存在，并被系统识别为 `scd0`。这些数字代表设备的 scs/目标/lun（逻辑单元号）。在刻录 CD 时你需要这个设备编号。

> 用于制作 CD 和 DVD 的 IDE 驱动器需要模拟为 SCSI 驱动器。Fedora 在安装时会自动执行此操作，但如果需要手动操作，你需要：
>
> - 在 `/etc/modules.conf` 中添加以下行：`probe ide2`
> - 编辑 `/boot/grub/menu.lst` 文件，在内核命令中添加：`ide2`
> - 重启计算机。
>
> 这些项目将加载相应的模块并提供 SCSI 模拟。你不再将 CD 驱动器称为 `/dev/hdd`，而是 `/dev/scd0`。检查符号 `/dev/cdrom` 以确保它指向 `/dev/scd0`。使用 2.6 内核时不需要 SCSI 模拟。

## 从命令行创建 CD

在 Linux 中，创建 CD 是分步骤的。你首先创建一个 `iso9660` 格式的镜像，然后将镜像写入 CD。正如你在第 10 章中学的，`iso9660` 是 CD-ROM 的默认文件系统。

使用 `mkisofs` 命令创建 ISO 镜像。`mkisofs` 命令有很多选项（参见完整列表），但你可以配合以下刻录使用：

```
$ mkisofs -r -v -J -l -o /tmp/your_special_cd.iso /source_directory
```

示例中使用的选项如下：

- `-r`—将文件权限设置为更有用的值。UID 和 GID（个人和组用户要求）设置为零，所有文件全局可读可搜索，且所有文件均设置为可执行（针对 Windows 系统）。
- `-v`—显示详细信息（而非简练信息），以便你可以看到过程中的状况；如果发生问题，这些信息有助于解决问题。
- `-J`—在 ISO9660 使用 Joliet 扩展，以便 Windows 伙伴更轻松地读取 CD。
- `-1`—允许 31 个字符的文件名；DOS 不喜欢，但大家都喜欢。
- `-o`—定义写入镜像的目录（即输出目录）及其名称。`/tmp` 目录为此目的非常方便，但镜像也可以放在你具有写入权限的任何地方。
- `/source_directory`—源目录的路径；即包含我们想要包含的文件的目录。指定路径下的（以及文件）文件——如果你需要了解其复杂性，主页中会有详细说明。我们简单的解决方案是构建新目录并向其中填充我们想要复制的文件，然后使用该目录作为源创建镜像。

还有许多可用选项，包括使 CD 变为可引导的选项。

在创建 ISO 镜像后，你可以使用 `cdrecord` 命令将其写入 CD：
