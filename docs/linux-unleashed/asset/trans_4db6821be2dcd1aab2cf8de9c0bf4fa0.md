

## 列表框

列表框控件使 Tk 应用程序的用户能够从由一个或多个项组成的列表中选择项目。如果要在列表框中显示的项目数量多于列表框的行数，则可以附加滚动条以访问额外的项目。

## 滚动条

滚动条控件用于控制其他控件中显示的内容。滚动条控件附着在其他控件上，允许用户在控件所包含的信息中上下滚动。通常，你会在任何被设计为包含任意行数信息的控件（例如列表框）或包含行数超过其大小所能显示的行数的控件上放置滚动条。

## 摘要

本章首先介绍 Tcl 和 Tk 工具包，并描述了两者的用途。尽管本章包含大量信息，但它仅触及了 Tcl 和 Tk 工具包所提供的编程工具的皮毛。

Tcl 拥有比本书描述得更多的编程特性。其中一些最显著的特性包括数组、列表和过程。也并非所有的 Tk 控件都在此处有所描述。我们未深入介绍的一些控件包括画布、刻度、标签、消息和文本编辑控件。如果你对深入学习 Tcl 和 Tk 感兴趣，请查阅相关主题的书籍。

Tk 只是 Tcl 扩展的一个示例。还有许多其他可用的扩展，它们以不同的方式扩展了 Tcl 的行为。其中一些扩展如下：

- **Ak**：一个用于 Tcl 的音频扩展，Ak 提供了用于声音录制和播放的众多命令。
- **XF**：一个针对 Tk 的交互式图形用户界面开发器。
- **Tcl-DP**：一个帮助程序员使用 Tcl 开发分布式应用程序的 Tcl 扩展。

要了解更多信息

- 关于 Linux 上支持的其他编译器，请参见第 30 章，“其他编译器”。
- 关于 CGI 编程（Perl 特别适合此项），请参见第 52 章，“CGI 脚本”。

## 其他编译器

作者：Tim Parker

### 本章内容

- Ada 538
- COBOL 538
- DSP 539
- Eiffel 539
- FORTRAN 539
- LISP 540
- Modula-3 540
- OGI 语音工具 541
- Scheme 541
- Scilab 541

在本节中，迄今为止我们已查看了一些流行编程语言及其在 Linux 下的支持情况。也许你并不是 C、C++、awk、Perl 或 Tcl 的忠实粉丝。也许你真的很想在你的 Linux 机器上使用 Ada 或 FORTRAN 进行编程。不要灰心。Linux 拥有种类繁多的语言编译器和支持工具，它们已被移植以在此操作系统下工作。本章将简要介绍你可以找到的语言以及获取它们的途径。

我们不可能希望涵盖 Linux 上可用的每一种语言：新的移植和语言开发几乎每周都在发生。然而，我们已经列出了一些最受欢迎的语言，并以此为出发点。

### Ada

Ada 语言在军事应用中得到广泛使用，并在过去十年中获得了认可。随着该语言在国防相关应用程序程序员中日益流行，针对 Linux 出现几个 Ada 移植版本是必然的。Linux 上最流行的 Ada 版本是 GNAT（Gnu Ada Translator）软件包，该包由纽约大学开发并主要提供支持。有关 GNAT 项目或 GNAT 最新版本的信息，请发送电子邮件至 gnat-request@cs.nyu.edu。当前版本的 GNAT 可从多个 FTP 站点获取，并需要使用 GNU C 编译器在你的 Linux 系统上编译。

> **提示**
> 多个 FTP 站点镜像了 NYU GNAT 归档。你可以在 FTP 站点 tsx-11.mit.edu 的目录 `/pub/linux/packages/ada` 中找到最新版本的 GNAT。

GNAT 涵盖了 Ada83 和 Ada90 Ada 语言标准，并与一些商业 Ada 编译器兼容。

### COBOL

COBOL 已经存在了几十年，世界上编写的 COBOL 代码很可能比任何其他语言都多。有几个针对 Linux 的商业 COBOL 编译器移植版本可用，其中最著名的是来自 Acucobol 的 COBOL-85 移植版本（更多信息请见 http://www.acucobol.com）。迄今为止，没有公共领域的 COBOL 编译器版本可用于 Linux，尽管从 Linux FTP 站点可以获得几种 COBOL 工具。

### DSP

一个名为 ObjectProDSP 的数字信号处理（DSP）包可用于 Linux。ObjectProDSP 是一个基于 X 的对象化数字信号处理开发工具，对许多工程和科学应用非常有用。

> **提示**
> 多个 FTP 站点提供针对 Linux 的 ObjectProDSP。你可以在 FTP 站点 tsx-11.mit.edu 的目录 /pub/linux/packages/dsp 中找到几个版本。如果你使用 Web 浏览器进行 FTP 访问，请使用 URL ftp://tsx-11.mit.edu/pub/linux/packages/dsp。

ObjectProDSP 的作者可通过电子邮件 mtnmath@mtnmath.com 联系。

### Eiffel

Eiffel 是一种面向对象编程语言，具有很高的代码重用能力。自 Bertrand Meyer 在 20 世纪 80 年代后期开发以来，Eiffel 已建立了一支忠实的追随者群体。Eiffel 已进入公共领域，并由非营利国际 Eiffel 联盟（NICE）管理。作为面向对象语言，Eiffel 具有你预期中的所有特性，表现出色。

> **提示**
> Linux 版 Eiffel 可在多个 FTP 站点以及通过 Web http://www.cm.cf.ac.uk/Tower 找到。

### FORTRAN

FORTRAN（公式翻译器）是 60 年代和 70 年代的标准编程语言之一，特别是在科学与工程领域。在 Linux FTP 站点上有几个 FORTRAN77 版本的 FORTRAN 移植版本可用，FORTRAN90 的非商业发布移植版本也开始出现。

多个 FTP 站点提供 Linux 版 FORTRAN。你可以在 FTP 站点 tsx-11.mit.edu 的目录 `/pub/linux/packages/fortran` 中找到几个版本。那里也有几个 Linux FORTRAN 支持工具。

除了 FORTRAN 编译器外，还有几个已转换为在 Linux 下运行的支持工具。其中大多数可通过上述 FTP 站点获取，包括从 FORTRAN 到 C 的转换器。

toolpack 软件包对 FORTRAN 程序员很有用。它包含许多用于简化输出格式化和打印任务的实用工具。mpfun 软件包允许进行最高达 1600 万位精度的 FORTRAN 多精度计算（对大多数人来说绰绰有余！）。还有几个可用的工具，用于检查你的 FORTRAN 代码是否符合 FORTRAN77 和 FORTRAN90 标准以及可移植性。

### LISP

LISP 是典型的人工智能语言，于 1950 年代后期开发，用于研究人工智能领域。一个名为 clisp 的 LISP 编译器包含在大多数 Linux CD-ROM 中，并可以从提供 Linux 软件的所有标准 FTP 站点获取。

### Modula-3

Modula-3 语言是由 Digital Equipment Corporation 对流行的 Modula-2 语言（本身是 Pascal 的发展）进行开发的。Modula-3 是一种用于开发多处理器分布式应用程序的面向对象语言。Modula-3 基于 X，并使用了有吸引力的 GUI。

多个 FTP 站点提供 Linux 版 Modula-3。你可以在 FTP 站点 gatekeeper.dec.com 的目录 `/pub/DEC/Modula-3` 以及站点 ftp.vlsi.polytml.ca 的目录 `/pub/m3/binaries/LINUX/m3` 中找到几个版本。Modula-3 的 Web 主页是 http://www.research.digital.com/SRC/。

Modula-3 会不定期发布新版本，因此请检查上述目录中每个版本的子目录和 tar 文件。

### OGI 语音工具

顾名思义，OGI 语音工具是一种用于语音处理的语言，用于多种目的，包括语音分析和信号操纵。OGI 工具由口语理解中心开发。使用 OGI 语音工具，你可以构建口语单词的解析器和数据库，从而为 Linux 构建语音接口。OGI 语音工具在 Linux 下运行需要声卡。

> **提示**
> 多个 FTP 站点提供 Linux 版 OGI 语音工具。你可以在 FTP 站点 sunsite.unc.edu 的目录 /pub/Linux/apps/sound 或站点 tsx-11.mit.edu 的目录 /pub/Linux/packages/ogi 中找到最新版本。

OGI 语音工具（相当复杂）的文档位于 FTP 目录中。

### Scheme

Scheme 是一种与 LISP 相关的人工智能语言，但融入了一些 C 元素。Scheme 是一种灵活的编程语言，学习和使用起来出奇地容易。从 FTP 归档站点可获得 Scheme 的几个版本，以及转换为其他语言的转换工具。

### Scilab

Scilab 是一个数学软件包，旨在允许科学家和工程师进行矩阵操作、绘图和功能设计。Scilab 是一个公共领域软件包，旨在与昂贵的商业数学软件包竞争，尽管后者通常具有更好的功能和支持。Scilab 由法国的计算机科学与自动化研究所（INRIA）开发。

