
# 智能过滤器的重要组成部分

智能过滤器的重要组成部分是将 `Ghostscript` 用作翻译程序。该软件包随 `FreeBSD` 一起发布，并在你的本地计算机上作为 `PostScript` 解释器。当作为 `BSD LPD` 打印机队列的一部分调用时，`Ghostscript` 实际上将任何受支持的打印机都变成了 `PostScript` 打印机。有关 `Ghostscript` 支持打印机列表，请参阅 Linux Printing 网站（[http://www.linuxprinting.org/printer_list.cgi](http://www.linuxprinting.org/printer_list.cgi)）。该网站包含比官方 `Ghostscript` 网站（[http://www.cs.wisc.edu/~ghost/](http://www.cs.wisc.edu/~ghost/)）更完整的信息，包括未随主 `Ghostscript` 软件包提供的驱动程序信息。

`Ghostscript` 并非设计为*仅*作为 `FreeBSD` 打印队列的一部分功能；它可以接受 `PostScript` 文件作为输入，并创建存储在磁盘上的输出文件。该程序的基本语法是

```text
gs [option(…)] [file(…)]
```

`gs` 手册页包含程序选项的列表。一些重要的包括

- `-sDEVICE=devicename` 此选项指定输出设备（即打印机驱动程序）；这*不是*指 `FreeBSD` 设备文件）。输入 `gs --help` 将显示包含系统中可用设备列表的帮助文本。其中一些名称可能并不一定显而易见，但 Linux Printing 网站提供了针对特定打印机使用适当设备的指示。
- `-r xres yres` 许多设备支持多种分辨率，你可以使用此选项指定。例如，`-r 360×720` 告诉 `Ghostscript` 以 360×720 点/英寸 (`dpi`) 创建输出。如果你省略 `x` 和 `y` `res`，`Ghostscript` 假设 `res` 与 `xres` 匹配。打印时，你必须指定你的打印机和你的打印机的 `Ghostscript` 驱动所支持的分辨率。
- `-sOutputFile=filename` 此选项指定输出文件名。在打印队列中使用时，`filename` 将是一个破折号 (`-`)，表示标准输出。如果你在打印队列之外调用 `gs`，你将需要提供适当的文件名。

`Ghostscript` 通常从标准输入接受输入。作为 `Ghostscript` 使用示例，假设你有一台 Hewlett Packard Laserjet 4 打印机。你可以使用类似以下命令从 `PostScript` 文件创建适当的输出文件：

```text
$ gs -sDEVICE=ljet4 -r600x600 -sOutputFile=escher.pcl escher.ps
```

## 252 FreeBSD：完整参考指南

> **提示**
>
> 除了打印机输出格式外，`Ghostscript` 还支持一些常见的图形文件输出格式。这些包括 `TIFF`（`tiff42anc` 等）、`PNG`（`png16`、`png256`、`png16m` 等）、`JPEG`（`jpeg`）、`EPS`（`epswrite`）、`PostScript`（`pswrite`）以及 `PDF`（`pdfwrite`）。虽然从 `PostScript` 输入生成 `PostScript` 输出听起来有些奇怪，但在某些情况下这非常有用，例如当您的 `PostScript` 打印机因内存不足或其他问题而无法处理原始 `PostScript` 文件时。

当输入如上述示例的 `Ghostscript` 命令时，每生成新的一页您都会看到一个提示，要求按 `ENTER`；之后您需要在提示符处输入 `quit` 以退出程序。通过在输入文件名之前添加 `-dNOPAUSE -dBATCH` 到命令中，您可以消除这些提示。如果您创建自定义滤镜来处理 `PostScript` 文件，这些选项可能极其重要。

创建输出文件后，您可以将其发送到打印机（通过 `cat` 或 `lpr`——但如果您已设置滤镜，`lpr` 可能无法正常工作）。您应该会得到合理的输出。如果没有输出，或者您得到了一页又一页的乱码，可能需要尝试另一种驱动程序。如果您看不到任何打印机活动的迹象，例如指示灯闪烁，您可能需要回过头去调查基本的打印机连接问题。

### 设置智能滤镜

`FreeBSD` 上有几种智能滤镜包可用。这些本质上是像 9-2 列表那样的滤镜，但更加复杂。它们可以识别许多不同的文件类型，并处理文件以便它们能在您的打印机上打印。最常见的是，这些滤镜调用常见的文件转换程序将输入文件转换为 `PostScript`。然后，滤镜使用 `Ghostscript` 将文件转换为您的打印机能够理解的格式。（如果您有 `PostScript` 打印机，最后这一步会被跳过。）配置完成后，打印任何受支持的文件类型只需将文件提供给该滤镜即可。两个特别流行的智能滤镜包是 `affsfilter` 和 `magicfilter`，两者都可通过 `sysinstall` 的 Print 软件部分获取。本节描述了 `magicfilter` 的配置。

使用 `magicfilter` 的正常方式有点不寻常：您将它的配置文件当作程序来调用。这种技术之所以有效，是因为配置文件被标记为可执行，并以 `FreeBSD` 用于像 shell 脚本语言一样启动 `magicfilter` 的代码开头。各种 `magicfilter` 配置文件位于 `/usr/local/libexec/magicfilter` 目录下，并以它们依赖的 `Ghostscript` 驱动程序命名。例如，针对 `ljjet4` `Ghostscript` 驱动程序的滤镜被称为 `Ljet4-filter`。作为 `magicfilter` 配置工作的一个示例，请考虑 9-3 列表，这是经过修改的 9-1 列表，用于对 Laserjet 4 或兼容打印机使用 `magicfilter`。如您所见，唯一的区别是添加了对 `magicfilter` 配置文件的调用。

**列表 9-3**

**使用 magicfilter 的 /etc/printcap 条目示例**

```text
lp|hp4000:\
:lp=/dev/lp0:\
:br#115200:\
:sd=/var/spool/lpd/hp4000:\
:mx#0:\
:s#:\n::if=/usr/local/libexec/magicfilter/ljet4-filter:
```

![](img/f34d37e3abe9f4517128e54f80ab2616_290_0.png)

如果 **magicfilter** 恰好附带了适用于您打印机的滤镜，那么打印机设置就很简单——或者至少不会比设置纯文本队列更糟。然而，如果 **magicfilter** 包缺少适用于您打印机的合适滤镜，您必须自己创建一个。

![](img/f34d37e3abe9f4517128e54f80ab2616_290_1.png)

`Ghostscript`——因此也包括 **magicfilter**——为打印机类别提供驱动程序。例如，许多激光打印机使用与各种 *Hewlett-Packard* 型号相同的打印机控制语言（`PCL`），因此您可能能够使用 *laserjet*、*ljet2dp*、*ljet3*、*ljet4* 以及类似的驱动程序（以及名称相似的 **magicfilter** 配置文件）来处理由 *Lexmark*、*Brother*、*Okidata* 和其他厂商销售的打印机。请咨询 **Linux Printing** 网站 (`http://www.linuxprinting.org/printer-list.cgi`) 以获取有关哪个 *Ghostscript* 驱动程序与您的打印机配合良好的信息。

如果您需要创建自定义的 **magicfilter** 配置文件，我建议从复制类似打印机的现有滤镜开始。最重要的标准是*不要*选择 `PostScript` 文件（这些文件以 `%!` 或 `%ps` 开头），因为这些文件将 `PostScript` 输出直接发送到打印机端口，而不调用 **Ghostscript**。大多数滤镜文件在文件的开头部分都包含对 **Ghostscript** 的引用，如下所示：

```text
# PostScript
0 !\t filter /usr/local/bin/gs -q -dSAFER -dNO_PAUSE -r600 -dDEVICE=ljet4 -oOutputFile-
0 `004!` filter /usr/local/bin/gs -q -dSAFER -dNO_PAUSE -r600 -dDEVICE=ljet4 -oOutputFile-
```
