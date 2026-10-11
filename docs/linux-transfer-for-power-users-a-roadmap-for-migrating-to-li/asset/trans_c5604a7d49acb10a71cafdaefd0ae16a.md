

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_212_0.png)

**图 6.** 在你选择相应的插件后，编辑菜单中的插入选项才会显示出来。

Gedit 实际上远不止一个简单的记事工具，它拥有众多配置选项，可针对 Java、LaTeX、HTML、XML 和 Perl 等格式进行优化，但相关内容超出了本书的讨论范围。

你会发现，尽管图 1 中“打开方式”菜单的选项列表中有九个编辑器，但并非所有编辑器都能通过主菜单访问。如果你想使用其他编辑器，你需要做几件事，将其作为图标显示在桌面或面板上，以便可用。

首先，你需要知道运行该编辑器的命令，这可能需要进行一些深入挖掘。通常，命令就是编辑器的名称，例如 "gedit" 或 "kate"。然后，你需要找到程序本身的位置（即具有该名称的文件）。它通常位于 /usr/bin 目录下，如果不是，第 14 章“幕后机制”中有关于如何查找文件的说明。最后，只需按照第 6 章“文件、目录结构和文件管理器”中的描述，在你的桌面或面板上创建一个图标即可。

## OpenOffice.org

直到大约两年前，阻碍 Linux 被考虑作为桌面操作系统的一个主要障碍可能是缺乏 Microsoft Office 的替代品。随着当时 OpenOffice.org 1.0 的引入，这一障碍被消除了。

OpenOffice.org（或简称“OOo”）已迅速成为全世界标准的开源办公套件（我这样说并非因为我们自己也出版了好几本 OOO 的书！）。它是每个主流 Linux 发行版的一部分，并得到 Sun Microsystems 的支持，该公司资助了 OOO 的前身 StarOffice，并仍提供大量的编程支持。

OOO 套件由几个主要应用程序组成，包括文字处理器（Writer）、电子表格（Calc）和演示文稿管理器（Impress）。此外，OOO 还有绘图包（Draw）、公式编辑器（Math），以及功能极其强大的宏编辑器和数据库访问功能。由于各平台上都有许多优秀的电子邮件客户端，因此 Ooo 不包含自己的电子邮件客户端。

对于文本编辑器而言，仅凭本章无法彻底介绍 Ooo。事实上，有许多书籍专门介绍 Ooo。Solweig Haugland 的 1040 页著作 *OpenOffice.org 资源指南*（Prentice-Hall 出版）是使用 OpenOffice.org 的最终详尽资源，而 Tamar Granor 的 *OooSwitch：关于从 Microsoft Office 切换到 OpenOffice.org 的 501 件事*（Hentzenwerke Publishing 出版）则从经验丰富的 Office 用户视角详细介绍了 Ooo。

不过，我可以给你做一次简要介绍，并指出一些亮点。使用 Ooo 有几个关键优势，你需要立即了解。

首先，Ooo 是完全跨平台的。这意味着真正的跨平台——它适用于 Windows、Linux 和 Macintosh——就像 Microsoft 使用“跨平台”一词指代 Windows ME 和 Windows XP 那样。由于 Ooo 是跨平台的，你可以在 Linux 机器上以及 Windows 或 Macintosh 上使用它，并且软件将读写相同的数据文件。当你的组织中有多种操作系统，或者家中和工作场所使用不同的操作系统时，这是一个非常出色的功能。

第二个关键特性恰恰就是——数据文件。Ooo 可以以两种不同的格式保存文件——其自身原生的、有公开文档说明的文件格式，以及专有的 Microsoft Office 格式。并且这些文件格式也可以跨平台交换。这意味着你拥有极大的灵活性。

例如，你可以在 Linux 机器上使用 OpenOffice.org Writer 编写文档，以 OpenOffice.org 的 .sxw 文件格式保存该文件，然后使用 Windows 或 Macintosh 计算机上 OpenOffice.org 的人可以打开并编辑该文件。此外，由于 .sxw 文件格式有完善的文档说明，其他应用程序也可以打开并可靠地处理这些文档。

同样适用于 OpenOffice.org 的其他文件格式——电子表格（.sxc）、演示文稿（.sxi）和绘图（.sxd）。

OpenOffice.org 还可以读取和写入以 Microsoft 专有文件格式保存的文件，因此 OpenOffice.org 用户可以与使用 Microsoft Office 的人交换文件。例如，你可以在 Linux 或 Windows 计算机上使用 OpenOffice.org Impress 创建演示文稿，然后使用 Microsoft PowerPoint（当然是在 Windows 计算机上）的人可以打开并编辑该文件。

在 Hentzenwerke Publishing，我们依赖这两种能力。作者使用其选择的工具和平台撰写原始草稿——无论是 Microsoft Word 还是 OpenOffice.org，无论是 Windows 还是 Linux。章节随后会在技术编辑过程中来回流转，技术编辑使用他们最熟悉的工具和平台。同样的过程也用于校对和排版；我们的大多数校对人员和排版人员使用 OpenOffice.org（在任一平台上），但偶尔会有自由撰稿人使用 Microsoft Word。

使用 OpenOffice.org 的第三个好处是，你可以直接从 Writer 文档、Calc 电子表格或 Impress 演示文稿生成 PDF。从 1.1 版本开始，Ooo 的功能工具栏上有一个“导出为 PDF”按钮，用于生成 PDF 文件。这些文件的质量足够好，我们 Hentzenwerke Publishing 直接生成 PDF 并以电子方式发送给我们的图书印刷商，并且在印刷书籍之前不需要任何手动预印工作。

一个类似的功能是将 Impress 演示文稿导出为 Macromedia Flash (.swf) 文件的能力，然后你可以在浏览器中运行这些文件，无需任何单独的运行时引擎（除了 Flash 播放器插件）。

考虑到这些内容，让我们快速浏览一下 OpenOffice.org。

## 安装

OpenOffice.org 默认随 Fedora Core 的桌面安装一起安装。如果你因某种原因未安装它，请使用“系统设置”下的“添加/删除应用程序”菜单项。安装完成后，OpenOffice.org 每个工具的菜单项都可以在“主菜单 | Office”下找到，如图 7 所示。

每个 OoO 应用程序的图标也可以在面板中找到；除了 Writer 之外，我删除了所有其他图标，因为我不怎么使用其他的，而我面板上的空间很宝贵。

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_214_0.png)

> 图 7. Office 菜单默认显示所有 OpenOffice.org 工具。

## 配置和选项

一旦你开始创建文档，你就会想要执行一些操作——其中一些操作可以根据你的喜好进行配置。因此，在我讨论文档处理之前，让我们花一点时间设置 OoO，使其按照你想要的方式运行。

有两个地方可以按你的意愿调整 OoO 的行为——一个是在“工具 | 选项”下，你可以在此控制 OoO 的功能。我们将首先在此处花费时间。

一旦你创建了一个文档，你就会想保存它。OpenOffice.org 文档的默认保存路径是你的家目录（例如，在我的机器上是 /home/whil）。

如果你在网络上，你可能想将此路径更改为网络驱动器。无论你是否保留原来的保存路径，你都可能希望立即更改其他一些设置。以下是我每次在新机器上安装 OOO 时都会更改的设置。

首先，这一点非常重要，你需要设置保存新文档的默认文件格式。在安装期间，OpenOffice.org 会询问默认应使用哪种文件格式（OpenOffice.org 或 Microsoft Office），但根据 OpenOffice.org 邮件列表中的问题，许多人跳过了该选择，结果后来对 OOO 的行为感到困惑。

在选项对话框中，选择“加载/保存”节点和“常规”子节点，如图 8 所示。

将注意力集中在“常规”页面底部的“标准文件格式”控件上。你需要为每种文档类型指定默认文件格式——这不是非此即彼的选择。在列表中选择“文本文档”，然后使用“始终保存为”框选择新文本文档要保存的文件格式类型。务必仔细阅读此框中的选项，因为有些选项看起来很相似，例如“OpenOffice.org 文本文档”和“OpenOffice.org 文本文档模板”。

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_215_0.png)

选定文本文档的默认文件格式后，突出显示“文档类型”列表中的下一项，在“始终保存为”框中更改其文件格式，并继续处理剩余的文档类型。

如果你选择将最初在 Microsoft Office 中创建的文件保存为 OpenOffice.org 中的 Microsoft Office 文件格式，在实际执行保存时可能会收到警告。此警告提醒你可能丢失某些格式。出现此警告是因为 Microsoft Office 格式是专有的，因此 OpenOffice.org 开发人员不得不逆向工程文件格式，以创建与 Microsoft Office 兼容的文件。实际上，你可以忽略该警告；它只是“以防万一”而存在，
