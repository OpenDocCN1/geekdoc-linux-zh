
助手客户端库允许你远程控制 Qt 助手应用程序。这允许你将助手作为应用程序的跨平台帮助浏览器。该模块的核心是 `QAssistantClient` 类。

用于 Qt 的自定义帮助页面以基础 HTML 标记提供，并附带一个描述文档结构的 XML 文件。

## 测试用例库 QtTestLib

TestLib 最初在核心发行版之外面向付费客户发布，从 Qt 4.1.0 开始进入常规 Qt 发行版。该库包含了为新写的类编写适当测试的设施，其范围与 Java 中的 JUnit 类似。

> 12 参见 http://www.w3.org/TR/SVGMobile.

## QtDbus 库

DBus 是一种消息协议，已成为 Linux 及其他 Unix 衍生系统上的事实标准。例如，Linux 硬件抽象层（HAL）以及即将推出的 KDE 4 使用 DBus 进行进程间通信。尽管存在 Windows 和 Mac OS X 的端口，但 Qt 4.2 将仅在 Unix 上构建此库。不过，这在未来的版本中可能会发生变化。

## ActiveQt 与迁移类

针对 Windows 的平台特定扩展 ActiveQt 使得实现 ActiveX 组件并在 Qt 程序中使用它们成为可能。它在商业版 Qt 桌面版可用。

Trolltech 还为基于 MFC、Motif 和 Xt 的应用程序提供了迁移解决方案。然而，与 ActiveQt 一样，它们仅作为 Qt 4 的独立商业附加组件（Qt Solutions）提供，不会在书中讨论。

## 1.5.2 工具与实用程序

此外，Qt 还包含了三个 GUI 程序，可以用于显示 Qt 文档、根据所见即所得（WYSIWYG）原则创建对话框，或将程序翻译成其他语言。工具包还提供了一系列命令行程序用于执行各种任务。

## 文档浏览器 "Qt Assistant"

Qt 文档由简单的 HTML 文件组成，可以使用任何网络浏览器或助手查看。与网络浏览器不同，助手显示整个 Qt 文档的索引，并允许对此类文档进行全文搜索（图 1.10）。

助手的关键字目录在日常使用 Qt 时特别有用。例如，如果你需要某个类的文档（例如 `QLabel`），只需在索引输入框中输入 `qlabel` 即可。按下回车键，你将立即进入该优质文档。

> 13 参见 http://www.trolltech.com/products/solutions/

## 基础、工具与第一个代码

图 1.10：

Qt Assistant 显示文档。

![](img/b663c93885d7333a091a433460ee647f_49_0.png)

助手是本书的一个重要补充，因为它不仅记录了新添加的 API 调用（或由于某种原因未讨论的），还提供了额外的示例。

## GUI 编辑器 "Qt Designer"

Qt Designer 允许你创建对话框和布局，这在创建复杂的 UI 时非常有用。它可以使用 HTML 标记创建所见即所得的界面（图 1.11）。你可以通过拖拽在 Designer 中添加小部件并设置它们的属性。例如，你可以更改 `QLabel` 的文本或颜色。

Designer 的预览模式允许你查看布局的变化。Designer 还具有一种模式可以指定小部件的顺序；即用户通过反复按 Tab 键访问小部件的顺序。这是用户界面的一个重要方面，也是你应该检查的。

> 14 对于偏好在网络浏览器中阅读的人，可以在 Trolltech 网站找到 Qt 类文档。

## 1.5 Qt 概览

顺序是合理的。注意，如果你不自己设置，Qt 会自动设置，这可能并不总是会导致理想的结果。

![](img/b663c93885d7333a091a433460ee647f_50_0.png)

图 1.11：

作为顶层窗口的 Designer 工具

# 基础、工具与第一行代码

这些内容以不同语言的对应项显示给用户。`locate` 从程序的源代码中提取需要本地化的文本，并根据项目文件的定义生成翻译文件：

```
TRANSLATIONS = application_fr.ts \
application_nl.ts
```

在翻译（即编辑）通过这种方式生成的翻译文件时，GUI Linguist 作为一个图形化实用程序（图 1.12）。`Release` 创建包含翻译内容的额外二进制文件，应用程序会在请求时在启动时加载这些文件，从而显示为已翻译的状态。通过这种方式使用 Linguist 和 Release，无需重写和重新编译应用程序代码即可生成支持另一种语言的发布版本。

为了完成这些工作，应用程序的源代码必须遵循某些约定。具体来说，表示待翻译文本的字符串必须传递给 `QObject::tr()` 或 `QApplication::translate()` 函数。这实现了两点：

- 允许 Qt 动态更改字符串。如果你在源代码中指定字符串 "Hello, world!"，那么在应用程序运行时将只使用这个字符串。但如果你通过 `QObject::tr()` 或 `QApplication` 类的 `translate()` 函数选择第一个字符串，该函数将锁定该翻译并返回一个包含该内容的字符串，该字符串将取代原始的 "Hello, world!"。

- 允许更新工具查找此类函数，并识别源代码中待翻译的更改。

图 1.12：Qt Linguist 允许将应用程序翻译成其他语言。

![](img/b663c93885d7333a091a433460ee647f_51_0.png)

遗憾的是，第 1 节中简单的 "Hello, world!" 程序无法翻译成其他语言，因为我们对字符串 "Hello, world!" 既没有使用 `tr()` 也没有使用 `translate()`。为了弥补这一缺陷，我们将行

```
QLabel label("Hello, world!");
```

替换为：

```
QLabel label(QApplication::translate("MyLabel", "Hello, world!"));
```

`QApplication::translate()` 函数第一个参数是文本的上下文标签，而 `QObject::tr()` 函数自动使用涉及部件的类名作为上下文标签¹⁵。例如，如果你对 `QLabel` 对象调用 `tr()`，Qt 会自动使用上下文名称 `QLabel`。这是可能的因为 `QLabel` 派生自基类 `QObject`，因此继承了 `tr()`。

上下文标签非常重要，因为相同的文本可能出现在多个地方，且具有不同的含义。如果目标语言对这些变化使用不同的术语，则原始文本实例的适当翻译将取决于上下文。例如，英语 Qt 对象可能出现在一个对话框中，具有 *open*（打开）的含义，但在另一个对话框中具有 *open connection*（建立连接）的含义；德语版本的程序将第一个实例渲染为 *Öffen*，将第二个渲染为 *Aufbauen*。当两个实例具有不同的上下文标签时，Qt 就能区分它们。

你应该通过 `tr()` 或 `translate()` 函数发送程序中的所有文本。你会发现，在代码开发期间，程序通常可以没有太大困难地翻译，而一旦编码完成，遍历整个大型程序的源代码并添加 `tr()` 或 `translate()` 调用将是非常繁琐的。本书其余部分的示例程序将从一开始就使用 `tr()`。

（你将在第 14 节中找到有关国际化和本地化的详情。）

# 创建项目

如第 1.1.1 节所示，`qmake` 为独立于平台的项目文件创建特定平台的 Makefile。存储在 Makefile（或 `nmake`）中的规则用于编译和链接应用程序。然而，`nmake`、`make` 仅适用于商业 Qt 版本，不适用于开源版本¹⁶。GPL 变体

- ¹⁵ 参见第 380 页。

- ¹⁶ 无论是否包含来自 Visual Studio 的库，Visual Studio 的 EULA 与 GPL 都不兼容。（等等，原文写的是 "anyway"，可能可能是 "even if"，但根据指令保留原词）。

# 基础、工具与第一行代码

Windows 版的 Qt 4 使用 GCC MinGW，它提供了来自 Linux 的已知 GNU make 而不是 `nmake`。

`qmake` 项目文件不需要我们担心编译器或链接器选项。因此，我们将在书中的所有示例重中使用 `qmake`。

在 Windows 中，如果你拥有商业 Qt 许可证，还可以使用 `qmake` 为 Microsoft Visual Studio 创建项目文件。（Qt 集成在免费版 Visual Studio Express 中不起作用；这些用户也依赖于基于命令行的版本 `qmake`。）

图 1.13：Code::Blocks 构建的

我们的 "Hello, world!" 程序。

![](img/b663c93885d7333a091a433460ee647f_53_0.png)

对于 Windows 中的开源开发者，开发环境 Code::Blocks¹⁷ 提供了一个实用的替代方案。它与 Qt 中的 MinGW 配合工作，并有一个针对 Qt 4 项目的模板。为了让它与 `qmake` 配合工作，你必须先停止它生成 Makefile。要做到这一点，选择 Project→Properties 并勾选选项 This is a custom Makefile。然后查找 Project→Build options 下的对话框并激活 Commands 选项卡。然后，在 Pre-build steps 字段中输入以下命令：

```
qmake -project
qmake
make.bat
```

> 17 参见 http://www.codeblocks.org。

## 1.5 Qt 概览

为了确保即使在其他程序（如 Qt Designer）运行时调用 `make`，请选择 Always execute 以保持最新的。图 1.13 显示了 "Hello, world!" 编译后的程序。

在 Designer 菜单中，这对于启动很有用。你也可以使用此项来快速启动你的程序，在 Tools 菜单中选择 Configure...

![](img/b663c93885d7333a091a433460ee647f_54_0.png)

图 1.14：Apple 的 Xcode IDE 实现了高效的项目管理，qmake 生成必要的文件。

在 Mac OS 上，首选开发环境是 Xcode IDE。Apple 免费提供此软件 OS X 10.3 (Panther)，但需要安装。qmake 在 Mac 上生成 Xcode 项目。然而，如果你避免 Xcode 并依赖命令行工具，只需附加 -spec macx-g 来生成 Makefile：

```
qmake -spec macx-g
```

相比之下，

```
qmake -spec macx-g
```

将导致 qmake 为所有版本生成 Xcode 项目。在 Linux 下创建应用程序时，开发环境 KDE¹⁸可能是最佳选择。3.4 版本支持 Qt 4。KDevelop 包含了模板以及用于 qmake 项目文件的图形化管理工具，它们可以无缝集成到 IDE 中。

> 18 参见 http://www.kdevelop.org。

首次启动时，KDevelop 将呈现一个几乎空白的主窗口。选择 Project→New Project 将启动向导，引导完成创建项目的初始步骤。要创建一个使用 qmake 的 Qt 4 项目，如图 1.15 所示，从树视图中选择 C++→CMake→Basic Qt application。在第一步，向导还需要应用程序名称以及一个存储所有文件的目录。

下一步中，KDevelop 询问默认作者名称、初始版本号和项目许可证。在此步骤中指定 Qt 4 版本 qmake 和 designer 的完整路径也很重要。这确保了程序不会意外选择 Qt 3 版本。下一步允许你选择源代码目录。如果你没有使用源代码管理系统，只需保持默认的 None。剩余步骤用于自定义插入到所有头文件和实现文件中的模板。这些文件通常包含许可证以及作者姓名。图 1.16 显示了向导完成后示例 main.cpp 文件的窗口。

按下 Shift+F9 将构建并执行项目；文本输出位于底部的“消息”（Messages）和“应用程序”（Application）选项卡中，它们分别会在构建和执行阶段自动打开。

## 1.5 Qt 概览

![](img/b663c93885d7333a091a433460ee647f_56_0.png)

图 1.16: 设置后的 KDE 编译窗口

![](img/b663c93885d7333a091a433460ee647f_56_1.png)

qmake-project管理器 QMake 管理器隐藏在右侧带有 Qt 符号的选项卡后面。展开后，你可以使用它图形化地添加、移动或打开文件。项目管理器将不同类型的源文件分开：Ddevelop 为普通源文件打开一个新标签页，而文件将自动用 Qt Designer 启动。

图 1.17: KDE 编辑器可以转换为强大的源代码编辑器。

对于不喜欢全屏 IDE（KDE 高级文本编辑器）的人来说，这是一个很好的替代方案，它包含一个下拉菜单，你可以通过该菜单直接运行编译器，如图 1.17 所示。根据你的发行版版本，你可能需要先安装 `kate-plugins` 包，该包（以及其他插件）至少提供了一个代码补全插件。通过这种配置，Kate 可以提供 C 和 C++ 文件中方法和成员变量的概述，甚至允许在“设置→配置 Kate→应用程序→插件”下进行代码段管理。

Kate 的设置对话框提供了一个子项“外部工具”（External Tools），你可以在其中存储你自己的命令，这与 Code::Blocks 一样，这些命令会出现在“工具→外部工具”下。“设置→配置快捷键”列出了键盘快捷键。

## 元对象编译器 moc

Qt 中的信号/槽概念并非纯 C++，而是 C++ 标准的扩展，为此需要使用命令行程序 moc（**元对象编译器**）来将信号和槽的结构转换为标准的 C++。moc 会为每个派自 `QObject` 的类生成额外的 C++ 代码。这确保了信号/槽可以在运行时动态生成。它还允许使用 `QObject` 作为基类的类名称在运行时动态确定，甚至可以确定一个类是否是另一个类的基类¹¹⁹

Qt 还包含一个属性系统，moc 为此生成必要的代码。属性是类的特殊特征，可以进行查询和设置。例如，`QLabel` 类有一个 `text` 属性，其值是一个包含标签显示文本的字符串。对于每个属性，有两个函数：一个返回其当前值（也称为 get 方法），另一个更改它（也称为 set 方法）。在 `QLabel` 的情况下，`text()` 是返回标签文本的 get 方法，而 `setText()` 是为标签新文本的 set 方法。这两个函数在类定义中被标记为属性，允许通过 `QObject::property()` 查询文本并通过 `QObject::setProperty()` 设置文本。这两者都需要一个字符串（即属性名称）作为参数。Designer 的**属性编辑器**（**Property Editor**）决定了属性在运行时的值，并允许更改这些属性。如果你在单独的类中需要属性，它们必须派自 `QObject`。

简而言之，每当类使用 `QObject` 作为基类时，就需要 moc。元对象编译器在运行 C++ 编译器之前，必须预处理每个实现此类类定义的每个文件。在每情况下，它都会创建一个以 `moc` 为前缀的文件。

例如，如果你编写了一个以 `QObject` 为基类的自定义对话框 `MyDialog`，类定义在 `MyDialog.h` 中，实际实现在 `MyDialog.cpp` 中，元对象编译器必须处理 `MyDialog.h`，然后生成 `moc_MyDialog.cpp` 文件，并将生成的文件集成到完整项目中。`qmake` 会自动完成这一切。

> ¹¹⁹ 我们所说的基类不仅是指派生它的类。
