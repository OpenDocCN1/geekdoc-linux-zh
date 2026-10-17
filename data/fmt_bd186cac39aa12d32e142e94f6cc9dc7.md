
使用 `ps2txt` 将 PostScript 文件转换为纯文本。将读取的 PostScript 文件名和写入的文本文件名作为参数提供。

- 要从输入文件 `'sutra.ps'` 制作文本文件 `'sutra.txt$`，输入：

  `$ ps2txt sutra.ps sutra.txt RET`

此命令写入一个名为 `'sutra.txt'` 的新文件。原始文件 `'sutra.ps'` 不会被更改。

## 第五部分：声音

## 声音

默认情况下，`psbook` 对整个文件使用书订页。如果文件页数不是 4 的倍数，它会在末尾添加空白页。

要指定使用的书订页大小——换句话说，单张纸上显示的页数——请将数字作为 `'-s'` 选项的参数。书订页大小始终是 4 的倍数。

- 要将文件 `'newsletter.ps'` 中的页面重新排列为八面书订页并将其写入 `'newsletter.bound.ps$`，请输入：

```
$ psbook -s8 newsletter.ps newsletter.bound.ps RET
```

## 20.2 操作 PostScript 文档

这些食谱针对整个 PostScript 文档的操作。

### 20.2.1 调整 PostScript 文档的大小

使用 `psresize` 调整 PostScript 文件的大小。它接受需要调整的文件和写入的输出文件作为参数；你还必须指定输出文件的页面大小，使用与 `pspage` 工具相同的格式：使用 `'-p'` 或 `'-h'` 和 `'-w'` 指定输出文件的大小，并使用 `'-P'` 指定输入文件的大小（请参见食谱 20.1.3 [合并 PostScript]，第 237 页）。

- 要将 PostScript 文件 `'double.ps'` 调整为美国信纸（US letter）尺寸，并将输出写入新文件 `'double.ps$`，请输入：

```
$ pletter double.ps double.ps RET
```

### 20.2.2 合并 PostScript 文档

使用 `psmerge` 将多个 PostScript 文件串联并合并为一个文件。将要合并的文件名作为参数提供，`psmerge` 会按照给定的顺序将它们输出到标准输出。你还可以使用 `'-o'` 选项指定输出文件名（不要在文件名和选项之间留任何空格）。

- 要将文件 `'slide1.ps'`、`'slide2.ps'` 和 `'slide3.ps'` 合并为一个新的 PostScript 文件 `'slideshow.ps$`，请输入：

```
$ psmerge -oslidehow.ps slide1.ps slide2.ps slide3.ps RET
```

注意：在编写时，`psmerge` 仅适用于使用相同应用程序制作的 PostScript 文件——这意味着例如，你可以合并多个用 TeX 创建的文件，或合并多个用 xfig 创建的文件，但不能将它们混合。

### 20.2.3 排版 PostScript 文档以制作小册

要排列 PostScript 文件中的页面以制作小册，首先使用 `psbook` 将页面重新排列为书订页，使用 `psup` 排列页面——在横模式下每页打印两个页面——然后使用 `pstop` 输出所有的奇页，然后是偶页。

# 第 20 章：PostScript

正确执行此操作的技巧是首先准确确定你需要做什么，然后计算用于 `ppstops` 的正确测量值。

- 从文件 `newsletter.ps` 制作小册：

  1. 将页面重新排列为书订页：

     `$ psbook newsletter.ps newsletter.signature.ps RET`

  2. 将两个页面横向放置在一页上，缩小为原始尺寸的 70%（全部写在一行）：

     `$ psnup -1 -pletter -2 -s.7 newsletter.signature.ps > newsletter.2up.ps RET`

  3. 输出奇页：

     `$ pstops "2:0(1in,0in)" newsletter.2up.ps > odd.ps RET`

  4. 输出偶页：

     `$ pstops "2:-1(1in,0in)" newsletter.2up.ps > even.ps RET`

然后，将打印小册的 `odd.ps` 打印机，将打印好的页面放入手动进纸器，并将 `even.ps` 发送到打印机。这会将奇、偶页打印在纸张的正反面。

- 从使用纵向信纸尺寸的文件开始，制作一个横向信纸尺寸的双面小册，请输入：

```
$ psbook input.ps > temp1.ps RET
...processing messages...
$ psnup -1 -pletter -2 -s.7 temp1.ps > temp2.ps RET
...processing messages...
$ pstops "2:0(1in,0in)" temp2.ps > odd.ps RET
...processing messages...
$ pstops "2:-1(1in,0in)" test2.ps > even.ps RET
...processing messages...
$
```

## 20.3 转换 PostScript

这些食谱展示了如何将 PostScript 文件转换为其他格式。另见准备打印用 PostScript 文件的食谱，食谱 25.3.1 [准备打印用 PostScript 文件]，第 275 页。

### 20.3.1 将 PostScript 转换为 PDF

使用“Ghostscript”软件包中的 `ps2pdf` 将 PostScript 文件转换为 PDF。将要读取的 PostScript 文件名和要写入的 PDF 文件名作为参数提供。

- 要从输入文件 `sutra.ps` 制作 PDF 文件 `sutra.pdf$`，输入：

  `$ ps2pdf sutra.ps sutra.pdf RET`

此命令写入一个 PDF 格式的名为 `'sutra.pdf'` 的新文件。原始文件 `'sutra.ps'` 不会被更改。**注意**：为了制作 PDF，请确保安装了 `gs` 6.0 或更高版本。

### 20.3.2 将 PostScript 转换为纯文本

使用 `ps2txt` 将 PostScript 文件转换为纯文本。将要读取的 PostScript 文件名和要写入的文本文件名作为参数提供。

- 要从输入文件 `'sutra.ps'` 制作文本文件 `'sutra.txt$`，输入：

  `$ ps2txt sutra.ps sutra.txt RET`

此命令写入一个名为 `'sutra.txt'` 的新文件。原始文件 `'sutra.ps'` 不会被更改。

## 第五部分：声音

## 声音

默认情况下，`psbook` 对整个文件使用书订页。如果文件页数不是 4 的倍数，它会在末尾添加空白页。

要指定使用的书订页大小——换句话说，单张纸上显示的页数——请将数字作为 `'-s'` 选项的参数。书订页大小始终是 4 的倍数。

- 要将文件 `'newsletter.ps'` 中的页面重新排列为八面书订页并将其写入 `'newsletter.bound.ps$`，请输入：

```
$ psbook -s8 newsletter.ps newsletter.bound.ps RET
```

## 20.2 操作 PostScript 文档

这些食谱针对整个 PostScript 文档的操作。

### 20.2.1 调整 PostScript 文档的大小

使用 `psresize` 调整 PostScript 文件的大小。它接受需要调整的文件和写入的输出文件作为参数；你还必须指定输出文件的页面大小，使用与 `pspage` 工具相同的格式：使用 `'-p'` 或 `'-h'` 和 `'-w'` 指定输出文件的大小，并使用 `'-P'` 指定输入文件的大小（请参见食谱 20.1.3 [合并 PostScript]，第 237 页）。

- 要将 PostScript 文件 `'double.ps'` 调整为美国信纸（US letter）尺寸，并将输出写入新文件 `'double.ps$`，请输入：

```
$ pletter double.ps double.ps RET
```

### 20.2.2 合并 PostScript 文档

使用 `psmerge` 将多个 PostScript 文件串联并合并为一个文件。将要合并的文件名作为参数提供，`psmerge` 会按照给定的顺序将它们输出到标准输出。你还可以使用 `'-o'` 选项指定输出文件名（不要在文件名和选项之间留任何空格）。

- 要将文件 `'slide1.ps'`、`'slide2.ps'` 和 `'slide3.ps'` 合并为一个新的 PostScript 文件 `'slideshow.ps$`，请输入：

```
$ psmerge -oslidehow.ps slide1.ps slide2.ps slide3.ps RET
```
