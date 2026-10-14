

## 16.4.1 它是 TeX 还是 LaTeX 文件？

处理 TeX 和 LaTeX 文件的命令是分开的，而且不能互换，所以当你想处理一个 TeX 或 LaTeX 输入文件时，应该先确定其格式。

按照惯例，TeX 文件总是具有 `.tex` 文件名扩展名。LaTeX 输入文件有时会使用 `.latex` 或 `.ltx` 文件名扩展名，但并非总是如此——判断一个 `.tex` 文件是否实际采用 LaTeX 格式的一种方法是使用 grep 在文件中搜索文本 `\document`，每个 LaTeX 文档（而不是 TeX 文档）都会有它。所以如果它输出任何匹配的行，你就有一个 LaTeX 文件。 （与 grep 一起使用的正则表达式是 `\document`，因为反斜杠字符必须用两个反斜杠指定。）

- 要确定文件 `gentle.tex` 是 TeX 还是 LaTeX 文件，输入：

```
$ grep '\\document' gentle.tex RET
$
```

在这个例子中，grep 没有返回任何匹配项，因此可以安全地假设 `gentle.tex` 是一个 TeX 文件而不是 LaTeX 文件。

NOTE: 有关 grep 和搜索正则表达式的更多信息，请参阅 Regular Expressions—Matching Text Patterns。

## 16.4.2 处理 TeX 文件

使用 tex 来处理 TeX 文件。它以要处理的 TeX 源文件名作为参数，并以与源文件相同的基文件名写入 DVI（“DeVice Independent”）格式的输出文件，但扩展名为 `.dvi`。

## 16.4.3 处理 LaTeX 文件

latex 工具的工作方式与 tex 相同，但用于处理 LaTeX 文件。

- 要处理 LaTeX 文件 `lshort.tex`，输入：

```
$ latex lshort.tex RET
```

此命令会写入一个名为 `lshort.dvi` 的 DVI 输出文件。

你可能需要连续多次运行 latex 处理一个文件。LaTeX 文档有时会有索引和交叉引用，由于 LaTeX 的工作方式，需要经过 latex 两次（在极少数情况下三次或更多次）处理才能完全处理。 如果你需要多次运行 latex 处理文件以生成正确的引用，你会在第一次处理后在 latex 处理输出中看到一条消息，指示你再次处理它。

- 为确保 `lshort.tex` 中的所有交叉引用都已正确生成，再次将输入文件通过 latex 运行一次：

```
$ latex lshort.tex RET
```

`lshort.dvi` 文件将被重写为包含交叉引用和索引条目中正确页码的更新版本。然后你可以像前一个处理 TeX 文件的配方中所述那样查看、打印或转换此 DVI 文件。

- 要处理文件 `gentle.tex`，输入：

```
$ tex gentle.tex RET
```

一旦你用此方法生成了 DVI 输出文件，你可以对其执行以下操作：

- 使用 xdvi 在屏幕上预览它；请参阅 Previewing a DVI File
- 使用 dvips 或 lpr 打印它；请参阅 Printing with Dvips
- 使用 dvips 将其转换为 PostScript；请参阅 Preparing a DVI File for Printing； （然后，你还可以将 PostScript 输出转换为 PDF 或纯文本）

## 16.4.4 使用 TeX 和 LaTeX 编写文档

@ssf (WWW): ftp://ctan.tug.org/tex-archive/documentation/gentle.tex
@ssf (WWW): ftp://ctan.tug.org/tex-archive/documentation/lshort/

要使用 TeX 或 LaTeX 创建文档，你通常使用你喜欢的文本编辑器编写包含以 TeX 或 LaTeX 格式化的文本的输入文件。然后，你处理此 TeX 或 LaTeX 输入文件以创建 DVI 格式的输出文件，你可以预览、转换或打印它。

程序员在介绍一种编程语言时，常常会给出一个简单的程序，只输出文本 `Hello, world' 到屏幕；这样的程序通常足够详细，可以让不熟悉该语言的人了解其基本语法。

我们可以用 TeX 和 LaTeX 等文档处理语言做同样的事情。以下是 TeX 文档的“Hello, world”：

```
Hello, world
\end
```

如果你用 tex 处理此输入文件，它将输出一个 DVI 文件，其中以默认 TeX 字体、默认页面大小和默认边距显示文本 `Hello, world'。

以下是 LaTeX 的相同“Hello, world”：

```
\documentclass{article}
\begin{document}
Hello, world
\end{document}
```

尽管 TeX 示例要简单得多，但 LaTeX 通常更容易“开箱即用”地用于编写某些结构化文档——例如通信和文章——因为它附带了预定义的文档类，可控制文档包含的结构元素的标记(27)。另一方面，Plain TeX 更适合更实验性的布局或专用文档。

TeX 和 LaTeX 标记语言各值一本书，提供其使用的介绍已远远超出了本文的范围。要学习如何为它们编写输入，我建议两本优秀的教程，Michael Doob 的 A Gentle Introduction to TeX，以及 Tobias Oetiker 的 The Not So Short Introduction to LaTeX——每本都可在上述 URL 的 WWW 上获得。这些文件分别采用它们所描述的格式；为了阅读它们，你必须首先像前面两个配方中所述那样处理这些文件。

格式良好的 LaTeX 文档可在许多 Linux 系统上安装在 `/usr/share/texmf/doc/latex/latex2e-html/` 目录中找到；使用 lynx 浏览器查看它（请参阅 Browsing Files）。

一些其他排版系统，例如 LyX、SGMLtools 和 Texinfo（都在本书其他地方描述）

