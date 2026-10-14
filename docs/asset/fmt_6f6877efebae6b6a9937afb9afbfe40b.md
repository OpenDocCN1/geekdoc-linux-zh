
你可以使用 Xine 观看 MPEG 和 DVD 视频。Xine 是一种多功能且流行的播放器，Ubuntu 已包含。Xine 可用于 AVI、QuickTime、Ogg 和 MP3 文件（后者在 Ubuntu 中禁用）。

## Adobe Flash

Firefox 浏览器的 Flash 插件是 Ubuntu 未提供的商业应用，但许多人它很有用。Adobe Flash 允许观看支持它的网站内容。获取官方版本 Flash 的简单方法是使用 `apt` 或 `synaptic` 安装 `flashplugin-nonfree` 包。完成后，任何基于 Firefox 的浏览器都可以运行。

另一个有趣的视频查看程序是 MPlayer（未由 Ubuntu 提供），它是 Linux 的电影播放器。MPlayer 可以使用 Win32 解码器并支持比 Xine 更广泛的视频格式，包括 DivX 和 Realmedia 文件。MPlayer 还使用特殊的显示驱动程序，支持 Matrixx、3dfx 和 Radeon 卡，并可以使用某些硬件解码板进行更好的 MPEG 解码。Ubuntu 软件包请访问 http://www.mplayer.hu；还提供 Win32 解码器以及其他软件包和 GUI 界面。

## 个人视频录制机

然而，将电视天线连接到电脑的最佳理由是将视频卡和电脑作为个人视频录制机。

个人视频录制机 TiVo 使用运行在 PowerPC 处理器上的 Linux 来录制各种自定义电视节目。TiVo 拥有巧妙的界面和强大的功能，包括录制/播放缓冲、定时录制和暂停、慢动作和反向效果。Ubuntu 没有提供任何尝试在桌面 PC 上模拟 TiVo 功能的应用程序。

# 第 7 章 多媒体应用

Linux。然而，包括 The Linux TV 项目和 OpenPVR 在内的几个应用程序已列在 http://www.exploits/v4/。这些项目正在开发中，并不提供 .rpm 文件，因此您需要了解如何从 CVS 下载并编译您自己的二进制文件。如果想尝试更简单一点，可以查看 http://www.mytv.org/ 上的 MyTV；对于 Ubuntu TiVo，可以从 ATRpms 获取 .rpm 文件。

### Linux、TiVo 与 PVR

一些 TiVo 用户表示，使用这种基于 Linux 的设备改变了他们的生活。事实上，使用个人视频录制机（PVR）的便利性可以让频繁换台的频道漫游者生活变得简单得多。尽管 Ubuntu 未包含 PVR 应用程序，但源代码开发者正在为 Linux 开发更内核、更好更新的易于安装且易于使用的 PVR 软件。有关 TiVo 的更多信息（它需要支付月费并连接电话，或使用较新的 TiVo2 宽带连接），请访问 http://www.tivo.com/。想要拆解或升级 TiVo Hack 的不懈 DVR 黑客可以在 http://www.9htee.com/tiovupgrades.htm 找到，或在 http://www.tifofaq.com/ 读取 TiVo Hack。PVR 让电视变得有趣多了！

## DVD 与视频播放器

现在只要安装了适当的软件，就可以使用 Ubuntu 播放 DVD。（Ubuntu 本身不提供。）访问 http://www.videolan.org/，然后下载、构建并安装 vlc 客户端。

您必须拥有至少 450MHz 的 CPU 和工作的声卡才能使用 DVD 播放器。Ubuntu 默认内核支持 DVD CD-ROM 文件系统。如前所述，Xine 和 MPlayer 在播放文件方面表现出色。

> 注意
>
> http://www.videolan.org/get VideoLAN HOWTO 讨论了用于视频流传输的网络构建。虽然您可能不想创建一个网络，但关于该企业涉及的软件硬件的大量有用信息可以通用到其他地方，因此值得一看。该网站还包含一个关于在 Linux 上交叉编译以生成 Windows 二进制文件的 HOWTO 链接。

## 参考文献

- http://www.cdcopyworld.com/—关于 CD 介质和 CD 刻录机的技术信息资源。
- http://hardware.redhat.com/hcl/—支持的硬件数据库。
- http://www.opensource.com/download.cgi—商业 OSS 音频驱动测试版下载。
- http://www.xmms.org/—Xms 音频播放器首页。
- http://www.thekompony.com/projects/tkcogripper/—一个免费（但非 GPL）Ogg CD 刻录机。
- http://faceprint.org/code/—名为 mp32ogg 的 MP3 转 Ogg 转换器。
- http://www.ibiblio.org/pub/linux/sound/convert/!INDEX.html—多个音频转换工具的主页。
- http://www.linux-sound.org/—Linux 音乐和的优秀资源。
- http://www.cnpbagweb.com/audio/html—音频格式 FAQ。
- http://www.icecast.org/—流媒体音频服务器。
- http://www.linuxnetmag.com/en/issue4/m4icecast1.html—Iecast 教程。
- http://linuxselfhelp.com/HOWTO/MP3-HOWTO-7.html—MP3 HOWTO 包含许多音频应用程序的描述，并关注 MP3 格式，这些信息可以很容易通用于其他音乐格式。
- http://www.exploits.org/v4/—Linux 视频资源。
- http://www.fame.sourceforge.net/—视频编码工具。
- http://teletext.mb21.co.uk/faq.shtml—文字广播 FAQ。
- http://www.xine.source.org/—Xine DVD/视频播放器主页。
- http://www.MPlayerHQ.hu/homepage/—MPlayer 视频播放器主页。
- http://www.videolan.org/—一个拥有良好的 VideoLAN 项目。
- http://fy.chalmers.se/approto/linux/DVD+RW/—Linux 版 DVD+RW+/R[R[W]，一个在 Linux 下创建 DVD 的 HOWTO。
- http://www.gimp.org—GIMP（Gnu 图像处理程序）首页。
- http://f-sot.org—F-spot 项目首页。
- http://www.linuxformat.org—Linux Format 网站，由 Michael J Hammel 编写的长期 GIMP 教程主页。
- http://www.exif.org—关于 EXIF 及其在数码相机用途更多信息。
- http://www.sane-project.org—SANE（轻松访问扫描仪）项目首页。
- http://www.imagemagick.org—ImageMagick 首页。
- http://www.codeweavers.com—流行的 crossover 办公主页；如果您想尝试在 Linux 下运行 Photoshop，则需要它。
- http://gimp.net/tutorials/—GIMP 官方教程。

# 第 8 章

## 本章内容

### 在 Ubuntu 中打印

- Ubuntu 打印概览
- 配置和管理打印服务
- 创建和配置本地打印机
- 参考文献

从一开始，Ubuntu 就提供了对来自许多不同制造商的海量打印机的支持。本介绍了如何让您的打印机连接并与其通信。与大多数 Linux 发行版一样，连接后，Ubuntu 使用 CUPS（通用 Unix 打印系统）来处理打印机和打印任务。

通过 `/etc/init.d/cups` 命令可以控制 Ubuntu 下的 CUPS。

## 互联网打印协议

CUPS 支持互联网打印协议（称为 IPP），并提供了许多独特功能，如打印机浏览、对 PostScript 描述 `.pdf` 文件的支持。根据互联网工程任务组（IETF），IPP 源于 Novell 在 1996 年提出的创建打印协议的建议。从那时起，该系统已发展为平台平台引擎。

## Ubuntu 打印概览

> 注意
>
> Ubuntu 的打印系统是打印许多类型文档的主要引擎。其核心是系统配置工具 `system-configprinter`。打印系统可以打印到本地（连接）或远程（网络）打印机。如果您使用本地打印机，它由打印设备表示，例如 `/dev/lp0` 或 `/dev/lp1`。本地和远程打印机使用系统数据库 `printcap`。正在打印的文档被称为打印任务，您可以在调度目录 `/var/spool/cups` 中查看和控制任务列表。注意，您只能控制自己的打印任务。

要向系统添加打印机，请使用 `system-configprinter` 创建、配置并保存您的打印机定义。
