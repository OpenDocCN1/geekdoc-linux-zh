
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

## 处理一些事件

显示电阻值列表是一项壮举，但遗憾的是，我们的产品目前没有其他功能。由于最小化点击次数总是有益的，我们将每当用户点击列表中的一项时更新显示的值。这可以通过添加事件处理程序来实现。选择一个树视图并切换到属性窗口的“信号”窗格。

接下来，点击“Tree View Signals Cursor Changed”旁边的白色区域。`MonoDevelop` 会用一个可以输入方法名的文本框替换空白区域。最后，按 `Enter` 生成以下骨架；它不会自动显示，但在后端代码中等待着你：

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
```

如果多个控件要共享一个事件处理程序，高级程序员可以通过一个小技巧避免多个函数。复制第一个控件事件处理程序字段中找到的文本并将其粘贴到其他控件中。`MonoDevelop` 检测到相似性并 refrain（克制）生成另一个方法。

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

### C# 代码片段

```csharp
float val;
TreePath[] templ=ring1.Selection.GetSelectedRows ();
TreePath aPath1 = templ [0];
TreePath[] temp2=ring2.Selection.GetSelectedRows ();
TreePath aPath2 = temp2 [0];
val = aPath1.Indices [0] * 10 + aPath2.Indices [0];
```

如果您发现当前元素的索引号不足，代码还可以提取模型中负责所选行的部分。这是按照以下方式完成的：

```csharp
TreeModel model;
TreeIter iter;
var s = ring3.Selection;
s.GetSelected (out model, out iter);
var str3 = model.GetValue (iter, 0).ToString ();
```

```csharp
switch (str3)
{
    case "Black":
        val = val;
        break;
    case "Brown":
        val = val*10;
        break;
    case "Red":
        val = val*100;
        break;
    case "Orange":
        val = val*1000;
        break;
    case "Yellow":
        val = val*10000;
        break;
    case "Green":
        val = val*100000;
        break;
    case "Blue":
        val = val*1000000;
        break;
    case "Violet":
        val = val*10000000;
        break;
    case "Gold":
        val = val*0.1f;
        break;
    case "Silver":
        val = val*0.01f;
        break;
}
```

最后，通过将其分配给 `Text` 属性，内容被打印到标签上。为了简洁起见，我们的示例省略了对容差环的分析：

```csharp
label1.Text = val.ToString ();
```
