
# VISUAL BASIC .NET

## 创建工具栏

你可以使用工具栏在表单上提供按钮，通常用于访问最常用的功能。`Toolbar`控件通过将`Appearance`设置`Normal`或`Flat`，提供了创建具有两种样式的基本工具栏所需的功能。虽然`Normal`是默认设置，但现代应用程序中的工具栏使用`Flat`样式。

`Toolbar`控件是`ListView`和`TreeView`控件族的一部分，允许你为工具栏获取图像。你可以使用`ImageList`属性附加一个`ImageList`控件。

每个按钮都包含在`Buttons`集合中。单个按钮具有`Text`属性、用于选择图像的`Index`属性、用于显示按钮提示的`ToolTip`属性以及`Style`属性。`Flat`样式是允许用户点击的标准工具栏样式。`ToggleButton`是一个在再次按下之前会保持按下状态的按钮。`Separator`是分隔符，用户无法点击它。

`DropDown`样式创建一个关联了下拉菜单的按钮。`DropDownMenu`属性允许你为按钮分配一个`ContextMenu`。有关上下文菜单的更多信息，请参阅第2章。

`TextAlign`属性允许将文本放置在控件下方或其右侧。

要使工具栏上的按钮具有功能，请使用`Toolbar_Click`事件，该事件返回用户点击的按钮的引用。对于切换按钮，你可以通过访问`Pressed`属性来检查它是否被切换到按下状态。下拉按钮在点击时应提供默认操作。当用户点击下拉按钮时，此事件将-

![](img/6e977c6eee8c1535039c864d41da5ccf_89_0.png)

- 1 在 Windows 应用程序项目中，添加一个`ImageList`控件来存放工具栏图像。
  注意：请参见“使用 ImageList”以获取更多信息。
- 2 双击`Toolbar`以添加它。
- 3 点击`ImageIndex`属性并选择`ImageList`控件。
- 4 点击`Buttons`属性。
  - 出现`Toolbar`集合编辑器。
- 5 点击`Add`。
- 6 在`TextBox`属性中为按钮输入标签，并在`ToolTip`属性框中输入描述。
- 7 点击`ImageIndex`属性并为工具按钮选择相应的图像。
  如果你为按钮分配了图像，则不需要填充`Text`属性。

用于工具栏的上下文菜单，允许用户选择性地显示和隐藏工具栏按钮。

![](img/6e977c6eee8c1535039c864d41da5ccf_90_0.png)

- 点击`Style`属性然后点击相应的样式。
- 默认的`PushButton`是标准工具栏按钮。你可以使用`Separator`类型在按钮之间留出空白。
- 你可以重复步骤5到8。
- 完成后点击`OK`。
- 按`F5`运行你的项目。
- 工具栏出现并允许你按下按钮。
- 要使按钮具有功能，你可以处理`ButtonClick`事件。

查看第2章以处理事件。

### 控件

#### 应用方法

你可以使用上下文菜单自定义 VB.NET `Toolbar`控件。下面的代码将工具栏按钮列入菜单，并允许用户切换每个按钮的可见性。只要每个按钮都有带有`Text`属性的标题，你就可以任何工具栏使用此代码。向控件添加一个`ContextMenu`并将`ContextMenu`属性设置为此。

输入以下内容：

结果：

```vb
Private Sub Form_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    MyBase.Load
    Dim button as ToolbarButton
    Dim menu as MenuItem
    For Each button In Toolbar1.Buttons
        ' 为每个工具栏按钮添加项
        menu = ContextMenu.Items.Add(button.Text, AddressOf MyClick)
        If button.Visible, then
            menu.Checked = button.Visible
        Next
    Next
End Sub
```

## 提供状态信息

你可以在表单上提供状态和帮助信息，通常位于底部的`StatusBar`控件。状态栏在右角还放置了一个易于调整大小的区域。`StatusBar`控件可以轻松在主应用程序空间内向用户广播，而不会干扰他们的操作。

面板的边缘。默认是`Sunken`，但其他选项包括`Raised`和`None`。你可以通过`Icon`属性向面板加载图标。`Toolbar`不缩放图标，因此图标需要16x16版本。

`StatusBar`有两种模式：`simple`和`paneled`。简单模式允许你只需设置`Text`属性并在状态栏上提供单行信息。

当`AutoSize`设置为`Content`时，允许面板根据内容调整自身大小。如果为`True`，则该属性定义面板的宽度。当面板设置了`AutoSize`时，你可以通过`MinWidth`属性定义最小宽度。

要启用面板模式，将`ShowPanels`设置为`True`。在此模式下，你定义了自定义的间距面板范围。每个面板都是可以放入文本信息的大小。VB.NET在`Panels`集合中定义-

所以如果`ShowPanels`为`False`，你可以通过设置`StatusBar.Text`等于文本字符串随时更改状态栏。在`ShowPanels`模式下，你需要通过设置`StatusBarPanel.Text`等于文本字符串单独更新不同的面板。

集合中的每个面板都有许多属性。`Text`允许你设置或检索其中的文本。`Alignment`允许左对齐、居中或右对齐。

![](img/6e977c6eee8c1535039c864d41da5ccf_91.png)

### 设置状态栏文本

查看第2章以处理事件。

- 1 在 Windows 应用程序项目中，添加一个`ImageList`控件来存放工具栏图像。
  注意：请参见“使用 ImageList”以获取更多信息。
- 2 双击`Toolbar`以添加它。

## 创建标签页界面

你可以在表单上提供状态和帮助信息，通常位于底部的`StatusBar`控件。状态栏在右角还放置了一个易于调整大小的区域。`StatusBar`控件可以轻松在主应用程序空间内向用户广播，而不会干扰他们的操作。
