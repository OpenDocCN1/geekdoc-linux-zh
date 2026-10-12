
00:0b.0 多媒体控制器：Brooktree Corporation Bt878 音频采集 (rev 02)
00:0d.0 以太网控制器：Realtek Semiconductor Co., Ltd. RTL-8029(AS)
00:0f.0 FireWire (IEEE 1394)：Texas Instruments TSB12LV23 IEEE-1394 控制器
00:11.0 网络控制器：Standard Microsystems Corp [SMC] SMC2602W EZConnect
01:05.0 VGA 兼容控制器：nVidia Corporation NV15 [GeForce2 Ti] (rev a4)

这里，列出多媒体视频控制器和多媒体控制器的行说明我们的电视卡使用了 Brooktree Bt878 视频采集芯片和 Brooktree Bt878 音频采集芯片。这张卡使用的是 Bt878 芯片组。根据你的计算机拥有什么卡和芯片组，结果会有所不同。这张卡碰巧是 ATI All-in-Wonder VE（也称为 ATI TV-Wonder）。（VE 代表价值版；因此，该卡上没有电视输出连接器和无线电芯片；多么超值！）芯片组的名称告诉我们，该卡使用 bttv 驱动程序。

用于录制声音的 **bt878** 内核声音模块的文档位于 `/usr/src/linux-2.6/Documentation/sound/ossbtaudio`。视频驱动程序的文档位于 `/usr/src/linux-2.6/Documentation/video4linux/bttv` 下。

在文档目录中，我们找到一个名为 `CARDLIST` 的文件，在该文件中，除了其他条目外，还有以下条目：

```
card=64 - ATI TV-Wonder VE
```

列出了 105 张卡以及 41 张无线电卡，包括：

```
card=0 - *** UNKNOWN/GENERIC ***
```

如果我们不知道我们卡片的制造商名称，就会使用这个条目。

位于同一目录中的名为 `Modules.conf` 的文件，为我们提供了放入我们的 `/etc/modules.conf` 文件的信息示例：

```
# i2c
alias char-major-89    i2c-dev
options i2c-core        i2c_debug=1
options i2c-algo-bit    bit_test=1

# bttv
alias char-major-81    videodev
alias char-major-81-0  bttv
options bttv           card=2 radio=1
options tuner          debug=1
```

我们需要做的只是将这些信息输入 `/etc/modules.conf`，并将 `card=2` 的值更改为 `card=64` 以匹配我们的硬件。我们可以删除对无线电卡（`radio=2`）的引用，因为我们没有无线电卡，其他值保持不变。然后我们必须执行

```
# depmod -a
```

重建模块依赖列表，以便自动加载所有模块。完成后，我们只需执行

```
# modprobe bttv
```

我们的电视卡应该就能完全正常工作。每次重新启动时，所有正确的模块都会自动加载。Fedora 足够聪明，能够检测并配置安装期间存在的受支持的电视卡。

> **TIP**
>
> 在 `/usr/src/linux-2.6/Documentation/_video4linux` 中可以找到其他有用的文档。在确定设备的驱动程序后，查看其源代码并不会造成伤害，因为许多驱动程序几乎没有正式文档；其中大部分内容都在源代码注释中。

Linux 中电视卡支持的开发已在 Video4Linux 项目中汇聚。Video4Linux 软件在 Fedora Core 中提供对视频采集、无线电和 Teletext 设备的支持。

## 视频格式

Fedora 识别多种视频格式。然而，MPEG 组、Apple 和 Microsoft 创建的主导格式占主导地位。视频格式的核心是*编解码器*——视频和音频信息的编码器和解码器。这些编解码器通常是专有的，但免费编解码器也存在。以下是一些最常见视频格式及其关联文件扩展名的列表：

- `.mpeG`—MPEG 视频格式；也称为 `.mpg`
- `.qt`—来自 Apple 的 QuickTime 视频格式
- `.mov`—另一种 QuickTime 视频格式
- `.avi`—Windows 音视频格式

> **TIP**
>
> 在 `http://www.freshrpms.net/` 可以找到提供 Linux DivX 编解码器的 RPM。DivX 是一种专利的 MPEG-4 视频编解码器，是同类中应用最广泛的编解码器。它允许将 MPEG-2 视频压缩 8 倍。更多信息见 `http://www.divx.com/`。

GetCodecs 应用程序是一个具有图形用户界面（GUI）的 Python 脚本，它将下载、安装并配置 Fedora 系统以使用 Fedora 未提供的多媒体编解码器，如 MP3、DivX 和 DVD 编解码器。该脚本可以从 http://sourceforge.net/projects/getcodecs/ 获取。

如果需要将视频从一种格式转换为另一种格式，你使用称为*抓取器*的编码器应用程序。这些应用程序从摄像头或电视卡等视频设备获取原始视频数据，并将其转换为标准 MPEG 格式之一或静态图像格式，如 JPEG 或 GIF。Fedora 不提供任何编码器应用程序（除了编码 MPEG-1 视频的 ppmtompeg 外），但你可以从 http://www.freshrpms.net/ 或其他在线来源找到它们（参见本章末尾的“参考”部分）。

## 在 Linux 中观看视频

由于前面提到的专利和许可问题，播放视频文件的功能已从 Fedora 中移除。如果你从 http://www.freshrpms.net/ 的 FreshRPMs 安装本节描述的应用程序完整版本，则可以恢复此功能。在那里，你将找到 Ogle、Xine、AlsaPlayer、Gstreamer、Grip、Mplayer、VCDImager、VideoLAN-client、Xmms 和 Zapping 等多媒体应用程序。

你可以使用 Linux 软件看电视、从电视广播中保存单个图像（拍摄快照）、保存一系列快照以构建动画序列，或采集视频、音频或两者兼有。以下各节介绍了你可以利用 Linux 多媒体软件工作的一些方法。

*noatun* 查看器随 Fedora 提供，用作 Konqueror 浏览器中的嵌入式查看器。noatun 被设置为它所播放的视频文件格式的默认关联。在 Konqueror 或 Nautilus 中打开视频文件，如果受支持，视频将在查看器中显示。查看器提供基本的 VCR 型开始、停止和快进功能。

你可以使用 Xine 观看 MPEG 和 DVD 视频。Xine 是一个多功能且流行的媒体播放器，未包含在 Fedora 中。Xine 用于观看 AVI、QuickTime、OGG 和 MP3 文件（后者在 Fedora Core 中禁用）。

### Macromedia Flash

用于 Mozilla 浏览器的 Macromedia Flash 插件是一个商业多媒体应用程序，Fedora 不提供，但许多人发现它很有用。Macromedia Flash 使你能查看支持该内容的网站上的 Flash 内容。Mozilla 插件可以从 http://macromedia.mplug.org/ 获取。提供 *.rpm* 和 *.tar.gz* 文件。

下载 Linux 文件，如果使用 *.tar.gz* 文件，用以下方式解压缩：

```
# tar zxvf install_flash_player_6_linux.tar.gz
```

这将生成一个名为 `flashplayer_installer` 的目录。用以下方式安装插件：

```
# ./install_flash_player_6_linux/flashplayer-installer
```

并按照屏幕提示进行安装，使其可用于 Mozilla 浏览器。

Macromedia Flash 的 Mozilla 插件有问题？只需手动将文件 `flashplayer.xpt` 和 `libflashplayer.so` 复制到 `/usr/lib/mozilla/plugins`。可以从 http://macromedia.mplug.org/ 获取一个应该可以无问题安装的 Flash `.rpm` 文件。

另一个有趣的视频查看器应用程序是 MPlayer（Fedora 不提供），这是一个用于 Linux 的电影播放器。MPlayer 可以使用 Win32 编解码器，支持比 Xine 更广泛的视频格式，包括 DivX 和一些 RealMedia 文件。MPlayer 还使用一些支持 Matrox、3Dfx 和 Radeon 卡片的特殊显示驱动程序，并可以利用一些硬件 MPEG 解码板以获得更好的 MPEG 解码。请在 http://www.MPlayerHQ.hu/homepage/ 查找 Fedora 软件包；还可以获取 Win32 编解码器软件包以及其他编解码器软件包和图形用户界面。

## 使用 Linux 观看电视

你可以配置多个视频输入源，将电视图像传输到你的计算机。你可以使用前面描述的受支持的任何电视设备连接有线电视、Xbox、Sega Dreamcast、PS/2，甚至外部电视天线到你的计算机，并在你的视频显示器上查看图像。

Fedora 提供 `tvtime` 电视观看应用程序，使你无需离开计算机即可观看 *South Park*。

> **NOTE**
>
> `kdetv` 应用程序（前身为 QtVision）在流行度和功能方面都在稳步增长，值得一试。可以从 http://www.kdetv.org/ 下载。

从命令行启动 `tvtime`：

```
$ tvtime &
```

右键单击它会切换选项菜单的显示。调整设置以适应你的硬件。

```
$ scantv
```

`tvtime` 配置文件的详细信息包含在 `tvtime` 的手册页中。

FreshRPMS.Net 上可用的替代电视观看应用程序是 Zapping，这是一个支持 Video4Linux、Video4Linux2 和 Xvideo 的 GNOME 查看器，可通过插件扩展功能。主页是 http://zapping.sourceforge.net/。

