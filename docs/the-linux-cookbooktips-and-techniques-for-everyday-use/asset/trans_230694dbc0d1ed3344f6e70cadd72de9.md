

你也可以通过 M-x 命令指定这些函数来运行它们；此外，lpr-buffer 和 lpr-region 函数会将缓冲区和区域发送到 lpr，而不会对文本进行分页或插入页眉。

- 要打印带页码和页眉的当前缓冲区，输入：
  
  M-x print-buffer RET
- 要打印当前缓冲区且不对文本进行任何额外的打印格式处理，输入：
  
  M-x lpr-buffer RET
- 要打印当前缓冲区的 PostScript 图像，输入：
  
  M-x ps-print-buffer RET

## 26.2.2 使用 Dvips 打印

你可以直接使用 dvips 工具打印 DVI 文件——省略用于指定输出文件的 `-o` 选项，它会将 PostScript 输出直接发送到默认打印机的 spool 队列。

- 要打印 DVI 文件 `list.dvi`，输入：
  
  $ dvips list.dvi RET

下表列出了 dvips 的一些用于控制打印输出的选项。

| OPTION | DESCRIPTION |
|---|---|
| -A | 仅打印奇数页（DVI 文件必须由 TeX 生成）。 |
| -B | 仅打印偶数页（DVI 文件必须由 TeX 生成）。 |
| -b | 指定要打印的份数——适用于打印传单、海报、标牌等多个副本。 |
| -k | 打印裁切标记。 |
| -l last | 指定要打印的最后一页页码。 |
| -m | 使用手动进纸盘。 |
| -p first | 指定开始打印的第一页。 |
| -r | 反转页面的顺序。 |
| -t format | 指定纸张尺寸和格式；有效选项包括 `letter`、`legal`、`a4` 和 `landscape`。 （你可以使用此选项两次，例如同时指定 `legal` 和 `landscape`）。 |

使用 `-m` 选项并通过 `-t` 选项将纸张格式指定为横向，对于在信封上打印非常有用。

- 要在默认打印机的手动进纸盘中装载的信封上打印文件 `envelope.dvi`，输入：

```
$ dvips -m -t landscape envelope.dvi RET
```

NOTE: 你也可以使用 `-d` 选项通过 lpr 打印 DVI 文件。

## 26.2.3 打印 Xterm 窗口的内容

要打印 xterm 窗口的内容，按住 CTRL 并在窗口内任意位置左键单击，然后选择 Print Window 选项。此命令会将当前窗口中的所有文本的副本发送到默认打印机。

## 26.3 为打印准备文件

并非所有打印机都识别所有输出格式，因此有时在打印前需要转换文件。

通常，你可以在任何打印机上打印纯文本。然而，大多数图形或图像文件必须转换为 PostScript 或 EPS（“封装式 PostScript”）。某些应用程序——例如 TeX——会产生 DVI 输出；在这种情况下，你需要将其转换为 PostScript 以便打印。

如果你有 PostScript 打印机，可以直接将 PostScript 文件打印到其上。如果没有，你需要将 PostScript 输出转换为打印机使用的格式。像 `magicfilter` 这样的过滤器程序通过为你完成这项工作使转换变得更容易，但它们并非万能药，因为你的系统可能使用众多过滤器之一。因此，需要以下配方。

- 26.3.1 为打印准备 PostScript 文件
- Preparing PostScript for printing.
- 26.3.2 为打印准备 DVI 文件
- Preparing DVI for printing.

## 26.3.1 为打印准备 PostScript 文件

@sf(Debian): `gs`
@sf(WWW): ftp://www.gnu.org/pub/gnu/ghostscript/

如果你没有 PostScript 打印机，可以使用 Ghostscript，gs，将 PostScript 转换为打印机可理解的输出格式。

使用 `-?` 选项列出你系统上安装的 gs 版本可写入的打印机。

- 要列出可用的打印机格式，输入：

```
$ gs -? RET
GNU Ghostscript 5.10 (1998-12-17)
...more output messages...
Input formats: PostScript PostScriptLevel1 PostScriptLevel2 PDF
Available devices:
x11 x11alpha x11cmyk x11gray2 x11mono lvga256 vgalib
t4693d8 tek4696 appledmp ccr lp2563 lpbp lps3 m8510
oki182 okiib6 la50 la70 la75 lp5plus sxlcrt deskjet
djet500 laserjet ljetplus ljet2p ljet3 ljet4 declj250
cdeskjet cdjcolor cdjmono cdj550 cdj500 djet500c
hpdi unip rint epson eps9mid eps9high epsonc lq850
ap3250 ibmpro bj10e bj200 bj c600 bj c800 ljet3d faxg3
faxg32d faxq4 dfaxhigh dfaxlow pcfaxlow pcfaxmono pcm
pbmraw pgm pgmraw pgnm pgmraw pnm pnmmraw ppm ppmraw
pkm pkmraw tiffcrle tiffg3 tiffg32d tiffg4 psmono
psgray jpeg
...more output messages...
$
```

典型的 gs 安装可以写入 100 多种不同的打印设备，包括 HP LaserJet 4 打印机（`ljet4`）、HP Color DeskJets（`cdeskjet`）和 Group 4 传真（`tiffg4`）。gs 的更新版本将对新打印机提供更好的支持，因此如果你有新型号的打印机，请确保安装了最新版本。

gs 将要转换的文件作为参数接收；将要写入输出的设备作为 `-sDEVICE=` 选项的参数给出，并将要写入的文件名作为 `-sOutputFile=` 选项的参数给出。

另外两个常用选项是：`-dSAFER`，可防止意外删除或覆盖文件，以及 `-dNOPAUSE`，可关闭页面之间的暂停。

