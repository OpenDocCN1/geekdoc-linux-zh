
# 在 vi 中复制、剪切和粘贴文本

要在 vi 中将文本复制到缓冲区，请使用 `y` 命令。`y` 是 yank（提取/粘贴）的缩写，它基本上将文本“提取”到缓冲区。表 6.8 展示了 yank 命令的各种用法。

### 表 6.8 vi 中的 yank 命令

| 命令 | 操作 |
|---|---|
| `yw` | 将光标当前所在的单词提取到缓冲区。 |
| `y$` | 从当前光标位置提取到当前行末尾的文本到缓冲区。 |
| `yy` | 将整个当前行提取到缓冲区。 |
| `nyy` | 这里，`n` 是你希望提取到缓冲区的行数。例如，`5yy` 会将当前行以及接下来的四行提取到缓冲区。 |

一旦你将文本提取到缓冲区，你就可以通过移动到文档中的正确位置，然后使用 `p` 或 `P` 命令来“放置”（粘贴）文本，将其粘贴到文档的任何位置。`p` 命令将文本放置在光标之后，而 `P` 命令将文本放置在光标之前。在你“放置”文本后，它会继续保留在缓冲区中。你可以再次使用 `p` 或 `P` 将文本复制到文档中的其他位置。

如果你想剪切而不是复制，请使用其中一个删除命令。例如，`5dd` 将剪切当前行以及接下来的四行。然后可以使用 `p` 或 `P` 将它们粘贴到文档中的另一个位置。

> **注意**
> vi 仅存储最后一次提取或删除的文本。换句话说，如果你使用 `dd` 删除一行文本，然后后来使用 `y` 复制一行文本，那么 `dd` 操作的文本将被 `yy` 操作的文本替换。这意味着 `dd` 操作的文本将不再可用，而且你将无法撤销删除操作。

vi 还有许多更强大的功能，由于篇幅有限，这里无法全面介绍。一旦你熟悉了 vi，你就会发现它是一个非常强大的编辑器，提供了一种快速编辑文档的方式。如果你想了解更多关于 vi 的信息，有一些相关书籍可供参考，包括 *Learning the vi Editor*（学习 vi 编辑器）和 *vi Editor Pocket Reference*（vi 编辑器袖珍参考指南），这两本书均可从 O'Reilly 出版社获得。

## 使用 GIMP 创建图形和编辑图像

FreeBSD 提供了多种图形程序和图像编辑程序，包括用于图像编辑的 GIMP 和用于绘制图形和插图的 Xfig。GIMP 在 FreeBSD 的 ports 集合中免费提供。

GIMP 代表 GNU 图像操作程序（GNU Image Manipulation Program）。它是一个免费且开源的图像编辑程序，由 GNU 项目维护。它具有许多高级功能，如图层和滤镜。如果你之前使用过 Adobe Photoshop 这样的程序，GIMP 的大多数功能对你来说都会很熟悉。不过，熟悉 GIMP 的布局可能需要一些时间。

GIMP 支持大多数图像格式，包括 BMP、GIF、JPEG、PNG、PCX 和 TIFF。GIMP 还可以读取 PostScript 文件。

GIMP 位于 FreeBSD ports 集合的 graphics 目录下。安装 GIMP 后，你可以简单地在 X-Windows 终端中输入 `gimp`，或者使用“运行”对话框并输入 `gimp`。有关如何在 X-Windows 内部启动应用程序的更多信息，请参阅第 5 章“使用 X-Windows”。

图 6.5 展示了 GIMP 的主控制面板。

![](img/48eec858cce7dfb89da36a4d40b7daf3_144_0.png)

**图 6.5** GIMP 的主控制面板允许你选择 GIMP 中可用的各种工具，以及加载和保存文件。

菜单栏中的“文件”选项通常是使用 GIMP 的起点。在这里，你可以打开现有文件、创建新文件或获取图像——无论来自屏幕截图还是来自已安装的受支持的扫描仪。

图 6.6 展示了 GIMP 中的“文件，打开”对话框。

> **提示**
> 从 Windows 图像编辑软件转换到 GIMP 的用户面临的主要障碍在于，GIMP 的大部分编辑功能是通过右键点击图像窗口来访问的。在使用 GIMP 时请记住这一点，转换过程会顺利得多。

![](img/48eec858cce7dfb89da36a4d40b7daf3_145_0.png)

图 6.6 在 GIMP 中打开文件。请注意，其中内置了一个简单的文件管理器。

## 使用多媒体

FreeBSD 的多媒体支持在相当短的时间内变得非常好。如果你拥有任何一张常见的声卡，FreeBSD 很可能原生支持它。即使 FreeBSD 不原生支持你的声卡，一家名为 4Front Technologies 的公司提供的商业声卡驱动程序可能支持你的声卡。如果你想了解商业驱动程序，4Front 声卡驱动程序的网站位于 www.opensound.com。有免费试用版本可用，因此你可以在购买前尝试这些驱动程序。

### 检查声音支持

在使用本节介绍的任何多媒体应用程序之前，你需要确保 FreeBSD 中有声音支持可用。

要查看是否加载了 PCM 驱动程序，请检查内核配置文件中 `device pcm` 这一行。如果存在该行，则说明声音支持已编译到内核中。如果你没有构建自定义内核，内核配置文件将位于 `/sys/1386/conf/GENERIC`。如果该行不存在，你需要添加它并重新构建内核。这并没有听起来那么可怕。有关重新构建内核的信息，请参阅第 16 章“内核配置”。

一旦你确认内核包含 PCM 驱动程序，请输入 `dmesg | more` 以检查内核的 dmesg 输出。查找指示声卡在系统启动时已被正确检测到的信息。例如，我系统中的 dmesg 输出包含以下行：

```
sbc0: <Creative SB AWE64> at port 0x220-0x22f,0x330-0x331,0x388-0x38b irq 5 drq 1,5 on isa0
pcm1: <SB16 DSP 4.16> on sbc0
```

此输出显示 FreeBSD 检测到了 SoundBlaster AWE 64，并给出了声卡所在的地址。

如果 FreeBSD 似乎找不到你的声卡，你可能想尝试使用 4Front 声卡驱动程序来使声音工作。再次提醒，可以在 www.opensound.com 获取它们。

请注意，如果你决定尝试使用 4Front 驱动程序，你可能需要从内核配置文件中删除或注释掉 `device pcm` 行，然后重新构建内核。否则，你可能会遇到内核声音驱动程序与 4Front 驱动程序冲突的问题。

有关内核配置和内核构建的完整说明，请参阅第 16 章。

## 混音器

一旦设备链接已创建，你应该能够从命令行访问 FreeBSD 混音器。从 shell 提示符或 X-终端窗口中，输入命令 **mixer** 并按 Enter。你的系统将输出类似以下内容：

```
Mixer vol    is currently set to  75:75
Mixer bass   is currently set to  50:50
Mixer treble is currently set to  50:50
Mixer synth  is currently set to  75:75
Mixer pcm    is currently set to  75:75
Mixer speaker is currently set to  75:75
Mixer line   is currently set to  75:75
Mixer mic    is currently set to  0:0
Mixer cd     is currently set to  75:75
Mixer igain  is currently set to  0:0
Mixer ogain  is currently set to  50:50
```

这显示了系统中每个音频设备设置的电平（取值范围为 0 到 100 的百分比值）。正如你预期的那样，冒号左边的数字表示左音频通道的电平，冒号右边的数字表示右音频通道的电平。

列表中的大多数项目都是不言自明的，但其中一些项目值得更多关注：

- 混音器 vol 是所有音频设备的主音量。
- 混音器 pcm 是大多数音频播放所使用的设备。这将控制 WAV 文件、MP3、Real Audio 文件等的音量。

