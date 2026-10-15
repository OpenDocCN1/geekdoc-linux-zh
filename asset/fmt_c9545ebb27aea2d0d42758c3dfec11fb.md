
商业个人视频记录器 TiVo 使用运行在 PowerPC 处理器上的 Linux 来记录电视节目，并具有各种自定义功能。TiVo 具有巧妙的界面和精彩的功能，包括录制/回放缓冲、定时录制和暂停、慢动作和倒放效果。Ubuntu 未提供任何尝试在运行 Linux 的桌面 PC 上模仿 TiVo 功能的众多应用程序。然而，多个此类应用程序，包括 DVR、The Linux TV Project 和 OpenPVR，都列在 http://www.exploits.org/v4l/ 上。这些项目正在开发中，不提供 .rpm 文件，因此你需要知道如何从 CVS 下载并编译自己的二进制文件。想要更简单一点的，可以查看 MythTV，网址为 http://www.mythtv.org/；它可通过 multiverse 仓库获取。

## Linux、TiVo 和 PVRs

一些 TiVo 用户表示，使用这款基于 Linux 的设备改变了他们的生活。的确，使用个人视频记录器（PVR）带来的便利可以让习惯频道冲浪的人的生活变得轻松得多。虽然 PVR 应用程序未随 Ubuntu 一起提供，但开源开发者正在为 Linux 开发更新更好、易于安装和易于使用的 PVR 软件。有关 TiVo 的更多信息，TiVo 需要每月费用和电话线（或带宽连接的新 TiVo2），请浏览 http://www.tivo.com/。决心要对 TiVo 进行解剖或升级的 Linux 硬件黑客可以浏览 http://www.9thtee.com/tivougrades.htm 或阅读 TiVo Hack FAQ，网址为 http://www.tivofaq.com/hack/faq.html。PVR 让观看电视变得更有趣！

许多 Linux 网站致力于 PVR 软件开发。请浏览 DVR 项目页面 http://dvr.sourceforge.net/。

## DVD 和视频播放器

只要安装适当的软件，你现在就可以轻松使用 Ubuntu 播放 DVD。（Ubuntu 不提供。）浏览 http://www.videolan.org/，然后下载、构建并安装 `vlc` 客户端。

使用 DVD 播放器，你需要至少 450MHz 的 CPU 和一个正常工作的声卡。默认的 Ubuntu 内核支持 DVD CD-ROM 文件系统。如前所述，`Xine` 和 `MPlayer` 在播放 DVD 文件方面做得非常出色。

## 注意

在 http://videolan.org/ 上找到的 VideoLAN HOWTO 讨论了构建视频流媒体的网络。虽然你可能并不想这样做，但其中涉及的企业软硬件的大量有用信息可以推广到其他地方使用，因此值得一看。该网站还包含一个关于在 Linux 上进行交叉编译以生成 Windows 二进制文件的 HOWTO 链接。

## 启用 Java

某些多媒体内容依赖于 Sun 的 Java 和 Java 浏览器插件。

过去，让 Java 插件与 Mozilla 浏览器正确配合使用简直是一场噩梦，但 Ubuntu 让它变得非常容易。你只需在 `synaptic`（新立得）中启用 multiverse 软件源，然后搜索 `sun-j2re1.5` 软件包即可。安装后，这将在系统范围内启用 Java，省去以往大量的工作！

## 相关的 Ubuntu Linux 命令

在使用 Ubuntu 的多媒体应用程序时，你会用到以下命令：

## CD/DVD 光盘

- `cdda2wav`—从 CD 复制 WAV 文件；供其他应用程序使用
- `cdlabelgen`—为 CD 光盘盒创建标签；用于脚本中
- `cdp`—文本模式 CD 播放器
- `cdparanoia`—CD 抓轨工具
- `cdrecord`—录制 CD 的命令行工具
- `dvd+rw-tools`—创建 DVD 的命令行工具
- `grip`—CD 音乐抓轨工具
- `mkisofs`—创建 ISO 文件
- `xcdroast`—CD 刻录程序

## 声音和音乐

- `alsamixer`—控制台音频混音器
- `kmid`—MIDI 播放器
- `mikmod`—MOD 音乐播放器
- `rhythmbox`—默认音乐播放器；可播放播放列表或互联网电台
- `sox`—声音转换工具
- `sound-juicer`—CD 抓轨工具
- `vorbis-tools`—OGG Vorbis 编解码器
- `xmms`—MP3 播放器

## 视频

- `kaboodle`—KDE 媒体播放器
- `noatun`—KDE 媒体播放器
- `tvtime`—电视观看程序
- `xine`—视频播放器
- `xmms`—MPEG1/2/3 播放器

## 参考

http://www.cdcopyworld.com/ — 关于 CD 介质和 CD 刻录机技术信息的资源。
http://www.opensound.com/download.cgi — 商业 OSS 声卡驱动试用版下载。
http://www.xmms.org/ — Xmms 音频播放器主页。
http://www.thekompany.com/projects/tkcoggripper/ — 一个免费（但非 GPL）的 OGG CD 抓轨工具。
http://faceprint.com/code/ — 名为 mp32ogg 的 MP3 转 OGG 转换器。
http://www.ibiblio.org/pub/linux/apps/sound/convert/INDEX.html — 多个声音转换工具的所在地。
http://linux-sound.org/ — Linux 音乐和声音的绝佳资源。
http://www.cnpbagwell.com/audio.html — 音频格式常见问题解答（FAQ）。
http://www.icecast.org/ — 流媒体音频服务器。

## 第 11 章

## 图像处理

数码摄影的兴起催生了一类新的摄影爱好者。随着数字暗房的发展，现在比以往任何时候都有更多人将摄影列为主要爱好之一。大量软件应运而生，从管理数码照片、修复常见照片问题，一直到通过处理照片来改变其外观，应有尽有。幸运的是，Ubuntu 可以使用许多软件包，让用户能够处理数字图像。

在本章中，我们将主要关注数字图像，了解 Ubuntu 可用的一些流行软件。我们将介绍 GIMP——Linux 平台上主要的照片和数字图像处理应用程序之一，还会看看其他一些照片管理应用程序。最后，我们将介绍在 Ubuntu 中如何进行扫描，以保存那些你想永远留存的照片。

## GNU 图像处理程序

如前所述，GIMP 是 Ubuntu 随附的主要数字图像处理软件包。它的设计风格与 Adobe 广受欢迎的 Photoshop 应用程序非常相似，但也有一些例外（参见侧边栏“Photoshop 有哪些功能是 GIMP 中所没有的？”）

## 本章内容

- 在 Ubuntu 中使用数码相机
- 在 Ubuntu 中使用扫描仪
- 参考

GIMP？）。然而，它是免费的，并且可以访问一系列插件，这些插件旨在增强和扩展 GIMP 的功能。

GIMP 可以在应用程序、图形菜单下找到。

首次启动 GIMP 时，您会看到一个安装对话框，然后是一系列对话框，显示有关创建和本地 GIMP 目录内容的信息。该目录包含个人设置、首选项、外部应用程序资源文件、临时文件以及编辑器使用的外部软件工具的符号链接。

## Photoshop 有什么功能是 GIMP 没有的？

尽管 GIMP 功能强大，但它确实缺少 Adobe Photoshop 提供的两个对一些图形专业人士很重要的功能。

其中第一个是为商业印刷机生成彩色分离的功能（CMYK 代表青色、品红色、黄色和键色 [或黑色]）。GIMP 使用 RGB（红、绿、蓝），这对于网页显示来说很棒，但对于印刷机来说就不太理想。GIMP 缺少的第二个功能是使用 Pantone 颜色（一种专利色彩规范）以确保准确的色彩匹配。

如果这些功能对您不重要，GIMP 就是一个出色的工具。如果您必须使用 Adobe Photoshop，CodeWeavers 的 CrossOver Office 当前版本可以在 Linux 中运行 Photoshop。

尽管这些功能已期盼了相当长一段时间，但它们在近期内出现在 GIMP 中的迹象并不明显。

初始配置完成后，GIMP 的主窗口和工具箱就会出现。GIMP 的主窗口包含用于选择、绘制、移动、放大或缩小视图、喷枪、绘画、涂抹、复制、填充和选择颜色的工具。根据您系统上安装的版本，工具箱可以容纳超过 25 种不同的工具。

工具箱的 File、Xtns 和 Help 菜单分别用于文件操作（包括通过电子邮件发送当前图像的功能）、图像获取或处理以及文档。如果您在打开的图像窗口上右键单击，您将看到 GIMP 菜单的丰富内容，如图 11.1 所示。

![](img/e464b828c497c99e41f61d4c55f1c0db_260_0.png)

**FIGURE 11.1** Right-click on an image window to access the GIMP’s cascading menus.

## 使用 Ubuntu 配合数码相机
