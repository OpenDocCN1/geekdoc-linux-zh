

## (Adobe Photoshop 导出至 QML)

你可以在包含于 `.zip` 文件中的 readme 文件（“qt-labs-photoshop-qmlxporter-cs6.zip”）中找到有关 `.qml` 文件导出选项的所有详细信息。

以下是从 Photoshop 导出文件时你应该看到的界面：

![](img/3d310cc066dda6e2dfa67a650614076f_227_0.png)

![](img/3d310cc066dda6e2dfa67a650614076f_227_1.png)

### (QML 导出扩展：导出选项)

通过此表单，你可以配置想要进行的导出类型（我们将在示例章节中说明每个选项的用途）。

导出过程受限于关于 Photoshop 文档中图层和文件夹的若干规则：

-   Photoshop 文档（.psd 文件）中的每个文件夹都将作为单个对象（一张图像）导出。
-   文件夹中的隐藏图层将完全不被导出。
-   文件夹的内容将按照其在 Photoshop 中显示的方式导出。
-   文件夹中的文本元素将被渲染（栅格化）。
-   导出过程中将尊重图层堆叠顺序。
-   Photoshop 文档（.psd 文件）中的文件夹层级结构在导出过程中将不会被保留。
-   你必须为设计中的每个图层指定一个名称。

为了亲身体验导出插件的功能和限制，你应在多种配置下对其进行测试，并使用 QT Design Studio（或根据你所遵循的方法论使用文本编辑器）验证生成的 .qml 文件。

## 8.6.5 使用 QML.NET 的示例程序 GUI

在本节关于使用 QML.NET 开发基于 .NET Core 3 的多平台应用程序中，我们将回顾三种不同类型的示例项目，以说明几种方法。

-   第一个示例来自 QML.NET 作者的 GitHub 仓库，已更新为使用 .NET Core 3（并进行了略微修改）。
-   第二个示例使用 QT Design Studio 设计的 GUI，采用标准的 QT Quick 控件。
-   第三个示例使用从 Photoshop 设计和导出的 GUI（使用前面描述的 QML Exporter 脚本）。

你可能已经注意到，我们尚未涉及和回顾 QT 运行时的设置过程（例如用于 GTK 开发的设置），这是因为在使用 QML.NET 开发时不需要这样做。

实际上，QML.NET 封装器的专用指令会检查所需 QT 运行时的存在性，并在必要时自动下载/安装它，无需用户进行任何干预（这几乎像魔法一样）。

因此，在 .NET Core 3 应用程序中使用 QT 运行时的唯一要求是在 C# 源代码中包含以下指令。

```csharp
RuntimeManager.DiscoverOrDownloadSuitableQtRuntime();
```

与旧方法相比，这种将运行时无缝集成到 .NET Core 3 程序中的方式对于需要部署基于 QML 的应用程序的 QT 运行时设置来说，绝对是开发者的一大福音。

### 8.6.5.1 QML.NET 示例应用程序

第一个示例应用程序由 Paul Knopf 开发，他是 QML.NET 框架的主要开发者之一。目前，这个示例项目仍然针对 .NET Core 2.2 框架，因此我们对其进行了略微修改，以针对 .NET Core 3（可在 netcore3 GitHub 仓库中找到）。

该应用程序演示了 QML.NET 中已可用的许多功能，构成了初学者 QML.NET 开发人员的理想学习示例。

侧边的滑动菜单在许多类型的应用程序中都是可重用的，此外，不同的页面还展示了特定的 QML.NET 功能。该程序的每个页面都包含一个关于如何使用不同功能来实现 C# 与 QML 之间交互的相关示例。

你应该仔细审阅这个示例，以便更深入地理解如何在自己的 .NET Core 3 应用程序中使用 QML 界面。

以下是该示例程序（已更新以针对 .NET Core 3）在不同平台上的渲染效果。

#### 在 macOS 上：

![](img/3d310cc066dda6e2dfa67a650614076f_231_0.png)

#### 在 Ubuntu 上：

![](img/3d310cc066dda6e2dfa67a650614076f_231_1.png)

#### 在 Windows 上：

![](img/3d310cc066dda6e2dfa67a650614076f_232_0.png)

运行这个第一个示例还将允许你验证开发环境和 QT 配置环境（检查所有是否按预期运行...）。

当你第一次运行这个示例程序时，QT5 运行时将被下载并安装到应用程序中，因此如果它花费很长时间请不要担心（这取决于你的互联网连接质量）。程序的第一次执行需要可工作的互联网连接。

也就是说，这适用于你尚未在开发机器上预先安装 QT5 运行时的情况。你可以借助 GitHub 上的专用项目预先安装 QT5 运行时（参见参考中的链接），这将节省在应用程序首次启动时的工作时间。

由于这是你测试的第一个 QT（或更确切地说是 QML.NET）程序，你可以注意到它在三个平台上的外观完全相同，QT 保证了 GUI 在跨平台实现中的一致性，这是 QT 的一个强项。

该应用程序的源代码可以在 GitHub 上找到。“qmlnet-samples” 并不针对 .NET Core 版本 3，要获取针对所需 .NET Core 版本的更新项目，请使用 netcore3 GitHub 仓库。

https://github.com/qmlnet/qmlnet-examples/

.Net Core 3 版本：https://github.com/netcore3/CodeBook/Chapter%208/6/QML.Features

### 8.6.5.2 QT Design Studio GUI 应用程序

通过这个第二个演示项目，我们将回顾如何使用 QT Design Studio 进行界面设计来开发 .NET Core 3 应用程序（实际上是为了生成 .qml 文件）。我们将创建一个简单的基表单，你可以将其作为未来使用 QML.NET 进行 .NET Core 3 开发的样板。

#### A) 在 QT Design Studio 中设计你的 GUI

对于此示例，我们将设计一个基本示例表单，包含一个标签和两个按钮，几乎是经典的表单模板。

#### B) 在项目中添加和使用 .qml 文件

一旦你设计（使用 QT Design Studio 编辑）了界面，就可以通过使用项目中的“添加现有项”菜单项轻松将其包含在 .NET Core 3 项目应用程序中。dotnet 方法由 QML 界面无缝调用（几乎如此，你需要实现它）。不要忘记将 .qml 文件的属性更改为“content”，如（*图 1*）所示。

![](img/3d310cc066dda6e2dfa67a650614076f_234_0.png)

该项目是一个用于开发基于 .NET Core 3 的 QML GUI 应用程序的基本项目示例，它使用通用的 QT Quick 控件进行界面设计。“Universal” 主题的使用说明了在 .qml 文件中使用主题的方法，主题也需要通过以下指令在 C# 代码中加载：

```csharp
QuickStyle.SetStyle("Universal");
```

在 QT Quick 中你可以选择几种预定义的主题：

-   Default
-   Material
-   Universal
-   Fusion
-   Imagine

你可以在下面的参考链接中找到关于 QT Quick 控件主题化的详细信息。

![](img/3d310cc066dda6e2dfa67a650614076f_235_0.png)

“解决方案资源管理器”窗口中的项目视图非常简单，仅包含添加到 Program.cs 的 .qml 文件。

在更复杂的项目中，你需要为每个使用的 .qml 文件添加一个类（.cs 文件）（最佳实践）。

![](img/3d310cc066dda6e2dfa67a650614076f_235_1.png)

请注意，你还可以将 "QT Design Studio" 关联为 .qml 文件类型的默认编辑器（参见 Visual Studio 内部的 Gtk/Glade 集成部分），以便更容易在 IDE 中操作此类文件。受之前示例（来自 Paul Knopf）的启发，该项目是一个带有标签和按钮的基本表单实现，这里没有使用效果或动画，这是最简项目（仅实现了使用 "Universal" 主题）。

该应用程序的功能相当有限（它实现了由按钮触发的标签控件文本更改），但它为开发 QML.NET 应用程序奠定了基础。

以下是该应用程序在不同平台上的渲染结果。

#### 在 macOS 上：

![](img/3d310cc066dda6e2dfa67a650614076f_236_0.png)

