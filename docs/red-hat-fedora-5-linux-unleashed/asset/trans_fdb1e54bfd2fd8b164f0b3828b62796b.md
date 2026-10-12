
## USB 扫描仪配置成功但过程曲折

由于失败有时比成功更具教育意义，在此书的前几版中，我们尝试配置一款不被支持的 USB 扫描仪：佳能 N650U。随着随 Fedora 发布的 SANE 版本更新，现在该扫描仪已得到支持，并能被自动检测！

然而，这里列出了当该扫描仪在 Linux 中无法正常工作、我们手动检测和配置它时所使用的步骤：

首先，连接扫描仪。对于这款 USB 扫描仪，请查看以下命令的输出：

```
# cat /proc/bus/usb/devices/
```

（在此处截取了输出内容，仅显示扫描仪相关信息。您也可以使用 `lsusb` 命令。）

```
T:  Bus=01 Lev=01 Prnt=01 Port=00 Cnt=01 Dev#=  2 Spd=12  MxCh=
D:  Ver= 1.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS=  8 #Cfgs=   1
P:  Vendor=04a9  ProdID=2206  Rev= 1.00
S:  Manufacturer=Canon
S:  Product=CanoScan
C:*  #Ifs=  1 Cfg#=  1 Atr=80  MxPwr=500mA
I:  If#=  0 Alt= 0 #EPs=  3 Cls=ff(vend.)  Sub=00  Prot=ff  Driver=(none)
E:  Ad=81(I)  Atr=03(Int.)  MxPS=   1 Ivl=16ms
E:  Ad=82(I)  Atr=02(Bulk)  MxPS=  64 Ivl=0ms
E:  Ad=03(O)  Atr=02(Bulk)  MxPS=  64 Ivl=0ms
```

第七行末尾的 "Driver=(none)" 表明设备未能在查找表中找到。由于我们现在拥有了“魔法”厂商 ID 和设备 ID，我们可以尝试手动加载驱动程序：

```
# /sbin/modprobe  scanner  vendor=0x04a9  product=0x2206
```

现在，之前 `cat /proc/bus/usb/devices` 命令的输出显示扫描仪设备驱动程序已与我们的扫描仪关联：

```
I:  If#=  0 Alt= 0 #EPs=  3 Cls=ff(vend.)  Sub=00  Prot=ff  Driver=usbscanner
```

并且 Kooka 和 Xsane 应用程序现在能够识别该扫描仪。

## 图形格式处理

图像文件格式的开发旨在服务于特定的技术目的（例如无损压缩，即在不牺牲图像质量的情况下减小文件大小），或者出于竞争原因满足对专有格式的需求。许多文件格式受到一项或多项专利的保护。例如，GIF 格式在开源社区中已失宠，因为专利持有人直到最近才决定停止执行其专利权。

如果您希望查看或处理图像，需要识别文件格式以选择正确的工具来处理该图像。文件扩展名是文件格式的第一个指示标志。Red Hat 附带的应用程序支持的图形图像格式包括：

- .bmp—位图图形，常用于 Microsoft Windows
- .cgm—计算机图形元文件
- .g3—CCITT Group 3 FAX 图像
- .gif—CompuServe 图形交换格式
- .ico—Microsoft Windows 图标图像
- .jpg—联合图像专家组
- .mng—多图像网络图形图像
- .pbm—可移植位图文件格式
- .pcx—IBM Paintbrush
- .pgm—可移植灰度图文件格式
- .png—可移植网络图形
- .pnm—可移植任意图
- .ppm—可移植像素图文件格式
- .rgb—原始红色、绿色和蓝色采样
- .rs—Sun 光栅图像
- .svg—可缩放矢量图形
- .tif—带标记图像文件格式
- .xbm—X 位图图像
- .xpm—X 像素图图像，常用于 Linux 图标图像

ImageMagick 的手册页中包含一个广泛的图像文件扩展名列表，ImageMagick 是一款卓越的应用程序，随 Fedora 附带提供，您将在本章后续部分进一步了解它。

> Fedora 包含数十个图形转换程序，几乎不存在任何无法在 Linux 中处理的图形文件格式。这些命令可用于 Perl 脚本、shell 脚本或命令行管道，以支持多种类型的复杂格式转换和图像处理任务。请参阅 ppm、pbm、pnm 和 pgm 系列命令的手册页。另请参阅 convert 命令的手册页，它是 ImageMagick 工具套件中一组功能极其强大的程序的一部分。

通常，您希望以某种方式处理的文件处于一种格式，该格式既不被您的图形应用程序使用，也不被最终应用程序使用。解决方案是转换图像文件——有时需要通过几种格式进行转换。ImageMagick 的 `convert` 实用程序非常有用，`netpbm` 系列实用程序也是如此。如果尚未安装，ImageMagick 可以通过系统设置菜单中的“添加/移除软件”GUI 进行安装；`netpbm` 工具默认总是已安装的。

`convert` 实用程序在 ImageMagick 识别的图像格式之间进行转换。在转换过程中，还可以操作颜色深度和大小。您可以使用 ImageMagick 追加图像、添加边框和标签、旋转和着色，以及执行其他适合脚本化的操作。与 ImageMagick 相关的命令包括 `display`、`animate`、`identify` 和 `import`。该应用程序支持 130 多种不同的图像格式——所有这些都列在 ImageMagick 的手册页中。

### 玩转 IMAGEMAGICK 的 identify

> 您可以使用 ImageMagick 的 `identify` 命令来识别图像文件的详细信息。GRUB 引导加载器使用的欢迎闪屏图像位于 `/boot/grub`，是一个压缩后的 `.xpm` 图像。如果您对该图像运行 `identify`，您将发现它是一个 640x480 的 xpm 图像，具有 16 位颜色深度。这就足以让您构建一个替换图像。使用 GIMP 或其他图形工具，将您选定的图像裁剪或调整大小为 640×480，并将颜色深度更改为 16 位。将图像保存为 `splash.xpm`，然后对生成的文件进行 `gzip` 压缩。替换原始的 `Red Hat` 文件，您现在就拥有了一个自定义的启动图像。`identify` 的使用有助于您复制原始图像的参数以符合 GRUB 的要求。
>
> `identify` 命令对于识别未知图像文件以及确定其是否损坏非常有用。

`netpbm` 工具默认安装，因为它们构成了图形格式处理的基础。每种图像格式的手册页都列出了相关的转换实用程序；这些实用程序的数量让您对该格式的使用方式有所了解，并展示了一种格式如何建立在另一种格式之上：

- `ppm`（可移植像素图文件格式）的手册页列出了 47 个与 `ppm` 相关的转换实用程序。这是合理的，因为 `ppm`，即 `portable pixmap`，被认为是彩色图像文件的最小公分母。因此，它通常用作中间格式。
- `pgm`（可移植灰度图文件格式）的手册页列出了 22 个转换实用程序。这是合理的，因为 `pgm` 是灰度图像文件的最小公分母。
- `pbm`（可移植**位**图文件格式）的手册页列出了 31 个与其相关的转换实用程序。然而，`pbm` 没有与之关联的独立格式名称，因为它与 `ppm`、`pgm` 和 **pnm** 协同工作。*(注：原文此处 OCR 有误，"anitmap" 已根据上下文修正为 "bitmap"；列表末尾的 "pbm" 在原书中可能是 "pnm" 的笔误，但结构保持不变，仅修正了明显的拼写错误 "anitmap" -> "bitmap"。实际上，查看 OCR 文本："pbm, the portable anitmap file format" -> "pbm" 代表 Portable **B**itmap，但文本写作 "anitmap"。前面的要点讨论了 PPM (Pixmap) 和 PGM (Graymap)。PBM 是 Bitmap。OCR 文本说 "portable anitmap"。应该是 "portable bitmap"。我将 "anitmap" 更正为 "bitmap"。最后一部分 "operates in concert with ppm, pgm, and pbm" 很可能是原书中 "pnm" 的笔误。我会将 "anitmap" 更正为 "bitmap"，因为这是 "bitmap" 的明显 OCR 错误 (b vs a/n)。等待，"pbm" 是 Portable B-i-t-m-a-p。文本说 "anitmap"。这是错误的。我将把 "anitmap" 改为 "bitmap"。)*

查看 pnm（可任意图文件格式）的手册页，未列出转换实用程序。它是一种单色格式，作为其他相关格式的基础。

## 捕获屏幕图像

您可以使用图形处理工具来捕获显示在计算机屏幕上的图像。虽然这项技术用于本书的制作，但它的用途更广；俗话说“一图胜千言”并非虚言。有时展示一个例子比描述它更容易。

捕获的屏幕图像（也称为*屏幕截图*或*screenshot*）可用于说明应用程序显示中的错误（例如字体问题）或复杂到无法手动复制的错误对话框。您可能只是希望与朋友分享您精心制作的自定义桌面配置的图像，或者用来说明您的书面文档。在本节中，您将学习如何捕获屏幕图像以用于这些和其他目的。

在使用 Gnome 桌面时，您可以利用内置的屏幕截图机制（`gnome-panel-screenshot`）。通过按下 Print Screen 键访问此工具。（Alt+Print Screen 仅对桌面上具有焦点的窗口进行截图。）捕获的图像以 .png 格式保存。

您还可以使用 Xserver 支持的工具从远程计算机捕获屏幕图像。`import` 命令（ImageMagick 命令之一）用于截取本书的屏幕截图；例如，使用本地计算机和局域网上的远程计算机。

首先，我们在远程计算机上运行 `$ xhost +` 以允许另一台计算机访问远程机器上的 X 服务器；截取屏幕截图的命令在我们的本地机器上像这样运行：

```
$ import -window root -display 192.168.2.4:0 12fig07.jpg
```

该实用程序简化了一项困难的任务，因为出版商要求从 800x600 屏幕（太小，操作起来不舒服）进行屏幕截图，以适应其印刷和生产设备。

我们也可以使用经典的 UNIX 工具 `xwd` 来截取屏幕截图。该命令看起来与 `import` 类似：

```
$ xwd -root -display 192.168.2.4:0 -out 12fig07.jpg
```

虽然可以使用 GIMP 截取屏幕截图并以适当格式保存，但我们必须在该计算机上运行 GIMP，并在每次捕获图像时导航菜单——`import` 的远程选项非常方便。

