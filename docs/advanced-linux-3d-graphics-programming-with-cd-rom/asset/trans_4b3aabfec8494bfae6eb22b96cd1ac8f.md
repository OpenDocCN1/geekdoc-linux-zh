
## 将代码移植到 Microsoft Windows

l3d 代码经过设计，可以轻松地移植到其他操作系统，例如 Microsoft Windows。除少数例外情况外，本书中的示例程序都可以在 Windows 下编译和运行。然而，对 Windows 的支持并非 l3d 的主要关注点，因为它旨在说明 Linux 下的图形编程，而且我在主要计算机上既未安装也未使用过任何微软产品。在（未必真实的）假设微软和 Windows 继续保持一定的短期市场相关性的前提下，你或许也会发现将程序同时发布在 Microsoft Windows 下是有趣的。

要在 Microsoft Windows 下编译代码，你可以使用 Cygnus GCC 编译器，它包含在 CD-ROM 的 *software/ms-win* 目录中。这是一个免费的 C++ 编译器和调试器，运行在 Microsoft Windows 下，可用于编译 l3d 代码。请务必阅读并安装随 Cygnus GCC 编译器提供的 OpenGL 头文件和库。OpenGL 文件位于 CD-ROM 上的归档文件 *opengl-1.2.1-1.tar.gz* 中。

文件 *makecyg.bat* 是一个批处理文件，它使用 Cygnus GCC 编译器为 Microsoft Windows 编译所有示例。以下是 Windows 特定的源代码文件，你应该将其作为理解移植代码的起点：

- *fwin.cc, fwin.h*：用于创建 Microsoft Windows 工厂类的工厂类
- *sc_mswin.h, sc_mswin.cc*：使用设备无关位图（DIB）节创建 2D 输出窗口的屏幕类
- *dis_mswin.h, dis_mswin.cc*：用于在 Microsoft Windows 下处理事件的调度类
- *sc_wogl.h, sc_wogl.cc, sc_wzogl.h, sc_wzogl.cc*：在 Windows 下使用 OpenGL 创建输出窗口的屏幕类

用于 Windows 对象文件和可执行文件的二进制目录是 `$13D/binaries/cygwin`。

移植过程通过复制 Linux 目录结构并按需编辑 Makefile 来完成。

默认情况下，Windows 代码使用软件渲染器和基于 OpenGL 的渲染器进行编译。这意味着你的系统上应安装 OpenGL 和 GLUT 库。OpenGL 库通常作为操作系统的标准配置提供，并且也作为专用驱动程序随任何现代 3D 显卡一起分发。GLUT 库（文件 `GLUT32.DLL`）包含在 CD-ROM 上随 Cygnus GCC 编译器提供的文件 `opengl-1.2.1-1.tar.gz` 中。如果你的 OpenGL 驱动程序支持硬件加速，那么 l3d 程序在 Microsoft Windows 下也将支持硬件加速。在极不可能的情况下，如果你的系统上完全没有安装 OpenGL 库，你可以更改 Makefile，以在没有 OpenGL 特定文件的情况下进行编译和链接；换句话说，在 Windows 下使用纯软件渲染来编译 l3d 也是可能的。

插件目前尚不能与代码的 Microsoft Windows 版本配合使用。在使用 Cygnus GCC 时，使用 Linux 风格的插件似乎存在一些困难。因此，使用插件的程序目前在 Windows 下无法工作。当前，代码依赖于对 Linux `dlopen` 系统调用的模拟来加载库。然而，Windows 拥有自己的动态库加载机制 `LoadLibrary`，可以用来替代。

> **注意** 使用脚本语言来实现动态行为，而不是使用插件，可以避免特定于系统的动态库约定带来的问题，但运行时性能可能会较慢。

务必查看本书的网站 `http://www.linux3dgraphicsprogramming.org`，以了解 Microsoft Windows 版 l3d 代码的状态并下载最新版本。或者，你可以选择完全放弃 Microsoft Windows，从长远来看，这可能是一个更好的解决方案。

## 用于制作本书的工具

应我的技术编辑 Kevin Seghetti 的建议，我现在将简要介绍用于制作本书的工具。

本书完全使用 Linux 工具编写。Linux 发行版是 SuSE 6.3，但由于 Debian 对自由软件社区的明确承诺，我目前正致力于迁移到 Debian。

文本是使用 Corel WordPerfect 8 for Linux 制作的。我本希望使用 LyX 来编写文本，LyX 是 LaTeX 文档准备系统的前端，常用于学术界。然而，在撰写本文时，没有可靠的方法将 LyX/LaTeX 文件转换为我的出版商所需的专有文字处理格式。当然，有一些工具可以完成大部分转换工作（例如 `latex2html`），但在尝试了大约五个不同的软件包后，我发现没有任何解决方案能够保留字体、列表、缩进、标题等。因此我使用了 WordPerfect，它可以以出版商所需的格式精确导出文件。

程序列表与文本分开存储，作为子文档。一个 Perl 脚本从所有源代码文件中删除多余的注释，并将 ASCII 源代码文件转换为 RTF 文件。然后，RTF 文件链接到主文档中。文本中的代码片段由代码中特殊格式的注释界定；另一个 Perl 脚本提取这些区域，并再次创建可以绑定到主文档的 RTF 文件。这些脚本包含在 l3d 发行版中，文件名为 `make_clean.sh`、`no_double_space.pl` 和 `snippets.pl`。每当需要更新源代码时，我只需再次运行我的脚本，更新的源代码就会自动重新绑定到主文档中。

2D 图形是使用 Xfig 生成的，Xfig 是一个非常灵活的基于对象（而非位图）的绘图程序。类图是使用概念建模工具包 TCM 手动生成的。其他有前途的类图工具包括 Argo/UML（我没有使用它，因为它专注于 Java）和 doxygen（它可以从未加注释的 C++ 代码自动生成出色的文档，我可能会在未来使用它）。3D 图形是使用 Blender 生成的。CD-ROM 上的注释也是使用 Blender 创建的。图形的后期处理工作是使用 GIMP 完成的。

方程是使用 LyX 生成的，LyX 是一个几乎所见即所得的 LaTeX 环境。我创建了一个 LyX 文件，包含特定章节的所有方程。接下来，我将 LyX 文件导出为 LaTeX 文件。然后，我使用 latex2html 将 LaTeX 代码转换为 HTML；latex2html 有一个奇妙的功能，可以自动将 LaTeX 方程转换为位图图像文件。这些位图图像文件随后被重命名为 CD-ROM 上的 `eqnxx-xx` 文件。

为了管理每个章节大量的图形和方程，我再次编写了一个 Perl 脚本，该脚本读取一个包含该章节所有图形列表（按顺序）的输入文件。这些图形随后被转换为出版商所需的格式，并被分配顺序文件名。这样，我就可以单独处理图形，使用不同的文件格式，而不必担心它们的准确顺序。如果添加或删除了图形，我只需对图形列表进行相应的更改，所有这些图形在脚本的下次运行期间都会获得正确的编号。脚本内部使用 PBM 实用工具将各种图像文件格式转换为一种通用格式。

## 资源

以下是一些印刷和在线资源的列表，它们可能有助于你继续探索——并希望推动 Linux 3D 图形的现状。下一节是本书中引用的具体文献的综合列表，但本节旨在向你介绍一些更具通用性的资源。

