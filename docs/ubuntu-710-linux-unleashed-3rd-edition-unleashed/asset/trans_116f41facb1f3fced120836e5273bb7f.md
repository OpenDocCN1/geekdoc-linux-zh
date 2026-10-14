
Linux 中电视卡支持的发展已在 Video4Linux 项目下汇聚。Video4Linux 软件为 Ubuntu 提供对视频捕获、无线电和图文电视设备的支持。

## 视频格式

Ubuntu 能识别多种视频格式。然而，由 MPEG 组织、苹果和微软所创建的视频格式占主导地位。视频格式的核心是编解码器——视频和音频信息的编码器和解码器。这些编解码器通常是专有的，但也有免费编解码器确实存在。以下是最常见的视频格式及其关联文件扩展名的列表：

- `.mpeg`—MPEG 视频格式；也称为 `.mpg`
- `.qt`—苹果的 QuickTime 视频格式
- `.mov`—另一种 QuickTime 视频格式
- `.avi`—Windows 音频视频格式

提示

可在 http://www.freshrpms.net/ 找到为 Linux 提供 DivX 编解码器的 RPM。DivX 是一种已获专利的 MPEG-4 视频编解码器，是其同类中使用最广泛的编解码器。它允许将 MPEG-2 视频压缩 8 倍。更多信息请参见 http://www.divx.com/。

GetCodecs 应用程序是一个带 GUI 界面的 Python 脚本，它为你的 Ubuntu 系统下载、安装并配置 Ubuntu 未提供的多媒体编解码器，例如 MP3、DivX 和 DVD 编解码器。该脚本可从 http://sourceforge.net/projects/getcodecs/ 获取。

如果需要将视频从一种格式转换为另一种格式，可以使用称为 *抓取器* 的编码器应用程序。这些应用程序从视频设备（如摄像头或电视卡）获取原始视频数据，并将其转换为标准 MPEG 格式之一，或转换为静态图像格式（如 JPEG 或 GIF）。Ubuntu 不提供任何编码器应用程序（除了编码 MPEG-1 视频的 `ppmtompeg`），但你可以在 http://www.freshrpms.net/ 或其他在线来源找到它们（请参阅本章末尾的“参考”部分）。

## 在 Linux 中观看视频

默认情况下，由于许可限制，Ubuntu 不支持任何专有视频编解码器。但是，如果你从 Universe 软件源安装本节所述应用程序的完整版本，则可以恢复此功能。你可以在那里找到多媒体应用程序，如 Ogle、Xine、alsaplayer、GStreamer、Grip、MPlayer、VCDImager、VideoLAN-client、XMMS 和 Zapping。

你可以使用 Linux 软件观看电视，从电视广播中保存单个图像（拍摄快照），保存一系列快照以构建动画序列，或者捕获视频、音频或两者。以下各节介绍了你可以利用 Linux 多媒体软件为你服务的几种方式。

你可以使用 Xine 观看 MPEG 和 DVD 视频。Xine 是一款功能多样且流行的媒体播放器，未随 Ubuntu 附带。Xine 用于观看 AVI、QuickTime、Ogg 和 MP3 文件（后者在 Ubuntu 中被禁用）。

## Adobe Flash

用于 Firefox 浏览器的 Adobe Flash 插件是一种商业多媒体应用程序，Ubuntu 默认并未提供，但许多人觉得它很有用。Adobe Flash 使你能够在支持它的网站上查看 Flash 内容。获取官方版 Flash 最简单的方法是使用 apt-get 或 Synaptic 安装 flashplugin-nonfree 软件包。一旦完成此操作，任何 Flash 动画都将在基于 Firefox 的浏览器中顺畅播放。

另一个有趣的视频查看器应用程序是 MPlayer（Ubuntu 未提供），它是一款 Linux 电影播放器。MPlayer 可以使用 Win32 编解码器，并且支持比 Xine 更广泛的视频格式，包括 DivX 和部分 RealMedia 文件。MPlayer 还使用一些支持 Matrox、3Dfx 和 Radeon 显卡的特殊显示驱动程序，并可以利用某些硬件 MPEG 解码板来获得更好的 MPEG 解码效果。请在 http://www.mplayerhq.hu 查找 Ubuntu 软件包；同时还提供 Win32 编解码器包以及其他编解码器包和 GUI 界面。

## 个人录像机

然而，将电视天线连接到计算机的最佳理由是将视频卡和计算机用作个人录像机。

商业个人录像机 TiVo 使用在 PowerPC 处理器上运行的 Linux 来录制电视节目，并具有多种自定义功能。TiVo 拥有巧妙的界面和出色的功能，包括录制/播放缓冲、定时录制与暂停、慢动作和倒放效果。Ubuntu 不提供任何试图在运行 Linux 的桌面 PC 上模拟 TiVo 功能的应用程序。然而，包括 DVR、Linux TV Project 和 OpenPVR 在内的几个此类应用程序列于 http://www.exploits.org/v4l/。这些项目仍在开发中，且不提供 .rpm 文件，因此你必须知道如何从 CVS 下载并编译自己的二进制文件。如果想要更简单一点，请查看 http://www.mythtv.org/ 上的 MythTV；应该有来自 ATRpms 的 Ubuntu .rpm 文件。
