
# patch

patch 是一个程序，它接收 `diff` 的输出，并将结果中的差异应用到原始文件中，以生成修改后的版本。如果有人感兴趣的话，它在开发源代码控制系统时会非常有用。

# PCL

PCL 是 CLOS（通用 Lisp 对象系统）大量子集的一个免费实现。它可以在 CLISP（前文提及）下运行。

# perl

perl 是由 Larry Wall 开发的一种编程语言，它结合了 sed、awk、shell 编程和 C 语言的特性与功能，同时还提供系统调用和许多 C 库例程的接口。对于不依赖复杂数据结构的复杂应用程序，perl 已变得非常流行。GNU Emacs 19 包含用于编辑 perl 代码的 "perl" 模式。

# ptx

GNU ptx 是传统置换索引生成器的 GNU 版本。它一次可以处理多个输入文件，产生与 TeX 兼容的输出，并且无需使用 nroff 程序即可生成可读的 KWIC（关键词在文中）索引。

# rc

rc 是一个具有类 C 语法（甚至比 csh 更甚）的 shell，并且拥有比 C 和 Bourne shell 更好的引用规则。它可以交互使用或用于脚本中。

# RCS

修订控制系统（RCS）用于软件项目的版本控制和管理。当与 GNU diff 一起使用时，RCS 可以处理二进制文件，如可执行文件和目标文件。有关 RCS 的更多信息，请参见第 56 章。

# recode

GNU *recode* 在字符集和用法之间转换文件。当无法进行精确转换时，它会删除任何违规字符或回退到近似值。该程序识别或生成近 150 种不同的字符集，并能够几乎在任何两个字符集之间转换文件。

# regex

regex 是 GNU 正则表达式库，其例程已在许多 GNU 程序中使用。现在它最终可以单独使用了。*sed* 编辑器附带了此库的一个更快版本。

# Scheme

Scheme 是一种与 LISP 相关的语言。主要区别在于，Scheme 可以将函数作为参数传递给另一个函数，可以将函数作为函数调用的结果返回，并且函数可以是表达式的值，而无需在特定名称下定义。

# screen

screen 是一个终端多路复用器，可以在单个物理字符终端上运行多个独立的“屏幕”（ttys）。每个虚拟终端都模拟 DEC VT100 及额外功能。*screen* 会话可以闲置，并在稍后不同类型的终端上恢复。

# sed

sed 是 *ed* 的非交互式、面向流的版本。它经常在 shell 脚本中使用，对于对一组文件应用重复编辑或创建转换程序非常有用。GNU sed 附带 rx 库，它是 *regex* 的一个更快版本。

# Shellutils

Shellutils 可以交互使用或在 shell 脚本中使用，并包括以下程序：*basename、date、dirname、echo、env、expr、false、groups、id、nice、nohup、printenv、printf、sleep、stty、su、tee、test、true、tty、uname、who、whoami* 和 *yes*。

# Smalltalk

GNU Smalltalk 是用 C 编写的解释型面向对象编程语言系统。Smalltalk 本身最近已在程序员中变得极其流行，并倾向于被视为一种“纯粹”的面向对象实现语言。

GNU Smalltalk 的特性包括二进制映像保存功能、调用用户编写的 C 代码并向其传递参数的能力、GNU Emacs 编辑模式、可以在 Smalltalk 内部调用的 X 协议版本，以及自动加载的每个用户初始化文件。它实现了 Smalltalk-80 中的所有类和协议，除了与图形用户界面（GUI）相关的类。

# Superopt

Superopt 是一个函数序列生成器，它使用重复的生成-测试方法来查找给定函数的最短指令序列。接口很简单：你向 GNU 超级优化器 gso 提供一个函数、要生成代码的 CPU 以及你接受的指令数量。

# tar

GNU tar 是一个文件归档程序，包括多卷支持、自动归档压缩/解压缩、远程归档，以及允许 tar 用于增量和完整备份的特殊功能。

# Termcap Library

GNU Termcap 库是 **libcrtmcap**.a 库的替代品。与大多数其他 Termcap 库不同，它不对 Termcap 条目的大小设置任意限制。

# TeX

TeX 是一个处理复杂排版（包括数学）的文档格式化系统。它是 GNU 的标准文本格式化器。有关 TeX 的更多信息，请参见第 19 章 “TeX 和 LaTeX”。

# Texinfo

Texinfo 是一组实用程序，可生成印刷手册和在线超文本风格文档（称为 “Info”）。也存在用于阅读在线 Info 文档的程序。第 3 版既包括 GNU Emacs Lisp，也包括用 C 或 shell 脚本编写的独立程序。GNU Emacs 的 texinfo 模式使 texinfo 文件的编辑和更新变得容易。提供的程序包括 makeinfo、info、texi2dv1、texindex、tex2patch 和 fixfonts。

# Textutils

TextUtils 程序操作文本数据，包括以下传统程序：cat、ckssum、comm、csplit、cut、expand、fold、head、join、nl、od、paste、pr、sort、split、sum、tac、tail、tr、unexpand、uniq 和 wc。

# Tile Forth

Tile Forth 是用 C 编写的 Forth-83 标准的 32 位实现。传统上，Forth 实现是用汇编器编写的，以尽可能优化地使用底层硬件，但这也使它们的可移植性较差。

# time

time 用于报告进程使用的用户时间、系统时间和实际时间的统计信息（通常来自 shell）。

# tput

tput 是 shell 脚本使用特殊终端功能的一种可移植方式。GNU tput 使用 Termcap 数据库，而不是许多其他工具使用的 Termio。

# UUCP

此版本的 UUCP（UNIX-to-UNIX copy）支持 f、g、v（在所有窗口和包大小下）、G、t、e、Zmodem 以及两个新的双向（i 和 j）协议。如果你有 Berkeley sockets 库，它可以建立 TCP 连接。如果你有 TLI 库，它可以建立 TLI 连接。

# uuencode/uudecode

uuencode 和 uudecode 用于通过仅支持简单 ASCII 数据的传输介质传输二进制文件。这两个实用程序最常见的用途是在 Usenet 新闻组中。

# wdiff

wdiff 是 GNU diff 程序的另一个接口。它比较两个文件，找出在创建第二个文件时第一个文件中删除或添加了哪些单词。它有许多输出格式，并与终端和诸如 more 等程序很好地交互。当两个文本仅相差几个单词且段落已被重新填充时，wdiff 特别有用。

## Summary

GNU 项目向所有人免费提供类 UNIX 软件，条件是如果分发给他人，它必须保持免费。GNU 软件可以为许多不同类型的系统进行编译，包括 Linux。许多 GNU 实用程序是现有 Linux 对应物的改进版，并包括 shell、C 编译器以及代码调试器的新实现。其他类型的 GNU 软件包括游戏、文本编辑器、计算器和通信实用程序。每个实用程序都可以单独解压缩、解 tar 并自行编译。

从这里，你可以阅读相关主题：

- 使用 vi 和 Emacs 等文本编辑器编写自己的文档在第 16 章 “文本编辑器：vi 和 emacs” 中介绍。
- 在连接的打印机上打印文档在第 20 章 “打印” 中介绍。
- 使用 awk 语言进行编程，这对于管理文件和匹配模式非常有用，在第 25 章 “gawk” 中介绍。

# CHAPTER 11

# bash

作者：Rick McMullin 和 Tim Parker

# 本章内容

- Shell 简介 204
- 再次 Bourne shell 207
- 自定义 bash 220
- bash 命令摘要 221

