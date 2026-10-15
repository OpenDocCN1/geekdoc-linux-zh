
- `tiff2bw` — 将 RGB 或调板色 TIFF 图像转换为灰度 TIFF 图像。
- `tiffps` — 将 TIFF 图像转换为 PostScript。
- `unix2dos` — 将 UNIX (Linux) 文件转换为 DOS 文本文件。

## 创建 DocBook 文档

文档项目通常需要生成多种格式输出的文档。例如，描述如何使用某个软件程序的相同文本可能需要输出为打印手册、HTML 页面和 PostScript 文件。Linux 社区最近为创建所谓的“结构化文档”所采用的标准是 SGML、XML 和 DocBook。

## 理解 SGML 和 XML

标准通用标记语言 (`SGML`) 的创建是为了提供一种标准的文本标记方法，以便以后能以各种格式输出。由于 `SGML` 标记是通过文本标签完成的，因此可以使用任何纯文本编辑器创建 `SGML` 文档。文档由你的文档文本和标识文本中每种信息的标签组成。

与 Groff 和 HTML 等语言不同，`SGML` 的目的并不是在创建文档时强制某种特定的外观。例如，你不会将某段文本标记为粗体或斜体，而是将其识别为地址、段落或名称。稍后，会将样式表应用到文档上，对已标记的文本分配外观和呈现效果。

`SGML` 包含许多标签，为了简化基于 `SGML` 的文档生成，出现了许多其他项目以更好地关注 `SGML` 的使用方法。特别是可扩展标记语言 (`XML`) 的创建，是为了提供 `SGML` 的一个易于管理的子集，专门为良好地基于 Web 的出版而定制。

到目前为止，在描述 `SGML` 和 `XML` 时，我只提到了用于生成结构化文档的框架。特定的文档项目需要为需要生成的文档类型创建并在某种程度上强制执行特定的标记定义。

这些定义被称为数据类型定义 (`DTD`)。对于 Linux 本身和其他开源项目的文档，DocBook 已成为首选的 `DTD`。

## 理解 DocBook

DocBook 是一种非常适合生成多种格式文档的 `DTD`。它最初由 OASIS 联盟创建。有很多项目使用 DocBook，但最常见的是 Linux 内核和 Red Hat Linux 相关的手册。

## 第 6 章：使用 Red Hat Linux 进行发布 239

`db2html` 命令为每个页面添加“上一页/下一页”按钮。它还将每个章节的标题放在第一页的目录中以及浏览器的标签栏中。

![](img/9fef5c8304e11e92fef0da9b18dad7b1_260_0.png)

从这里开始，你可以继续添加内容并定义不同类型的标签。如果你正在为特定项目（如前面提到的 Linux 项目）编写文档，你应该获取有关特定标签的信息以及它们所要求的其他样式问题。

## 转换 DocBook 文档

上一个示例展示了如何创建一个简单的 DocBook 文档并将其转换为 HTML 输出。以下 Red Hat Linux 实用程序可以将 DocBook 转换为其他格式：

- `docbook2dvi` — 将 DocBook 文件转换为设备无关格式（Device Independent format）。
- `docbook2html` — 将 DocBook 文件转换为 HTML 格式。
- `docbook2man` — 将 DocBook 文件转换为 man 页面（帮助页）格式。
- `docbook2pdf` — 将 DocBook 文件转换为便携式文档格式（PDF）。
- `docbook2ps` — 将 DocBook 文件转换为 PostScript 格式。
- `docbook2rtf` — 将 DocBook 文件转换为富文本格式（RTF）。
- `docbook2xi` — 将 DocBook 文件转换为 GNU TeXinfo 格式。
- `docbook2txt` — 将 DocBook 文件转换为纯文本格式。

## 使用 Red Hat Linux 打印文档

Red Hat Linux 使用 `LPRng` 服务配置打印机。Red Hat Linux 中也提供了 `CUPS` 服务来处理打印服务。然而，这两项服务都允许你使用本章描述的同一组基本打印命令进行打印。

> 交叉引用：请参阅第 10 章，了解如何使用替代系统（Alternatives system）在 `LPRng` 和 `CUPS` 之间选择默认打印服务。有关为 Red Hat Linux 配置本地和远程打印机的信息，请参阅第 17 章。

作为非管理员用户，你对打印机的配置没有太大控制权。不过，你可以检查打印队列（等待打印的文件）的状态，并删除你自己的任何队列打印任务。

## 打印到默认打印机

当系统管理员（或你）为计算机配置打印机时，其中一个被定义为默认打印机。如果你不确定哪个是你的默认打印机，输入 `lpstat` 并查找带有勾选标记的打印机。

商业文字处理软件（如 StarOffice）允许你从可用列表中选择打印机。一些从命令行运行的复杂 Linux 实用工具，例如 `dvips`（打印 PostScript 文件）和 `groff` 打印 troff/noff 文件）会自动将输出发送到默认打印机。

作为普通用户，可以使用 `PRINTER` 环境变量覆盖默认打印机。例如，如果你计算机上的默认打印机是 `lp0`，而你想经常打印到 `lp1`，可以通过设置 `PRINTER` 变量来更改默认打印机：

```
$ export PRINTER=lp1
```

要使此效果永久生效，你可以将此行添加到你的 shell 配置文件之一（如果你使用 bash shell，则为 `$HOME/.bashrc`）。

## 从 shell 打印

`lpr` 命令用于打印文件。你可以使用 `lpr` 来检查是否正在使用 `LPRng` 还是 `CUPS` 服务。如果你已经有一个格式化好的文件，使用 `lpr` 打印它。例如，如果你有一个 PostScript 输出文件（`file.ps`）并想将其打印到你的 PostScript 打印机，使用以下命令行：

```
$ lpr file.ps
```

如果你想指定特定的打印机（默认打印机之外），请添加 `-Pprinter` 选项。例如，打印到 lp0 打印机，你可以输入：

```
$ lpr -Plp0 file.ps
```

## 第 6 章：使用 Red Hat Linux 进行发布 241

如果你想打印文档的多个副本，请使用 `#num` 选项，其中 num 替换为你想要的副本数。例如，要打印文件的五个副本，使用：

```
$ lpr -5 file.ps
```

`lpr` 命令还可以接受标准输出进行打印。例如，你可以通过管道将 groff 命令的输出传递给 lpr 来打印其输出，正如下所示：

```
$ groff -Tps -man /tmp/ch.1 | lpr -Flp0
```

> 提示：该包中的 `enscript` 命令是另一个打印纯文本文件的有用工具。它将文件转换为 PostScript 并将其发送到打印机或指定的文件。

## 检查打印队列

要检查已入队打印任务的状态，你可以使用 `lpq` 命令。默认情况下，`lpq` 会列出默认打印机队列中的任务列表。例如：

| 排名 (Rank) | 所有者 (Owner) | 任务 (Job) | 文件 (Files) | 总大小 (Total Size) |

| :--- | :--- | :--- | :--- | :--- |

| 第1 | | root | | (标准输入) | 625 bytes |

| 第2 | | root | 1 | memol.ps | 12273 bytes |

| 第3 | | chuck | 5 | bikes.ps | 10880 bytes |

`lpq` 的输出显示了等待打印的文件。Rank 列表显示它们在队列中的顺序。Owner 是入队任务的用户。Job 显示任务编号。Files 列显示文件名或标准输出。你可以添加 `-Pprinter` 来指定特定的打印机（默认打印机之外）来查看任务。Owner 是入队队列任务的用户。Total Size 显示了文件大小。

## 删除打印任务

如果你误打印了文档，可以使用 `lprm` 清除队列。在 Red Hat Linux 中使用 `lprm` 删除打印任务。例如，要删除 root 的所有任务（假设你是 root），输入以下内容：

```
$ lprm
```

## 242 第二部分：使用 Red Hat Linux

## 打印机状态

有时打印机没有打印任何东西，你不知道为什么。`lpc` 命令是一个可以运行的打印机状态检查工具，可能会给你提供线索。`lpc` 命令是为管理员设计的，因此它可能不在你的默认 PATH 中。启动 `lpc` 命令，输入以下内容：

```
# /usr/bin/lpc
lpc status
Printer Spooling Jobs Server
hp@localhost enabled disabled 4 none
lp0@localhost enabled enabled 0 none
lpc
```

在 `lpc` 提示符下输入 `status`。此示例显示了两个打印机的状态：hp 和 lp0。hp 打印机有 4 个等待任务。虽然队列和打印已启用，但由于队列已禁用，它们没有打印。

## 使用 Ghostscript 和 Acrobat 显示文档

如果你每次想更改文档的内容或格式都将文档发送到打印机，Red Hat Linux 的发布可能会非常耗纸。为了节省纸张和运行时间，可以使用打印预览程序在屏幕上显示文档在打印页面上的样子。以下章节描述了使用 ghostscript 命令显示 PostScript 文件，以及使用 Adobe Acrobat 显示便携式文档格式（PDF）文件。

## 使用 ghostscript 和 g 命令

在 Red Hat Linux 中显示 PostScript 或 PDF 文档可以使用 ghostscript 命令。ghostscript 命令是一个相当粗糙的界面，旨在让你逐行解释文档。（如果你的系统没有安装 ghostscript 命令，你可以通过随书附的 CD-2 安装 ghostscript 包来获取。）

如果你在计算机上有任何 `.ps` 或 `.pdf` 文件，就可以显示它们。例如，如果安装了 samba 包，你可以输入以下内容显示 PDF 文件（否则，你可以找到自己的 PDF 文件进行尝试）：

```
ghostscript /usr/share/doc/samba-*/docs/Samba-HOWTO-Collection.pdf
>>showpage, press <return> to continue<<
```

## 第 6 章：在 Red Hat Linux 上发布

在提示符处，按下 Enter（或 Return）键可以逐页查看文件。当文件查看完毕后，你可以输入另一个 PostScript 或 PDF 文件的名称进行查看。完成后，输入 `quit`。

`gv` 命令（ghostview）是查看 PostScript 文件的另一种更友好的方法。（如果你的系统中没有安装 `gv` 命令，你可以通过安装随书附带 CD-3 中的 `gv` 软件包来获取它。）

要使用 `gv` 打开名为 `bashref.ps` 的文件，你需要输入以下内容：

```bash
$ gv /usr/share/doc/bash-doc-*/bashref.ps
```

窗口打开后，你就可以看到文档了。在页面上点击鼠标左键并上下移动以滚动文档。你可以点击键盘 `Page Up` 和 `Page Down` 键来翻页。你可以点击左侧列中的页码跳转到特定页面，或点击 `Print All` 按钮打印整份文档。

### 使用 Adobe Acrobat Reader

便携文档格式（PDF）提供了一种以打印显示形式存储文档的方法。通过 Adobe Acrobat Reader，你可以以友好的方式查看 PDF 文件。Adobe Acrobat 让在 PDF 文件中移动变得非常简单。PDF 文件可能包含超链接、目录、图形和各种字体。

你也可以从 Adobe 网站（www.adobe.com/support/downloads）下载 Acrobat Reader 的免费版本。Acrobat Reader 是免费的，目的是鼓励人们购买 Acrobat 4 程序来创建 PDF 文档。通过 Acrobat 4，你可以将几乎任何类型的文档转换为 PDF，从扫描图像创建 PDF 文件，在 PDF 文档中添加电子注释和高亮，并应用数字签名（用于安全保护）。

在安装 Adobe Acrobat Reader 后，输入以下命令启动程序：

```bash
$ acrobatread
```

点击 `File -> Open`，并选择你要显示的 PDF 文件的文件名。图 6-12 显示了在 Adobe Acrobat Reader 中查看 PDF 文件的示例。

![](img/9fef5c8304e11e92fef0da9b18dad7b1_265_0.png)

图 6-12：在 Adobe Acrobat Reader 中显示 PDF 文件。

Acrobat Reader 具有许多功能。例如，你可以在文档旁边显示书签列表，点击书签即可进入特定页面。你还可以显示页面缩略图以便滚动和选择页面。

使用菜单栏或按钮，你可以翻阅 PDF 文档、放大缩小、跳转到文档开头或结尾，并显示文档的不同视图（以及显示书签和页面缩略图）。要打印副本，点击 `File -> Print`。

### 处理图形

在 Red Hat Linux 中，创建和处理图形的工具既多又强大。领先领先的是 GNU 图像处理程序（GIMP）。GIMP 允许你组合和创作图像，还可以修照片。Red Hat Linux 附带的其他创建图形工具包括 `xv`（一个用于截图的程序）和 `xpaint`（用于处理位图）。

> 交叉引用：请参第 8 章关于其他多媒体应用程序的描述，例如用于处理数码相机图像的 gphoto 窗口。

### 使用 GIMP 处理图像

GIMP 程序是一个随 Red Hat Linux 附的免费软件，用于处理照片和图形图像。要使用 GIMP 创建图像，你可以导入绘画、照片或 3D 图像，也可以从零开始。你可以通过点击系统菜单中的 `Graphics -> The GIMP` 或在终端窗口中输入 `gimp` 来启动 GIMP。

图 6-13 显示了 GIMP 的示例。

![](img/9fef5c8304e11e92fef0da9b18dad7b1_266_0.png)

**图 6-13：** GIMP 是一个强大的图形处理工具。

> **注意：** 如果你的系统中没有 GIMP 或未正确安装，你可以从随书附带的 CD-2 安装它。或者，你也可以从 www.gimp.org 获取最新版本的 GIMP。

在许多方面，GIMP 与 Adobe Photoshop 相似。有些人人认为 GIMP 的脚本功能可以与 Adobe Photoshop 中的“动作（Actions）”相媲美，甚至更优。然而，GIMP 缺少的一个功能是不支持 CMYK 分色。

### 屏幕截图

如果你想展示在 Red Hat Linux 上完成的工作示例，可以使用 `xv` 实用程序来捕捉屏幕图像。该工具对于我们这些写计算机书籍的人来说特别方便。（本书中的大部分图像都是使用 `xv` 实用程序截取的。）由于 `xv` 是共享软件，若要商用，你应该向 `xv` 的创建者发送 25 美元的费用（点击 `About xv` 按钮查看许可信息和费用发送地址）。

`xv` 不再是 Red Hat Linux 发行版的一部分。从存储 Linux 的 FTP 站点（例如 ftp://ftp.redhat.com/pub/contrib/libc6/i386/）获取 `xv` 的副本。要打开 `xv` 窗口，输入：

```bash
$ xv &
```

当你首次启动 `xv` 时，会显示 `xv` 图像显示窗口（截图将出现的地方）。点击该窗口查看 `xv` 控制窗口（包含抓取和保存屏幕的按钮）。

要使用 `xv` 抓取图像，点击 `Grab`。对话框让你选择 `Grab`（使用鼠标左键抓取窗口）或 `AutoGrab`（在几秒后自动抓取光标所处的窗口）。

对于 `Grab`，你可以点击想要抓取的窗口，或使用鼠标（如果是三键鼠标）拖动出一个矩形区域进行抓取。在使用 `AutoGrab` 之前，你必须输入 `Delay`（单位为秒），让 `xv` 等待多久后再抓取光标指示的窗口。

抓取图像后，你可以对其进行处理。在图像窗口上选择一个矩形区域。然后，从控制窗口点击 `Scissors`（裁剪区域）、`Crop`（裁剪区域外）或任一箭头按钮（上下或左右翻转选取区域）。点击旋转箭头向某个方向旋转图像。

要保存图像，点击 `Save`。从 15 种不同的图像输出类型中选择格式。选择彩色、黑白抖动或灰度。选择图像的目录和文件名。然后点击 `OK`。如果你想查看计算机上的任何图像，点击 `Load` 并选择你要的文件。

> 注意：如果你只是想快速截屏，Ksnapshot 效果很好。要使用 Ksnapshot，在主菜单点击 `All Applications -> Graphics -> Screen Capture Program`。Ksnapshot 窗口打开并显示桌面的缩略图。只需点击 `Save` 将图像保存为该文件名。或者你也可以捕捉新图像或更改保存图像的文件。

### 使用 KPaint 修改图像

使用 KPaint 窗口（这是 KDE 桌面 `kpaint` 软件包附带的实用程序），你可以处理并转换多种格式的图像。图 6-14 显示了 KPaint 的示例。

![](img/9fef5c8304e11e92fef0da9b18dad7b1_267_0.png)

图 6-14：使用 KPaint 编辑位图图像。

## 248 第二部分：使用 Red Hat Linux

![](img/9fef5c8304e11e92fef0da9b18dad7b1_269_0.png)

- `xscanimage` — 另一个基于 xsane 的窗口，用于预览和从 Linux 扫描仪或数字照相机扫描图像。从命令行启动 `xscanimage` 可以让你将图像保存为 PBM（黑白）、PGM（灰度）或 PPM（彩色）格式。当作为 GIMP 插件使用时，GIMP 会处理这些图像。
