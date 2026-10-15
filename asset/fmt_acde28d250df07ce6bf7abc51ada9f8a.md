
*(由于原始文本后半部分高度重复且无意义，我将为您提供前两个核心章节的专业翻译：)*

## 第二部分：使用 Fedora RHEL

- Linux 摄像头 (http://302found.com/linux_webcams/)

我在本章示例中使用的 QuickCam Pro 300 摄像头与 Fedora 自带的 `pwc` 驱动配合良好。为了检查其运行状态，我运行了 `lsmod` 命令，看到 `pwc` 驱动已加载并与 `video4` 模块关联：

```
# lsmod
pwc 43392 0
compat_ioctl132 5569 1 pwc
video4 5120 1 pwc
```

要查看 `pwc` 模块的信息（该摄像头专用），我输入了以下 `modinfo` 命令：

```
# modinfo:Device nodes hints
dev_hint:LED on,off time in milliseconds
compression:Preferred compression quality. Range 0（未压缩） to 3 
（高压缩率）
power_save:Turn power save feature in camera on or off
trace:For debugging purposes
mbuffers:Number of external (mmmap)ed image buffers
buffers:Number of internal buffers to reserve

fps:Initial frames per second. Varies with model, useful range 5-30
size:Initial size. One of sqcif, qscif, qcif, sif, cif, vga
```

### 运行 Ekiga

启动 Ekiga，选择 应用程序 (Applications) -> IP 电话、VOIP 和视频会议 (Video Conferencing)。要从终端启动 Ekiga，输入 `ekiga &`。如果没有安装，你可以从书中附带的 DVD 安装 Ekiga 软件包。第一次运行 Ekiga 时，会启动 Ekiga 配置助手。该助手允许你输入以下信息：

- 个人数据 - 你的名字、姓氏、电子邮件地址、连接方式和位置。你还可以选择是否加入 Ekiga ILS 目录。
- 连接类型 - 指明你的互联网连接速度（56k 调制解器、ISDN、DSL/电缆、T1/LAN 或自定义）。
- 音频管理器 - 通常，你会选择 ALSA 作为你的音频管理器。
- 视频管理器和设备 — 通常，你会选择 Video4Linux 作为视频管理器，并将你的摄像头作为输入设备。

> 注意：如果你以后想重新配置 Ekiga，请运行以下命令清理设置：`ekiga-config-tool --clean`。在运行此配置工具之前，确保所有的 Ekiga 实例都已停止。此外，确保关闭停止 Ekiga 后可能仍在运行的面板应用程序。再次运行 `ekiga` 以重新进入设置。

### 第 8 章：Linux 中的音乐、视频和图像 343

图 8-10 显示了 Ekiga 窗口，右侧有历史日志。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_390_0.png)

图 8-10：连接到 ILS 服务器使用 Ekiga 进行视频会议。

在打开的 Ekiga 窗口中，你可以点击通讯录（rolodex）打开地址录。从地址录中选择 Ekiga 白页 (White Pages)。通过在搜索过滤器中输入名称，你可以根据名、姓、电子邮件地址或位置搜索可能连接 Ekiga 服务器的人员。从出现的列表中选择一个人，如果他接受了你的通话，就可以开始视频会议。历史 (History) 标签显示了你所有的活动。

### 使用 Cheese 拍摄摄像头视频和快照

Fedora 有一个新的 GNOME 桌面应用程序，用于从摄像头拍摄快照和视频。使用支持的摄像头（前文描述），你可以使用新的 Cheese 应用程序 (http://www.gnome.org/projects/cheese) 通过几次鼠标点击从摄像头捕获图像。

要安装 Cheese，请在终端以 root 用户身份输入以下命令：

```
# yum install cheese
```

然后，使用你的摄像头，以 root 用户身份从终端输入以下内容……（注：原文此处开始出现严重重复，翻译已停止以保证质量）。

## 第二部分：使用 Fedora RHEL

- 未经授权复制受版权保护的材料绝是非合法的。即使是合法的视频解码也不意味着复制商业电影和其他受保护的内容并分发给他人是合法的。例如，制作 DVD 的备份副本（这是计算机软件中广泛接受的法律做法）是否合法尚存在疑问。没有所有者的许可，对电影、音乐或其他媒体内容的任何重新分发都是非法的。

由于专利化消除了专利中所披露的（或已公布的专利申请）主题的秘密保护，许多人提出了一个问题：为什么人们不能自由地 `libdvdcss`（基于 DeCSS 解密）来播放 DVD 电影。在 CSS 没有版权或专利保护的情况下，分发 `libdvdcss` 应该不是非法的，而且没有人需要为使用它支付许可费。在《数字千年版权法案》（DMCA）中，DMCA 可能会让 DeCSS 变得非法，因为该技术被用于破解加密方案以规避版权保护的内容。

至于软件问题，人们在与多媒体内容相关的多个战线上进行了斗争。如前所述，许多开源支持者之间的争论在于，软件应该受版权保护而非专利保护（参见本章前面的“理解 Linux 中的多媒体和法律问题”部分）。

综上所述，本章的后续部分将继续描述 Linux 中哪些播放器可以播放广泛的视频内容。这取决于你如何理清哪些解码器是你可以免费使用的，以及以何种方式使用。

## 理解视频内容类型

在介绍视频播放器之前，我想尝试消除一些关于视频文件和格式的困惑：

- 视频文件格式——视频文件本质上描述了用于组合音频和视频内容的视频文件结构。该结构还可以定义字幕以及音频和视频如何同步。然而，可能已经使用了多种视频和音频解码器来编码内容。因此，仅仅因为你可以播放一个标记为 MPEG (`.mpg`)、Audio Video Interleaved (`.avi`)、QuickTime (`.mov`)、RealMedia (`.rm`)、Windows media (`.wmv`)、Advanced Streaming Format (`.asf`) 或其他文件的视频，并不意味着你可以播放所有标记为这些格式的视频文件。
- 视频和音频解码器——解码器用于编码和解码视频音频内容。完全使用免费软件编码的视频可能使用 Theta 编码视频，并使用 Ogg Vorbis 编码音频。流行的视频解码器包括 MPEG-4、DivX、Xvid、RealVideo 和 MJPEG。

并不是所有的视频解码器和文件格式都适用于流媒体传输。例如，AVI 和 MPEG-2 不支持流。然而，RealMedia、MPEG-4 和 ASF 格式可以流传输，这减轻了服务器的负载，意味着你不需要下载整个视频即可开始观看。查看后续章节中视频播放器的描述，获取有关哪些播放器支持哪些器的信息。

如果你硬盘上有一个视频播放器，并想知道它包含什么类型的内容，可以使用 `file` 命令。这里有一个检查电影预告片内容的 `file` 命令示例：

```
$ file movie.avi
movie.avi: RIFF (little-endian) data, AVI 640 x 272, 23.98 fps, video: DivX 3, audio: MPEG-1 Layer 3 (stereo, 44100 Hz)
```

此示例显示文件包含 DivX 3 视频和 MPEG-1 Layer 3 音频。视频大小为 640 x 272 像素。视频以每秒 23.98 帧的速度捕获。这可以帮助你找到需要播放的视频类型。在安装了正确解码器的情况下，MPlayer、Xine、VLC 或其他播放器都能播放此内容。

## 将视频转换为 Theora

目前还没有很多工具可以创建 Theora。为了获得视频进行尝试，我用我的 Sony Handycam 拍摄了一段视频，它将视频存储在 30 分、1.4GB 的 DVD 中。我下载了一个 Theora.org 网站推荐的工具，名为 `ffmpegtheora`。我的摄像机录制的 VOB 格式的家庭电影，我将其复制到硬盘并转换为 Theora/Ogg Vorbis，如下所示：
