
GIMP 支持许多不同的图形文件格式，它是将图像转换为其他地方可以使用（最特别是在 Web 上）的极佳工具，并且可以在不牺牲质量的情况下缩小文件大小。标题为“GIMP 支持的图形格式”的侧边显示了 GIMP 支持的所有图形和相关的文件扩展名。

这里是一些关于使用 GIMP 缩小图像大小的技巧，以便您能够轻松地在网页上分享它们，甚至将其发送给爱的人：
- 将您的文件保存为支持压缩的损耗格式。PNG 文件是一个很有吸引力的选择，因为支持高达 48 色彩，但我发现 JPEG 文件与其它类型计算机系统的用户交换最容易（并且在所有网络浏览器中都支持）。确保用不同的名称保存修改后的文件，这样您仍然拥有原始文件，以防您想要打印它们或在其他工具中编辑它们。

![](img/e88880e40d650bfe19d5b6927bd86568_379_0.png)

![](img/e88880e40d650bfe19d5b6927bd86568_380_0.png)

### GIMP 支持的图形格式

GIMP 允许按以下格式保存图形文件，每个格式由一个或多个相关的扩展名标识：

| 格式 | 扩展名 |
| :--- | :--- |
| Photoshop image | `.psd` |
| Wavefront PIX image | `.pix`, `.mask`, `.alpha` |
| 艺术 | `.txt`, `.text` |
| FLIC 动画 | `.fli` |
| 文件存档 | `.xcf` |
| 医学通信图像 | `.dcm`, `.dicom` |
| PostScript image | `.eps` |
| 图像传输 | `.fits` |
| 笔触 | `.gbr` |
| 笔触（动画） | `.gih` |
| 压缩图像 | `.xjt` |
| 图案 | `.pat` |
| GIMP 图像 | `.xcf` |
| 表格 | `.xcf` |
| JPEG | `.jpg`, `.jpeg` |
| 图标 | `.ico` |
| 动画 | `.pgm` |
| 文档 | `.ppm` |
| 图像 | `.sgi` |
| 图像 | `.rgb`, `.bw`, `.html` |
| 图像 | `.tga` |
| 位图图像 | `.bmp` |
| 位图图像 | `.xpm`, `.pc` |

一旦您对 GIMP 与您的目标输出格式关联的默认值进行了任何更改，点击“确定”（OK）保存您的屏幕截图。

GIMP 支持广泛的输出图形格式，但它也让捕获您的屏幕图像并微调您创建的文件特性变得非常简单。

主要专注于创建 OpenDocument Drawing (`.odg`) 格式的绘图。类似于 Inkscape（本章稍后介绍），OpenOffice.org Draw 允许你创建 SVG 格式的绘图，尽管目前导入现有的 SVG 图形的能力非常有限。请期待！

为了避免过频繁地使用“OpenOffice.org Draw”这个短语，在本节的剩余部分中，我将将其简称为 `oodraw`（这是从命令行界面执行 OpenOffice.org Draw 时必须输入的应用程序名称）。

## 安装 OpenOffice.org Draw

如果你从 Live CD 安装 Ubuntu、从使用安装程序的 Alternate 镜像 CD 安装，或者使用 OEM Mode 安装程序从 Alternate 安装程序安装，则系统会默认安装 Draw。如果你手动安装了 OpenOffice.org 演示软件 Impress，也会安装 Draw。

要在尚未安装 Draw 的系统上安装它，请从“管理”（Administration）菜单启动 Synaptic 软件包管理器（Synaptic Package Manager），选择“搜索”（Search），在显示的搜索框中输入 `Draw` 并点击“搜索”。搜索完成后，在新的 Draw 类别软件包列表中向下滚动，直到找到 OpenOffice.org Draw，然后在弹出菜单中右键点击该项目进行安装，如图 12.11 所示。

Synaptic 软件包管理器中的 OpenOffice.org Draw

根据你之前在 Ubuntu 系统上安装的软件，对话框可能会显示其他也必须安装的软件包并可能请求确认。点击“标记”（Mark）以接受（并强制安装）软件包。

一旦完成选择，点击 Synaptic 工具栏中的“应用”（Apply）在你的系统上安装 Draw。安装完成后，你就可以开始使用 Draw 了！

有关如何使用 Synaptic 软件包管理器或命令行 `apt-get` 或 `aptitude` 软件工具安装软件的更多详细信息，请参见第 20 节“添加、删除和更新软件”。

![](img/e88880e40d650bfe19d5b6927bd86568_383_0.png)

357

## 使用 Draw

在 6.06 LTS 版本中，Office 菜单中没有为 OpenOffice.org Draw 提供菜单项，因此你必须通过在 GNOME Terminal 或 xterm 窗口中输入 `oodraw` 命令并按回车来启动它。你可以使用 Alacarte 菜单编辑器为 Draw 添加菜单项，如第 5 章所示。当 OpenOffice.org Draw 启动时，它会显示一个空文档，如图 12.12 所示。

### Draw Tour

OpenOffice.org Draw 提供了优秀的在线帮助，OpenOffice 套件中的所有工具也是如此，因此我将不再介绍它包含的每个菜单和条目。然而，作为 Draw 的快速概览，图 12.12 中的标注突出了以下区域：
- `菜单`：Draw 中的下拉菜单结构与其他绘图软件包的组织方式类似，提供了熟悉的用户体验。右侧带有箭头的菜单项将指向其他相关的子菜单。
- `工具栏`：默认情况下，Draw 显示标准（Standard）、线条和填充（Line and Filling）以及绘图（Drawing）工具栏，点击相应的图标即可一键访问特定命令。你可以通过点击位于最右侧的工具栏控件来修改工具栏上显示的图标列表。你可以通过从视图（View）➪工具栏（Toolbars）子菜单中选择工具栏来显示其他工具栏或禁用默认工具栏。Draw 提供了丰富的绘图导向工具栏，例如 3D 对象工具栏，以便你快速方便地创建和修改 3D 图像的几何结构。

![](img/e88880e40d650bfe19d5b6927bd86568_384_0.png)

- `尺`：这些尺显示光标在当前绘图中的水平和垂直位置。每个尺的灰色部分反映了当前文档使用的页边距。你可以通过取消勾选视图（View）➪标尺（Ruler）菜单命令来禁用这些尺。
- `样式和格式窗口`：尽管默认不显示，但你可以随时按键盘上的 `F11` 键来显示此窗口。（再次按 `F11` 可以关闭此窗口。）样式和格式窗口可以方便地访问当前绘图中的可用样式，如果你选择不显示格式工具栏，这尤为方便。像 OpenOffice 中的任何浮动窗口一样，你可以通过双击窗口标题的灰色部分来停靠（dock）此窗口，使其成为 OpenOffice 界面的一部分而不是浮动窗口。你可以在停靠区域重复此过程来取消停靠窗口。
- `上下文敏感菜单`：在 OpenOffice.org Draw 中，工作的任何绘图的背景上点击右键，都会显示图 12.13 所示的上下文敏感菜单。此菜单提供了快速访问几个常用命令和子菜单的方法，包括修改当前页面格式、显示网格以及控制对齐到网格点的命令。

**图 12.13**

OpenOffice.org Draw 的上下文敏感菜单

OpenOffice.org Draw 提供了丰富的在线帮助，可以通过从帮助（help）菜单中选择 OpenOffice.org Help，或随时按键盘上的 `F1` 键来获取。图 12.14 显示了 Draw 帮助的主页，它包含可搜索的索引和从初始显示窗口列出的常用主题列表。

![](img/e88880e40d650bfe19d5b6927bd86568_385_0.png)

359

## 关于 OpenOffice.org Draw

OpenOffice 套件持续流行，并有更多免费资源可用。我最喜欢的几个 Draw 相关的网站是：
- http://www.openoffice.org/en/tutorials/: 绘图教程和
- http://www.openoffice.org: OpenOffice 的母站，该网站提供了邮件列表、文档等内容。
- http://www.openoffice.org/faq/: 多种语言的常见问题（FAQ）文件。

在互联网成为交换和展示文本图像的常用平台之前，图形格式并不重要。旧格式如 GIF 和 JPEG 正随着便携网络图形（PNG）以及同样强大的开放标准——W3C 标准可矢量图形（SVG）格式的出现而得到扩展。（关于 SVG 的更多信息，请参见 www.w3.org/Graphics/SVG/。）
