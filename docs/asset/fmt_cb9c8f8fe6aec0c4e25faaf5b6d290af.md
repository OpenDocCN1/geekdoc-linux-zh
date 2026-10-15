
的的的的的菜单，菜单菜单菜单菜单菜单菜单快捷快捷。。通过在字母前使用 `&` 符号来菜单快捷键。例如，`&`。你可以使用 `Shortcut` 属性为菜单项分配快捷键。将 `Show键` 属性设置为 `True`，如果你希望快捷键菜单项右侧。

` `` ````。。。。。。。。。， `，控件控件来添加控件。

![](img/6e977c6eee8c1535039c864d41da5ccf_51.png)

## 添加菜单

1 创建一个新的 Windows 应用程序或打开一个现有的。
2 打开工具箱。如果没有工具箱，点击“查看工具箱”。
3. 双击控件。
4. 通过输入项添加到菜单。
5. 输入名称。
6. 按回车保存。
7. 添加破折线创建分隔符，或者右键点击区域点击分隔符。
8 点击任何控件。
9. 点击右侧的占位符。
10. 输入键并按回车。
11. 点击控件。
12. 在属性窗口中，选择新的快捷键。
13. 按 `F5` 运行项目。
你的项目加载并在顶部提供了一个菜单栏。

## 开始使用 Windows 窗体

### 2

每个菜单项都有许多可以单独修改的属性。
`MenuItem1.Visible = False` 隐藏一个菜单项。`MenuItem1.Enabled = False` 禁用菜单项。你使用属性根据应用程序的当前状态动态更改菜单。对于具有 `New`、`Open` 和 `Save` 项的文件，当你的应用程序没有更改时，通过向文件的 `Click` 事件添加代码来禁用 `Save`。

示例：
动态菜单示例：

```
Private Changes As Boolean = False

Sub MenuItem1_Click(ByVal sender As System.Object, ByVal e As EventArgs) Handles MenuItem1.Click
```

```
If Changes Then

FileSaveMenuItem.Enabled = True

Else

FileSaveMenuItem.Enabled = False
```

你可以在代码中动态创建菜单项，程序使用 `Dim` 创建新菜单，设置其属性，然后将其添加到选择的父菜单中。

动态创建菜单项的示例：
`NewMenuItem.Text = "Text for menu item"` `NewMenuItem.Shortcut = System.Windows.Forms.Shortcut.ShiftF1` `Menu.Items.Add(NewMenuItem)`

![](img/6e977c6eee8c1535039c864d41da5ccf_52_0.png)

## 创建上下文菜单

你可以使用上下文菜单（Context-sensitive menus）来提供与用户点击区域相关的选项列表。上下文菜单有时被称为“右键菜单”，因为你使用鼠标右键来访问它们。上下文菜单自 Windows 95 引入以来一直存在，现在上下文菜单是微软 Office 的一项必要功能。

单个表单上只应存在一个 `Menu` 控件。但对于 `ContextMenu` 控件并非如此。表单上的大多数视觉组件都应该存在一个独立的 `ContextMenu` 控件。

要在表单上添加上下文菜单，你需要添加一个 `ContextMenu` 控件并像定义标准菜单一样定义该菜单。创建菜单时，选择“A Menu（一个菜单）”部分。无法为菜单标题命名，因为上下文是源于控件而不是菜单栏。然后，使用所有控件和表单本身提供的 `ContextMenu` 属性，并选择要关联的 `ContextMenu`。

要在程序中添加和删除上下文菜单中的项，你可以操作上下文菜单的 `MenuItems` 属性提供的项集合。声明 `Menu` 对象的实例并将此对象传递给 `MenuItems.Add` 方法，这是在上下文菜单内部复制菜单的唯一方法；你也可以在设计时间进行复制粘贴，或者在运行时添加代码来创建菜单的副本。通过 `CloneMenu` 方法传递新菜单。通过 `ContextMenu` 控件中 `Items` 集合的 `Add` 方法。

## 创建上下文菜单

![](img/6e977c6eee8c1535039c864d41da5ccf_53_0.png)

![](img/6e977c6eee8c1535039c864d41da5ccf_53_1.png)

- 1 在新的 Windows Application 项目中打开第一个表单。
- 2 在工具箱中双击 `ContextMenu` 控件。
- 3 点击第一个菜单项的占位符。
- 4 为菜单项输入说明（Caption）。
- 5 在工具箱中，点击你想要分配给上下文菜单的控件。

## 开始使用 Windows Forms

使用 Apply It 上下菜单是让你的程序更具功能的简单方法。许多用户期望在右键点击时看到该项目的功能。在大多数情况下，你必须将相同的功能放置在上下文菜单或主菜单中。如果处理不好，你会在上下文菜单的点击事件和主菜单的点击事件中复制代码。

输入以下内容：

```
Private Sub Menu1_Click()

    RemoveSelectedItems()

End Sub
```

```
Private Sub Button1_Click()

    RemoveSelectedItems()

End Sub
```

将你的主要部分分在独立的过程中，而不是简单地直接在事件中定位代码，是值得的。如果你有一个具有相同函数的表单和上下文菜单，你可以重用这些代码。为了使此代码生效，请使用下方步骤所示的示例，并在表单上添加一个按钮。有关处理事件的更多信息，请参第 2 章。

# 结果：

按钮和上下文菜单的功能属性相同。

![](img/6e977c6eee8c1535039c864d41da5ccf_54_0.png)

- 6 将控件添加到表单中。
- 示例向表单中添加了控件。

注意：要控制表单，请查看“向表单添加控件（Add a Control to the Form.）”部分。

- 7 设置你刚刚创建的 ListBox 的 `ContextMenu` 属性。
- 8 按 `F5` 运行你的项目。
- 9 右键点击你的控件以查看你的上下文菜单。
- 当右键点击相应的控件时，`ContextMenu` 控件控制你创建的菜单。

## 添加新表单

额外的表单对于创建应用程序中的弹出窗口、对话框和各种功能是必要的。你可以通过使用“添加表单（Add Form）”对话框为你的项目创建额外的表单。

VB .NET 项目由多个文件、类、表单和模块组成。项目可以包含无限数量的每种类型。你可以使用表单有效地将你的程序拆分为供用户导航和理解的可管理部分。在单个表单上包含一个单一概念。例如，如果你的项目有四个功能，请不要尝试在一个表单中实现所有功能。

Microsoft Word 有一个主窗口和几十个辅助窗口，用于打开和保存文件、修改选项和配置格式。VB .NET 用唯一的表单来表示应用程序中的每个窗口。

提供打开和关闭文件选项的窗口被称为对话框。你可以在 VB .NET 中创建这些对话框。要创建对话框，请查看“创建对话框（Create a Dialog Box）”部分。在在 VB .NET 中可以使用工具箱创建另一种类型的窗口。像 Adobe Photoshop 这样的程序使用浮动窗口提供一组工具，用户可以在主应用程序窗口中访问这些工具。你可以使用所有表单（owned forms）创建工具箱窗口。有关创建自定义表单的更多信息，请查看“所有表单（An Owned Form）”部分。

在大多数情况下，使用 VB .NET 创建的标准 Form 作为主窗口。你可能需要添加辅助窗口。例如：

![](img/6e977c6eee8c1535039c864d41da5ccf_55_0.png)

## 添加新表单

![](img/6e977c6eee8c1535039c864d41da5ccf_55_1.png)

- 1. 在 Windows Application 项目中，点击 `Project > Add Form`。
- 2 为表单输入名称。
- 3. 点击 `OK`。
- 4 右键点击表单以编辑其属性。
- 5. 将 `FormBorderStyle` 改为 `FixedDialog`。
- 6. 将 `MinimizeBox` 和 `MaximizeBox` 设置为 `False`。

## 开始使用 Windows Forms

# VISUAL BASIC .NET

## 创建对话框

你可以使用对话框提示用户。对话框在用户提供信息之前不会消失。

对话框是一种模态表单，在用户关闭它之前限制对父表单的访问。对话框的示例包括文件文件。要创建对话框，创建一个表单并使用方法接受或取消。有关更多信息，请考虑“添加控件（Add a Control）”。

在之前的 Visual Basic 版本中，你必须在显示之前创建实例。示例：

```vb
Dim frm As New Form()

frm.Show()
```
