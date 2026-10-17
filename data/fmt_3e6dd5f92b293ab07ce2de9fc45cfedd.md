
LibreOffice 和 OpenOffice 中各个软件的名称是相同的。文字处理器称为 `Writer`，演示文稿称为 `Impress`，表格程序称为 `Calc`，数据库管理程序称为 `Base`，绘图软件称为 `Draw`，还有一个名为 `Math` 的软件包。将 `LibreOffice` 或 `OpenOffice Writer` 与 `Microsoft Word` 相比，你会发现具有许多相同的功能，包括向导、表格、引用和目录标题、拼写和语法检查器、标子、定义宏的能力、邮件合并、脚注/尾注、页眉和页脚。

图 5.6 显示了 `Office Writer`、`Impress` 和 `Calc` 的顶部区域。任何 `Microsoft Office` 用户在学习 `LibreOffice` 或 `OpenOffice` 的等效软件时应该没有困难，尽管 `LibreOffice` 和 `OpenOffice` 看起来更像 `Microsoft Office 2003` 而不是更新的版本，因为它们使用下拉菜单而不是按钮栏菜单，正如你在图 5.6 中所示。

![](img/c3d46558b4f2c37c3a715bd825868fef_199_0.png)

图 5.6 几个 `OpenOffice` 软件。

## 5.4 LATEX

`Linux` 用户经常使用的另一种流行软件是 `LaTeX`；`LaTeX` 是一种文字处理器，但与 `Microsoft Word` 和 `OpenOffice Writer` 不同，它是 WYSIWYG（所见即所得）。相反，在 `LaTeX` 中，格式命令使用特殊序列嵌入在文中，类似于 `html`。例如，要标记一段字符序列应该带有下划线，你会使用 `\underline{text}` 来添加下划线。

要使用 `LaTeX`，你首先需要创建一个文档。通常，你会将其保存为 `.tex` 文档。`Tex` 是 `LaTeX` 调用的一个更原始的程序；因此，你实际上可以使用 `LaTeX` 的 `Tex` 命令。

接下来，给定你的文件，运行文档文件名：

```
latex filename.tex
```

只要没有遇到错误，`LaTeX` 会产生至少一个文件，`filename.dpi`。`dpi` 扩展代表“device indent”，意味着它可以使用其他几个程序处理。其中一个程序是 `dvips` 创建 `postscript` 文件。如今，更常见的是使用 `dvpdf` 创建 `pdf` 版本。

一旦创建了 `pdf`，就可以查看或打印该文件。`LaTeX` 还会生成其他文件，包括 `filename.log` 和 `filename.aux`。`log` 文件包含 `LaTeX` 生成的注释，而 `aux` 文件可能包含任何错误信息。

`LaTeX` 的另一个功能是方便插入参考文献。首先，创建多个参考文献，称为 `bibtex` 文件。这些文件包含了你在任何文档中可能引用的信息。`bibtex` 文件中的参考文献将包含作者、标题、书或期刊名称、卷、页码、编辑和地址等信息。每个条目之前都有引用类型，如 `article`、`book` 或 `collection`。以下是一个文章条目的示例。

`# Linux 应用 ■ 173`

### 表格 5.2 常用 `LaTeX` 命令

| 命令 | 含义 | 示例用法 |
| :--- | :--- | :--- |
| `\documentstyle` | 修改文档类型 | `\documentstyle[twocolumn][book]` |
| `\author` | 作者姓名以较小字体居中 | `\author[Richard Fox and Frank Zappa]` |
| `\chapter[], \section[], \subsection[], \part` | 创建文档章节，标题大小和编号由类型决定 | `\chapter[How to Use LaTeX]\section(Starting Your Document)\subsection[]` |
| `\begin{tabular}{...}... \end{tabular}` | 创建带有带有 | `\{tabular}{l|r]` |
| `\maketitle` | 用于生成标题页 | |
| `\newline, \linebreak, \nobreak` | 插入新行或允许在此处换行，不允许换行 |
| `\parindent{}, \textwidth{}` | 设置段落缩进和页边距 | `\parindent{.3in}\textwidth{1in}` |

```latex
\documentclass{report}
\begin{document}
\begin{center}文档标题\end{center}
\vspace{2pc}
这是一个句子。这是第二个句子。这是第三个句子。这是第四个句子。这是一个段落的结束。

这是一个新段落。两个段落之间的空行表示新段落。看它是如何自动缩进的？我们也可以防止缩进。\noindent 我们在不缩进的情况下开始一个新段落。这是非缩进段落的另一个句子。

现在我们有了另一个缩进的段落。让我们看一下列表。

\begin{itemize}
\item 第一个项目
\item 第二个项目
\item 第三个项目
\end{itemize}

这非常像 html。我们在需要格式化的单词周围指定格式，如 {\it 斜体文本}，{\bf 粗体字体}或 \underline{下划线文本}。

\end{document}
```

我们在不缩进的情况下开始一个新段落。这是非缩进段落的另一个句子。
现在我们有了另一个缩进的段落。让我们看一下列表。

- `*` 第一个项目
- 第二个项目
- 第三个项目

这非常像 `html`。我们在需要格式化的单词周围指定格式，例如*斜体文本*、**粗体字体**或*下划线文本*。

图 5.7 `LaTeX` 文件（顶部）和生成的文档（底部）。

条目的顺序（`article`、标题等）并不重要，且取决于条目的类型，某些字段是可选的，例如文章的卷号（`volume`）。请注意 `fox2010` 是我们在 `LaTeX` 文件中使用的标签。

```bibtex
@article{fox2010,
  author={Fox, R. and Zappa, F.},
  title={Using Linux to Dominate Mankind},
  journal={The Linux Journal},
  volume = {March,
  year = 2010,
  pages = {85-93}
}
```

在你的 `LaTeX` 文档中，通过 `\cite` 命令引用参考文献条目，如 `\cite(fox2010)` 或 `\cite(fox2010,keneally2008,mars2012)`。你还必须通过 `\bibliography{filename}` 命令指定参考文献列表的位置。文件名是与你的 `LaTeX` 文件在同一目录下的一个或多个 `bibtex` 文件。这些文件预计以 `.bib` 结尾，例如 `myrefs.bib`。你也可以插入一个 `\ographystyle{type}` 来指定参考文献的类型。样式类型可以使用 `aai-`、`abbrev`、`abstract`、`acm`、`alpha`、`apa`、`bba`、`chicago`、`klauwer`、`plain` 等（仅为列举）。

一旦你处理了 `LaTeX` 文件，在创建 `ps` 或 `pdf` 文件之前，你需要处理参考文献。这是通过命令 `bibtex filename` 完成的，其中 `filename` 是你的 `LaTeX` 文件的文件名。参考文献条目将以方括号 `[]` 显示在你的文档中，并根据所选的格式类型存储作者的名字或缩写。例如，一个引用可能是 `[5]` 或 `[fox13]`。

## 5.5 加密软件

在本节中，我们将检查 `Linux` 中可用的加密软件，如 `openssl` 和其他支持工具。在查看软件之前，让我们先考虑什么是加密以及我们为什么要使用它。

### 5.5.1 什么是加密？

加密是将信息转换为字符字符串形式（无论是 `ASCII`、`Unicode`、二进制或其他形式）并通过某些代码对其进行更改的过程。如果编码的消息被截获，该信息将变得难以理解。加密和解密分别是将信息获取并将其放入编码格式，以及获取编码消息并恢复其原始形式的翻译过程。

我们希望在通信中应用加密，以确保诸如密码、信用卡号和机密文本信息等信息在通信过程中被截获时无法被查看。这是必要的，因为互联网的设计初并不是为了以安全的形式广播信息。我们可能会对计算机上的数据文件进行加密，以防它们落入他人手中。

一旦加密，信息应该处于一种几乎无法破解的代码中。若要让一个人能够在没有代码的情况下查看原始信息，该人必须尝试破解代码。这可能需要尝试代码的所有排列。这种尝试破解代码的行为被称为暴力破解（`brute-force approach`）。此类攻击所需的组合数量取决于加密算法。今天使用的最好的加密算法可能需要几十台超级计算机花费超过 `10^8`（十亿年）的时间才能破解。

## 带有操作系统概念的 `Linux`
