

## Extra

你可以使用 TreeNode 类创建包含子节点的整个节点。通过这种方法，可以在将节点添加到控件之前设置节点的全部属性。构建 TreeNode 还允许你在添加到 TreeView 之前先构建整套节点和子节点。当程序已经运行时，这种方法非常有用，因为一次性添加整个树比逐个向树中添加项目要快得多。

## Example:

```
Dim newNode As New System.Windows.Forms.TreeNode()
Dim newChildNode As New System.Windows.Forms.TreeNode()
newNode.Text = "Sample item"
newChildNode.Text = "Sample child node"
newNode.Nodes.Add(newChildNode)
TreeView1.Nodes.Add(newNode)
```

7 点击 Add Root 添加顶级项目，或点击现有项目然后点击 Add Child 以将其作为子项添加。

8 输入节点的标签。

可选地，点击并为该项目选择自定义图像。

9 重复步骤 7 到 8 以添加必要的项目。

10 完成后点击 OK。

11 按 F5 运行项目。

TreeView 显示项目并允许用户关闭和打开子树。

## CREATE A TOOLBAR

你可以使用工具栏在窗体上提供按钮，通常位于顶部，以便访问最常用的功能。Toolbar 控件提供了创建基本工具栏的功能，有两种样式，由 Appearance 属性设置：Normal 或 Flat。虽然 Normal 是默认设置，但现代应用程序中的大多数工具栏都使用 Flat 样式。

Toolbar 控件是 ListView 和 TreeView 系列的一部分，需要一个 ImageList 来为工具栏按钮检索图像。你可以使用 ImageList 属性附加一个 ImageList 控件。

每个按钮都包含在 Buttons 集合中。单个按钮具有 Text 属性、用于从 ImageList 中选择适当图像的 ImageIndex 属性、用于为按钮显示工具提示的 ToolTipText，以及 Style 属性。PushButton 样式是用户可以点击的标准工具栏按钮。ToggleButton 是按下后保持按下状态直到再次按下才释放的按钮。Separator 是分隔符，用户无法点击它。

DropDownButton 样式创建了一个带有相关下拉菜单的按钮。DropDownMenu 属性允许你将 ContextMenu 控件分配给该属性。有关 Context Menu 控件的更多信息，请参阅第 2 章。

TextAlign 属性允许你将文本放置在图标下方，或放置在图标右侧。

要使工具栏上的按钮具有功能，请使用 Toolbar_ButtonClick 事件。事件变量 e 返回用户点击的按钮的引用。对于切换按钮，你可以通过访问 Pressed 属性如 e.Button.Pressed 来检查按钮是否被切换到按下状态。下拉按钮应在点击时提供默认操作。当用户点击下拉按钮时，不会触发此事件。

## CREATE A TOOLBAR

![](img/d6f772854306e15fb6df39b861a7b541_89_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_89_1.png)

- 1. 在 Windows 应用程序项目中，添加并设置一个 ImageList 控件以保存工具栏图像。
- Note: See the section "Work with ImageLists" for more information.

- 2. 双击 Toolbar 控件以添加它。
- 3. 点击 ImageList 属性并选择 ImageList 控件。
- 4. 点击 Buttons 属性。

- 4. 出现 Toolbar Collection Editor。
- 5. 点击 Add。
- 6. 在 Text 属性框中输入按钮的标签，并在 ToolTipText 属性框中输入描述。

- 7. 点击 ImageIndex 属性并选择工具按钮的适当图像。
- 如果你为按钮分配了图像，则无需填写 Text 属性。

## WORK WITH CONTROLS 3

## Apply It

你可以使用上下文菜单来自定义 VB.NET ToolBar 控件。下面的代码将工具栏按钮加载到菜单中，并允许用户切换每个按钮的可见性。只要每个按钮都使用 Text 属性设置了标题，就可以使用该代码与任何工具栏一起使用。将 ContextMenu 控件添加到窗体并将 Toolbar 的 ContextMenu 属性设置为此控件。

## TYPE THIS:

```
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load

Dim button As ToolBarButton, menuItem As MenuItem
' Loop through all toolbar buttons
For Each button In ToolBar1.Buttons
  ' add a menu item for each toolbar button
  menuItem = ContextMenu1.MenuItems.Add(button.Text, AddressOf MyMenuClick)
  ' if button is visible, check menu.
  menuItem.Checked = button.Visible
Next
End Sub

Private Sub MyMenuClick(ByVal sender As Object, ByVal e As System.EventArgs)
' get menu item from sender object
Dim menuItem As CType(sender, MenuItem)
' find toolbar button based on menu item
Dim button As ToolBarButton = ToolBar1.Buttons(menuItem.Index())

button.Visible = Not button.Visible
menuItem.Checked = Not menuItem.Checked
End Sub
```

## RESULT:

一个用于工具栏的上下文菜单，允许用户选择性地显示和隐藏工具栏按钮。

![](img/d6f772854306e15fb6df39b861a7b541_90_0.png)

8 点击 Style 属性的并然后点击适当的样式。

默认的 PushButton 是标准工具栏按钮。你可以使用 Separator 类型在按钮之间创建空白。

你可以根据需要重复步骤 5 到 8。

9 完成后点击 OK。

10 按 F5 运行你的项目。

Toolbar 出现并允许你按下按钮。

要使按钮具有功能，可以处理 ButtonClick 事件。

Note: See Chapter 2 to handle events.

