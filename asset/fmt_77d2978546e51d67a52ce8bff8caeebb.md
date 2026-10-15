
每次执行更多测试之前，应先输入 `rm -v /tmp/lpdfilter*` 删除这些文件。

## 关于 Ghostscript 的一点介绍

Ghostscript 接受 PostScript 和 PDF 数据作为输入，并包含众多 Ghostscript 驱动（在 Ghostscript 中称为设备），用于转换为其他格式。Ghostscript 转换分两步进行：

- 1. PostScript 数据被转换为矩阵。由 PostScript 语言描述的图像被解析为精细的单个像素矩阵图案。此过程与各个 Ghostscript 驱动无关。矩阵越精细（分辨率越高），输出质量越高，但处理器和内存消耗也越多，因为分辨率加倍时矩阵中的点数会翻两番。
- 2. 最后，解析为点阵的图像现在被转换为所需格式，即所需的打印机语言。

Ghostscript 不仅提供打印机驱动，还可以处理用于屏幕输出的 PostScript 文件（参见*基础手册*中的“从应用程序打印”一节），甚至可以将其转换为 PDF。使用 `gv` 程序（包 `gv`）可以轻松地在屏幕上以 Ghostscript 的图形用户界面查看 PostScript 文件的输出。

Ghostscript 是一个功能非常复杂的应用程序，具有众多命令行选项。除了 `gs` 的手册页（`man gs`）和 Ghostscript 驱动列表外，最基本的文档可以在 `/usr/share/doc/packages/ghostscript/catalog.devices` 中找到，以及

`file:/usr/share/doc/packages/ghostscript/doc/index.html`

`file:/usr/share/doc/packages/ghostscript/doc/use.htm`

`file:/usr/share/doc/packages/ghostscript/doc/Devices.htm`

`file:/usr/share/doc/packages/ghostscript/doc/hpdj/gs-hpdj.txt`

`file:/usr/share/doc/packages/ghostscript/doc/hpijs/hpijs_readme.html`

`file:/usr/share/doc/packages/ghostscript/doc/stp/README`

如果直接启动，Ghostscript 会打开一个带有其自身提示符 `GS>` 的对话框。用 `quit` 退出。

帮助命令 `gs -h` 列出最重要的选项并输出当前的设备列表。如果某个驱动支持多个型号，则只会出现诸如 `uniprint` 和 `stp` 之类的基本驱动描述。`uniprint` 和 `stp` 型号的参数文件在 `/usr/share/doc/packages/ghostscript/catalog.devices` 中有更详细的列出。

## 使用 Ghostscript 的示例

在 `/usr/share/doc/packages/ghostscript/examples` 中查找 PostScript 示例文件。`colorcir` 很适合用于打印机测试（`file:/usr/share/doc/packages/ghostscript/examples/colorcir.ps`）。

## X11 输出

在 X 图形界面中，使用 `gs` 命令在屏幕上查看 PostScript 文件：

```
newbie@earth:  > gs -r60 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps
```

分辨率通过选项 `-r` 指定，该选项必须与输出设备（打印机或屏幕）兼容。例如，可以用 `-r30` 试试。要退出程序，请在启动 `gs` 的终端中按 (Ctrl) + (C)。

## 转换为 PCL5e 或 PCL6

使用以下命令将 PostScript 文件转换为 PCL5e 或 PCL6 打印机的特定格式：

```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \
    -sDEVICE=ljet3 -r300x300 \
    /usr/share/doc/packages/ghostscript/colorcir.ps quit.ps
```

其中命令在一行内输入，不带反斜杠（`\`）。同时假定文件 `/tmp/out.prn` 尚不存在。

## 转换为 PCL3

使用以下命令将 PostScript 文件转换为 PCL3 打印机的特定格式：

```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \
    -sDEVICE=hpdj -r300x300 \
    -sModel=500 -sColorMode=mono -dCompressionMethod=0 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \
    quit.ps
```

```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \
    -sDEVICE=cdj300 -r300x300 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \
    quit.ps
```

```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \
    -sDEVICE=cdj500 -r300x300 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \
    quit.ps
```

```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \
    -sDEVICE=cdj550 -r300x300 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \
    quit.ps
```

（每条命令在一行内输入，忽略“\”。）

## 转换为 ESC/P、ESC/P2 或 ESC/P 点阵

使用以下命令将 PostScript 文件转换为 ESC/P2、ESC/P 或 ESC/P 点阵打印机的特定格式：

```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \
    @stcany.upp \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \
    quit.ps
```

```
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \
    -sDEVICE=cr360x360 \
    -dBitsPerPixel=1 -dDithering=gsmono -dNoWeave \
    -sOutputCode=plain \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \
    quit.ps
```

这里可以看到，当为 `uniprint` 驱动程序或其他 Ghostscript 驱动程序使用参数文件时，命令之间的区别。由于所有驱动程序特定的参数都位于 `uniprint` 参数文件中，因此与其他 Ghostscript 驱动程序不同，无需指定任何其他驱动程序特定参数。

## 直接打印机输出

在上述每条命令之后，打印机特定的数据都位于 `/tmp/out.prn` 中。只要打印机连接到第一个并行端口 `/dev/lp0`，就可以使用以下 root 命令（无需假脱机程序或过滤器）将这些数据直接发送到打印机：

```
earth: # cat /tmp/out.prn >/dev/lp0
```

## 关于 a2ps 的一点说明

在使用 Ghostscript 打印 ASCII 文本文件之前，必须将其转换为 PostScript，因为 Ghostscript 期望输入的是 PostScript。为此使用 `a2ps`（软件包 `a2ps`）。`a2ps` 是一个强大的工具，可以从简单文本生成高质量的 PostScript 输出。它是一个非常复杂的程序，带有众多命令行选项。最重要的文档可以在 `a2ps` 的手册页中找到（`man a2ps`）。

## 使用 a2ps 的示例

### 使用 a2ps 直接输出文本文件到打印机

以下命令可用于将文本文件使用 `a2ps` 转换为 PostScript，使两页缩小并适合打印在一页上：
