
# 将代码迁移到 Microsoft Windows

`l3d` 代码的设计初衷已经考虑了可以轻松移植到其他操作系统，例如 Microsoft Windows。除少数外，书中的示例程序都可以在 Windows 下编译并运行。然而，对 Windows 的支持并不是 `l3d` 的首要考虑问题，因为在我的电脑上既没有安装过、也不需要任何微软产品。在（不一定）假设微软和 Windows 将继续保持某些短期市场相关性的情况下，将你的程序也迁移到 Microsoft Windows 可能是一件趣事。

要在 Microsoft Windows 下编译代码，你可以使用 Cygnus GCC 编译器，该编译器包含在 CD-ROM 的 `book/software/ms-win` 目录中。这是一个免费的 C++ 编译器和调试器，运行在 Microsoft Windows 环境下，并可用于编译 `l3d` 代码。请务必使用 Cygnus GCC 编译器阅读并安装 OpenGL 头文件和库。OpenGL 文件位于 CD-ROM 上的 `opengl1.2.1-tar.gz` 压缩文件中。

`makecy.bat` 文件是一个批处理文件，它使用 Cygnus GCC 编译器为 Microsoft Windows 编译所有示例。以下是 Windows 特有的源文件，你应该将其作为理解迁移代码的起点：

- `fwin.cc`, `fwin.h`: 用于创建 Microsoft Windows 工厂的工厂类。
- `sc_mswin.h`, `sc_mswin.cc`: 使用设备无关位图 (DIB) 节创建 2D 输出窗口的屏幕类。
- `dis_mswin.h`, `dis_mswin.cc`: 在 Microsoft Windows 下进行事件处理的分发器类。
- `sc_wogl.h`, `sc_wogl.cc`, `sc_wogl.h`, `sc_wogl.cc`: 在 Windows 下使用 OpenGL 创建输出窗口的屏幕类。

目录对象和可执行文件的二进制文件位于 `$L3D/binaries/cygwin`。迁移是通过复制 Linux 目录结构并根据需要修改 `Makefiles` 完成的。

默认情况下，代码同时使用软件渲染器和基于 OpenGL 的渲染器进行编译。这意味着你的系统中应该安装 OpenGL 和 GLUT 库。OpenGL 库通常随操作系统标准提供，并作为任何现代 3D 显卡的专用驱动程序发布。GLUT 库（文件 `GLUT32.DLL`）包含在 CD-ROM 上 Cygnus GCC 编译器的 `opengl-1.2.1-1.tar.gz` 文件中。如果你的 OpenGL 驱动支持硬件加速，那么 `l3d` 程序在 Microsoft Windows 下也将通过硬件加速运行。如果在极少数情况下你的系统中完全没有 OpenGL 库，你可以修改 `Makefiles` 在不包含 OpenGL 特定文件的情况下编译和链接；换句话说，在 Windows 下使用纯软件渲染编译 `l3d` 也是可能的。

插件在 Microsoft Windows 版的代码中不起作用。使用 Cygnus GCC 使用 Linux 风格插件似乎存在一些困难。因此，目前任何使用插件的程序无法在 Windows 下运行。目前代码依赖于 Linux `dlopen` 系统调用的仿真来加载库。可以使用 `LoadLibrary`。

> 注意：使用脚本语言来实现动态行为代替插件，可以避免特定系统动态库内容的问题，但运行时性能可能会较慢。

请务必检查本书的网站 `http://www.linux3programming.org` 以查看 Microsoft Windows `l3d` 代码的状态并下载最新版本。或者，你也可以完全放弃 Microsoft Windows，从长远来看，这可能是更好的解决方案。

# 准备本书时使用的工具

在我的技术编辑 Kevin Seghetti 的建议下，我将简要介绍准备本书时使用的工具。

本书完全使用 Linux 工具编写。所使用的 Linux 发行版是 SuSE 6.3，尽管我目前正在迁移到 Debian，因为 Debian 对自由软件社区有明确的承诺。

正文是使用 Linux 版的 Corel WordPerfect8 准备的。我本希望使用 `LyX` 编写文本，`LyX` 是 `LaTeX` 准备系统的前端，通常在学术界使用。在编写本文时，还没有可靠的方法可以将 `LyX`/`LaTeX` 文件转换为我出版商所需的私有文字处理格式。在这里，有几种工具可以完成大部分转换（例如 `latex2html`），但在尝试了五个不同的包后，我没有找到任何能保留字体、列表、缩进等内容的解决方案。因此，我使用了 WordPerfect，它可以导出出版商所需的切切格式。

程序列表作为子文档单独存储。一个 Perl 脚本删除了所有源文件中的多余注释，而文本中的 ASCII 源代码由代码中特种格式的注释界定；另一个 Perl 脚本提取这些区域，并再次创建了可以合并到主文档的 RTF 文件。这些脚本位于 `l3d` 分发包中，分别为 `make_clean.sh`、`no_double_space.pl` 和 `snippets.pl`。每当我需要更新源代码时，只需再次运行我的脚本，更新后的源代码就会自动重新合并到主文档中。

2D 图形是用 `Xfig` 生成的，这是一种非常灵活的基于对象的程序（而非位图绘制程序）。类图是由 `TCM`（概念建模工具包）手动生成的。其他有前景的工具包括 `Argo/UML`（因为它专注于 Java，我没有使用）和 `doxygen`（它可以从无注释的 C++ 代码生成生成文档，我可能会使用）。3D 图形是用 `Blender` 生成的。CD-ROM 动画也是使用 `Blender` 创建的。图形的后期处理是用 `GIMP` 完成的。

公式是使用 `LyX` 生成的，它是 `LaTeX` 的所见即所得环境。我为每个章节创建一个包含所有公式的 `LyX` 文件。接下来，将 `LyX` 导出为 `LaTeX` 文件。然后，我使用 `latex2html` 将 `LaTeX` 代码转换为 HTML；`latex2html` 是将 `LaTeX` 公式转换为位图的工具。这些图像文件随后被重命名为 CD-ROM 上的 `eqn-xx` 文件。为了管理每个章节大量的图形和公式，我再次编写了一个 Perl 脚本来读取包含图形列表的文件。这些图形被转换为出版商所需的格式并分配了顺序文件名。通过这种方式，我可以单独处理不同格式的图形，而不必担心它们的顺序。如果添加或删除了图形，我只需对列表进行相应修改，图形在下次运行时就会获得正确的编号。脚本使用了 PBM 工具将各种文件格式转换为一种通用格式。

# 资源

以下列出的一些印刷物和在线资源，在你继续探索并可能推进 3D 图形领域时可能有所帮助。下一部分是书中引用的参考文献详细列表。

- `Blender vl.5 Manual` 作者 Roosendaal。这是使用 `Blender` 的权威指南。参见 `http://www.blender.nl`。
- `Computer Graphics, Principles and Practice` 作者 James Foley, Andres van Dam, Steven Fein 和 John Huges。该书被许多人视为该领域的经典，涵盖了与 2D 和 3D 图形程序员相关的极其广泛的主题。几乎每个主题都涉及了，尽管简洁。这本书带有某种数学倾向。
- `The C++ Programming Language` 作者 Bjarne Stroustrup。这当然是 C++ 语言的权威参考。
- `Das Buch` 作者 Karsten Wassmann。这本书提供了使用 `Blender` 的实用介绍和指南，包含几个实操教程。（德语）
- `Data Structures and Program Design` 作者 Robert Kruse。这本关于数据结构的介绍介绍了计算机科学中许多基础结构，这些结构对于所有类型的程序（包括 3D 程序）都至关重要。

- 《设计模式：可重用面向对象软件的元素》，由 Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissides 著。这部具有里程碑意义的文件首次引入了“设计模式”的概念，提供了一份可重用模式目录，并鼓励在面向对象开发中使用这种技术。

- 《数字角色动画 2，第1卷：核心技术》，由 George Masai 著。这本独立书籍通过大量的练习和插图说明了角色动画的基础知识，帮助你理解并掌握其中的困难点。

- 《右脑画画》，由 Betty Edwards 著。这本书探讨了如何培养视觉技能以成为一名出色的 2D 艺术家。虽然它没有直接涉及计算机图形，但你从书中中学到的视觉技能对所有类型的视觉表达（包括 3D 建模）都非常有效。

- 《吉他手册》，由 Ralph Denyer 著。我发现优秀的程序员通常也是优秀的艺术家——无论是在音乐、视觉上还是其他方面。如果你在编写交互式 3D 程序（如游戏），你还需要编写音乐来配合这些程序。这本书虽然侧重于吉他，但对音乐理论也有很好的讲解。

- 《绘画的钥匙》，由 Bert Dodson 著。这本书也没有涉及计算机图形，但为创作有效的 2D 艺术提供了许多实用的技巧或“钥匙”。

- 《3D 看起来更好看》，由 Andrew Reese 著。这本侧向实践的书籍解释了 3D 图像的基本原理，并阐述了用于创建有效演示效果的 3D 图形技术。

- 《面向对象软件构建》，由 Bertrand Meyer 著。这本书是对面向对象性及其如何提高软件质量的全面论述。书中非常易读，同时也对面向对象究竟是什么、它与其他软件方法论以及整个科学研究领域的关系提供了严谨的论述。尽管许多文献试图让面向对象看起来很简单，但这本书并不回避展示软件构建中真实的、微妙的、现实世界中的困难，以及面向对象是如何直面地解决这些问题的。

- 《OpenGL 编程指南》，由 Mason Woo、Jackie Neider 和 Tom Davis 著。这是使用 OpenGL 编程的权威指南。

- 《实时渲染》，由 Tomas Meller 和 Eric Haines 著。这本书包含了实时渲染高质量图形所需的大量算法和概念。目前（2001年3月）它是该领域最先进的书籍之一，也是最实用的当代技术的良好汇集。

- 《大学物理》，由 Francis W. Sears、Mark W. Zemansky 和 Hugh D. Young 著。这本本科级教材为物理领域提供了实用的介绍，其中一些可以应用于计算机仿真。

- 《X Window 系统：使用 Xt 进行编程与应用》，由 Douglas Young 和 John Pew 著。这本书介绍了如何编程 X Window 系统。

- `http://mesa3d.sourceforge.net`。`Mesa` 主页提供了新闻和库的最新版本，该库与 OpenGL 有效兼容。
