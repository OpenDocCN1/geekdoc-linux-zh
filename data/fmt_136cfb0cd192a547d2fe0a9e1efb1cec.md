
- Ogg-Vorbis `.ogg`——Fedora 优的音频编码格式。当您使用这种开源编码格式处理音频文件时，您可以获得更好的压缩效果和音频播放体验，并免受诉讼之扰。

> 注意
>
> 由于专利和许可问题，Fedora 移除了 Fedora Linux 中对 MPEG、MPEG2 和 MPEG3 `MP3` 文件格式的支持。虽然我们无法提供任何法律建议，但个人使用 MP3 软件似乎是没问题的；只是 Fedora 不能分发这些代码，因为它销售其发行版。似乎——在目前看来——您获取一个支持 MP3 的 XMS 版本（例如，一个播放 MPEG1/2/3 文件的 Winamp 克隆版本）是完全正确的。您可以直接从 `http://www.xmms.org/` 获取 XMMS，因为该小组有分发 MP3 代码的权限。

## 音频与音乐

您也可以通过 `livna.org` yum 仓库在 Fedora 中启用 MP3 解码器。您可以通过安装 `gstreamer-plugins-mp3` 实现此。

另一种选择是使用 Ogg-Vorbis 格式；它是免费的。您可以在 `http://thekom.com/` 下载并安装 MP3 播放器，并在 `http://faceprint.com/` 获取 MP3-to-Ogg 转换器。

Fedora 包含了实用程序（如 `so` 命令用于在格式之间进行转换），您可以轻松地将音频转换为另一种格式。`http://freesrpm.net`。

## 提示

> 欲了解更多关于音频格式的技术细节，请阅读 Chris Bagwell 的《音频 FAQ》(`http://www.cnbag.com/audio.html`)。

Fedora 还提供了用于将音频文件从一种格式转换为另一种格式的工具。当您需要当前应用程序不支持的格式时，转换工具非常有用。`http://biblio.org/pub/apps/convert/INDEX.html` 包含了 MP3 和 CD 实用程序。您可以从源码编译。

## 查看视频

要确定您的显卡是什么芯片组，请使用 `lspci` 命令。例如，我电脑的 `lspci` 输出如下：

```
# lspci
00:00 Host bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1]
-System Controller (rev 13)
00:01 PCI bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1] AGP Bridge
00:07 ISA bridge: VIA Technologies, Inc. VT82C58B [Apollo South South] (rev 40)
00:71 IDE interface: VIA Technologies, Inc. PIPC Bus Master IDE
- rev 06
00:72 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:73 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:74 SMBus: VIA Technologies, Inc. VT82C58B [Apollo Super ACPI] (rev 40)
00:90 Multimedia audio controller: Eniqiq 5880 AudioPCI (rev 02)
00:b0 Multimedia video controller: Brooktree Corporation Bt878 Video Capture
- rev 02
00:b1 Multimedia controller: Brooktree Corporation Bt878 Audio Capture (rev 02)
00:d0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8029(AS)
00:f0 FireWire (IEEE 1394): Texas Instruments TSB12LV23 IEEE-1394 Controller
01:10 Network controller: Standard Microsystems Corp [SMC] SMC2620 EZConnect
01:05 VGA compatible controller: Nvidia Corporation NV15 [GeForce 2i] (rev a4)
```

在这里，列出多媒体视频控制器和控制器的行说明该电视板使用了 Brooktree Bt778 视频芯片和 Brooktree Bt778 音频芯片。您的卡使用的是 Bt778 芯片组。您的结果取决于

你的电脑使用的是什么显卡和芯片组。这张显卡恰好是 ATI All-in-Wonder VE（也称为 ATI TV-Wonder）。（VE 代表 Value Edition；因此显卡上没有 TV 接口也没有无线电芯片；真是超值！）芯片组的名称表明该显卡使用 `bttv` 驱动。

在文档目录中有一个名为 `CARDLIST` 的文件，文件中包含以下条目（等）：

```
card=64 - ATI TV-Wonder VE
```

列出了 105 块显卡，以及 41 块无线电显卡，包括：

```
card=0 *** UNKNOWN/GENERIC ***
```

如果你不知道显卡的制造商名称，就可以使用这一项。

位于同一目录下的 `Modules.conf` 文件提供了以下一个可以放置在 `/etc/modules.conf` 中的信息示例：

```
# i2c
alias char-major-89 i2c-dev
options i2c-core i2c-debug=1
options i2c-algo-bit bit_test=1
```

```
# bttv
alias char-major-81 videodev
alias char-major-81-0 bttv
options bttv card=2 radio=1
options tuner debug=1
```

你只需要将这些信息输入 `/etc/modules.conf`，并将 `card=2` 的值更改为 `card=64` 以匹配你的硬件。你可以删除对无线电卡的引用（`radio=2`），因为并没有这种卡，并保持其他值不变。你必须执行

```
# depmod -a
```

以重新构建模块依赖列表，以便所有模块都能自动加载。完成后，你只需要执行

```
# modprobe bttv
```

然后你的电视卡就能完全正常工作了。每当你重启时，所有正确的模块都会自动加载。Fedora 足够聪明，可以在安装期间检测并配置已存在的支持的电视卡。

### 提示士

其他有用的文档可以在 `/usr/src/linux-2.6/Documentation/_video4linux` 中找到。在你确定了设备的驱动程序后，查看它的源代码并无害，因为许多驱动程序几乎没有正式文档；其大部分内容都在源码注释中。

Linux 对电视卡支持的开发已在 Video4Linux 项目下整合。Video4Linux 软件为 Fedora 提供了视频采集、无线电和文字电视设备的支持。

## 视频格式

Fedora 识别多种视频格式。然而，由 MPEG 组、Apple 和微软创建的格式占据主。视频格式的核心是编码器——视频和音频信息的编码器和解码器。这些编码器通常是专有的，但存在免费的编码器。是最常见的视频格式及其相关文件扩展名的列表：

- `.mpg`—MPEG 视频格式；也称为 `.mpg`

- `.qt`—Apple 的 QuickTime 视频格式

- `.mov`—另一个 QuickTime 视频格式

- `.avi`—Windows 音视频格式

### 提示士

为 Linux 提供 Divx 编码器的 RPM 软件包可以在 `http://www.freshrpms.net/` 找到。Divx 是一种专利 MPEG-4 视频编码器，是该类型中应用广泛的编码器。它允许对 MPEG-2 视频进行 8 倍压缩。更多信息请访问 `http://www.divx.com/`。

`GetCodes` 应用是一个带有 GUI 界面的 Python 脚本，它可以下载、安装并配置 Fedora 未提供的多媒体编码器，例如 MP3、Divx 和 DVD 编码器。该脚本从 `http://forge.net/projects/getcodes/` 获取。

如果你需要将视频从一种格式转换为另一种格式，你需要使用编码器抓取器（grabbers）。这些应用程序来自摄像头或电视卡等视频设备的原始数据，并将其转换为标准 MPEG 格式之一或静态图像格式（如 JPEG 或 GIF）。Fedora 不提供任何编码器应用程序（除了 `ffmpeg`，它可编码 MPEG-1 视频），你可以在 `http://www.freshrpms.net/` 或另一个在线源找到它们（参见本章末尾的“参考”部分）。

## 在 Linux 中观看视频
