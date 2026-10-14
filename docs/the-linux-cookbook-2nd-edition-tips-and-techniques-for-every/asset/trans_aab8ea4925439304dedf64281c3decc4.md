
documents.（LaTeX 可能比纯 TeX 格式的日常使用更频繁，但在我的经验中，每种格式在不同情况下都有用。）

“TeX”不是读作牛仔的名字，“LaTeX”也不是读作一种油漆：字母“T”、“E”和“X”代表希腊字符 tau、epsilon 和 chi（源自希腊语 techne，意为“艺术与科学”）。因此“TeX”中的最后一个音与“Bach”中的最后一个音相同，而“LaTeX”根据当地口音，发音为“lay-tek”或“lah-tek”。那些精通使用该系统的人 Knuth 称之为 TeXnicians。

TeX 及相关程序（包括 Metafont；参见 Recipe 16.5 [Using Other Font Tools]，第 403 页）的集体家族有时被称为“TeX and friends”，它们总是保存在名为 texmf 的目录中。例如，随裸 TeX 系统提供的补充文件保存在 /usr/lib/texmf 目录树中。

下面的配方描述了如何开始为 TeX 编写输入以及如何处理这些文件以便查看和打印。虽然不是每个人都想或需要用 TeX 和 LaTeX 编写文档，但这些格式被广泛使用——尤其是在 Linux 系统上——因此每个 Linux 用户都有可能遇到其中一个文件，并且应该知道如何处理它们。

## 15.3.1 Distinguishing Between TeX and LaTeX Files

处理 TeX 和 LaTeX 文件的命令是分开的，而且不可互换，因此当你想处理 TeX 或 LaTeX 输入文件时，应首先确定其格式。

按照惯例，TeX 文件始终具有 .tex 文件名扩展名。LaTeX 输入文件有时具有 .latex 或 .ltx 文件名扩展名，但并非总是如此——判断一个 .tex 文件是否实际上是 LaTeX 格式的一种方法是使用 grep 在文件中搜索文本“\document”，每个 LaTeX（而非 TeX）文档都会有它。因此，如果搜索输出任何匹配的行，你就有一个 LaTeX 文件。（与 grep 一起使用的正则表达式是“\document”，因为反斜杠字符必须用两个反斜杠指定。）

⇒ 要确定文件 smith.tex 是 TeX 还是 LaTeX 文件，输入：

```
$ grep '\document' smith.tex [RET]
\documentclassletter
$
```

在此示例中，grep 返回了一个匹配项，因此可以安全地假设 smith.tex 是一个 LaTeX 文件（“letter”文档类），而不是 TeX 文件。

NOTES：有关正则表达式和用 grep 搜索的更多信息，请参阅 Recipe 14.3 [Regular Expressions—Matching Text Patterns]，第 335 页。

## 15.3.2 Processing a TeX File

使用 tex 处理 TeX 文件。它以要处理的 TeX 源文件名作为参数，并以与源文件相同的基文件名写入输出文件，但扩展名为 .dvi，格式为 DVI（“DeVice Independent”）。

⇒ 要处理文件 gentle.tex，输入：

```
$ tex gentle.tex [RET]
```

一旦你用此方法生成了 DVI 输出文件，你可以对其执行以下任何操作：

- 使用 xdvi 在屏幕上预览它；参见 Recipe 17.4.1 [Previewing a DVI File]，第 413 页。
- 使用 dvips 或 lpr 打印它；参见 Recipe 25.2.5 [Printing a DVI File]，第 515 页。
- 使用 dvips 将其转换为 PostScript；参见 Recipe 25.3.2 [Preparing a DVI File for Printing]，第 520 页；然后，你还可以将 PostScript 输出转换为 PDF 或纯文本。

## 15.3.3 Processing a LaTeX File

latex 工具的工作方式与 tex 相同，但用于处理 LaTeX 文件。

⇒ 要处理 LaTeX 文件 lshort.tex，输入：

```
$ latex lshort.tex [RET]
```

此命令会写入一个名为 lshort.dvi 的 DVI 输出文件。

你可能需要连续多次运行 latex 处理一个文件。LaTeX 文档有时会有索引和交叉引用，由于 LaTeX 的工作方式，需要经过 latex 两次（在极少数情况下三次或更多次）处理才能完全处理。如果需要多次运行文件以生成正确的引用，你将在 latex 处理输出中看到一条消息，指示你再次处理它。

