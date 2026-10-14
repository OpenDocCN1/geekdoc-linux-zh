

## 18.3 使用 GIMP

GIMP
DEB: gimp1.2
gimp-manual
RPM: gimp
WWW: http://www.gimp.org/

如果你打算进行哪怕最轻微或最偶尔的图像编辑，比如对图像应用滤镜或特效、润饰、调整大小或裁剪数码照片，你都会希望花些时间熟悉 GIMP（“GNU 图像处理程序”）。

它是基于 Linux 的系统上的旗舰级图像编辑器，是一个功能全面的图像处理程序，可用于以复杂方式绘画、绘制、创建和编辑图像。你也可以用它转换图像文件、润饰和编辑照片、浏览图像集合。

GIMP 自带数百种工具、滤镜、字体和其他实用功能。以下是其核心功能的部分列表：

- 包含一整套绘图工具，包括画笔、铅笔、喷枪和克隆工具。
- 支持自定义画笔和图案。
- 包含一整套图像选择、变换和处理工具，包括渐变编辑器、颜色混合和特殊效果。
- 支持动画。
- 允许使用图层和通道。
- 支持大型图像，其大小仅受可用磁盘空间限制。
- 提供高质量字体抗锯齿。
- 支持完整的 Alpha 通道。
- 支持命令脚本。
- 允许多次撤销和重做，仅受可用磁盘空间限制。
- 允许同时打开多个图像。
- 支持所有主流图像文件格式，包括 JPEG、PNG、XPM、TIFF、TGA、MPEG、PS、PDF、PCX 和 BMP。
- 可以轻松添加 100 多个插件，以支持新的文件格式和新的特效滤镜。

GIMP 在 X Window 系统下运行，可通过运行 gimp 命令或从窗口管理器的菜单中选择它来启动。将要打开的图像文件的名称作为参数传入。

⇒ 要在 shell 提示符下于后台启动 GIMP，请输入：

```
$ gimp & [RET]
```

启动时，你作为参数传入的任何图像文件都会在各自的窗口中打开。主 GIMP 面板会在其自己的窗口中打开，如图 18-10 所示。

![](img/be7f02611e5cefde1a18c788fede22f7_468_0.png)

图 18-10：GIMP 主面板。

注意：若要了解使用 GIMP 的基础知识，请查阅《GIMP 用户手册》以及可从 GIMP 网站 [http://www.gimp.org/] 获取的其他文档和资源。你也可以在系统上安装该手册；在 Debian 系统上，它随 gimp-manual 软件包单独提供。

## 18.4 使用其他图像编辑器

Linux 上有各种各样的图像编辑应用程序——制作和编辑图像的方式与可用的工具同样多。

下表列出了一些你可能想探索的其他常用图像制作和编辑工具与应用程序。该列表并不详尽。

Aa3d
生成“ASCII 艺术”立体图。
DEB: aa3d
RPM: aa3d
WWW: http://aa-project.sourceforge.net/aa3d/

AutoTrace
将位图图像转换为矢量图形格式。
DEB: autotrace
RPM: autotrace
WWW: http://autotrace.sourceforge.net/

Barcode
生成条形码图像；支持所有商业标准。
DEB: barcode
RPM: barcode
WWW: http://tinyurl.com/36s28

Bitmap
用于位图文件的编辑器，位图文件在 X Window 系统中用于图标和平铺图案（参见技巧 4.7.3 [更改根窗口参数]，第 118 页）。
DEB: xbase-clients
RPM: XFree86-progs
WWW: http://www.xfree86.org/

Blender
广受欢迎的 3D 建模、渲染、动画和游戏设计软件。
DEB: blender
RPM: blender
WWW: http://www.blender.org/

CADUBI
绘制“ASCII 艺术”。
DEB: cadubi
WWW: http://langworth.com/CadubiProject

Drgenius
Drgeo
两个用于绘制交互式几何图形的相关工具。
DEB: drgenius
RPM: drgenius
WWW: http://ofset.sourceforge.net/drgenius/
WWW: http://ofset.sourceforge.net/drgeo/

Dia
用于绘制简单图表和示意图的工具。可将文件导出为 EPS（参见第 20 章 [PostScript]，第 451 页）。
DEB: dia
dia-common
RPM: dia
WWW: http://www.gnome.org/projects/dia/

Effectv
通过各种特殊效果处理电视输入。
DEB: effectv

Electric
用于设计电路图、原理图等图像的 CAD 系统。
DEB: electric
RPM: electric
WWW: http://tinyurl.com/3yzbf

Figurine
矢量图形编辑器，旨在比经典的 Xfig（见下文）更容易上手，同时保持与 Xfig 的文件格式兼容。
DEB: figurine
RPM: figurine
WWW: http://figurine.sourceforge.net/

Findimagedupes
对两个图像文件执行“视觉差异比较”；给定一组文件，它会找出相似或重复的图像。
DEB: findimagedupes
WWW: http://www.kudla.org/raindog/perl/

Gnuplot
功能强大的非交互式函数绘图工具。根据数据文件和公式生成图表和图形（参见技巧 29.8 [绘制数据]，第 575 页）。
DEB: gnuplot
RPM: gnuplot
WWW: http://www.gnuplot.info/

Innovation3d
3D 建模程序。
DEB: innovation3d
innovation3d-plugins
WWW: http://innovation3d.sourceforge.net/

