
更强大的选项是 XML Editor。它是为编辑包括 XML、DocBook、DITA 在内的大多数标记语言设计的。它还具有架构验证、语法高亮、标签补全和拼写检查功能。对于专业文档专家来说，这是最实用的选项。你可以从 Ubuntu 仓库安装 XML Editor，他们的网站在 http://xml-copy-editor.sourceforge.net 提供版本及更多信息。

## 使用 LaTeX

LaTeX 是为学术界创建并广泛使用的。它是一种为 TeX 排版系统创建的GIWYW（所得即所得）文档标记语言。有多个编辑器可供 LaTeX 使用，并且可以在几乎每个操作系统上找到它们。

> 注意
>
> WYSIWYG 是“所见即所得”的缩写，用于描述使用图形界面的文字处理器和文档创建系统。遗憾的是，任何用这些程序（包括本章早些提到的 LibreOffice 等）创建文档的人都知道，你在屏幕上看到的并不总是出现在纸质打印版本中。在使用 LaTeX 编辑器编写你的 Tex 文档时，无法保证屏幕上的内容将或将如何显示，但该格式保证了最终输出将完全按照你要求的。

本节讨论了从 Ubuntu 软件中心提供的几个流行的 LaTeX 编辑器。你还可以创建和编辑可以使用任何文本编辑器，包括 Gedit。

Texmaker 不仅在 Ubuntu 软件中心提供了一个版本，还通过 www.xmlmath.net/texmaker/ 提供了 Windows 和 Mac OS X 版本。它免费、易用且成熟。该程序已经运行了很一段时间，非常稳定，具有许多实用功能，在 TeX 世界中相当流行。

LyX 在 Ubuntu 软件中心提供了两个版本，还通过其网站 www.lyx.org 提供了 Windows 和 Mac OS X 版本。LyX 的主要吸引力在于它的图形化界面，这使其成为从 WYSIWYG（所见即所得）到 LaTeX 的一个有趣桥梁。它还拥有许多可用插件来扩展功能。

Kile 是为 KDE 编写并设计的。因此，它与 Kubuntu 融合良好，但可以在标准的 Ubuntu 安装上运行。它还提供了 Windows 版本；详情请参见 http://kile.sourceforge.net。

## 为 Microsoft Windows 编写的生产力应用

Microsoft Windows 与 Linux 有本质上的不同，但你可以使用名为 Wine 的应用程序在 Linux 中安装和运行某些 Microsoft Windows 应用程序。Wine 允许你在基于 UNIX 的系统上使用 Windows 和 DOS 程序。Wine 包含一个程序加载器，你可以用它创建 Windows 二进制文件，以及一个实现 Windows 命令调用的 DLL 库，将其转换为等效的 UNIX 和 X11 命令调用。由于 Wine 代码库的频繁更新，Ubuntu 并没有安装 Wine。请从 www.winehq.org/ 下载当前版本的 Wine。要查看你喜爱的应用程序是否被 Wine 支持，可以查看 https://appdb.winehq.org/ 上的 Wine 数据库。

其他解决方案（主要是来自 CodeWeavers 的 CrossOver）也允许使用 Microsoft 生产力应用。如果你正在寻找一种无痛的方法不仅运行 Microsoft Office，还有 Apple iTunes 和其他软件，你应该调查 CodeWeavers。CrossOver 是你可以用来让基于 Windows 的程序正常运行的最简单的程序之一。访问 www.codewavers.com 下载最新软件的试用版。

## 参考文献

- www.libreoffice.org—LibreOffice 套件的首页。
- www.documentfoundation.org—Document Foundation 的首页。
- www.openoffice.org—OpenOffice.org 办公套件的首页。
- [https://wiki.gnome.org/Projects/GnomeOffice](https://wiki.gnome.org/Projects/GnomeOffice)—GNOME Office 站点。
- www.koffice.org/—KOffice 套件的首页。
- http://www.pdfdeit.cz/en/index.html—PDF Edit 的首页。
- www.codewavers.com/—CodeWeavers 的 CrossOver Office 首页，它允许你在 Linux 下运行某些 Windows 程序。

## 第 6 章 多媒体应用

### 本章内容

- 音频与音乐
- 图形处理
- 在 Ubuntu 中使用数字相机
- 在查看器中刻录 CD 和 DVD
- 查看视频
- 参考文献

二十一世纪已成为数字生活的世纪，全球数百万计算机用户正在拥抱每一项新技术，例如数字相机、MP3 播放器和其他各种多媒体设备。10 年前，你可能在 Windows 安装中散落着少量 WAV 文件，而今天，你更有可能在不同的计算机上散布着数百甚至数千个 MP3 文件。随着视频剪辑、动画和其他图形出现，组织和维护这些庞大库的需求驱动着应用程序的发展。流行的专有应用（如 iTunes 和 Google 图片）曾是 Linux 用户渴望之的，但现在已经存在开源应用提供了真正的替代方案，对于某些人来说，这些是他们需要全职使用 Linux 的最终原因。

本章概述了 Ubuntu 自带的一些基础多媒体工具。在本章中，你将发现如何创建自己的 CD、看电视、将音频 CD 刻录为开源的 Ogg 音频格式进行播放，以及如何管理你的媒体库。你还将了解到 Ubuntu 如何处理图形、图片等内容。

### 音频与音乐

Linux 曾因对音频和通用多媒体应用支持不良而闻名。然而，近年来在纠正这一方面取得了巨大进展，现在的支持已经比以前好得多。（知道这可能会让你会心一笑：微软不再支持 Microsoft 声卡了，但 Linux 用户仍然享受到它的支持，这无疑只是为了惹恼雷德蒙德的人们。）然而，UNIX 一直拥有良好的多媒体支持，正如 UNIX 作者和大师 David Taylor 所指出的那样：

> 最初的计算机图形工作是由 Evans 和 Sutherland 在 UNIX 系统上完成的。MIT 媒体实验室的创新是在 UNIX 工作站上完成的。1985 年，我们在 HP 实验室正在 UNIX 工作站上创建复杂的多媒体沉浸式环境，所以也许 UNIX 比暗示的更具多媒体特性。Linux 支持的局限并不意味着 UNIX 具有相同的局限性。我认为这是一个后勤问题，因为有数百种声卡和数千种可能的 PC 配置。

最后一句说得很好。UNIX 支持的硬件范围有限；而 Linux 拥有数百种声卡。声设备驱动程序长期以来缺乏厂商的支持，而且 Linux 的音频子系统没有标准。

在这一节中，你将学习声卡、音频文件格式以及 Ubuntu 提供的音频应用程序。

### 声卡

Ubuntu 支持多种音频硬件和软件。两种声卡驱动程序模型在当今市场中竞争激烈：

- ALSA，高级 Linux 音频架构（Advanced Linux Sound Architecture），它是完全开源的。
- OSS，开放声音系统（Open Sound System），提供免费和商业驱动程序。

Ubuntu 使用 ALSA 是因为 ALSA 是内核的音频架构，从 2.6 系列一直现在的 4.x 系列。在这里可能仍然找到 OSS，但它已不再被广泛使用，应被视为废弃。

ALSA 支持很长的声卡列表。如果你感兴趣，可以在 www.alsa-project.org/main/index.php/Main_Page 查看列表，但 Ubuntu 在初始安装时会检测大多数声卡，并应该检测任何新增设备。可以通过搜索 Dash 配置音频偏好图形工具。

此外，Ubuntu 使用了一层名为 PulseAudio 的额外软件。PulseAudio 是一个音频服务器，作为具有音频输出的多媒体程序与 ALSA 内核驱动程序之间的协调者。年来，Linux 中使用了许多音频服务器，每种都有不同的优点、可用性问题和文档水平。

这些不同的音频服务器经常被迫在同一台计算机上运行，导致了各种混乱和问题。PulseAudio 旨在取代它们，作为一个单一处理器接受来自任何常用音频服务器（如 ESD、OSS、GStreamer 和 Jack）API 的应用程序输出，并将各种输出路由在一起。这提供了许多优势，包括单独控制各种程序的输出音量。

PulseAudio 仍然很年轻，它的潜力尚未完全发挥；然而它在过去的几个版本中已经成熟，并且比任何时候都更好、更强大。虽然在包含 PulseAudio 的第一个版本中存在稳定性问题投诉，但在罕见的硬件组合和特殊情况下似乎不再是问题，越来越多的功能已经实现。关于 PulseAudio 的更多信息，请参阅 www.pulseaudio.org。

### 调整音量

Ubuntu 提供了一个实用的实用程序，可以使用它来控制计算机各种输出的音量。对于简单的主音量控制，只需点击屏幕右上角的扬声器图标并向左或向右滑动，如图 6.1 所示。
