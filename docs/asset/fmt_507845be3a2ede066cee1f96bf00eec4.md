
Recursive Method[Form.vb] (`Form.vb`) FileSystemWatcher_Created

`Public Event FileSystemWatcher.Created`

`System.IO`; `System.Form`

Windows Form register created

`Private Sub FileSystemWatcher_Created(FileSystemEventArgs e)`

`ListBox.Items.Add(e.Name, e.ChangeType.ToString())`

`End Sub`

![](img/6e977c6eee8c1535039c864d41da5ccf_130_1.png)

# VISUAL BASIC .NET

## 访问目录信息

目录列表帮助用户以分层、逻辑化的方式存储文档。你可以使用 `DirectoryInfo` 类查看并修改目录结构。

在本地计算机上，`Root` 返回根驱动器目录作为 `DirectoryInfo` 对象。

你可以使用 `GetDirectories` 方法返回一个表示子目录的 `DirectoryInfo` 对象的数组。`GetFiles` 方法返回目录中的文件。这两个方法都有可选参数，用于搜索文件或目录的特定模式。例如，`GetFiles("*.txt")` 仅返回具有 `.txt` 扩展的文件。有关数组的更多信息，请参阅第 4 章。

`IO` 命名空间包含 `DirectoryInfo` 类。你使用 `Dim` 语句声明一个变量来持有该类。要创建实例，请使用 `New` 语句。构造函数只需要一个参数，即目录名称，即可加载到 `DirectoryInfo` 类中。关于实例化类和构造函数的更多信息，请参阅。

`Name` 属性检索并返回目录名称以及 `FullName`。你可以通过 `Parent` 属性返回父目录，该属性返回一个 `DirectoryInfo` 类。`Root` 属性返回指定路径中最底层的目录。如果你有

`CreateSubdirectory` 方法相对于 `DirectoryInfo` 中的目录创建一个子目录。将子目录路径作为唯一参数传递。若要将整个目录及其所有内容移动到另一个位置，请使用带有单个参数的 `Move` 方法。`Delete` 方法将删除整个目录及其所有内容。

## 访问目录信息

| AccessDirectoryInfo - Microsoft Visual Basic .NET [Design] - Module1.vb |
|---|---|---|
| | Readline | |

| AccessDirectoryInfo - Microsoft Visual Basic .NET [Design] - Module1.vb |
|---|---|---|
| | Readline | |

| Method - Module1.vb |
|---|---|---|
| Method (Directory.DirectoryInfo) |
| Module Module1 |

| Method - Module1.vb |
|---|---|---|
| Method (Directory.DirectoryInfo) |
| Module Module1 |

```vb
Sub Main()
  Dim myDir As New DirectoryInfo("C:\")
End Sub
```

- 1 创建一个新应用程序或在现有应用程序上进行。
- 2 在方法或事件中，输入 `myDir As New DirectoryInfo("C:\")`，将变量名和 `C:\` 替换为加载到类中的路径。
- 3 输入代码以访问任何必要的属性或方法。
- 4 示例创建新的子目录。

![](img/6e977c6eee8c1535039c864d41da5ccf_133_0.png)

## 提供输入和输出

### 应用

使用递归方法，你可以使用 `DirectoryInfo` 组件构建整个目录树。事实上，你可以使用此递归算法填充 `TreeView` 控件并构建一个类似于资源管理器的程序。此示例向表单添加了一个名为 `TreeView` 的 `TreeView` 控件。了解更多关于向表单添加 `TreeView` 控件的知识。请查看第 3 章关于如何添加控件。

## 输入这些：

```vb
Private Sub Form_Load(...)
    BuildNode("My Drive","C:\", TreeView.Nodes)
End Sub

Sub BuildNode(ByVal Name As String, ByVal FullPath As String, ByVal nodes As TreeNodeCollection)
    Dim dirInfo As New DirectoryInfo(FullPath)
    Dim newNodes As TreeNode, subDir As IO.DirectoryInfo
    newNodes = nodes.Add(Name)
    Try
        For Each subDir In dirInfo.GetDirectories()
            BuildNode(subDir.Name, subDir.FullName, newNodes)
        Next
    Catch
        发生了一个错误。添加响应。
    Try
End Sub
```

# 结果：

- My Drive
- Document and Settings
- InetPub
- Program Files
- Accessories
- Common Files
- Temp
- WinNT

![](img/6e977c6eee8c1535039c864d41da5ccf_134_0.png)

![](img/6e977c6eee8c1535039c864d41da5ccf_134_1.png)

- 4. 为了列出目录的内容，声明一个存储变量并创建一个循环来访问目录的内容。
- 5 输入代码以访问记录。
- 6 按 F5 运行项目。
示例声明了一个子目录变量并创建了 `For Each` 循环。
- 7 `DirectoryInfo` 类通过文件列表并通过操纵底层结构做出响应。

## 提供文件对话框

你每天都使用 `Open` 和 `Save` 对话框来处理应用程序。在许多情况下，这些对话框允许用户在应用程序之间移动，并理解如何以此方法加载和保存文档。`OpenFileDialog` 和 `SaveFileDialog` 允许你使用常用的文件对话框，允许用户只看到文件。例如，`Filter` 可能类似于“文本文件 (*txt); 所有文件 (*.*)”。这两个对话框都可以作为 Windows Forms 控件在工具箱中可用。控件在加载时出现在组件区中，并允许你编辑其外观。`InitialDirectory` 属性指定目录对话框何时加载。`ValidateNames` 确保用户不会输入无效字符。`Filter` 属性指定对话框显示的文件类型。你可以指定支持的格式列表以便用户进行选择。`Filter` 属性允许通过管道 `|` 分隔过滤器。你可以通过在它们之间放置管道符来添加多个过滤器。如果你的应用程序支持文本，你需要在 `Filter` 属性中添加一个条目。`DefaultExtension` 属性指定用户未输入扩展名时自动添加的扩展名。你必须在用户未输入扩展名时指定一个扩展名。对话框在加载时指定的目录。关于过滤的更多信息

![](img/6e977c6eee8c1535039c864d41da5ccf_135_0.png)

- 4. 为了列出目录的内容，声明一个存储变量并创建一个循环来访问目录的内容。
- 5 输入代码以访问记录。
- 6 按 F5 运行项目。
示例声明了一个子目录变量并创建了 `For Each` 循环。
- 7 `DirectoryInfo` 类通过文件列表并通过操纵底层结构做出响应。

## 提供文件对话框

你每天都使用 `Open` 和 `Save` 对话框来处理应用程序。在许多情况下...

## 提供输入与输出

### 应用

你可以通过组合 `PrintDocument` 和 `Stream` 命令来创建一个简单的文本文件打印器。要使此代码运行，你需要一个名为 `Button1` 的按钮和一个名为 `PrintDoc` 的文档。

类型定义：

```vbnet
Private printFont As New Font ("Arial", 10), streamToPrint As IO.StreamReader

Private Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs)
    streamToPrint = New IO.StreamReader("C:\MyFile.txt")
    PrintDoc.Draw()
End Sub
```
