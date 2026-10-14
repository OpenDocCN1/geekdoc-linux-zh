
PL 的目的是尽可能紧密地模仿 GNUstep/OPENSTEP 中使用的属性列表的行为（它们由 `NSString`、`NSData`、`NSArray` 和 `NSDictionary` 类形成）并保持适当的兼容性。PL 使使用配置文件或首选项文件的程序能够使这些文件与 GNUstep/OPENSTEP 的用户默认值处理机制兼容，而无需使用 Objective-C 或 GNUstep/OPENSTEP 本身。

## libc —（版本 5.3.12，5,259K） [B]

较旧的 Linux 系统（包括 Red Hat Linux 2.0 至 4.2 之间的所有版本）基于 `libc` 版本 5。`libc` 软件包包含 `libc5` 库和其他基于 `libc5` 的库。安装这些库后，需要它们的旧应用程序将能够在你的 `glibc`（`libc` 版本 6）上运行

## 附录 C：软件包列表

基于系统。应安装 `libc6` 软件包，以便你能运行需要 `libc` 版本 5 的旧应用程序。

## libelf —（版本 0.6.4，76K）

`libelf` 软件包包含一个用于访问 ELF 对象文件的库。`Libelf` 允许你访问 ELF 对象文件格式的内部结构，以便查看 ELF 文件的不同部分。如果需要访问 ELF 对象文件内部结构，请安装 `Libelf`。

## libghttp —（版本 1.0.2，85K）

[W][S]

用于发出 HTTP 1.1 请求的库。

## libgr —（版本 2.0.13，235K）

[W][S]

`libgr` 软件包包含一个函数库，支持处理各种图形文件格式的程序，包括 `.pbm`（便携式位图）、`.pgm`（便携式灰度图）、`.pnm`（便携式任意图）、`.ppm`（便携式像素图）等。

## libgtop —（版本 1.0.1，431K）

[W]

一个获取有关运行系统信息的库，例如 CPU 和内存使用情况、活动进程等。在 Linux 系统上，此信息直接取自 `/proc` 文件系统，而在其他系统上则使用服务器从 `/dev/kmem` 等读取该信息。

## libgtop-examples —（版本 1.0.1，937K）

这些是 `LibGTop` 的示例，`LibGTop` 是一个检索有关系统信息的库，例如 CPU 和内存使用情况。

## libjpeg —（版本 6b，239K）

[W][S]

`libjpeg` 软件包包含用于操作 JPEG 图像的函数库，以及用于访问 `libjpeg` 函数的简单客户端程序。`Libjpeg` 客户端程序包括 `cjpeg`、`djpeg`、`jpegtran`、`rdjpgcom` 和 `wrjpgcom`。`Cjpeg` 将图像文件压缩为 JPEG 格式。`Djpeg` 将 JPEG 文件解压缩为常规图像文件。`Jpegtran` 可对 JPEG 文件执行各种有用转换。`Rdjpgcom` 显示 JPEG 文件中包含的任何文本注释。`Wrjpgcom` 将文本注释插入 JPEG 文件。

## libjpeg6a — (Version 6a, 137K)

该软件包是一个用于处理 JPEG 图像的函数库，以及用于操作 JPEG 图像的简单客户端。此版本仅包含一个库，用于保持与 Red Hat Linux 早期版本向后兼容。

## libpng — (Version 1.0.3, 270K)

[W][S]

`libpng` 软件包包含用于创建和操作 PNG（便携式网络图形）图像格式文件的函数库。PNG 是一种与 GIF 格式类似的位图图形格式。PNG 是为取代 GIF 格式而创建的，因为 GIF 使用受专利保护的数据压缩算法。如果您需要操作 PNG 格式图像文件，应安装 `libpng`。

## libstdc++ — (Version 2.9.0, 3,421K)

[B]

EGCS 是一个自由软件项目，旨在使用开放的开发环境推动 GNU 编译器的发展。`egcs` 软件包包含 `egcs` 编译器，该编译器旨在集成高性能和稳定开发环境所需的所有优化和功能。EGCS 包含运行 C++ 应用程序所需的共享库，以及额外的 GNU 工具。如果您想使用实验性的 GNU 编译器，请安装 `egcs`。

## libtermcap — (Version 2.0.8, 58K)

[B]

`libtermcap` 软件包包含访问 termcap 数据库所需的基本系统库。`termcap` 库支持轻松访问 termcap 数据库，以便程序能够以终端无关的方式输出基于字符的显示。

## libtiff — (Version 3.4, 568K)

[W][S]

`libtiff` 软件包包含用于操作 TIFF（标记图像文件格式）图像格式文件的函数库。TIFF 是一种广泛使用的位图图像文件格式。TIFF 文件通常以 `.tif` 扩展名结尾，并且通常相当大。如果您需要操作 TIFF 格式图像文件，应安装 `libtiff` 软件包。

## libungif — (Version 4.1.0, 80K)

[W][S]

`libungif` 软件包包含用于加载和保存 GIF 格式图像文件的共享函数库。`libungif` 库可以加载任何 GIF 文件，但它仅以未压缩格式保存 GIF（即，它不会使用用于保存“普通”压缩 GIF 文件的受专利保护的 LZW 压缩）。如果您需要操作 GIF 文件，请安装 `libungif` 软件包。您还应安装 `libungif-progs` 软件包。

## libxml — (Version 1.0.0, 154K)

[W][S]

该库允许您操作 XML 文件。

## ncurses — (Version 4.2, 2,627K)

[B]

`curses` 库例程是一种终端无关的方法，可在合理优化的情况下更新字符屏幕。`ncurses`（新 `curses`）库是已停产的 4.4BSD 经典 `curses` 库的自由分发替代品。

## ncurses3 — (Version 1.9.9e, 330K)

`curses` 库例程是一种终端无关的方法，可在合理优化的情况下更新字符屏幕。`ncurses`（新 `curses`）库是已停产的 4.4BSD 经典 `curses` 库的自由分发替代品。

## newt — (Version 0.40, 128K)

[B]

`Newt` 是一个用于彩色文本模式、基于部件的用户界面的编程库。`Newt` 可用于向文本模式用户界面添加堆叠窗口、输入部件、复选框、单选按钮、标签、纯文本字段、滚动条等。该软件包还包含使用 `newt` 构建的程序所需的共享库，以及一个名为 `whiptail` 的 `/usr/bin/dialog` 替代品。`Newt` 基于 `slang` 库。

## p2c — (Version 1.22, 723K)

`P2c` 是一个将 Pascal 程序翻译成 C 语言的系统。`P2c` 接受某些 Pascal 方言的输入源文件：HP Pascal、Turbo/UCSD Pascal、DEC VAX Pascal、Oregon Software Pascal/2、Macintosh Programmer’s Workshop Pascal 和 Sun/Berkeley Pascal。`P2c` 输出一组 `.c` 和 `.h` 文件，这些文件构成与原始 Pascal 程序等效的 C 程序。然后可以使用标准 C 编译器（如 `gcc`）编译该 C 程序。如果您需要将 Pascal 代码翻译成 C 代码的程序，请安装 `p2c` 软件包。

## pythonlib — (Version 1.22, 236K)

[W][S]

`pythonlib` 包包含各种 Red Hat Linux 程序使用的 Python 代码。`Pythonlib` 包含多字段列表框和具有非标准键绑定的输入部件所需的代码等。

## qt — (Version 1.44, 2,093K)

`Qt` 是一个 GUI 软件工具包。`Qt` 简化了为 X Windows 编写和维护 GUI（图形用户界面）应用程序的任务。`Qt` 用 C++ 编写，并且完全面向对象。它拥有创建专业 GUI 应用程序所需的一切。而且它能让你快速创建它们。`Qt` 是一个跨平台工具包。在使用 `Qt` 开发软件时，你可以在 X Window 系统（Unix/X11）或 Microsoft Windows NT 和 Windows 95/98 上运行它。只需在你想要的平台上重新编译源代码即可。该软件包包含运行 `Qt` 应用程序所需的共享库，以及 `Qt` 的 README 文件。

## readline — (Version 2.2.1, 262K)

[B]

`readline` 库从终端读取一行并返回它，允许用户使用标准的 emacs 编辑键编辑该行。`readline` 库允许程序员为用户提供易于使用且更直观的界面。如果你想开发使用 `readline` 库的程序，你还需要安装 `readline-devel` 软件包。

## slang — (Version 1.2.2, 250K)

[B]

S-Lang 是一种解释型语言和编程库。S-Lang 语言的设计使其可以轻松嵌入到程序中，为程序提供强大的扩展语言。本软件包提供的 S-Lang 库提供了 S-Lang 扩展语言。S-Lang 的语法类似于 C，这使得在需要时将 S-Lang 过程重新编码为 C 变得容易。

## svgalib — (Version 1.3.1, 489K)

[W]
