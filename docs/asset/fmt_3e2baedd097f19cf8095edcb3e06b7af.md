
- KDevelop：一个用于 C 和 C++ 应用程序的图形 IDE，基于 KDE 桌面环境。KDevelop 是一个非常流行且易于使用的 IDE，它提供了向导，可以简单地创建标准的命令行 Linux 应用程序，以及使用 Qt、GNOME 和 KDE 图形环境的图形应用程序。关于 KDevelop 的更多信息，请访问其主页 www.kdevelop.org。

- Motor：motor IDE 是一个用于 C、C++ 和 Java 应用程序的文本集成开发环境，可以在任何终端以及 xterm 或 Gnome Terminal 中良好运行。motor IDE 支持各种 GCC 编译器和 GNU 调试器。关于 Motor 的更详细信息，请访问其主页 http://konst.org/motor/。

- NetBeans：NetBeans IDE 是一个用于开发 C、C++ 和 Ruby 等语言应用程序的代码 IDE。因为它是用 Java 编写的，它可以运行在 Windows、Linux、Mac OS 和 Solaris 等多个平台上，因此是 Eclipse 的跨平台 IDE 替代的良好选择。关于 NetBeans 的更多信息，请访问其主页 http://netbeans.org。

- Pida：Pida (Python Integrated Development Application) IDE 是一个基于 GTK 的 IDE，用于用 Python 脚本语言开发文本或图形应用程序。Pida IDE 非常流行，并支持在其统一框架内轻松集成开发工具。关于 Pida 的更多信息，请访问其主页 http://pida.co.uk。

- SBCL：SBCL (Steel Bank Common Lisp) IDE 是一个用 Lisp 编程语言编写的应用程序的图形开发环境。SBCL IDE 最初基于 Carnegie Mellon大学 CMU Common Lisp 提供的 Common Lisp 开发环境，但现在正被活跃地维护和增强。SBCL IDE 特具有原生 Lisp 编译器和复杂的调试器。关于 SBCL 的更多信息，请访问其主页 http://sbcl.sourceforge.net。

此列表是 Ubuntu 仓库可用 IDE 的子集，但它突出了许多不同的 IDE，以及许多 IDE 专注于特定开发语言的事实。我最喜欢 Eclipse IDE，它最初由 IBM 开发作为 Java 开发的扩展框架，后来作为开源发布，并从那时获得了流行。Eclipse 现在由 Eclipse Foundation (www.eclipse.org) 发布和支持，这是一个非营利组织，致力于推广 Eclipse 并帮助其在整个软件开发行业的发展和接受。Eclipse 提供了一个基于插件的框架，易于创建、集成和支持提供特定功能或针对特定开发者的工具。这种插件模型还赋予了开发者自由，让他们选择并集成来自不同项目或商业供应商的插件，并组装完全符合他们需要的 IDE。Eclipse 适用于 Linux、HP-UX、AIX、Solaris、QNX、Mac OS X 和 Microsoft Windows 系统。

## 第23 章：在 Ubuntu 上进行软件开发

正如你从上一段推测的，本章的其余部分将关注安装和使用 Eclipse IDE。

## 安装 Eclipse

要安装 Eclipse 及相关包，请使用你喜欢的软件安装工具安装 `eclipse` 包。该包会安装大量的关联/所需包，并提供使用标准 Eclipse IDE 开发 Java 应用程序、Java 和 Python 开发插件、构建 Java 库的 ant 工具等所需的一切。

有关在 Ubuntu 系统上安装应用程序的详细信息，请参阅第 19 章。

### 注意

如果你在使用或安装 Ubuntu 仓库提供的版本 Eclipse 中的插件和功能时遇到问题，可以使用你喜欢的包管理工具删除 `eclipse` 软件包，然后从网站（www.eclipse.org/downloads）下载“官方”版本的 Eclipse。Eclipse 网站为 Java 开发、C/C++ 开发者等人员提供了预配置的 Eclipse 版本。如果你从 Eclipse 网站下载了归档 tar 文件并解压其内容，可以通过执行目录中名为“eclipse”的文件来运行下载的 Eclipse。你将无法通过标准的 Ubuntu 更新管理器获取 Eclipse 的更新，但可以使用 `Help -> Check for updates`（帮助 -> 检查更新）项保持这些版本的更新。根据你下载的版本，你可能仍然想要启用并安装额外的 Eclipse 功能。

## 使用 Eclipse 开发 C 应用程序

本节提供了两个使用 Eclipse 的示例：一个显示了如何从头创建一个简单的应用程序，另一个显示了如何将现有软件包的源代码导入 Eclipse，以利用其编译、调试和易用性功能。关于使用 Eclipse 有大量的书籍，这些介绍性章节与它们不等同，但它们应该能让你对 Eclipse IDE 的强大、功能和易用产生感觉。

### 注意

接下来两个章节中的示例都是 C 程序，因此假设你遵循了“安装 GCC 编译器及其工具”中的指令并安装了 `build-essential` 包，该包提供了构建 C 应用程序所需的用户空间头文件。

## 启动 Eclipse

在 Ubuntu 系统上安装 Eclipse 会创建“应用程序 -> 开发 -> Eclipse”菜单项，你可以选择它来启动 Eclipse IDE。

第一次启动 Eclipse 时，Eclipse 会显示一个对话框，提示你创建一个工作空间的位置，然后在指定位置（通常是你的主目录）创建工作空间和 `.eclipse` 目录。除非你有充分理由使用其他位置，否则接受默认建议并勾选“将此作为默认且不再询问”复选框，这样你就再也不需要担心这个问题。

### 提示

Eclipse 使用工作空间目录存储你创建的项目，并使用 `.eclipse` 目录存储你的配置设置、最后一次使用 Eclipse UI 的信息、已安装的功能等。你可以通过 `--data` 命令行参数后跟要使用的工作空间目录完整路径，使用不同的工作空间目录启动 Eclipse。

在创建这些目录并加载初始执行环境后，Eclipse 会显示欢迎屏幕，其中包含几个奇怪的图形对象，但没有任何类似于代码开发工具。

此欢迎屏幕上的图形对象实际上是使用 Eclipse 的信息源链接，例如教程、示例代码，只需点击欢迎标签中的 X 即可。你可以通过选择 `Help ➔ Welcome`（帮助 -> 欢迎）随时重新打开它。

关闭欢迎屏幕后，将显示标准的 Eclipse 用户界面，如图 23-1 所示。

此时，Eclipse 环境非常，因为你还没有创建任何项目。接下来的几节将解释如何解决这个问题。

图 23-1

标准的 Eclipse 用户界面

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_867_0.png)

## Eclipse 术语

Eclipse 框架最初由 IBM 开发，它似乎开发了一套自己的语言来指代 Eclipse 用户界面和框架的元素。对于过去与 IBM 一过工作的人来说，这并不意外。以下是你在使用 Eclipse 时会遇到的一些术语——和大多数语言一样，一旦你吸收了它们，就能完全理解，但起初可能会令人困惑：

- **editor（编辑器）**：允许你编辑特定类型文件或其他资源的窗口。Eclipse 工具栏和菜单根据当前活动的编辑器提供不同的选项。

- **feature（功能）**：一个或多个插件的封装包，有助于构建产品。

- **perspective（视角）**：Eclipse GUI 内的一组窗口，与特定插件或任务关联并按特定方式组织。

- **plugin（插件）**：执行特定功能或一组功能并可以集成到 Eclipse 框架中的代码。

- **view（视图）**：Eclipse GUI 内部的窗口，可以支持或访问特定类型的资源。每个视图都有一个标题栏，带有标签以选择在视图中打开的不同资源，并且通常提供自己的菜单，可以通过右键单击或选择标题栏中的图标来使用。

- **workbench（工作台）**：Eclipse IDE 提供的两个关键插件之一，workbench 插件提供了基本的用户界面、菜单结构、事件通知以及创建新窗口和视图的机制。该插件还提供了开发者可以用于为其插件创建菜单、菜单项、编辑器和视图的扩展点。从用户的角度来看，工作台就是 Eclipse 用户界面。

- **workspace（工作空间）**：Eclipse IDE 提供的第二个关键插件，workspace 插件允许你与外部资源（如项目目录、文件等）进行交互。“工作空间”一词也可以用于描述 Eclipse 用于存放项目的目录。

这些是我对 Eclipse 官方术语的解释。Eclipse 的在线帮助在其“工作台用户指南”部分提供了这些术语的官方定义。

## 获取附加组件和更新
