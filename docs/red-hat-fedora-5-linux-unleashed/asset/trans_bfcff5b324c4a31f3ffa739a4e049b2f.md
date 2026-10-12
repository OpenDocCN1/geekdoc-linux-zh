

![](img/2045828cf45e5632bf056f9ca99d6755_311_0.png)

图 10.6 Rhythmbox 可以处理播客、网络电台、CD 和本地音频文件。

> 在 Fedora Core 桌面系统默认提供的 GNOME 元数据桌面环境中，可以进行菜单编辑。你只需右键单击 Fedora 应用程序按钮，然后选择“编辑菜单”即可。之后，你可以根据需要选中或取消选中选项。

## 流式音频

流式音频用于玩游戏、收听网络电台以及其他在线音频内容。流式音频旨在产生不间断的声音输出，但要求系统执行一系列内容操作。本质上，系统的音频缓冲区会持续接收音频信息，这些信息通过系统的互联网连接输入到缓冲区中。由于服务器和连接能力的不同，输入速率可能会有变化。由于音频以恒定速率被使用，管理流式音频的技巧在于始终保持缓冲区充足，尽管你可能无法以恒定速率填充它。

在 Fedora 中，流式音频通常以 .m3u 格式处理。MPEG 格式也用于流式音频。虽然 Xmsm 支持流式音频，但另一个流行的应用程序是 Real Player，可从 http://www.real.com/linux/ 获取。http://linux-sound.org/ 是 Linux 音乐和声音方面的一个优秀资源。该网站的“网络音频”部分包含一份详尽的流式音频应用程序列表。

Icecast 应用程序（Fedora 未附带）是一个流行的流式音频服务器。你可以使用 Icecast 通过家庭局域网（LAN）提供你的 MP3 音乐收藏。你可以在 http://www.icecast.org/ 了解有关 Icecast 的更多信息。一个关于 Icecast 的精彩教程可在 http://www.linuxnetmag.com/en/issue4/m4icecast1.html 找到。

> **提示**
> 你還可以阅读第 18 章“网络连接”，了解如何使用网络文件系统（NFS）通过网络挂载远程音乐文件目录。

## 观看电视和视频

你可以使用 Fedora 的工具和应用程序在 PC 上观看电影和其他视频演示。本节介绍了随本书提供的 Fedora Core Linux 发行版中附带的一些电视和动态影像视频软件工具。

除了这里阅读的信息外，你还应该查阅第 3 章“安装 Fedora”和第 6 章“X 窗口系统”，以了解有关安装和配置视频图形卡的更多信息。

### 电视和视频硬件

要在 PC 上观看电视和视频内容，你必须安装受支持的电视卡，或者安装视频/电视组合卡。Fedora 支持的电视和视频卡的完整列表位于 http://www.expolots.org/~v4/l/。有关 ATI 视频组合卡的信息，请参见 http://gatos.sourceforge.net 上的 Gatos 项目。

对于具有电视输出插孔的视频卡，Linux 免费提供的电视显示支持较差。这种支持必须来自 X11 驱动程序，而不是来自 Video4Linux 通过设备驱动程序支持的视频设备。一些组合电视调谐器/视频显示卡具有支持，包括 Matrox Marvel、Matrox Rainbow Runner G-Series 和 RivaTV 卡。许多其他组合卡缺乏支持，尽管某个独立开发者可能已经为支持自己的卡而进行了某种修改。你最好的行动方案是使用 Google 进行彻底的互联网搜索。

许多仅支持电视的 PCI 卡是受支持的。然而，在 Linux 中，它们是通过所使用的视频芯片组支持的，而不是通过某些制造商贴在通用主板上的名称支持的（同一块主板通常由不同的制造商以不同的名称出售）。最常见的芯片组是 Brooktree Bt8xx 系列芯片；它们由 bttv 设备驱动程序支持。

如果你的计算机中有受支持的卡，它应在安装过程中被检测到。如果你稍后添加，Kudzu 硬件检测实用程序应该能够检测并配置它。你始终可以手动进行配置。

要确定你的卡使用什么芯片组，请使用 lspci 命令列出 PCI 设备信息，找到电视卡列表，并查找该卡使用的芯片组。例如，我们计算机的 lspci 输出显示：

```bash
# lspci
00:00.0 Host bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]
    - System Controller (rev 13)
00:01.0 PCI bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]
    - AGP Bridge
00:07.0 ISA bridge: VIA Technologies, Inc. VT82C686 [Apollo Super South]
    - (rev 40)
00:07.1 IDE interface: VIA Technologies, Inc. VT82C586B PIPC Bus Master IDE
    - (rev 06)
00:07.2 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.3 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.4 SMBus: VIA Technologies, Inc. VT82C686 [Apollo Super ACPI]
    - (rev 40)
00:09.0 Multimedia audio controller: Ensoniq 5880 AudioPCI (rev 02)
00:0b.0 Multimedia video controller: Brooktree Corporation Bt878 Video Capture
    - (rev 02)
00:0b.1 Multimedia controller: Brooktree Corporation Bt878 Audio Capture
    - (rev 02)
00:0d.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8029(AS)
00:0f.0 FireWire (IEEE 1394): Texas Instruments TSB12LV23 IEEE-1394
    - Controller
00:11.0 Network controller: Standard Microsystems Corp [SMC]
    - SMC2602W E2ZConnect
01:05.0 VGA compatible controller: nVidia Corporation NV15 [GeForce2 Ti]
    - (rev a4)
```

在这里，列出多媒体视频控制器和多媒体控制器的行表明，我们的电视板使用 Brooktree Bt878 视频捕获芯片和 Brooktree Bt878 音频捕获芯片。这张卡使用 Bt878 芯片组。根据你的计算机拥有的卡和芯片组不同，你的结果也会不同。这张卡恰好是一块 ATI All-in-Wonder VE（也称为 ATI TV-Wonder）。（VE 代表 *价值版*；因此，卡上没有电视输出连接器和无线电芯片；多么超值！）芯片组的名称告诉我们该卡使用 bttv 驱动程序。

在文档目录中，我们找到一个名为 **CARDLIST** 的文件，该文件中有如下条目，以及其他条目：

```
card=64 - ATI TV-Wonder VE
```

列出了 105 张卡，以及 41 张无线电卡，其中包括：

```
card=0 - *** UNKNOWN/GENERIC ***
```

如果我们不知道制造商对我们卡的命名，本应使用此项。

位于同一目录中的名为 Modules.conf 的文件，为我们提供了应放置在 /etc/modules.conf 文件中的信息示例：

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

我们只需将此信息输入 /etc/modules.conf，并将 card=2 的值更改为 card=64 以匹配我们的硬件。由于我们没有无线电卡，我们可以删除对无线电卡的引用（radio=1），并保持其他值不变。然后我们必须执行：

```
# depmod -a
```

以重建模块依赖列表，使所有模块都能自动加载。完成后，我们只需执行：

```
# modprobe bttv
```

我们的电视卡应该就能完全正常工作。每次重启时，所有正确的模块都会自动加载。Fedora 足够智能，能够检测并配置在安装期间存在的受支持的电视卡。

![](img/2045828cf45e5632bf056f9ca99d6755_314_0.png)

> 其他有用的文档可以在 /usr/src/linux-2.6/Documentation/video4linux 中找到。在确定了设备的驱动程序后，查看其源代码也无妨，因为许多驱动程序缺乏正式的文档；其中很大一部分内容存在于源代码注释中。

Linux 中对电视卡支持的开发已汇聚到 Video4Linux 项目之下。Video4Linux 软件为 Fedora Core 中的视频捕获、无线电和图文电视设备提供支持。

## 视频格式

Fedora 识别多种视频格式。然而，MPEG 组、Apple 和 Microsoft 创建的格式占主导地位。视频格式的核心是编解码器——即视频和音频信息的编码器和解码器。这些编解码器通常是
