
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## termcap

`termcap` 包提供了 `/etc/termcap` 文件。`/etc/termcap` 是一个定义了各种终端和仿真器能力的数据库。程序使用 `/etc/termcap` 访问终端的不同功能（蜂鸣、颜色和图形等）。出自 Mandrake 9.0 RPM

http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## termcap-compat

旧版 `termcap` 程序的兼容性。`termcap–compat` 包提供了 `libtermcap.so.2` 和 `/etc/termcap` 文件，运行非 Debian、仅二进制的 `termcap` 程序所必需。由于基于 `libc6` 的程序希望与 `ncurses` (`slang`) 链接，此包仅提供基于 `lib5` 的库兼容性。运行 Debian-GNU Linux 仿真器不需要安装此包。如果一个程序（你无法重新编译）在运行时出现错误“message... = can’t find libtermcap.so.2”或缺少 `/etc/termcap`，请不要使用此包。`termcap–compat` 包并非用于编译需要 `termcap` 的程序，为什么不尝试用 `ncurses` 替换 `termcap` 呢？只需像用 `ncurses` 代替 `termcap` 一样简单（即在 `Makefile` 中将 ‘`-termcap`’ 替换为 ‘`-ncurses`’）。各种仿真程序将 `terminfo` 转换为文件中的 `termcap` 条目，因此你甚至不需要 `/etc/termcap` 文件。此包提供：`libtermcap` 共享库，版本 2.0.8；`termcap` 数据库，版本 10.2.7 出自 Debian 3.0r

http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## Terminal

一种向远程计算机发送命令的设备。至少，这通常意味着键盘和显示器以及一些电路。你通常在个人电脑上使用终端——软件模拟（仿真）物理终端，并允许你向别处的计算机输入命令。出自 Matisse

http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## 终端仿真

## Linux 词典

使用通信程序将计算机转换为终端，以进行数据通信。源自 QUECID http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## 模拟器

## 终端服务器

一种特殊用途计算机，一侧必须连接许多调制解调器，另一侧连接网络。因此，终端服务器负责接听来并将连接传递给相应的节点。大多数服务器提供连接到互联网的 `PPP` 或 `SLIP` 服务。源自 Matisse http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## 终端窗口

输入系统命令的应用程序屏幕。参见 `prompt`。源自 Redhat–9–Glosary http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## TERMINFO

终端信息 (Unix) 源自 VERA http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## terman

终端包装器源自 Whatis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## terraform

高度场投影。允许你创建一个分形（也称为高度场）并使用多种算法对其进行转换。它是为那些想要为光线追踪或其他仿真生成数字地形模型的人设计的。源自 Debian 3.0/0 APT http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## TES

技术启用营销源自 VERA http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## TESS

指数安全系统 (RFC 1824) 源自 VERA http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## test

检查文件类型并比较值源自 Whatis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

n. 1. 原型机上的真实用户希望彻底熟悉它，并对结果进行细致的监控和遵循。2. 一些无聊的用户尝试使用更简单的工具，同时有开发者在旁监视，准备防止错误发生。从大多数软件的质量来看，第二种定义更具相关性。另见 `demo`。源自 Jargon http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## testpmap

检查 `mb.conf` 的内部正确性源自 Whatis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## testprns

通过 Whatis 检查打印机名称的有效性 http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## tetex

`TeX` 是适用于 Linux 或 UNIX 系统的 `TeX` 的实现。`TeX` 以一个文件和一组格式命令作为输入，并创建一个 `.dvi`（设备无关）文件作为输出。通常，`TeX` 与 `LaTeX` 或 `PlainTeX` 等更高级软件包配合使用，`TeX` 本身对用户并不友好。如果你想使用该格式系统，如果你正在安装它，还需要安装 `tex-afm`（用于 `TeX` 的 PostScript(TM) 字体计数）、`tex-divmf`（用于将 `.dvi` 转换为 HP 格式以便在 HP 及兼容打印机上打印）、`tex-dvips`（用于将 `.dvi` 转换为 PostScript 格式以便打印）、`tex-latex`（一个为 `TeX` 提供更易于接口的高级格式软件包）以及 `tex-xdvi`（用于预览 `.dvi` 文件）。除非你精通 `TeX`，否则还应该安装包含 `TeX` 文档的 `tex-dev` 包。Red Hat 8.0 RPM http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## ethereal

网络流量分析器（控制台）。Ethernet 是一种用于 Unix 和类 Unix 操作系统的流量分析器或“嗅探器”。用于从线路上捕获数据。Ethernet 包含许多协议（无法列举）。该包提供了名为 "`tether`" 的 `ethereal` 版本。源自 Debian 3.0 APT http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## tetradraw

ANSI 绘图实用工具。`redraw` 是一种简单的绘图工具，让你可以使用如微笑之类的字符，而著名的单框和双框包含更多。前景和背景颜色的改变很难实现。`tetviewer` 是此类图像查看器。源自 Debian 3.0 APT http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## tech

由 Donald E. Knuth 编写的极其强大的宏文本格式化器，在计算机科学社区非常流行（它足够优秀可以取代 Unix `troff`，后者在许多安装中甚至更青睐）。`TeX` 被认为是在仅限 ASCII 的设备上接受的语言。`TeX` 坚持正确的（正统的）发音和拼写（全大写、压缩、带有基线）。粉丝们喜欢大量使用“`TeX`”一词——例如 Texian（`TeX` 用户）、Teacker（`TeX` 程序员）、Master（胜任的 `TeX` 程序员）和 Teax。Knuth 之成为 `TeX`，是因为他拒绝在他巨著《计算艺术》（`TeX` 也是圣经）中接受排版技术的衰落。作为解决手头及所有问题的典型冲动的体现，他开始设计自己的语言。他本以为他会在 1978 年休假期间完成它；他错了大约 8 年。该语言在 1985 年左右定型，即《计算艺术》的卷。`TeX` 的设计使得没有人需要它（注：此处可能为原文逻辑错误或误指，意指设计精良）。`TeX` 设计之初是为了解决高质量的排版问题。Knuth 设计了这种技术，以解决排版问题。Knuth 设计了这种技术是为了解决高质量的排版问题。Knuth 设计了这种技术是为了解决高质量的排版问题。Knuth 设计了这种技术是为了解决高质量的排版问题。Knuth 设计了这种技术是为了解决高质量的排版问题。Knuth 设计了这种技术是为了解决高质量的排版问题。Knuth 设计了这种技术是为了解决高质量的排版问题。

## tex

基于宏的文本格式化器。来自 http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## tex
