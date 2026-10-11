
将 `{name}` 替换为您创建的文档类型。文件的文本以及您的格式化命令放在开始和结束命令之间。

# 图 21.10

使用 LyX 编辑器图形化创建 LaTeX 文档。

![](img/fa18693414a802b12c8add5f8c4be910_608_0.png)

## 使用 LyX 时需要的 N 件事

- 1. LyX 带有优秀的文档——请务必使用它们！从帮助 > 简介开始，这将向你对文档进行简要介绍。然后通过帮助 > 教程来学习如何使用 LyX。
- 2. LyX 是我们所谓的“文档处理器”。从设计上讲，它与普通的文字处理器不同——这种方式让编写文档变得更容易。但只有一点点不同，所以不要担心。文档会为你说明一切。

如果你想在普通的文本编辑器中编辑 LaTeX，你将熟悉 LaTeX 命令。要查看 LaTeX 命令的完整列表，请输入 `latex` 然后阅读出现的“LyX 文档中的命令”。

# 使用 LyX LaTeX 编辑器

使用 `lyx` 命令启动 LyX LaTeX 编辑器。LyX 附带许多支持性文档。点击“帮助”来选择教程、用户指南或其他信息。

要开始你的第一个文档，我建议你选择 LyX 提供的模板之一。模板位于 `/user/share/lyx/templates`。点击“文件 > 从模板新建”来打开模板。将出现一个可用模板列表。你可以使用它们创建信函、幻灯片和文章等。

提供剪切、复制、粘贴等标准编辑功能外，“布局”菜单允许你执行各种标记功能。对于数学函数，“数学”菜单允许你向文档中插入公式、平方根、指数、求和和积分函数。当你需要时，你可以：

- 将文件打印到 PostScript 打印机或输出 PostScript `.ps` 文件。（点击文件 > 打印，选择打印方法，然后点击确定）
- 将文件导出为 LaTeX、DVI、PostScript 或 ASCII 文本。（点击文件 > 导出，并从文件格式列表中选择。）

# 第四部分 运行应用程序

LyX 自称为 WYSIWYM —— 所所见即所得（What You Say What You Mean）。因此，你在编辑时在屏幕上看到的与打印出来的文档并不完全相同。例如，多次按回车键不会在行之间产生额外的空白。

由于 LyX 支持样式字体（style faces），它允许你创建符合多种不同标准的文档。例如，LyX 支持使用 `article` 类为美国数学学会（AMS）期刊进行排版。支持的其他文本类包括：

- 无章节的单面纸。
- 双面报告，通常比文章长。
- 与报告相同，但带有额外的前言和后。
- 幻灯片 `slides` —— 用于制作透明片。
- 信函 `letter` 包含地址、签名和其他元素的特殊环境。

# 使用 LaTeX 文件

无论你是创建自己的 LaTeX 文件、从 LyX LaTeX 编辑器导出，还是从互联网下载，都有多种实用程序可以格式化、打印或显示输出结果。以下是你的一些选择：

- 要格式化 LaTeX 文件 `filename.tex`，运行以下命令：
  ```
  $ latex filename.tex
  ```
- 要打印 DVI 文件 `filename.dvi`，将其发送到你的默认 PostScript 打印机，并输入以下内容：
  ```
  $ dvips filename.dvi
  ```
- 要在 X 窗口中显示 DVI 文件，输入以下内容：
  ```
  $ xvdi filename.dvi
  ```
- 要将 DVI 文件打印到 PCL 打印机（如 HP LaserJet），输入以下内容：
  ```
  $ dvicopy filename.dvi
  $ dvilj filename.dvi
  ```

`dvilj` 命令直接不支持虚拟字体。`dvicopy` 会转换字体以便 PCL 打印机可以处理。

# 转换文档

文档可以通过许多不同的格式提供。搜索互联网上的一些 Linux FTP 站点，你就会发现 PostScript、DVI、man、PDF、HTML 和 TeX 文件。还有各种图形格式。表 21-2 是常见文档和图形转换器的列表：

## 表 21-2

### 文档和图形转换实用程序

| 实用程序 | 转换 | 到 |
| --- | --- | --- |
| dos2unix | DOS 文本文件 | UNIX (Linux) 文本文件 |
| fax2ps | TIFF 真真图像文件 | 压缩的 PostScript 格式（PostScript 输出针对发送到低速线路的打印机进行了优化。这种格式对于大量黑色或连续调的图像效率较低，tiff2 可能更有效。） |
| fax2tiff | 传真数据 (Group 3 或 Group 4) | TIFF 格式（输出为低分辨率或中分辨率 TIFF。） |
| g32pbm | Group 3 文件（digifrax 或原始格式） | 可变位图 |
| gif2tiff | GIF (87) 文件 | TIFF 格式 |
| man2html | Man 页面 | HTML 格式 |
| pal2rgb | TIFF 图像（调板色） | 全色 RGB 图像 |
| pbm26g | 可变位图图像 | 传真文件 (Group 3) |
| pdf2dsc | PDF 文件 | PostScript 文（符合 Adobe 文档标准的 PostScript 文件。输出允许 Ghostview 等 PostScript 阅读器一次页地读取 PDF 文件。） |
| pdf2ps | PDF 文件 | PostScript 文件（2 级） |
| pfb2fa | Type 1 PostScript | ASCII |
| pk2bm | TeX | 位图 |
| ppm2tiff | PPM 文件 | TIFF |
| ps2ascii | PostScript | ASCII 文本 |
| ps2epsi | PostScript | 封装的 PostScript |
| ps2pdf | PostScript | PDF |
| ps2pk | PostScript | TeX |
| pstext | PostScript | ASCII 文本 |
| ras2tiff | 栅格文件 | TIFF |
| texihtml | TeX | HTML |
| tiff2bw | TIFF | 灰度 |
| tiff2image | TIFF | RGB 图像 |
| tiff2ps | TIFF | PostScript |
| unix2dos | UNIX (Linux) 文本文件 | DOS |

# 文字与图像处理 21

DocBook 对 Linux 和开源社区来说非常重要，因为许多开源项目都使用它来生成文档。例如，以下是使用 DocBook 创建描述其软件文档组织列表：

- Linux 文档项目 (`www.tldp.org/LDP/LDP-Author-Guide`)
- GNOME 文档 (`developer.gnome.org/projects/gdp/handbook/gdp-handler`)
- KDE 文档项目 (`www.kde.org/documentation`)
- FreeBSD 文档项目 (`www.freebsd.org/docproj`)

如果你想为这些文档项目中的任何一个贡献，请参考各组织的网站。在任何情况下，你编写的作者指南或样式都将描述它们所支持的 DocBook 标签。

## 创建 DocBook 文档

你可以在任何文本编辑器中创建文档，使用外观与 HTML 标签相似的标签（以小于号和大于号之间开头）。某些文字处理程序也允许你创建 DocBook 标记。

以下步骤展示了如何使用纯文本编辑器生成并通过 Linux 系统可用工具输出为 HTML 的简单 DocBook 文档示例。

> DocBook DTD 同时提供 SGML 和 XML 格式。在两者中，XML 格式正在被活跃维护。

![](img/fa18693414a802b12c8add5f8c4be910_612_0.png)

1. 在你的主目录下创建一个用于工作的目录，并进入该目录。例如，你可以在终端窗口输入以下命令：

```bash
$ mkdir $HOME/doctype
$ cd $HOME/doctype
```

2. 打开一个文本编辑器来编写你的 DocBook 文档。例如，你可以输入：
```bash
$ edit cardoc.xml
```
（使用如 `edit` 的文本编辑器，你可以在 `www.jedit.org` 获取，对于处理 DocBook 中使用的标签名称也非常有用。）

3. 输入你希望出现在文档中的标签和文本。大多数 DocBook 文档要么是 `<book>` 类型（大型多部分文档），要么是 `<article>` 类型（单章节文档）。要尝试创建一个 DocBook 文档，请输入：

```xml
<?xml version="1.0" ?>
<article>
  <title>选择一辆新车</title>
  <abstract>
    在这篇文章中，你将学习如何对汽车进行定价、议价和购买。
  </abstract>
</article>
```

# 第四部分 运行应用程序

```xml
<section>
```
