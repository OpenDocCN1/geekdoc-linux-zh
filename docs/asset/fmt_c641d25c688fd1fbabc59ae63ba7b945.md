
查看以下网站，可以了解在 Linux 中受支持和不受支持的 Webcam 的更完整列表。但请记住，这些 Webcam 中并非所有驱动程序都能在 Fedora 或 RHEL 的最新内核中正常工作。
- Kamerstòi Linux (www.cs.umu.se/~e00ahs/exjobb/linuxcams.html)
- Linux USB 设备驱动程序 (www.linux-usb.org/devices.html)

我在本章示例中使用的 Logitech QuickCam Pro 3000 Webcam 与 Fedora 7 附带的 `pwc` 驱动程序配合工作良好。为了确认其正常工作，我运行了 `lsmod` 命令，查看 `pwc` 驱动程序是否已加载并与 `videodev` 模块关联：
```bash
# lsmod
pwc                     43392 0
compat_ioctl32          5569 1 pwc
videodev                5120 1 pwc
```
要查看关于 `pwc` 模块（特定于此 Webcam）的信息，我输入了以下 `modinfo` 命令：
```bash
# modinfo -p pwc
size:Initial image size. One of sqcif, qgif, qcif, sif, cif, vga
fps:Initial frames per second. Varies with model, useful range 5-30
fbufs:Number of internal frame buffers to reserve
mbufs:Number of external (mmap(1ed) image buffers
trace:For debugging purposes
power_save:Turn power save feature in camera on or off
compression:Preferred compression quality. Range 0 (uncompressed) to 3 (high compression)
leds:LED on,off time in milliseconds
dev_hint:Device node hints
```

### 运行 Ekiga

要启动 Ekiga，请选择 Applications -> Internet -> IP Telephone, VOIP and Video Conferencing。要从终端窗口启动 Ekiga，请输入 `ekiga &`。如果未安装，您可以从随本书附带的 DVD 中安装 `ekiga` 包。首次运行 Ekiga 时，Ekiga 配置向导将启动。该向导允许您输入以下信息：
- **个人资料** — 您的名、姓、电子邮件地址、备注和位置。您还可以选择是否希望在 Ekiga ILS 目录中列出您的信息。
- **连接类型** — 指示您的互联网连接速度（56K 调制解调器、ISDN、DSL/电缆、T1/LAN 或自定义）。
- **音频管理器** — 通常您会选择 ALSA 作为您的音频管理器。
- **视频管理器和设备** — 通常您会选择 Video4Linux 作为视频管理器，并选择您的 Webcam 作为输入设备。

> **注意：** 如果您以后想重新配置 Ekiga，请运行以下命令以清除旧设置：`ekiga-config-tool --clean`。在运行该配置工具之前，请确保所有 Ekiga 实例都已停止。再次运行 `ekiga` 以重新输入您的设置。

图 8-11 显示了带有右侧历史记录日志的 Ekiga 窗口。

![](img/fb202c163797a743c3c6cf236316bc96_385_0.png)

在打开的 Ekiga 窗口中，您可以点击名片图标打开地址簿。从地址簿中选择 Ekiga 白页。通过在搜索过滤器中输入姓名，您可以按名、姓、电子邮件地址或位置搜索可能连接到 Ekiga 服务器的人。从出现的列表中选择一个联系人，如果对方接受您的呼叫，您就可以开始视频会议。

通过选择 View → Control Panel（视图 → 控制面板），您可以选择在视频窗口下方显示标签页，以调整您的音频水平和视频外观。历史标签页显示您的活动日志。

## 播放视频

视频录制（编码）和播放（解码）仍然是开源软件中最具争议且潜在诉讼最多的领域。一方面，拥有复杂视频格式专利持有者可能会对开源编解码器收取专利费（即使软件是从头编写的）。另一方面，电影行业则针对发布他们曾希望保密的加密技术（DeCSS）的人发起攻击，以防止商业电影的开源解码。问题在于，允许您在 Linux 中播放电影的同一技术也可用于复制和分享它们。

> 注意：Codec 是 COder/DECoder（编码器/解码器）或 COmpressor/DECompressor（压缩器/解压缩器）的缩写，具体取决于您询问的对象。无论哪种情况，编解码器都是使计算机能够处理和编码音频和视频的关键。

与音频录制一样，如果您是从头开始，有一个名为 Theora（www.theora.org）的开源编解码器，截至本书撰写之时，您可以使用它而无需支付任何专利费。只要您拥有您录制的版权所有，您就可以自由分发该内容，并允许他人播放它。

关于包含视频编解码器（除免费的 Theora 外），Red Hat, Inc. 采取了谨慎的态度。虽然 Fedora 和 RHEL 现在包含诸如 Totem 之类的视频播放器（在本章后面会有描述），它们不包含那些通常与存在争议的编解码器一起打包的播放器（例如 MPlayer 和 Xine 媒体播放器）。如果你想在 Red Hat Linux 系统中播放商业电影、流行视频片段或其他视频内容，你必须从其他地方获取这些编解码器。

本节描述了在 Linux 中播放和创建视频所涉及的一些问题。它还介绍了随 Fedora 和 RHEL 附带的视频播放器，以及你可以获取用来播放各种视频内容的其他播放器。

## 审视影响视频和 Linux 的法律

我需要首先提醒每个人，我并不是律师，因此对于你安装在计算机上的任何软件，你需要自行承担责任。然而，在 Linux 中播放开源软件的视频内容方面，出现了一些主题：
- **专利编解码器的授权费可能需要支付。** 虽然许多视频编解码器受专利保护，但一些专利持有人对个人使用不收费。但是，你应该检查拥有你计划使用的编解码器专利的公司当前的政策，因为使用条款在不断变化。例如，曾经在 DivX 网站上发布的以下声明已不再存在：“DivX 视频软件的个人使用是免费的。商业使用不是免费的，需要您从 DivXNetworks 获取商业使用许可证。”（有关 DivX 授权的信息，请参阅 DivX 网站 www.divx.com。）

由于 MPEG-2 和 MPEG-4 视频格式受多种专利保护，专利持有人团体已联合起来，对相关编码器和解码器收取授权费。这些努力并非由主导创建这些格式的标准组织赞助，可能也不涵盖你付费软件相关的所有专利持有人。有关 MPEG 专利问题的详情，请参阅 MPEG 行业论坛（www.m4if.org/patents）。

请记住，现在已有多种方式可以为许多流行的音频/视频格式购买编解码器，以便在 Linux 中使用。有关从 Fluendo 购买编解码器的信息，请参阅“扩展编解码器的自由度”一节。
- **未经授权复制受版权保护的材料从未合法。** 即使是合法的视频编解码器，也不能使复制商业电影和其他受保护内容并将其分发给他人变得合法。关于是否合法制作 DVD 电影的私人备份副本（在计算机软件中这是一种普遍接受的合法做法）存在疑问。但是，未经所有者许可，重新分发电影、音乐或其他媒体内容是不合法的。

由于专利化消除了专利（或已公开的专利申请）中披露的主题的贸易秘密保护，许多人提出了一个问题：为什么不能自由分发 libdvcss（基于 DeCSS 解密）来播放 DVD 电影。由于 CSS 没有版权或专利保护，分发 libdvcss 不应是非法的，也没有任何人需要为使用它支付许可费。关于 libdvdcss，在美国出现了另一个问题：《数字千年版权法》（DMCA）。DMCA 可能使 DeCSS 非法，因为该技术被用于破解加密方案以规避受版权保护的材料。

至于软件专利问题，除了与多媒体内容相关的问题外，这些正在多个方面进行抗争。如前所述，许多开源倡导者认为，软件应该受版权保护而不是专利保护（参见本章前面的“理解 Linux 中的多媒体和法律问题”一节）。

综上所述，本章接下来的部分将继续描述在 Linux 中可用于播放广泛视频内容的播放器。至于哪些编解码器可以免费供你使用以及如何使用，需要你自行弄清楚这个迷宫。

## 理解视频内容类型

在深入介绍视频播放器之前，我想尝试澄清一些关于视频文件格式和编解码器的混淆：
