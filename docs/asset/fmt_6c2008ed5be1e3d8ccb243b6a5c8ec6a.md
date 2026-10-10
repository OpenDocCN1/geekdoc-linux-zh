
如果你使用的硬件缓慢，`AbiWord` 的性能比 `OpenOfficeorg Writer` 好。如果你在跨平台环境中工作，你可以获得适用于 Windows、Mac OS X、QNX 以及大多数 UNIX 派生版（Linux、BSD、Solaris 等）的 `AbiWord` 版本。

# 第 6 章：在 Fedora 和 RHEL 上发布

最近添加的功能（如样式和项目符号）继续使 `AbiWord` 成为一个更有用的文字处理工具。虽然它与类似的商业产品相比没有竞争力，但它的开发者仍在对其进行改进。

## 使用 KOffice

有一套配合 KDE 桌面系统的 KDE 办公套件。`KOffice` 软件包包含了你在集成办公套件中预期的基础应用程序：文字处理器 (`KWord`)、电子表格 (`KSpread`)、演示文创建器 (`KPresenter`) 和绘图程序 (`KChart`)。

尽管 `KOffice` 不是 Fedora Core 发行版的一部分，但可以通过 Fedora Extras 获取（使用命令 `install koffice-suite` 来安装 `KOffice` 软件包件）。当你使用 `KOffice` 时，可以从左列选择不同的办公应用。在任何一个应用程序中打开多个文档。然后点击左列的“文档 (Documents)”来选择当前显示哪一个。

图 6-2 显示文档的 `KWord`

你可以处理各种文档、电子表格和图像类型；支持的商业文档类型不多。在将文档读入 `KWord` 之前，你可能需要使用其他工具导入文档。然而，`KSpread` 程序可以打开多种不同的电子表格样式，例如 Microsoft Excel 和 GNumeric 电子表格。`Kivio` 是一种流程图工具。

![](img/c7605e408543e0a1829c1fd0cf2f687d_292_0.png)

## Web 服务器简介

众所周知的世界维网起源于蒂姆·伯纳斯李（Tim Berners-Lee）在欧洲核研究中心（CERN）的一个项目。其最初的目标是为全球分布的需要访问各种格式的研究人员和科学家提供一个统一的接口。从这个想法产生了使用一个客户端（Web 浏览器）从多种类型的服务器（HTTP, SMTP, Gopher, NNTP, WAIS, Finger 和流媒体服务器）访问数据（文本、图像、声音、视频和二进制文件）的概念。

Web 服务器的工作通常简单，只需接收超文本 (HTTP) 请求并向客户端发送响应。随着服务器还需要执行诸等功能，这项工作可能会变得复杂得多：

图 6-2：你可以在 `KWord` 中处理 Word 文。

## 使用传统的 Linux 发布工具

使用旧式的文本处理器（如 `Groff` 和 `TeX`），你可以在写作时忽略文档的外观。纯文本宏后处理器会指导你在写作完成后如何为打印排版文档。而使用文字处理器（如 OpenOffice Word 和 StarOffice Writer），你可以对文本进行标记并看到文档的基本布局。

传统 Linux 发布工具的某些属性使得它们特别适合某些类型的文档发布。`Groff` 和 `LaTeX`（基于 Tex）随 Fedora 和 RHEL 附带了文档，并且在技术同仁中非常受欢迎。原因如下：

- 你可以操作纯文本格式的文件。使用如 `grep` 等工具，你可以通过单个命令或脚本扫描并更改一份或几百份文档。
- 支持科学计数法。通过 `eqn`，你可以创建复杂的方程。`LaTeX` 和 `TeX` 适用于技术符号。某些数学出版物需要 `LaTeX`。
- 编辑可以更快，因为传统的 Linux 文档是用文本编辑器创建的。通常你从文本编辑器中获得的效果比文字处理器更好。

简单的布局非常适合于 Linux 文档工具。例如，一本带有少量图表和图像的技术书籍可以使用 `Groff` 或 `LaTeX` 轻松地制作和维护。使用这些工具编写信函和备忘录也容易的。当然，Linux 页面是使用基于文本的工具创建的。

此外，Linux 喜欢 PostScript。尽管人们认为 PostScript 是一种打印语言，但它实际上是一种编程语言（你可以直接编写 PostScript 代码）。Linux 文档处理软件包含了 PostScript 的打印驱动程序。有很多工具可以将 PostScript 转换为其他格式。此外，网络上的一些文档以 PostScript (`.ps`) 格式发布。

传统 Linux 文档工具的缺点是它们不直观。虽然 `LaTeX` 有一些简单的方法（见后文对 `LyX` 的描述），如果你在文本编辑器中创建文档，你需要学习在文档中输入哪些宏，以及使用哪些格式和打印命令。

> 注意：多年来，由 AT&T 分发的 UNIX 系统文档是以 `troff`/`nroff` 格式创建的，这些格式早于 `Groff`。文档对页面和指南材料使用了单独的宏。使用源代码控制系统 (`SCCS`)，可以将数千页文档迁移到不同的 UNIX 系统上。如今，Fedora 和 RHEL 包含了相同的工具来处理许多页面。

## 在 Groff 或 LaTeX 中创建文档

你可以使用任何文本编辑器为 Linux 的 `Groff` (`troff`/`nroff`) 或 `LaTeX` (`TeX`) 风格创建文档。Fedora 和 RHEL 附带了几个文本编辑器，你也可以从互联网下载其他的。请查看“选择文本编辑器”侧边栏获取更多信息。

在 `Groff` 或 `LaTeX` 中创建文档的过程包括以下通用步骤：

- 使用任何文本编辑器创建一个文档。文档将包含文本和标记。
- 使用与你创建的文档样式匹配的格式命令格式化文档（例如使用 `groff` 或 `latex`）。在此步骤中，你可能需要指示文档包含特殊内容，例如方程（`eqn` 命令）、表格（`tbl` 命令）或线条图（`gic` 命令）。
- 将文档发送到输出设备。该设备可以是打印机或显示系统。

如果你习惯带有 GUI 的文字处理器，你可能会发现这些发布工具很困难。

## 使用 Groff 处理文本

Web 服务器的工作通常简单，只需接收超文本 (HTTP) 请求并向客户端发送响应。随着服务器还需要执行诸等功能，这项工作可能会变得复杂得多：

（注：原文中存在大量重复的 OCR 错误，已根据逻辑进行去重处理）

### Groff 预处理器

- `eqn` — 该预处理器用于格式化在 `groff` 中生成方程的宏。
- `pic` — 该预处理器用于格式化在 `groff` 中创建简单线条图的宏。
- `tbl` — 该预处理器用于格式化在 `groff` 中生成表格的宏。

格式化后的 `Groff` 文档输出到特定设备。设备可以是打印机、窗口或（对于纯文本）你的 shell。`Groff` 支持以下输出格式：

- `ps` — 为 PostScript 打印机或 PostScript 查看器生成 PostScript。
- `lj4` — 为 HP LaserJet4 或其他兼容 PCL5 的打印机生成输出。
- `ascii` — 生成可以在终端窗口查看的纯文本。
- `dvi` — 生成 `TeX` dvi 格式的输出，用于后文描述的设备。
- `X75` — 为 X11 75 点/英寸查看器生成输出。
- `X100` — 为 X11 100 点/英寸查看器生成输出。
- `latin1` — 使用 ISO Latin-1 字符集生成类似打字机的输出。

## 使用 Groff 格式化和打印文档

你可以使用 Fedora 或 RHEL 系统上的任何 man 页（例如 `/usr/share/man/*`）来格式化和打印现有的 `Groff` 文档。这些 man 页是压缩的，因此你可以它们拷贝到临时目录并解压。尝试一下 `Groff`。

这些命令将选定的 man 页复制到 `/tmp` 目录并解压。然后，`groff` 将选定的 man 页格式化为纯文本，以便你可以在屏幕上查看。

```bash
$ cp /usr/share/man/man/chown.1.gz /tmp
gunzip /tmp/chown.1
groff -Tascii -man /tmp/chown.1 | less
```

在前面的例中，man 页 (`chown.1.gz`) 被复制到 `/tmp` 目录，使用 `gunzip` 进行解压，并使用 man 宏 (`-man`) 以纯文本格式 (`-Tascii`) 输出。输出通过管道传给 `less`，以便在屏幕上进行翻页查看。与其传传给 `less`，你也可以将输出重定向到文件（`> /tmp/chown.txt`）。

为了为了排版格式化页面，你可以指定 PostScript 或 LaserJet 输出。你应该将输出重定向到文件或打印机。这里有几个例子：

```bash
$ groff -Tps -man /tmp/chown.1 > /tmp/chown.ps
$ groff -Tlj4 -man -1 /tmp/chown.1
```

第一个示例创建 PostScript 输出 (`-Tps`) 并将其重定向到名为 `/tmp/chown.ps` 的文件。该文件可以使用 PostScript 查看器（使用 `ghostscript`）查看，或发送到打印机 (`lpr /tmp/chown.ps`) 并定向到默认打印机 (`-Tlj4 -1` 选项)。
