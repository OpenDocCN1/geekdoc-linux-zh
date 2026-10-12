
# LaTeX 项目介绍

你了解 LaTeX 项目吗？如果了解，请查看我们对 LaTeX 项目的（短期）描述。多年来，许多作者、贡献者等对 LaTeX 项目做出了贡献。许多版本以 `PDF` 形式提供。如果你想查看 LaTeX 中可使用的代码，请查看。如果你想通过捐赠支持 LaTeX 开发，请向 LaTeX 用户组捐赠。你可以轻松地创建自己的目录、图表列表或列表。如果你遇到困难并寻求帮助，请阅读我们关于在哪里可以找到帮助的提示。以静默模式执行 `latexmk`。LaTeX 是一个实用的文档生成程序，可以为你节省时间。

## 目录

| 目录 |
| :--- |
| 1 仪表板 |
| 1.1 第一章目录 |
| 1.2 第一章节 |
| 1.3 第一章图表 |
| 1.4 第一章表格 |
| 2 仪表板 |
| 2.1 第二章目录 |
| 2.2 第二章节 |
| 2.3 第二章图表 |
| 2.4 第二章表格 |
| 3 仪表板 |
| 3.1 第三章章节目录 |
| 3.2 第三章节 |
| 3.3 第三章图表 |
| 3.4 第三章表格 |

## 使用 LaTeX 编写书籍

学习如何使用 LaTeX 及其包排版、美化并自定义你自己的书籍。

### 顾问

`Mihalis Toukoulos` 是一位 UNIX 管理员、程序员（Unix 和 iOS）、数据库管理员和数学家。他从 1993 年开始一直使用 LaTeX。

### 资源

*   **LaTeX 项目**
    `http://www.latex.org/`

*   **综合 LaTeX 存档**
    `http://www.fay.psu.edu/~collins/software/`
    `latexmk-pj`

### 综合 LaTeX 描述

`LaTeX` 公司，第二版，Wesley，2004。`Donald Knuth` 在 1970 年创建了 `TeX` 作为一种排版语言，在计算机上编写书籍后发现程序还不够，例如，最大的选择是在 LaTeX 和 InDesign 之间。LaTeX 被证明是最佳选择。它的起源于 C 编程语言，但它有很多低级命令且难以使用，`Leslie Lamport` 决定让它变得更容易。他编写了许多高级命令并变成了 LaTeX，现在被广泛使用。许多人想要排版大约 350 页的大型著作。这篇文章对于那些从未听说过它并好奇它为什么如此流行的人，你应该知道它帮助许多论文作者轻松地完成工作。

## 在 LaTeX 中写书籍

### 简化专业代码

首先你需要安装 LaTeX。野外大量的输出包含名称，运行 `apt-cache search`。你可以通过执行以下命令获取更有帮助的输出：

```bash
apt-cache search | grep latex
```

#### 02 使用 LaTeX

安装基础 LaTeX 包后，你应该尝试编译后续 LaTeX 代码以确保一切运行完全符合你的预期。

```latex
\documentclass{article}
\title{Title of Hello}
\author{Michael Thomas}
\date{January 2015}
\document
Hello world!
\end
```

你可以使用以下命令编译文档：

```bash
helloworld.tex
```

上一个命令产生 DVI 文件，你可以将其转换为 PDF 格式。

#### 03 优缺点

LaTeX 有它的优点，包含许多细节，如果你刚刚开始，这些细节足够了。使用传统的 WYSIWYG 编辑器编辑文本更好，但 LaTeX 是对每个人的强大工具。

因此，你可能需要运行 LaTeX 来看到输出。此外，LaTeX 具有各种平台。它最大的优点之一是输出看起来专业，因为 LaTeX 是一个工具。然而，你必须编译代码才能看到输出，并可能实验和设置更改文档样式。

#### 04 安装 LaTeX

以下命令改进了你的构建过程：

```bash
sudo apt-get install texlive-full
```

以下软件包已安装且不再需要：`texlive-libs`。使用 `autoremove` 将其删除。

将安装以下额外的包（日志输出）：

```text
tex-base-archaic-common-context-modules-divpingymfmf-cmfont-freefont-artemis-villeker-vanilla-texfont-recommended--recommended-latex-base-recommended-texlive-bibtex-extra-texlive-science-texlive-tools-generic-fonts-recommended-texlive-fonts-extra--recommended-gfs-fonts-texlive-lmodern-fonts-texlive-lmodern-math-texlive-math-extra-texlive-plain-recommended-texlive-plain-extra-texlive-plain-extrabundle-texlive-generic-tex-base-archaic-common-context-common-latex-mystify-texlive-latex-base-texlive-extra-texlive-recommended-texlive-latex-fonts-texlive-fonts-extra-texlive-fonts-recommended-texlive-fonts-common-texlive-fonts-min-texlive-fonts-math-recommended-texlive-fonts-size-texlive-cmigraph-texlive-cmigraph-extra-texlive-graphics-recommended-recommended-recommended-texlive-source-recommended-texlive-source-extra-texlive-source-common-texlive-source-math-texlive-source-size-texlive-recommended-texlive-recommended-extra-texlive-common-texlive-recommended-extra-texlive-common-texlive-recommended
```

## 教程

你现在可以使用以下方法在 LaTeX 中使用 MyCode 样式了。

### 06 创建参考文献

LaTeX 提供了 BibTeX 来处理参考文献。所有的 BibTeX 条目将位于一个名为 `biblist.bib` 的文件中。每个 BibTeX 条目都遵循以下格式：

> @Kernaghan8
>
> author = (Brian W. Kernighan and Robert Pike)
>
> title = (The UNIX Programming Environment)
>
> year = (1983)
>
> isbn = (020193783)
>
> publisher = (Prentice Hall Technical Reference)

```latex
\begin{MyCode}[fontsize=\size{-1}]
#include <stdio.h>
int main (int argc, const char *argv[]) {
    printf("Hello, World!");
    return 0;
}
\end{MyCode}
```

以下 LaTeX 命令用于美化并将参考文献插入到此项目中：

*   `\bibliography`
*   `\addcontentsline{toc}{toc}(Bibliography)`
*   `\bibliography`

如果你将值从 `-1` 更改为 `+1`，代码字体会变大。

### 08 型目录

如果你的书籍较厚，你可能需要在每个章节的开头添加一个小型目录。这段 LaTeX 包代码增加了对小型目录（mini TOC）功能的支持。

应使用以下命令开启或关闭小型目录功能。最后，在每个章节的开头添加主目录。

```latex
\setcounter(minitoc)
```

![](img/2f9ef091d4813dbe86196f7ccfd0107_31_0.png)

#### 2.2 章节

你可以在 LaTeX 代码中这样引用 `Kernighan8`：

> `:Kernighan8`

### 10 包含页眉和页脚

以下 LaTeX 代码生成页面的页眉和页脚。右页 (`RO`) 与左页 (`LE`) 不同。还需要注意的是，每个章节的第一页 (`COI`) 有另一个规则，将页码放在页脚底部，并带有任何页眉信息。

### 07 代码格式化

LaTeX 会生成带有目录、插图列表和表格列表的页面。使用命令创建目录 (TOC)：

```latex
\tableofcontents
```

如果你只想包含章节和节的条目，请在第 6 步中包含以下前缀：

```latex
\setcounter{tocdepth}(1)
```

为了包含插图列表，请插入以下命令：

```latex
\listofffigures
```
