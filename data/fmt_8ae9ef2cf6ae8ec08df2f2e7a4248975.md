
在这个示例中，在更改上述参数后，64 MB 的缓冲磁盘读取时间从 19.31 秒缩短到了 2.2 秒。现在的播放体验会顺畅得多。

- `xine` 播放特定媒体时，如果出现“no input plug-in”（无输入插件）的消息，意味着你正尝试播放的格式不受支持，或者它需要额外的插件（例如播放 DVD 的情况）。如果信息是“broken file”（损坏的文件），该文件可能是某种受支持格式的私有版本。例如，我有一个 QuickTime 视频播放失败，因为它需要 `SVQ` 解码器（目前 Linux 下不支持），尽管其他 QuickFiles 播放正常。

## 第二部分：运行 Linux 桌面系统

### 使用 Totem 电影播放器

`Totem` 电影播放器 (`www.gnome.org/projects/totem`) 随 GNOME 桌面环境一起提供。在大多数 GNOME 桌中，`Totem` 可以播放带有 Ogg 音频的 Theta 视频。`Totem` 使用 `GStreamer` 框架 (`http://gstreamfreedesktop.org`)，它可以利用任何与 `GStreamer` 兼容的视频解码器。特别是，你可以从 `www.fluendo.com` 购买免费或付费的解码器，以便用 `Totem` 播放各种商业音频/视频格式。

`Totem` 还支持 x 后端，允许它播放广泛的视频内容（换句话说，任何支持的视频都可以播放）。要播放商业 DVD 电影，你需要安装可用的 `totem-x` 软件包（对于 Fedora，它在 `rpmfus.org` 仓库中）。从该仓库中，你可以添加 `libvdccds`、`libdvdplay` 和 `x-lib-nonfree` 包（前提是你在所在地区软件是合法的）。运行 `totem-x` 命令而不是 `Totem` 来播放电影。

除了你预期电影播放器常见的控制功能（播放、暂停、快进、后退等）外，`Totem` 还允许你创建播放列表、截取当前帧快以及调整音量。你可以更改偏好、添加私有插件、选择视频设备并平衡色彩。图 4-10 显示了 `Totem` 窗口的示例。

## 图 4-10

在 GNOME 桌面上使用 `Totem` 播放电影。

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_147_0.png)

## 使用数码相机

通过大多数带有 GNOME 桌面的 Linux 系统内置的 `GNOME Volume Manager`，从数码相机获取图像可以像任何桌面操作系统一样简单。对于大多数可以连接到计算机 USB 端口的数码相机，只需将相机插入 USB 端口（并将相机设置为发送和接收），`GNOME Volume Manager` 就会：

- 立即像你想从相机下载图像一样响应。
- 运行 `gThumb` 图像查看器和浏览器程序，你就可以查看、处理和下载数码相机的内容了。

尽管 `GNOME Volume Manager` 在图像查看器中打开了相机的内容，但你可以像对待硬盘或优 盘上的存储区域一样对待相机中的存储区域。我还会描述如何使用你的相机来存储其他数据。

## 在 gThumb 中显示图像

`GNOME Volume Manager` 会统计你的 USB 相机内容，将相机的内存视为任何文件存储设备。当我尝试奥洋（Olympus）数码相机时，我的图像可以在 `/media/usdisk/dcim/100olym` 目录下找到。图 4-11 显示了 `gthumb-import` 窗口显示数码相机图像的示例。

> 图 4-11
使用 `gThumb` 查看器从数码相机下载图像。

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_148_0.png)

### 使用数码相机作为存储设备

正如在带有 GNOME 桌面的大多数 Linux 系统中配备的 `GNOME Volume Manager` 那所示，从数码相机获取图像可以像任何桌面操作系统一样简单。

## 文字与图像处理

## 本章内容

编写文档一直是桌面型电脑的核心功能。在桌面出版应用方面，Linux 系统已经稳步地赶上了 Mac 和 Windows 系统。现在，几乎你所对文档写作、布局和出版（包括纸质版和 Web 版）所预期的每种功能，在 Linux 系统中都可以实现。

- Linux 下的桌面出版
- 使用文字处理器
- 使用 Scribus 进行页面布局
- 将文档从 Windows 迁移到 Linux
- 图像处理
- 使用 Inkscape 制作矢量图形
- 使用扫描仪
- 在 Web 上发布

本章介绍了流行的 Linux 办公套件（such如 `OpenOffice.org` 和 `OpenOffice`），它们可用于创建文档、演示文稿和电子表格。`Scribus` 是一个用于页面布局的绝佳应用程序。在图像处理方面，我介绍了 GNU 图像操纵程序（the `GIMP`）以及几款查看器（如 `Gview` 和 `Eye of GNOME`）。对于矢量图形处理，我描述了 `Inkscape` 矢量图形编辑器。

## 第二部分：运行 Linux 桌面

## Linux 桌面的桌面出版

无论你是在写信、备忘录还是书籍，你通常都从文字处理器开始。如果你的电脑性能不高，你可能会从一个简单的文本编辑器或像 `AbiWord` 这样要求较低的文字处理器开始。然而，Linux 用户通常从 `OpenOffice.org Writer` 开始。

## 使用文本编辑器和记事本

- **GNOME 文本编辑器 (`gedit`)**——从 GNOME 桌面，选择“应用程序 > 辅助工具 > 文本编辑器”。
- **KDE 文本编辑器 (`kwrite`)**——在 KDE 中，该程序是默认文本编辑器。
- **便签本 (`tomboy`)**——不同的笔记记录应用程序包括 `KNotes`（用于 KDE）和 `Tomboy`（用于 GNOME）。

## 使用文字处理器

`OpenOffice.org` 是一个强大的开源办公套件，提供下载并适用于 Linux 发行版。`OpenOffice.org` 基于 Sun 微型系统的 `StarOffice` 生产力套件，包含一个文字处理器、电子表格、演示文稿管理器和其他个人生产力工具。

## 第 5 章：文字与图像

![图 5-1 文字与图像](img/5-1.png)

## OpenOffice 套件

在办公、教育和政府领域，一些人认为它是 Microsoft 统治地位的重大威胁。在 Linux 上，许多发行版包含了 `OpenOffice.org`。此外，在 Fedora 上，你可以安装 `openoffice.org-calc`、`openoffice.org-draw`、`openoffice.org-impress`、`openoffice.org-writer` 以及 `openoffice.org-math`。

## 第二部分：运行 Linux 桌面

## 注意事项

在编写本文时，`OpenOffice` 的最新版本为 3.1。

`OpenOffice.org` 与 `StarOffice` 共享内核，包含以下办公应用程序：

- `Writer`——文字处理应用程序
- `Calc`——电子表格应用程序
- `Draw`——绘图应用程序
- `Math`——计算程序
- `Impress`——演示文稿应用程序

## 第5 章：处理文字和图像

要打开 `OpenOffice.org` 应用程序，请选择应用程序菜单。

### 图 5-2

在 `OpenOffice.org Writer` 中的 Microsoft Word 文档或开放文档格式。

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_156_0.png)

## 其他文字处理器

- `StarOffice`—StarOffice 生产力套件包含文字处理、电子表格、演示文稿、电子邮件、新闻、图表和图形应用程序。
- `AbiWord`—`AbiWord` 处理器 (`abword` 命令) 是由 `AbiSource` 项目 (`www.abisource.com`) 的非商业软件。
- `KOffice`—Office 软件包包含一组用于 KDE 桌面的办公生产力应用程序。

## 使用 StarOffice

`StarOffice` 来自 `Sun Microsystems, Inc.` (`www.sun.com/software/staroffice`)，是一款运行在 Linux、UNIX 和 Windows 系统上的产品。

## 使用 AbiWord

`AbiWord` 处理器是来自 `AbiSource` 项目 (`www.abisource.com`) 的一个优秀的免费的文字处理器。

## 使用 KOffice

`K` 桌面环境 `KDE` 提供了一个包含数百个其他程序的办公套件。`KOffice` 软件包包含了你在集成式办公套件中预期的基本应用程序：文字处理器 (`KWord`)、电子表格 (`KSpread`)、演示文稿创建器 (`KPresenter`) 和绘图程序 (`KChart`)。

### 图 5-3

`KOffice` 工作空间允许你同时处理多个 KDE 应用程序。

# 第5 章：处理文字与图像

## 从 Windows 迁移文档

## 第二部分：运行 Linux 桌面

## 备注

Word 2007 文件的默认格式是 `.docx`——Open XML。

## 注意事项

在从 Microsoft Office 进行任何批量转换之前，请确保你需要使用的文件与你所选择的新 Office 套件兼容。

## 转换文档

| 工具 | 转换对象 | 目标 |
| :--- | :--- | :--- |
| `dos2unix` | DOS 文本文件 | UNIX (Linux) 文本文件 |
| `fax2ps` | 传真文档 | PostScript (level 2) |
| `pdf2ps` | PDF 文件 | PostScript 文件 |
| `ps2pdf` | PostScript 文件 | 便携式格式 (PDF) |

许多图形应用程序（如 `GIMP`）还可以通过“另存为”功能将图像保存为多种格式（BMP、JPEG、PNG、TIFF 等）。

# 理解 SGML 和 XML

标准通用标记语言 (`SGML`) 创建是为了提供一种标准的标记方法，以便输出多种格式。

# 第5章：处理文字与图像

## 理解 DocBook

`DocBook` 是一种非常适合生成各种格式软件文档的 DTD。它最初由 OASIS 联合会（`www.oasis-open.org`）创建。

## 第二部分：运行 Linux 桌面

## 创建 DocBook 文档

你可以在任何文本编辑器中创建文档，使用外观与 HTML 标签相似的标签。

```
