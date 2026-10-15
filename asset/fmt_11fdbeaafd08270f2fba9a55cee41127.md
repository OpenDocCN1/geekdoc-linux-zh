
有关配置声卡的更多信息，请将浏览器指向 CD 上的 `/Doc/Sound-HOWTO.html` 以查看 Sound-HOWTO 文档。

测试声卡是否正常最简单的方法是播放一张音乐 CD。KDE 和 Gnome（以及许多其他 Linux 窗口管理器）都包含至少基本的 CD 播放程序。

在 KDE 和 Gnome 中，你都可以从多媒体（Multimedia）菜单中选择 CD 播放器（CD Player）。这里显示了 KDE 窗口。

![](img/ba933c244f3be8993f8191427d25c74c_150_0.png)

当然，如果你没有听到任何声音，可能其他几个地方出了问题。如果你使用双启动系统且声音在 Windows 中工作正常，请尝试使用不同的内核模块或参数，并阅读 Sound-HOWTO 文档。如果 Windows 中的声音也无法工作，在调整 Linux 命令之前请检查以下项：

- 声卡是否牢固地安装在系统主板的插槽中？
- 声器是否插入了声卡上正确的接口（而不是麦克风接口）？
- 声器是否连接了电源（许多声器需要交流电源适配器或电池）？
- 声器是否开启？

![](img/ba933c244f3be8993f8191427d25c74c_150_1.png)

## 让你的系统变得趣味性

- 你的系统中是否有多个设备（扫描仪、音频混音器、声卡等）可能在使用冲突的 IRQ 中断号？

## 尝试 OpenSoundSystem

如果你真的对在 Linux 上使用音频功能感兴趣，可以考虑尝试 OpenSoundSystem。这是一个用于 Linux 的商业音频驱动程序包，包含一个易于使用的基于菜单的配置实用程序并支持许多不同的音频设备。

你可以从 4Front Technologies 网站 `http://www.opensound.com` 下载该产品的评估版本。在输入一些个人信息后，下载是免费的。该项目非常支持 Linux——会发布适用于 Linux 的新驱动程序。该公司还赞助了 `xmms` 项目，该项目在第 29 节“创建一个基于 Linux 的音乐工作室”中有所描述。

## 让 Linux 成为你的个人视频播放器

网络上有成千上万的视频片段，从电影预告和宣传片到个人创建的视频。Linux 有几种实用程序让你可以在屏幕上查看这些视频片段。

在 Linux 上播放视频的核心是 XAnim 程序。该程序运行在任何使用窗口系统的 Linux 版本上。它支持以下视频格式，其中 MPEG 是目前基于 Web 的视频片段最流行的格式：

- MPEG 视频
- Quicktime 动画（MOV 文件）
- AVI 动画
- FLI 和 FLC 动画
- IFF 动画
- GIF89a 动画
- DL 动画（格式 1、2 以及它们的大部分）
- Amiga MovieSetter 动画
- Utah Raster Toolkit RLE 图像和动画
- SGI Movie 格式文件

注意 XAnim 不支持 RealAudio 和 RealVideo 格式。这些流格式是专有的。请访问 `http://www.real.com` 了解这些播放器的详情并下载免费的 Linux 版本。

XAnim 包含在大多数 Linux 发行版中，例如 Red Hat 6、Suse 6.1 和 Calder OpenLinux 2.2。如果你正在运行这些发行版之一，请尝试在图形桌面的任何命令行中运行 `xanim`：

```
xanim hurricane.mpg
```

`hurricane.mpg` 电影包含在 CD 的 `/Source/Video` 目录下。它来自 NASA 网站；你可以在 `http://www.nasa.gov/gallery/index.html` 查看他们的整个多媒体画廊。图 27.1 显示了 XAnim 播放 MPEG 文件。XAnim 包含了用于控制和图像的独立窗口。

### XAnim 包含了控制和视频播放的独立窗口。

![](img/ba933c244f3be8993f8191427d25c74c_152_0.png)

## 让你的系统变得趣味性

XAnim 的控制包括播放、暂停、快进、倒退和音量控制（然而，许多 MPEG 文件不包含声音）。

如果 XAnim 没有作为你的 Linux 发行版的一部分安装，你可能从你的 Linux CD 安装它。XAnim 也包含在本书的 CD 的 `/Source/Video` 中。

由于 XAnim 支持许多视频文件格式并且在 Linux 上免费提供，它已被作为流行的 Linux 桌面其他视频播放器的基础。

GXAnim 程序围绕 Gnome 桌面和 `GTK+` 库构建。它依赖 `xanim` 作为引擎来显示视频文件。

GXAnim 与 XAnim 类似，但具有更吸引人的界面，旨在与你的 Gnome 桌面融合。它包含一个控制面板和一个显示视频的独立窗口，所示。

![](img/ba933c244f3be8993f8191427d25c74c_153_0.png) 偏好设置对话框让你设置 GXAnim 的选项，所示。

![](img/ba933c244f3be8993f8191427d25c74c_153_1.png) `gxanim` 的 rpm 归包位于 CD 上的 `/Binaries/Video`。你可以使用以下命令安装 `gxanim`：

```
rpm -Uvh /mnt/cdrom/Binaries/gxanim-0_35-1_386
```

对于 KDE 有类似的包。像 GXAnim 一样，Aktion 依赖 `Xanim` 作为引擎。Aktion 有一个包含控制和视频播放的窗口，所示。

![](img/ba933c244f3be8993f8191427d25c74c_154_0.png) Aktion 的源码包位于 CD 上的 `/Source/Video`；Red Hat 的预编译二进制文件位于 `/Binaries/Video`。Aktion 包括：

- 全屏模式
- 一个可以添加到其他 KDE 程序中的视频小部件（`KXanim`）
- 帧捕捉（在视频播放期间按 C 将当前帧保存到文件）

多种语言的文档（如果你需要爱沙尼亚语的话）
如果你的系统中没有 KDE 或 Gnome，请尝试位于 CD 上 `/Source/Video` 或 `/Binaries/Video` 的 MPEGTV。要安装 MPEGTV 包，你需要先安装 `Xforms` 包。使用这些命令开始（注意第二个命令中的 `nodepops`）：

```
rpm -Uvh /mnt/cdrom/Binaries/Extras/xforms-0_88-1_386
rpm -Uvh -nodepops /mnt/cdrom/Binaries/Video/mtv-1_0_9_386
```

该程序在任何图形 Linux 系统上播放 MPEG 视频片段；MpegTV 的控制所示。

![](img/ba933c244f3be8993f8191427d25c74c_155_0.png)

## 使用 Linux 收听广播或电视

PC 有多种类型的扩展卡提供广播或电视调谐器并将信号输出到 PC。许多程序可以在 Linux 中利用这些卡。

这些程序都依赖于近期 Linux 内核的一个功能，称为 Video4Linux。此功能允许 Linux 捕捉来自电视调谐卡等视频设备的输入数据。Video4-Linux 项目的主页是 `http://runner.swansea.uk.linux/v41.html`。

这是一个 KDE 应用，让你在 KTV “工作”时看电视。该程序包含一个独立的视图，并带有对话框来控制各种项目（见图 28.1 和 28.2），包括：

- 扫描电视调谐器以查找可用电台并编程
- 从独立的对话框列表选择电台
- 使用混音器调整音频质量
- 设置视频图像大小和输入源
- 使用与你的 Linux PC 交互的程序编程红外遥控器控制选定的频道

## 使用 LINUX 收听广播或看电视

图 28.1 KwinTV 可以扫描调谐器输入以查找可用电台和节目。

![](img/ba933c244f3be8993f8191427d25c74c_156_0.png)

图 28.2 KwinTV 维护频道列表，并包含混音器和视频流传输对话框。

![](img/ba933c244f3be8993f8191427d25c74c_156_1.png)

KwinTV 以源码包的形式位于 CD 的 `/Source/Video`，并以二进制包的形式位于 CD 的 `/Binaries/Video`。

除了电视调谐器卡外，还有提供无线电信号（如 FM 波段）的显卡。`gtuner` 程序让您通过类似于本文部分之前描述的 CD 播放器的接口来收听广播。

`gtuner` 的源码包位于 CD 的 `/Source/Audio`。`/Binaries/Audio` 包含一个二进制文件（不是完整的 rpm，只是可执行文件）。Guner 用于 Gnome 桌面。该界面

![](img/ba933c244f3be8993f8191427d25c74c_156_2.png)

## 让你的系统变得有趣

`gtuner` 的界面类似于汽车音响，如下所示。您可以选择电台的波段、频率和音量。

![](img/ba933c244f3be8993f8191427d25c74c_157_0.png)

如果您愿意，可以使用滑块选择电台，并在听的同时通过图形化方式观察音乐，如下。

![](img/ba933c244f3be8993f8191427d25c74c_157_1.png)

Gtuner 包含全套配置框，您可以在其中设置功能，如：

- 睡眠定时和唤醒闹钟
- 退出时静音
- 电台列表（内存）
- 支持多块无线电卡
- 用于扩展的插件接口

Linux 的最后一个广播相关程序是 `icecast`。Icecast 是一个 MPEG3 音频（`mp3` 文件）流媒体服务器。使用 `icecast`，可以将您的计算机（作为服务器）广播音频文件到网络上的任何其他系统（如果有足够的带宽，也可以是互联网）供他人收听。实际上，您可以通过使用 `icecast` 服务器提供流音频信号来成为一名数字 DJ。

`icecast` 项目是开源的，主页位于 `http://icecast.org/`。该页面包含了网络广播列表。您可以访问其中一个页面并收听互联网上 `icecast` 服务器提供的音乐（见图 28.3）。

图 28.3 互联网上的许多音频服务器使用 `icecast` 流媒体服务器提供音乐。

![](img/ba933c244f3be8993f8191427d25c74c_158_0.png)

`icecast` 服务器的源代码位于 CD 的 `/Source/Audio`。

## 创建基于 Linux 的音乐工作室

Linux 拥有几十种出色的音频工具。这些工具始于许多 CD 播放器，其中一些可以在任何图形环境下运行。其他程序可以播放您从互联网下载的热门格式音频文件。合成器、音频编辑器和混音器也可用。其他工具可以转换格式或帮助您创作音乐。

![](img/ba933c244f3be8993f8191427d25c74c_158_1.png)

## 在 Linux 上播放音频文件

音频 CD 在 Linux 上已经存在多年，而且似乎随着时间的推移变得越来越。除了 KDE 和 Gnome 自带的默认播放器外，其他 CD 播放器让可以在任何图形环境下工作的同时享受音频。

Linux 的两个 CD 播放器是 `xmcd` 和 `xfreed`，它们都位于 CD 的 `/Source/Audio`。`/Binaries/Audio` 还包含一个 `xfreed` 的 rpm 二进制包（`xfreed` 的二进制文件默认安装在 `/usr/local/bin` 中）。

但 CD 不是收集数字音乐的唯一方法。像 `www.mp3` 这样的许多网站提供样本曲目，或让您创建并下载个性化的收藏。这些内容大部分可能是 MPEG3 音频（`.mp3` 文件）。Linux 支持这些以及许多其他音频格式，包括：

- MPEG3 (`.mp3` 文件)
- WAV
- au 文件
- MIDI (`.mid` 文件)

数字音乐中需要了解的一个重要区别是，MIDI 格式是对音乐属性的描述，而 WAV 和 MPEG 格式是数字记录（压缩的）。解释这些格式差异的另一种方法是，MIDI 类似于 Postscript，而 WAV 和 MPEG 类似于 PCX 位图图像。

了解这些格式之间的区别很重要，因为 MIDI 播放器（如 KDE 自带的）必须能够解释 MIDI 文件中描述的“乐器”以创建声波，而播放其他格式则需要（广义上）将音频数据转储到声卡。不同的实用程序处理各种音频格式时可能有截然不同的能力。

如果您想在不进入 X 环境的情况下播放您的 MPEG3 音频文件之一，可以使用 `mpg123` 命令行程序在您工作时在后台播放文件：

```
