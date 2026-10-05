

## 11.5 FTP客户端

![](img/cd7585e53abd949068548271c07fcdd8_170_0.png)

图 11–2 屏幕分为命令区域和输出区域

- 使用 TAB 键完成文件名和命令补全。
- 使用类似 less 或 more 的分页页器查看远程文件。
- 在上传或下载文件时支持通配符表达式。
- 支持 ftp: URL，例如，ftp://www.snerdwump.org/pub/wump-1.2.4.tgz。
- 批量操作。

## XFTP

XFTP 是一个基于 X-Motif 的 FTP 客户端。它支持许多方便的功能，例如选择一组文件进行上传或下载。它还可以在其他计算机之间移动文件（即这两台电脑都不需要运行 XFTP，尽管它们都需要运行某种形式的 ftppd）。

可以使用内置的弹出视图或用户指定的查看器（如 emacs、less 或 more）来查看本地和远程文件。此外，您还可以为各种图形格式指定要使用的程序。

最后，该界面允许大量的用户配置。

下一页的图 11-3 显示了 XFTP 的截图。

![](img/cd7585e53abd949068548271c07fcdd8_171_0.png)

图 11–3 XFTP

## 11.6 总结

FTP 是一个非常有用的服务，是少数没有被 Web取代的服务。（像 gopher、archie 和 wais 等东西现在几乎死掉了，被 Web 的对应品所取代。）

你们最坏的情况下只需要设置一个匿名 FTP 服务器，并可能需要确保用户可以通过 FTP 访问他们的账户。如果您的机器最初就配置为处理 FTP（大多数 Linux 都是如此），这可以轻而易举。您可能需要创建几个文件和目录。

设置起来复杂的是 FTP 专用账户和虚拟 FTP 客户端。希望我们提供的信息足够让您开始。

- 匿名 FTP 位于 /home/ftp
- FTP 客户端为 FTP 提供了更好的界面

## 12 Linux 应用

Linux 不仅仅是一个服务器——桌面应用程序正在日益增加。

本章对 Linux 流行的应用程序进行介绍。这些应用程序涵盖了从集成办公套件到符号数学程序，再到运行其他操作系统模拟器。

## 12.1 办公产品、文字处理器和编辑器

这一类别包括办公套件、独立的文字处理器和电子表格软件、编辑器以及出版工具。

### Applixware

Applixware 由 Applix, Inc. (http://www.applicix.com/) 开发，可能是 Linux 上可用的最完整且集成最紧密的办公套件。它是

Staroffice 是另一个办公套件，但遗憾的是它需要 Caldera OpenLinux，不能在其他发行版上运行。它由 Star Division (http://www.stardivision.com/) 开发，是一个功能全面的办公效率套件，包含了 StarWord（文字处理器）、StarCalc（电子表格）、StarDraw（图形和演示包）、StarImage（图像处理）、StarGallery（多媒体工具）和 StarChart（绘图和图表制作工具）。

### WordPerfect

Corel 的 WordPerfect 7（及之前的版本）已由 Software Development Corporations (http://www.sdcorp.com/) 移植到 Linux，WordPerfect 8 应该很快就会移植。WordPerfect 可能是 Linux 上功能最丰富的文字处理器。

使用 WordPerfect 的缺点是 Corel 的其他办公产品没有随之一起移植，因此它没有一个良好的、集成良好的办公套件可以交互。尽管如此，Corel 本身正在将其整个办公套件移植到 Java。这门课程将允许任何带有 Java 虚拟机的机器运行它。有关 Java 版 Corel Office 的更多信息，请参见 http://www.corel.com/javastrast/index.htm。

图 12-3 是 WordPerfect 7 30 天试用版的截图。

![](img/cd7585e53abd949068548271c07fcdd8_177_0.png)

图 12–3 - WordPerfect 30 天试用版

Network Extensible Spreadsheet（网络扩展电子表格）由 X Engineering Software Systems (http://www.xess.com/) 开发。NExS 是一个功能全面的电子表格，具有近 250 个内置函数，表格大小支持 32,767 行、4,096 列，支持导入和导出制表符数据或其他格式（见 12–5）。

![](img/cd7585e53abd949068548271c07fcdd8_179_0.png)

## TeX/LaTeX

### 简介

Linux 操作系统开始受到关注，这将使其普及程度超过过去几年的水平。Web 服务器、互联网服务器、文件和打印机服务器的爆炸式增长和需求，正引导越来越多的管理员去查看与其它解决方案相比成本较低的类 Unix 系统。今天约有百分之十的 Web 以 Linux 为基础。Red Hat 发行版 Linux 在 1996 年被 InfoWorld 评为“年度产品”，并经常有贡献者发布关于 Linux 最佳实践公告和文章。

技术期刊和杂志正充斥着与 Linux 开发、管理、发行和使用相关的广告和文章。《SysAdmin》杂志最近还专门了一期 Linux 专题。

系统管理员对一本深入浅出的书籍的需求是显而易见的。

### 作者

Mark P. Komarinski 自 1989 年起使用 Unix，从 1992 年起使用 Linux。他曾是《Linux Journal》的作家，《The Linux Sampler》的特稿作家，并且是《Linux for Users and System Administrators》的作者。他目前在马萨诸塞东部的 Aurora Technologies 工作，利用 Linux 技能维护 Aurora 的网络。他每年都是 Linux 大会的演讲者。

图 12–2 文档可以在应用程序之间共享，并由不同的程序插入

TeX 是原始的排版程序。它不是文字处理器，也没有编辑环境。TeX 文件可以使用任何文本编辑器创建。因为 TeX 源是纯文本，而且 TeX 已经移植到几乎每个平台，用它创建的文档具有迁移性。

当处理 TeX 或相关文件时，输出会被 DVI（设备无关）文件。DVI 是一种格式

- LaTeX——目前最常见的 TeX 扩展。它实际上是一组宏，允许与 TeX 进行更高层次的交互。它为文章、书籍和信提供了特定的模式。

- BibTeX——参考文献和引用系统。它还允许您从较大的、可能共享的列表中为特定文档构建参考文献。

- SliTex——专门为制作幻灯片或大字打印文档设计。

- MakeIndex——一个为 TeX 文档创建索引的工具。它支持多达三级的索引。

- HyperTex——TeX 的一个扩展，允许您创建带有超链接的文档。源将超链接信息传递给 .avi 文件，该文件随后可以转换为 Acrobat 格式。（Acrobat 本质上是压缩 Postscript 的叠加层，支持超链接。）

- LaTeX2HTML——一个将 LaTeX 源代码转换为 HTML 文件的工具。它会创建一个链接目录，将数学公式转换为嵌入 GIF，并正确处理引用和脚注。

TeX 有综合 TeX 存档网络（CTAN）的支持。可以通过 http://www.tex.ac.uk/ 访问 CTAN，在那里你可以找到 LaTeX 和其他 TeX 扩展的信息。

Xemacs

Xemacs（见图 12–6）是适用于 GNU emacs 的增强版。Xemacs 是一个功能极其强大的编辑器。它拥有数十种文件的编辑模式，包括 HTML、C、Perl、Python、C++、Makefile、TeX、LaTeX 和 FORTRAN，仅列举几个。

此外，Xemacs 支持语音合成和语音控制。结合 Usenet 新闻阅读器、Web 浏览器和邮件读取器，使其成为视障用户的显而选择。

Xemacs 支持在多帧中编辑多个缓冲区。帧也可以垂直或水平分割成子窗口。

Xemacs 还可以以屏幕模式运行。在这种情况下，你将失去一些功能，主要与帧和下拉菜单有关。

