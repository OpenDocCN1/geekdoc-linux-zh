
在 Ubuntu 系统上：

![](img/3d310cc066dda6e2dfa67a650614076f_237_0.png)

在 Windows 系统上：

![](img/3d310cc066dda6e2dfa67a650614076f_237_1.png)

第一个按钮在 .qml 文件内部更新标签文本，另一个按钮则调用一个 C# 方法来更新文本标签。

这个简单的示例“qmlSimpleForm”可以作为基于 .NET Core 3 开发 QML.NET 表单应用程序的原型模板。它也是一个 QML 与 .NET Core C# 之间通信的良好示例（这非常有用了，不是吗）。

一如既往，该应用程序的源代码可以在 GitHub 上找到。

![](img/3d310cc066dda6e2dfa67a650614076f_238_0.png)

## 8.6.5.3 Photoshop GUI 应用程序

对于这个示例“photoshopQMLForm”，我们将回顾在 .NET Core 3 / QML.NET 项目中使用从 Adobe Photoshop 导出的 .qml 文件的方法（请查看有关 QML 文件导出器安装的相关章节）。此界面将包含设计好的 UI，包括自定义设计的按钮和图片。它实现了基本效果和动画的使用。

以下是开发此示例所遵循的基本流程：

- 1. 在 Photoshop 中设计 GUI（包含每个元素的各种状态）。
- 2. 从 Photoshop 导出 .qml 文件（在之前回顾的限制范围内）。
- 3. 修改和更新你的 .qml 文件以使其与你的应用程序兼容（使用 QT Design Studio）。
- 4. 将 .qml 文件导入你的 Visual Studio 2019 项目中。
- 5. 通过实现交互效果和动画来改进 .qml 代码（直接编写 .qml 文件代码或使用 QT Design Studio）。
- 6. 实现应用程序的后端 C# 代码（应用程序的实际处理部分）。

请注意，即使你的 .psd 文件（Photoshop 格式）包含时间轴，动画也不会从 Photoshop 导出。然而，图层上的效果过滤器会被正确导出，并包含在 .qml 文件中的单个对象里。

在界面开发过程中，你将在 QT Design Studio 内修改并测试所做的更改。QML 语言允许指定图形元素的行为以及元素之间的交互。

从 Photoshop 导出 .qml 文件将生成 QML 代码以及与图形设计对应的资源图像文件（.png）。

提示：如果你在 Photoshop 中更新了设计，请选择不导出 .qml 文件（在导出器选项中），否则所有关于效果和动画的工作将被新版本覆盖。

导出的 .qml 文件需要进行修改（在 QT Design Studio 中更容易操作），以包含应用程序所需的功能，你需要进行以下更新：

- 添加所需的依赖项（用于动画、效果、控件等）。
- 根据你的应用程序需求更改不同元素的容器。
- 检查并更新图层的位置（QML 导出器经常出错）。

以下是该 .qml 文件在用于我们的应用程序之前和之后的 QT Design Studio 视图

![](img/3d310cc066dda6e2dfa67a650614076f_240_0.png)

*(从 Photoshop 导出的原始 .qml 文件)*

![](img/3d310cc066dda6e2dfa67a650614076f_241_0.png)

*(可在项目中使用已修改的 .qml 文件。)*

从 Visual Studio 来看，该项目将具有明显的架构，包括主对象（此示例中只有一个表单）。GUI（QML）代码和你的应用程序逻辑（C#）是完全分离的，并有助于提高代码的良好可读性。

以下是该项目的“解决方案资源管理器”视图。

![](img/3d310cc066dda6e2dfa67a650614076f_242_0.png)

该应用程序包括在 QML 代码中使用动画和交互式更新，此应用程序中没有使用 C# 后端。“photoshopGUIForm”示例的目的是展示 QML 语言在动画和效果领域所能实现的功能。

这只是 QT 为实施动态图形界面所提供的功能的一瞥，但这个示例将帮助你熟悉 QML 语言及其在 .NET Core 3 应用程序中的使用。

以下是该应用程序在各个操作系统上运行的最终结果。

在 macOS 上：

![](img/3d310cc066dda6e2dfa67a650614076f_243_0.png)

在 Ubuntu 上：

![](img/3d310cc066dda6e2dfa67a650614076f_243_1.png)

**在 Windows 上：**

![](img/3d310cc066dda6e2dfa67a650614076f_244_0.png)

正如你所注意到的，应用程序在各个平台上渲染的效果是均一的。如果你的项目开发目标在于实现这一目标，使用 Photoshop 设计的 GUI 来构建 QML.NET 应用程序似乎是一个理想的选择。

该应用程序的源代码及相关的 .psd 文件可以在 GitHub 上找到。

> https://github.com/netcore3/CodeBook/Chapter 8/6/QML.photoshop

## 8.7 AVALONIA GUI 应用程序 (XAML)

这是在 .NET Core 3 多平台桌面应用程序中实现 GUI 的最后一种解决方案。由于它被视为 .NET Core 框架在实现 GUI 方面的逻辑扩展，因此它在 .NET 开发者社区中是最著名和最受欢迎的解决方案之一。

### 8.7.1 什么是 Avalonia？

Avalonia 是一个基于多平台 XAML 的 GUI 框架。它由三位独立开发者于 2015 年创建：Dan Walmsley、Nikita Tsukanov 和 Steven Kirk。

Avalonia 的灵感来源于微软的 XML 描述性界面语言 WPF，Avalonia 也由此得名，“Avalon” 是微软在 WPF 开发早期使用的代号。

Avalonia 提供 XAML 支持，但也包含来自 CSS 的功能用于界面样式设置。Avalonia 使用与其他 XAML 框架（如 WPF）类似的逻辑概念，但它支持广泛的操作系统，如 Windows、Linux、macOS、Android 和 iOS。

经过数年的 Alpha 和 Beta 版本测试，Avalonia 发布于 2019 年 4 月 5 日（当前版本为 2019 年 7 月的 0.81 版，包含一些错误修复）。

作为一个开源项目，当前开发版本的源代码可自由在 GitHub 上获取，Avalonia 目前采用 MIT 许可证。

![](img/3d310cc066dda6e2dfa67a650614076f_245_0.png)

参考网站提供了关于 API 的丰富文档，以及开发 Avalonia 应用程序的教程和快速入门指南。

![](img/3d310cc066dda6e2dfa67a650614076f_246_0.png)

除了框架本身，Avalonia 还提供了一系列工具以利于顺畅的应用开发，例如**Visual Studio 2019 扩展**，它提供了多个模板和 IDE 扩展，用于开发 Avalonia 应用程序。

其他一些有用的开源工具也可以使用，如**“Avalonia Design Studio”**（专用的 Avalonia IDE）和**“Avalonia Themes Designer”**（用于定义新的主题方案）。

### 8.7.2 Avalonia Visual Studio 扩展

Visual Studio 2019 的 Avalonia 扩展在 Visual Studio 市场上可用（当然也可以在 Visual Studio 内部通过菜单 工具/扩展 获取），你可以在下方找到下载 .vsix 文件（Visual Studio 扩展安装程序类型）的链接。

![](img/3d310cc066dda6e2dfa67a650614076f_246_1.png)

此扩展提供了多个项目模板（2 个）用于创建 Avalonia 应用程序，它还展示了 Avalonia XAML 的预览器。该扩展还提供了项目模板，用于创建新的表单。

以下是安装 Avalonia 扩展后新建项目窗口的副本。

![](img/3d310cc066dda6e2dfa67a650614076f_247_0.png)

在此屏幕中，你可以找到两种新的 Avalonia 应用程序类型：

- Avalonia MVVM (Model-View-ViewModel) 应用程序。
- Avalonia 客户端应用程序（经典架构）。

你可以在网站上找到使用这些模板创建 Avalonia 项目的详细教程。

