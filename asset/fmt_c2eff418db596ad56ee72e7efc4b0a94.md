
| 文件名 | 配置效果 |
| --- | --- |
| animate | 定义窗口或其他程序最小化时使用的动画设置或 |
| asroot | 配置 asroot 模块，该模块控制 AfterStep 的背景外观 |
| asmail | 配置应用程序小工具 asmail，用于高效处理邮件 |

# 表 8.1 续：AfterStep 配置文件

| 文件名 | 配置效果 |
| --- | --- |
| audio | 配置音频模块，以便您在特定操作中使用音效，或使用需要音频增强的插件模块 |
| autoexec | 定义 AfterStep 启动时自动加载的程序和模块 |
| base.xxbb | 定义模块、图形位图、光标图标和 AfterStep 文件的目录路径 |
| clean | 管理 Clean 模块，该模块在定义的空闲时间后自动关闭或最小化窗口 |
| compatibility | 决定启动 AfterStep 1.8 及更高版本时，是否使用程序早期版本的配置文件（即 `.steprc` 文件） |
| database | 定义各种应用程序的配置，包括它们的窗口行为和外观 |
| feel.name | 配置窗口管理器的感觉，包括窗口行为和其他机械功能（与下文的 look.name 配合使用） |
| forms | 包含 AfterStep 使用的表单信息 |
| ident | 定义 Ident 模块的变量，该模块控制每个打开窗口的基本信息 |
| look.name | 配置窗口管理器的外观，包括颜色和渐变阴影（与上述 feel.name 配合使用） |
| pager | 定义 Pager 模块的变量，用于显示各种虚拟桌面及其内容 |
| scroll | 定义 Scroll 模块的变量，该模块决定桌面上的单个窗口如何从上到下或从侧面滚动 |
| wharf | 定义 Wharf 模块的变量，包括停靠图标和其他插入桌面显示中的其他小工具 |
| winlist | 定义 WinList 模块的变量，显示所有打开窗口的信息 |
| zharf | 定义 Zharf 模块的变量，该模块是 Wharf 模块的文本版本 |

# WindowMaker

与 AfterStep 类似，WindowMaker 是基于 NeXT 显示的窗口管理器。图 8.5 所示的结果是一个整洁且易用的界面。WindowMaker 是 GNU 项目的产品，因此它是自由软件，并设计为可以与其他 GNU 程序良好地工作。我们在随书提供的 CD-ROM 中包含了 WindowMaker。WindowMaker 提供了一个复杂的菜单系统，带有可以拆卸的菜单，可以通过将其“固定”在桌面上来保留；WindowMaker 还有一个名为 Dock 的功能，其作用与 AfterStep Wharf 或 KDE 和 Gnome 面板相同。

WindowMaker 和 AfterStep 一样，不是可用的最快的窗口管理器，在使用方面也不是最小的，而且没有最华丽的功能。然而，它在所有这些组件之间取得了很好的平衡，对于那些想要全功能窗口管理器、但又不想要集成桌面带来的过人系统需求，且希望窗口管理器能够轻松处理多项任务而没有基础窗口管理器那种简陋外观的用户来说，它是一个很好的选择。WindowMaker 具有大量可配置的功能，而不会像 Enlightenment 有时那样出现配置过载的问题。

图 8.5：

WindowMaker 像 AfterStep 一样，基于 NeXT 显示，具有整洁简单的界面。

![](img/c297036e8ead34f32fa6046c0fa309ee_156_0.png)

在 WindowMaker 和 AfterStep 之间做出选择是困难的，因为这两个管理器看起来几乎相同。两者之间的主要区别是 WindowMaker 在其核心二进制文件中集成了比 AfterStep 的功能，不像 AfterStep 那样依赖模块。

# 配置 WindowMaker

WindowMaker 使用多文件系统而不是单文件（如 BlackBox 或 IceWM）。AfterStep 配置文件被分为若干较小文件，包含在主目录下的 `~/GNUStep/Library/AfterStep/` 目录中。要将这些文件放入您的主目录，请创建上述目录。然后，从 `/usr/local/share/afterstep` 目录拷贝系统配置并根据需要进行编辑。如果您在 `~/GNUStep/Library/AfterStep` 目录中有文件，则 AfterStep 将使用这些配置作为您账户的默认配置，无论系统管理员设置了系统默认值如何。

> 在 1.8 版本之前的旧版 AfterStep 使用名为 `.steprc` 的配置。如果您使用的是使用 `.steprc` 的 AfterStep 版本，我们建议您升级到最新版本（可在 http://www.afterstep.org 获取）。您会发现自 1.8 发布以来有许多变化，包括该配置处理方式的彻底改变。

共有 18个 AfterStep 配置文件，如表 8.1 所示。您可能永远不需要碰其中某些文件，也可能想对它们进行大量编辑。语法非常直观，每个条目以变量名开头，随后是该变量的特定定义。浏览您想要编辑的特定文件，查看文件中如何处理单个变量的示例。您可以在 AfterStep 手册页中找到每个配置文件的变量完整列表，通过在 shell 提示符输入 `man afterstep` 即可访问。注意，AfterStep 的页面非常长，但各个模块也有它们自己的手册。

# 表 8.1：AfterStep 配置文件

| 文件名 | 配置效果 |
| --- | --- |
| animate | 定义窗口或其他程序最小化时使用的动画设置或 |
| asroot | 配置 asroot 模块，该模块控制 AfterStep 的背景外观 |
| asmail | 配置应用程序小工具 asmail，用于高效处理邮件 |

# 表 8.1 续：AfterStep 配置文件

| 文件名 | 配置效果 |
| --- | --- |
| audio | 配置音频模块，以便您在特定操作中使用音效，或使用需要音频增强的插件模块 |
| autoexec | 定义 AfterStep 启动时自动加载的程序和模块 |
| base.xxbb | 定义模块、图形位图、光标图标和 AfterStep 文件的目录路径 |
| clean | 管理 Clean 模块，该模块在定义的空闲时间后自动关闭或最小化窗口 |
| compatibility | 决定启动 AfterStep 1.8 及更高版本时，是否使用程序早期版本的配置文件（即 `.steprc` 文件） |
| database | 定义各种应用程序的配置，包括它们的窗口行为和外观 |
| feel.name | 配置窗口管理器的感觉，包括窗口行为和其他机械功能（与下文的 look.name 配合使用） |
| forms | 包含 AfterStep 使用的表单信息 |
| ident | 定义 Ident 模块的变量，该模块控制每个打开窗口的基本信息 |
| look.name | 配置窗口管理器的外观，包括颜色和渐变阴影（与上述 feel.name 配合使用） |
| pager | 定义 Pager 模块的变量，用于显示各种虚拟桌面及其内容 |
| scroll | 定义 Scroll 模块的变量，该模块决定桌面上的单个窗口如何从上到下或从侧面滚动 |
| wharf | 定义 Wharf 模块的变量，包括停靠图标和其他插入桌面显示中的其他小工具 |
| winlist | 定义 WinList 模块的变量，显示所有打开窗口的信息 |
| zharf | 定义 Zharf 模块的变量，该模块是 Wharf 模块的文本版本 |

# WindowMaker

与 AfterStep 类似，WindowMaker 是基于 NeXT 显示的窗口管理器。图 8.5 所示的结果是一个整洁且易用的界面。WindowMaker 是 GNU 项目的产品，因此它是自由软件，并设计为可以与其他 GNU 程序良好地工作。我们在随书提供的 CD-ROM 中包含了 WindowMaker。WindowMaker 提供了一个复杂的菜单系统，带有可以拆卸的菜单，可以通过将其“固定”在桌面上来保留；WindowMaker 还有一个名为 Dock 的功能，其作用与 AfterStep Wharf 或 KDE 和 Gnome 面板相同。

WindowMaker 和 AfterStep 一样，不是可用的最快的窗口管理器，在使用方面也不是最小的，而且没有最华丽的功能。然而，它在所有这些组件之间取得了很好的平衡，对于那些想要全功能窗口管理器、但又不想要集成桌面带来的过人系统需求，且希望窗口管理器能够轻松处理多项任务而没有基础窗口管理器那种简陋外观的用户来说，它是一个很好的选择。WindowMakerMaker 具有大量可配置的功能，而不会像 Enlightenment 有时那样出现配置过载的问题。

图 8.5：

WindowMaker 像 AfterStep 一样，基于 NeXT 显示，具有整洁简单的界面。
