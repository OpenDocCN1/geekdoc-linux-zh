
## 图形应用程序

我们不会在此应用上过多纠缠，但需要指出的是，用户界面同样易于使用，并提供了一种比 `cdrecord` 选项更简单（尽管灵活性较低）的替代方案。您只需使用对话框的上半部分定位要刻录的文件，将它们拖拽到对话框的下半部分（代表 CD-ROM 驱动器），然后选择 `Record`（刻录）选项即可。

![](img/b852150740856958b10aff9e8c9d2adc_199_0.png)

Red Hat Linux 中安装了大量的图形应用程序；有些作为 KDE 或 GNOME 的一部分存在。其他的一些则可以在 OpenDraw（包含在 OpenOffice 中）等应用程序套件中找到，还有一些是为操纵图像这一单一目的而编写的独立应用程序。

在本章中，我们将重点介绍随 Red Hat Linux 9 默认安装的应用程序：The GIMP、PDF Viewer、GQView 和 OpenDraw。其中大多数包含在 Graphics（图形）软件包组中（您可以在 RPM 的 Applications（应用程序）类别中找到该组），并可以在 `Main Menu | Graphics` 菜单中找到它们。

### The GIMP

GNU 图像操纵程序（或简称 GIMP，它的亲切昵称）是一款功能非常强大的软件，用于图形操纵。它既适合作为简单的绘图程序，也适合修图您拥有的照片。它可以通过众多 Linux 应用程序共通的插件技术进行扩展，也可以通过使用内部脚本接口来增强功能，该接口允许您自动化任务。

GIMP 是根据 GNU 通用公共许可证发布的，因此是自由分发的软件。它随 Red Hat Linux 9 默认安装，其网站位于 [http://www.gimp.org/](http://www.gimp.org/)，在那里您可以找到文档、支持和下载资源。

您可以通过选择 **Main Menu | Graphics | The GIMP** 或在命令行输入 `gimp` 来启动该应用程序。启动应用程序时会出现各种配置和控制窗口，您可以使用主 **GIMP** 窗口（即下图所示三个窗口中左上角的那个）的 **File | Dialogs** 菜单来控制任何特定时刻打开的对话框：

![](img/b852150740856958b10aff9e8c9d2adc_200_0.png)

如您所见，GIMP 应用程序是一个独立的窗口，包含菜单、图标工具栏和颜色信息。每幅新图像都在其独立的窗口中显示（此处未展示），该窗口拥有自己的菜单（通过右键单击图像访问）。

该应用程序比 Microsoft Paint 强大得多，其功能与 Photoshop 或 Paint Shop Pro 等应用程序更为接近。例如，它支持：

- 多种绘图工具
- 图层和通道支持
- 高级脚本和插件功能
- 渐变编辑器和混合工具
- 旋转和缩放等变形支持
- 多种文件格式

GIMP 的功能繁多，无法详细列举，再次留给您去探索该应用程序。在线文档（位于 [http://www.gimp.org/docs.html](http://www.gimp.org/docs.html)）非常详尽，并可以由其主网站（位于 [http://www.gimp.org/](http://www.gimp.org/)）上的文档作为补充。此外，网站上提供了一个庞大的资源集，涵盖图案、调色板、画笔、渐变、脚本和字体，并包含指向 The GIMP 其他重要网站的链接（例如位于 [http://registry.gimp.org/index.jsp](http://registry.gimp.org/index.jsp) 的插件注册表，以及非常有用的 **GIMP User Group** – 或 GimpForce – 位于 [http://gug.sunsite.dk/](http://gug.sunsite.dk/)）。

### GQView

GQView 是一个简单的应用程序，允许您同时查看多幅图形图像。您首先选择包含图形文件的目录，然后从左侧窗格中选择文件（其图像将在右侧窗格中显示），或使用 View（视图）菜单上可用的 Slideshow（幻灯片）功能。

要启动此应用程序，请选择 **Main Menu | Graphics | More Graphical Applications | GQView Image Viewer** 或从命令行运行 `gqview`。下图显示了该实用程序用于显示我们在第 1 章中讨论的 Red Hat Linux 安装过程中的截图：

![](img/b852150740856958b10aff9e8c9d2adc_201_0.png)

### PDF Viewer

**PDF Viewer** 是另一个简单的应用程序，其功能仅限于在屏幕上查看 PDF 文件。要启动 PDF Viewer，请选择 **Main Menu | Graphics | PDF Viewer** 或从命令行运行 `xpdf` 应用程序。要访问文件，请使用鼠标右键并从菜单中选择 **Open**（打开）。

您可以从命令行查看 PDF 文档，将其作为命令行中的第一个参数指定。如果我们想显示文件 `chapter05.pdf`，我们可以使用以下命令：

```bash
$ xpdf chapter05.pdf
```

如果您想将文档转换为 PDF 格式，有几种方法可以实现。本质上，这涉及将文档转换为 PostScript 文件格式，然后使用 Ghostscript 提供的 **PS2PDF** 转换器将其转换为 PDF 文件格式。更多信息请参阅 [http://www.pathcom.com/~kuusra/pdf_idx.htm](http://www.pathcom.com/~kuusra/pdf_idx.htm)。

### OpenDraw

**OpenDraw** 应用程序作为 OpenOffice 套件的一部分安装，类似于现在嵌入在 Microsoft Word 中的 Microsoft Draw 应用程序。它允许您使用各种 2D 和 3D 对象及形状绘制图表，对它们进行分组和上色，然后将您的图表嵌入到 OpenOffice 文档中。它还支持生成图表以及操纵图像中的文本。

## 系统应用程序

有许多其他应用程序可供使用并随 Red Hat 9 安装。新操作系统的一大乐趣在于探索所有这些应用程序。有许多东西并非默认安装，但可以在互联网上作为免费软件获取。

在本章的这一部分中，我们将讨论一些方便实用的系统实用程序和基本应用程序，它们通常不令人兴奋，但旨在让您的生活更轻松。我们要在这里考察的应用程序包括文件管理器、文件压缩工具和仿真器。

## 一个简单的文本编辑器

对于许多用户来说，主要通过基于 GUI 的应用程序来完成任务这一方式是一个巨大的吸引力。Unix 总是与命令行输入相关联，直到 X-Windows 系统提供 GUI 前端后才变得更容易使用。其中一种适合这种输入方式的应用程序是简单的文本编辑器。

当然，您可以使用 OpenWriter 等编辑器来编辑此类文档，但对于配置文件和类似文档来说，OpenWriter 等应用程序提供的格式化和功能确实显得多余。这正是 **gedit** 非常有用的地方。

**gedit** 应用程序类似于 MS Windows 中的 Notepad 或 Wordpad，是一个具有良好图形用户界面的高效文本编辑器。要启动 gedit，请选择 `Main Menu | Accessories | Text Editor`，或在命令行键入 `gedit`：

![](img/b852150740856958b10aff9e8c9d2adc_203_0.png)

## 一个文件管理应用程序

文件管理器是一种 GUI，允许您管理和导航系统和网络上的各种驱动器类型和目录结构。鉴于如今硬盘的大小（60GB 是常态）、CD-ROM 驱动器、DVD-ROM 驱动器的容量，更不用说您的局域网了，快速导航和管理这些设备文件的能力极其重要。

为了帮助您开始导航文件系统，Red Hat Linux 在主桌面上放置了一个指向您的主目录（`/home/<username>`）的链接 – 我的那个标记为 Mark’s Home。这个快捷方式会启动 Red Hat Linux 9 的首选文件管理器 – Nautilus 应用程序 – 从而允许您通过 Nautilus 的图形用户界面轻松管理您的文件和文件系统。

或者，您可以在命令行键入 `nautilus` 来启动 Nautilus。例如，要开始探索 `/usr` 目录，您可以键入：

```bash
$ nautilus /usr
```

让我们来看看 Nautilus 的 GUI：

