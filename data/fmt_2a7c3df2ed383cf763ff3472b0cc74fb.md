
LAME 最初代表 "Lame Ain't an Mp3 Encoder"，但它很早已经演变为一个完整的 MP3 编码器，其软件根据 LGPL 许可提供。它包含在 VideoLAN 和 FFmpeg 中，并且 Yum 将从 Livna 下载以支持 MPlayer 和 Xine。

由于许可和专利问题，Fedora 不包含对 MP3 文件的支持。XMMS 和 Noatun 等多媒体播放器已删除了 MP3 播放功能。作为 MP3 的替代方案，你可以对音乐文件使用 Ogg Vorbis 压缩（`www.vorbis.com`）。

# CD 刻录机

从 `www.kde-apps.org` 可以获得几个用于 CD 音乐和 MP3 写入（写入和刻录仪）的 CD 写入程序。这些包括 `Kb` 和 `KAudioCreator`（CD 刻录仪），见表 6-6。对于 GNOME，你可以使用 `CD-REC` 和 Nautilus CD 刻录机，后者集成在 Nautilus 文件管理器中，后者是 GNOME 桌面的默认文件管理器。使用 `mkisofs`、`dcdirect` 和 `cda2wav` CD 写入程序，它们作为 Fedora 发行版的一部分被安装。GNOME 还有具有随 Fedora 安装的两个音频刻录仪：`Grip` 和 `Juicer`。

| 应用程序 | 描述 |
| :--- | :--- |
| `K3b` | KDE CD 写入界面 |
| `KAudioCreator` | KDE CD 刻录机和刻录仪 |
| `dvauthor` | 用于 DVD 工具 (`dvauthor.sourceforge.net`)。从 `rpm.livna.org` 下载 RPM。 |
| `Qauthor` | `dvauthor` 的 KDE 前端 (`www.kde-apps.org`) |
| `DVDStyler` | 用于 GNOME 的 DVD 制作应用程序 (`dvdstyler.sourceforge.net`)。 |

**表 6-6：DVD 刻录机**

# 视频应用程序

多个项目提供了电视、视频、DivX、DVD、多媒体应用程序（见表 6-7）。许多项目以源码形式提供，你需要编译并安装，你可以从 `rpm.livna.org` 下载 RPM 包。

## 222 第 2 部分：应用程序

`Xine` 是一种用于 Linux/Unix 系统的多功能视频播放器，可以播放视频、DVD 和音频盘。访问 `xine.de` 获取更多信息。`Xine` 以源码形式提供，你需要编译并安装，你可以从 `rpm.livna.org` 下载 RPM 包。

# 视频与 DVD 播放器

`d.sourceforge.org` 提供 DVD 和媒体播放器。在这里你可以找到 VideoLAN、`MPlayer` 和 `Xine` 等播放器的链接。

- `VideoLAN` 项目 (`www.videolan.org`) 为大多数格式提供网络流支持，包括 MPEG-4、`x264` 和 MPEG-2。它包含一个跨平台多媒体播放器 `VLC`。
- `MPlayer` 是目前最流行且功能强大的多媒体/DVD 播放器之一。它是 RealPlayer 和 Windows Media Player 的跨平台开源替代方案。`MPlayer` 支持 DivX。你可以从 `www.mplayerhq.org` 下载 `MPlayer`。`MPlayer` 使用大量的支持库和支持性应用程序，如 `lirc`、`lame`、`izo` 和 `aalib`。如果在显示视频时遇到问题，请确保检查不同视频设备的设置，选择最合适的。
- 随 Fedora 安装 `Totem` 是基于 `Xine` 的 GNOME 电影播放器。要扩展 `Totem` 的功能，你需要额外的 GStreamer 插件（见图 6-10）。`Totem` 现在具有针对 DVB、MyTV 和 YouTube 的插件。

# 第 6 章：图形与多媒体 223

- `Kaffeine` 随 KDE 安装，是一款支持多种格式的 KDE 多媒体播放器，包括 DVD、DVB 和音乐 CD。
- 如需 DVD 转码和对 DivX 的支持，请查看 `DVD::rip` 项目。`www.exit1.org/dvdrip`。
- `kdtv` 是 KDE 电视查看器
- `tvtime` 是电视查看器
- 额外的解码器支持由 `ffmpeg` 和 `x264` 提供。`x264` 解码器是由 VideoLAN 开发的 H.264 高清解码器的开源版本。

| 项目与播放器 | 网站地址 |
| --- | --- |
| LinuxTV.org | 包含视频、电视和 DVD 网站的链接：`linuxxtv.org` |
| DVD 播放器列表 | `dvd.sourceforge.net` |
| `Xine` | Xine 视频播放器：`xinehq.de` |
| `Totem` | 基于 Xine 并使用 GStreamer 的 GNOME 的 Totem 视频和 DVD 播放器，包含 DVB、YouTube 和 MythTV 的插件：`xinehq.de` |
| `VideoLAN` | 网络多媒体流媒体，包含 x264 高清支持。`www.videolan.org` |
| `MPlayer` | MPlayer DVD/多媒体播放器 `www.mplayerhq.hu` |
| `MythTV` | 具有 DVD、DVR 和电视功能的家庭媒体中心 `www.mythtv.org`（软件包位于 rpms 目录） |
| `DVD::rip` | DVD 转码和 DivX 软件 `www.exit1.org/dvdrip` |
| `kdtv` | KDE 电视查看器 |
| `tvtime` | 电视查看器器，`tvtime.sourceforge.org` |
| Linux 版 DivX | `labs.divx.com/DivLinuxCodec`（需要下载） |
| `XviD` | 开源 DivX，`www.xvid.org` |

# 表 6-7：视频与 DVD 项目及应用

Fedora 软件存储库中没有任何开源软件可以对商业 DVD 执行 CSS 解密。然而，你可以：

下载并安装 `libdvdcss` 库（`rpm.livna.org`），它通过将 DVD 解密为块设备来绕过 CSS 解密，允许你使用任何 DVD 播放器运行商业 DVD。它还提供了无区访问。请记住，在某些要求 DVD 播放器拥有 CSS 许可的国家，这可能是不合法的。

注意：要在 Fedora 上播放 DivX 媒体，请使用 `labs.divx.com/DivXLinuxCodec` 中的 Linux 版 DivX 解码器。

最初，许多播放器不支持 DVD 菜单。通过 `libdvdnav` 和 `libdvdplay` 库，这些播放器现在具备了完整的 DVD 菜单支持。`libdread` 库提供了基础的 DVD 接口支持，例如读取 IFO 文件。你可以从 `rpm.livna.org` 下载这些软件包的 RPM 二进制文件。

![](img/9a8872dc6f2acaed163529fd9d421e05_225_0.png)

图 6-10：Totem 电影播放器

# 电视播放器

`www.linuxtv` 网站提供了 DVD、数字电视广播（DVB）和多播的详细链接。该网站还提供了许多 Linux 视频应用程序的下载。

Fedora 上的主要电视播放器是 `tvtime`，它与许多常见的视频采集卡配合，依赖于为这些卡上的电视调谐芯片（如 Conexant 芯片）开发的驱动程序。它只能显示电视图像，没有录制或文件播放功能。更多信息请查看 `http://tvtime.sourceforge.net`。

对于 KDE，有多个视频应用程序可用或正在开发中，包括 `kdekv`。请访问 `www.kde-apps.org` 查看项目。对于基于 Gnome 的播放器，请访问 `www.gnomefiles.org`。许多程序在 Fedora 软件存储库中均可用。

# HDTV 支持
