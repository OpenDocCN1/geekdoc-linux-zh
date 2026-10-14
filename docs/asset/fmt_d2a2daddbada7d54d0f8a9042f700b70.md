
`Sub Cube(DoubleResult As Double, ByVal DoubleValue As Double)`

`DoubleResult = DoubleValue*3`

`End Sub`

`DoubleTheResult` 是按引用传递的，而 `DoubleValue` 是按值传递的。然而，通过观察子程序调用 `Cube(DoubleTheResult, DoubleValue)`，这种区别并不直观。一个更好的解决方案是通过函数传递结果：

```
Sub CubeWithFunction

Dim DoubleResult As Double, DoubleValue As Double

DoubleValue = 3

DoubleResult = Cube(DoubleValue)

MsgBox("the cube of " & DoubleValue & " is " & DoubleTheResult,

64, "Cube")

End Sub
```

```
Function Cube(ByVal DoubleValue as double) as double

Cube = DoubleValue*3

End Function
```

对程序的修改使得情况变得清晰许多。`DoubleTheResult = Cube(DoubleValue)` 意味着变量 `DoubleValue` 没有发生任何变化。由于核心 Basic 语言没有任何用户定义对象，在任何情况下都不可能避免通过引用变量进行通信。当你使用不同的方法时，对子程序调用进行适当注释是非常重要的：

```
CalculateSumOfVectors(Rx, Ry, Ax, Ay, Bx, By)

call by reference

call by value
```

# 可选参数

在某些情况下，留空某个参数是方便的。考虑 `MsgBox` 命令。它的语法如下：

```
MsgBox Text [,Type, [[Dialogtitle]]
```

你可以只用一个参数调用 `MsgBox`：

```
MsgBox("I am the Text")
```

消息框以标准类型出现，没有图标，并带有标准的对话框标题 "soffice"。如果你用两个参数调用它，例如

```
MsgBox("I am the Text", 32)
```

那么类型 32 代表一个问题——带有一个问号图标。最后，如果你使用三个参数（如下所示），则不使用默认值：

```
MsgBox("I am the Text", 32, "I am the Title")
```

在接下来的示例中，你创建了自己的对话框来显示账单的金额。标准货币是美元；如果不将字符串 "$" 传递给打印子程序会更方便。同时，如果程序足够灵活，能够显示外币的金额就很好。为了实现这一结果，你可以在参数列表声明之前放置 `optional` 关键字来使用可选参数：

![](img/0c37bec6d524340470497d629db7f6b8_1318_0.png)

## 1292 | 第 38 章 理解 StarBase 结构与语句

```
Sub CalculateAmount
'使用默认货币在屏幕上打印金额
'结果将是 $ 33.45
PrintTheAmount(33.45)
'使用指定的货币在屏幕上打印金额
'结果将是 DM 33.45
PrintTheAmount(33.45, "DM")
End Sub
```

```
Sub PrintAmount(SingleAmount As Single, optional strCurrency As String)
'如果 strCurrency 不是字符串类型 (8)，则没有第二个参数
因此给 strCurrency 分配默认货币美元符号。
If VarType(strCurrency) <> 8 then strCurrency = "$"
MsgBox("The amount is " & strCurrency & " * " & SingleAmount, 64, "Yep")
End Sub
```

调用的过程 `PrintTheAmount(33.45, '')` 具有相同的结构。所有给定的参数都使得 `PrintAmount` 中的所有变量均有效。然而，`PrintTheAmount(33.45)` 的情况稍微复杂一些。第二个参数 `Currency` 被给出了，反过来该变量是无效的。在 `MsgBox` 语句中使用无效变量名会导致错误。因此，你首先需要检查是否提供了参数。如果没有原始提供，你需要给它赋值。你可以通过使用 `VarType()` 或 `TypeName()` 函数使用类型。如果 `strCurrency` 不是字符串类型，也可以使用 `If...Then...Else...` 语句来检查是否提供了参数。

表 38.8 给出了 `VarType()` 和 `TypeName()` 函数使用的值列表：

| VarType() | TypeName() | 说明 |
| --- | --- | --- |
| 0 | Empty | 变量未定义 |
| 1 | Null | 无数据 |
| 2 | Integer | 基础类型 |
| 3 | Long | 基础类型 |
| 4 | Single | 基础类型 |
| 5 | Double | 基础类型 |
| 6 | Date | 基础类型 |
| 7 | String | 基础类型 |
| 8 | Object | 基础类型 |
| 9 | Error | 传递参数 |
| 10 | Boolean | 基础类型 |
| 11 | Variant | 基础类型 |

# 控制语句

控制语句控制程序的流程。你需要决策、循环和退出语句来控制程序的流程。在接下来的章节中，你将使用之前提到的布尔表达式来制定决策。

## 决策语句

你经常需要根据不同情况使用决策语句。如果条件只有是或否（也就是说答案只有 True 或 False），你就使用 `If` 语句。`Select Case` 语句根据枚举的值执行不同的块。

`If...Then...Else...`块的语法如下：

```
If <Condition> Then
<Statement block>
```

如果条件结果为 True，则执行语句块。否则，程序在 `Endif` 之后继续运行，如下所示：

```
Sub UseDocuments
...
Dim BoolError As Boolean
Call CheckDocumentExists('c:\work\actual.doc')
检查其他内容并赋值给 Error
...
If BoolError Then
MsgBox("Can't find the Documents.", 16, "Error")
Endif
...
End Sub
```

如果语句块只包含一个命令，你可以将该命令与 `If` 语句放在同一行。在这种情况下不需要 `Endif`。

如果你有一个 True 的条件，想要执行特定的代码，而如果条件为 False 则执行另一段代码，你可以使用 `If...Then...Else` 语句：

```
If <Condition> Then
<Statement block No. 1>
Else
<Statement block No. 2>
Endif
```

## 1294 第 38 章 理解结构与语句

在这里，如果条件结果为 True，则执行语句块 1；否则，执行语句块 2。现在考虑这个示例：

```
Sub PrintAddress
...
If StrGender = "female" Then
StrSalutation = "Mrs."
Else
StrSalutation = "Mr."
Endif
...
End Sub
```

因为前面的示例赋值非常常见，StarBasic 提供了如下所示的 `IIF` 语句：

```
IIF(<Condition>, <Expression No. 1>, <Expression No. 2>)
```

`IIF` 实际上是一个函数，当条件为 True 时返回 `Expression No. 1`，在所有其他情况下返回 `Expression No. 2`。`If...Then...Else...End` 示例可以压缩为一行

```
StrSalutation = IIF("female", "Mrs.", "Mr.")
```

# 根据变量或函数的值执行不同的语句块，可以使用嵌套 `If` 语句。因此，你可以使用重复的 `Else` 语句来覆盖多个条件。看看下面的示例。StarBasic 调用 `GetStateType` 获取图形界面 (GUI)。它返回一个指向系统中给定的 GUI 的数值。（你可以在 StarBasic 帮助系统中找到关于 `GetStateType` 的更多信息。）然后，如果你想使用操作系统代码，这样做：

```
Sub InitializeForOS
