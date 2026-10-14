
PostScript 编程语言由 Adobe Systems 的 John Warnock 在 20 世纪 80 年代初设计并实现，用于描述“页面”的外观。页面通常是一张物理纸（PostScript 常用于将文档发送到打印机硬件），但它们可以是任何类型的输出显示器.¹PostScript 文件是文本文件，包含 PostScript 语言命令，用于绘制要在页面上打印的图像。

与普通纯文本文件一样，PostScript 文件在互联网上十分常见（并被商业打印机使用），因为使用纯文本，它们可以轻松地跨平台和硬件共享。同一个 PostScript 文件可以输出到高端显示器或低端打印机，并达到该硬件的最佳性能。PostScript 是一种紧凑且优雅的格式。

虽然可以直接用 PostScript 语言进行编写（有些人已经精通 PostScript 编程），但有许多工具和应用程序可以在文件与 PostScript 之间进行转换，因此你不需要自己编写。请参见 Recipe 15.2 [输出到 PostScript]，第 359 页，了解将纯文本转换为 PostScript 的方法。

GNU Ghostscript 是 PostScript 语言的免费解释器。²它带有 `gs`，这是一个用于将文件从 PostScript 或 PDF 转换为其他格式的工具。它通常用于用于非 PostScript 打印机（见 Recipe 25.3.1 [为打印准备 PostScript 文件]，第 518 页）。`ghostview` 工具用于在屏幕上查看 PostScript 文件（见 Recipe 17.4.2 [预览 PostScript 文件]，第 414 页）。

EPS，或封装的 PostScript（Encapsulated PostScript），是一种描述页面内方框内容的格式。EPS 文件可以嵌入到 PostScript 文件的页面中，因此在向文档中插入插图时经常使用（例如，*Cookbook*（食谱）中打印的所有插图都是 EPS 文件）。你可以像处理 PostScript 文件一样查看和打印 EPS 文件。

本章包含了格式化和处理 PostScript 文件的配方。配方分为两类：一种针对 PostScript 文件中的单个逻辑页面（文件中的数字页，但不一定是输出的物理页），另一类则针对整个文件。

> ¹ PostScript 最初是为 Apple LaserWriter 打印机设计的；新闻是 Sun Microsystems 开发的一种 UNIX 窗口系统，使用 PostScript 绘制显示内容。

> ² 它也是 Adobe 可便携文档格式（PDF）语言的解释器。

本章中使用的许多工具都是 Angus Duggan 的 `psutils`（“PostScript 工具”）包的一部分提供的。这些工具可以用于本章描述之外的其他用途；更多细节请参见它们各自的手手册（man pages）。

## 20.1 处理 PostScript 页面

这些配方针对 PostScript 文件的单个页面，而不是文件本身。

### 20.1.1 将 DVI 页面提取为 PostScript

```
DVIPS
DEB: tetex-bin
RPM: tetex-dvips
WWW: http://www.radicaleye.com/dvips.
```

要从 DVI（“设备无关”）文件中提取特定页面到 PostScript，请使用 `dvips` 并通过 `-pp` 选项提供要输出的页码或连字符页码范围。

- 要仅从 `abstract.dvi` 文件中提取第一页并将 PostScript 输出发送到打印机，输入：

```
$ dvips -ppi abstract.dvi RET
```

默认情况下，`dvips` 将输出到打印机；若要将 PostScript 输出保存到文件，请指定用于输出的文件作为 `-o` 选项的参数。

- 要将 `abstract.dvi` 文件的第 137 到 146 页作为 PostScript 输出，并写入 `abstract.ps` 文件，输入：

```
$ dvips -ppi137-146 -o abstract.ps abstract.dvi RET
```

### 20.1.2 从 PostScript 文件中提取页面

```
PSUtils
DEB: psutils
RPM: psutils
WWW: http://www.ctan.org/tex-archive/support/psutils/
```

使用 `psselect` 从 PostScript 文件中选择页面；当你提供输入文件时，它会输出一个包含指定页面的新 PostScript 文件。输出被发送到标准输出或第二个参数指定的文件。

将要选择的页面作为 `-p` 选项的参数；你可以列出单页和用逗号分隔的页码范围。使用两个用连字符分隔的数字表示范围；因此，“4-6”指定从第四页到第六页（包含在内）。如果你省略页码对中的第一个数字，则假设为第一页；如果省略最后一个数字，则假设为最后一页。页面按照指定的顺序写入新文件。

⇒ 以下是使用此工具的一些方法。

- 从 `newsletter.ps` PostScript 文件中选择第 47 页并输出到 `selection.ps` 文件，输入：

```
$ psselect -p47 newsletter.ps selection.ps RET
```

- 要从 `newsletter.ps` 文件中选择前十页、第 104 页、第 23 到 28 页以及第 2 页并写入 `selection.ps` 文件，输入：

```
$ psselect -p1-10,104,23-28,2 newsletter.ps selection.ps RET
```

折叠并装订的；在文档中，这些页面通常不是顺序顺序的（例如，在一个八页一订的文档中，第 8 页和第 1 页可能打印在同一张纸上）。

要按订码（signature）重新排列 PostScript 文件的页面——通常用于将文件打印成书籍或小册——请使用 `psbook`。提供要读取的 PostScript 文件名和输出文件名作为参数；`psbook` 会读取文件内容，重新排列页面，然后将 PostScript 输出写入第二个文件。

+   → 要将文件 `newsletter.ps` 的页面重新排列为订码并写入 `newsletter.bound.ps`，请输入：

```
$ psbook newsletter.ps newsletter.bound.ps RET
```

默认情况下，`psbook` 对整个文件使用一个订码。如果文件页数不是 4 的倍数，它会在末尾添加空白页。

要指定要使用的订码大小——换句话说，单张纸上显示的页数——请将数字作为 `-s` 选项的参数。订码大小始终是 4 的倍数。

+   → 要将文件 `newsletter.ps` 的页面重新排列为八页订码并写入 `newsletter.bound.ps`，请输入：

```
$ psbook -s8 newsletter.ps newsletter.bound.ps RET
```

## 20.2 处理 PostScript 文档

这些配方适用于整个 PostScript 文档。

### 20.2.1 调整 PostScript 文档的大小

PSUtils

DEB: psutils

RPM: psutils

WWW: http://www.ctan.org/tex-archive/support/psutils/

使用 `psresize` 调整 PostScript 文档的大小。它需要要调整的文件和输出文件作为参数；否则，它将从标准输入读取并写入标准输出。如果你提供了输出文件名，则必须指定要使用的页面大小，格式与 `psnu` 工具相同：使用 `-p` 或 `-h` 和 `-w` 指定输出文件的大小，使用 `-P` 指定输入文件的大小（参见配方 20.1.3 [合并 PostScript 页面]，第 455 页）。

⇒ 要将 PostScript 文件 `double.ps` 调整为美国信纸大小（letter-sized），并将输出写入新文件 `double.ps`，请输入：

```
$ presize -pletter double.ps doublet.ps RET
```

### 20.2.2 合并 PostScript 文档

将多个 PostScript 文件连接并合并到一个文件中有两种值得介绍的方法。一种是更健壮的解决方案，另一种更易于输入。我将从首选的方法开始，这是我在合并本书的 PostScript 页面时发现的。

# 方法 #1

+   Ghostscript

DEB: gs-common

gs

RPM: ghostscript

WWW: http://www.cs.wisc.edu/~ghost/
