
# GIMP

FreeBSD 提供了多种图形程序和图像编辑程序，例如用于创建背景图案和鼠标指针的 GIMP，以及用于绘制图形和插图的 Xfig。KDE 和 GNOME 也附带简单的图像编辑程序，如 ColorPaint（Microsoft Paint 的克隆版）和 Krita（一个功能强大的 Photoshop 风格应用——是 Koffice 的一部分）。然而，GIMP 是今天开源世界中最重要且功能最强大的图形程序。

GIMP 全称为 GNU Image Manipulation Program，是一个由 GIMP 项目维护的免费可用图像编辑程序。它具有许多高级功能，如图层、过滤器、路径以及对位板输入的支持。它旨在提供 Adobe Photoshop 的免费替代方案，因此如果你熟悉 Photoshop，GIMP 的大部分功能和术语对你来说都会熟悉。不过，适应 GIMP 的布局可能需要一些时间。

GIMP 识别流行的图像格式，包括 BMP、GIF、JPEG、PNG、PCX 和 TIFF。GIMP 还可以读取 PostScript 文件，甚至读写 Photoshop 的 PSD 格式。

GIMP 可于 FreeBSD ports 集合或 graphics（图形）类别下的包中。安装 GIMP 后，你可以像本章前面提到的那样，直接从终端中使用 `gimp`。图 6.8 显示了 GIMP 的主面板，在最简单的形式下没有任何调色板。

![](img/9d11c158b3f7a22d28ac4f03f601d54f_177_0.png)

图 6.8 GIMP 主面板允许选择各种工具，以及加载和保存文件。

文件菜单（File Menu）通常是 GIMP 的起点。在这里，你可以打开现有文件、创建新文件，或者从截图或扫描仪获取图像。图 6.9 显示了 GIMP 中的打开图像对话框。它从主目录开始，你可以从中选择任何现有文件，其预览将出现在右侧面板。

![](img/9d11c158b3f7a22d28ac4f03f601d54f_178_0.png)

图 6.9 在 GIMP 中打开文件。文件浏览器内置预览和类型过滤器。

图像窗口打开，无论是创建新文件还是修改现有文件，你可以使用各种画刷和编辑工具（大部分模仿 Photoshop 版）来编辑图像。使用图层进行非破坏性编辑，使用路径制作平滑曲线并可以用选定的线条进行描边。最后，使用 GIMP 默认 XCF 格式保存文件，或使用 Photoshop 的 PSD 格式创建一个 Photoshop 可以打开并包含所有图层和路径的文件。在保存图像对话框中，只需在文件名中包含相应的扩展名即可指定输出文件类型；例如，要将图像保存为 TIFF 文件，请命名为 `image.tiff`。

# 音频应用程序

由于多年来的缺失，FreeBSD 的音频和多媒体支持在近年来变得相当良好。今天它支持各种流行的声卡，例如 Creative 的 SoundBlaster 系列插件设备，或者如 NVIDIA nForce 这样的集成主板音频芯片组。如果你拥有许多其他常见声卡之一，很有可能 FreeBSD 原生支持它。即使 FreeBSD 不对你的声具有原生支持，来自 4Front Technologies 公司的商业声卡驱动可能支持它。适用于 FreeBSD 6.x（及早期版本）的声卡驱动可以在公司网站 http://www.opensound.com 以 49 美元购买，也有免费试用版。

## 启用声音支持

在默认配置下，FreeBSD 没有激活的音频子系统。声音支持通过一组内核模块提供，每种常见的声卡类型都对应一个模块。你需要加载相应的内核模块来为系统启用声音支持。声音驱动程序都位于 `/boot/kernel/`，并且它们都以 `snd_` 为前缀。如果你无法一眼看出哪种型号的声卡匹配某个命名模糊的内核模块，请参阅 FreeBSD 在线手册中关于支持硬件的章节，地址为 http://www.freebsd.org/releases/6.0/hardware-i386.html#SOUND（请根据你的 FreeBSD 版本调整地址），将你的声卡型号与合适的内核模块进行匹配。例如，SoundBlaster Audigy 2 声卡是：

> + 提示
>
> 如果你不确定应该使用哪种驱动程序，或者在手册网站的任何支持内核模块列表中找不到你的声卡，可以尝试使用通用的 `snd_driver` 模块。这是一个元驱动，会一次性将所有驱动程序加载到内核中，可能会你的声卡工作。最好确定要使用哪种驱动——一次性加载许多内核模块是导致系统不稳定的极大方法。在加载驱动程序后使用 `/dev/sndstat` 命令来查找实际正在使用的是哪一个。

找到要使用哪种声音驱动程序后，将其添加到你的 `/boot/loader.conf` 文件中，以便其在启动时加载：

```
snd_emu10k_load="YES"
```

然后重启系统。如果你不想重启，可以使用 `kload` 立即加载内核模块：

```
# kload snd_emu10k
```

然后使用 `kload` 命令验证声音驱动程序是否已加载。

启用相应的声音驱动程序并重启后，使用 `dmesg |` 检查内核的 `dmesg` 输出。寻找指示声卡已在系统中正确检测的信息。例如，你系统上的 dmesg 输出包含以下：

```
sb0:<Creative SB AWE64> at port 0x220-0x2ff,0x330-0x331,0x388-0x38b irq 5 drq
1 is isa0
pcm1:<SB 15B 4.16> on sb0
```

此输出显示 FreeBSD 检测到了一个 SoundBlaster AWE 64，并给出了声卡占用的内存地址和 IRQ。使用 `cat /dev/sndstat` 命令查找关于你声卡的更多信息，并确保系统正确识别了它。

FreeBSD 似乎没有找到你的声音，你可能想使用 4Front 驱动程序让声音支持工作。再次，你可以在 http://www.opensound.com 获取它们。

> > 提示
>
> 为了加快启动过程，你可能选择将声卡的驱动程序编译到内核中，而不是让 FreeBSD 在每次启动时动态加载。要此操作，请向你的内核配置文件 `/usr/src/sys/i386/conf/MYKERNEL` 中添加以下两行：
>
> **device sound**
>
> **device snd_emu10k1**
>
> 在第二行中使用相应的声音驱动程序。然后按照第 8 章“内核配置”中详细的说明重新编译内核。请注意，如果你将声音支持构建到内核中，如果你购买了 4Front 声音驱动程序，可能会与它们发生冲突；如果你还没有启用它们，请确保将它们从 `/boot/loader.conf` 文件中删除。

> > 注意
>
> 通常情况下，在 FreeBSD 中，同时只有一个应用程序可以产生声音输出；如果一个应用程序打开了声音设备，你可能会收到类似 `cannot open /dev/dsp!` 的错误。如果发生这种情况，尝试使用 `fstat ; grep /dev/dsp` 来查找是否有你运行的程序（或其他用户）占用了声音输出设备。

## 使用混合器 (Mixer)

在内核声音支持加载后，设置声音的下一步是使用混合器为各种音频源和频率范围设置适当的声音输出电。你应该能够从命令行访问 FreeBSD 混合器。从 shell 提示符或终端输入命令 `mixer` 并按回车。你的系统将输出类似以下的内容：

```
Mixer vol          is currently set to 75:75
Mixer bass          is currently set to 50:50
Mixer treble        is currently set to 50:50
Mixer synth         is currently set to 75:75
Mixer pcm           is currently set to 75:75
Mixer speaker      is currently set to 75:75
Mixer line          is currently set to 75:75
Mixer mic           is currently set to 0:0
Mixer cd            is currently set to 75:75
Mixer igain         is currently set to 0:0
Mixer again         is currently set to 50:50
```

这显示了系统中的每个音频设备设置的电平（从 0 到 100 的百分比值）。用冒号分隔的数字代表每个声音组件的左、右立体声道。

列表中的大多数项目都是自言易懂的，但有几个需要更多关注：

- Mixer vol 是所有音频设备的主音。
- Mixer pcm 是播放音频的设备。它将控制 WAV 文件、MP3、Real Audio 文件等的音量。
- Mixer synth 控制合成器的音量。这通常影响 MIDI 文件。
- Mixer cd 控制音频 CD 的音量。
