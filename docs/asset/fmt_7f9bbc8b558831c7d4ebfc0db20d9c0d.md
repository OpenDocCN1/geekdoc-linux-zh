
我们的 TV 卡就能完全工作了。每当我们重启时，所有正确的模块都会自动加载。Ubuntu 足够聪明，可以在安装期间检测并配置存在的支持的 TV 卡。

Linux 对 TV 卡的支持开发已在 Video4Linux 项目下整合。Video4Linux 软件为 Ubuntu 提供了视频捕获、无线电和文字电视的支持。

## 视频格式

Ubuntu 识别多种视频格式。然而，由 MPEG 组、Apple 和微软创建的格式占据主地位。视频格式的核心是编码器——视频和音频信息的编码器和解码器。这些编码器通常是专利的，但存在免费的编码器。是最常见的视频格式及其相关文件扩展名的列表：

- `.mpeg`—MPEG 视频格式；也称为 `.mpg`
- `.qt`—来自 Apple 的 QuickTime 视频格式
- `.mov`—另一种 QuickTime 视频格式
- `.avi`—Windows 视听格式

> 提示
Win32 编码器（在 Windows 下支持的编码器的通称）在 Ubuntu 中最初无法直接使用。相反，你需要进行一些“提示”来启用它们。获取编码器最简单的方法是下载 EasyUbuntu 脚本并使用它安装编码器（参见第 4 章）。

如果你需要将视频从一种格式转换为另一种格式，可以使用编码器应用程序。这些应用程序从摄像头或 TV 卡等视频设备获取原始视频数据，并将其转换为标准 MPEG 格式之一或静态图像格式（如 JPEG 或 GIF）。Ubuntu 不提供任何编码器应用程序（除了 ffmpeg 编码 MPEG-1 视频外），但你 可以在 http://www.freshfps.net/ 或另一个在线源找到它们（参见本章末尾的“参考”部分）。

# 在 Linux 中观看视频

由于前面提到的专利和许可问题，Ubuntu 删除了播放视频文件的功能。如果你从 synaptic 中的 universe 和 multiverse 存储库安装本节描述的应用程序完整版本，就可以恢复此功能。在那里将找到许多多媒体应用，如 Ogle、AlsPlayer、Gstreamer、Grip、Mplayer、VDMplayer、VideoLAN-client、Xms 和 Zapping。

你可以使用软件观看电视、从电视节目中保存单个图像（截图）、保存一系列快照以构建动画序列，或捕获视频、音频或两者。以下章节描述了你可以如何使用 Linux 多媒体软件来为你服务。

Ubuntu 提供了 notuat，作为 Konqueror 浏览器的嵌入式查看器。nuatat 被设置为视频文件格式的默认关联。在 Konqueror 中打开视频文件，如果支持，视频将会在查看器中显示。查看器提供了基本的 VCR 类功能：开始、停止和快进。

你可以使用 Xine 观看 MPEG 和 DVD 视频。Xine 是一种多功能且受欢迎的媒体播放器，Ubuntu 并不包含它。Xine 用于观看 AVI、QuickTime、OGG 和 MP3 文件。

## Macromedia Flash

Mozilla 浏览器的 Macromedia Flash 插件是一种商业多媒体应用，Ubuntu 不提供，但许多人发现它很有用。Macromedia Flash 使你能够查看支持它的网站上的 Flash 内容。可以使用 multiverse 存储库中的包 `flashplugin-nonfree` 获取 Mozilla 插件。这实际上是一个元包，将从 Macromedia 下载并安装真实的 Flashplayer。一旦安装，Firefox 中将启用所有的酷 Flash 动画。

另一个有趣的视频查看器应用程序是 MPlayer，一个 Linux 电影播放器。MPlayer 可以使用 Win32 编码器，并且支持比 Xine 更广泛的视频格式，以及 DivX 和 RealMedia 文件。MPlayer 还使用一些支持 Matrox、3DFx 和 Radeon 卡的特殊显示驱动，并可以使用某些硬件解码板以获得更好的 MPEG 解码效果。

> 注意
位于 http://videolan.org/ 上的 VideoLAN HOWTO 讨论了用于视频流传输的网络构建。虽然你可能不想这样做，但涉及该企业级软件和硬件的大量有用信息可以通用并应用到其他地方，因此值得一看。该网站还包含一个关于在 Linux 上进行交叉编译以生成 Windows 二进制文件的 HOWTO 链接。

## 启用 Java

某些多媒体内容依赖 Sun 的 Java 和 Java 浏览器插件。

让 Java 插件在 Mozilla 浏览器中正常工作曾是一场噩梦，但 Ubuntu 让这一切变得非常简单。你只需要在 synaptic 中启用 multiverse 存储库并搜索 `sun-j2re1.5` 软件包。一旦安装，它将在整个系统范围内启用 Java，节省了以前大量的工作！

## 相关的 Ubuntu Linux 命令

当你在 Ubuntu 上处理多媒体应用时，将将使用这些命令：

### CD/DVD 光盘
- `cddawav`—从 CD 复制 WAV 文件；供其他应用程序使用
- `cdabeligen`—为 CD 盒创建标签；用于脚本
- `cdp`—文本模式 CD 播放器
- `cdparanoia`—CD 提取器
- `cdrecord`—用于刻录 CD 的命令行工具
- `dvd+rw-tools`—创建 DVD 的命令行工具
- `grip`—CD 音乐刻录机
- `mkisofs`—创建 ISO 文件
- `xcdroast`—CD 刻录机

### 音频与音乐
- `alsamixer`—控制台音频混合器
- `kmid`—MIDI 播放器
- `mikmod`—MOD 音乐播放器
- `rhythmbox`—默认音乐播放器；它可以播放播放列表或网络电台节目
- `sox`—声音转换工具
- `sound-juicer`—CD 刻录工具
- `system-config-soundcard`—默认声卡配置程序
- `vorbis-tools`—OGG Vorbis 解码器
- `mms`—MP3 播放器

### 视频
- `kaboodle`—一个 KDE 媒体播放器
- `noatun`—KDE 媒体播放器
- `tvime`—电视查看器
- `xine`—视频播放器
- `mmms`—MPEG1/2/3 播放器

## 参考

http://www.cdcopoyworld.com/—关于 CD 介质和 CD 刻录机的技术信息资源。

http://www.opensound.com/download.cgi—商业 OSS 音频驱动版本下载。

http://www.xmms.org/—Xms 音频播放器主页。

http://www.thekomany.com/projects/tkcogripper—一个免费（但非 GPL）OGG CD 提取器。

http://faceprint.com/code/**—一个名为 mp32ogg 的 MP3 转 OGG 转换器。

http://www.ibbiblio.org/pub/linux/apps/sound/convert/INDEX.html—多个音频转换工具的首页。

http://linux-sound.org/—关于 Linux 音乐和声音的优秀资源。

http://www.cnpkgwell.com/audio.html—音频格式常见问题解答。

http://www.icecast.org—一个音频流媒体服务器。

http://www.linuxmag.com/en/issue4/micecast1.html—一个 Icecast 教程。

http://linuxhelp.com/HOWTO/MP3-HOWTO-7.html—MP3 HOWTO 包含许多音频应用的简要描述，它专注于 MP3 格式，这些信息很容易推广到其他格式。

http://www.exploits.org/v4/—Video for Linux 资源。

http://fame.sourceforge.net/—视频编码工具。

http://teletext.mb21.co.uk/faq.shtml—文字广播常见问题解答。

http://xine.sourceforge.net/—Xine DVD/视频播放器主页。

http://www.MPlayerHQ.uk/homepage/—MPlayer 视频播放器主页。

http://www.videolan.org/—一个拥有良好文档的视频项目。

http://fy.chalsmers.se/~appro/linux/DVD+RW/—Linux 下 DVD+RW+[R/-R][W]，一个在 Linux 下创建 DVD 的 HOWTO。

http://banshee-project.org/—Banshee 项目主页，一个使用 mono 开发的开源音乐刻录和播放应用。

![](img/757e95bd85c59465935194247625328c_266_0.png)

# 第 11 章

# 图形处理

## 本章内容

- 在 Ubuntu 中使用数码相机
- 在 Ubuntu 中使用扫描仪
- 参考

数字摄影的兴起催生了一批新的业余摄影师。随着数字暗房的发展，比任何时候最多的人将摄影视为自己的主要爱好之一。涌出了大量的软件，涵盖了从管理数字照片到修复常见照片问题，再到处理照片以改变其外观的方方面面。对于 Ubuntu 来说，幸运的是它可以使用许多允许用户处理数字图像的软件包。

在本章我们将主要关注数字图像，查看 Ubuntu 上可用的一些流行软件。我们将查看 GIMP，它是 Linux 平台最主要的照片和数字成像应用之一，还将查看其他可用的照片管理应用程序。最后，我们将查看 Ubuntu 中的扫描功能，用于那些你想要永远保存的照片。

## GIMP 图像处理程序

如前所述，GIMP 是主要的数字图像处理程序。它是一个强大且免费开源的工具，用户可以非常易地获取。它可以使用许多软件包，允许用户处理数字图像。

在本章中，我们将主要关注数字图像，查看 Ubuntu 上可用的一些流行软件。我们将查看 GIMP，它是 Linux 平台最主要的照片和数字成像应用之一，还将查看其他可用的照片管理应用程序。最后，我们将查看 Ubuntu 中的扫描功能，用于那些你想要永远保存的照片。

如前所述，GIMP 是主要的数字图像处理程序。它是一个强大且免费开源的工具，用户可以非常易地获取。它可以使用许多软件包，允许用户处理数字图像。

## 在 Ubuntu 中使用数码相机

大多数数码相机现在都是即插即用的，但也有例外。原本包含在 Linux 内核中以支持 Phillips 摄像头的 `pwc` 驱动已被撤回，这实际上切断了所有使用 Logitech 或 Phillips 摄像头的连接，尽管互联网上可能有第三方解决方案。

![](img/757e95bd85c59465935194247625328c_266_0.png)

## 咖啡机 (Coffee Pot Cam)

摄像头最有趣的用法之一是传奇的“互联网咖啡机”（始于 1991 年，但于 2001 年 8 月 22 日关闭——这将是载入臭名的一天）。摄像头对准咖啡机，系统管理员无需离开工位就能看到是否有新鲜咖啡。有些摄像头会拍摄不同城市交叉路口的快照。你可能会为你的摄像头找到类似的设备。

## 手持数码相机

数码相机是过去几年主要的成功案例之一。现在你可以拍照并立即看到照片预览。照片本身存储在光盘或内存卡上，可以轻松地插入 Ubuntu 并使用 GIMP 或软件进行进一步处理。遗憾的是，相机随附的大多数软件往往只适用于 Windows 用户，这使得你依赖于 Ubuntu 提供的软件包。

## 在 Ubuntu 上使用数码相机

幸运的是，得于 Ubuntu 和 GNOME 的良好开发，你现在可以通过 USB 接口将几乎任何相机连接到计算机，并且 Ubuntu 会自动将相机识别为 USB 大容量存储设备。你甚至可以设置 Ubuntu 在插入相机时进行识别，以便它自动为你导入照片。

要实现此操作，你需要设置可移动驱动器和媒体的设置。你可以在“系统”->“偏好设置”菜单中找到它。点击“相机”选项卡，并选择导入已连接数字照片的选项（见图 11.2）。

![](img/757e95bd85c59465935194247625328c_272_0.png)

图 11.2 通过设置让 GNOME 智能处理可移动媒体，自动导入照片。

现在当你将数码相机连接到计算机时，GNOME 会自动检测到（见图 11.3），并询问你是否要导入照片。

![](img/757e95bd85c59465935194247625328c_272_1.png)

图 11.3 GNOME 检测到数码相机的存在并询问是否导入照片。

默认情况下，GNOME 使用优秀的 gThumb 软件包（见图 11.4），该软件虽然看起来简单，但提供了易于使用的界面和强大的分类功能。

![](img/757e95bd85c59465935194247625328c_273_0.png)

图 11.4 利用 gThumb 管理你庞大的照片集。

## 使用 F-Spot

随着 Mono 在 Ubuntu 中的引入，Ubuntu 现在可以使用非常出色的 F-Spot 照片管理应用程序。然而，F-Spot 默认并不安装，因此你必须使用以下命令进行快速安装：
