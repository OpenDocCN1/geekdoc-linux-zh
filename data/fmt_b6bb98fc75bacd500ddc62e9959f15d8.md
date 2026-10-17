
你也可以通过使用鼠标抓取任何窗口的标题栏并移动该窗口来确认此插件已启用。总有更大的改进空间！`gconftool-2` 对于从命令行快速查询和操作 GConf 设置非常有用。然而，`gconftool-2` 可能不是设置“正确”的 GConf 键、识别可能的值以及反复迭代多个设置和值直到获得你想要的效果的合适工具。我是命令行工具的忠实粉丝，但在大多数情况下，图形化工具比命令行工具更易用，特别是当你需要进行多次更改并使用配置值进行测试时。GNOME 用于检查和编辑 GConf 存储库的图形化工具 `gconf-editor` 在基于 GNOME 的系统上默认安装。你可以自己启动 `gconf-editor`，而不是通过 `sudo gconftool-2`，这样你编辑的就是你个人 GNOME 存储库的内容：

图 6-2 显示了 `gconf-editor` 启动时的界面。要找到特定的存储库键，点击 Find 命令显示图 6-3 所示的对话框。

# 图 6-2
图形化 GNOME 配置编辑器
![](img/1a233c34336fbf5a85d6eb785e401709_238_0)

*(注：由于您提供的待翻译文本包含大量重复的描述性文字，此处已针对核心内容进行了整合翻译。)*

# 第6 章：使用 Compiz 窗口管理器

大多数配置实用程序都让你非常容易地反复更改过多选项，以至于你都不知道如何将它们恢复到原始值（或者至少不知道那些原始值是什么）。CompizConfig 界面为这个问题提供了一个很好且一致的解决方案：它在每个单独配置设置的右侧提供了一个看起来像搅拌器的小图标。随时点击此图标即可将关联配置选项恢复到其原始默认值。

要启用任何插件但使用其默认配置，请点击图标和名称左侧的复选框，如图 6-7 所示。要配置任何 Compiz 或 Compiz Fusion 插件，点击该插件的名称或图标。这将显示该插件的配置面板，图 6-8 为示例。你也可以通过在配置面板（如图 6-8 所示）左侧面板的“使用此插件”（Use This Plugin）标签下方选择或取消勾选复选框，来启用或禁用插件。你可以点击左下角的“返回”（Back）按钮返回顶层 CompizConfig 面板。

图 6-8

在 CompizConfig 中配置特定插件

![](img/1a233c34336fbf5a85d6eb785e401709_242_0.png)

CompizConfig 屏幕顶部的“通用选项”（General Options）组（参考图 6-7）允许你配置 Compiz 本身的选项，因此可能会影响多个（或所有）插件。命令（Commands）、GNOME 兼容性和 KDE 兼容性组允许你定义键/命令映射，并微调 Compiz 对 GNOME 和 KDE 桌面的仿真。这些较少使用，因此我将在本节中重点介绍“通用选项”组。

# 第二部分：面向桌面用户的 Ubuntu

选择“通用选项”组后，会显示五个标签，如图 6-9 所示。

图 6-9
CompizConfig 中的“通用选项”

![](img/1a233c34336fbf5a85d6eb785e401709_243_0.png)

这些标签中的每一个都包含多个配置选项，例如：

- **通用（General）**：允许你配置光标及其大小、配置用于命令行功能的终端应用程序、控制 Compiz 是否提供警告和错误消息的听觉通知等。
- **显示设置（Display Settings）**：允许你配置 Compiz 与显示器交互的各个方面：屏幕显示表面纹理的精细程度、Compiz 是否尝试自动检测屏幕刷新率、屏幕在变换时是否会变暗（光照）、屏幕刷新率、屏幕更新是否仅限于在垂直消隐期间进行、Compiz 知知的输出设备以及它是否尝试自动识别它们等。
- **焦点与置顶行为（Focus & Raise Behaviour）**：允许你指定鼠标如何与窗口交互并选择：你是否必须点击窗口来设置焦点、当鼠标悬停在窗口上方时窗口是否会自动置顶（以及发生这种情况需要多长时间）、点击窗口内的任何地方是否会将窗口带到顶，以及哪些窗口在出现时不会自动抢占焦点。（最后一种需要启用 Regex Matching 插件，任何需要识别特定窗口或类型窗口的插件也是如此。）
- **按键绑定（Key Bindings）**：允许你定义与常用窗口操作（通用部分）相关的键绑定、鼠标操作或屏幕区域，以及在调用特定的 `run_command` 函数时运行的命令（命令部分）。此标签页上的命令还允许将按键、鼠标操作或屏幕区域映射到增加透明度（Increase Opacity）和减少透明度（Decrease Opacity）操作。
- **桌面尺寸（Desktop Size）**：允许你设置 Compiz 为每个桌面支持的视口数量及其水平和垂直结构。正如我在本节稍后讨论的，如果你要使用桌面立方体（Desktop Cube）插件，水平虚拟尺寸必须设置为 4。

作为使用 CompizConfig 的一个示例，让我们启用“旋转立方体”（Rotate Cube）插件，它是 Compiz 最著名的插件之一。在完全配置（连同相关插件）后，该插件会将你的活动视口显示为立方体的四个面，你可以快速旋转它来切换可用视口。你也可以在三维内旋转立方体以暴露它的顶部和底部，你可以用图像对其进行装饰。如果不充分利用极其强大的显卡，那不是太浪费了吗？要激活旋转立方体插件，请遵循以下步骤：

- 1. 配置你的桌面以便可以使用四个可用视口。
- 2. 如本节之前所述，你必须使用“通用选项”中的“桌面尺寸”标签将桌面的水平虚拟尺寸设置为 4，以提供四个可以作为 Compiz 立方体四面的视口，如图 6-10 所示。（默认值为 2，这很令人困惑。）要执行此操作，请选择 CompizConfig 的“通用选项”部分，选择“桌面尺寸”标签，要么输入新值 4，要么使用向上箭头增加“水平虚拟尺寸”参数的默认值 2。

![](img/1a233c34336fbf5a85d6eb785e401709_244_0.png)

完成后，你的屏幕应该看起来像图 6-10 所示。点击“返回”按钮返回主 CompizConfig 屏幕。

- 3. 点击图标和名称左侧的 X 来激活“桌面立方体”插件。如果你之前没有进行过任何配置更改，你将看到一个类似图 6-11 所示的警告对话框。

# 图 6-11

识别潜在的插件冲突

![](img/1a233c34336fbf5a85d6eb785e401709_245_0.png)

此类对话框是使用 gconf 而不是通用工具的优势之一。因为 Setting Manager 更了解插件，因此它可以检测冲突并提议禁用它们。

- 4. 选择“旋转立方体”插件（即桌面立方体）旁边的勾钩。此时，你应该能够以三种方式之一旋转桌面的面：
- 使用 `Ctrl+Alt+Right` 组合键将桌面向右旋转
- 使用 `Ctrl+Alt+Left` 组合键将桌面向左旋转
- 点击窗口标题栏并将窗口拖动到屏幕左边缘或右边缘。立方体会旋转，你移动的窗口将移动到新的视口。
- 将鼠标光标放在桌面上并移动鼠标滚轮（如果你有的话）。很厉害吧？更引人注目的是按住 Ctrl 和 Alt 键，点击并按住鼠标主键，上下移动鼠标以暴露顶部和底部。通过按下 `Ctrl+Alt+Down` 将立方体展开（展平为单屏幕），然后使用相应的方向键左右滚动。这让你很容易找到你寻找的视口。当你寻找的视口显示在屏幕中心时，释放 Ctrl、Alt 和方向键以全尺寸显示它。

现在你已经玩过了这个插件，你可能想进一步对其进行微调。一些有趣的建议是：

- 使用桌面立方体的“外观”标签，通过在“立方体盖”（Cube Caps）部分指定图像文件为桌面立方体的顶部和/底部添加自定义图像。
- 使用桌面立方体的“外观”标签，通过选择渐变开始和结束颜色或在“天穹”（Skydome）部分指定图像文件，为三维旋转立方体后的空间指定背景图像或渐变。
- 使用桌面立方体的“透明立方体”（Transparent Cube）标签将立方体设置为透明，然后激活“立方齿轮”（Cube Gears）插件，在立方体旋转时在其内部显示旋转的齿轮。

图 6-12

在使用立方齿轮插件时旋转透明立方体

![](img/1a233c34336fbf5a85d6eb785e401709_246_0.png)

# 第二部分：面向桌面用户的 Ubuntu

这些建议展示了通过 Compiz 及其插件可以享受的乐趣，以及它提供的图形能力惊人的范围和威力。鉴于你可以配置的潜在设置数量以及 Compiz 提供的各种华丽功能，你可能再也无法静心投入实际工作了！

## 提示

一个常见的 Compiz 问题是新创建窗口的标题栏会显示在屏幕顶部的 GNOME 面板下方。如果发生这种情况，请首先确保已启用“放置窗口”（Place Windows）插件。该插件使用了一种更智能的算法，在将新窗口放置在屏幕上时考虑标题栏。你也可以通过按住 `Alt` 键并在想要移动的窗口中按住鼠标左键来移动窗口，使其标题栏可见。此时会显示标准的窗口移动图标，你可以拖动窗口直到其标题可见。■

# 这些是我最喜欢的事物之一。

我通常在默认设置中激活的某些插件如下：

- **桌面立方体/旋转立方体 (Desktop Cube/Rotate Cube)**：在上一节中讨论过，快速切换可用的视口并旋转带有这些视口侧面的立方体不仅具有吸引力，而且非常出色。尽管我意识到这正在消耗更多的 CPU 资源，但这种效果太酷了，我无法抵制激活它。
- **环形切换 (Ring Switch)**：此插件增加了 `Super+Tab` 命令，以环绕旋转的圆形环状显示可用窗口，并在中心显示所选窗口的标题。它类似于标准的 `Alt+Tab` 应用程序切换器，但有趣得多。
- **水滴效果 (Water Effect)**：这个插件绝对会让邻居们惊讶又开心，可以通过 `Shift+F9` 切换雨滴。这只有在雨滴激活时才会浪费计算能力，但当你向别人展示 Compiz 时，它的视觉效果非常震撼。
- **果冻窗口 (Wobbly Windows)**：在本章中关于使用 GNOME 配置工具来配置 Compiz 效果的章节中讨论过，果冻窗口在移动窗口时会提供一种摇晃的、胶质的视觉效果。桌面立方体/旋转立方体插件提供了 Compiz 的经典效果之一。

正如本章较早提到的，请参阅 http://wiki.compiz-fusion.org/Plugins 获取所有可用 Compiz 和 Compiz Fusion 插件及其配置的完整列表。www.compiz.org/Plugins  Compiz 插件列出了与 Compiz 捆绑默认插件，并提供了你可能认为有用的额外外部插件的链接。

208

# 第 6 章：使用 Compiz 窗口管理器

# Compiz 的其他实用软件包

上一节显示，Ubuntu 仓库中提供了一些非常有用的 Compiz 相关软件，但 Ubuntu 系统默认并未安装它们。上一节讨论了 Compiz 配置设置管理器（CompizConfig Settings Manager）；本节及其子节将讨论其他一些你可以安装并供 Compiz 使用的有趣包（这些包实际上可以在任何合成环境中工作，包括 Xcompmgr）。

# 安装和使用 Avant Window Navigator（前卫窗口导航器）

如果你见过 Mac OS X，你可能熟悉它的 dock（程序坞），它是屏幕底部（默认情况下）的一个面板状应用程序，你从中查找你喜爱的应用程序，以及代表运行应用程序的图标和垃圾桶图标。尽管 Gnome 有自己的面板，Microsoft Windows 有自己的任务栏，但很难否认 Mac OS Dock 是这些具有相似功能的实体中最活跃的一个。也许直到现在都是如此。Avant Window Navigator (AWN) 是一款用于合成窗口管理器的开源 dock 应用程序，为 Compiz 提供了一个具有吸引力、强大、可扩展且完全可自定义的 dock。Avant Window Navigator 由 Neil Patel 开发，目前其主页位于 Ubuntu Launchpad 网站，地址为 https://launchpad.net/awn。图 6-13 显示了同时运行 Avant Window Navigator 及其配置工具的 Ubuntu 桌面的默认外观。

Ubuntu 系统默认不安装 Avant Window Navigator，但你可以使用你喜爱的包管理工具轻松安装它，如第 19 节所示。安装 Avant Window Navigator 还会安装它使用的库、它所需的一些 Python 模块以及配置管理器。

**提示** 要获取最新版本的 Avant Window Navigator 及其插件，你应该将 `http://ppa:launchpad.net/awn-testing/ubuntu` 添加到 `/etc/apt/sources.list` 中列出的源中。有关启用 Ubuntu 包管理系统所需的其他源的信息，请参阅第 19 章。

安装 AWN 后，你可以从任何命令行应用程序（如 `xterm` 或 GNOME Terminal）手动启动。要配置 AWN 在登录时自动启动，你可以在 Awn 设置应用程序中启用它（本文稍后将讨论），或将其添加到标准的启动应用程序设置中。对于后者，选择系统偏好设置中的启动应用程序工具。在“启动程序”选项卡上，点击“添加”，并输入 Avant Window Navigator 的信息，如图 6-14 所示。

# 第二部分：面向桌面用户的 Ubuntu

图 6-13

Avant Window Navigator 及其管理应用程序

![](img/1a233c34336fbf5a85d6eb785e401709_249_0.png)

图 6-14

配置 Avant Window Navigator 在登录时自动启动

![](img/1a233c34336fbf5a85d6eb785e401709_249_1.png)

210

# 第 6 章：使用 Compiz 窗口管理器

在 Ubuntu 系统中，我倾向于取消底部面板，并将通常包含的有用小组件（最著名的是空间切换 Space Switch）添加到顶部面板，如图 6-13 所示。在屏幕底部使用 AWN 并在顶部使用标准的 GNOME 面板为我兼顾了这两者的优点。

一旦安装并启动 AWN 管理器，你可以通过选择 系统 > 偏好 > AWN manager 来启动 AWN 应用程序。这将显示图 6-13 所示的应用程序，允许你自定义 dock 图标的显示方式；配置在使用时不自动隐藏；配置 dock 的外观；添加小组件、启动器和主题来自定义 dock。图 6-15 显示了具有以下自定义的 AWN：

- **偏好行为 (Preferences Behavior)**：这个实际上很难显示，因为它会导致 dock 在不使用时消失在屏幕底部。要重新显示 dock，请将光标移动到屏幕底部。
- **偏好图标效果 (Preferences Icon Effects)**：作为图标效果的聚光灯会导致当光标悬停在 dock 中的图标上时，任何图标都会闪烁。
- **偏好样式 3d (Preferences Style 3d)**：代替 2D dock 背景，激活此项将允许 AWN 使用图 6-15 所示的渐变背景。与图 6-13 显示的默认扁条进行比较。

默认情况下，AWN 只显示运行应用程序的图标。AWN 两个最棒的功能是能够安装执行特定功能的小组件，以及安装新主题来自定义 dock 本身的外。Ubuntu 提供了一组良好的 AWN 小组件，但你可以从 http://wiki.awn-project.org/Applets 和 http://wiki.awn-project.org/Awn-extras 查看可用小组件列表（并学习如何构建和安装它们）。

## 提示

AWN 插件允许你改进某些应用程序与其在 AWN 中图标之间的交互。针对 Amarok、Audacious、Banshee 和 Rythmbox 等音频应用程序的插件，以及在线即时聊天应用程序 Pidgin 和 XChat 的插件，可以从 http://wiki.awn-project.org/Plugins 获取。

AWN 主题允许你对 dock 外观进行额外配置，其安装和使用简单得多。可以从 http://wiki.awn-project.org/Themes 下载大量的自定义主题。我最喜欢的主题之一 Transparent 3D 已经不可用，但你可以从 www.queervisions.com/2007/10/awn_avantwindow.html 下载它。

211

# 第二部分：面向桌面用户的 Ubuntu

## 图形 6-15
自定义后的 Avant Window Navigator（高级窗口导航器）

![](img/1a233c34336fbf5a85d6eb785e401709_251_0.png)

一旦你下载了 AWN 主题，可以通过选择 Awn Manager 的“主题”（Themes）选项卡、点击“添加”（Add）并导航到存储主题的位置来安装它。（我倾向于将它们放在 `~/ART/AWN` 中，这样我想在其他系统上使用它们时就知道该去哪里找了。）然后选择包含该主题的压缩 tar 存档文件并点击“打开”（Open）。添加主题后，“主题”选项卡将如图 6-16 所示。

# 第 6 章：使用 Compiz 窗口管理器

![](img/1a233c34336fbf5a85d6eb785e401709_252_0.png)

然后你可以选择想要使用的主题并点击“应用”（Apply）使其生效。图 6-17 显示启用了名为 Frosted Glass（磨砂玻璃）主题的 AWN。

AWN（以及 Compiz 本身）变得越来越流行，会有越来越多的小组件、应用程序启动器和主题可用。期待享受数小时的自定义乐趣。有关 AWN 的更多信息，请参阅 http://wiki.awn-project.org 上的 Avant Window Navigator Wiki。

## 提示
我已经使用 AWN 有段时间了，并看到过它崩溃过几次，此时它所有的图标都会消失，尽管 dock 本身仍然可见。要让 AWN 重新绘制所有图标，只需启动任何其他图形应用程序。你所有的图标都会重新出现。■

# 第二部分：面向桌面用户的 Ubuntu

## 图形 6-17
带有 Frosted Glass 主题的 Avant Window Navigator

![](img/1a233c34336fbf5a85d6eb785e401709_253_0.png)

## Ubuntu 系统的其他 Dock 软件

如果你喜欢拥有 dock 的主意，但对 Avant Window Navigator 的外观和体验不满意，还有其他几个软件包可以提供 dock。毕竟这是 Linux——选择从来不是问题。我最喜欢的 dock 有以下：

- Cairo-Dock：一个优秀且高度可定制的 dock 软件包，提供了许多有趣的插件。与其他 dock 一样，Cairo-Dock 在 Ubuntu 系统没有默认安装。为了尝试 Cairo-Dock，你应该安装 `cairo-dock` 和 `cairo-dock-plugins` 软件包，以充分利用 Cairo-Dock 的功能。图 6-18 显示了一个在屏幕底部运行的高度自定义 Cairo-Dock 实例，用于替换底部面板。

# 第 6 章：使用 Compiz 窗口管理器

## 图形 6-18
自定义的 Cairo-Dock 安装

![](img/1a233c34336fbf5a85d6eb785e401709_254_0.png)

- **Gnome Do：** 一个流行的 GNOME 应用程序启动器，同时也提供了集成搜索功能，GNOME Do 还提供了一个名为 *Docky* 的快速轻量级 dock，你可以通过在 GNOME Do 首好应用程序的“外观”（Appearance）选项卡上选择 Docky 为“已选主题”（Selected Theme）来启用它。与其他 dock 一样，Ubuntu 默认没有安装 GNOME Do——你必须安装 `gnome-do` 软件包来尝试 GNOME Do。图 6-19 显示了屏幕底部运行的自定义版本 Docky，用于替换底部面板。

# 第二部分：面向桌面用户的 Ubuntu

## 图形 6-19
Docky 模式下的 GNOME Do

![](img/1a233c34336fbf5a85d6eb785e401709_255_0.png)

如果你决定喜欢这些主题，可以通过 System -> Preferences 启动 Emerald。Emerald Theme Manager 如图 6-20 所示，也显示了该程序认为自己是 Thamer，从现在起我将这样称呼它。

Thamer 显示的初始对话框并不有趣，主要是因为默认没有提供主题。图 6-20 显示了加载两个主题后的对话框。要下载并安装默认主题集，请使用你喜欢的浏览器访问以下网站并寻找标记为 Emerald Theme 或 Beryl Emerald Theme 的主题：

- www.compiz-themes.org
- http://compizfusion.blogspot.com/2008/01/compiz-fusion-emerald-themes.html

# 第二部分：面向桌面用户的 Ubuntu

## 图形 6-20
Emerald Theme Manager，即 Emerald Thamer

![](img/1a233c34336fbf5a85d6eb785e401709_257_0.png)

尝试主题是趣的。选择一个吸引你的主题可以帮助你的计算机系统反映你的个性和审美。我这周最喜欢的是 SolidSlateModified，我忘记上个月喜欢的是什么了。

如果你下载的所有默认主题都不“完美”，并且你很有艺术天赋，你甚至按照以下地址提供的说明创建（并发布）你自己的主题：http://wiki.compiz-fusion.org/Decorators/Emerald。

## 总结

合成窗口管理器（特别是 Compiz 窗口管理器）长期以来一直是 Linux 世界的宠儿。现在，Compiz 已经成为基于 GNOME 的 Ubuntu 系统上默认安装并启动的窗口管理器。本章解释了合成窗口管理器背后的基本概念，并简述了 Linux 上合成技术以及 Compiz 本身的历史。随后，本章解释了如何配置 Compiz、如何查找并安装插件以增强其功能，以及安装和使用各种 Compiz 相关的工具，如 CompizConfig Settings Manager（Compiz 配置设置管理器）、Avant Window Navigator、其他流行的抽栏工具以及 Emerald 窗口装饰器。

下一章将讨论 Evolution，这是一款流行的 GNOME 电子邮件客户端，它支持标准的 POP 和 IMAP 邮件传输器，并与微软 Exchange 邮件服务器提供了令人深刻的互操作性，包括日历和其他办公相关功能，这些功能在商业环境中使用 Linux 系统时几乎是必须的。

# 使用 Evolution 管理电子邮件和个人信息

在网页浏览器之后，电子邮件是互联网的杀手级应用。与 Web 浏览器一样，发送和接收电子邮件在开源社区中同样重要。此外（不幸的是，与随处使用 HTML 的 Web 浏览不同），有许多不同的协议用于接收电子邮件。你对电子邮件客户端的选择取决于它是否支持你的互联网服务提供商（ISP）、公司或学术机构用于发送、存储和递送电子邮件的协议。

解决“用哪种协议、哪种客户端”问题的最简单方案是使用一个支持人类已知的各种现代电子邮件协议的单一客户端。Ubuntu 包含一个名为 Evolution 的电子邮件客户端，它履行了这个承诺。Evolution 是一个基于 GNOME 的邮件客户端，最初由一家名为 Ximian 的公司开发。奇怪的是，Ximian 最终被 Novell 收购，虽然 SUSE 的 Linux 产品很大程度上以 KDE 为中心，但至少说明 Novell 有眼光，能看出好软件。

Evolution 可以从支持所有流行电子邮件协议的邮件服务器接收邮件，包括 POP、IMAP、IMAP4rev1、Microsoft Exchange、Menlo GroupWise，以及几个需要通过 Google 搜索才能找到是谁在使用它们（以及为什么用）的协议。对于发出的邮件，Evolution 可以与任何简单邮件传输协议（SMTP）服务器或任何兼容标准 Linux/UNIX Sendmail 程序的服务器通信。

此外，Evolution 不仅仅是一个多协议电子邮件客户端——它实际上更像是一个个人信息管理（PIM）包，发送和接收电子邮件只是其一方面。Evolution 还提供了对 PIM 功能的集成支持，包括：

- 管理存储在本地或在轻量级目录访问协议（LDAP）或 Microsoft Exchange 服务器上的联系人
- 管理存储在本地或 Microsoft Exchange 服务器上的任务列表
- 管理本地日历、基于 Web 的日历或 Microsoft Exchange 日历

## 本章内容

- 设置你的电子邮件客户端
- 发送和接收电子邮件
- 组织你的电子邮件
- 归档电子邮件（存档）
- 处理垃圾邮件
- 访问 Web 邮箱
- 管理联系人
- 管理你的日历

现在，你可能在这一引言中看到某种线索——与 Microsoft Exchange 服务器及其提供的服务的兼容性。无论如何，许多企业都依赖 Microsoft Exchange 来满足诸如安排会议、检查和共享同事的邮件服务器以及其他办公相关功能等需求。Exchange 服务器的邮件服务器部分只是特殊的 IMAP 邮件服务器，但 Exchange 的日历和调度部分在很大程度上是微软特有的。Evolution 对完全互操作的支持确实令人印象深刻。

本章解释了如何配置和使用 Evolution 作为邮件客户端、联系人管理器和日历系统。本章首先讨论了如何创建初始邮件账户以及如何读取、发送、组织和过滤邮件；并讨论了 Evolution 独有的强大的虚拟文件夹（Virtual Folders）功能。它解释了如何使用 Evolution 访问 Gmail、Yahoo! 和 Microsoft Hotmail/Live 等流行的 Web 邮箱系统。然后讨论了如何配置和使用 Evolution 的联系人和日历管理部分。有关 Evolution 功能的更多信息，请参阅本章末尾的“关于 Evolution 的附加信息”章节。

## 启动 Evolution

你可以通过多种不同的方式启动 Evolution：

- 选择屏幕顶部 GNOME 工具栏中的信封图标（如图 7-1 所示），并从下拉菜单中选择邮件（Mail）。这是启动 Evolution 最早且最常见的方式。
- 从“应用程序-办公”菜单中选择“Evolution Mail and Calendar”。
- 在 GNOME Terminal 或 `xterm` 窗口中输入 `evolution` 命令并按回车。

图 7-1
你 GNOME 桌面上的 Evolution 图标

Evolution 图标

![](img/1a233c34336fbf5a85d6eb785e401709_261_0.png)

# 第7章：使用 Evolution 管理电子邮件和个人信息

Ubuntu 的 GNOME 桌面还经过预先配置，如果你在 Web 浏览器或其他网络应用程序中点击设计用于发送电子邮件信息的统一资源定位符（URL）（称为 mailto URL），它会自动为你启动 Evolution。

下一节将讨论 Evolution 设置向导（Evolution Setup Assistant），它将引导你完成在 Evolution 中创建第一个电子邮件账户的过程。

# 使用 Evolution 设置向导

当 Evolution 首次启动时，Evolution 设置向导的“欢迎”窗口会显示并开始引导你完成在 Evolution 中创建第一个电子邮件账户的过程。

为了稳妥起见，在这里稍微说明一下——Evolution 设置向导是配置 Evolution 在某处发送和接收账户；它并不创建账户。例如，尽管我使用我的 Ubuntu 发送和接收邮件，但我的电子邮件账户实际上位于托管我域名的 ISP。Evolution 设置向导让我告诉 Evolution 从何处检索收到的邮件，以及通过哪个邮件服务器发送出的邮件。

# 注意

当然，如果你运行邮件服务器且它就在你运行 Evolution 的同一台机器上，那么你的 Ubuntu 可能就是你的正式电子邮件账户。我将在第 30 章“设置邮件服务器”中详细讨论这一点。■

接收电子邮件的概念可能会令人困惑，我通常将其理解为“接收”与“检索”的区别——我的实际电子邮件账户（在 ISP 处）接收我的邮件，而 Evolution 让我从那里检索邮件以便读取、归档或删除它们。在正式术语中，这种区别是邮件传输代理（MTA）、邮件传递代理（MDA）和邮件用户代理（MUA）。ISP 处的 MDA 将 MTA 接收到的邮件放入你的 ISP 邮箱箱中。MUA（在此例中 Evolution）从你的 ISP 邮箱箱中检索邮件并在本地系统上显示。有关这些术语的更多详细信息，请参阅第 30 章。

设置向导欢迎窗口显示后，点击“下一步”进入设置过程的下一个部分。显示一个如图所示的窗口。

如果你已经是 Evolution 用户并在另一个系统中创建了 Evolution 备份文件，可以通过勾选“从备份文件恢复 Evolution”复选框，并在点击“选择要恢复的 Evolution”按钮后通过对话框导航到 Evolution 备份文件的位置来导入其内容。在较新版本的 Evolution 中，你可以通过选择文件菜单中的“备份设置”命令并指定要创建的备份文件名来创建这些备份文件。备份文件以压缩的 tar 包格式创建，默认名为 `evolution-backup.tar.gz`。

## 从旧版本的 Evolution 迁移

如果你已经是 Evolution 的用户，但使用的 Evolution 版本没有提供“备份设置”命令，你仍然可以使用命令创建一个压缩的 tar 文件，该文件包含你主目录下 `.evolution` 目录（及其子目录）的内容的内容并以此来迁移你现有的 Evolution 配置信息。你可以通过使用如下命令来实现此：

```
