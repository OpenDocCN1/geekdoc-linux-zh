

# 第二部分：面向桌面用户的 Ubuntu

...系统。关于 Eclipse 的更多信息，请参阅本章中关于 IDE 讨论的其余部分或访问 Eclipse 主页 www.eclipse.org。

-   KDevelop：一个基于 KDE 桌面环境的 C 和 C++ 应用程序图形化 IDE。KDevelop 是一款非常流行且易于使用的 IDE，它提供了向导功能，可以简化标准命令行 Linux 应用程序的创建，也可以创建使用 Qt、GNOME 和 KDE 图形环境的图形化应用程序。有关 KDevelop 的更多信息，请访问其官方主页 www.kdevelop.org。
-   Motor：motor IDE 是一个用于 C、C++ 和 Java 应用程序的文本集成开发环境，可以在任何典型的应用程序（如 xterm 或 Gnome Terminal）中良好运行。motor IDE 对各种 GCC 编译器和 GNU 调试器 gdb 的集成支持。有关 Motor 的更详细信息，请访问其官方主页 http://konst.org/motor。
-   NetBeans：NetBeans IDE 是一个用于开发 Java、C++ 和 Ruby 等语言应用程序的完整 IDE。它用 Java 编写，支持包括 Microsoft Windows、Linux、Mac OS X 和 Solaris 在内的许多平台，因此是 Eclipse 跨平台 IDE 替代品的良好选择。关于 NetBeans 的更详细信息，请访问其官方主页 http://netbeans.org。
-   Pida：Pida（Python Integrated Development Application）是一个基于 GTK 的 IDE，用于用 Python 脚本语言开发文本模式或图形化应用程序。Pida IDE 非常流行，并支持在其统一框架内轻松集成熟悉的工具。有关 Pida 的更多信息，请访问其官方主页 http://pida.co.uk。
-   SBCL：SBCL（Steel Bank Common Lisp）是一个用于 Lisp 编程语言应用程序的图形化开发环境。SBCL IDE 最初基于卡内基·梅隆大学 CMU Common Lisp 提供的 Common Lisp 环境，该环境目前正在积极维护和增强。SBCL 提供了原生 Lisp 编译器和复杂的调试器。有关 SBCL 的更多信息，请访问其官方主页 http://source.forge.org。

此列表是 Ubuntu 仓库中可用 IDE 的子集，它突出了许多种不同的 IDE，以及许多 IDE 专注于特定编程语言的事实。我最喜欢的 IDE 是 Eclipse IDE，它最初由 IBM 开发，作为一个易于扩展的 Java 开发框架，后由 IBM 开源发布，并自那时起人气飙升。Eclipse 现在由 Eclipse 基金（www.eclipse.org）发布和支持，该基金是一个致力于推广 Eclipse 并引导其在整个软件开发行业中开发和被接受的非营利组织。Eclipse 提供了一个插件框架，可以轻松地创建、集成和支持提供特定功能或针对某些开发者的工具。这让开发者能够自由地从不同项目或商业供应商处选择并集成插件，从而组装出一个完全符合他们需求的 IDE。Eclipse 适用于 Linux、HP-UX、AIX、Solaris、QNX、Mac OS X 和 Microsoft Windows 系统。

# 第 23 章：在 Ubuntu 上进行软件开发

正如你可能从上一段猜测的那样，本章的其余部分将集中在安装和使用 Eclipse IDE。

# 安装 Eclipse

要安装 Eclipse 及相关包，请使用你喜喜欢的软件安装工具安装 `eclipse` 软件包。该包会安装大量的关联/所需包，并提供使用标准 Eclipse IDE 开发 Java 应用程序所需的一切，包括用于 Java 和 Python 开发的插件、用于构建 Java 应用程序的 ant 实用程序、所有所需的库等。

有关在 Ubuntu 系统上安装应用程序的详细信息，请参阅第 19 章。

# 注意

如果你在使用 Ubuntu 仓库提供的 Eclipse 版本安装或使用插件和功能时遇到问题，你可以随时使用喜喜欢的包管理工具删除 `eclipse` 包，然后从 eclipse.org 网站下载并安装“官方”版本的 Eclipse（www.eclipse.org/downloads）。Eclipse 为 Java EE 开发者、C/C++ 开发者等提供了预先配置好的版本。从 Eclipse 网站下载归档文件并解压内容后，你可以通过执行解压目录中的 "eclipse" 文件来运行下载的 Eclipse 版本。如果你使用这种方法（我经常经常用这种方法来获取最新版本的 Eclipse），你将无法通过标准的 Ubuntu 更新管理器获取 Eclipse 的更新，但你可以通过“检查更新”（Check for Updates）菜单项来保持版本为最新。对于你下载并安装的版本，你可能可能仍然想要启用并安装额外的 Eclipse 功能。

# 使用 Eclipse 进行 C 应用程序开发

本节提供了两个使用 Eclipse 的示例：一个展示了如何从零开始创建一个简单的应用程序，另一个展示了如何将现有软件包的源代码导入 Eclipse，以利用其编译、调试和易用性功能。关于使用 Eclipse 的完整书籍，这些介绍性章节还无法与之相比，但它们应该帮助你对 Eclipse IDE 的强大、能力和易用性有一个初步的感觉。

# 注意

接下来两个节中的示例都是程序，因此假设你已经遵循了“安装 GCC 编译器、make 及其他”部分中的说明，并安装了 `build-essential` 软件包，该包提供了构建 C 应用程序通常所需的用户空间头文件。

# 启动 Eclipse

在你的 Ubuntu 系统上安装 Eclipse 会创建一个“应用程序编程 Eclipse”菜单项，你可以选择它来启动 Eclipse IDE。

第一次启动 Eclipse 时，Eclipse 会显示一个对话框，提示你选择创建一个工作空间（workspace）的位置，然后在指定位置（通常是你的主目录）创建工作空间和 eclipse 目录。

# 第二部分：面向桌面用户的 Ubuntu

# 提示

如果你想使用不同的工作空间，只需点击 `File > Switch`。

# Eclipse 界面

第一次启动 Eclipse 时，Eclipse 会显示一个对话框，提示你选择创建一个工作空间的位置，然后在指定位置创建工作空间和 eclipse 目录（通常是你的主目录）。

# 工作空间

第一次启动 Eclipse 时，Eclipse 会显示一个对话框，提示你选择创建一个工作空间的位置，然后在指定位置创建工作空间和 eclipse 目录（通常是你的主目录）。

# Eclipse 界面

一旦 Eclipse 运行，你将看到界面。界面如图所示：

Eclipse 界面由几个部分组成，每个部分都有其用途：

-   **菜单栏（Menu bar）**：位于窗口顶部，包含选项。
-   **工具栏（Toolbar）**：位于菜单栏下方，提供了常用的命令。
-   **资源管理器（Project Explorer）**：通常位于左侧，显示项目和文件。
-   **编辑器（Editor）**：这是编写和编辑代码的主区域。
-   **控制台（Console）**：通常位于窗口底部，显示输出。
-   **状态栏（Status bar）**：位于窗口最底部，显示信息。

Eclipse 的布局是可以自定义的。你可以拖动视图来调整布局。如果你想重置布局，可以 `Window > Reset Perspective`。

# Eclipse 术语

对于熟悉其他 IDE 的人来说，这些术语应该不会感到很意外。以下是你在使用 Eclipse 时会遇到的几个术语：

-   **编辑器（editor）**：允许编辑特定类型文件或资源的窗口。Eclipse 的工具栏根据激活的编辑器提供不同的选项。
-   **功能（feature）**：一组一个或多个插件的集合，实现特定的。
-   **透视图（perspective）**： 界面内与特定插件关联的一组窗口，这些窗口按任务组织。
-   **插件（plugin）**：执行特定功能或一组功能的代码，可以集成到特定的。
-   **视图（view）**：标题栏内的窗口，可以支持编辑器或提供特定类型资源的访问。每个视图都有自己的菜单和图标，可以通过右键点击或选择标题栏中的图标。
-   **工作台（workbench）**：Eclipse 提供的两个关键插件之一，工作台插件提供了基础的用户界面、菜单结构、事件通知机制以及创建新窗口和视图的机制。该插件扩展了开发者可以创建菜单、菜单项、编辑器和视图。从用户的角度来看，工作台就是用户界面。
-   **工作空间（workspace）**：Eclipse 提供的两个关键插件之一，工作空间插件允许你与外部资源进行交互，如项目目录、文件等。工作空间这一术语也可能用于描述持有项目。

这些是对官方 术语的解释。Eclipse 的在线帮助在其“工作台用户指南”部分提供了这些术语的官方定义。

