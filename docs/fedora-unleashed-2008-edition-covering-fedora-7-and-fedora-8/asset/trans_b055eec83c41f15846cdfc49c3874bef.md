

ALSA 支持长名单的声卡。您可以在 http://www.alsa-project.org/alsa-doc/ 查看该列表。如果您的声卡不受支持，它可能在 OSS 的商业版本中受到支持。您可以下载商业软件的试用版本，并在 http://www.opensound.com/download.cgi 测试您的声卡。

Fedora 在原始安装过程中会检测大多数声卡。如果在初始安装后添加或更换声卡，Kudu 新硬件配置实用程序将在下次重启时自动检测并配置它。若要在其他时间配置声卡，请使用 `system-config-soundcard` 图形工具。该图形工具可在“系统”、“管理”菜单下的“声卡检测”菜单项中找到。

### 调整音量

Fedora 现在受益于 PulseAudio 的引入，这是一种在 Fedora 上控制声音的新方式。PulseAudio 允许您根据具体需求为每个程序量身定制音量设置，而不是拥有一个单一的全局音量级别。您可能希望将音乐播放得比视频更响；使用 PulseAudio 可以轻松做到这一点，PulseAudio 位于“应用程序”、“声音和视频”下，如图 7.14 所示。

![](img/34e72348d53ca54c2a1d9c871316691b_196_0.png)

**图 7.14** 使用音量滑块控制当前处理声音的每个应用程序的音量级别。

您也可以通过“输出”选项卡下的滑块来设置全局输出音量。

或者，您可以控制系统的所有输出音量，以确保您已将所有设置调整到满意的程度，如图 7.15 所示。要访问音量控制，请右键单击扬声器图标并选择“打开音量控制”。

![](img/34e72348d53ca54c2a1d9c871316691b_197_0.png)

**图 7.15** 使用音量控制管理所有声音输出设备的音量设置。

## 音频格式

存在多种用于存储录音的格式。其中一些格式与特定技术相关联，另一些则纯粹出于专有原因使用。Fedora 支持几种最流行的音频格式，包括：

- 原始格式（.raw）——更准确地称为无头格式（headerless format），使用该格式的音频文件包含各种特定设置和编码器的无定形变体。所有其他音频文件都在开头包含一小段代码——一个文件头——用于识别格式类型。
- MP3（.mp3）——一种流行但受商业许可保护的数字编码格式，被许多 Linux 和 Windows 应用程序使用。MP3 不受 Fedora 包含的任何软件支持（建议改用开源的 Ogg-Vorbis 格式）。
- WAV（.wav）——流行的未压缩 Windows 音频视觉声音格式。它通常用作音频编码的中间文件格式。
- Ogg-Vorbis（.ogg）——Fedora 首选的音频编码格式。当您对音频文件使用这种开源编码格式时，您可以享受更好的压缩率和音频播放质量，并免受诉讼困扰。

**注意**

由于专利和许可问题，Fedora 在 Fedora Linux 中移除对 MPE、MPEG2 和 MPEG3（MP3）文件格式的支持。虽然我们不提供任何法律建议，但看起来个人使用 MP3 软件是合法的。只是 Fedora 无法分发代码，因为它出售其发行版。目前看来，您获取支持 MP3 的 Xms 版本（例如，这是一个可以播放 MPEG1/2/3 文件的 Winamp 克隆）是完全没问题的。您可以直接从 http://www.xmms.org/ 获取 Xmms，因为该组织有权分发 MP3 代码。

您也可以通过使用 livna.org yum 软件仓库在 Fedora 中启用 MP3 编解码器。您需要安装 `gstreamer-plugins-mp3` 包，这将在所有 GNOME 应用程序中启用 MP3 编解码器。

另一种替代方案是使用 OggVorbis 格式；它完全不受限制。CD 音乐的抓轨器可从 http://www.thekompany.com/projects/tkcogripper/ 获取，MP3 转 Ogg 转换器可从 http://faceprint.com/code/ 获取。或者，您可以从 FreshRPMS 在 http://www.freshrpms.net/ 下载并安装未阉割版本的多媒体应用程序。

Fedora 包含软件（例如用于在音频格式之间转换的 sox 命令），以便您可以更轻松地收听以多种格式提供的音频文件，例如 AU（来自 NeXT 和 Sun）、AIFF（来自 Apple 和 SGI）、IFF（最初来自 Commodore 的 Amiga）、RA（来自 Real Audio）和 VOC（来自 Creative Labs）。

**提示**

若要了解音频格式的技术细节，请阅读 Chris Bagwell 的音频格式常见问题解答（FAQ），位于 http://www.cnpbagwell.com/audio.html。

Fedora 还提供用于将声音文件从一种格式转换为另一种格式的工具。转换工具在您希望使用当前首选应用程序不接受的格式中的声音时非常方便。转换工具库位于 http://libiblio.org/pub/linux/apps/sound/convert//INDEX.html，包括 Fedora 中找不到的 MP3 和音乐 CD 导向的工具。但是，您需要知道如何从源代码编译和安装。如果您看到有用的内容，如果您不想执行此任务，可以查看 http://www.rpmfind.net/ 以定位二进制 RPM。

Fedora 确实提供了 sox，这是一个自我描述的音频翻译器，可以在 AIF、AU、VAR、DAT、Ogg、WAV 和其他格式之间转换音乐。它还可用于更改音频文件的许多其他参数。

Timidity 是一个 MIDI 转 WAV 的转换器和播放器。如果您对 MIDI 和乐器感兴趣，Timidity 是一个便捷的应用程序；它还可以处理卡拉 OK 文件，显示歌词以配合您的演唱尝试。

### 查看视频

您可以使用 Fedora 工具和应用程序在 PC 上查看电影和其他视频演示。本节介绍随本书提供的 Fedora 发行版中包含的一些电视和电影视频软件工具。

### 电视和视频硬件

要在 PC 上观看电视和视频内容，您必须安装受支持的电视卡，或者安装视频/电视组合卡。Fedora 支持的电视和视频卡的完整列表位于 http://www.exploits.org/v4l/。

对于具有 TV-out 插孔的视频卡，自由可用的 Linux TV 显示支持较差。该支持必须来自 X 驱动程序，而不是来自 Video4Linux 通过设备驱动程序支持的视频设备。一些组合电视调谐器/视频显示卡具有支持，包括 Matrox Marvel、Matrox Rainbow Runner G-Series 和 RivaTV 卡。许多其他组合卡缺乏支持，尽管独立开发人员可能已自行修改以支持自己的卡。您最佳的做法是通过 Google 进行彻底的互联网搜索。

许多仅电视 PCI 卡受支持。然而，在 Linux 中，它们由所使用的视频芯片组支持，而不是由某些制造商贴在通用板上的名称支持（通常相同的板以不同名称由不同制造商销售）。最常见的芯片组是 Brooktree Bt8xx 系列芯片；它们由 bttv 设备驱动程序支持。

如果计算机中有受支持的卡，应在安装期间检测到它。如果稍后添加，Kudzu 硬件检测实用程序应检测到并配置它。您也可以始终手动进行配置。

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

此处，列出多媒体视频控制器和多媒体控制器的行表明，该电视板使用 Brooktree Bt878 Video Capture 芯片和 Brooktree Bt878 Audio Capture 芯片。此卡使用 Bt878 芯片组。您的结果会有所不同，取决于
