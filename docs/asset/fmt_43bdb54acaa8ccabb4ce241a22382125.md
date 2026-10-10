
您可以使用 Fedora 工具和应用程序在 PC 上查看电影和其他视频演示。本节介绍随本书提供的 Fedora 发行版中包含的一些电视和电影视频软件工具。

### 电视和视频硬件

要在 PC 上观看电视和视频内容，您必须安装受支持的电视卡，或者安装视频/电视组合卡。Fedora 支持的电视和视频卡的完整列表位于 http://www.exploits.org/v4l/。

对于具有 TV-out 插孔的视频卡，自由可用的 Linux TV 显示支持较差。该支持必须来自 X 驱动程序，而不是来自 Video4Linux 通过设备驱动程序支持的视频设备。一些组合电视调谐器/视频显示卡具有支持，包括 Matrox Marvel、Matrox Rainbow Runner G-Series 和 RivaTV 卡。许多其他组合卡缺乏支持，尽管独立开发人员可能已自行修改以支持自己的卡。您最佳的做法是通过 Google 进行彻底的互联网搜索。

许多仅电视 PCI 卡受支持。然而，在 Linux 中，它们由所使用的视频芯片组支持，而不是由某些制造商贴在通用板上的名称支持（通常相同的板以不同名称由不同制造商销售）。最常见的芯片组是 Brooktree Bt8xx 系列芯片；它们由 `bttv` 设备驱动程序支持。

如果计算机中有受支持的卡，应在安装期间检测到它。如果稍后添加，`Kudzu` 硬件检测实用程序应检测到并配置它。您也可以始终手动进行配置。

要确定卡的芯片组，请使用 `lspci` 命令列出 PCI 设备信息，找到电视卡列表，并查看卡使用的芯片组。例如，我的计算机的 `lspci` 输出显示以下内容：

```bash
# lspci
00:00.0 Host bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P] 
System Controller (rev 13)
00:01.0 PCI bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P] AGP Bridge
00:07.0 ISA bridge: VIA Technologies, Inc. VT82C686 [Apollo Super South] (rev 40)
00:07.1 IDE interface: VIA Technologies, Inc. VT82C586B PIPC Bus Master IDE 
(rev 06)
00:07.2 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.3 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.4 SMBus: VIA Technologies, Inc. VT82C686 [Apollo Super ACPI] (rev 40)
00:09.0 Multimedia audio controller: Ensoniq 5880 AudioPCI (rev 02)
00:0b.0 Multimedia video controller: Brooktree Corporation Bt878 Video Capture 
(rev 02)
00:0b.1 Multimedia controller: Brooktree Corporation Bt878 Audio Capture (rev 02)
00:0d.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8029(AS)
00:0f.0 FireWire (IEEE 1394): Texas Instruments TSB12LV23 IEEE-1394 Controller
00:11.0 Network controller: Standard Microsystems Corp [SMC] SMC2602W EZConnect
01:05.0 VGA compatible controller: nVidia Corporation NV15 [GeForce2 T1] (rev a4)
```

此处，列出多媒体视频控制器和多媒体控制器的行表明，该电视板使用 Brooktree Bt878 Video Capture 芯片和 Brooktree Bt878 Audio Capture 芯片。此卡使用 Bt878 芯片组。您的结果会有所不同，取决于你的电脑拥有什么样的显卡和芯片组。这张卡恰好是 ATI All-in-Wonder VE（也称为 ATI TV-Wonder）。（VE 代表 Value Edition（价值版）；因此，该卡上没有 TV-out 连接器和无线电芯片；这就是所谓的“价值”所在！）芯片组的名称表明该卡使用 `bttv` 驱动程序。

在文档目录中有一个名为 `CARDLIST` 的文件，该文件中包含以下条目（除其他内容外）：

```
card=64 · ATI TV-Wonder VE
```

列出了 105 张卡，以及 41 张无线电卡，包括

```
card=0 · *** UNKNOWN/GENERIC ***
```

如果你不知道该卡的制造商名称，本来可以使用这个条目。

位于同一目录下的文件 `Modules.conf` 提供了以下示例信息，用于放置在 `/etc/modules.conf` 文件中：

```
# i2c
alias char-major-89 i2c-dev
options i2c-core i2c_debug=1
options i2c-algo-bit bit_test=1

# bttv
alias char-major-81 videodev
alias char-major-81-0 bttv
options bttv card=2 radio=1
options tuner debug=1
```

你只需要将这些信息输入 `/etc/modules.conf`，并将 `card=2` 的值更改为 `card=64` 以匹配你的硬件。你可以删除对无线电卡的引用（`radio=2`），因为并没有该组件，而其他值保持不变。然后你必须执行

```
# depmod -a
```

以重建模块依赖列表，以便所有模块都能自动加载。完成后，你只需执行

```
# modprobe bttv
```

你的电视卡就应该可以完全正常工作了。每次重启时，所有正确的模块都会自动加载。Fedora 足够聪明，可以在安装期间检测并配置支持的电视卡（如果存在的话）。

# 视频格式

Fedora 识别多种视频格式。然而，MPEG 组、Apple 和 Microsoft 创建的视频格式占据主导地位。视频格式的核心是编解码器——视频和音频信息的编码器和解码器。这些编解码器通常是专有的，但也存在免费编解码器。以下是最常见的视频格式及其关联文件扩展名的列表：

- `.mpeg`—MPEG 视频格式；也称为 `.mpg`
- `.qt`—来自 Apple 的 QuickTime 视频格式
- `.mov`—另一种 QuickTime 视频格式
- `.avi`—Windows 音频视觉格式

如果你需要将视频从一种格式转换为另一种格式，你使用称为 *抓取器*（grabbers）的编码器应用程序。这些应用程序从摄像头或电视卡等视频设备获取原始视频数据，并将其转换为标准的 MPEG 格式之一，或转换为静态图像格式，如 JPEG 或 GIF。Fedora 不提供任何编码器应用程序（除了 `pnmtopng`，它用于编码 MPEG-1 视频），但你可以从 http://www.freshrpms.net/ 或其他在线资源（参见本章末尾的“参考”部分）找到它们。

# 在 Linux 中观看视频

由于前面提到的专利和授权问题，播放视频文件的功能已从 Fedora 中移除。如果你从 FreshRPMs 安装本文所述应用程序的完整版本（位于 http://www.freshrpms.net/），可以恢复此功能。在那里，你可以找到 `Ogre`、`Xine`、`AlsaPlayer`、`Gstreamer`、`Grip`、`Mplayer`、`VCDImager`、`VideoLAN-client`、`Xmmns` 和 `Zapping` 等多媒体应用程序。

你可以使用 Linux 软件看电视、保存单独的图像（从电视广播中截取快照）、保存一系列快照以构建动画序列，或捕获视频、音频或两者。以下各节介绍了一些你可以让 Linux 多媒体软件为你工作的方法。

Fedora 提供 `noatun` 查看器，用作 `Konqueror` 浏览器中的嵌入式查看器。`noatun` 被设置为其所播放视频文件格式的默认关联。在 `Konqueror` 或 `Nautilus` 中打开视频文件，如果该格式受支持，视频就会在查看器中显示。该查看器提供基本的开始、停止和快进等 VCR 类型功能。

你可以使用 `Xine` 观看 MPEG 和 DVD 视频。`Xine` 是一个多功能且流行的媒体播放器，但不随 Fedora 提供。`Xine` 用于观看 AVI、QuickTime、Ogg 和 MP3 文件（后者在 Fedora 中是禁用的）。

## Macromedia Flash
