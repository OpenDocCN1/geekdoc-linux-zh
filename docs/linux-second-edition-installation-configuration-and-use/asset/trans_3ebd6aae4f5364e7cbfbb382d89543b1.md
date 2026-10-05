

当单页包含超过 16 种不同字体时（这会导致 dvips 失败），或 LaTeX 文本使用 PostScript 字体时，也建议通过 dvips 这一中转方案。gs 同样无法精确表示 PostScript 字体，但它提供的结果仍然比 dvips 更好。

如果你想打印出包含 PostScript 字符集的 `*.dvips` 文件，你应该通过 `dvips` 和 `gs` 进行中转——结果一定会更好。`dvips` 会无情地将所有 PostScript 字符集替换为 10 点的 LaTeX 字体。

dvips 拥有一个非常详尽的手手册（man page）。你可以在其中找到关于其余选项以及如何双面打印（通过先打印奇数页，然后在刚才打印的纸张反面打印偶数页）的信息。

## PostScript $\rightarrow$ 打印机格式转换 (gs)

Ghostscript（即 gs 程序）可以将 PostScript 文档转换为多种打印机格式（包括传真格式）。当 PostScript 文档中使用 LaTeX 宏包时，质量不会有损失；如果使用了 PostScript 字符集，gs 必须使用 `/usr/lib/ghostscript/fonts` 下的字符集文件，而并非所有文件都能匹配原始字体质量。

```
gs [options] postscript.file [quit.ps]
```

为了让 gs 正确运行，必须指定两个选项：`sDEVICE=` 设置输出格式，`-outputfile=` 指定结果写入的文件。按照惯例，使用 `sPAPERSIZE=4` 和 `-DOPAUSE` 选项也是合理的。

- `-dNDISPLAY` 抑制在屏幕上显示各种信息。此外，不再需要用 `--` 来确认每一页的完成。

- `-dSAFER` 所有文件均仅以只读方式打开。当 gs 用作过滤器时（例如用于打印后台进程处理程序），必须使用此选项。

- `-q` 抑制各种状态信息（静静模式）。

- `-resolution` 设置图形分辨率。转换为各种点阵打印机格式时，此选项是必要的。

- `-sDEVICE=` 指定 gs 将 PostScript 文件转换为什么种格式。可以通过 `gs -h` 获取所有可能的格式列表。其中最重要的格式包括桌面端的 `djet500`、`lserjet`、`ljet3`、`ljet4`、`necp6`、`bj10e` 和 `bj200ibmpro`。仅包含一页（一张图像）的 PostScript 文件也可以转换为各种图形格式，如 `tiff3` 或 `png256`。无法转换为 ASCII 文本。

```
-sOutputFile=file.name
```

将转换结果写入指定的文件。

```
-sPAPERSIZE=size
```

指定输出的纸张大小。大多数情况下必须使用 `a4`，否则 gs 将默认使用较小的美国信纸格式。

gs 以交互方式工作，在处理最后一页后会显示输入提示符。为了让 gs 知道转换结束，你只需要输入 Ctrl+D。如果你想避免这种输入，可以指定一个名为 `quit.ps` 的第二个文件，该文件从 `/usr/lib/ghostscript/` 加载且仅包含 `quit` 命令。

以下指令将 `test.ps` 转换为 HP LaserJet 3 格式。结果写入 `test_out.ps`，gs 随后立即终止。

```
gs -sDEVICE=ljet3 -soutputfile.ps \
  > -sPAPERSIZE=64 -dMOPAUSE test.ps
```

gs 有多个版本，均受不同的版权保护；最新版本是 'Aladdin Ghostscript n'。虽然该版本可以在互联网上免费获取，但商业发行（如 Linux 发行版中）只有通过许可协议才是可能的。旧版本在一段时间后会变为 'GNU Ghostscript n'。它们遵循 GPL ，即分发（几乎）不受限制。根据与 Aladdin Enterprises 的协议，Linux 发行版因此部分包含了 Aladdin 版本，另一部分包含了 Ghostscript 版本。
对于终端用户来说，GNU Ghostscript 的缺点是最新的驱动尚未实现。关于不同 Ghostscript 版本的最新信息可以在网上找到：

```
http://www.wisc.edu/ghost/
```

> gs 的 man 文本相当全面。此外，目录 `/usr/share/ghostscript/n/n/doc` 包含了关于 GhostScript 内部的更多信息。

提示

## PostScript 工具 (psutils)

通过 `ghostview`，你还可以从文件中选择单个页面并将其存储为单独的 PostScript 文件。如果你希望自动化此及其他类似任务，`psutils` 包中的命令将非常有用。某些命令是自包含程序，其他则是 bash 或 Perl 脚本。

出于空间考虑，本节无法包含大量命令的详细描述——但只需查看列表就能让你有一个直观的了解。更多细节可以在相应的 man 手册中找到。

## 文档与图形转换 511

- `epsffit` 调整 EPS 文件的大小

- `extractres` 分析文件并为所有文件提供 `%%IncludeResource` 注释等

- `fixmps` 将 FrameMaker 文件适配为 psutils 标准

- `fixmacaps` 将 Macintosh 文件适配为 psutils 标准

- `fixscribeps` 将 ScScript 文件适配为 psutils 标准

- `fixtpps` 将 Troff/Tscript 文件适配为 psutils 标准

- `fixwfps` 将 WinWord 文件适配为 psutils 标准

- `fixwwps` 将 WordPerfect 文件适配为 psutils 标准

- `fixxwps` 将 MS Write 文件适配为 psutils 标准

- `getafm` 为字体描述生成 AFM 文件

- `includeres` 将提取的资源注释包含在文件中

- `psbook` 将页面组合成书页

- `psnup` 缩小页面尺寸

- `psresize` 调整页面尺寸

- `psselect` 从文件中提取单页

- `pstops` 将页面转换为 PostScript 页面

上述命令仅在 PostScript 文件包含注释时才有效。DSC 代表文档结构化。注释不会被打印，但包含了关于嵌入的信息（带有图像）。PostScript 文件在 Windows 下生成。

> 如果任务是将 man 格式化为 PostScript，则 rman 命令允许 man 页面转换。

## 文本格式化 (groff)

groff 是一种用于格式化 man 等文本的高级系统。在实践中，groff 程序起的是次要作用——例外是用于格式化易读的 ASCII 文本。groff 程序共同构成了一个与 LaTeX 可相比的排版系统，但在格式功能方面较简单。

以下对 groff 的描述仅解释将 man 源转换为 DVI 或 PostScript 文件的选项。

```
groff [options] file > target.file
```

- `-maname` 使用 `/usr/lib/groff/tmac` 目录下的宏文件。转换 man 时必须使用 `mandoc`。

- `-Tformat` 输出格式。默认设置为 `ps`（PostScript）。其他设置为 `dvi`（用于 dvi 文件）、`ascii`（用于 ASCII 文本）和 `latin`（带语言字符）。

如果 man 文本不仅以格式化版本存在，还以源码存在，可以使用 groff 将此文件转换为高质量的 PostScript 文件。源码可以在 man 目录（x 代表 1 到 9、n、g）中找到，例如 `/usr/man/manx`。以下命令将源码 `groff.1` 转换为 PostScript 格式并将结果写入主目录下的 `test.ps`：

```
user groff /usr/man/man1/groff.1 -mandoc > /book/test.ps
```

通过以下命令可以相同的结果（尽管控制有限）：

```
man -t groff > /book/test.ps
```

> 注意：Linux 发行版中的 man 文本仅提供预格式版本，因此无法使用 groff。在这种情况下，可以使用 rman 命令转换。

## info 文本格式化 (Texinfo)

info 文本通过 Texinfo 创建。Texinfo 系统的巨大优势在于源文件（后缀为 *.texi）可以同时创建 info 和 DVI 文件。生成的 *.dvi 文件可以通过 dvips 转换为 PostScript 文件并随后打印。因此，*.texi 文件既适用于创建在线文档，也适用于生成排版精美的手册。

