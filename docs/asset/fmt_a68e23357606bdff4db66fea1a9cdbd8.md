
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

`TeX`（读作 "tex"）是一个命令集合，主要用于生成科学和数学排版文档。使用 `TeX` 的常用方法是 `LaTeX`，它采用格式化方法。

> > 提示：本书中示例所需的 `tex-*` 包位于随附的 DVD 中。

`TeX` 解析 `LaTeX` 格式的宏。默认情况下，`latex.fmt` 和 `plain.fmt` 文件是在安装 `tex` 包时自动生成的。可以使用 `TeX` 的其他宏文件包括：

- `amstex` — 数学出版，包括美国数学学会的官方排版系统。
- `epile` — 用于索引和目录的宏。
- `texinfo` —— 生成软件手册的宏。

你可以使用任何文本编辑器创建 `TeX/LaTeX` 文档。在创建文本和宏后，你可以运行 `tex` 命令（或相关工具之一）来格式化文件。输入文件有三种：

- `filename.dvi` — 设备无关的输出文件，可以由多种设备（如 PostScript）转换。
- `filename.log` — 包含信息的日志文件。
- `filename.aux` — `LaTeX` 使用的辅助文件。

生成的 `.dvi` 文件可以针对特定设备格式化。例如，你可以使用 `dvips` 命令将生成的 `dvi` 文件输出到你的 PostScript 打印机 (`dvips filename.dvi`)。或者你可以使用 `xdv` 命令在 X 中预览 `dvi` 文件。

# 第 6 章：使用 Fedora 和 RHEL 发布文档

每个命令都定义了要执行的操作。该操作可以控制页面布局、使用的字体、间距、段落布局或文档的许多其他操作。`LaTeX` 文档可以包含的最少格式如下：

```
\documentclass{name}

\begin{document}

在此处输入文本！

\end{document}
```
