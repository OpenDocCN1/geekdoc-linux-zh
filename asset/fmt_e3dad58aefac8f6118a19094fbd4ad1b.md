
有效地使用文本框需要大量的测试。由于文本框存在自由输入功能，用户可能会输入错误的数据，这需要程序员提供验证来检查用户输入的内容。`VB.NET` 具有新的验证功能。你可以在“提供错误消息”部分了解 `ErrorProvider` 控件。

![](img/d6f772854306e15fb6df39b861a7b541_69_0.png)

- 1. 创建一个新的 Windows 应用程序项目或打开现有项目。
- 2. 单击并拖动 `Toolbox` 中的 `Label` 控件将其添加到窗体。
- 3. 在 `Properties` 窗口中，使用 `Text` 属性输入用户输入的文本的描述。

  文本会出现在窗体上的 `Label` 控件中。
- 4. 单击并拖动 `Toolbox` 中的 `TextBox` 控件将其添加到窗体。
- 5. 在 `Properties` 窗口中，通过选择文本并按 `Delete` 键删除提供的文本。

  如有需要，可在 `Text` 属性中输入自己的默认值。

## Apply It

在多行 `TextBox` 控件中，`Lines` 属性维护一个字符串数组，表示 `TextBox` 控件中的每一行。你可以使用此属性从文本框中检索特定行的信息或操作控件中的文本。下面的示例将该属性的内容加载到新数组中，并在你必须添加到窗体的 `ListBox` 控件中显示每一行。

### TYPE THIS:

```vb
Public Sub GetTextBoxContents()
' Create a string array and store the contents of the Lines property.
Dim textLines() As String, line As String
textLines = TextBox1.Lines

For Each line In textLines
    ListBox1.Items.Add(line)
Next
End Sub
```

### RESULT:

This is line #1 in the text box.

This is line #2 in the text box.

![](img/d6f772854306e15fb6df39b861a7b541_70_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_70_1.png)

## CREATE A MULTI-LINE TEXT BOX

- 6. 选择 `Text Box` 控件后，双击 `Property window` 中的 `Multi-line` 属性将其切换为 `True`。
- 7. 单击 `ScrollBars` 属性的箭头并选择你想要的滚动条样式的常量。
- 8. 按 `F5` 运行你的项目。

`TextBox` 显示文本并以标准方式启用用户编辑文本。

## 使用富文本控件

你可以使用 `RichTextBox` 输入富数据，例如格式化的文本、图片和 `OLE` 对象。富文本框的使用示例是 `WordPad`，这是一个随 Windows 提供的程序。你可以在你的应用程序中创建 `WordPad` 中可用的大部分功能。

`RichTextBox` 控件以 `RTF` 格式存储框内的内容。大多数应用程序都可以理解这种格式，因此在运行时你可以将富文本从 `Microsoft Word` 等应用程序剪切并粘贴到此控件中，反之亦然。与 `TextBox` 控件类似，你可以使用 `Text` 属性读取或设置框的纯文本。`Rtf` 属性返回带有所有格式代码的文本。当你将 `AcceptsTab` 属性设置为 `True` 时，用户可以将制表符作为文本输入到控件中。如果该属性为 `False`，则焦点会转移到下一个控件。

只有当用户输入的内容超过框边界所能容纳的范围时，才会显示滚动条。`ScrollBars` 属性允许你将控件设置为 `None`、`Vertical`、`Horizontal` 或 `Both` 滚动条。该属性的其他设置是 `FixedHorizontal`、`FixedVertical` 和 `FixedBoth`；它们会强制显示指定的滚动条。

运行时属性在使用 `RichTextBox` 控件功能时起着重要作用。`Format` 属性适用于所选文本。使用 `SelectionStart` 和 `SelectionLength` 属性分别选择起始点和选择的长度。如果用户进行选择，这些属性会自动更新。框中的第一个字符对于 `RichTextBox` 控件而言索引为零。

你可以使用 `SelectedText` 和 `SelectedRtf` 属性接收或设置选择中包含的文本。你也可以使用选择来更改所选文本的格式。例如，当 `SelectionBullet` 属性设置为 `True` 时，会为控件中选中的行添加项目符号。

![](img/d6f772854306e15fb6df39b861a7b541_71_0.png)

- 1. 创建一个新的 Windows 应用程序项目或打开一个现有项目。
- 2. 从工具箱中，单击并拖动 `RichTextBox` 控件到窗体上，调整到你想要的大小。
- 3. 添加一个控件供用户更改富文本的格式。
- 4. 双击该控件以更改格式。

### 应用

在用户指定选择后，或你设置选择代码后，你可以通过重新分配文本的 `SelectionFont` 为新的 `Font` 类来格式化文本。`SelectionColor` 允许你重新分配所选文本的颜色。将 `SelectionBullet = True` 设置为将选中的行变为项目符号项。

`SelectionIndent`、`SelectionRightIndent` 和 `SelectionHangingIndent` 影响包含所选文本的段落。这些属性允许你为各种缩进样式指定像素量。

### 输入以下内容：

```vb
Private Sub Button1_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles Button1.Click
    ' Store the font for the selected text.
    Dim tempFont As System.Drawing.Font = RichTextBox1.SelectionFont
    ' Create FontStyle to contain the style for the current selection.
    Dim tempStyle As System.Drawing.FontStyle = RichTextBox1.SelectionFont.Style
    ' Determine whether the current text selection is bold.
    If tempFont.Bold = True Then
        ' Create a new font based on the existing font for selection,
        ' but use an exclusive or bitwise operator to remove the bold style.
        RichTextBox1.SelectionFont = New Font(tempFont.FontFamily, _
        tempFont.Size, tempStyle And Not FontStyle.Bold)
    Else
        ' Create a new font based on the existing font for selection,
        ' but use an exclusive or bitwise operator to remove the bold style.
        RichTextBox1.SelectionFont = New Font(tempFont.FontFamily, _
        tempFont.Size, tempStyle Or FontStyle.Bold)
    End If
End Sub
```

### 结果：

字体在粗体和常规样式之间切换。

![](img/d6f772854306e15fb6df39b861a7b541_72_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_72_1.png)

控件的默认事件在代码编辑器中加载。

在此示例中，所选文本在粗体和标准文本之间切换。

富文本框允许编辑。

你可以通过完成必要的操作来运行事件或方法代码，从而看到格式更改。

- 5. 输入适当的代码以更改选择。
- 6. 通过按 `F5` 运行项目。

## 框架控件
