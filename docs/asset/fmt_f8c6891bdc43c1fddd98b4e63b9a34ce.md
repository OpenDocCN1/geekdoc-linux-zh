
通常，您想要以某种方式操作的<|message|>在您的图形应用程序或最终应用程序都无法使用的格式中。解决方案是将图像文件转换——有时需要经过几种格式。`ImageMagick`的`convert`实用程序很有用，`netpbm`工具家族也是如此。如果尚未安装，可以通过“系统设置”菜单中的“添加/删除软件”GUI 安装`ImageMagick`；`netpbm`工具默认始终已安装。

`convert`实用程序在`ImageMagick`识别的图像格式之间进行转换。颜色深度和大小也可以在转换过程中进行操作。您可以使用`ImageMagick`来附加图像、为其添加边框、标签、旋转和着色，并执行其他非常适合脚本操作的操纵。与`ImageMagick`关联的命令包括`display`、`animate`、`identify`和`import`。该应用程序支持超过130种不同的图像格式——（全部列在`ImageMagick`的man手册中）。

## 使用 ImageMagick 的 Identify 玩转

您可以使用`ImageMagick`的`identify`命令来识别图像文件的详细信息。用于`GRUB`启动加载器的欢迎闪屏图像位于`/boot/grub`中，是一张被`gzip`压缩的`.xpm`图像。如果您对该图像运行`identify`，您会发现它是一张`640×480` `xpm`图像，颜色深度为`16`位。这就是您构建自己的替换图像所需了解的全部信息。使用`GIMP`或其他图形工具，将您选择的图像裁剪或调整大小为`640×480`并将颜色深度更改为`16`位。将图像保存为`splash.xpm`，然后`gzip`生成的文件。替换原始的`Red Hat`文件，您现在就拥有了一个自定义启动图像。`identify`的使用帮助您复制原始图像的参数以符合`GRUB`的要求。

`identify`命令可用于识别未知图像文件并确定它们是否已损坏。

`netpbm`工具默认已安装，因为它们构成了图形格式操作的基础。每个图像格式的man手册都列出了相关的转换实用程序；这些实用程序的数量可以让您了解该格式的使用方式，并显示一种格式是如何建立在另一种格式之上的：

- `ppm`的man手册，便携式像素图文件格式，列出了47个与`ppm`相关的转换实用程序。这是有道理的，因为`ppm`，即便携式像素图，被认为是彩色图像文件的最低公分母。因此，它通常用作中间格式。
- `pgm`的man手册，便携式灰度图文件格式，列出了22个转换实用程序。这是有道理的，因为`pgm`是灰度图像文件的最低公分母。
- `ppm`的man手册，便携式任意图文件格式，列出了31个与其相关的转换实用程序。然而，`PNM`没有关联的格式，因为它与`ppm`、`pgm`和`pbm`协同工作。

检查`pbm`的man手册，即便携位图文件格式，发现其中没有转换工具。它是一种单色格式，是其他相关格式的基础。

## 捕获屏幕图像

你可以使用图形处理工具来捕获计算机屏幕上显示的图像。虽然这种技术被用于本书的制作，但它有更广泛的用途；“一图胜千言”这句老话是有道理的。有时展示一个例子比描述它更容易。

捕获的屏幕图像（也称为屏幕抓取或截图）可用于说明应用程序显示中的错误（例如字体问题）或过于复杂而无法手工抄写的错误对话框。你可能只是想与朋友分享你精心制作的自定义桌面配置的图像，或为你的书面文档作图。在本节中，你将学习如何为这些及其他目的捕获屏幕图像。

在使用`GNOME`桌面时，你可以利用内置的截图机制（`gnome-panel-screenshot`）。通过按下`Print Screen`键访问此工具。 （`Alt+Print Screen`仅捕获桌面上处于焦点的窗口。）捕获的图像以`.png`格式保存。

你也可以使用`Ubuntu`支持的工具从远程计算机捕获屏幕图像。`import`命令（`ImageMagick`的命令之一）被用于拍摄本书的截图；例如，使用本地计算机和局域网上的远程计算机。

首先，我们在远程计算机上运行了`$ xhost +`以允许另一台计算机访问远程机器上的`X`服务器；截图命令在我们的本地机器上运行如下：

```
$ import -window root -display 192.168.2.4:0 12fig07.jpg
```

这个实用程序使一项困难的任务变得简单，因为出版商要求截图必须在`800×600`的屏幕上完成（对于舒适工作来说太小了）以适应其印刷和生产设备。

我们也可以使用经典的`Unix`工具`xwd`来拍摄截图。命令将类似于`import`：

```
$ xwd -root -display 192.168.2.4:0 -out 12fig07.jpg
```

虽然截图可以用`GIMP`拍摄并保存为适当格式，但我们必须在该计算机上运行`GIMP`并每次捕获图像时导航菜单——`import`的远程选项非常方便。

我们没有使用`Ksnapshot`（未包含在菜单中，但可从命令行获得），因为它不支持出版商过去使用的`.pcx`格式并且必须在本地运行，但它可以轻松拍摄截图，并且是我们用于单机使用的首选工具。

## 相关 Ubuntu 命令

在为`Ubuntu`使用图形应用程序时，你将使用以下命令：

### 相机

- `gtkam`—`gPhoto2`的前端
- `kamera`—`KDE`数字相机实用程序
- `dvgrab`—使用`FireWire`连接的摄像机捕获实用程序

### 扫描仪

- `kooka`—`KDE`扫描仪应用程序
- `xsane`—扫描仪应用程序

### 图形

- `eog`—`Eye of GNOME`图像查看器
- `ImageMagick`—图像处理应用程序
- `gimp`—`GNU`图像处理程序
- `gqview`—`GNOME`图像查看器
- `kcoloredit`—`KDE`调色板编辑器
- `kiconedit`—`KDE`图标编辑器
- `kpaint`—图形应用程序
- `kuickshow`—`KDE`图像查看应用程序
- `kview`—`KDE`嵌入式图像查看器
- `netpbm-progs`—用于处理`netpbm`格式图形的工具
- `xfig`—矢量图形应用程序

### 参考

- `http://www.gimp.org`—`GIMP`（`Gnu Image Manipulation Program`）的主页。
- `http://www.gnome.org/projects/f-spot/`—`F-Spot`项目的主页。
- `http://www.linuxformat.co.uk`—`Linux Format`的网站，`Michael J Hammel`的长期`GIMP`教程所在地。
- `http://www.exif.org`—有关`EXIF`及其在数码相机中如何使用的更多信息。
- `http://www.sane-project.org`—`SANE`（`Scanner Access Now Easy`）项目的主页。
- `http://www.imagemagick.org`—`ImageMagick`的主页。
- `http://www.codeweavers.com`—流行的`Crossover Office`的所在地；如果你想尝试在`Linux`下运行`Photoshop`，则需要它。
- `http://gimp.net/tutorials/`—`GIMP`的官方教程。

# 第12章

## 使用 Ubuntu 打印

从一开始，`Ubuntu`就为来自许多不同制造商的海量打印机提供支持。在本章中，我们将了解如何将打印机连接到`Ubuntu`并使其与`Ubuntu`通信，以及`Ubuntu`用于管理打印机和打印作业的软件。

与大多数其他`Linux`发行版保持一致，`Ubuntu`使用`CUPS`（`Common UNIX Printing System`，即通用`UNIX`打印系统）来处理打印机。还支持其他系统，例如`LPRng`，但您将无法从`Ubuntu`中访问一些图形化管理工具。

### 互联网打印协议（IPP）

`CUPS`支持互联网打印协议，即`IPP`，并提供许多独特功能，例如网络打印机目录（打印机浏览）服务、加密支持以及对`PostScript Printer Description`（`.ppd`）文件的支持。

根据互联网工程任务组（`IETF`）的说法，`IPP`源于`Novell`于`1996`年提出的一项创建可在互联网上使用的打印协议的提案。此后，该系统得到了开发，已发展成为可在各种`Linux`和类`UNIX`操作平台上使用的稳定打印系统。

### Ubuntu 打印概述

`Ubuntu`的打印过滤器系统是使能够打印许多类型文档的主要引擎。该引擎的核心是`Aladdin`的`Ghostscript`解释器的`GNU GPL`版本，即`gs`客户端。系统管理员的打印机配置工具是`gnome-cups-manager`客户端。

### 本章内容

- `Ubuntu`打印概述
- 配置和管理打印服务
- 创建和配置本地打印机
- 参考

### 注意
