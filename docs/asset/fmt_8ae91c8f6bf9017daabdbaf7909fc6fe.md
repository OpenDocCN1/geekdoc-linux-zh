
```csharp
public class MainWindow : Window
{
    private HorizontalBox _horizontalBox;
    private Button _button;
    private Label _label;

    public MainWindow(string title = "Multi:Platform UI", int width = 500, int height = 200, bool hasMenuBar = false) : base(title, width, height, hasMenuBar)
    {
        InitializeComponent();
    }

    private void InitializeComponent()
    {
        _verticalBox = new VerticalBox { AllowPadding = true; };
        this.Child = _verticalBox;

        _label = new Label("Hello from LibUI");
        _verticalBox.Children.Add(_label);

        _button = new Button("Sample Button");
        _verticalBox.Children.Add(_button);

        _button.Click += (sender, args) =>
        {
            MessageBox.Show("This is a message box.", "More detailed information can be shown here.");
        };
    }
}
```

此代码片段用于 `corelibUIForm` 示例程序（见下一节）。

这是此处介绍的 `LibUI` 包装器的非常基本的实现，但它让您对选择此库开发 `.NET Core 3` 项目所涉及的开发类型有了很好的了解。

### 8.4.4 示例项目

在 `.NET Core 3` 桌面应用程序中使用 `LibUI` 的包装器通过以下示例项目进行了说明。

- 第一个示例项目是一个经典的 `ControlGallery` 项目，改编自包装器的 GitHub 仓库。
- 第二个示例旨在为您提供一个样板项目，用于开发您自己的应用程序。

这两个示例都可以在 `Visual Studio 2019` 中使用和扩展，它们都针对 `.NET Core 3`。

#### 8.4.4.1 Control Gallery 示例应用程序

此应用程序是原始 `DevZH.UI` 仓库中提供的应用程序的更新版本。

该项目旨在说明在开发桌面 `.NET Core 3` 应用程序时，使用它可以达到的结果类型。它展示了使用各种小部件的示例。

如您在下面看到的，该应用程序的外观和感觉完全符合每个操作系统的设计规范（在每个操作系统上看起来都非常棒）。性能也不受影响，`LibUI` 是一个轻量级库。

**在 macOS 上：**

![](img/3d310cc066dda6e2dfa67a650614076f_175_0.png)

**在 Ubuntu 上：**

![](img/3d310cc066dda6e2dfa67a650614076f_176_0.png)

**在 Windows 上：**

![](img/3d310cc066dda6e2dfa67a650614076f_176_1.png)

该示例应用程序是几种类型控件的基本实例化和初始化的良好模板，但该演示中并未展示通过包装器可用的所有控件（通过详细审查包装器的源代码，您可以找到其他类型的控件实现）。

作为一个示例应用程序，该应用程序具有轻量级架构。该应用程序只是一个演示，带有 3 个选项卡表单，用于说明控件的使用。

您可以在 `Visual Studio` 的 `解决方案资源管理器` 中看到：

![](img/3d310cc066dda6e2dfa67a650614076f_177_0.png)

*（`LibUI ControlGallery` 项目示例）*

此示例的原始代码来自原始 `DevZH.UI` GitHub 仓库，已更新以用于 `NuGet` 包和 `.NET Core 3`。

重构后的示例（针对 `.NET Core 3`）的源代码可在 GitHub 上获取：

![](img/3d310cc066dda6e2dfa67a650614076f_178_0.png)

您可以尝试自行使用此简单示例，以便更熟悉 `LibUI` 和包装器 `DevZH.UI` 的使用。您也可以使用 "`coreLibUIForm`" 项目作为新项目的起点。

#### 8.4.4.2 基本表单项目示例

此示例项目的目标是提供一种快速使用 `LibUI` 包装器 `DevZH.UI` 开发应用程序的方法。

该项目包含一个带有标签和按钮的基本窗口。它是一个经过验证的模型，可用作项目开发的基准（灵感来自 `Visual Studio WinForms` 默认项目模板）。

该项目已准备就绪，并已包含此类项目所需的所有依赖项。

如您在下图（图 1）所见，项目架构极简。

![](img/3d310cc066dda6e2dfa67a650614076f_179_0.png)

（图 1）

以下是该应用程序在每个操作系统上运行时的预览。

**在 macOS 上：**

![](img/3d310cc066dda6e2dfa67a650614076f_179_1.png)

**在 Ubuntu 上：**

![](img/3d310cc066dda6e2dfa67a650614076f_180_0.png)

**在 Windows 上：**

![](img/3d310cc066dda6e2dfa67a650614076f_180_1.png)

该项目的源代码和架构旨在作为开发 `.NET Core 3` GUI 桌面应用程序的最小实现，因此它提供了一个用于启动自己项目的示例。

该项目的完整源代码可在 GitHub 上获取。

`https://github.com/netcore3/CodeBook/Chapter 8/4/corelibUIForm`

### 8.4.5 基于 LibUI 的 .NET Core 3 应用程序回顾

总之，`LibUI` 为开发 GUI 桌面应用程序提供了一种轻量级且高效的解决方案，它不需要安装依赖项的先决条件，也不需要安装专用工具。它轻量且快速，社区正在持续工作以进行改进集成。

在此背景下，`LibUI` 似乎应该是用于 `.NET Core 3` GUI 应用程序的完美工具（至少在该时间内，不同操作系统的显示 API 保持稳定），然而，缺乏用于 GUI 设计的可视化设计器可能会阻止许多开发者在专业环境或快速开发中使用它。掌握包装器以设计 GUI 所需的时间不应被低估，但一旦完成，该库取得的效果可能非常令人印象深刻。

## 8.5 GTK GUI 应用程序

`GTK`：“The Gimp Toolkit”最初是 Gnome 为在 Linux 上开发 GUI 应用程序而发起的倡议。`GTK` 在开源许可证（GNU）下开发。`GTK` 构建在 `Glib`（以及其他库）之上，这是一个经过充分测试且流行的库。

`GTK` 未提供大量文档，并且有特定的先决条件，因此被大多数开发者视为一种工具使用起来比较困难。但我们会看到，无论目标平台是什么，使用这种工具都能实现灵活的开发并获得良好的结果。因此，使用你喜欢的开发工具 `Visual Studio 2019`，你可以在其中获得极佳的开发舒适度来完成此类项目。

## 8.5.1 GTK 简介

`GTK` 位于许多知名的跨平台商业应用程序底层，在 GUI 项目开发方面被专业人士广泛认可。例如，Ubuntu 的 Gnome 桌面应用就是使用 `GTK` 开发的。

我们可以简要列举 `GTK` 的核心优势如下：

- 稳定性：`GTK` 已经研发了数十年。
- 酷炫的外观和交互体验。
- 支持主题。
- 面向对象（OO）方法。
- 本地化。
- 国际化。
- 良好的文档（文档正在不断完善）。

请记住，`GTK` 是为了配合使用并基于 C 和 C++ 语言开发的，因此它沿袭了这些语言的总体架构和编程逻辑。因此，这种开发模式非常适合希望利用 `.NET Core 3` 来实现生产力飞跃的 C 和 C++ 开发者。

`GTK` 工具包是 Linux 原生的，而 Windows 和 macOS 版本属于模拟环境；在这些操作系统上，`GTK` 工具包需要安装一系列库（并非完整列表）：

- `Atk`：`GTK` 的无障碍框架。
- `Cairo`：用于向量和图像合成的图形库。
- `Gdk`：包含窗口中的图形基元。
- `Gio`：用于 `GTK` I/O 操作的辅助函数。
- `Glib`：`GTK` 的工具箱和辅助函数（`GTK` 的基础之一）。
- `Gtk`：包含控件架构（用于窗口和控件）。
- `Pango`：`GTK` 的字体渲染库。

![](img/3d310cc066dda6e2dfa67a650614076f_183_0.png)
