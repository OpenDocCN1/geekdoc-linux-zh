
- `dosunix`：将 DOS 文本文件转换为 UNIX (Linux) 文本文件。你可能想使用此命令的原因是 DOS 文本文件包含双字符换行符，而 Linux (UNIX) 文本文件具有单字符换行。

- `fax2ps`：将 TIFF 传真图像文件转换为压缩的 PostScript 格式。PostScript 输出针对发送到低速线路上的打印机进行了优化。这种格式对于黑色背景或连续调的图像效率较低。（在这些情况下，`tiff2ps`可能会更有效。）

- `fax2tiff`：将传真数据（第 3 组或第 4 组）转换为 TIFF 格式。输出是低分辨率或中分辨率的 TIFF 格式。

- `gif2tiff`：将 GIF (87) 文件转换为 TIFF 格式。

- `man2html`：将 man 页面转换为 HTML 格式。

- `pal2rgb`：将 TIFF 图像（调板色）转换为全彩色 RGB 图像。

- `pdf2dsc`：将 PDF 文件转换为 PostScript 文档 DSC 文件。PostScript 文件符合 Adobe 文档结构规范 (DSC)。输出允许 PostScript 阅读器（如 Ghostview）一次性读取 PDF 文件。

- `pdf2ps`：将 PDF 文件转换为 PostScript (level 2)。

- `pfb2pfa`：将 Type 1 Postscript 字体（二进制 MS-DOS）转换为 ASCII 可读。

- `pk2bm`：将 TeX 字体文件转换为位图。

- `ppm2tiff`：将 PPM 文件转换为 TIFF。

- `ps2ascii`：将 PostScript 文件转换为 ASCII 文本。

- `ps2si`：将 PostScript 文件转换为封装的 PostScript (Encapsulated PostScript)。

- `ps2pdf`：将 PostScript 文件转换为 PDF 格式。

- `ps2pk`：将 PostScript 文件转换为 TeX。

- `ps2rgb`：将 PostScript 文件转换为 RGB。

- `ras2tiff`：将光栅文件转换为 TIFF。

- `sun2tiff`：将 Sun 文件转换为 TIFF。

- `tiff2ps`：将 TIFF 图像转换为 PostScript。

- `tiff2tiff`：将 TIFF 图像转换为 TIFF 格式。

- `tiff2bw`：将 TIFF 图像转换为灰度模式。

- `tunix`：将 TIFF 图像转换为 UNIX (Linux) 文本文件。

- `unix2dos`：将 UNIX 文本转换为 DOS 文本文件。

- `unix2ps`：将 UNIX 文本转换为 PostScript。

- `unix2tiff`：将 UNIX 文本转换为 TIFF 格式。

# 理解 SGML 和 XML

标准通用标记语言 (`SGML`) 的创建是为了提供一种标准的文本标记方式，以便输出为各种格式。由于 `SGML` 包含许多标签，特别是可扩展标记语言 (`XML`) 的创建是为了提供一个易于管理的 `SGML` 子集，专门为良好的 Web 发布而定制。

# 309 第二部分：使用 Fedora 和 RHEL

在 particular

文档由识别文本中每种信息的标签组成。与 `Groff` 和 `HTML` 等标记语言不同，`SGML` 在创建文档时并不强制执行特定的外观。因此，例如你不会将某部分文本标记为粗体或斜体，而是将其识别为地址、段落或名称。随后，将一个样式表应用于文档。

到目前为止在描述 `SGML` 和 `XML` 时，我只提到了用于生成结构化文档的框架。特定的文档项目需要创建并在某种程度上为它们需要生成的文档类型强制特定的标记定义。这些定义被称为数据类型定义 (`DTDs`)。对于 Linux 本身和其他开源项目的文档，`DocBook` 是首选选择。

# 理解 DocBook

`DocBook` 是一种非常适合以各种格式生成计算软件文档的 `DTD`。它最初由 `OASIS` 联盟 (`www.oasis-open.org/docbook`) 创建，现在由许多不同的社区和开源工具支持。

> 交叉引用：你可以在 `www.docbook.org` 找到 `DocBook` 的官方文档。

`DocBook` 的重点是内容，而不是指示外观（即字体、大小、位置等）。它包含了允许你自动化创建索引、插图列表和目录的标记。在 Fedora 和 RHEL 中，你将 `DocBook` 文档输出为 `HTML`、`PDF`、`DVI`、`PostScript`、`RTF` 等格式。

`DocBook` 对 Linux 社区很重要，因为许多开源项目正在使用 `DocBook` 制作文档。例如，以下是使用 `DocBook` 创建描述软件文档的组织及相关网站：

- Linux 文档项目 (`www.tldp.org/LDP-Author-Guide`)

- GNOME 文档 (`developer.gnome.org/projects/gnome/handbook/gdp-handbook`)

# 第 6 章：使用 Fedora 和 RHEL 27 发布

- [KDE 文档项目](www.kde.org/documentation)

- [FreeBSD 文档项目](www.freebsd.org/docproj)

如果你想为上述任何文档项目做出贡献，请参考各机构的网站。在所有情况下，它们都会发布作者指南或样式指南，描述它们在写作工作中支持的 `DocBook` 标签。

## 创建 DocBook 文档

你可以使用任何文本编辑器创建文档，使用外观与 `HTML` 标签相似的标签（起始标签和结束标签出现在小于号和大于号之间）。还有一些文字处理程序也允许你创建 `DocBook` 标记。例如，你可以从 `OpenOffice Writer` 将文档导出为 `DocBook` 格式。

以下步骤包含一个使用纯文本编辑器生成简单 `DocBook` 文档，并使用 Fedora 和 RHEL 自带工具输出为 `HTML` 的示例。（你需要安装 DVD 上的 `docbook` 软件包才能执行以下操作）

- 1. 在你的主目录中创建一个工作目录并进入该目录。例如，你可以在终端窗口输入以下内容：

```
$ mkdir $HOME/doctest
$ cd $HOME/doctest
```

- 2. 打开一个文本编辑器来存放你的 `DocBook` 文档。例如，你可以输入：

```bash
$ gedit cardoc.sgml
```

（也可以使用从 `www.edit.org` 获取的 `edit` 等编辑器来处理 `docbook` 中使用的长标签名。）

- 3. 输入你想在文档中显示的标签和文本。大多数 `DocBook` 文档要么是 `<book>` 类型（大型多部分文档），要么 `<article>` 类型（单章节文档）。要尝试一个 `DocBook` 文档，输入以下内容：

```xml
<?xml version="1.0">
<article>
  <title>选择一辆新车</title>
  <header>
    <abstract>
      在本文中你将学习如何对汽车进行定价、
      谈判和购买。
    </abstract>
  </header>
  <section>
    <title>开始指南</title>
    <para>
```

<para>你将学到的第一点是如何确定你的预算承受范围。</para></section><title>下一步</title><para>在你知道自己能负担起什么之后，就可以开始搜索了。</para></section></article>
```

关于此文档，有几点你需要注意。整个文档被封装在 `article` 标签 `<article> </article>` 中。文章标题位于 `title` 标签 `<title></title>` 中。`section` 标签 `<section></section>` 表明具有标题和每个段落的文本章节。这些章节之后可以在目录（TOC）中被单独处理。

- 4. 保存文件并退出编辑器。

- 5. 接下来，你可以将刚刚创建的文档转换为几种不同的格式。例如，要创建 `HTML` 输出，你可以输入以下内容：

```
$ db2html cardoc.sgml
```

结果是一个名为 `cardoc` 的目录。`cardoc` 目录中 `db2html` 的结果是：`stylesheet-images` 目录、`t2.html` 文件和 `x12.html` 文件。

- 6. 要查看刚刚创建的 `HTML` 文件，我输入了以下内容：

```
$ firefox $HOME/doctest/cardoc/t2.html
```
