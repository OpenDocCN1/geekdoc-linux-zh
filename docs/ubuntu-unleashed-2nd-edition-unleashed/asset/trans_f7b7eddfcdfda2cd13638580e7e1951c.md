
## 注意

在 http://videolan.org/ 上找到的 VideoLAN HOWTO 讨论了构建视频流媒体的网络。虽然你可能并不想这样做，但其中涉及的企业软硬件的大量有用信息可以推广到其他地方使用，因此值得一看。该网站还包含一个关于在 Linux 上进行交叉编译以生成 Windows 二进制文件的 HOWTO 链接。

## 启用 Java

某些多媒体内容依赖于 Sun 的 Java 和 Java 浏览器插件。
过去，让 Java 插件与 Mozilla 浏览器正确配合使用简直是一场噩梦，但 Ubuntu 让它变得非常容易。你只需在 synaptic（新立得）中启用 multiverse 软件源，然后搜索 `sun-j2re1.5` 软件包即可。安装后，这将在系统范围内启用 Java，省去以往大量的工作！

## 相关的 Ubuntu Linux 命令

在使用 Ubuntu 的多媒体应用程序时，你会用到以下命令：

## CD/DVD 光盘

- cdda2wav—从 CD 复制 WAV 文件；供其他应用程序使用
- cdlabelgen—为 CD 光盘盒创建标签；用于脚本中
- cdp—文本模式 CD 播放器
- cdparanoia—CD 抓轨工具
- cdrecord—录制 CD 的命令行工具
- dvd+rw-tools—创建 DVD 的命令行工具
- grip—CD 音乐抓轨工具
- mkisofs—创建 ISO 文件
- xcdroast—CD 刻录程序

## 声音和音乐

- alsamixer—控制台音频混音器
- kmid—MIDI 播放器
- mikmod—MOD 音乐播放器
- rhythmbox—默认音乐播放器；可播放播放列表或互联网电台
- sox—声音转换工具
- sound-juicer—CD 抓轨工具
- vorbis-tools—OGG Vorbis 编解码器
- xmms—MP3 播放器

## 视频

- kaboodle—KDE 媒体播放器
- noatun—KDE 媒体播放器
- tvtime—电视观看程序
- xine—视频播放器
- xmms—MPEG1/2/3 播放器

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
