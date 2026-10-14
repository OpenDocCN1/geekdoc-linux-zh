
# 第 25 章：打印

## 25.2.6 打印 Emacs 缓冲区

你可以从 Emacs 打印缓冲区，打印整个缓冲区或仅打印区域。这里有几种方法。

“打印”子菜单中有“打印区域”（Print Region），它只打印点（point）和标记之间的文本（参见食谱 10.1.1 [熟悉 Emacs]，第 232 页）。这两个命令都会将硬拷贝输出分成若干页进行打印，并在每页的顶部带有页眉，显示文件名和当前页码。

### 方法 #2

要生成并打印缓冲区的 PostScript 图像，可以使用 `ps-buffer-function`，该函数在“打印”子菜单中也可用。相关函数 `ps-print-region` 用于打印区域的 PostScript 图像。这些命令用于将缓冲区的文本发送到 PostScript 打印机。

⇒ 要将当前的 Emacs 缓冲区作为 PostScript 文件发送到默认打印机，输入：

```
ALT-X ps-print-buffer RET
```

### 方法 #3

你可以通过 `ALT-X` 命令指定并运行上述任何打印函数。此外，`lpr-buffer` 和 `lpr-region` 函数会将缓冲区和区域发送到 `lpr`，而不会对文本进行分页处理或插入页眉。

⇒ 这里有一些使用方法：

- 要打印带有页码和页眉的当前缓冲区，输入：

  ```
  ALT-X ps-print-buffer RET
  ```

- 要打印不给文本添加任何额外打印格式的当前缓冲区，输入：

  ```
  ALT-X lpr-buffer RET
  ```

- 要打印当前缓冲区的 PostScript 图像，输入：

  ```
  ALT-X ps-print-buffer RET
  ```

## 25.2.7 打印 Info 节点

当你运行 `info`（超文本 Info 视视器）时，可以通过运行 `print-node` 函数来打印当前节点。

⇒ 要在 Info 中打印当前节点，输入：

```
ALT-X print-node RET
```

## 25.2.8 打印终端窗口内容

要打印 X 中 `xterm` 窗口的内容，请按住 `CTRL` 并在窗口内任何位置点击左键，然后选择“打印窗口”（Print Window）选项。此命令将当前窗口内所有文本的副本发送到默认打印机。

## 25.3 为打印准备文件

严格来说，这些是文件格式转换，但它们通常被用于打印到某些设备。并不是所有的打印机都能识别所有的输出格式，因此有时在打印之前需要转换文件。

通常情况下，你可以在任何打印机上打印纯文本。然而，大多数图形或图像文件必须转换为 PostScript 或 EPS（“封装式 PostScript”）。某些应用程序（如 TeX）产生 DVI 输出；在这种情况下，你可能需要将 PostScript 输出转换为你的打印机使用的格式。

如果你有一台 PostScript 打印机，可以直接向其打印 PostScript 文件。如果没有，你将需要将 PostScript 输出转换为你的打印机使用的格式。像 `magicfilter` 这样的过滤程序可以通过替你完成工作来让转换变得更容易，但它们并不是万能药，因为你的系统可能使用了许多打印过滤器中的一种。因此，才需要以下食谱。

### 25.3.1 为打印准备 PostScript 文件

```
Ghostscript
DEB: gs-common
RPM: ghostscript
WWW: http://www.cs.wisc.edu/~ghost/
```

如果你没有 PostScript 打印机，可以使用 Ghostscript（`gs`）将 PostScript 转换为你的打印机可以识别的输出格式。

使用 `-?` 选项列出你系统中安装的 `gs` 版本可以输出的格式。

⇒ 要列出可用打印格式，输入：

```
$ gs -? RET GNU Ghostscript 5.10 (1998-12-17)
... output messages...
Input formats: PostScript PostScriptLevel1 PostScriptLevel2 PDF
Available devices:
x11 xalpha x11myck x11gray x1imono lvga256 vgalib
t4693d8 tek46696 laserjet ljplus addcsp cdj50 cdj50 lp2563 lb8 laps m8510
ok182 okiibm la50 la70 la75 la75plus sxclert deskjet
djet500 laserjet ljplus ljet2p ljet3 ljet4 declj250
deskjet djcolor cdjmono cdj50 cdj50 djet500c
hpdj unprint epson eps9mid eps9high epsonc lq850
ap3250 ibm bj10e bj200 bcj600 bcj800 ljet3fd faxg3
faxg32d pgmar fgfaxah dfaxlow pcmoono pcgray pbm
pbmraw pgmar pgnum pgnmar ppm pnmr ppmkm tiffercrle tiff3 tiff32d tiff4 psmono
psgray jpeg
... output messages...
$
```

一个典型的 `gs` 安装可以写入 100 多种不同的打印设备，包括 HP Laser Jet 4 打印机（`ljet4`）、HP Color Desjets（`cdsketch`）和第 4 页传真（`tiff4`）。较新版本的 `gs` 对新打印机有更好的支持，如果你有新型号打印机，请确保安装了最新版本。

`gs` 将要转换的文件作为参数；将输出设备作为 `-sDEVICE=` 选项的参数；将要写入的文件作为 `-sOutputFile=` 选项的参数。

可以使用另外两个选项：`-dSAFER`（它防止意外删除或覆盖文件）以及 `-dNOUSE`（它会关闭页与页之间的暂停）。

转换完成后，输入 `quit` 退出。

⇒ 要将 PostScript 文件转换为适用于 `cdj50` 打印机的格式，请输入：

```
$ gs -sDEVICE=cdj50 -sOutputFile=tiger.dj -dSAFER -dNOUSE < /dev/null
```

此命令写入 `tiger.dj`，你可以通过 `lpr` 将其发送到打印机。打印一个 PostScript 文件。

### 25.3.2 为打印准备 DVI 文件

| RPM | `tetex-dvps` |
| --- | --- |
| WWW | `http://www.radicaleye.com/dvips.html` |

你可以直接用 `dvips` 打印 DVI 文件——`-o` 选项用于指定输出文件，它会将 PostScript 输出直接发送到默认打印机的打印队列。

要打印 `list.dvi`，输入：

```
$ dvips list.dvi (回)
```

下表列出了 `dvips` 控制打印输出的一些选项。

- `-A` 仅打印奇数页（DVI 文件必须由 TeX 生成才能使用此选项）。
- `-B` 仅打印偶数页（DVI 文件必须由 TeX 生成才能使用此选项）。
- `-b` 指定打印份数，用于打印传单、标语等的多个副本。
- `-k` 打印裁剪标记。
- `-1` 指定打印的最后页码。
- `-m` 使用手动进纸器。
- `-p` 指定开始打印的第一页。
- `-r` 反转页面顺序。
- `-t 格式` 指定页面大小和格式；有效选项包括“letter”、“legal”、“a4”和“landscape”（你可以多次使用此选项，例如同时指定“legal”和“landscape”）。

使用 `-m` 选项并使用 `-t` 选项指定横向作为纸张格式，对于打印信封非常有用。

⇒ 要在默认打印机的手动进纸器上加载的信封上打印文件，输入：

```
$ dvips -m -t landscape envelope.dvi
```

```
DVIPS
DEB: tetex-bin
RPM: tetex
WWW: http://www.radical.com/dvps.html
```

要将 DVI 格式的文件转换为 PostScript，使用 `dvips`。它接受文件作为参数；将文件名作为 `-o` 选项的参数。

输出 DVI 文件的特定页，将它们作为 `-pp` 选项的参数。

⇒ 这里有一些使用方法：

- 要带页码和页眉打印当前缓冲区，输入：

  ```
  $ dvips -o-.ps buffer
  ```

- 要在不给文本添加任何额外打印格式的情况下打印当前缓冲区，输入：

  ```
  $ dvips -o- buffer
  ```

- 要打印当前缓冲区的 PostScript 图像，输入：

  ```
  $ dvips -o- buffer
  ```

