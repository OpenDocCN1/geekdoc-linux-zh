
# 使用 MonoDevelop 窗体创建用户界面

创建基于 GTK 的 UI 过去是一项令人沮丧的工作，但 MonoDevelop 改变了这一切...

+ **Tim Hanna** 自 Amiga PC 时代起就从事 IT 行业。作为记者、导师、演讲者以及科学书籍的作者，他多次见证移动市场的各个方面

使用 GTK 很痛苦：其基于句柄函数的编码范式在 Palm OS 时代可能看起来很酷，但现在看起来非常过时。

V-CL 试图通过为大多数 GUI 类提供面向对象封装来改善这种情况。这导致了更紧凑的代码，但它离真正的 RAD（快速应用程序开发）还差得远：看到您正在工作的用户界面是生产力的真正助推器。Visual Basic 在这方面一直是领导者。该产品的第一个版本在 DOS 下运行，但它并未吝啬于提供 WYSIWYG-GUI 编辑器。

尽管 Mono 包含对 Microsoft 的 `Windows.Forms` 命名空间的运行时仿真，但 MonoDevelop 的 WYSIWYG 编辑器是基于 GTK 的。由于该框架与 Mono 一样具有跨平台性，对于大多数基于桌面的应用程序来说，使用 GTK 不应是问题。此外，这里讨论的许多概念也可以应用于各种其他 GUI 工具。

MonoDevelop 将为您生成默认的 `GTK 2.0` 项目骨架。除了已知的 `C#` 文件外，我们的项目现在还有一个包含窗体布局和几个图标的资源文件的文件夹。实际的程序执行仍然通过 `Program.cs` 处理，默认情况下包含以下代码：

```csharp
class MainClass
{
    public static void Main (string[] args)
    {
        Application.Init ();
        MainWindow win = new MainWindow ();
        win.Show ();
        Application.Run ();
    }
}
```

`Application.Init()` 是 GTK 框架主类中的静态方法。在创建并显示 `MainWindow` 类的新实例后，我们调用 `Run()` 以启动事件循环。

## 资源

- **MonoDevelop**
    - [monodevelop.com](http://monodevelop.com)

首先启动 MonoDevelop。我们在这个 `C#` 和 MonoDevelop 系列的第一部分中涵盖了安装和部署说明（第 157 期）。然后基于模板 `C# > Gtk 2.0 Project` 创建新项目。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_45_1.png)

右：这次我们将制作一个简单的电阻色码计算器

我们的窗体由一个 WYSIWYG（所见即所得）组件布局和一个后端代码类组成，其结构如下：

```csharp
public partial class MainForm : Gtk.Window
{
    public MainForm() : base(Gtk.WindowType.TopLevel)
    {
        Build();
    }
}
```

`MainWindow` 的构造函数调用了 `Build()` 方法。它连接到 MonoDevelop 后端，并利用那里的逻辑来生成一个准备就绪的窗体实例。`OnDeleteEvent` 展示了两个有趣的范式：

```csharp
protected void OnDeleteEvent(object sender, DeleteEventArgs a)
{
    Application.Quit();
    a.RetVal = true;
}
```

首先，`Application.Quit()` 在 `MainForm` 关闭时被调用。这防止应用程序以僵尸般的状态在后台继续运行。

其次，设置一个标志以将事件标记为“已完全处理”。这一点非常重要，因为大多数 GUI 框架都会创建类似的事件管道：事件会经过一组事件过滤器，由它们接受或拒绝每个事件。如果开发者的代码未表现出对某个事件的兴趣，该事件通常会被系统默认处理器“埋没”。

# 编码电阻器

电工讨厌处理电阻器——它们怪异的颜色编码使确定元件数值变得困难。因此，看到许多专门用于这项相对简单任务的应用程序并不令人惊讶。

我们将通过双击 `MainForm` 的窗体文件开始。通过分别点击左下角的“Source”或“Designer”切换按钮，可以以文本模式或 GUI 模式显示它。

位于屏幕右侧的小选项卡允许你打开工具箱或属性对话框。工具箱包含一个可通过拖放放置在窗体中的各种控件列表，而属性对话框则显示与当前选中元素相关的属性和设置。

从 Visual Studio 转换过来的开发人员需要了解一个小怪癖。在窗体预览中选中控件不会显示其属性；相反，你需要在文档的大纲窗口中选中它们。

为了降低复杂性，我们将程序限制在对四色环电阻的解码。在 Designer 模式下选中窗体并拉伸其边框，以增大窗体大小。

# 树视图

用户对屏幕分辨率的喜好始终在变化：有些人发誓要使用 1280 x 800 分辨率的 12 英寸 HP EliteBook，而另一些人则在两块 100 英寸 4K 屏幕组成的套装上施展魔法。不幸的是，人类视觉不会如此广泛地扩展——这一事实通过频繁调整窗体大小来适应。`GTK+` 强制你尊重这一点，要求添加窗体。添加一个 `HBox` 并用 `VBox` 填充其顶部单元格，以实现下图中“文档大纲”所示的外观。可以通过右键单击元素来调整网格单元的数量及其间距。在此情况下，MonoDevelop 会通过显示带有更多选项的上下文菜单来对此做出反应。接下来，通过拖动四个树视图和一个标签到由我们的 `HBox` 和 `VBox` 布局创建的网格中来添加它们。完成后，窗体应该与下图中左侧的结构相同。

MonoDevelop 版本的 `GTK+` 不提供经典的列表框。相反，开发人员需要在窗体中添加一个树视图，并通过操作后端代码将其限制为传统的列表模式。属性允许你为控件分配友好的名称。下一步假设你拥有与上一张图片中显示的结构和树视图相同。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_46_0.png)

# 添加另一个窗体 – 第 1 部分

我们的计算器是一个典型的例子，它只需要一个窗体就能应付，因为大多数应用程序需要一组窗体。让我们来做到这一点！我们将增加一些真实感。重新打开 `MainForm` 的 WYSIWYG 部分并添加布局中的一行。然后添加一个按钮并将其 `Clicked` 方法连接到以下代码：

```csharp
protected void Button1_Clicked(object sender, EventArgs e)
{
    NewCalculatorWindow();
    mWindow.Show();
}
```

左图：我们的电阻计算器将由四个相邻的滚动窗口窗体组成

# 教程

# MonoDevelop

# 添加窗体 – 第 2 部分

完成上述操作后，是时候注册第二个窗体了。点击“文件/新建/文件”并选择模板 `Gtk+Window`。将类名设置为“AboutWindow”并点击“新建”，以便将资源添加到项目中。在下一步中，从后端代码文件中移除命名空间声明。

运行当前状态下的程序，以便让你的眼睛在第二个空对话框上停留——它正等待你的创造力！

# 模型疯狂

树视图与经典列表视图不同，因为它们通过实现模型-视图-控制器（MVC）概念提供了额外的灵活性。数据通过页眉、布局管理器和数据容器模型的组合来显示。

```csharp
public Mainwindow() : base(Gtk.WindowType.TopLevel)
{
    Build();
    var column = new Gtk.TreeViewColumn();
    column.Title = "RING";
    ring1.AppendColumn(column);
    ring1.HeadersVisible = false;
}
```

首先，必须设置存储在树视图中的数据的基本“模型”。我们只需要添加一列数据；其标题不需要显示。

下一步涉及创建实际数据。它在一个 `ListStore` 中找到庇护所——并且因为它也可以作为多列存储。`AppendValues` 是一个可变参数函数：
