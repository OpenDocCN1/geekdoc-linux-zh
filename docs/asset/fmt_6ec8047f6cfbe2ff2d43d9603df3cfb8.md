
- **OmniVision 摄像头** (`ov551` 驱动) — 此驱动支持来自 OmniVision 摄像头芯片的 USB 摄像头（www.ov.com/app2_table.asp?id=4）。摄像头包括 Creative WebCam 3、MediaForte MV300、AVERMedia 摄像头以及 D-Link DSC-B300。
- **Philips USB 摄像头** (`pwc` 驱动) — 此驱动支持多种 Philips USB 摄像头，包括 PCA645、PCA646、PCVC675、PCVC680、PCVC690、PCVC730、PCVC740 和 Askey VC010。这还了一些廉价的罗技摄像头，包括 QuickCam Pro 3000。
- **Endpoints 摄像头** (`se401` 驱动) — 支持包含 Endpoints SE401 组的摄像头。参见 Kensington VideoCam 摄像头（67014, 67015, 67016 和 67017）以及 Aox se401 摄像头（se401）。
- **SONIC PC 摄像头** (`sn9c102` 驱动) — 此驱动支持基于 SONIC PC 摄像头控制器的 USB 摄像头。包括 X300、X-Eye 和 Chicony Twinkle 摄像头。`sn9c102` 驱动由 Linux Projects（www.linux-projects.org）维护。
- **STMicroelectronics 芯片** (`stv0680`) — 此驱动支持包含 STMicroelectronics（www.st.com）USB 版本 STV0680 芯片的摄像头。摄像头包括 AIPtec Peninsula 和 Nissan Quickpix2（厂商/产品 ID 05533/020）。有关该驱动的信息，请参考 Linux STV0680-usb 页面页面（http://stv0680-usb.sourceforge.net）。
- **Ultracram 摄像头** (`ultracam` 驱动) — 支持如 IBM UltraPort Camera II 等摄像头。有关驱动的信息，请查看 ultracam 驱动页面（www.gutwin.org/cam/source）。
- **Vicam 摄像头** (`vicam` 驱动) — 此驱动支持 3Com HomeConnect USB 摄像头。更多信息请参考该驱动的项目（http://homeus.sourceforge.net）。
- **Winbond 摄像头** (`w9968cf` 驱动) — 支持来自 Winbond Electronics 的 W9668cf USB 双模式摄像头芯片。使用该芯片的摄像头包括 ADG-5000 Aroma Digi Pen、Zonics EZ-802 EZMeCam 和 Pretec DigiPen-480。更多信息请参考 Linux Projects 网站（www.linux-projects.org）。

查看以下网站以获取更完整的支持和不支持 Linux 的摄像头列表。请注意，这些设备的所有驱动并不都能在 Fedora 或 RHEL 的最新内核中运行。
- Linux 下的摄像头支持 (www.cs.um.se/~c00ahs/exjobb/linuxcams.html)
- Linux USB 设备驱动 (www.linux-usb.org/devices.html)

# 第 8 章：Linux 中的音乐、视频和图像 349

我在本章示例中使用的罗技 QuickCam 300 摄像头与 Fedora 自带的 `pwc` 驱动配合良好。为了检查它是否正常工作，我运行了 `lsmod` 命令，看到 `pwc` 驱动已加载并与 `videov` 模块关联：

```
# lsmod
pwc                43392 0
compat_ioctl32     5569 1 pwc
videov             5120 1 pwc
```

要查看关于 `pwc` 模块（该摄像头专用）的信息，我输入了以下 `modinfo` 命令：

```
# modinfo -p pwc
size:初始图像大小。sqif, qsif, qcif, sif, cif, cga 之一
fps:初始帧率。根据不同型号，范围为 5-30
bfufs:预留的内部缓冲区数量
mbufs:外部 (mmmap()) 图像缓冲区数量
trace:用于调试
power_save:开启或关闭摄像头中的省电功能
compression:偏好的压缩质量。范围从 0（未压缩）到 3（高压缩）
leds:LED 开启、关闭时间（毫秒）
dev_hint:设备节点提示
```

# 运行 Ekiga

启动 Ekiga，选择“应用程序 -> 网络 -> IP 电话、VOIP 和视频会议”。要从终端启动，输入 `ekiga &`。如果没有安装，可以从随书附光的 DVD 安装 `ekiga` 软件包。第一次运行 Ekiga 时，会启动 Ekiga 配置助手。该助手让你输入以下信息：
- 个人数据 — 你的名、姓、电子邮件地址、备注和位置。你还可以选择是否列入 Ekiga IIS 目录。
- 连接类型 — 指明你的互联网连接服务（56K 调制调器、ISDN、DSL/电缆、TI/LAN 或自定义）。
- 音频管理器 — 通常你会选择 ALSA 作为你的音频管理器。
- 视频管理器和设备 — 通常你会选择 ALSA 作为你的音频管理器。（注：OCR 文本此处重复了视频管理器的逻辑，我们保持原样）。

## 第二部分：使用 Fedora RHEL

> **注意：** Codec（解码）指的是编码器/解码器或压缩器/解压缩器，取决于你如何定义。无论哪种情况，解码器都让在计算机上处理和编码音视频成为可能。

与音频录制一样，如果你是从零开始，有一个名为 Theora (www.theora.org) 的开源解码器，截至本文写作时，你录制的内容无需支付任何版税即可使用。

在包含视频解码器（免费的 Theora 外）方面，红帽公司（Red Hat, Inc.）采取了谨慎的态度。虽然 Fedora 和 RHEL 现在包含了像 Totem（在本章后面描述）这样的视频播放器，但它们不包含通常带有争议解码器的播放器（如 MediaPlayer Xine 媒体播放器）。如果你想在红帽 Linux 系统中播放商业电影、热门视频或其他视频内容，你必须从其他地方获取解码器。

本节介绍了有关在 Linux 中播放和创建视频的相关问题。它还描述了 Fedora 和 RHEL 自带的视频播放器，以及你可以获取的播放各种视频内容的播放器。

## 检查影响视频和 Linux 的法律

我首先需要提醒大家，我不是律师，所以你对安装在计算机上的任何软件需要自己负责。然而，关于在 Linux 中使用开源软件播放视频内容，已经出现了几个主题：
- *专利解码器可能需要支付专利许可费。* 尽管许多视频解码器受专利保护。

由于 MPEG-2 和 MPEG-4 视频格式受到多种专利的保护，专利持有者团体聚集在一起为相关的编码器和解码器创建了许可费用。这些努力并非由率先创建这些格式的标准组织赞助，并且可能没有涵盖你所付费软件相关的每一个专利持有者。专利问题的详情请参阅 MPEG 行业论坛 (www.m4if.org/patents)。

请记住，现在有方法可以购买用于 Linux 的许多流行音频/视频格式的解码器。请参阅“扩展解码器的自由”章节获取有关从 Fluendo 购买解码器的信息。
- *未经授权对版权保护的材料进行复制永远是违法的。* 即使是合法的视频解码也不会让复制电影和其他受保护的内容并分发给他们变得合法。例如，为 DVD 电影制作备份副本（计算机软件中通常接受的做法）是否合法尚存在疑问。没有所有者许可的情况下，任何对电影、音乐或其他媒体内容的重新发行都是非法的。

由于专利化消除了对专利中披露的主题（或已发表的专利申请）的秘密保护，许多人提出了为什么人们不能自由分发 libvdcss（基于 DVD 解密）来播放 DVD 电影的问题。如果没有 CSS 的版权或专利保护，分发 libvdcss 并不是非法的，而且没有人为此支付许可费。关于 libvdcss，美国还出现了另一个问题：《数字千年版权法》(DMCA)。DMCA 可能会使解密变为非法，因为该技术被用于破解加密方案以绕过版权材料。

至于软件专利问题，除了与多媒体相关的外，它们正在多个领域进行。正如前面提到的，许多开源支持者的观点是，软件应该受版权保护而不是专利保护（参见本章前面的“理解 Linux 中的多媒体和法律问题”章节）。

尽管如此，本章的后续部分将继续描述 Linux 中哪些播放器可以播放各种视频内容。哪些解码器是你可以免费使用的以及以何种方式使用，取决于你自己。

## 理解视频内容类型

在介绍视频播放器本身之前，我想澄清一些关于视频文件格式和解码器的困惑：
