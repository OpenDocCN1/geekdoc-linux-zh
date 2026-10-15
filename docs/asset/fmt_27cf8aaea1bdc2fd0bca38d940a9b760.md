
## 创建消息框

1. 创建新项目或打开现有项目。
2. 打开要显示消息框的方法或事件。
3. 单击空代码行。
4. 输入 `System.Windows.Forms.MessageBox.Show(`.
5. 输入要在引号中显示的文本或 `string` 类型的变量。
6. 输入逗号，并输入消息框的标题。
7. 输入另一个逗号。

出现 IntelliSense 框并显示各种按钮选项。

### 应用它

你可以使用消息框向用户提问然后做出响应。`Show` 方法返回对应于 `DialogResult` 值的值。每个消息框按钮都有对应的 `DialogResult` 类型，你可以使用它来确定用户按下了哪个按钮：`OK`、`Cancel`、`Yes`、`No`、`Retry`、`Ignore`、`Abort`。要测试消息框的返回值，请使用 `DialogResult.OK` 或其他常量。`If` 测试可以轻松检查用户的响应。有关使用 `If` 语句的更多信息，请参阅第 4 章。

#### TYPE THIS:

```
Dim result As DialogResult
result = MessageBox.Show("Do you like strawberry ice cream", "Ice cream", MessageBoxButtons.YesNoCancel, MessageBoxIcon.Question)
If result = DialogResult.Yes Then
    MessageBox.Show("Me too!!!")
Else
    If result = DialogResult.Cancel Then
        MessageBox.Show("You are no fun.")
    Else
        result = MessageBox.Show("Too bad. How about chocolate ice cream?", "Ice cream", MessageBoxButtons.YesNoCancel, MessageBoxIcon.Question)
        If result = DialogResult.No Then
            MessageBox.Show("What do you like???")
        End If
    End If
End If
```

#### RESULT:

Do you like strawberry ice cream?

Me too!!

![](img/d6f772854306e15fb6df39b861a7b541_60_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_60_1.png)

8 输入或单击其中一个按钮选项。
9 输入另一个逗号，并重复步骤 7 和 8 以设置图标。
10 输入另一个逗号，选择默认按钮并输入右括号。
11 按 `F5` 运行你的项目。
12 调用必要的代码以显示你的消息框。

消息框出现并等待用户按下按钮。

## 添加一个已拥有的窗体

你可以使用已拥有的窗体来创建可随父窗体一起出现的浮动窗口。单个父窗体可以拥有任意数量的窗体。使用已拥有的窗体可以在节省主程序窗口空间的同时仍允许访问功能。已拥有的窗体还允许用户移动浮动窗口来自定义其自己的环境。

你不需要将已拥有的窗体放在父窗体的边界内，但已拥有的窗体始终浮动在其父窗体之上。如果用户最小化父窗体，则已拥有的窗体消失，并在用户恢复父窗体时重新出现。Visual Basic 开发工作室本身就是已拥有窗体的一个很好的例子。然而，开发工作室提供的停靠功能并不是已拥有窗体提供的标准功能的一部分。

已拥有的窗体与任何标准窗体没有区别。创建类似工具箱的浮动窗口需要一些设置，使其看起来像其他应用程序。将 `FormBorderStyle` 设置为 `FixedToolWindow` 或 `SizableToolWindow` 以减少标题栏浪费的空间。将 `MaximizeBox` 和 `MinimizeBox` 设置为 `False`，并将 `ShowInTaskBar` 设置为 `False`，使其不像独立的应用程序窗口。

要将窗体设置为已拥有的窗体，你可以使用两种方法，具体取决于对你的应用程序最方便的位置。你可以设置子窗体为已拥有；例如如果 `FormToolbar` 需要浮动在 `FormMain` 之上，设置 `FormToolbar.Owner = FormMain`。或者父窗体可以接管子窗体，例如 `FormMain.AddOwnedForm(FormToolbar)`。你最常使用第二种方法，因为在大多数情况下，主应用程序窗体创建已拥有的窗体，而不是相反。

已拥有的窗体与任何标准窗体没有区别。创建类似工具箱的浮动窗口需要一些设置，使其看起来像其他应用程序。

![](img/d6f772854306e15fb6df39b861a7b541_61_0.png)

1 创建一个 Windows 应用程序项目或打开一个现有项目。
2 向项目添加一个新窗体。

注意：请参阅“添加新窗体”部分以创建新窗体。
3 适当调整新窗体的大小。
4 对于新窗体，在属性窗口中单击 `FormBorderStyle` 属性并选择 `SizableToolWindow`。
5 双击 `MaximizeBox` 属性将其更改为 `False`。
6 将 `MinimizeBox` 更改为 `False`。
7 将 `ShowInTaskbar` 更改为 `False`。
8 加载原始窗体并双击它以进入代码编辑器。

## 开始使用 Windows 窗体

### 应用它

通常，你必须使放置在已拥有窗体上的组件在其父窗口上执行操作。例如，你需要使已拥有窗体上的一个名为 `Open` 的按钮执行与父窗口上的 `File`、`Open` 菜单相同的操作。你必须在主窗口中声明提供功能的代码——在示例中，提供文件打开对话框并打开文件的代码——在它自己的子例程中。你使此例程为 `Public`，以便你可以在窗体外部访问它。请参阅第 4 章以了解有关方法的更多信息。

#### 输入以下内容：

```
Public Class FormToolWindow

    Private Sub ButtonFileOpen_Click(...)
        Dim frm As FormMain = Me.Owner
        Frm.FileOpenRoutine()
    End Sub

End Class

Public Class FormMain

    Public Sub FileOpenRoutine()
    End Sub

    Private Sub MenuFileOpen_Click(...)
        FileOpenRoutine()
    End Sub
End Class
```

#### 结果：

工具箱提供的打开功能与文件打开菜单项相同。

![](img/d6f772854306e15fb6df39b861a7b541_62_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_62_1.png)

8 代码编辑器为主要窗体打开。
9 在窗体加载事件中，声明已拥有窗体的实例。
10 输入 `Me.AddOwnedForm(` 后跟已拥有窗体的变量名和一个右括号。
11 输入已拥有窗体的变量名后跟 `.Show()`.
12 按 `F5` 运行项目。

已拥有的窗体浮动在其父窗体之上，当用户最小化父窗体时消失，并在用户恢复父窗体时再次出现。

## 排序 Tab 键移动

你使用 `Tab` 键作为在不使用鼠标的情况下在应用程序中移动的标准方法。默认情况下，Windows 窗体按你将控件添加到窗体的顺序分配移动顺序。很少有开发人员第一次就能完美地布局窗体，因此 `TabIndex` 属性允许你编辑控件的顺序。

用户期望从窗体的左上角开始输入。通常，按 `Tab` 键会从左到右或从上到下移动。虽然你可能会发现重置所有控件的 Tab 索引是繁琐的工作，但 Microsoft Windows 应用程序指南要求这样做，并且这样做会使应用程序更专业。设置 Tab 顺序还会使你的应用程序对进行数据输入的人员以及习惯于使用键盘而不是强制用户在输入或更改数据之前单击每个控件在计算机上移动的任何人更易于访问。数据库和其他需要大量数据处理的应用程序在采用智能 Tab 顺序布局后会变得显著更易于使用。

设置 Tab 顺序最简单的方法是完全设计你的窗体，移动控件直到出现明显的视觉顺序。此时，从应用程序的左上角开始，将控件的 `TabIndex` 属性设置为零。然后根据对你的应用程序有意义的方式，移动到下一个控件并将其 `TabIndex = 1` 分配给它。继续直到每个控件都有合理的 Tab 顺序。

你还可以通过将控件的 `TabStop` 属性设置为 `False` 来将其从 Tab 顺序中移除。该属性对于标签和其他不直接涉及数据输入的控件很有用。默认情况下，窗体上的每个控件的 `TabStop` 都是 `True`。

![](img/d6f772854306e15fb6df39b861a7b541_63_0.png)

1 创建一个新的 Windows 应用程序项目或打开一个现有项目。
