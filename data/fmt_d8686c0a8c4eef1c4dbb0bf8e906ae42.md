
图 16-1 显示了处理此 TeX 文档生成的 DVI 文件视图，在作为 `texlive` 软件包一部分安装的 xdv DVI 查看器中显示。

# 图 16-1

预览纯 TeX 示例的输出

![](img/e3248f698da647444405a34229bd9df5_643_0.png)

# 引入 LaTeX 标记

面对现实吧——无论输出看起来如何，使用上节所示的低级 TeX 命令编写文档将是巨大的痛苦，尤其是大量使用手动格式化和间距命令。为了简化使用 TeX 创建文档，开发者们开发了各种宏包，其中最好的是 Leslie Lamport 的 LaTeX 宏包。它支持不同类型的文档（如文章、手册、信件等），并为这些类型文档的传统组件提供了易记的宏。为了方便起见，当你在 Ubuntu 系统上安装 `texlive` 时，LaTeX 软件包及相关应用程序会自动安装。

作为使用 LaTeX 文章类型的示例，之前的 TeX 代码在 LaTeX 中看起来如下所示：

```
\documentclass{article}

\begin{document}
```

# 创建发布文档

```
\title{This is a Title}

\author{Bill von Hagen}

\date{today}

\maketitle
```

```
\begin{abstract}

此示例展示了当使用 \LaTeX 宏而非 \TeX 命令进行标记时，同样的文档会变得简单多少，并旨在说明如果我使用某种高级别的包，同样的文本将会变得简单得多。这很棒（而且凡人也能理解）。

\end{abstract}
```

```
\section{Introduction}

This would be the text of an introduction...

\end{document}
```

运行 LaTeX 产生的比之前运行 TeX 的示例稍微冗长一些。上一个示例的输出存储在 `example_latex.tex` 文件中，如下：

```
$ example_latex.tex

This is pdfTeX, Version 3.141592-1.40.3 (Web2C 7.5.6)

&& line parsing enabled.

extending extended mode

./example_latex.tex

LaTeX 2005/12/01

\babel[v]{english} and hyphenation parameters for english,

english, dumplay, hyphenation, loaded.

/usr/share/texmf/tex/latex/base.cls

./example_latex.aux

[1] (output)

Output written on example_latex.dvi (1 page, 172 bytes).

Transcript written on example_latex.log.
```

注意，格式化 LaTeX 文档的命令比之前使用的 `tex` 命令更容易。从“Hello, World!”示例的标记可以看出，不需要许多 TeX 命令就能生成简单的文档。然而，这里的关键在于简单。要使用不同的字体、居中和不同章节创建一个稍微复杂一点的文档，你的原生 TeX 代码看起来如下：

```
\center(This is a Title)

\smallskip

center(Bill von Hagen)

\center(\tt 17 May, 2008)

\bigskip
```

```
\bigskip

\beginskip 1. Introduction

\smallskip

This would be the text of an introduction...

\bye
```
