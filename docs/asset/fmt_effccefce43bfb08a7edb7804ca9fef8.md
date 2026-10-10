
# UserForm 事件与验证

## 事件概述

并非所有事件对每个控件可用。在代码窗口中，检查过程列表以查看与选控件相关的事件。

每个 `UserForm` 有两个元素：图形布局和代码窗口。图形布局允许你在对话框中添加控件。有关设计自定义对话框的更多信息，请参阅“创建自定义对话框”部分。每个 `UserForm` 还有一个代码窗口，其中包含了你用于为每个控件创建事件的所有代码。`Excel` 会考虑在对话框中发生的每一次交互，例如滚动列表、选择 `OK` 按钮或在文本框中输入。`UserForm` 控件控制着若干你可以捕获的不同事件。最常见的事件是 `Click`，它是默认发生的，当你点击控件时，`Visual Basic` 编辑器会为该控件创建一个 `Click` 事件。如果已存在 `Click` 事件，`Visual Basic` 编辑器将仅显示代码窗口。你创建 `VBA` 代码来监控控件的事件（例如点击按钮），并确定 `Excel` 何时执行。你捕获控件事件以确定何时执行特定代码。以下列表标识了放置在 `Userform` 上的各种控件发生的常见事件。

## 从自定义对话框获取输入（继续）

![](img/b1f17ae2919b92b22fb561904c497d03_223_0.png)

![](img/b1f17ae2919b92b22fb561904c497d03_223_1.png)

- 8 创建新模块。

注意：有关创建宏的信息，请参阅第9章。

- 9 输入 `PublicSelection As String`，将 `UserSelection` 替换为全局变量名。

- 10 创建一个新的子程序。

- 11 使用 `Userform.ListBox1`，将 `Userform` 和 `ListBox1` 分别替换 `Userform` 和 `ListBox` 控件。

- 12 输入 `.AddItem "Jan"`，将 `"Jan"` 替换为添加到 `ListBox` 的值。

- 13 为每个项目重复步骤12。

- 14 `End With`.

## 额外

| 控件事件 | 发生情况 |
|---|---|
| `BeforeDragOver` | 用户正将数据拖放到控件上。 |
| `BeforeUpdate` | 在控件数据更改之前。 |
| `Change` | 当控件的 `Value` 属性改变时。 |
| `Click` | 用户用鼠标按钮双击控件时。 |
| `DblClick` | 用户双击控件时。 |
| `Enter` | 在用户按下 `Enter` 键使控件获得焦点之前。 |
| `KeyDown` | 用户按下按键时。 |
| `MouseDown` | 用户按下鼠标按钮时 |

## Excel 数据分析

## 验证对话框的输入

验证可以确保你接收用于分析的信息是准确的且格式正确的。在将对话框控件指定的数值传回你的过程 `procedure` 之前，你必须对这些值进行验证，原因有两个：首先，确保用户为控件使用了某个值。如果用户忘记了选择某个值，你可以立即提醒他或她。其次，确保你的代码中不会发生严重错误，因为向过程传递了错误类型的数据。

在该程序 `routine` 的验证代码中，你使用条件语句（如 `If Then` 语句）来检查每个控件的属性。例如，为了确保用户在对话框的文本框中使用字符串，你可以在你的过程中添加 `If TextBox1.Text = "" Then` 语句。检查 `Text` 控件以确保它包含值。如果该属性为空（或不包含内容），你的 `VBA` 代码可以调用 `Msgbox` 显示消息，告诉用户输入一个值。

你可以创建代码来检查用户窗 `UserForm` 上发生的任何事件的用户输入。最简单的方法是在关闭对话框之前。例如，如果一个 `CommandButton` 按钮将值传递给全局变量并关闭对话框，这就是你验证数据的理想位置。当你放置代码时，你还使用验证函数来验证控件是否包含适当的数据类型。例如，如果 `IsNumeric(TextBox1.Value) Then`，则确保用户在 `TextBox` 控件中输入了数字。

## 验证对话框的输入

- 在用户窗 `UserForm` 上，双击你想要验证数据值的控件。

- 通常，`OK` 命令按钮是验证数据值的良好位置。

- 代码窗口打开，光标位于所选控件的 `Click` 事件开头。

## 实践

与其创建运行在控件事件上的验证代码，不如使用 `UserForm` 事件来启动代码，例如捕获 `UserForm` 的 `QueryClose` 事件。以下代码确保了在关闭对话框之前，已为 `ListBox` 控件选择了一个值。

示例

```vba
Private Sub UserForm_QueryClose(Cancel As Integer, CloseMode As Integer)
If Not IsNumeric(Text1.Value) Then
    MsgBox "Must be a number"
    Cancel = 1
End If
End Sub
```

`QueryClose` 事件有两个参数：`Cancel` 和 `CloseMode`。`Cancel` 参数接受一个整数值。如果该参数的值非零，则 `QueryClose` 事件将停止，并且相关的对话框将保持打开。`CloseMode` 参数包含一个指示 `QueryClose` 事件原因的值。你可以通过输入与常量关联的值 0 或使用四个常量中的一个来更改此参数的值。使用 `vbFormControlMenu` 指定用户选择了对话框上的关闭 `Close` 按钮；使用 `vbFormCode` 指明由 `Unload` 语句启动的代码；使用 `vbAppWindows` 表示 `Windows` 操作系统正在结束，且任务管理器正在关闭 `Excel`。

- 要检查的控件和属性值。

- 紧随 `MsgBox` 之后的是 `MsgBox` 的文本。

- `Exit Sub`。

- `End If`。

- 切换到 `Excel` 并运行宏。

如果未为控件选择值，则会出现消息框。

## 安装 Excel 加载项

你可以使用 `Excel` 利用许多加载项——这些加载项提供了额外的财务和科学函数及选项。除了 `Excel` 加载项外，你还可以添加提供其他功能的加载项。在 `Excel` 自带的加载项中，你应该考虑使用：

- `Excel` 工具库 `Excel ToolPak`，提供了财务和科学函数及选项。例如，此加载项包含一组用于执行工程计算的函数，以及其他财务、数据与时间和数学函数。分析工具库 `Analysis ToolPak` 还包含本章描述的统计分析工具。

- 分析工具库 — `VBA` `Analysis ToolPak — VBA`，具有财务、数学以及日期和时间函数。例如，你加载 `ACCRINT` 函数来计算应计利息金额。

- 条件求和向导 `Conditional Sum Wizard`，可以让你快速创建公式，该公式仅在你指定的情况下进行计算。更多信息，请参见“使用条件求和向导”章节。

`Excel` 将任何带有 `.xlsa` 后缀的文件识别为加载项，在“加载项”对话框中列出它们，并自动将加载项文件加载到硬盘上某个文件夹之一：
