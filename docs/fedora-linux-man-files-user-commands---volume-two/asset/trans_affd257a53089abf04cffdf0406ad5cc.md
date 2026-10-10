

## 作者

由 Ross Paterson 撰写。

## 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 请向 <http://translationproject.org/team/> 报告 fmt 翻译错误。

## 版权

Copyright © 2015 自由软件基金会，Inc. 许可证 GPLv3+：GNU GPL 第 3 版或更高版本 <http://gnu.org/licenses/gpl.html>。这是自由软件：您可以自由修改和重新分发它。在法律允许的范围内，**不提供任何保证**。

## 另请参阅

完整文档位于：<http://www.gnu.org/software/coreutils/fmt> 或通过以下命令本地可用：`info ‘(coreutils) fmt invocation’`

# FONT2C

## 名称

font2c - 将 PostScript Type 0 或 Type 1 字体写入 C 代码

## 语法

`font2c fontnames`

## 描述

此脚本使用以下选项调用 `gs(1)`：

    -q -dNODISPLAY -dWRITESYSTEMDICT

后跟来自命令行的参数。这将把 PostScript Type 0 或 Type 1 字体编写为 C 代码，该代码可以与解释器链接。

## 另请参阅

`gs(1)`

## 版本

本文档最后一次修订是针对 Ghostscript 版本 9.16。

## 作者

Artifex Software, Inc. 是 Ghostscript 的主要维护者。此手册页由 George Ferguson 编写。

# FONTTOSFNT

## 名称

fonttosfnt - 将位图字体封装在 sfnt (TrueType) 包装器中

## 语法

`fonttosfnt [ options ] -o file.ttf [ --- ] font...`

## 描述

将位图字体或一组位图字体封装在 sfnt (TrueType 或 OpenType) 包装器中。

## 选项

- `-v`
  显示详细信息。
- `-c`
  不裁剪字形。这通常会增加文件大小，但对于小字符单元字体（终端字体），有时可能会使文件大小适度减小。
- `-b`
  写入字节对齐的字形数据。默认情况下，写入未对齐的数据，这会生成较小的文件大小。
- `-r`
  不重新编码字体。默认情况下，尽可能将字体重新编码为 Unicode。
- `-g n`
  设置我们要写入的可缩放字形的类型。如果 n 为 0，则不写入可缩放字形；这是合法的，但会让当前大多数软件感到困惑。如果 n 为 1，则写入单个可缩放字形（未定义的字形）；这是推荐的，但会触发当前版本 `FreeType` 中的一个 bug。如果 n 为 2（默认值），则写入足够数量的空白字形，这在 `FreeType` 中可以正常工作，但会增加文件大小。
- `-m n`
  设置我们要写入的可缩放度量值的类型。如果 n 为 0，则不写入可缩放度量值，这可能是合法也可能不合法。如果 n 为 1，则写入单个字形的完整度量值，并为其他字形仅写入左侧边距值。如果 n 为 2，则写入所有字形的可缩放度量值，这会增大文件大小且不推荐。默认值为 1。

---

选项结束。

## 错误

某些字体级别的值，特别是下标和上标位置，是占位值。

## 另请参阅

`X(7)`, `Xserver(1)`, `Xft(3x)`。*X11 中的字体*。

## 作者

X.Org 基金会发布的此版本 `Fonttosfnt` 最初由 Juliusz Chroboczek <jch@freedesktop.org> 为 XFree86 项目编写。

# FOOMATIC-CLEANUPDRIVERS

## 名称

foomatic-cleanupdrivers - 删除没有命令行的驱动程序条目

## 语法

`foomatic-cleanupdrivers [DBDIR]`

## 描述

`foomatic-cleanupdrivers` 命令删除所有命令行空的驱动程序 XML 文件。

它不打算直接由用户调用。

# FOOMATIC-COMBO-XML

## 名称

foomatic-combo-xml - <在此处放置简短描述>

## 语法

`foomatic-combo-xml [OPTION]...`

## 描述

由 Till 用 C 编写的 Foomatic 加速引擎，它计算打印机/驱动程序组合 XML 文件和打印机概览 XML 文件。

## 退出状态

`foomatic-combo-xml` 返回 ???

## 作者

Manfred Wassmann <manolo@NCC-1701.B.Shuttle.de> 为 foomatic 项目编写，使用相关二进制的输出。

## 错误

此手册页需要编辑。

请在以下位置发布错误报告：
<http://lists.freestandards.org/mailman/listinfo/printing-foomatic>

# FOOMATIC-COMPILEDB

## 名称

foomatic-compiledb - 编译 Foomatic 打印机/驱动程序数据库

## 语法

`foomatic-compiledb [ -t type ] [ -f ] [ -j n ] [ driver ... ]`

## 描述

`foomatic-compiledb` 为所有可能的打印机/驱动程序组合生成所有 PPD 文件或 Foomatic 组合 XML 文件，或者仅为选定范围的驱动程序生成。通常除非想要生成一组用于分发的 Foomatic 数据文件，否则不需要这样做。对于配置单个打印机，`foomatic-ppdfile(1)` 和特别是 `foomatic-configure(1)` 会自动计算它们所需的内容。

### 选项

- `-t type`
  输出文件类型，即 ppd 或 xml。
- `-f`
  强制：即使目标目录已存在也写入其中。
- `-j n`
  n = 要运行的工作进程数
- `driver ...`
  仅为这些驱动程序生成数据文件

## 另请参阅

`foomatic-ppdfile(1)`, `foomatic-configure(1)`

## 退出状态

除非发生意外情况，`foomatic-compiledb` 返回 0。

## 作者

Manfred Wassmann <manolo@NCC-1701.B.Shuttle.de> 和 Till Kampeter <till.kampeter@gmail.com> 为 foomatic 项目编写，使用相关二进制的输出。

## 错误

现有文件始终被保留，而不是覆盖旧文件。因此建议删除目标目录 (`rm -rf dir`) 并在不带 `-f` 选项的情况下调用 `foomatic-compiledb`。

请在以下位置发布错误报告：

<http://lists.freestanders.org/mailman/listinfo/printing-foomatic>

# FOOMATIC-CONFIGURE

## 名称

foomatic-configure – foomatic 打印系统的主要配置程序。

## 语法

`foomatic-configure [OPTION]...`

`foomatic-configure -n queue name [ -N description ][ -L location ][ -c connect ][ -d driver ][ -p printer ][--ppd ppdfile ][ -s spooler ][ -C [ sourcespooler ] sourcequeue ][ -o option1=value1 -o ... ][ -q]`

`foomatic-configure -D -n queue name [ -s spooler ][ -q ]`

`foomatic-configure -R -n queue name [ -s spooler ][ -q ]`

`foomatic-configure -Q [ -s spooler ][ -n queue name ][ -r ]`

`foomatic-configure -P [ -s spooler ][ -n queue name ][ -d driver ][ -p printer ][-- ppd ppdfile ][ index ]`

`foomatic-configure -X -p printer | -d driver | -p printer -d driver`

`foomatic-configure -O`

`foomatic-configure -h`

`foomatic-configure --help`

## 描述

`foomatic-configure` 是一个为所有已知打印队列（CUPS、LPing、LPD、GNUlpr、PPR、PDQ、CPS、无打印队列）和 Foomatic 数据库中所有有效的打印机/驱动程序组合或 PostScript 打印机附带的任何 PPD 文件设置和配置的程序。作为 RIP 过滤器（光栅图像处理器，将 PostScript 转换为打印机原生语言），始终使用 `foomatic-rip(1)`，除了 CUPS 或 PPR 下 PostScript 打印机的 PPD 文件外，它们将不使用 RIP 过滤器。

它还包括用户工具的程序化 API 的一半：你可以在这里学习和控制有关打印队列静态属性的所有内容。与姊妹程序 `foomatic-printjob(1)` 一起，你可以执行与打印队列动态状态相关的所有操作：提交任务，并查询、取消、重新排序和重定向它们。

### 选项

- `-n queuename`
  配置此打印队列
- `-N Name/Description`
  使用此适当的人类可读名称/描述
- `-L Location`
  描述此打印机位置的简短短语
- `-c connection`
  打印机连接方式（例如 file:/dev/lp0）
- `-d driver`
  所需打印机驱动程序的 Foomatic 数据库名称
- `-p printer`
  打印机的 Foomatic id
- `--ppd ppdfile`
  PPD 文件，例如 PostScript 打印机制造商提供的文件
- `-s spooler`
  显式打印队列类型（cups, lpd, lprng, pdq, ppr, direct）
- `-o option=value`
  将选项的默认值设置为 value
- `-o option`
  默认开启选项
- `-D`
  将此队列设置为默认队列（只需提供 `-n queuename`）
- `-R`
  完全移除此队列（只需提供 `-n queuename`）
- `-C [ sourcespooler ] sourcequeue`
  将 sourcequeue 从 sourcespooler（如果未提供 sourcespooler 则为当前打印队列）复制到由 `-n queuename` 给出的队列（当前打印队列）。

