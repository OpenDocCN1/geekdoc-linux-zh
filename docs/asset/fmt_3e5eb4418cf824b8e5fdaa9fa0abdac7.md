
它曾被称为 `KDE 4`，但现在分为 `KDE Plasma` 工作空间、应用程序和平台，整合为 `KDE` 软件编译 4。自 2014 年以来，`KDE` 不代表 `K`。`Matthias Ettrich` 在 1996 年首次启动了 `KDE`。`KDE` 为 `Linux` 用户提供图形界面以选择桌面。你可以将 `KDE` 视为 `Linux` 的 `GUI`。`KDE` 证明了 `Linux` 用户像 `Windows` 一样使用它。为 `Linux` 用户选择桌面。

你可以认为没有 `KDE` 和 `GNOME` 的 `Linux` 类似于 `Windows`，只是它们通过 `x` 服务器连接到 `Linux` 而不是操作系统。在安装 `Linux` 时，你在三个不同的桌面环境（如 `KDE` 和 `GNOME`）中选择你的桌面。另一个流行的站点如 `KDE` 是 `GNOME`。两者都带有其他特性和一些分发。`KDE` 带有各种特性。一些关键特性列在如下。

`KDE` 项目由 `KDE` 社区管理，这是一个创建和推广自由软件的人群，例如 `KDE Plasma` 和 `KDE Frameworks`。还有非 `Qt` 应用程序，如 `Gcompris`（最初是 `GTK`）或基于 `Web` 的项目如 `WikiLearn`。

## KDE 平台的各个部分

`KDE` 是一个大型软件开发者社区。我们在构建多年开发的基础设施方面具有共同点：`KDE` 平台。

- `KDE Plasma` 工作空间：这是一个针对各种设备（如 `PC`、`笔记本`或`移动设备`）优化的用户界面特性。`KDE Plasma` 是具有自定义布局和面板的自定义桌面架构，支持虚拟桌面和小组件。它们使用 `Qt 5` 和 `KDE Frameworks 5` 编写。

- `KDE Frameworks`：许多 `KDE` 应用程序是在集成框架的帮助下构建的。它是基于 `Qt` 的软件和库集合（以前称为“`kdelibs`”或“`KDE Platform`”）。

- `KDE` 应用程序：许多运行如 `Kdenrive`、`Krita` 的应用程序主要构建在 `KDE Frameworks` 中，并且通常是 `KDE` 应用程序的一部分。

## KDE 核心项目

### Plasma 工作空间

工作空间用于减少杂乱并使桌面更易于导航。它还可用于组织你的工作。例如，你可以在一个工作空间放置通信窗口（如电子邮件和聊天程序），在另一个工作空间处理你的工作。以下是 `K Desktop Environment 1.1` 中使用的工作空间：

- 1. `KDM`
- 2. `KWin`
- 3. `Plasma`
- 4. `Systemsettings`

“工作空间”是 `KDE` 提供的所有图形环境的统称。`Plasma` 将组件分为“数据引擎”和对应的可视化部分。它的设计目的是当给定数据有多种可能的可视化方案时，减少总编程工作，并让数据引擎和工作空间更容易独立地编写。目前，正在开发三个工作空间：

- 针对传统桌面电脑和笔记本电脑的 `Plasma Desktop`
- 针对笔记本的 `Plasma Network`
- 针对平板电脑和设备的 `Plasma Active`

`Plasma` 下有多种工作空间：

- 桌面（`Desktop`）：`Plasma Desktop` 是 `KDE` 开发的第一个工作空间。它随着 `KDE SC 4.2` 的发布而宣布。它专为桌面电脑和较大的笔记本电脑设计。默认配置类似于 `K Desktop Environment 3` 和微软 `Windows XP`，具有高度的可配置性，允许大幅偏离默认布局。它是对早期类 `Unix` 系统 `KDE` 桌面环境中包含的几个桌面交互程序的根本性重写，侧于视觉效果和特殊图形特效。桌面工作空间用统一系统取代了 `K Desktop Environment 3` 中最后的 `KDesktop` 外壳、`Kicker` 任务栏和 `SuperKaramba` 组件引擎，可以替代其他设计。

- 网络电脑（`Netbook`）：`Plasma Netbook` 是第二个工作空间。它针对网络电脑（网络电脑是一类小型、轻量、无遗留且廉价的笔记本电脑），也可用于平板电脑 —— 它是随 `KDE SC 4.4` 发布的第一个稳定版本。

- `Plasma Active`：它本身不是一个工作空间，而是构建在框架之上的一个服务，允许使用任何 `QML` 文件创建完整的工作空间，而无需使用 `C++` 编程。`Plasma Active` 是兼容触摸屏工作空间的基础。兼容 `Active` 的 `Contact` 应用和基于 `Calligra Suite` 的文档查看器已经可用。

- 轮廓（`Contour`）：`Contour` 是用于平板设备的 `Plasma` 接口。其开发由 `basysKom` 于 2011 年 4 月启动。`Contour` 取代了早期的平板原型，现在是主要工作空间，并作为 2011 年 10 月发布的 `Plasma Active 1.0` 的部分发布。

- 移动（`Mobile`）：`Plasma Mobile` 的目标是通过触摸输入的智能手机和平板设备。它们最初于 2011 年随 `Plasma Active 1.0` 一起发布，但开发重心转向 `Contour`。与此同时，`Plasma Mobile` 被 `Plasma Active` 代代。

## 特性

- `Plasma` 本质上是一个包含其他小部件的应用（`applet`）。两个主要的容器（`containments`）示例是桌面背景和任务栏。容器可以是开发者想要的任何内容：图像、动画甚至是 `OpenGL`。图像通常被使用，但在 `Plasma` 中，用户可以使用任何小部件作为桌面背景而不会丢失该部件的功能。这允许小部件在桌面、任务栏以及不同的可视化界面之间拖动 —— 从 `KDE 4.0` 到 `4.2`，默认主题如 `Oxygen`。该主题以深色调为特征。在 `KDE 4.3` 中，新的 `Air` 取代了它，`Air` 在透明度和基础色上占主导地位。可以通过权限选择并安装 `Plasma` 的新主题。

- `Plasma` 组件的可扩展性允许它们调整大小并旋转到任何尺寸，只需短暂暂停即可重绘。`Kross` 脚本框架将允许开发者使用 `C++` 之外的多种编程语言编写组件。组件的大小是可变的，并且可以根据其大小显示更多或更少的数据。

- `Plasma` 支持其他组件。`SuperKaramba` 是 `KDE 3` 系列使用的组件引擎，出于遗留原因被添加进来。

## KWin – 窗口管理器

它是 `X` 窗口系统的管理器。它是 `KDE` 软件编译不可或缺的一部分，尽管它可以独立使用或与其他桌面环境一起使用。

`KWin` 有多种窗口装饰，包括默认的 `Oxygen`、类似微软 `Windows` 的 `Redmond` 以及 `Keramik`。只要安装了 `kdeartwork` 软件包，也可以使用 `IceWM` 主题。目前可用的后端包括 `XRender`、`OpenGL 1.x`、`OpenGL 2.x` 和 `OpenGL ES 2.x`。

## 辅助功能

- 命名 (`Name`)
- 反转 (`Invert`)
- 查看 (`Looker`)
- 跟踪 (`Track`)
- 缩放 (`Zoom`)

### 外观

- 渐入 (`Fade`)
- 渐淡出 (`Fade`)
- 滑动 (`Slide`)

### 窗口管理

- 登录 (`Login`)
- 魔法 (`Magic`)
- 鼠标 (`Mouse`)
- 翻转 (`Flip`)
- 呈现 (`Present`)
- 滑动 (`Slide`)
- 覆盖 (`Cover`)
- 翻转 (`Flip`)
- 是
- 是
- 是深度的一部分
- 它是 `KDE` 的不可或缺的一部分。

### KParts – 轻量进程内图像的框架

`KPart` 技术用于 `KDE` 以重用 `GUI` 组件。`KPart` 提供的优势是它带有预定义的工具栏操作。通过在应用程序中使用 `KPart`，开发者可以减少使用文本编辑器或命令行功能的时间（例如，使用 `kate` 代替它们）。`KPart` 还用于插件技术，以将应用程序嵌入到内部，例如将 `PIM` 应用集成到 `Contact` 中。

### XML GUI

`XML GUI` 是一个 `KDE` 框架，使用 `XML` 和动作（`action`）概念来设计用户交互应用程序。在这个框架中，编辑器设计其应用程序可以使用的操作，由编辑器在 `KDE` 框架中定义少数操作，例如打开文件或关闭应用程序。标题操作（`Caption action`）与各种数据关联，包括缩略图、标题和提示。

这种设计中一个令人兴奋的部分是，操作并不是由编辑器包含在菜单或工具栏中的。相反，编辑器提供一个 `XML` 文件来解释菜单栏和工具栏布局。通过使用该应用程序，用户可以重新排列用户界面而无需接触应用程序的代码。

此外，`XML GUI` 对 `KDE` 组件的 `KParts` 接口有用，因为应用程序可以轻松将其集成到自己的 `GUI` 中。`Konqueror` 是此功能的经典示例。

### Phonon – 多媒体框架

`Phonon` 是 `KDE` 提供的多媒体 `API`，也是管理 `KDE` 内流的标准，并被多个 `Qt` 应用使用。`Phonon` 创建是为了让 `KDE` 和 `Qt` 软件独立于任何单一的多媒体框架（如 `GStreamer` 或 `xine`），并为之前的版本提供稳定的 `API`。这样做有多个原因：构建 `KDE/Qt` 风格的多媒体 `API`、更好地支持 `Windows` 和 `macOS` 的原生多媒体框架，以及修复可能忽略或存在 `API/ABI` 不稳定的框架问题。

### KIO – 可扩展网络访问
