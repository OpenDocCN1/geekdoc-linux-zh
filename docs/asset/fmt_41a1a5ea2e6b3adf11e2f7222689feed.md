
- http://sunsite.unc.edu/emusic-l/—EMUSIC 列表主页，包含 MIDI 规范、关于构建 MIDI 触发器的章节、大量电子音乐设备评论，以及购买第一台键盘的建议。
- http://mitpress.mit.edu/Computer-Music-Journal/CMJ.html—MIT 的《计算机音乐期刊》存档，是电子音乐技术文章极极资源，以及指向其他电子音乐网站的长链接列表。
- http://www.ircam.fr/index-e.html—法国声学与音乐协调研究所 (IRCAM) 的 WWW 服务器。
- http://www.yahoo.com/Computers_and_Internet/Multimedia/Sound—音频相关链接。
- http://www.yahoo.com/Computers_and_Internet/Multimedia/Archives—各类音频存档链接。

## 流媒体音频

网络上较新的音频格式之一被称为流媒体音频（streaming audio）。这实际上是多种格式之一，从特殊服务器向流媒体音频播放器提供数字音频流。目前有两家公司提供最著名的流媒体音频形式：Progressive Network 的 RealAudio 和 Xing Technologies。后者使用 MPEG 向专门设计的客户端播放器传输音频和视频，而前者则使用专有格式。

这两家公司目前都免费提供名为“播放”的客户端软件，并支持包括 Linux 在内的多个平台。这两种格式都需要商业级服务器（由公司向音频提供商出售）来流传输音频。在两种情况下，Linux 版本的客户端软件都是自包含的，这意味着它不需要额外的软件或配置。甚至不需要应用程序资源。用户只需要下载压缩的软件包包，设置好相应的 MIME 类型和 `mailcap` 条目，然后找到提供流媒体音频的服务器即可。RealAudio Player 比 StreamWorks 播放器多几个配置选项。其中大部分与选择传输类型（如 `UDP` 或 `TCP`）、使用哪个端口或多个端口以及使用的传输速度（14.4、28.8 或更高）有关。两者都允许在没有浏览器的情况下使用播放，但结合浏览器使用效果最佳。

> 提示 RealAudio 可以在 http://www.realaudio.com 找到。Xing Technologies 可以在 http://www.xingtech.com 找到。这两个网站都有指向其服务器软件并提供各种流媒体音频的内容提供者的链接。

为了让用户能够从浏览器访问流媒体音频内容，必须设置 `mailcap` 和 MIME 配置文件。在 Netscape 3.0 中，这是一个相当简单的过程：

1. 首先，打开 `Options`（选项）下拉菜单并选择 `General Preferences...`（常规首选项...）选项。`General Preferences` 窗口将打开，显示多个标签页。
2. 选择 `Helpers`（助手）以查看当前配置的助手应用程序列表。
3. 右侧有一个标记为 `New`（新建）的按钮。点击此按钮。弹出的窗口将提供一系列输入字段，用于描述你可能在 Web 上遇到的一个或多个文件类型的应用程序。
4. 在 `Description`（描述）字段中，输入音频播放器的名称（StreamWorks 或 RealAudio）。
5. 在 `Type`（类型）字段中，你需要指定适用于你所需的流媒体格式的 MIME 类型：对于 StreamWorks，MIME 类型是 `application/x-xdma`；对于 RealAudio，MIME 类型是 `audio/x-pn-realaudio`。
6. `Suffix`（后缀）字段应包含感兴趣内容文件的后缀。对于 RealAudio，这是 `.rma`，对于 StreamWorks 是 `.xdm`。
7. 最后，在 `Handle By`（处理方式）标题下，有一个浏览器可访问这些文件的方法选择。
8. 选择 `Application`（应用程序）并输入音频播放器的完整路径。RealAudio 播放器名为 `replayer`，StreamWorks 播放器名为 `swplayerer`。
9. 点击 `OK`（确定）按钮，你的浏览器现在就可以准备访问流媒体文件了。

图 8-4：Netscape 3.0 助手窗口。

图 8-5：当你的播放器位于防火墙后，互联网上的 RealAudio 音频服务器

当你的播放器位于防火墙后要访问流媒体服务器时，必须配置防火墙允许音频数据包通过。对于 StreamWorks 音频流，必须配置防火墙允许 `UDP` 数据包通过端口 `1558`。RealAudio 流可以使用 `TCP` 或 `UDP`。`TCP` 端口为 `7070`，且该连接必须允许入站和出站数据包。这种的更佳配置是仅允许通过现有连接入站数据包，但你的防火墙软件可能不提供此类配置。RealAudio 也支持 `UDP`，可以配置为使用单个端口或端口范围。默认情况下，使用 `6970` 到 `7170`（包含在内）之间的端口范围。这两种播放器都可以通过其网络配置选项（通过下拉菜单）配置为使用。

## 第 8 章：真多媒体

图 8-6：StreamWorks 播放器。

RealAudio 服务器需要 2MB 的磁盘空间。这意味着，使用 14.4 压缩算法， 1 小时的音频节目将占用 3.6MB 的磁盘空间。RealAudio 2.0 将编码大多数常用格式，但也提供了自己的两种格式，一种适用于 14.4 调制解调器速度，另一种适用于 28 速度。前者提供 AM 级音质，后者提供 FM 级音质。

服务器附有一份 105 页的 PDF 文档。PDF 是 Adobe 的格式，为多种平台（包括各种 UNIX 系统）提供阅读软件。管理员文档非常详尽。

## UNIX Web 服务器

| 连接速度 | 容量 |
| :--- | :--- |
| 56 kbps | 10 路流 |
| ISDN BRI | 50 路流 |
| T1 连接 | 100 路流 |
| T3 连接 | 3000-4000 路流 |

表 8-5：支持的平台。

| RealAudio | StreamWorks |
| :--- | :--- |
| Sparc Solaris, SunOS, Windows NT, FreeBSD, SGI IRIX, Linux, Power Macintosh 7.5 | SGI IRIX, Sparc Solaris, Linux, Windows NT |

# 互联网上的数字视频

北美大多数视频信号（包括录像带、电缆电视和空中传输）都是根据国家电视标准委员会定义的广播级。NTSC 标准 dic-

# 318 UNIX Web 服务器书籍

该规定信号以每秒 30 帧的速度以隔行的方式显示，奇数和偶数水平线（即扫描线）在每次扫描时交替。此过程将每帧划分为两个场，从而每秒产生 60 个场。视频图像的垂直分辨率由扫描线的数量决定（NTSC 标准定义为 525 条）。交替奇偶扫描线是图像隔行的另一种形式（请参阅第 7 章，介绍了另一种并非如此均匀划分的形式）。

不言说，数字化和复制广播级视频信号需要速度、硬盘存储空间，以及这些需求通常是计算机工作站无法提供的内存容量。尽管高端数字化系统能够满足需求，但海量的数据会让大多数机器应付不堪。一秒钟等相当于 NTSC 的数字化视频包含 30 帧（640 X 480 像素）、24 位图像，大约占用 26MB 的磁盘空间。在没有音频的情况下，一分钟就超过了 1.5GB！

这些令人望而畏的需求导致了网上低质量视频片段的接受。这些文件与模拟和高端数字视频源的不同之处在于，它们不是以隔行场显示，而是作为一系列图像显示。由于这个原因，网上的数字化视频文件通常被称为动画（animations），因为它们的显示方法类似于卡通片，或者超越了传统的视频。由于动画播放通过快速（或不快速）显示一系列单独图像来提供运动的幻觉，视频（video）、动画（animation）和电影（movie）这些术语是被交叉使用的。

## 捕获视频输入流

与其对应的是，UNIX 机器上的视频硬件差异很大。大多数（如果不是所有）视频录制软件都是商业分发的，因为必须为特定的输入卡进行定制。许多 Silicon Graphics 机器都配备了 MovieMaker 和 MoviePlayer 应用，Sun 为其某些视频输入板分发视频录制和编辑软件。要查询你的机器是否有可用的视频录制器/编辑器，最好联系制造商或在相关的 Usenet 新闻组提问。

## 视频采集程序

以下应用程序均从 `ftp://sunsite.unc.edu/pub/Linux/apps/video` 获取，支持 Linux 下的一些视频采集卡：

- `PMS-grabber.2.0.tgz`—支持 Pro MovieStudio，这是一种用于 PC 的商业视频数字化卡。
- `ScrMachl_1.0.tar.gz`—FAST Screen Machine II 视频采集卡的驱动和实用程序。
- `ScreenMachin.2.0.tgz`—FAST Screen Machine II 实时视频叠加的驱动程序。
- `fgrabber`—WinVision B&W（黑白）视频采集卡的驱动。
- `vid_src-0.6.tgz`—Linux 和 DOS 下 Video Blaster 视频卡用法。

你不一定得有一个视频数字化卡才能制作电影。由于动画只不过是图像的序列，因此可以将一系列图像串联并将它们转换为电影。当然，这样做比从输入板捕获视频要耗时得多，但如果你无法使用任何视频数字化设备，尝试这种方法会很有趣。

## 动画文件格式

本节回顾了目前互联网上使用的大多数动画文件格式。这些格式并不代表所有可用的动画或视频文件格式，但它们是你在日常使用中最可能遇到的格式。实际上，所涵盖的许多格式正在逐渐被遗忘，但它们是作为参考点进行讨论，以便你更好地了解不同格式之间的差异。对于大多数当前 Web 浏览器不直接支持的格式，我们在每个文件格式后列出了相应的 MIME 类型。

## GIF89a

Web 的优点之一是它让一些较旧的概念和技术焕发生机。HTML 是 SGML 的子集，SGML 是一种存在已久的格式语言（从计算机术语而言）。TCP/IP 已经作为 UDP 形式使用了多年，但直到互联网开放并包含世界维网之后，它才真正兴起。同样，GIF 图像格式从其最早的发布之一（GIF87a）起就支持动画，但直到最近这项功能才真正流行起来。

使用 GIF 图像格式的动画利用了该格式的设计，允许将多个图像存储在单个文件中。每幅图像被称为一*帧*（frame），就像电影胶片中的帧一样。GIF89a 格式还提供了额外功能，如图像显示之间的延迟、透明颜色、注释，以及帧在显示后如何删除（如果删除的话）。Netscape 添加了一些自己的扩展（在文件中支持特定应用程序扩展的区域），支持诸如图像循环等功能。

所有 Web 浏览器在某种程度上都支持 GIF89a 格式。某些不支持动画功能，但在这些情况下，它们只会显示序列中的第一张图像。Netscape 2.0 或更高版本的浏览器支持 Netscape 扩展，Microsoft 的 Internet Explorer 支持动画（尽管它可能不支持 Netscape 的循环扩展）。在任何情况下，使用 GIF89a 格式的动画在所有浏览器上至少应以静态格式（无动画）显示。注意，GIF 格式没有指定在动画中包含音频的方法。

我们将在“视频软件”章节中介绍使用 GIF 格式制作动画的示例。

> 有关 GIF89a 格式以及如何使用它创建动画图像的详细讨论，请参见 Royal Frazier 的 GIF 动画页面，地址：http://www.ecafe.org/tools/gifanim/gifanim.htm。

## QuickTime

MIME 类型：
`video/quicktime` `mov` `moov` `qt`

QuickTime 是 Apple 的专利动态数据格式，最初实现在 Macintosh 上。自从 Apple 针对 Microsoft Windows 环境和 Silicon Graphics 机器发布了 QuickTime 启用程序，这种格式已成为网络上日益受欢迎的动画文件格式。这些电影可以在带有 IRIX v5.1 及更高版本的 Silicon Graphics 机器上使用 MoviePlayer 播放，也可以在任何带有 Xanim 的其他 UNIX 系统上播放（有关 Xanim 的信息请参见下一节“视频软件”）。

关于 QuickTime 电影最重要的一点是，它们通常在 Macintosh 操作系统下创建，该系统将文件分为两个独立的“分支”（forks）：数据分支（data forks）和资源分支（resource forks）。资源分支包含描述文件属性的小程序代码块，而数据分支包含实际数据。

QuickTime 的最新版本同时支持音频采样（参见上一节“音频格式”），因此可以包含占用空间极小的音轨。Xanim（参见本章后文“视频软件”）可以播放扁平化 QuickTime 电影的视频和音频段。

#322 UNIX Web 服务器

如果你可以访问 Macintosh，可以使用 QuickTime Starter Kit 自带的 Movie Converter 工具或公开的 Flattov 完成转换。Apple 有一个致力于 QuickTime 的站点：http://quicktime.apple.com。Xanim 的作者 Mark Podlip 提供了 UNIX 系统的 QuickTime 扁平化程序，可以在 `ftp://xanim.va.pubnik.com/misc/flatten-c.z` 找到。

## MPEG

MIME 类型：
`video/mpeg` `mpe`

上一节“格式”中讨论的 MPEG 压缩可以用于音频和视频文件。通过硬件和软件的适当组合，在许多平台上可以实现实时压缩和解压缩。压缩的使用减少了高质量音频视频文件传输的带宽，而没有过度牺牲原始信号质量，使其成为在线发布多媒体的理想方式。

互联网上的大多数 MPEG 电影没有字幕，其中一些支持 MPEG-1 2 层音频。包含音频数据的 MPEG 电影有时被称为 Xing 电影，指的是 Xing Technology 公司。Xing 为包括 Linux 和 Solaris 在内的许多平台推出了许多廉价的 MPEG 音视频录制和播放工具。

`mpeg2play`（后文）是另一种在 X Windows 下播放 MPEG 电影的免费工具。

有几种方法可以将 QuickTime 电影转换为 MPEG 文件。

- `ftp://mm-ftp.cs.Berkeley.edu/pub/multimedia/mpeg/encode/`—加州大学伯克利多媒体项目。
- http://www.arc.umn.edu/GVL/Software/mpeg.html—来自明尼苏达大学图形可视化实验室。
- http://www.mcs.anl.gov/home/planman/movie/howto.html—为你的 XMosica 制作 MPEG 电影。

## AVI

MIME 类型：
`video/x-msvideo` `avi`

AVI 是微软的专有视频格式，也称为 Windows 视频。它的性能特性与 QuickTime 类似，并且有许多免费的 AVI 转 QuickTime 以及 QuickTime 转 AVI 的转换器可用。与 QuickTime 文件一样，AVI 文件可以包含音频轨道。

Xanim（参见本章后文的“视频软件”章节）可以在 X Windowing 环境下播放 AVI 电影的视频和音频段。

## FLI & FLC

MIME 类型：
`video/x-fli` `fli,flc`

FLI 和 FLC 是 Autodesk 的“Flick”格式。FLI 是 Autodesk Animator 的原始格式，分辨率限制为最大 320 X 200 像素，64 色调板，且每个文件最多 4,000 帧。FLC 是随 Animator Pro 引入的第二代动画格式，支持更大的图像（宽度和高度均可达 65,536 像素），但每帧限制使用 256 色调板。这两种格式都不支持音频。

Xanim（参见本章后文的“视频软件”章节）可以在 X Windowing 环境下播放 AVI 动画。

> 关于动画文件格式的更多详细信息可以通过 http://www.viewpoint.com 获取。该网站包含了旧的 Avalon 3D 数据文件存档。

## IFF/ILBM

MIME 类型：
`video/x-iff` `iff`

IFF/ILBM（交换文件格式）由 Electronic Arts 定义为一种多媒体文件标准，旨在方便图像、文本、音频和其他数据的传输。它专门设计用于与 Amiga 硬件高效工作。IFF/ILBM（交错位图）既是一种图形格式也是一种动画格式。

# 324 UNIX Web 服务器

Xanim（参见本章下一节的“视频软件”）可以在 X Windowing 环境下播放 IFF 动画。

## 视频软件

为了使用这些播放实用程序之一查看大型动画文件，必须拥有大量的 RAM。例如，如果你有一台带有 8MB RAM 运行 X Windows 的 Linux 机器，并尝试播放大型动画文件（超过 2MB），可能会遇到问题。许多人 report说，如果没有足够的 RAM，平化 QuickTime 电影的声音在每次访问硬盘时都会断断续续。

本节讨论的某些应用程序仅适用于特定平台，因此最好熟悉各种可提供的不同选项，然后决定哪些工具最适合你。在程序名称之后，我们提供了你需要放入 `mailcap` 文件的条目，以及获取更新的网站 URL。

## WhirlGIF

http://www.msg.net/utility/whirlgif
这个由 Kevin Kadow 开发的工具不是用于查看动画的，而是用于创建它们的。WhirlGIF 获取一系列 GIF 图像并将它们合并为一个 GIF 文件，适当设置 GIF 头，以便该文件可以在支持 GIF 规范此项功能的 Web 浏览器中作为 GIF 动画使用。WhirlGIF 是一个命令行工具，意味着它没有 GUI，但对于大多数 Linux（或其他 UNIX）用户来说，这应该不是问题。

WhirlGIF 作为输入的图像序列可以使用任意数量的工具创建。用于此的两个非常好的工具是 POV-Ray 和 GIMP。前者提供了一种在帧内精确定位对象的方法，例如，地球仪的旋转可以使用帧与帧之间相同的旋转量来实现。GIMP 可以创建一系列从一种颜色过渡到另一种颜色的图像，例如流过文本标志线条的色彩波浪，或者制作动画旋转淡出效果，即图像在缓慢淡出的同时绕其中心旋转。

## 第 8 章：真多媒体

WhirlGIF 带有源代码和一些简单的文档。它的简单性让作者预计它在未来某个时候会被移植为 GIMP 的插件。

## Xanim

基于 X11 的动画查看器 Xanim 是一个很棒程序，可以让你查看网络上的任何动画文件格式。它显示了许多动画和图形格式，包括 FLI、FLC、IFF、AVI 和 QuickTime（参见图 8-7）。

Xanim 的最新版本还支持 AVI（原始和 ADPCM）以及 QuickTime 音频。许多网站（如 CNN、ESPN 和 SciFi Channel）现在从它们的网站提供 QuickTime 音频/视频片段。许多此类 QuickTime 音频/视频片段需要 Xanim 构建时支持 Radius Cinepek。幸运的是，Xanim 的作者 Mark Podlicec 为许多平台提供了预编译的对象文件，这些文件可以链接到 Xanim 源码中；此外，在 Linux 下，Xanim 使用 Linux 音频驱动程序（在本章早期介绍）在 8 位和 16 位音频卡上进行编译。有关如何添加此支持的更多文档（在 Makefile 中）。例如，如果音频文件指定在动画文件之后，则可以使用任何动画文件类型播放 `.wav` 文件，如下面的命令行所示：
