
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

选择 文件 -> 打开，然后选择你想要显示的 PDF 文件名。图 6-7 显示了在 Adobe Acrobat Reader 中查看 PDF 文件的示例。

![](img/1ccbe2b8efb451392a781396103b1e4e_305_0.png)

**图 6-7：**在 Adobe Acrobat Reader 中显示 PDF 文件。

# 266 第二部分：使用 Fedora 和 RHEL

Acrobat Reader 有很多很好的功能。例如，你可以在文档旁边显示书签列表，并点击书签跳转到特定页面。你还可以显示页面的缩略图以便快速滚动和选择页面。

使用工具栏或按钮，你可以翻阅 PDF 文档、放大和缩小、跳转到文档开头或结尾，并显示文档的不同视图（以及显示书签和页面缩略图）。要打印副本，选择文件 → 打印。

## 使用 Scribus 进行页面布局

对于小册、杂志、时报、目录和其他需要复杂布局的材料，你无法使用文字处理器来完成，而是需要一个页面布局应用程序。最流行的开源页面布局应用程序称为 Scribus (http://www.scribus.net)。

虽然 Scribus 主要用于制作印刷出版物，但你也可以使用它来制作所谓的“智能 PDF”。通过用 Scribus 创建的 PDF，你可以包含 JavaScript 和其他功能，让其他人与你的文本交互（例如填写表单）。Scribus 类似于 Windows 提供的 Publisher 应用程序。

在 Fedora 中使用 Scribus，请安装 `scribus` 包。该包附带了你可以启动项目的模板和示例（通常在 `/usr/share/scribus/` 中）。

安装 `scribus` 包后，你可以通过选择 GNOME 桌面上的应用程序 -> 办公 -> Scribus 来启动 Scribus。图 6-8 显示了 Scribus 中的小册布局示例。

当 Scribus 在桌面上运行后，你可以从选择模板开始（选择文件 -> 从模板新建）。选择一个小册、时报、演示文稿或基于文本的布局开始。以下是你可以可以在示例布局上的一些步骤，以熟悉使用 Scribus：

- **编辑文本**——在文本框中右键点击并选择编辑文本。在出现的 Story 编辑窗口中，更改文本、字号、文本宽度/高度缩放、字体对齐、颜色和其他属性。选择文件 -> 更新文本框和编辑以保存更改。
- **添加图像**——右键点击图像并选择图像。在你的文件夹中浏览你需要的图像。如果图像不合适，右键点击图像并选择编辑图像在 GIMP 中打开图像以调整大小或进行修改。右键点击图像并调整框架以调整大小以适应你的图像。
- **更改现有框架**——在任何框架中右键点击，然后点击已锁定（Is Locked）使框消失。一旦取消锁定，你就可以进行许多更改。抓住框架的角或侧边来调整大小。右键点击它并选择采样文本（填充它），或剪切、复制或删除它。用鼠标抓住框架将其拖动到某处。

# 第 6 章：使用 Fedora 和 RHEL 出版 267

- **更改属性**——选择设置。在文档设置窗口中，你可以更改尺寸和方向（如单面、双面、三折或四折）。同样，你也可以设置边距。从设置中添加作者、标题、页脚和页码。
- **你可以在 Scribus 上任何地方进行手绘**——插入手绘（笔图标）或插入贝塞尔曲线（墨水图标），然后使用鼠标在页面上绘图。你还可以使用工具栏绘制框、多边形。右键点击绘图元素设置属性。

![](img/1ccbe2b8efb451392a781396103b1e4e_307_0.png)

月份中的水果

此文档包含 2012 年 6 月的编译文本。Lorem ipsum 不是文本，真实的快乐并不存在于行中。

苹果是新物

此文档包含 2012 年 6 月的编译文本。Lorem ipsum 不是文本，真实的快乐并不存在于行中。

梨是新的

此文档包含 2012 年 6 月的编译文本。Lorem ipsum 不是文本，真实的快乐并不存在于行中。

行中的水果

此文档包含 2012 年 6 月的编译文本。Lorem ipsum 不是文本，真实的快乐并不存在于行中。

图 6：使用 Scribus 预制的高质量布局。

当你创建布局时，可以通过选择文件 → 打印来打印它。预检器窗口显示有关文档的信息。在页面右上角，你可以选择 PostScript 或几种 PDF 版本。你可以选择将输出指向打印机或到 PDF 或 PostScript 文件。

## 处理图形

用于创建和处理图形的工具变得丰富且强大。列表是 GNU 图像程序 (GIMP)，或者有时称为 GIMP。GIMP 让你能够创作以及修饰照片。Fedora 和 RHEL 自带的其他用于创建图形的工具包括截图（用于捕捉屏幕的程序）和用于创建矢量图形的 Inkscape。

> 交叉引用：参见第 8 章有关其他媒体应用程序的描述。

# 268 第二部分：使用 Fedora 和 RHEL

GIMP 是 Fedora 和 RHEL 自带的免费软件，用于处理照片和图形图像。要用 GIMP 创建图像，你可以导入绘画、照片或 3D 图像，或者从零开始。你可以通过点击应用程序菜单中的图形 -> GIMP 或在终端窗口中输入 `gimp` 来启动 GIMP。

图 6-9 显示了 GIMP 的示例。

![](img/1ccbe2b8efb451392a781396103b1e4e_308_0.png)

图 6-9：GIMP 是一个强大的图形处理工具。

GIMP 2.6 代表了 GIMP 一直以来最重要的版本之一。许多新功能旨在改进专业设计师所需的工具。所有新的选择工具都允许设计师选择带圆角的矩形区域。增加了一个滑块可以让你更精确地选择画刷大小。新的网格和对齐功能使其更加容易

## 第 6 章：在 Fedora 和 RHEL 上发布

对齐图层、路径或指南。数字照片编辑通过内置的红眼消除、全屏编辑以及新的裁剪和打印工具得到了改进。

在许多方面，GIMP 与 Adobe Photoshop 相似。有些人认为 GIMP 的脚本功能可以与 Photoshop 中的“操作”（Actions）相媲，甚至更优。GIMP 在色彩管理方面的能力一直落后于 Photoshop。然而，通过 GIMP 的最新功能，你可以校准屏幕，并使用来自相机和传感器的色彩配置文件进行工作（http://docs.gimp.org/en/gimp-imaging-color-management.html）。

熟悉 GIMP 最简单的方法之一是裁剪或修剪电脑上已有的图像文件。要裁剪一个文件，请按照以下步骤操作：

- 1. 启动 GIMP 并打开图像文件。
- 2. 在图像上点击右键。从区域的右键菜单中，选择工具（Select Tools） $\rightarrow$ 变换工具（Transform Tools） $\rightarrow$ 裁剪（Crop）。光标会出现（一个十字和刀的图标）。
- 3. 将光标移动到想要裁剪的图像区域左上角。点击并拖动光标到要裁剪区域的右下角。这样做，选定区域周围会出现一个选择矩形。
- 4. 松开鼠标按钮。选定区域边界的角上会出现选择框。点击并拖动句柄来调整边界大小。
- 5. 当边界处于正确位置时，按 Enter 键。图像将裁剪为边界大小。

> 提示：如果你出错了，可以从 GIMP 菜单中选择编辑（Edit） $\rightarrow$ 撤销（Undo），或按下 Ctrl+Z 组合键。输入 Ctrl+Y 可重做撤销的操作。

## 截图

如果你想展示在 Fedora 或 RHEL 上完成的工作示例，可以使用截图（Screenshot）程序捕获屏幕图像。GNOME 桌面在“应用程序”菜单的“辅助工具”（Accessories）下带有“截图”（Take Screenshot）程序。

> 注意：如果你没有安装 GNOME，也可以使用 GIMP 来捕取桌面截图。

要进行截图，从应用程序菜单点击辅助工具（Accessories） $\rightarrow$ 截图（Take Screenshot）（或输入 `gnome-screenshot`）。图 6-10 显示了截图程序的示例。

当截图程序首次打开时，它提供了捕获窗口内容或整个桌面的选项。你还可以设置几秒后延迟截图。一旦拍摄了截图，系统会提示你保存。你也可以将图像复制到剪贴板。

截图程序以 PNG 格式保存图像。你可以使用 GIMP 将其转换为其他格式。

![](img/1ccbe2b8efb451392a781396103b1e4e_310_0.png)

**图 6-10** 使用截图获取桌面或所选窗口的照片。

## 使用 Inkscape 创建矢量图形图像

当你需要在处理图形和文本时获得最大的灵活性时，矢量图形编辑器让你处理几何元素（如线、曲线和方框），而不是点（如你使用图像编辑器时那样）。因此，你的字体和图形将获得更清晰的边缘，并能够根据意愿绑定和塑造元素。Inkscape（http://www.inkscape.org/）是一款随 Fedora 一起提供的流行的矢量图形编辑器。

通过 Inkscape，你拥有一款与 Adobe Illustrator 和 CorelDraw 等商业产品功能相似的应用程序。Inkscape 以可缩矢量图形（SVG）创建图像——这是 W3C 的一个开放标准（http://www.w3.org/Graphics/SVG）。数千个 SVG 图形和剪贴画元素在公共领域或根据 Creative Commons 许可可用。

在 Fedora 中，安装 `inkscape` 包以获取 Inkscape。我建议你也安装 `openclipart` 包，这将为你提供数百个可用于在 Inkscape 创建中使用的剪贴画项目。安装了 `inkscape` 和 `openclipart` 包后，选择应用程序 $\rightarrow$ 图形 $\rightarrow$ Inkscape 矢量图形编辑器打开 Inkscape 窗口。图 6-11 显示了 Inkscape 窗口的示例：

![](img/1ccbe2b8efb451392a781396103b1e4e_311_0.png)

**图 6-11：** Inkscape 让你能够轻松操纵矢量图形和文本。

你可以从 Inkscape 提供的几十个模板之一开始（选择文件 File $\rightarrow$ 新建 New，并选择网页横幅、名片、DVD 封面或其他模板）。在新窗口打开后，有几种方法可以开始 Inkscape：

- **添加文本**——从左侧工具栏上选择文本图标，点击页面并开始输入。输入后，选择选择（Select）图标并点击文本。使用侧边栏或箭头调整文本大小。再次点击文本并使用箭头旋转它。用鼠标按住文本并拖动到你想去的地方。在文本仍被选中的情况下，选择文本 Text $\rightarrow$ 字体 Font，进入一个可以选择字体族、字体样式、布局和行间距的窗口。
- **添加图形元素**——从左侧工具栏选择矩形、3D 箱、圆形、星形或旋涡按钮。将光标移动到你想放置新元素的地方。将光标移动到你想放置新元素的地方，在该处点击并按鼠标，移动元素。

- **添加剪贴画**——如果你使用 `openclipart` 包，可以从那里导入剪贴画。选择文件 File $\rightarrow$ 导入 Import 并浏览 `/usr/share/clipart/openclipart`。从食物、地理、办公室、娱乐和交通等类别中选择。图像导入后，再次使用鼠标对其进行造型。
- **组合对象**——选择文本或剪贴画对象，然后按住 Shift 键选择其他对象。当选择了所有所需的对象后，选择对象 Object $\rightarrow$ 组合 Group。你现在可以将所有组合的对象作为一个整体处理。
- **使用图层**——选择图层按钮以添加、删除或调整图层大小。当你创建矢量图形时，可以通过选择 $\rightarrow$ 打印 Print 来打印该图形。从渲染（Rendering）选项卡中，你可以以矢量或位图格式保存图像。

## 使用扫描仪

Linux 扫描仪软件正由一项名为 Scanner Now Easy (SANE) 的努力驱动。这项努力希望标准化创建扫描仪、数字相机和视频摄像机等设备驱动程序的方法，并帮助简化使用这些设备的应用程序接口。

SANE 现在包含在 Fedora 和 RHEL发行版中。`sane-backends`、`frontends` 和 `xsane-image` 包都包含在本书的 DVD 中。你可以从 http://www.sane-project.org 获取最新的 SANE 驱动包。

想要将 Linux 作为发布平台的人通常对扫描仪的两个问题感兴趣：哪些扫描仪被支持，以及有哪些应用程序可以使用扫描仪。在过去，大多数 SCSI 扫描仪都得到了并行扫描仪的支持。然而，现在想知道更方便的 USB 扫描仪。

由于持续开发，新的扫描仪不断被支持。你可以在 http://www.sane-project.org/sane-supported-devices.html 找到当前的支持扫描仪列表。对于应用程序，这些目前在 Fedora 中可用！

- `xsane` —— 这是一个基于 X 的 SANE 图形界面；`xsane` 可以作为 GIMP 插件工作，也可以作为独立的应用程序。（从应用程序菜单，选择图形 $\rightarrow$ 扫描。）它支持 JPG、TIFF、PNG、PostScript 和 PNM 格式的 8 位输出。目前有实验性的 16 位 PNM (ASCII) 和原始格式输出。
- `scimage` —— 这是用于获取扫描图像的命令行界面。它支持与 `xsimage` 相同的格式。该命令获取扫描图像，并将数据重定向到标准输出（你可以将其保存到文件或管道到另一个程序）。

# 第6 章：在 Fedora 和 RHEL 上发布

除了这些应用程序之外，OpenOffice.org 套件还支持 SANE。由于 SANE 扫描仪驱动程序的架构，可以将扫描仪驱动程序与扫描应用程序分离。这使得在网络上共享扫描仪成为可能。

## Web 发布

你的文档和图像的终点不必是纸。在过去的几年里，在 Web 上发布已成为常见。如果你想控制自己的网站来发布思想和图片，Linux 系统包含了许多软件包可以帮助你实现这一目标。

如果你正在创建简单的网页，可以使用 OpenOffice.org Writer 或 SeaMonkey composer 等文字处理器创建基础的 HTML 文档。如果你足够勇敢，甚至可以尝试使用文本编辑器并手动添加 HTML 标记。对于更复杂的网站，有很多选择。

以下列表描述了可以用于发布到 Web 的开源软件包。这里描述的所有软件包都已为 Fedora 以及其他发行版制作了包。

> 警告：Web 服务器是互联网上坏法之分子的持续攻击目标。如果你决定尝试下面描述的某些软件，请务必检查项目网站，以确保你获得了最新的安全补丁和更新。

- **图片库**——Gallery 项目（http://gallery.menalto.com）让你创建在线相册。Gallery 让你能够轻松地将照片组织成相册、编辑图像、标记它们，并使用各种主题和颜色展示它们。在 Fedora 中，安装 `gallery2` 软件包。
- **博客软件**——流行的 WordPress 网站（http://www.wordpress.org）使用其开源 WordPress 软件（http://www.wordpress.org）为他人提供博客账户。如果你有自己的博客站点，可以在 WordPress.com 上注册一个免费账户，也可以使用该软件建立你自己的博客站点。在 Fedora 中安装 `wordpress` 软件包即可开始。
- **Wiki 软件**——Wiki 让你能够在在线上收集和组织大量的信息。与其自己编写关于某个主题的所有内容，不如创建一个 wiki，允许人们注册账户并在你的网站上添加正确的文章。开源社区可用的 Wiki 包括 MediaWiki（`mediawikiwiki` 软件包）和 MoinMoin（更多信息请分别查看 http://MediaWiki.org 和 http://MoinMoin.wiki.org 站点）。
- **内容管理系统 (CMS) 软件**——对于某些网站，你可能想提供一系列信息。对于活跃的社区，你可能想要提供文章、论坛、在线投票、下载和其他多样化的活动。内容管理系统（CMS）如 Drupal（安装 `drupal` 软件包）提供了一个在线创建和管理此类活动的平台。其他开源 CMS 系统包括 Plone（http://www.plone.org）和 Zope（http://www.zope.org）。Plone 和 Zope 也都为 Fedora 和其他 Linux 系统制作了包（分别为 `plone` 和 `zone` 软件包）。

在安装并让这些任何类型的网站在互联网上可用之前，你应该记住，要保持软件更新的最新并维护网站需要投入一些精力。但如果你愿意做出这种承诺，上述的开源项目可以帮助你制作出在互联网上发布的高质量网站。

### 总结

Linux 中提供的在纸张和 Web 上发布文字和图像的工具可以与市面上的商业软件相竞争。对于制作纸质文档，你有如 OpenOffice.org、AbiWord 和 StarOffice 等文字处理器。对于页面布局，有 Scribus。对于处理照片，你有 GIMP；对于矢量图形，你可以使用 Inkscape。

现在在互联网上发布内容的软件也涵盖了你可以想象的几乎任何类别。对于博客，你可以创建一个 WordPress 站点。对于图片库，有 Gallery 软件。内容管理系统包括 Drupal、Plone 和 Zope。创建 wiki，有 MediaWiki 和 Moin。

# 第7 章

# 在 Fedora 和 RHEL 中的游戏

### 本章内容

- Linux 游戏
- 在 Fedora 中玩开源游戏
- 寻找商业 Linux 游戏
- 在 Linux 中运行 Windows 游戏

每种 PC 游戏现在 Linux 上都可用。无论你是在寻找一个纸牌游戏来打发时间，还是寻找一个完整的在线 3D 游戏体验，你都会在 Linux 桌面上有几十（或数百）种选择。Fedora 项目中有一个强大的游戏特兴趣小组，确保了许多开源游戏不仅在 Fedora 中可以运行，而且运行得良好。

一些公司，如 ID Software（Quake）和 Epic Games（Unreal Tournament）已经做了将他们的游戏移植到 Linux 的工作，另一些则使用了第三方开发者（如 RuneSoft）将商业游戏移植到 Linux。独立游戏开发者，如 FrictionalGames（http://frictionalgames.com）和 Introversion Software（http://www.introversion.co.uk）现在正在 Linux 上制作高质量的游戏体验。商业在线游戏的 Linux 客户端，如 EVE Online（http://www.eve-online.com），也是可用的。

一些专家预测，游戏将是让 Linux 进入家庭的软件。遗憾的现实是，目前的“热门”标题仍然需要通过某种 Win32 仿真（通过 Cedega，位于 www.cedega.com）来引入 Linux。但即使是这样也变得更容易、更可靠。由于市场上的游戏应用程序相当有限，Linux 中的其他其他方面，越来越多的游戏每天都在变得可用。

Linux 中游戏相关软件增长的一个领域是用于制作高质量 3D 动画的工具。例如，Blender（http://www.blender.org）是一个用于制作动画、3D 模型、后期制作和渲染的开源项目，今天被用于制作商业游戏。Blender 的功能开始与商业 3D 动画软件竞争，例如 Studio Max（http://www.autodesk.com/3dsmax）、Maya（http://www.autodesk.com/maya）和 SoftImage SI（http://www.softimage.com）。

> 注意：你可以在 BlenderArtists.org 站点参与艺术家和游戏开发者社区。该站点提供了关于 Blender Game Engine 的许多活跃论坛。

本章检查了 Linux 游戏的现状，包括准备游戏环境的基础知识以及游戏的硬件考虑。它还描述了 Fedora 和 RHEL 自带或可以在其他地方找到的免费（主要是简单的 X 游戏）。对于运行其他平台的游戏，本章介绍了来自 Transgaming 的模拟器。

本章还讨论了有 Linux 版本的商业游戏。如果你喜欢这些演示，可以购买它们，有些可以在 Linux 上原生运行。

## 进入 Linux 世界

如果你运行了 Linux 系统并想立即开始，这里有一些建议：

- **检查游戏菜单**—— Fedora 的默认安装已经安装了许多游戏。如果你在 Linux 中运行 GNOME 桌面，从面板中选择应用程序 游戏。（本章描述了 KDE 和 GNOME 游戏）。
- **为你的 Linux 发行版制作的游戏**——许多流行的开源游戏已为你的发行版制作了包。打开添加/删除软件（PackageKit）窗口并选择游戏，查看 200 多个可以下载和运行的游戏。在 Ubuntu 中，添加/删除应用程序窗口显示了 300 多个可供下载和运行的游戏。
- **其他开源游戏**——如果你想要的开源游戏没有为你的发行版制作包，尝试去游戏的项目网站获取。互联网上有很多包含游戏列表以及指向每个游戏网站链接的站点。维基页面（http://en.wikipedia.org/wiki/Linux_gaming）和 Linux Game Tome（http://happypenguin.org）是很好的起点。
- **商业 Windows 游戏**——最新的商业游戏并未全部移植到 Linux。Linux 盒装商业游戏包括 Unreal Tournament 2003 和 2004，以及大约 50 款移植到 Linux 的顶级商业游戏。通过 Cedega.com，你可以运行数百种流行的 Windows 游戏。要查看你想要的游戏是否已验证可以在 Linux 中运行，请访问 Transgaming 游戏数据库（http://www.cedega.com/gamesdb/）查看其状态。

## 第 7 章：在 Fedora 和 RHEL 27 中游戏

在玩一些要求较高的 3D 游戏之前，你需要检查你的硬件是否能够处理这些游戏。某些需要 3D Linux 加速的游戏需要更多的内存（RAM）、更快的处理器以及特定的显卡才能在 Linux 上运行。在 Linux 中设置游戏机的问题将在本章稍后部分进行描述。

以下是 Fedora 以及许多其他 Linux 发行版中提供的游戏快速列表，你可以尝试一下。我按照从“简单上瘾”到“复杂上瘾”的顺序列出了它们：

- [Frozen Bubble](http://www.frozen-bubble.org) —— 《冰冻泡泡》被认为是最成瘾的 Linux 游戏。射击缓慢下降的冰冻泡泡和彩色泡泡组。每三个消除一组泡泡，或者直到它们全部消失（它们会过来并冰冻住你）。该游戏可以多人一起玩。（安装 `frozen-bubble` 包并从“游戏”菜单中选择它。）
- [Gweled](http://sebdebian.free/gweled) —— 这是热门游戏 Bejeweled 的克隆版，交换两个宝石以匹配三个或更多宝石（垂直或水平）。（安装 `gweled` 包并从“游戏”菜单中选择 Gweled。）
- [Warzone 2100](http://www.warzone2100.gameplanet.com) —— 这款 1999 年的实时策略游戏在 2004 年开源发布。建立一个基地，并在其基础上设计和建造车辆与武器，建立结构并研究新技术来进行全球战争。（安装 `warzone2100` 包并从“游戏”菜单中选择 Warzone 2100。）
- [Quake 3 Arena](ftp.idsoftware.com) —— Quake 系列中的几款第一人称射击游戏可以从 Id Software 下载。在 Fedora 中，安装 `quake3` 包并选择 Quake 3 Arena。启动的应用程序允许你下载 `quake3` 文件的演示版本，这些文件可以免费下载。阅读并接受许可条款以下载数据文件并开始玩 Quake 3 Arena。
- [Vega Strike](http://vastrike.sourceforge.net) —— 在这款 3D 动作游戏中探索宇宙。模拟模式允许你运输货物、成为赏金猎人或巡逻太空。在这个 3D 环境中，你可以与酒保聊天或观看新闻广播以关注宇宙中的事件。（要在 Fedora 中玩此游戏，请安装 `vastrike` 包并从“游戏”菜单中选择 Vega Strike。）

注意：尽管 Linux 游戏方面有所进展，但仍然有很多流行的 Windows 游戏无法在 Linux 上运行。出于这个原因，一些 PC 玩家会在电脑上维护一个独立的 Windows 分区，以便启动到 Windows 玩特定的游戏。

## Linux 游戏基础信息

Fedora 仓库中的“游戏”组有 200 多个软件包。然而，如果你只是在找几个消遣时间的游戏或现在已公开的旧商业游戏，但如果你兴趣了解更多在 Linux 上运行的新商业游戏，或者想了解 Linux 游戏的总体状况，有几个网站是你应该查看的。

## 在哪里获取 Linux 游戏信息

要找到 Linux 的最新游戏以及下载站点链接，请访问一些可用网站。以下是几个入门选网站：

- [TransGaming Technologies Cedega](http://www.cedega.com) —— 该公司的使命是将游戏从其他平台（Windows）引入 Linux。TransGaming 是 Cedege（以前名为 WineX）的提供者，这是一个强大的工具，允许你在 Linux 系统上玩数百款 PC 游戏。
- [The Linux Game Tome](http://happyppenguin.org) —— 该网站包含一个运行在 Linux 上的游戏描述和评论数据库。你可以通过关键词搜索此处列出的游戏。该网站还包含获取不同游戏的链接，以及其他游戏网站的链接。
- [Linuxgames.com](http://www.linuxgames.com) —— 这个网站可以让你对 Linux 游戏的状况有很好的见解。这里有教程（HOW-TOs）和常见问题（FAQs）的链接，以及讨论 Linux 游戏的论坛。还有包含特定游戏信息的网站链接。
- [Wikipedia](http://en.wikipedia.org) —— 在过去的几年里，维基百科已成为 Linux 商业和开源游戏的绝佳资源。通过维基百科有一份[开源游戏列表](http://en.wikipedia.org/wiki/List_of_open_source_games) 和一个[通用 Linux 游戏页面](http://en.wikipedia.org/wiki/Linux_games)。
- [id Software](http://www.idsoftware.com) —— id Software 提供 Doom 3、Quake 系列和 Rayenstein 的 Linux 版本。
- [Garage Games](http://www.garagegames.com) —— Garage Games 是一个托管独立游戏制作游戏的网站。在游戏商店（http://www.garagegames.com/pg）出售的许多游戏都有专门针对 Linux 的游戏移植版。
- [linuxgamepublishing.com](http://www.linuxgamepublishing.com) —— Linux 游戏世界的较新进入者，linuxgamepublishing.com 旨在成为原生 Linux 游戏以及其他平台游戏移植版的一站式门户。编写时，他们提供了大约二十款游戏，更多在路上。注意，要从此网站购买游戏必须创建一个用户账户。

- [Loki Entertainment](http://www.lokigames.com) —— Loki 的产品包括 Unreal Theatre、《Civilization: Call to Power》、《SimCity 3000》、《Railroad Tycoon》和 Quake III。Loki 公司已不再运营，但 Loki Launcher 仍可用作查看这些游戏的演示。
- [Tux Games](http://www.tuxgames.com) —— 如果你准备购买游戏，Tux Games 网站致力于销售 Linux 游戏。除了提供 Linux 新闻和产品，该网站还包含即将发布的游戏公告。
- [Linux Gamers' FAQ](http://icululus.org/lgfaq) —— 这个 FAQ 包含了关于免费游戏的丰富信息。它列出了将游戏移植到 Linux 的公司，告诉你在哪里获取 Linux 游戏，并解答了关于常见问题的疑问。关于游戏列表，请参见 http://icululus.org/lgfaq/gamelist.php。

## 为游戏选择显卡

通常情况下，游戏比大多数应用程序需要更多的内存、更强的处理器以及更多的磁盘空间。然而，显卡是最重要的硬件。

Fedora 对显卡的支持主要来自 X.Org 项目。要详细了解当前 Fedora 或 RHEL 版本具体支持哪些功能和显卡，请参考 X.Org Wiki (http://wiki.x.org)。从 X.Org 网站选择适用于你的 Fedora 或 RHEL 版本的 X.Org 软件版本的文档链接。

一种极大提升游戏体验的显卡是直接渲染基础（DRI）。无论你是使用 Cega 运行还是在 Linux 中原生运行游戏，显卡都需要支持硬件加速的视频显示。你可以从 DRI 项目（http://dri.sourceforge.org/）获取更完整的支持 DRI 的显卡列表。

以下是一些可以在 Fedora 和 RHEL 中用于游戏的显卡建议，它们支持私有 Linux 驱动或支持 DRI：

- NVIDIA — NVIDIA 显这是 Linux 游戏中最流行的显卡。开源驱动（nv）对 NVIDIA 显卡可用。此外，Fedora 11 将 Nouveau 驱动设置为 NVIDIA 显卡的默认驱动。Nouveau 为新显卡提供了更好的支持，以及更现代桌面所需的功能，特别是针对游戏。这些功能包括 RANDR 和 XRENDER 支持。你也可以从 NVIDIA 网站获取由 NVIDIA 提供的驱动。虽然这些不是开源驱动，但你可以下载二进制 NVIDIA 驱动。

来自 (http://www.nvidia.com) 或从 rpmfusion.org 网站获取。（若要直接从 NVIDIA 网站安装驱动程序，您必须安装 `kernel-dev` 和 `xorg-sdx` 软件包。）

注意：由于纯二进制驱动程序不是 Linux 内核的一部分，如果您在某个时刻更新了内核，您也需要更新 NVIDIA 驱动程序。rpmfusion.org 网站提供了一项很好的服务，将 NVIDIA 和 ATI 显卡驱动封装为 RPM 软件包，以匹配新的 Fedora 内核更新。更多信息请参阅此站点：http://rpmfusion.org/RPMFusion。由于已知 NVIDIA 驱动会在 Fedora 中运行共享的 Xorg 文件，有时会破坏你在系统中使用其他显卡的能力，因此在大多数情况下，使用来自 rpmfusion.org 的 RPM 包是 Fedora 安装 NVIDIA 驱动的最佳方式。

- **AMD 的 ATI Technologies** —— 2006 年，AMD微处理器公司（AMD）收购了图形芯片制造商 ATI Technologies。支持 DRI 的芯片包括 Mach64 (Rage Pro)、Radeon 7600 (R100)、Radon 2/8500 (R200) 和 Radeon 128 (Standard, Pro, Mobility)。基于这些芯片组的卡包括 All-in-Wonder 128、Rage Fury、Rage Magnum、Xpert 99 和 Xpert 2000。最近已添加对直到 9200 的 Radeon 芯片集的 DRI 支持。ATI 卡的专有纯二进制驱动程序可以直接从 AMD 网站 http://amd.com/support/ 获取。

AMD 关于其 ATI 图形芯片的公告承诺未来将对 Linux 提供强力支持。AMD 扩展了 Catalyst 软件的功能，以支持 ATI Radeon 2000 系列图形处理器。计划未来的功能将显著提升流行的 Linux 游戏（包括《毁灭战士3》和《雷云4》）的性能，并增加对 3D 加速特效加速间接 GLX (AGLX) 支持。

- **Intel** Intel 支持的视频芯片包括 i80（例如和 -dc100）和 i815。Intel 已向开源社区发布了这些及其他显卡的部分驱动程序。您可以从 Intel Linux 显卡驱动网站 (http://www.inteluxgraphics.org) 了解更多关于这些驱动程序的信息。

- **Matrox** Matrox 芯片组 (http://www.matrox.com) 拥有支持 DRI 的驱动程序包括 G200、G400 和 G450。使用这些芯片的卡包括 Millennium G450、Millennium G400、Millennium G200 和 Mystic G200。

要检查 DRI 是否在当前的显卡上运行，可以使用 `glxinfo` 命令（由 `glx-utils` 软件包提供）。输入以下内容：

```
