
$ cp `/usr/share/man/man1/chown.1.gz` `/tmp`

$ gunzip `/tmp/chown.1.gz`

$ groff -Tascii -man `/tmp/chown.1` | less

在这个示例中，帮助页（`chown.1.gz`）被复制到 `/tmp` 目录，被解压（使用 `gunzip`），并使用 man 宏（`-man`）以纯文本（`-Tascii`）输出。输出通过管道传给 `less`，以便在屏幕上翻页。与其管道传给 `less`（`| less`），你可以将输出重定向到文件（`> /tmp/chown.txt`）。

# 第 20 章 ✦ 处理文字与图像 513

为了排版对地图进行格式化，可以使用系统上的任何页面。开箱即用的可以指定 PostScript 或 HP LaserJet 输出。将输出定向到文件或打印机。这里有几个示例：

```
$ groff -Tps -man /tmp/chown.1 > /tmp/chown.ps

$ groff -Tlj4 -man /tmp/chown.1
```

第一个示例创建了 PostScript 输出（`-Tps`）并将其定向到名为 `/tmp/chown.ps` 文件。该文件可以使用 PostScript 查看器（如 Ghostscript）读取，或发送到打印机（`lpr /tmp/chown.ps`）。下一个示例创建了 HP LaserJet 输出（`-Tlj4`）并将其定向到默认打印机选项。

# 使用 Groff 创建帮助页

在 HOWTO 和文件之前，帮助页是关于 UNIX 和类 UNIX 系统的基础。每个命令、文件、格式或组件都有它自己的帮助页，或者分组在类似组件的帮助页中。创建自己的帮助页需要学习一些宏（特别是格式化宏）。图 20-3 显示了一个名为 `waycool` 的虚拟帮助页源码。

```
.waycool.1 - roff processor for waycommand

# "Linux Programmer's Manual" 2000

# waycool 1, my cool command

# NAME

# SYNOPSIS

# groff [ -l [ file ... ]

# 此帮助页描述 GNU waycommand version.XX

# EXPLANATION

# waycool 是一个 cool 命令。

# 这个版本的 groff 比上一个好。

# OPTIONS

# -l 所有的选项。

# 使用符号代替任何引用（在可以更改符号缩进的系统中可用）。

# -V 命令的版本号。

# COMMENTS

# 如果你喜欢这样，别告诉我，这会让我伤心的。

# 这些环境变量被 groffvr 使用；

# -DISPLAY

# 这设置显示变量。

# FILES

# 包含 waycommand 数据库的位置。

# /usr/local/waycool - 包含 waycommand 内容的目录。

# AUTHOR

# Craft Craig (chrismandhistory.com)

# REPORTING BUG

# 反馈至 bug-filing@gnu.org。

# COPYRIGHT

# Free Software Foundation, Inc.

# © 2001 根据复制条件的自由软件。没有

# 保证（除非另有提到）适用于性或特定用途。

# ACKNOWLEDGEMENTS

# 我感谢所有的朋友。
```

图 20-3：创建帮助页需要简单的标记。

# 514 第四部分 ♦ 运行应用程序

大多数帮助页存储在 `/usr/share/man` 的子目录下。在创建帮助页之前，参考类似的帮助页以查看它们包含的标记和标题。`man1` 有系统调用；`man3` 有库函数；`man4` 有设备文件（`/dev/*`）；`man5` 有格式；`man6` 有游戏；`man7` 有杂项；`man8` 有管理命令。

帮助页中使用了其他类型的宏。`.JP` 宏用于选项等内容的缩进段落。帮助页还包含低级字体请求；例如，`\fb` 将当前字体加粗，`\ir` 将其改回普通字体。这种标记比使用特定字体类型的标记更好（因为它可以将字体变为加粗、斜体或普通）。图 20-4 显示了 waycol 帮助页在使用 groff 格式化后的样子：

```
$ man -Tps -1 waycol.1

waycol(1)                                     waycol(1)

Linux Pages Manual

NAME

waycol - 列出命令

SYNOPSIS

waycol [option] file, ...

VERSION

此帮助页描述 GNU waycol 命令。

DESCRIPTION

waycol 是一个 waycol 命令。这个版本的 waycol 比上一个好。

OPTIONS

- 加粗。

- 使用斜体。

- 使用语法代替任何引用（仅适用于可以更改符号缩进的系统）

-- 带命令打印行号。

ENVIRONMENT VARIABLES

这些变量被 waycol 使用：

DISPLAY

这设置 DISPLAY 变量。

WAYCOL

这设置 waycol 数据库的位置。

FILES

/usr/local/directory - 包含 waycol 文件的目录。

AUTHOR

Chris Clark <chris@linuxmaster.com>

REPORTING BUGS

请向 bugs@freesoftware.org 报告 bug。

COPYRIGHT

Copyright © 1999 Free Software Foundation, Inc. 版权所有。没有保证，除非：适用于性或特定用途。

ACKNOWLEDGMENTS

我会告诉所有的朋友。
```

图 20-4 帮助页格式化添加了页眉并布局了文本页。表 20-1 列出了你可以在帮助页上使用的宏。这些宏在 `man(7)` 手册中有描述（输入 `man 7` 查看该页面）。

# 表 20-1 帮助页宏

| 宏 | 描述 |
| :--- | :--- |
| .B | 加粗 |
| .BI | 加粗后斜体（交替） |
| .BR | 加粗后正体 |
| .DT | 设置默认值 |
| .HP | 开始标题 |
| .L | 左对齐 |
| .IB | 斜体 |
| .IR | 斜体 |
| .IP | 缩进段落 |
| .LP | 左段落 |
| .PP | 新段落 |
| .RB | 右加粗 |
| .RE | 缩进 |
| .RI | 斜体缩进 |
| .RS | 右缩进 |
| .SB | 小号加粗 |
| .SM | 小号文本 |
| .SH | 节标题 |
| .SS | 副标题 |
| .TH | 标题 |
| .TP | 标签段落 |

# 使用 Groff 创建信、备忘录或白皮书

备忘录宏（配合 `-mm` 选项使用）深受 UNIX 用户欢迎，用于制作技术文档、信件和备忘录。虽然具有各种模板的现代文字处理器已使 mm 宏过时，但在需要时它们仍然是在文本环境中创建排版风格文档的快速方法。

使用 mm 宏格式化并打印（到 PostScript 打印机）文档，请使用命令：

```
$ groff -mm -Tps -l letter.mm
```

这是一个使用 mm 宏制作信的简单示例：

```
.WA "Christopher T. Craft"

999 Anyway Way

Anytown, UT 84111 USA

.WE

.IA

John W. Doe

111 Notown Blvd.

Notown, UT 84111

.IE

.LO RN "我们的电话对话"

.LO SA "亲爱的 Doe 先生："

.LT
```

关于我们 4 号的电话对话，我致电是为了确认我们即将到来的 18 号的预约。我期待讨论合并。我相信这是一个双赢的局面。

```
.FC "您诚恳的."

.SG
```
