

- `ascii` — 生成纯文本输出，可通过终端窗口查看。
- `dvi` — 生成 TeX dvi 格式的输出，以便输出到后文描述的多种设备。
- `X75` — 生成适用于 X11 75 点/英寸预览器的输出。
- `X100` — 生成适用于 X11 100 点/英寸预览器的输出。
- `latin1` — 使用 ISO Latin-1 字符集生成类似打字机的输出。

### 使用 Groff 格式化和打印文档

您可以尝试使用 Red Hat Linux 系统上任意手册页（man page）（例如 `/usr/share/man/*` 中的那些）来格式化和打印现有的 Groff 文档。（由于这些手册页是压缩的，您可以将它们复制到临时目录并解压以测试 Groff。）

这些命令将 `chown` 手册页复制到 `/tmp` 目录并将其解压。然后，`groff` 以纯文本格式格式化 `chown` 手册页，以便您可以在屏幕上逐页浏览。

```bash
$ cp /usr/share/man/man1/chown.1.gz /tmp
$ gunzip /tmp/chown.1.gz
$ groff -Tascii -man /tmp/chown.1 | less
```

在上面的示例中，`chown` 手册页（`chown.1.gz`）被复制到 `/tmp` 目录，通过 `gunzip` 解压，并使用 man 宏（`-man`）以纯文本（`-Tascii`）格式输出。输出通过管道传递给 `less`，以便在屏幕上逐页浏览。除了通过管道传递给 `less`（`| less`），您也可以将输出定向到文件（`> /tmp/chown.txt`）。

要将手册页格式化为排版输出，您可以指定 PostScript 或 HP LaserJet 输出。您应该将输出定向到文件或打印机。以下是两个示例：

```bash
$ groff -Tps -man /tmp/chown.1 > /tmp/chown.ps
$ groff -Tlq4 -man -l /tmp/chown.1
```

第一个示例创建 PostScript 输出（`-Tps`）并将其定向到名为 `/tmp/chown.ps` 的文件。该文件可以被 PostScript 预览器（如 `ghostscript`）读取，或发送到打印机（`lpr /tmp/chown.ps`）。下一个示例创建 HP LaserJet 输出（`-Tlq4`）并将其定向到默认打印机（`-l` 选项）。

### 使用 Groff 创建手册页

在 HOW-TO 文档和 info 文件出现之前，手册页是关于 UNIX（及类 UNIX）系统信息的基础。每个命令、文件格式、设备或其他组件要么有自己独立的手册页，要么与相似组件分组在一个手册页中。创建自己的手册页要求您学习一些宏（特别是 man 宏）。图 6-1 显示了一个虚构的命令 `waycool` 的手册页源代码。

> **提示：** 大多数手册页存储在 `/usr/share/man` 的子目录中。在创建手册页之前，请参考类似的手册页，查看它们包含的标记和标题。`man1` 包含命令；`man2` 包含系统调用；`man3` 包含库函数；`man4` 包含特殊设备文件（`/dev/*`，`/*`）；`man5` 包含文件格式；`man6` 包含游戏；`man7` 包含杂项组件，`man8` 包含管理命令。

```text
." 
." waycool.1 - the roff document processor source for the waycool command 
." SH waycool 1 "May 12, 2002" GNU "Linux Programmer's Manual" 
.SH NAME 
waycool - my cool command 
.SH SYNOPSIS 
\fBwaycool\fR [ \fB-abcv\fR ] [ \fI file ... \fR ] 
.SH VERSION 
This man page documents the GNU waycool version X.XX 
.SH DESCRIPTION 
\fBwaycool\fR is a way cool command. 
.PP 
This version of \fBwaycool\fR is better than the last one. 
.SH OPTIONS 
.IP -a 
Run all options with it. 
.IP -b 
Run some options. 
.IP -c 
affect symbolic links instead of any referenced file 
(available only on systems that can change the 
ownership of a symlink) 
.IP -v 
Print the version number with the command. 
.SH COMMENTS 
If you don't like the command, don't tell me. It will just hurt my feelings. 
.SH ENVIRONMENT VARIABLES 
These environment variables are used by \fBwaycool\fR: 
.IP "DISPLAY" 
This sets the X Display variable. 
.IP "WAYCOOL" 
This contains the location of the waycool database. 
.SH FILES 
/usr/local/waycool - Directory containing waycool stuff. 
.SH AUTHOR 
Chris Craft <chris@handsonhistory.com> 
.SH "REPORTING BUGS" 
Report bugs to `bug-fileutils@gnu.org`. 
.SH COPYRIGHT 
Copyright \(co 2001 Free Software Foundation, Inc. 
.br 
This is free software\see the source for copling conditions. There is NO 
warranty\enot even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. 
.SH ACKNOWLEDGEMENTS 
I'd like to thank all my friends.
```

图 6-41：创建手册页只需简单的标记。

手册页中还使用了其他几种宏。`.IP` 宏为选项等项目格式化了缩进段落。手册页还包含一些低级字体请求；例如，`\fB` 表示将当前字体更改为粗体，`\fi` 将字体更改为斜体，`\fR` 将其改回常规字体。（这种标记比请求特定的字体类型更好，因为它只是将当前字体更改为粗体、斜体或常规。）图 6-2 显示了 `waycool` 手册页经过 `groff` 格式化后的外观：

```bash
$ groff -man -Tps -l waycool.1
```

![](img/1744bde8c889adfab3fc911e1687fecf_244_0.png)

图 6-2：手册页格式化添加了页眉并布局了文本页面。

表 6-1 列出了您可以在手册页中使用的宏。这些宏在 `man(7)` 手册页中有描述（输入 `man 7 man` 查看该页）。

### 表 6-1：Man 宏

| 宏 | 描述 | 宏 | 描述 |
| :---- | :---- | :---- | :---- |
| `B` | 粗体 | `BI` | 粗体，然后斜体（交替） |
| `BR` | 粗体，然后罗马体（交替） | `.DT` | 设置默认制表位 |
| `.HP` | 开始悬挂缩进 | `I` | 斜体 |
| `IB` | 斜体，然后粗体（交替） | `.IP` | 开始悬挂标签。用于选项。长标签使用 `.TP` |
| `.IR` | 斜体，然后罗马体（交替） | `.LP` | 开始段落 |
| `.PD` | 设置段落间距 | `.PP` | 开始段落 |
| `.RB` | 罗马体，然后粗体（交替） | `.RE` | 结束相对缩进（在 `.RS` 之后） |
| `RI` | 罗马体，然后斜体（交替） | `.RS` | 开始相对缩进（使用 `.RE` 结束缩进） |
| `.SB` | 小字号文本，然后粗体（交替） | `.SM` | 小字号文本。用于显示全大写字母。 |
| `.SH` | 节标题 | `.SS` | `.SH` 标题内的子标题。 |
| `.TH` | 标题页头。在手册页开头使用一次。 | `.TP` | 开始悬挂标签。文本从下一行开始，不与标签在同一行。 |

### 使用 Groff 创建信函、备忘录或白皮书

备忘录宏（使用 Groff 的 `-mm` 选项）曾一度在 UNIX 用户中很流行，用于生成技术文档、信函和备忘录。虽然具有各种所见即所得（WYSIWYG）模板的现代文字处理软件使 `mm` 变得过时，但在紧急情况下，`mm` 仍然可以在文本环境中快速创建排版风格文档。

要使用 `mm` 宏格式化并打印（到 PostScript 打印机）文档，请使用以下命令：

```bash
$ groff -mm -Tps -l letter.mm
```

以下是如何使用 `mm` 宏生成信函的简单示例：

```text
.WA "Christopher T. Craft"
999 Anyway Way
Anytown, UT 84111 USA
.WE
.IA
John W. Doe
111 Notown Blvd.
Notown, UT 84111
.IE
.LO RN "Our telephone conversation"
.LO SA "Dear Mr. Doe:"
.LT

In reference to our telephone conversation on the 4th, I am calling to
confirm our upcoming appointment on the 18th. I look forward to
discussing the merger. I believe we have a win-win situation here.
.FC "Yours Truly,"
.SG
```

如果您使用代码示例前一段中提到的 `groff` 命令行，信函的输出如图 6-3 所示。

![](img/1744bde8c889adfab3fc911e1687fecf_246_0.png)

`mm` 宏常用于生成技术备忘录。以下是一个签名页的示例，可能放置在较大的技术备忘录前面。

```text
.TL
Merger Technical Specifications
.AF "ABC Corporation"
.AU "Christopher Craft"
.AT "President"
.AS
This memo details the specifications for the planned merger.
.AE
.MT "Merger Description and Marching Orders"
As a result of our talks with XYZ corporation, we plan to go forward with the merger. This document contains the following:
.BL
.LI
Schedule and time tables.
.LI
Financial statements.
.LI
Asset allocations.
.LE
.SP
Please add corrections and sign the approval line.
.FC
.SG
.AV "John W. Doe, XYZ Corporation President"
.AV "Sylvia Q. Public, XYZ Corporation CFO"
.NS
Everyone in the corporation.
.NE
```

图 6-4 显示了此备忘录的输出。

