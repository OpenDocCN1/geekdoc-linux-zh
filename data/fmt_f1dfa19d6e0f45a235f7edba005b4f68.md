
为了能够发送视频，您需要一个在 Linux 中受支持的摄像头。虽然并非所有摄像头都在 Linux 中受支持，但您仍有几十种型号可供选择。以下部分向您展示如何设置摄像头并使用 GnomeMeeting 进行视频会议。

### 获取受支持的摄像头

与电视采集卡的支持类似，摄像头支持通过 `video4linux` 接口提供。一些受支持的摄像头具有并行端口接口，尽管目前 Linux 支持的大多数摄像头都需要 USB 端口。

要检查您的摄像头是否受支持，请查看 `/usr/src/linux*/Documentation` 目录。并行端口视频摄像头中的一些在 `video4linux` 子目录中有描述；但是，大部分受支持的摄像头列在 `usb` 目录中。

> **提示：** 经过一番研究，我购买了一款 Logitech QuickCam Pro 3000。该摄像头的驱动程序是为 Philips USB 摄像头制作的，但它也适用于 Logitech、Samsung、Creative Labs 和 Askey 的摄像头。在购买之前，我在 `www.smc.c.demon.nl/webcam` 上查看了驱动程序的描述。

受支持的 USB 摄像头应被自动检测，以便在插入时自动加载必要的模块。只需启动 `gnomemeeting` 或 `xawtv` 命令，如果一切正常，您应该在 Linux 桌面上看到来自摄像头的视频。以下是我输入的一些用于检查摄像头是否正常工作的命令：

```bash
# lsmod
pwc
43392 1
videodev
5120 2 [pwc]
usbcore
59072 1 [audio pwc usb-uhci]
```

`lsmod` 的输出显示 `pwc` 驱动程序已加载，并与 `videodev` 模块和 `usbcore` 模块相关联。要查看关于 `pwc` 模块（特定于此摄像头）的信息，我输入了以下 `modinfo` 命令：

```bash
# modinfo -p pwc
filename:
/ lib/modules/2.4.18-0.13/kernel/drivers/usb/pwc.o
description: "Philips USB webcam driver"
author: "Nemosoft Unv. <nemosoft@smcc.demon.nl>"
license: "GPL"
parm:
size string, description "Initial image size. One of sqcif, qcif, qcif, sif, cif, vga"
parm:
fps int, description "Initial frames per second. Varies with model, useful range 5-30"
parm:
fbufs int, description "Number of internal frame buffers to reserve"
parm:
m buffs int, description "Number of external (mmap(ed) image buffers"
parm:
trace int, description "For debugging purposes"
parm:
power_save int, description "Turn power save feature in camera on or off"
parm:
compression int, description "Preferred compression quality. Range 0 (uncompressed) to 3 (high compression)"
parm:
leds int array (min = 2, max = 2), description "LED on,off
```

time in milliseconds"

parm: dev_hint 字符串数组 (min = 0, max = 10)，描述 "设备节点提示"

输出显示 `pwc` 是一个飞利浦 USB 摄像头驱动程序。它还展示了你可以通过 `pwc` 模块设置的选项，以便更改图像大小、每秒帧数以及调试级别等。这些信息关于你的摄像头驱动器的选项，如果你以后想要调整摄像头的行为或追踪问题，将非常有用。

## 运行 GnomeMeeting

你可以从终端窗口启动 GnomeMeeting（输入 `gnomemeeting&`）或从 Gnome 菜单启动（程序 → 互联网 → GnomeMeeting）。图 8-7 显示了一位不情愿的作者正在视频 conferencing (ILS) 服务器上搜索朋友。

![](img/1744bde8c889adfab3fc911e1687fecf_327_0.png)

在打开的 GnomeMeeting 窗口中，你可以点击书本图标打开搜索窗口（如图 8-7 右侧所示）。搜索窗口允许你连接到 ILS 目录。通过在搜索过滤器中输入姓名，你可以按名字、姓氏、电子邮件地址或位置搜索可能连接到该服务器的人。从出现的列表中选择一个联系人，如果对方接受你的呼叫，你就可以开始视频 conferencing。

视频窗口下方的标签页让你可以调整音频水平和视频外观。历史记录标签页显示你活动的日志。

## 播放视频

如果你想展示视频片段或播放来自互联网的视频流，你在 Linux 下的软件选择有些有限。你可以使用 Xanim X 查看器播放各种视频格式，例如 Quicktime 和 AVI。RealPlayer 的 Linux 版本允许你播放 RealMedia 内容。

由于你可能会观看互联网上的视频片段或视频流，你可能希望将这些视频技术整合到你的互联网浏览器中。Netscape 允许通过添加所谓的*插件*或*辅助应用程序*，在 Netscape Navigator 互联网浏览器中播放视频（以及其他数据类型）。Linux 版的 Plunger 插件允许你将多种不同的视频和音频技术整合到 Netscape 中。

### 使用 Xanim 查看器

Xanim 是一个运行在你的 X 桌面上的查看器。它可以播放动画、视频和音频文件。在 Red Hat Linux 7.1 之前，`xanim` 包是 Red Hat Linux Powertools CD 的一部分。虽然不再有 Powertools CD，但你可以从任何 Red Hat FTP 站点下载 `xanim` 包。

Xanim 支持的媒体格式类型包括：

- **动画** — 支持 FLI、FLC、IFF（支持各种压缩、颜色循环和显示模式）、GIF87a（单图像和多图像支持）以及 GIF89a（带有动画扩展）、DL 动画、Amiga PFX、Amiga MovieSetter 和 Utah Raster Toolkit。

- **AVI 动画** — 支持多种视频编解码器（*编码器/解码器*），包括：IBM Ultimotion、JPEG、Motion JPEG、Intergraph JPEG、Microsoft Video 1、Radius Cinepak、Intel Indeo 3.1、Intel Indeo 3.2、Intel Raw YUV、Creative CYUV、未压缩 RGB、游程编码和可编辑的 MPEG。

- **Quicktime 动画** — 支持多种视频编解码器，包括：未压缩原始视频、Apple Graphics、Apple Animation、Apple Video、Radius Cinepak、Intel Indeo 3.1、Intel Indeo 3.2、Intel Raw YUV、Component Video、Photo JPEG、Kodak Photo CD 和 Microsoft Video 1。

- **SGI 电影格式文件** — 支持多种视频编解码器，包括：未压缩 RGB、MVC1、MVC2 和 JPEG。

- **MPEG 动画** — 仅支持 Type I MPEG 帧（忽略 Type GB 和 Type P 帧）。

你需要阅读单独的说明文件才能添加 Radius Cinepak、Intel Indeo 和 Creative Technology CYUV 支持。你可以在 `/usr/share/doc/xanim*` 目录中找到这些说明文件。除了视频和动画，Xanim 还可以播放多种不同的音频格式。以下是 Xanim 支持的音频格式列表：

- **Quicktime 音频** — 支持这些编解码器：Unsigned PCM、signed PCM、uLAW、IMA4、GSM 6.10。

- **SGI 电影格式音频** — 支持这些编解码器：Unsigned PCM 和 signed PCM。

- **WAV 音频** — 支持这些 WAV 音频编解码器：PCM、uLaw、MSADPCM、Intel DVI 和 GSM。任何没有音频的动画都可以添加 WAV 音频并通过 Xanim 播放。

- **AU 音频** — 任何没有音频的动画都可以添加 AU 音频并通过 Xanim 播放。
