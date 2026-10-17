
$ zcat /usr/share/state/us-constitution.gz | pbmtext | convert constitution.jpeg

# 19.5 使用其他图像导入工具

还有许多从各种来源导入图像的工具。该领域不断变化，随着新硬件设备和新导入工具的出现。下表描述了目前流行的一些工具。

| 工具 | 说明 | DEB | RPM | WWW |
| :--- | :--- | :--- | :--- | :--- |
| Camediplay | 从带有 Sanyo 固件的任何数字相机下载图像，包括 Olympus Camedia 系列。 | camediplay | camediplay | |
| Cqcam | 捕捉 Color QuickCam。 | cqcam | cqcam | http://www.cs.duke.edu/~raynolds/cqcam/ |
| Dvgrab | 从使用 IEEE1394 链路（称为 FireWire）的数字摄像机捕捉音频视频，输出为 AVI 文件。 | dvgrab | dvgrab | http://kino.schirmacher.de |
| Fujiplay | 导入（并进行处理）富士数字相机的图像。 | fujiplay | fujiplay | |

## GOCR

一个从扫描图像中输出纯文本的命令行 OCR 工具。
DEB: gocr
RPM: gocr
WWW: http://jocr.sourceforge.net/

## gPhoto

从数码相机导入图像。
DEB: gphoto
RPM: gphoto
WWW: http://www.gphoto.org/

## Grunch

将部分扫描结果合并形成更大的图像。
DEB: grunch
WWW: http://www.radagast.org/~dplatt/

## Gsumi

从压力敏感输入设备（如绘图板）导入黑白图像。
DEB: gsumi

## Pencam

从使用 STV0680B-001 芯片的数码相机导入图像。
DEB: pencam
WWW: http://stv0680-usb.sourceforge.net/

## Streamer

从 video4linux 设备捕捉图像。
DEB: streamer
RPM: xawtv-streamer
WWW: http://bytesex.org/xawtv/

# 20. PostScript

PostScript 语言由 Adobe 系统的 John Warnock 在 20 世纪 80 年代设计并实现，用于描述“页面”的外观。页面通常是一张物理纸张（PostScript 常用于发送文档到打印机硬件），但它们可以是任何类型的输出显示¹。PostScript 文件是包含 PostScript 语言命令的文本文件，用于绘制要在页面上打印的图像。

与纯文本文件一样，PostScript 文件在网上常见（被商业打印机使用），因为作为纯文本，它们可以轻松地跨平台和硬件共享。同一个 PostScript 文件可以在高端显示器或低端打印机上输出，发挥硬件的最佳性能。PostScript 是一种紧凑且优雅的格式。

虽然可以直接用 PostScript 语言编写代码（有些人已经精通 PostScript 编程），但有许多工具和应用程序可以转换文件，你不需要自己编写。参见方案 15.2 [将文本输出到 PostScript]，第 359 页，获取将文本转换为 PostScript 的方法。

GNU Ghostscript 是 PostScript 语言的免费解释器²。它附带 `gs` 工具，用于将文件从 PostScript 或 PDF 转换为其他格式。它通常用于打印到非 PostScript 打印机（参见方案 25.3.1 [为打印准备 PostScript 文件]，第 518 页）。`ghostview` 工具用于在屏幕上预览 PostScript 文件（参见方案 17.4.2 [预览 PostScript 文件]，第 414 页）。

EPS，或称为封装 PostScript（Encapsulated PostScript），是一种描述页面内一个框内容的文件。EPS 文件可以嵌入到 PostScript 文件的页面中，因此在向文档中插入插图时常用（例如，《Linux 食谱》中打印的所有插图都是 EPS 文件）。你可以像处理 PostScript 文件一样查看和打印 EPS 文件。

本章包含了格式化和处理 PostScript 文件的方案。方案分为类：针对 PostScript 文件中单个逻辑页的操作（文件中的编号页，但不一定是输出的物理页），以及针对整个文件的方案。

> ¹PostScript 最初是为 Apple LaserWriter 打印机设计的；news 是 Sun Microsystems 的一个旧 UNIX 系统，它使用 PostScript 绘制显示。

> ²它也是 Adobe 便携文档格式（PDF）语言的解释器。

# 《Linux 食谱》第二版

本章中使用的许多工具都是 Angus Duggan 的 `psutils`（“PostScript 工具集”）包的一部分。这些工具可以用于本章描述的其他用途；更多详情请参阅各自的手册（man pages）。

# 20.1 操作 PostScript 页面

这些方案适用于 PostScript 文件的单个页，而不是文件本身。

## 20.1.1 将 DVI 页面提取为 PostScript

### DVIPS

DEB: tetex-bin
RPM: tetex-dvips
WWW: http://www.radicaleye.com/dvips.html

若要将 DVI（“设备无关”）文件的特定页提取为 PostScript，请使用 `dvips` 并通过 `-pp` 选项指定要输出的页码或连字符格式的页范围。

- 从文件 `abstract.dvi` 中仅提取第一页并将 PostScript 输出发送到打印机，输入：

```
$ dvips -pp1 abstract.dvi
```

默认情况下，`dvips` 将输出到打印机；要将 PostScript 输出保存到文件，请指定文件名作为 `-o` 选项的参数。

- 将 `abstract.dvi` 的第 137 到 146 页输出为 PostScript 并写入文件 `abstract.ps`，输入：

```
$ dvips -pp137-146 -o abstract.ps abstract.dvi
```

## 20.1.2 从 PostScript 文件中提取页面

### PSUtils

DEB: psutils
RPM: psutils
WWW: http://www.ctan.org/tex-archive/support/psutils/

使用 `psselect` 从 PostScript 文件中选择页面；当你提供输入文件时，它会输出一个包含指定页的新 PostScript 文件。输出发送到标准输出或作为第二个参数指定的文件。

## 20.1.3 合并 PostScript 页面

### PSUtils

DEB: psutils
RPM: psutils
WWW: http://www.ctan.org/tex-archive/support/psutils/

使用 `psnup` 在单张纸上打印多个 PostScript 页面；通过选项指定每张纸上合并（或放置“up”）的页数。

要创建一个新的 PostScript 文件 `double.ps`，将 `single.ps` 文件中的两个页放在每一页纸上，输入：

```
$ psnup -2 single.ps double.ps
```

要指定页面大小，请为 `-p` 选项提供标准页面的名称：a3, a4, a5, b5, letter, legal, tabloid, statement, executive, folio, quarto 或 10x14。你可以使用 `-h` 和 `-w` 选项指定任意高度和宽度；单位可以是厘米（后跟 "cm"）或英寸（后跟 "in"）。如果未指定尺寸，`psnup` 假设页面大小为 a4。

当页面为横向方向（相对于纵向逆时针旋转 90 度）时，使用 `-l` 选项；当页面为海景方向（相对于纵向顺时针旋转 90 度）时，使用 `-r` 选项。

页面在输出文件中按“行主序”布局排列，即逻辑页跨页面按行排列。使用 `-c` 选项指定“列主序”布局，即逻辑页沿页面按列排列。通过向 `-s` 选项提供一个百分比系数来缩放页面尺寸；例如，`-s .5` 将页面缩放为原始尺寸的 50%。

要在每个页面周围绘制边框，请为 `-d` 选项提供以点（points）为单位的边框宽度（如果未指定宽度，则假设值为 1）。

## 20.1.4 在订页中排列 PostScript 页面

### PSUtils

DEB: psutils
RPM: psutils
WWW: http://www.ctan.org/tex-archive/support/psutils/

订页（signature）是文档中的一组页面，对应于纸张并经过装订；这些页面在文档中通常不是按顺序排列的（例如，一个八页订页的文档，第 8 页和第 1 页可能打印在同一张纸上）。

要通过订页重新排列 PostScript 文件的页面——通常是将文件打印成书或小册——请使用 `psbook`。将要读取的 PostScript 文件名和输出的文件名作为参数；`psbook` 读取第一个文件的内容，重新排列页面，然后将 PostScript 输出写入第二个文件。

- 要将文件 `newsletter.ps` 的页面重新排列成一个订页并写入文件 `newsletter.bound.ps`，输入：

```
$ psbook newsletter.ps newsletter.bound.ps
```

默认情况下，`psbook` 为整个文件使用一个订页。如果文件的页数不是 4 的倍数，它会在末尾添加空白页。

要指定使用的订页大小——换句话说每张纸出现的页数——请将该数字作为 `-s` 选项的参数。订页大小始终是 4 的倍数。

- 要将文件 `newsletter.ps` 的页面重新排列为八页并写入 `newsletter.bound.ps`，输入：

```
$ psbook -s8 newsletter.ps newsletter.bound.ps
```

# 20.2 操控 PostScript 文档

这些配方适用于整个 PostScript 文档。

## 20.2.1 调整 PostScript 文档尺寸

### PSUtils

DEB: psutils
RPM: psutils
WWW: http://www.ctan.org/tex-archive/support/psutils/

使用 `presize` 调整 PostScript 文档的大小。它接受需要调整的文件和写入的输出文件作为参数；否则，它将从标准输入读取并写入到标准输出。如果你提供了输出文件名，则必须指定要使用的页面大小，格式与 `psnup` 相同：使用 `-p` 或 `-h` 和 `-w` 指定输出文件的大小，并使用 `-P` 指定输入文件的大小（参考方案 20.1.3 [合并 PostScript 页面]）。

- 要将 PostScript 文件调整为美国信纸（letter）尺寸，并将输出写入新文件 `doublet.ps`，输入：

```
$ presize -pletter double.ps doublet.ps
```

## 20.2.2 合并 PostScript 文档

将多个 PostScript 文件连接并合并为单个文件时，有两种值得提及的方法。一种是更健壮的解决方案，另一种更容易输入。我将从首选的方法开始，这是我在合并这本书的 PostScript 页面时发现的。

### 方法 #1

DEB: gs-common / gs
RPM: ghostscript
WWW: http://www.cs.wisc.edu/~ghost/

你可以使用 `gs` 将许多 PostScript 文件合并为一个。使用 `-q`、`-dNOPAUSE` 和 `-dBATCH` 标志使其静默启动且不暂停，并使用 "pswrite" 作为写入设备，将其作为 `DEVICE=` 选项的参数。使用特殊的 `-sOutputFile` 选项指定输出文件名，最后，按照你想要的顺序指定要合并的文件。

- 要按顺序合并 PostScript 文件 `part1.ps`、`part2.ps` 和 `part3.ps` 并写入一个新文件，输入：

```
$ gs -q -dNOPAUSE -dBATCH -sDEVICE=pswrite -sOutputFile=output.ps part1.ps part2.ps part3.ps
```

**注意**：如果你计划对所有文件执行此操作，可以使用脚本来简化：

```bash
#!/bin/sh
gs -q -dNOPAUSE -dBATCH -sDEVICE=pswrite -sOutputFile=output.ps $@
```

### 方法 #2

DEB: psutils
RPM: psutils
WWW: http://www.ctan.org/tex-archive/support/psutils/

你可以使用 `psmerge` 将许多 PostScript 文件合并为一个。要按顺序合并 PostScript 文件 `part1.ps`、`part2.ps` 和 `part3.ps`，输入：

```
$ psmerge part1.ps part2.ps part3.ps > output.ps
```

**注意**：`psmerge` 方法更容易输入，但没有 `gs` 方法那样健壮。

## 20.3.1 将 PostScript 转换为 PDF

### Ghostscript

DEB: gs-common gs
RPM: ghostscript
WWW: http://www.cs.wisc.edu/~ghost/

要将 PostScript 文件转换为 PDF，请使用 `ps2pdf`，它是 Ghostscript 包的一部分。将要读取的 PostScript 文件名和要写入的 PDF 文件名作为参数。

- 要从输入文件 `sutra.ps` 写入一个 PDF 文件 `sutra.pdf`，输入：

```
$ ps2pdf sutra.ps sutra.pdf
```

此命令会创建一个名为 `sutra.pdf` 的 PDF 格式新文件。原始文件 `sutra.ps` 不会被更改。

**注意**：为了进行正确的 PDF 转换，请确保已安装 Ghostscript 6.01 或更高版本；使用 `gs` 配合 `-v` 选项输出已安装的版本。

## 20.3.2 将 PostScript 转换为纯文本

### Ghostscript

DEB: gs-common gs
RPM: ghostscript
WWW: http://www.cs.wisc.edu/~ghost/

要将 PostScript 文件转换为纯文本，请使用 `ps2ascii`，它是 Ghostscript 包的一部分。将要读取的 PostScript 文件名和要写入的文本文件名作为参数。

- 要从输入文件 `sutra.ps` 创建一个文本文件 `sutra.txt`，输入：

```
$ ps2ascii sutra.ps sutra.txt
```

此命令会写入一个名为 `sutra.txt` 的文本文件。原始文件 `sutra.ps` 不会被更改。

# V. 声音

# 21. 播放与录制

本章介绍了 Linux 声音系统的基本控制，包括如何调整音频混合器以及如何使用基本工具播放和录制声音文件。你还可以使用 Snd（参见第 23 章 [编辑音频文件]，第 487 页）以及许多其他音频应用程序播放和录制音频。

为了让你的系统声音正常，你需要为你的声卡安装并配置声音驱动程序。这是控制你声卡的软件，反过来又是 Linux 声音系统的一部分。

多年来，独立的 ALSA（“高级 Linux 声音架构”）一直是音频应用程序中声音系统的流行选择，优于 Linux 内核带的旧版 OSS/Free（Open Sound System）。

从 2.6 内核开始，ALSA 现在已包含在 Linux 中。如果你的 Linux 内核版本较旧，你必须让管理员安装 ALSA，或者直接使用旧的 OSS/Free 驱动程序。大多数系统都经过配置，因此你必须是超级用户才能使用声音设备（包括音频 CD）。如果你的系统情况如此，请要求管理员授予你对这些设备的访问权限，通常是将你加入 audio 组（参见方案 6.1 [在组中工作]，第 163 页）。

## 21.1 调整音频控制

### ALSA Utilities

DEB: alsa-utils
RPM: alsa-utils
WWW: http://www.alsa-project.org/

混合器程序用于调整各种音频设置（如音量和录制电平），并用于开启或静音麦克风或其他输入设备。在播放或录制声音之前，你必须使用混合器调整你的音频设置。

录制之前，请确保静音所有通道，但你的输入源——但别忘了以后当你想听它们发出的声音时把它们取消静音！

ALSA 的默认混合器称为 `amixer`，下面的方案将展示它的用法。还有其他混合器，其中一些比 `amixer` 容易用得多。我的建议安装 `amixer`。参见本章末尾的其它建议，包括在 X 中使用的图形化混合器，见方案 21.5 [使用其他声音工具]，第 474 页。

### 21.1.1 列出当前音频设置

要列出所有音频输入输出设备及其设置，输入不带任何选项的 `amixer`。

你的声卡组件按组组织，从包含主左、主右音量设置的 Master 组，到用于音频 CD 和数字声音文件的独立组。（这些组与方案 6.1 [在组中工作]，第 163 页中描述的文件访问组无关。）

- 要查看当前混合器设置，输入：

```
$ amixer | less
```
