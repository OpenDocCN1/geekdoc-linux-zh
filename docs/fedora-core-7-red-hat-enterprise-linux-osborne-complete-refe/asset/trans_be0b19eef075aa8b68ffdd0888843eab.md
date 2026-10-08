
## GStreamer MP3 兼容性：iPod

为了让您的 iPod 和其他 MP3 设备能够与 Rhythmbox 等 GNOME 应用程序配合使用，您需要为 GStreamer 安装 MP3 支持。由于许可问题，Red Hat 发行版中未包含 MP3 支持。不过，您可以下载并安装前面提到的 GStreamer **gstreamer-plugins-ugly** 支持软件包，该软件包维护着 Fedora 中未随发行版提供的大多数多媒体支持软件包。您可以从 **freshrpms.net** 下载该软件包。

为了从 iPod 进行同步和导入，您可以使用 iPod 管理软件，例如 GUI for iPod (gtkpod)。目前已有若干针对 iPod 操作的脚本和工具可用；包括 SyncPOD、myPod、gtkpod（iPod 的图形界面）和 iPod for Linux。请检查 **sourceforge.net** 并搜索 iPod。

## 声音应用程序

Linux 上的声音设备由构成声音系统的驱动程序支持。在当前的 Fedora 内核中，声音支持由高级 Linux 声音架构（ALSA）系统实现。ALSA 取代了之前版本中使用的 Open Sound System 的自由版本，以及最初内置的声音驱动程序（参见第 32 章）。您可以在 **www.alsa-project.org** 上找到有关 ALSA 的更多信息。

## 使用 Lame 的 MP3

LAME 最初代表 **L**ame **A**in'**t** an **M**p3 **E**ncoder（劣质不是一个 MP3 编码器），但它早已发展成为一个完整的 MP3 编码器，其软件在 **LGPL** 许可下可用。它包含在 VideoLAN 和 **FFmpeg** 中，Yum 将从 **Freshrpms.net** 下载以支持 Mplayer 或 Xine。您可以单独下载它：

```bash
yum install lame
```

由于许可和专利问题，Red Hat Linux 已移除对 MP3 文件的支持。XMMS 和 Noatun 等多媒体播放器已移除 MP3 播放功能。作为 MP3 的替代方案，您可以使用 Ogg Vorbis 压缩来播放音乐文件（**www.vorbis.com**）。

> *注意：Linux 已成为许多专业级多媒体任务的首选平台，例如为电影特效生成计算机生成图像（CGI）和动画，使用 Maya 和 Softimage 等要求苛刻的软件。Linux 图形库包括 OpenGL、MESA 和 SGI 的库。*

## 音乐应用程序

目前有许多音乐应用程序可用于 GNOME，包括声音编辑器、MP3 播放器和音频播放器。您可以使用 GNOME CD Player 播放音乐 CD，并使用 GNOME Sound Recorder 录制声音源。请检查 **www.gnomefiles.org** 上的软件地图以了解当前版本。也有许多适用于 KDE 的应用程序，包括两个媒体播放器（Kaiman 和 Kaboodle）、一个混音器（KMix）和一个 CD 播放器（Kscd）。请查看 **www.kde-apps.org** 以了解最新添加的内容。大多数发行版都安装了若干基于 X 窗口系统的多媒体应用程序。这些包括 XMMS 和 Xplaycd（CD 音乐播放器），以及 Xanim（动画和视频播放器）。

Red Hat 和 Fedora 在“声音和视频”菜单中提供 XMMS 多媒体播放器、GNOME CD Player、GNOME Sound Recorder 和 GNOME Volume Control。额外的声音和视频菜单列出了若干 KDE 应用程序，包括 KMidi、Kaboodle 和 Noatun。Fedora 还包含 HelixPlayer，即用于 RealPlayer 的开源项目。HelixPlayer 仅适用于开源媒体，如 Ogg Vorbis 文件（尽管您可以为该播放器获取 RealPlayer 音频和视频编解码器）。有关更多信息，请参阅 helixcommunity.org。您还可以从 www.real.com 下载 RealPlayer（互联网流媒体播放器）的副本。请务必选择适用于 Unix 的 RealPlayer，并将操作系统设为您的操作系统。Pulse 声音服务器允许您从设备引导和管理声音流，允许您将声音引导和修改到不同的客户端。位于 linux-sound.org 的 Linux Sound & Midi Software 网站目前持有许多声音应用程序的 Web 和 FTP 站点链接。

## CD 刻录机与提取器

www.kde-apps.org 提供了几种可用于 CD 音乐和 MP3 写入（刻录机和提取器）的 CD 刻录程序。这些包括 K3b、CD-Richve 和 KAudioCreator（CD 提取器）。对于 GNOME，您可以使用 CD-REC 和 Nautilus CD 刻录机，它集成在 Nautilus 文件管理器中，即 GNOME 桌面的默认文件管理器。它们都使用 mkisofs、cdrecord 和 cdda2wav CD 刻录程序，这些作为 Red Hat 发行版的一部分进行安装。GNOME 还包含两个随 Red Hat Fedora 安装在一起的 CD 音频提取器，Grip 和 Sound Juicer。

> **提示** 如果您的 CD 或 DVD 应用程序在查找您的 CD/DVD 播放器或刻录机时遇到困难，您可能需要检查 HAL 是否使用 /dev/cdrom 或 /dev/dvdrom 为您的 CD/DVD 设备创建适当的链接。这些链接应自动生成（参见第 32 章）。

## 视频应用程序

目前正在推进若干项目，以提供 Linux 的电视、视频、DivX、DVD 和数字电视（DTV）支持（参见表 12-4）。其中许多应用程序不在 Red Hat 或 Fedora 软件仓库中。在大多数情况下，最新版本将以源代码形式存在于原始站点上。对于这些，您必须下载源代码，然后需要编译和安装。不过，许多应用程序已经以二进制 RPM 包的形式提供，可在 rpm.livna.org 和 freshrpms.net 上找到。freshrpms.net 站点拥有更大、更新的软件包集合，尽管 rpm.livna.org 在 Fedora 上可能更可靠。建议先安装 Freshrpms 或 Livna Yum 配置文件，然后使用 Pirut（添加/移除软件）、Yumex（应用程序 | 系统工具）或命令行（终端窗口）上的 yum 命令。Yumex 具有额外的功能，允许您禁用或启用软件仓库。在混合使用 Livna 和 Freshrpms 软件仓库时，这可能是一个需要考虑的问题。您可以禁用 Livna 并使用 Freshrpms 处理所有多媒体应用程序，同时在您想要更新驱动程序（如厂商图形驱动程序）时启用 Livna。

您也可以选择在手动下载和安装软件包，尽管您还必须手动安装任何依赖项。对于像 mplayer 这样具有众多依赖项的软件包来说，这并不实用。对于没有依赖项的较小软件包，这运行良好。对于 RPM 软件包，Firefox 将提供使用 system-config-packages 自动安装 RPM 的选项。对于像 .tar.bz2 文件这样的压缩归档文件，FireFox 将自动调用 File Roller，让您能够立即解压缩并提取源代码文件到选定目录。

### 表 12-4 视频和 DVD 项目与应用程序

| 项目和播放器 | 站点 |
|---|---|
| LinuxTV.org | 指向视频、电视和 DVD 站点的链接，**linuxtv.org** |
| DVD 播放器列表 | **dvd.sourceforge.net** |
| xine | Xine 视频播放器，**xinehq.de** |
| Totem | 基于 Xine 并使用 GStreamer 的 GNOME Totem 视频和 DVD 播放器，**xinehq.de** |
| VideoLAN | 网络多媒体流媒体，包括 x264 高清支持，**www.videolan.org** |
| MPlayer | MPlayer DVD/多媒体播放器，**www.mplayerhq.hu** |
| PowerDVD | Cyberlink PowerDVD for Linux，**gocylebrink.com** |
| DVD::rip | DVD 转码和 DivX 软件，**www.exit1.org/dvdrip** |
| kdetv | KDE 电视查看器，**www.kdetv.org** |
| tvtome | 电视查看器，**tvtome.sourceforge.net** |
| DivX for Linux | **labs.divx.com/DivXLinuxCodec** |
| XviD | 开源 DivX，**www.xvid.org** |

> **提示** *对于 HDTV 接收，您可以使用 PCHDTV 视频卡（www.pchdoto.org）。对于最新的 PCHDTV 卡，您可以使用 Fedora 中包含的 c88-dvb 驱动程序。对于较早版本，您将必须下载、编译和安装单独的驱动程序。DVB 内核驱动程序默认不安装。您必须使用 modprobe 手动安装。使用可用的 dvd 工具来管理访问。您可以使用 MythTV 和 vdr 来观看和记录。*

## 视频和 DVD 播放器

dvd.sourceforge.net 提供当前 DVD 和媒体播放器的访问。在这里，您可以找到 VideoLAN、MPlayer 和 Xine 等播放器的链接。

- VideoLAN 项目（**www.videolan.org**）为大多数媒体格式提供网络流媒体支持，包括 MPEG-4、x264 和 MPEG-2。它包含一个多媒体播放器 VLC，可以在任何类型的系统上工作。
- MPlayer 是目前使用最流行且功能最强大的多媒体/DVD 播放器之一。它是 RealPlayer 和 Windows Media Player 的跨平台开源替代品。MPlayer 包括对 DivX 的支持。您可以从 **www.mplayerhq.hu** 下载 MPlayer。MPlayer 使用大量的支持库和支持应用程序，如 **lirc**、**lame**、**lzo** 和 **aalib**。如果您在显示视频时遇到问题，请务必检查不同视频设备的偏好设置，选择效果最好的一个。

