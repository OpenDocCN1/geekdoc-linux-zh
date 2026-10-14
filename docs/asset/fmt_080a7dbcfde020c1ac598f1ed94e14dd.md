
## 使用 OpenOffice.org Writer

## 使用 Scribus

## Linux 的其他文字处理器

## 创建和发布文档

### 在 Ubuntu 上使用文档标记语言

当人们只使用终端时，文字处理意味着在文本编辑器中创建文档，并使用特殊命令告诉其他应用程序如何为特定的输出格式格式化你的文档。创建这些文档的格式被称为*标记语言*，其中一个例子是 `HTML`。当然，`HTML` 设计用于标记目标为 Web 页面的文档，但同样的原理也适用。在标记语言中创建文档仍然很流行，因为许多机构和期刊使用标记语言的文本文件作为提交的*最低公约数*。这使得他们能够将来自不同来源的文档合并成一份风格统一的出版物，而而不必担心谁使用了哪个版本的软件、使用了什么字体等。

`LaTeX`（发音为 *la-tekh*）是一种排版程序和相关的标记语言，设计用于产生高质量的输出，特别是对于科学和数学符号。

`Knuth` 在 1977 年编写了 `TeX`，很大程度上是因为他需要为他的《计算机程序设计》系列丛制作一个足够高质量的工具。如果编写自己的格式系统不很酷的话，`Knuth` 原初在他自己的一的一个名为 `WEB` 的系统中编写了 `TeX`，这是一种将文档和 Pascal 源代码混合在单个源文件系统。

今天有多种 `TeX` 的实现版本，它们都提取自原始版本，有些被翻译成其他语言，有些经过增强以添加额外功能。`Ubuntu` 仓库提供的 `TeX` 版本（如现在的 x 系统上）是 `TeTeX`，这是一个适用于类 Unix 系统的完整 `TeX` 分发版，由 `Thomas Esser`（因此 teTeX 中的“te”）开发。`teTeX` 的主页是 `www.tug.org/tetex`。

### 在你的 Ubuntu 系统上安装 TeX

`TeX` 并不是所有人需要的，它没有默认安装在 `Ubuntu` 系统上。要安装 `TeX`，从系统 ➪管理菜单启动“软件包管理器”，并选择“`TeX` 作者”部分（`Synaptic` 对话框的左侧）。虽然有许多 `TeX` 相关的软件包，但三个关键的包如下：

- `tetex-base`
- `tetex-bin`
- `tetex-doc`

你可能想要选择 `tetex-doc` 包，它提供了各种 `HOWTO` 和其他文档。图 10.1 显示了 `Synaptic` 软件包管理器中选中的这些软件包。

软件包管理器

这三个包并安装它们还将安装一些其他强制性包。一旦安装完成，你就可以开始尝试 `TeX` 了。有关使用 `Synaptic` 软件包管理器的更多详细信息，参见第 20 页，“添加、删除和更新软件”。

### TeX 标记

用法非常简单。例如，产生格式化输出字符串“Hello, World!”的 `TeX` 文档源代码如下：

```
lo, World!
```

要处理此文档，你只需在 `Ubuntu` 命令行执行 `tex` 命令，并将文件作为参数。你将在屏幕上看到类似下面的的内容：

```
ex hello.tex
s is TeX, Version 3.141592 (Web2C 7.5.4)
hello.tex \[1\] )
put written on hello.dvi (1 page, 228 bytes).
nscript written on hello.log.
```

使用 `TeX` 的文件会生成 `DVI`（设备无关）格式的输出文件。`DVI` 输出是一种中间二进制格式，仅包含字符定位和字体信息（当然还有文档本身），并且必须由另一个程序进行后处理，该程序需要理解如何在你的屏幕上渲染此文件，或者按你的打印机使用的特定格式或打印机控制语言生成输出。

从“Hello, World!”示例的样本 `TeX` 标记可以看出，你不需要许多 `TeX` 命令就能生成简单的文档。然而，这里的关键词是“简单”。要使用不同的字体、居中对齐和不同的章节生成一个稍微复杂的文档，你的原生 `TeX` 代码看起来如下所示：

```latex
\interline{This is a Title}
\allskip
\interline{Bill von Hagen}
\interline{\tt 24 March, 2006}
\gskip
\narrower\noindent
```

该示例展示了执行原始 `\TeX` 命令的一些复杂性，并旨在说明如果我使用某种高级宏包，这段相同的文本将会变得简单得多。那样不是好吗……\par

\gskip

\section 1. 引言

\allskip

这将是引言的文本……

图 2 显示了处理此纯 `TeX` 文档生成的 `DVI` 文件预览，在 `DVI` 预览器中显示。

来自纯 `TeX` 示例

![](img/e88880e40d650bfe19d5b6927bd86568_294_0.png)

### 使用 LaTeX 标记

无论输出看起来有多好，使用上一节中的低级 `TeX` 命令编写文档将是巨大的痛苦，尤其是大量使用手动格式命令。为了简化使用 `TeX` 创建文档，开发者开发了各种宏包，其中最著名的是 `Leslie Lamport` 的 `LaTeX` 宏包。这些宏包支持许多类型的文档，如文章、手册、信函等，并提供了这些类型文档易于记忆的传统组件。为了方便起见，当你在 `Ubuntu` 系统上安装 `teTeX` 时，`LaTeX` 宏和相关应用程序会自动安装。使用 `LaTeX` `article` 文档类型的示例，之前的纯 `TeX` 代码看起来像下面的 `LaTeX`：

```latex
\documentclass{article}
\begin{document}
\title{This is a Title}
\author{Bill von Hagen}
\date{\today}
\begin{abstract}
此示例展示了当使用 \LaTeX 宏而非原始 \TeX 命令进行标记时，此相同的文档会变得简单多少，并旨在说明如果我使用某种高级宏包，这段相同的文本将会变得简单得多。这确实很好（而且凡人也能理解）。
\end{abstract}
\section{Introduction}
这将是引言的文本……
\end{document}
```

`TeX` 产生的输出比之前运行 `TeX` 的示例略显冗长。处理上一个示例的输出（存储在 `example_latex.tex` 文件中）如下：

```bash
latex example_latex.tex
This is pdfeTeX, Version 3.141592-1.21a-2.2 (Web2C 7.5.4)
loading extended mode
example_latex.tex
pdfTeX2 <2003/12/01>
engine <v3.8d> and hyphenation patterns for loaded.
src/share/texmf-tetex/tex/latex/base/article.cls
document Class: article 2004/02/16 v1.4f Standard LaTeX document class
src/share/texmf-tetex/tex/latex/base/size10.clo)
example_latex.aux
overfull \hbox (9.76526pt too wide) in paragraph at lines 10-14
1/cmr/m/n/9 become when marked up using \LaTeX macros rather than raw \TeX commands
(./example_latex.aux) (see the transcript file for additional information)
output written on example_latex.dvi (1 page, 1164 bytes).
script written on example_latex.log.
```

格式化 `LaTeX` 文档的命令是 `latex` 而不是之前使用的 `tex` 命令。`latex` 调用了一个预编译的 `TeX` 版本，其中包含了所有宏、字体数据和 `LaTeX` 定义的信息。图 10.3 显示了处理此 `TeX` 文档生成的 `DVI` 文件预览，在 `xdvi` `DVI` 预览器中显示。从样本 `LaTeX` 输入可以看出，`LaTeX` 为标题、日期、摘要、章节（带自动编号）等逻辑元素提供了宏。图 10.3 显示输出基本上是相同的，只是在页面居中方面存在差异。

来自简单的 `LaTeX` 示例

如今使用 `TeX` 创建文档的人实际上使用 `LaTeX`，不仅是因为其宏的便利性，还因为它支持自动创建目录、插图列表等既重要又实用的文档结构。然而，讨论创建 `LaTeX` 文档不在本书的范围之内，但许多其他人都已经建议了关于创建 `LaTeX` 文档和使用 `LaTeX` 的详细信息来源，例如本章后面的“关于 `TeX` 和 `LaTeX` 的信息”。

### 查看和预览 DVI 文件

要查看由 `TeX` 或 `LaTeX` 创建的 `DVI` 文件，你需要一个 `DVI` 查器。你可以使用名为 `xdvi` 的应用程序立即预览你的 `DVI` 文件，或者使用其他 `DVI` 处理器：

- `dmps`: 生成适用于 `PostScript` 的输出。
- `dvips`: 生成适用于 `PostScript` 的输出。
