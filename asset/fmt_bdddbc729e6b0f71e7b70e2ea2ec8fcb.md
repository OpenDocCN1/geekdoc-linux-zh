
你可以使用`cdrecord`命令的`--blank`选项来擦除 CDRW 光盘。`cdrecord`命令的选项比`mkisofs`少，但它提供了`-multi`选项，允许你制作多会话 CD。多会话 CD 允许你写入数据轨道、退出，稍后向 CD 中添加更多数据。单会话 CD 只能写入一次；任何剩余的 CD 容量都会被浪费。可以在`cdrecord`的 man 页面阅读有关其他选项。

CD 介质的当前容量为 700MB 数据或 80 分钟音乐。（有 800MB/90 分钟的 CD，但很罕见）。某些 CD 可以“超刻录”，即刻录到超过标准容量的容量。如果你的 CD-RW 驱动器支持，`cdrecord`命令和图形程序能够进行超刻录。你可以在 https://www.cdmediaworld.com/hardware/cdrom/cd_oversize.shtml 了解更多关于超刻录 CD 的信息。

## 从命令行创建 DVD

DVD 有几种相互竞争的格式，如下：

- DVD+R
- DVD-R
- DVD+RW
- DVD-RW

+ 和 - 格式之间的差异主要与数据调制到 DVD 自身的方式有关，+ 格式在缓冲欠载恢复（buffer underrun recovery）方面具有优势。这种实现方式会影响新创建 DVD 在任何 DVD 播放器上的播放性。DVD+ 格式在有划痕或干燥介质上记录时也有一些优势。大多数驱动器都支持 DVD+ 格式。与任何技术一样，实际情况可能有所异。

我们关注 DVD+RW 驱动器，因为大多数都支持标准。Ubuntu 提供的软件也支持写入到 DVD-R/W（可重写）介质。在尝试使用`dvdrw-tools`之前，复阅 DVD+/+/-R[W] http://fy.chalmers.se/~linux/DVD+RW/ 对你很有帮助，你需要该工具来启用 DVD 创建（也称为刻带）以及`cdrtools`软件包。你可以忽略 HOWTO 中关于内核补丁和编译这些工具的讨论。

## 提示

- DVD 介质的 4.7GB 大小是按每 GB 1000 兆字节计算的，而不是使用更传统但并不完全准确的每 GB 1024 兆字节（近似给定的 GB），因此当实际格式化后的容量（约 4.4GB）低于预期时，不要感到惊讶。关于这种差异和修正必要性的良好解释可以在 http://en.wikipedia.org/wiki/Gibibyte 获取。大多数硬盘制造商也进行了这种切换。`dvdrw-tools`不允许你超过光盘的容量。

你需要安装`dvdrw-tools`（以及`cdrtools`软件包）。`dvdrw-tools`软件包包含`growisofs`应用（作为`mkisosf`的前端）和 DVD 格式化工具。

你可以用两种方式使用 DVD 介质记录数据。第一种与记录会话 CD 的类似，第二种方法是使用包写入（packet writing）将数据作为真正的文件系统记录。

## 会话写入

要在会话中记录数据，你需要两个阶段的过程：

1. 首先使用`dvd+rw-format /dev/scd0`格式化磁盘（仅在第一次使用磁盘时需要，`/dev/scd0`是你的驱动器的设备名称）。

2. **使用`growisofs -Z /dev/scd0 R -J /your_files`向磁盘写入你的数据。**

`growisofs`命令仅是将数据流传输到磁盘。对于后续会话，请使用`-M`参数而不是`-Z`。`-Z`参数仅用于初始会话记录；如果你在已使用的磁盘上使用`-Z`参数，它将擦除现有文件。

## 注意

某些 DVD 是预格式化的；在使用它们时再次进行格式化可能会导致 DVD 无用。请务必仔细阅读 DVD 的包装，确保你不会再次制作一张“废光片”。

## 提示

写入至少 1GB 的第一个会话有助于保持你记录的数据与其他光驱驱动器的兼容性。DVD 播放器通过尝试从磁盘上的特定位置读取数据来完成校准；你需要在那里有数据，驱动器才能读取并进行自我校准。

此外，由于 Linux 中 ISO9660 文件系统的局限性，不要启动多会话 DVD 的新会话并创建一个跨越 4GB 边界的目录路径。如果这样做会导致用于指向文件的偏移量“回绕”并指向错误的文件。

## 包写入

包写入将 CD 或 DVD 视为硬盘，你在硬盘上创建一个文件系统（如 ext3）并格式化磁盘，然后像写入传统硬盘一样随机写入。这种方法虽然在基于 Windows 的计算机上很常见，但在 Linux 上长期以来一直被认为是实验性的，而且从未由于 USB 使用过。

## 提示

许多 DVD 是预格式化的。然而在 Linux 中，内核仅支持特定的卡。如果你的计算机中有支持的卡，它可能在安装期间被检测到。如果你添加了它，硬件检测工具应该能检测到它。你可以手动进行配置，但由于 Ubuntu 内核尝试将所有可用硬件编译为模块，这样做并没有太大用处。

首先，要确定卡使用的芯片组，请使用`lspci`命令列出 PCI 设备信息，找到显卡列表，并查找卡使用的芯片组。例如，一台计算机的`lspci`输出所示。

```
Bt878 Audio Capture (rev 02)
00:0d.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8029 (AS)
00:0f.0 FireWire (IEEE 1394): Texas Instruments TSB12LV23 IEEE-1394 Controller
00:11.0 Network controller: Standard Microsystems Corp [SMC] SMC2602W EZConnect
01:05.0 VGA compatible controller: NVIDIA Corporation NV15 [GeForce2 Ti] (rev a4)
```

这里列出了多媒体视频控制器和多媒体控制器，表明这块电视板使用了 Brooktree Bt878 视频采集芯片和 Brooktree Bt878 音频采集芯片。此卡使用了 Bt878 芯片组。你的结果将取决于电脑拥有的显卡和芯片组。这似乎是一个 All-in-Wonder VE（也称为 ATI TV-Wonder）。VE 代表 Value Edge（价值边缘）；因此，卡上没有 TV 输出控制器，也没有收音机；真是划算！

然后，你需要确定需要哪个模块，可能使用 Google 搜索“Bt878 linux”或“Bt878 Ubuntu”，并开始阅读文档。你想寻找官方页面而不是博客文章。最后，你需要将一些信息输入`/etc/modules.conf`。此文件在默认的 Ubuntu 安装中并不存在，但可以根据需要创建，并在启动时读取。然后，你通过`sudo depmod -a 模块名称`计算模块依赖关系以加载模块。再次强调，这在 Ubuntu 中是没有必要的，因为如果它对他们可用，他们就会提供给你，无需你进行额外工作，系统会自动扫描启动时应该加载哪些内容并进行拉取。

Ubuntu 识别多种视频格式。然而，由 MPEG、Apple 和微软创建的格式占据主地位。视频格式的核心是编码器——编码器和解码器。这些编码器通常是专有的，但也存在免费的编码器。以下是最常见的视频格式及其相关扩展名的列表，尽管还有许多格式：

- AVI (.avi)—Windows 音频格式
- FLV (.flv)—用于 Adobe Flash，支持 H.264 等其他格式
- MPEG (.mpeg)—MPEG 视频格式；也称为 mpg
- MOV (.mov)—另一个 QuickTime 视频格式
- OGV/OGG (.ogg/.ogg)—Ogg Theora 免费许可视频格式
- QT (.qt)—来自 Apple 的 QuickTime 视频格式
- WEBM (.webm)—Google 为 HTML5 设计的免版税音视频封装格式

## 在 Linux 中观看视频

在默认情况下，由于许可限制，Ubuntu 不支持任何专有编码器。然而，如果你从 Ubuntu 仓库安装了`ubuntu-restricted-extras`包，就可以获得此功能。你可以在 https://help.ubuntu.com/restrictedFormats 了解更多信息。

你可以使用 Totem 播放器（图 6.11）观看视频文件和 DVD，该播放器是默认安装的。它也可以用于几种其他格式的视频和音频，并且特别适合你在安装了`ubuntu-restricted-extras`包后可能使用的几乎任何内容。

![](img/cdb9271985389cacf21d88a58ef49e_187_0.png)

图 6.11 Totem 播放器支持大多数视频和音频格式。

## Adobe Flash
