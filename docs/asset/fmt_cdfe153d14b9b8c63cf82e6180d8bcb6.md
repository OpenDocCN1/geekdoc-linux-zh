
一个典型的 `gs` 安装可以写入 100 多种不同的打印设备，包括 HP Laser Jet 4 打印机（`ljet4`）、HP Color Desjets（`cdsketch`）和第 4 页传真（`tiff4`）。较新版本的 `gs` 对新打印机有更好的支持，如果你有新型号打印机，请确保安装了最新版本。

`gs` 将要转换的文件作为参数；将输出输出设备作为 `-sDEVICE=` 选项的参数；将要写入的文件作为 `-sOutputFile=` 选项的参数。

可以使用另外两个选项：`-dSAFER`（它防止意外删除或覆盖文件）以及 `-dNOUSE`（它会关闭页与页之间的暂停）。

转换完成后，输入 `quit` 退出。

- ⇒ 要将 PostScript 文件转换为适用于 `cdj50` 打印机的格式，请输入：

```
$ gs -sDEVICE=cdj50 -sOutputFile=tiger.dj -dSAFER -dNOUSE < /dev/null
```

此命令写入 `tiger.dj`，你可以通过 `lpr` 将其发送到打印机。打印一个 PostScript 文件。

### 25.3.2 为打印准备 DVI 文件

```
DVIPS
DEB: tetex-bin
RPM: tetex
WWW: http://www.radical.com/dvps.html
```

要将 DVI 格式的文件转换为 PostScript，使用 `dvips`。它接受文件作为参数；将文件名作为 `-o` 选项的参数。

输出 DVI 文件的特定页，将它们作为 `-pp` 选项的参数。

⇒ 这里有一些使用方法：

- 要输出 DVI 的第 14 和第 36 页，输入：

```
$ dvips -pp14,36 -o-.ps buffer
```

- 要输出 DVI 的第 2 到 100 页，输入：

```
$ dvips -pp2-100 -o-.ps buffer
```

- 要输出 DVI 的第 1 页和第 5 到 20 页，输入：

```
$ dvips -pp1,5-20 -o-.ps buffer
```

要指定输出纸张尺寸，将它作为 `-t` 选项的参数；如果你有一台 PostScript 打印机，也可以直接将输出发送到打印机（参见食谱 25.2.5 [打印 DVI 文件]，第 515 页）。

- ⇒ 以 `legal` 纸张尺寸将 `buffer` 输出为 PostScript 文件，输入：

```
$ dvips -t legal -o-.ps buffer
```

- 要以横向模式输出 `buffer`，输入：

```
$ dvips -t landscape buffer
```

- ⇒ 要从 `buffer` 生成 PDF，输入：

```
$ dvips -pdf -oabstract.pdf buffer
```

此命令创建一个 PDF 格式的新文件 `abstract.pdf`。注意：这种转换不仅适用于打印准备。一旦 DVI 文件转换为 PostScript，你就可以将 PostScript 转换为其他格式，如纯文本或 PDF——参见食谱 20.3 [转换 PostScript]，第 459 页。

## 25.3 为打印准备 PDF 文件

```
Xpdf
DEB: xpdf-common
xpdf-reader
RPM: xpdf
WWW: http://www.foools.com/xpdf/

Ghostscript
DEB: gs-common
g
RPM: ghostscript
WWW: http://www.cs.wisc.edu/~ghost/
```

至少有两种方法可以转换并打印 Adobe 便携文档格式（PDF）文件，该文件通常以 `.pdf` 扩展标记。

第一种方法是在 `xpdf`（PDF 视视器）中查看文件，然后左点击打印机图标。这不会真的将文件发送到打印机，但会在同一目录下写入一个 PostScript 文件，其文件名与 PDF 文件相同，但扩展名为 `.ps`。你可以通过 `lpr` 打印此文件，或将其转换为其他格式（参见食谱 25.3.1 [为打印准备 PostScript 文件]，第 518 页）。

有很多方法可以为打印准备文本。你可以对文本进行分页并控制其他格式，正如第 13 章[格式化文本]第 305 页所示。然后，你可以使用 `encript` 将文本转换为 PostScript 并进行打印。这非常适合使用特定字体打印文本；你还可以选择某些页面进行打印，包括页码范围，或者仅打印偶数页或奇数页。

# 第 25 章：打印

在准备 etexts 打印时，有两个值得注意的方法。

## 方法 #1

### Etext 过滤器

WWW: http://dsl.org/comp/enscript/

使用 `encript` 的 `etext` 过滤器将 etext 转换为 PostScript。这会读取一个使用 etext 规范编写的纯文本文件（包括 etext 风格的斜体，参见配方 13.9 [下划线文本]第 327 页），转换斜体，并写入一个 PostScript 文件作为输出。

- ⇒ 要将 etext `youth.txt` 转换为 PostScript，请输入：

```
$ enscript -Eetext -B f "Times-Roman12" -o youth.ps txt RET
```

## 方法 #2

### Txt2html

```
DEB: txt2html
RPM: txt2html
WWW: http://txt2html.sourceforge.net/
```

要将纯文本转换为 PostScript 用于打印——无论文本是否是按照 etext 规范编写——先使用 `txt2html` 将文本转换为 HTML，然后从 Web 浏览器中打印文本，如配方 25.2.4 [打印网页]第 514 页所示。

- ⇒ 要为打印准备文件 `essays`，请输入：

```
$ txt2html essays > essays.html RET
```

此命令会写入一个新文件 `essays.html`，你可以用 Web 浏览器对其进行打印。

备注：你也可以使用 `txt2tex` 将文本转换为 LaTeX（参见配方 15.7 [使用其他文字处理器和排版系统]第 391 页）。

# 跨平台转换

有时，这种情况是不可避免的——并非出于你的选择，你必须处理来自另一个操作系统的磁盘，或者存储在这些系统专有格式的文件。

本章的配方关于从其他平台转换数据——读取来自 DOS、Windows 和 Macos 系统的磁盘，以及转换 DOS 文本和 Microsoft Word 文件。

要转换图像文件格式，请参见配方 18.2 [转换图像文件]第 432 页；要转换音频文件格式，请参阅配方 23.3 [转换声音文件]第 493 页。

## 26.1 使用 DOS 和 Windows 磁盘

### Mtools

```
DEB: mtools
RPM: mtools
WWW: http://mtools.linux.lu/
```

mtools 包提供了一系列工具，方便操作 MS-DOS 文件。这些工具允许你在无需挂载 MS-DOS 文件（通常是软盘，但也支持 Jaz 和 Zip 驱动器）的情况下使用并操作它们；它们处理不同的 Microsoft Windows 操作系统（包括 Windows NT）所使用的 MS-DOS格式扩展。

以下配方介绍了如何使用该包中的某些工具获取 MS-DOS 磁盘的目录列表、在磁盘之间复制文件、删除磁盘上的文件，甚至对其进行格式化。它们用法和语法与相应的 MS-DOS 命令相似。

你也可以挂载 DOS 和 Windows 磁盘（参见配方 26.3 [挂载 Windows 和 NT 分区]）第 529 页。

### 26.1.1 列出 DOS 磁盘的内容

使用 `mdir` 获取 dos 磁盘的目录列表。将 DOS 使用的磁盘“驱动器号”作为参数提供。例如，要指定主软驱器，使用 `A:` 作为读取驱动器，并使用 `B:` 指定次软驱器。

- ⇒ 要获取主软盘中当前 DOS 磁盘的目录列表，请输入：

```
$ mdir a: RET
```

### 26.1.2 在 DOS 磁盘之间复制文件

使用 `mcopy` 从 DOS 磁盘中复制文件。

要将文件复制到 DOS 磁盘，将要复制的文件名和目标磁盘的“驱动器号”作为参数。

- ⇒ 要将文件 `readme.txt` 复制到主软盘中的 DOS 磁盘，请输入：

```
$ mcopy readme.txt a: RET
```

从 DOS 磁盘复制文件，提供源磁盘的“驱动器号”，后跟要复制的文件名，无需其他参数；`mcopy` 将将指定的文件复制到当前目录。

- ⇒ 要从次软盘中的 DOS 磁盘将 `resume.doc` 复制到当前目录，请输入：

```
$ mcopy b:resume.doc
```

要从 DOS 磁盘复制所有文件，只需提供“驱动器号”而无需文件名。

- ⇒ 要将主软盘中 DOS 磁盘的所有文件和目录复制到当前目录，请输入：

```
$ mcopy a: RET
```

### 26.1.3 删除 DOS 磁盘上的文件
