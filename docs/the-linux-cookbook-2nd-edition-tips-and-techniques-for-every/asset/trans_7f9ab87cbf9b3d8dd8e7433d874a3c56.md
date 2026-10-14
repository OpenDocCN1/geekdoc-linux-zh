

## METHOD #2

PSUtils
DEB: psutils
RPM: psutils
WWW: http://www.ctan.org/tex-archive/support/psutils/

使用 psmerge 将 PostScript 文件合并为一个。把要合并的文件名作为参数给出，psmerge 会按给定顺序将它们输出到标准输出。你也可以使用 -o 选项指定输出文件名（不要在文件名和选项之间留空格）。

⇒ 要将文件 slide1.ps、slide2.ps 和 slide3.ps 合并到新的 PostScript 文件 slideshow.ps 中，输入：

```
$ psmerge -oslideshow.ps slide1.ps slide2.ps slide3.ps [RET]
```

NOTES: gs 方法其实更可取；psmerge 仅适用于用同一应用程序生成的 PostScript 文件。例如，psmerge 可以合并多个用 TeX 生成的文件，或多个用 Xfig 生成的文件，但不能合并两者的组合。

## 20.2.3 Arranging a PostScript Document in a Booklet

PSUtils
DEB: psutils
RPM: psutils
WWW: http://www.ctan.org/tex-archive/support/psutils/

要将 PostScript 文件中的页面排列成小册子，先用 psbook 将文件重新排列成签名，然后用 psnup 将页面排列（每张打印页横向放置两页），最后用 pstops 先输出奇数页再输出偶数页。

正确操作的诀窍是首先确定需要做什么，然后为 pstops 计算合适的测量值。

⇒ 要从文件 newsletter.ps 制作小册子，请执行以下操作：

- 1. 将页面重新排列成签名：
```
$ psbook newsletter.ps newsletter.signature.ps [RET]
```
- 2. 将页面以横向方式两页合一，缩小至原始大小的 70%（全部在一行输入）：
- $ psnup -1 -p letter -2 -s.7 newsletter.signature.ps > newsletter.2up.ps [RET]
- 3. 输出奇数页：
- $ pstops "2:0(1in,0in)" newsletter.2up.ps > odd.ps [RET]
- 4. 输出偶数页：
- $ pstops "2:-1(1in,0in)" newsletter.2up.ps > even.ps [RET]

然后，要打印小册子，将 odd.ps 发送到打印机，重新将打印好的页面放入手动进纸盘，然后发送 even.ps 到打印机。这样可在纸张的正反两面打印奇数页和偶数页。

⇒ 要从一个使用 letter 大小纵向方向的文件制作 letter 大小纸张横向方向的双倍大小小册子，输入：

```
$ psbook input.ps > temp1.ps [RET]
...processing messages...
$ psnup -1 -p letter -2 -s.7 temp1.ps > temp2.ps [RET]
...processing messages...
$ pstops "2:0(1in,0in)" temp2.ps > odd.ps [RET]
...processing messages...
$ pstops "2:-1(1in,0in)" temp2.ps > even.ps [RET]
...processing messages...
$
```

NOTES: 如果你要经常做这个操作，你可能想看看 ps2book 实用程序，它是一个脚本，可帮助使用 PSutils 制作小册子 [http://www.kis.uni-freiburg.de/~dobler/utils/ps2book.html]。

## 20.3 Converting PostScript

这些配方展示如何将 PostScript 文件转换为其他格式。另请参阅准备 PostScript 文件以便打印的配方，Recipe 25.3.1 [Preparing a PostScript File for Printing]，第 518 页。

### 20.3.1 Converting PostScript to PDF

Ghostscript
DEB: gs-common gs
RPM: ghostscript
WWW: http://www.cs.wisc.edu/~ghost/

要将 PostScript 文件转换为 PDF，请使用 ps2pdf，它是 Ghostscript 软件包的一部分。将要读取的 PostScript 文件名和要写入的 PDF 文件名作为参数给出。

⇒ 要从输入文件 sutra.ps 写入 PDF 文件 sutra.pdf，输入：

```
$ ps2pdf sutra.ps sutra.pdf [RET]
```

此命令写入一个名为 sutra.pdf 的新 PDF 格式文件。原始文件 sutra.ps 未被更改。

NOTES: 要进行正确的 PDF 转换，请确保已安装 Ghostscript 6.01 或更高版本；使用 gs 的 -v 选项输出已安装的版本。

### 20.3.2 Converting PostScript to Plain Text

Ghostscript
DEB: gs-common gs
RPM: ghostscript
WWW: http://www.cs.wisc.edu/~ghost/

要将 PostScript 文件转换为纯文本，请使用 ps2ascii，它是 Ghostscript 软件包的一部分。将要读取的 PostScript 文件名和要写入的文本文件名作为参数给出。

⇒ 要从输入文件 sutra.ps 制作文本文件 sutra.txt，输入：

```
$ ps2ascii sutra.ps sutra.txt [RET]
```

此命令写入一个名为 sutra.txt 的文本文件。原始文件 sutra.ps 未被更改。

