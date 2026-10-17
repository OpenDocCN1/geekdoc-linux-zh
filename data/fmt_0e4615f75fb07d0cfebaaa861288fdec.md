
`matthew@seymour:~$ sudo user_application | growisofs -Z /dev/scd0=/dev/fd0`

It is also possible to burn from an existing image (or file, named pipe, or device):

`matthew@seymour:~$ sudo growisofs -Z /dev/scd0=image`

在使用该程序之前，`/usr/share/doc/dvd+rw-tools/index.html`上的`dvd+rw-tools`文档是必读内容。我们建议您先使用 DVD-RW（可重写）介质进行实验，因为如果您犯了错误，您仍然可以重复使用光盘，而不是为咖啡杯制作几个新的杯垫。

## 查看视频

您可以使用 Ubuntu 工具和应用程序在 PC 上观看电影和其他视频演示。本节介绍随本通知提供的 Ubuntu 发行版中包含的一些电视和电影视频软件工具。

### 电视和视频硬件

要在 PC 上观看电视和视频内容，您必须安装受支持的电视卡或安装视频/电视组合卡。您可以在 `http://linuxtv.org/wiki/index.php/Main_Page` 上找到 Linux 支持的电视和视频卡的当前列表。

从具有 TV-out 接口的显卡自由提供 Linux 电视显示支持的情况比几年前有所改善，但仍然相当糟糕。支持必须来自 X 驱动程序，而不是 Linux 通过设备驱动程序支持的视频设备。其中一些组合电视调谐器/显示卡具有支持，包括 Matrox Marvel、Matrox Rainbow Runner G 系列和 RiVA 卡。许多其他卡缺乏支持，尽管独立开发者可能为自己的卡拼凑了一些东西。您最好的做法是使用 Google 进行彻底的互联网搜索。

多对一 PCI 卡受支持。但是在 Linux 中，它们由视频芯片组支持，而不是由在通用板上贴上自己标签的同一制造商支持。最常见的选择是 Brooktree 系列芯片，由 `bttv` 驱动程序支持。

如果您的计算机中有受支持的卡，它应该在安装期间被检测到。如果您添加了它，硬件检测实用程序应该检测并配置它。可以尝试手动配置它，但由于 Ubuntu 内核试图将所有可用的硬件选项作为模块编译并制作它，因此可能对您没有多大用处。即使如此，这就是您要做的事情。

First, to determine which card you have, use the `lspci` command to list the PCI device information, find the TV card list, and look for the chip that the card uses. For example, `lspci` output on one computer shows the following:

```
matthew@~$ lspci
000.00 Host bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P] System
Controller (rev 13)
000.01 PCI bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P] AGP Bridge
007.00 ISA bridge: VIA Technologies, Inc. VT825C686 [Apollo Support Set] (rev 40)
007.01 IDE interface: VIA Technologies, Inc. VT825C686 PIPC Bus Master IDE (rev 06)
007.02 USB Controller: VIA Technologies, Inc. USB (rev 1a1)
007.03 USB Controller: VIA Technologies, Inc. USB (rev 1a1)
007.04 SMBus: VIA Technologies, Inc. VT825C686 [Apollo Support ACPI] (rev 40)
009.00 Multimedia audio controller: Ensoniq 5880 AudioPCI (rev 02)
00b.00 Multimedia video controller: Brooktree Corporation Bt8788 Video Capture
(rev 02)
```

## 第6章 多媒体应用

00:0b.1 多媒体控制器: Brooktree Corporation Bt878 Audio Capture (rev 02)

00:0d.0 以太网控制器: Realtek Semiconductor Co., Ltd. RTL-8029 (AS)

00:0f.0 FireWire (IEEE 1394): Texas Instruments TSB2LV23 IEEE-1394 Controller

00:11.0 网络控制器: Standard Microsystems Corp [SMC] SMC2602W EZConnect

01:05.0 VGA 兼容控制器: Nvidia Corporation NV15 [GeForce2] (rev a4)

这里，列出视频控制器和多媒体控制器的行表明该电视板使用 Brooktree Bt878 视频采集芯片，而 Brooktree Bt878 音频采集芯片使用 Bt878 芯片。你的结果会有所不同，这取决于你的电脑使用什么卡和芯片组。该卡恰好是 ATI All-in-Wonder VE（也称为 ATI TV Wonder）。（VE 表示 Value Edition；这里，该卡上没有电视调谐器也没有无线电芯片；

然后你弄清楚需要什么模块，可能使用 Google 搜索 "`Bt878 linux`" 或 "`Bt878 ubuntu`"，并阅读文档。你希望首先查找官方页面而不是博客文章。最后，你需要在 `/etc/modules.conf` 中输入一些信息。该文件在默认的 Ubuntu 安装中不存在，但可根据需要创建，并在启动时读取。然后，使用 `sudo depmod -a` 和 `sudo modprobe name` 计算模块和内核依赖关系以加载模块。同样，这在 Ubuntu 中是不必要的，因为人们对内核配置进行了模块化，一切皆模块，所以如果他们可以使用，就会在不额外工作的情况下让你也能使用，系统会扫描在启动时应加载的内容并随后引入所需内容。

### 视频格式

Ubuntu 识别多种视频格式。然而，由 MPEG 组织、Apple 和 Microsoft 创建的格式占据主导地位。视频格式的核心是编解码器——视频和音频信息的编码器和解码器。编解码器通常是专有的，但也存在免费编解码器。以下是最常见的视频格式及其相关文件扩展名的列表，尽管存在许多格式：

- AVI (`.avi`)—Windows 音视频格式

- FLV (`.flv`)—在 Adobe Flash 中；H.264 和其他 6 种

- MPEG (`.mpg`)—MPEG 视频格式；也称为 `.mpg`

- MOV (`.mov`)—QuickTime 视频格式

- OGG/OGV (`.ogg`)—Ogg Theora 自由许可的视频格式

- QT (`.qt`)—来自 Apple 的 QuickTime 视频格式

- WEBM (`.webm`)—Google 为 HTML5 生成的免版税音频和视频容器（如 VP8 格式）

### 在 Linux 中观看视频

开箱即用时，由于许可限制，Ubuntu 不支持任何专有视频编解码器。然而，如果你从 Ubuntu 软件仓库安装 `ubuntu-restricted-extras` 软件包，则可以获得此功能。你可以在 `https://help.ubuntu.com/community/RestrictedFormats` 了解更多信息。

你可以使用默认安装的 Totem 电影播放器观看视频文件和视频 DVD。它也可以与多种其他文件格式以及视频和音频一起使用，并且在安装 `ubuntu-restricted-extras` 软件包后特别适合你可能想要的几乎任何内容。

另一个有趣的查看器应用程序是 VLC，它可在软件仓库中使用，也适用于其他操作系统，如 Windows 和 macOS。VLC 使用自己的一套音频和视频编解码器，并支持我们遇到的任何其他媒体播放器所支持的更广泛的视频格式。如果 VLC 无法播放它，它可能无法播放。

### 个人视频录像机

将电视天线连接到计算机的最佳理由是使用视频卡和计算机作为个人视频录像机。

商业个人视频录像机 TiVo 开创了一种新趋势，使用运行在 PowerPC 上的 Linux 来录制电视节目并进行各种定制。你可以使用来自 `www.mythtv.org` 的 Myth TV 将你的计算机变成个人视频录像机，这是一款基于 Linux 的数字视频录像软件，由 `www.mythbuntu` 的 Mythbuntu 项目为 Ubuntu 用户提供了更简便的方式。你需要的一切都可在 Ubuntu 仓库中使用，并且可以轻松安装和配置，这要感谢参与这些项目的人员。

### 视频编辑
