

## 查看视频

你可以使用 Ubuntu 工具和应用程序在你的 PC 上观看电影和其他视频演示。本节介绍随本书附带的 Ubuntu 发行版中包含的一些电视和电影视频软件工具。

## 电视和视频硬件

要在 PC 上观看电视和视频内容，你必须安装受支持的电视卡或安装视频/电视组合卡。Ubuntu 支持的电视和视频卡的完整列表位于 http://www.exploits.org/r4l/。

视频卡上带有 TV-out 接口的电视显示的免费 Linux 支持很差。该支持必须来自 X 驱动程序，而不是 Video4Linux 通过设备驱动程序支持的视频设备。其中一些组合电视调谐器/视频显示卡有支持，包括 Matrox Marvel、Matrox Rainbow Runner G 系列和 RivaTV 卡。许多其他组合卡缺乏支持，尽管独立开发者可能为自己的卡拼凑了一些破解方案。你最好的做法是使用 Google 进行彻底的互联网搜索。

许多仅电视的 PCI 卡都受支持。然而在 Linux 中，它们是由其使用的视频芯片组支持的，而不是由某些制造商贴在通用板上的名称支持的（同一块板通常由不同制造商以不同名称出售）。最常见的芯片组是 Brooktree Bt*** 系列芯片；它们由 bttv 设备驱动程序支持。

如果你的计算机中有一张受支持的卡，它应该在安装期间被检测到。如果你稍后添加它，Kudzu 硬件检测实用程序应该检测到它并配置它。你也可以手动配置它。

要确定你的卡使用什么芯片组，请使用 lspci 命令列出 PCI 设备信息，找到电视卡列表，并查找卡使用的芯片组。例如，我的计算机的 lspci 输出显示

```
$ lspci
00:00.0 Host bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P] System Controller (rev 13)
00:01.0 PCI bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P] AGP Bridge
00:07.0 ISA bridge: VIA Technologies, Inc. VT82C686 [Apollo Super South] (rev 40)
00:07.1 IDE interface: VIA Technologies, Inc. VT82C686 PIPC Bus Master IDE (rev 06)
00:07.2 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.3 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.4 SMBus: VIA Technologies, Inc. VT82C686 [Apollo Super ACPI] (rev 40)
00:09.0 Multimedia audio controller: Ensoniq 5880 AudioPCI (rev 02)
00:0b.0 Multimedia video controller: Brooktree Corporation Bt878 Video Capture (rev 02)
00:0b.1 Multimedia controller: Brooktree Corporation Bt878 Audio Capture (rev 02)
00:0d.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8029(AS)
00:0f.0 FireWire (IEEE 1394): Texas Instruments TSB12LV23 IEEE-1394 Controller
00:11.0 Network controller: Standard Microsystems Corp [SMC] SMC2602W EZConnect
01:05.0 VGA compatible controller: nVidia Corporation NV15 [GeForce2 Ti] (rev a4)
```

这里，列出多媒体视频控制器和多媒体控制器的行说明这块电视板使用 Brooktree Bt878 视频采集芯片和 Brooktree Bt878 音频采集芯片。这张卡使用 Bt878 芯片组。你的结果会有所不同，这取决于你的计算机拥有什么卡和芯片组。这张卡碰巧是 ATI All-in-Wonder VE（也称为 ATI TV-Wonder）。（VE 表示 Value Edition；因此，该卡上没有 TV-out 连接器也没有无线电芯片；多么划算！）芯片组名称说明该卡使用 bttv 驱动程序。

在文档目录中有一个名为 CARDLIST 的文件，其中包含以下条目，其中之一：

```
card=64 - ATI TV-Wonder VE
```

列出了 105 张卡，以及 41 张无线电卡，包括

```
card=0 - *** UNKNOWN/GENERIC ***
```

如果你不知道卡的制造商名称，这就是你可以使用的内容。

位于同一目录中的名为 Modules.conf 的文件提供了以下要在 /etc/modules.conf 文件中放置的信息示例：

```
$ i2c
alias char-major-89 i2c-dev
options i2c-core i2c_debug=1
options i2c-algo-bit bit_test=1
```

```
$ bttv
alias char-major-81 videodev
alias char-major-81-0 bttv
options bttv card=2 radio=1
options tuner debug=1
```

你所需要做的就是将此信息输入 /etc/modules.conf 并将 card=2 的值更改为 card=64 以匹配你的硬件。你可以删除对无线电卡的引用（radio=2），因为没有无线电卡，其余值保持不变。然后你必须执行

```
$ sudo depmod -a
```

以重建模块依赖列表，以便所有模块自动加载。完成后，你所需要做的就是执行

```
$ sudo modprobe bttv
```
