

## 第 6 章：在 Fedora 和 RHEL 上发布

- `me` 宏在 Berkeley UNIX 系统上用于生成备忘录和技术论文。使用 `-me` groff 选项格式化 me 文档。

Groff 宏包存储在 `/usr/share/groff*/tnac`。`man` 宏从 `.tmac` 文件调用，`mm` 宏来自 `.tmac`，`me` 宏来自 `.etmac`。每个宏包的命名约定为 `xxx.tmac`，其中 `xxx` 替换为一个或多个代表宏包的字母。在每情况下，你都可以在后缀文件的开头添加 `an` 来理解它。

> > 提示：与其指定特定的宏包，你可以使用 `-mandoc` 来选择宏包。

当你运行 groff 格式化命令时，可以在命令行上指定你正在使用的宏包。你还可以指定文档通过以下任何一个命令来运行，这些命令会对特定格式的文本进行预处理：

- `eqn` 该处理器格式化在 groff 中生成方程的宏。
- `pic` 该处理器格式化在 groff 中创建简单线条图的宏。
- `tbl` 该处理器格式化在 groff 中生成表格的宏。
- `ps` 为 PostScript 打印机或 PostScript 查看器产生 PostScript 输出。
- `lj4` 为 HP LaserJet 打印机或其他兼容 PCL5 的打印机产生输出。
- `ascii` 可以在终端窗口查看的纯文本输出。
- `dvi` 生成 Tex dvi 输出，输出到后文描述的各种设备。
- `X75` 为 X11 75 点/英寸查看器产生输出。
- `X100` 为 X11 100 点/英寸查看器产生输出。
- `latin1` 使用 ISO Latin-1 字符集产生类打字机输出。

格式化后的 Groff 文档输出到特定设备。该设备可以是打印机、窗口或纯文本。Groff 支持的输出格式有：

## 使用 Groff 格式化和打印文档

你可以尝试使用 Fedora 或 RHEL 系统上的任何页面（例如 `/usr/share/man/*` 中的页面）来格式化现有的 Groff 文档。这些页面是经过压缩的，因此你可以将它们复制到临时目录并解压，以便由 Groff 输出。

这些命令将 `chown` man 页面复制到 `/tmp` 目录并解压。然后 Groff 将 man 页面格式化为纯文本，以便你可以在屏幕上打印。

```
$ cp /usr/share/man/man/chown.1.gz /tmp
$ gzip /tmp/chown.1.gz
$ groff -Tascii -man /tmp/chown.1 | less
```

在前面的示例中，`chown` man 页面 (chown.1.gz) 被复制到 `/tmp` 目录，被解压（使用 gzip），并使用 man 宏 (-man) 以纯文本格式输出。输出通过管道传输给 less，从而在你的屏幕上显示。与其传给 less (`| less`)，你可以将输出重定向到文件 (`>tmp/chown.txt`)。

## 258 第二部分：使用 Fedora 和 RHEL

为了排版 man 页，你可以指定 PostScript 或 HP LaserJet 输出。你应该将输出重定向到文件或打印机。这里有几个例子：

```
$ groff -Tps -man /tmp/chown.1 > /tmp/chown.ps
$ groff -Tlj4 -man -1 /tmp/chown.1
```

第一个示例创建了 PostScript 输出 (-Tps) 并将其重定向到文件 `/tmp/chown.ps`。该文件可以由 PostScript 查看器（如 Ghostscript）读取或发送到打印机 (lpr /tmp/chown.ps)。下一个示例处理 LaserJet 输出 (-Tlj4) 并将其重定向到默认选项。

> > 提示：你可以将 man 页转换为 HTML 格式以便在浏览器中查看。例如：`cat /usr/share/man/man1/chown.1.gz | man2html | /tmp/chown.html`。

## 使用 Groff 创建 man 页

在有了 info 文件之前，man 页是 UNIX（以及类 UNIX）系统信息的字体。每个命令、文件格式、设备或其他都有自己的 man 页，或者分组在具有相似组件的 man 页中。创建你自己的 man 页需要学习一些宏（特别是 man 宏）。图 6-3 显示了一个虚构命令 `waycool` 的 man 页源码。

```
. the document processor source for the command waycool
.TH way 1 "May 12, 2000" "GNU Linux Programmer's Manual"
.SH NAME
.waycool -v my cool command
.BR
.BfwaycoolVR [V-abfVR] [I file ...]
.SH SYNOPSIS
This man page documents the GNU waycool usage X,XX
.SH DESCRIPTION
.BfwaycoolVR is a cool command.
.SH VERSION
The first version of \waycoolVR is better than the last one.
.SH OPTIONS
-o
-a
带文件运行所有选项。
-f
影响对任何引用的文件生效，仅在可以更改符号链接行为的系统中可用。
-v
带命令打印版本号。
.SH COMMENTS
如果你喜欢这个命令，请不要告诉我。这会伤害我的朋友。
.SH ENVIRONMENT
\waycoolVR 使用了一些环境变量：
.SH UID
这设置了 UID 显示变量。
.SH PATH
这包含了 waycool 数据库的位置。
.SH FILES
.Bf
/usr/local/share/commodity.com/
.SH REPORTING
向 waycool 功能报告 bug。
.SH COPYRIGHT
Copyright (c) 2003 Free Software Foundation, Inc.
.AR
这是免费软件：有些用于复制命令。对于维护性或适用于特定用途不提供任何保证。
.SH ACKNOWLEDGEMENTS
我想和所有的朋友们谈谈。
```

图 6-3：创建 man 页需要简单的标记。

## 第 6 章：在 Fedora 和 RHEL 上发布 259

> > 提示：大多数 man 页存储在 `/usr/share/man` 的子目录下。在创建页面之前，请参考类似的 man 页以查看标记和包含的头部：man1 是命令；man2 是系统调用；man3 是库函数；man4 是设备文件 (/dev/*)；man5 是文件格式；man6 是游戏；man7 是杂项组件；man8 是管理命令。

man 页中还使用了其他宏。`IP` 宏格式识别使用偏移量的内容的段落。man 页还包含低级请求，例如，`\B` 将当前字体更改为粗体，`\I` 将字体更改为斜体，`\R` 恢复正字体。（这比请求特定字体要好，因为它只是将当前字体变为粗体、斜体或正字体。）图 6-4 显示了 weeway man 页在用 groff 格式化后的样子：

```
$ groff -man -Tps -1 weeway,1
```

| weeway(1) Linux Programmer's Manual | weeway(1) |
| :--- | :--- |
| NAME weeway - my command. | |
| SYNTAX weeway [option] [file], ... | |
| VERSION This page does not contain the GNU man page version X.XX. | |
| DESCRIPTION weeway is a cool command. This version of weeway is better than the last one. | |
| OPTIONS -B font in bold.\\n-I font in italic.\\n-U offset text in underline of any reference text (available only on systems that support the selection of text).\n-t Print the version number with the command. | |
| COMMENTS If you like this command, don't tell me. It will just hurt my friends. | |
| ENVIRONMENT Some environment variables are used by \waycoolVR:\nDISPLAY This sets the UID variable.\nPATH This contains the location of the waycool database. | |
| FILES .Bf\n/usr/local/share/commodity.com/ | |
| REPORTING Report bugs to waycool functionality. | |
| COPYRIGHT Copyright (c) 2003 Free Software Foundation, Inc.\n.AR\nThis is free software: some for copying commands. There is NO\nguarantee for MAINTAINABILITY or FITNESS A PARTICULAR PURPOSE. | |
| ACKNOWLEDGEMENTS I'd like to talk to all of my friends. | |

图 6-4：创建 man 页需要简单的标记。

## 使用 TeX/LaTeX 处理文本

TeX（读作 "tex"）是一个命令集合，主要用于生成科学和数学排版文档。使用 TeX 的常用方法是 LaTeX，它采用格式化方法。

> > 提示：本书中示例所需的 `tex-*` 包位于随附的 DVD 中。

TeX 解析 LaTeX 格式的宏。默认情况下，`latex.fmt` 和 `plain.fmt` 文件是在安装 tex 包时自动生成的。可以使用 TeX 的其他宏文件包括：

- amstex — 数学出版，包括美国数学学会的官方排版系统。
- epile — 用于索引和目录的宏。
- texinfo —— 生成软件手册的宏。

你可以使用任何文本编辑器创建 TeX/LaTeX 文档。在创建文本和宏后，你可以运行 `tex` 命令（或相关工具之一）来格式化文件。输入文件有三种：

- filename.dvi — 设备无关的输出文件，可以由多种设备（如 PostScript）转换。
- filename.log — 包含信息的日志文件。
- filename.aux — LaTeX 使用的辅助文件。

生成的 .dvi 文件可以针对特定设备格式化。例如，你可以使用 `dvips` 命令将生成的 dvi 文件输出到你的 PostScript 打印机 (dvips filename.dvi)。或者你可以使用 `xdv` 命令在 X 中预览 dvi 文件。

(注：由于原文存在大量重复和 OCR 错误，翻译内容已根据核心逻辑进行了去重和清理，确保输出的可读性并符合您的要求。由于输入中包含大量重复的段落和 OCR 错误，我将提供最终的、干净的输出。)

