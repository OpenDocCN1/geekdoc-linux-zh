

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

用户对屏幕分辨率的喜好始终在变化：有些人发誓要使用 1280 x 800 分辨率的 12 英寸 HP EliteBook，而另一些人则在两块 100 英寸 4K 屏幕组成的套装上施展魔法。不幸的是，人类视觉不会如此广泛地扩展——这一事实通过频繁调整窗体大小来适应。GTK+ 强制你尊重这一点，要求添加窗体。添加一个 HBox 并用 VBox 填充其顶部单元格，以实现下图中“文档大纲”所示的外观。可以通过右键单击元素来调整网格单元的数量及其间距。在此情况下，MonoDevelop 会通过显示带有更多选项的上下文菜单来对此做出反应。接下来，通过拖动四个树视图和一个标签到由我们的 HBox 和 VBox 布局创建的网格中来添加它们。完成后，窗体应该与下图中左侧的结构相同。

MonoDevelop 版本的 GTK+ 不提供经典的列表框。相反，开发人员需要在窗体中添加一个树视图，并通过操作后端代码将其限制为传统的列表模式。属性允许你为控件分配友好的名称。下一步假设你拥有与上一张图片中显示的结构和树视图相同。

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

```csharp
var rStore = new Gtk.ListStore(typeof(string));
rStore.AppendValues("Black");
rStore.AppendValues("Brown");
rStore.AppendValues("Red");
rStore.AppendValues("Orange");
rStore.AppendValues("Yellow");
rStore.AppendValues("Green");
rStore.AppendValues("Blue");
rStore.AppendValues("Violet");
rStore.AppendValues("Gray/ey");
rStore.AppendValues("White");
rStore.AppendValues("Gold");
rStore.AppendValues("Silver");
```

最后，需要启动实际的显示处理。这通过向模型的行分配渲染器类来实现。它们使用其嵌入的绘图逻辑显示分配给它们的每个元素。由于我们处理的是纯文本，谦逊的 `CellRendererText` 就是我们所需要的一切：

```csharp
var renderer4Cell = new Gtk.CellRendererText();
column.PackStart(renderer4Cell, true);
column.addAttribute(renderer4Cell, "text", 0);
ring1.Model = rStore;
```

其他三个环将以类似的方式填充：通过调整 `AppendValues` 的调用次数以及提供给它颜色名称来调整添加到列表中的元素数量。

请注意，每个“辅助对象”一次只能分配给一个列表框。尝试回收利用，例如列表中显示的那种，是导致崩溃的可靠方法：

```csharp
var column = new Gtk.TreeViewColumn();
column.Title = "RING";
ring1.AppendColumn(column);
ring2.AppendColumn(column);
```

运行程序以查看窗体。最后，使其外观类似于前一页和另一页上的图片。如果你正确填充了行，我们的电阻计算器就准备就绪了。

# 处理一些事件

显示电阻值列表是一项壮举，但遗憾的是，我们的产品目前没有其他功能。由于最小化点击次数总是有益的，我们将每当用户点击列表中的一项时更新显示的值。这可以通过添加事件处理程序来实现。选择一个树视图并切换到属性窗口的“信号”窗格。

接下来，点击“Tree View Signals Cursor Changed”旁边的白色区域。MonoDevelop 会用一个可以输入方法名的文本框替换空白区域。最后，按 Enter 生成以下骨架；它不会自动显示，但在后端代码中等待着你：

```csharp
protected void OnChange(object sender, EventArgs e)
{
    throw new NotImplementedException();
}
```

由于复制程序逻辑是不好的，我们将激活事件连接到一个名为 `refreshContent` 的通用方法。由于空间限制，我们将提示代码限制为 `OnChange` 的新版本：

```csharp
protected void OnChange(object sender, EventArgs e)
{
    recalculateWindow();
}

如果多个控件要共享一个事件处理程序，高级程序员可以通过一个小技巧避免多个函数。复制第一个控件事件处理程序字段中找到的文本并将其粘贴到其他控件中。MonoDevelop 检测到相似性并 refrain（克制）生成另一个方法。

`recalculateWindow` 开始确定每个窗口中当前选中的行：如果其中任何一个“未触碰”（未选择），我们打印一个错误：

```csharp
private void recalculateWindow()
{
    if (ring1.Selection.CountSelectedRows() == 0 ||
        ring2.Selection.CountSelectedRows() == 0 ||
        ring3.Selection.CountSelectedRows() == 0 ||
        ring4.Selection.CountSelectedRows() == 0) 
    {
        label1.Text = "Missing Values";
        return;
    }
}
```

下一步涉及电阻的实际计算。我们的代码是故意构造的，因为它展示了解决确定实际选中哪个项目问题的两种方法。在列表索引和元素之间关系已知的情况下，可以制定一个公式来确定内容，而无需查找模型。

