
你必须使用两个参数调用此版本的子过程——结果和消息框标题——如本例所示：

```basic
PrintOneResult(IntTheResult, Result of CalculateSomething)
```

## 自定义函数

StarBasic 包含一个名为`sqr()`的运行时函数，用于计算给定参数的平方根。通常情况下，你将该函数的赋值传递给一个变量。`sqr()`的示例如下：

```basic
DoubleASquareRoot = sqr(9)
```

在这里，变量`DoubleASquareRoot`的值现在是 3。

你可以创建自己的函数，即自定义函数。在这里，你将数学函数`Power`创建为自定义的 StarBasic 函数：

```basic
Function Power(DoubleTheBase As Double, DoubleThePower As Double) As Double

Power = DoubleTheBase^DoubleThePower

End Function
```

`Power`函数的参数是两个浮点值，将基数和指数传递给函数。管理函数的参数列表与子过程所示。主要区别在于返回值。自定义函数返回一个浮点值。函数会自动在其范围范围内声明一个变量作为函数类型。在先前的示例中，该变量被称为`Power`。你必须对结果变量（`Power`）至少赋值一次。函数中的变量可以像往常一样。

## 处理过程与函数

要调用函数，你使用与调用子程序相同的语句。然而，函数返回一个值。以下示例演示了如何使用函数结果：

```basic
Sub Main

Result = sqr(16)

MsgBox("The square root is: " & Result)

End Sub
```

### 处理过程与函数

```basic
Sub Cube(DoubleResult As Double, ByVal DoubleValue As Double)

DoubleResult = DoubleValue^3

End Sub
```

`DoubleResult`是按引用传递的，而`DoubleValue`是按值传递的。然而，通过观察子过程调用`Cube(DoubleResult, DoubleValue)`，这种结果并不直观。更好的解决方案是通过函数来传递结果：

```basic
Sub CubeWithFunction

Dim DoubleResult As Double, DoubleValue As Double

DoubleValue = 3

DoubleResult = Cube(DoubleValue)

MsgBox("The cube of " & DoubleValue & " is " & DoubleResult, 64, "Cube")

End Sub
```

```basic
Function Cube(ByVal DoubleValue as double) as Double

Cube = DoubleValue^3

End Function
```

## 第八部分

对程序的修改使得情况变得清晰多得。`DoubleResult`意味着对变量`DoubleValue`没有进行任何更改。由于核心 StarBasic 语言没有任何用户定义对象，在这种情况下无法避免与调用引用的通信。当你使用不同的调用方法时，对子过程调用进行适当注释是非常重要的：

```basic
CalculateSumOfVectors(Rx, Ry, Ax, Ay, By)
```

- 按引用调用
- 按值调用

## 可选参数

在某些情况下，省略一个参数是方便的。考虑`MsgBox`命令。它的语法如下：

```basic
MsgBox Text [,Type,Dialogtitle]
```

你可以用一个参数调用`MsgBox`：

```basic
MsgBox("I am the Text")
```

消息框以标准类型出现，没有图标，并带有标准的对话框标题`soffice`。如果你用两个参数调用它，如下：

```basic
MsgBox("I am the Text", 32)
```

那么类型`32`代表一个问题——一个带有问号的图标——但对话框标题仍为`soffice`。最后，如果你使用三个参数（所示），则不会使用默认值：

```basic
MsgBox("I am the Text", 32, "I am the Text")
```

在下一个示例中，你创建了自己的对话框来显示账单的金额。标准货币是美元；如果不需要向打印子过程传递字符串`$`，将更方便。同时，如果程序足够灵活，能够显示外币金额，那就更好了。为了实现这一点，你可以在参数列表声明之前放置`optional`关键字来使用可选参数：

## 第 38 章理解 StarBasic 结构与语句

```basic
Sub CalculateTheAmount

  '使用默认货币在屏幕上打印金额

  '结果将是 $ 33.45

  PrintTheAmount(33.45)

  '使用指定的货币在屏幕上打印金额

  '结果将是 DM 33.45

  PrintTheAmount(33.45, "DM")

End Sub
```

```basic
Sub PrintTheAmount(SingleAmount As Single, optional StrCurrency As String)

  '如果 StrCurrency 不是字符串类型 (8)，说明没有第二个参数

  '所以给 StrCurrency 赋值 8，然后是默认货币美元

  If VarType(StrCurrency) <> 8 then StrCurrency = "$"

  MsgBox("The amount is " & StrCurrency & " " & SingleAmount, 64, "Yep")

End Sub
```

调用的`PrintTheAmount(33.45, "DM")`子过程是同一个例程。所有参数都已给出，使得`PrintTheAmount`中的所有变量均有效。然而，调用`PrintTheAmount(33.45)`稍微复杂一些。第二个参数`StrCurrency`未给出，反之该变量是无效。在`MsgBox`语句中使用无效的变量名会导致错误。因此，你首先检查是否给出了参数。通过使用运行时函数`varType()`或`TypeName()`检查数据类型。如果`StrCurrency`原本没有给出字符串，你需要给它赋值一个。你也可以使用`If...Then...Else...End`语句来检查是否给出了参数。

表 38.8 列出了`VarType()`和`TypeName()`函数使用的值列表。

| `VarType()` | `TypeName()` | 说明 |
| --- | --- | --- |
| 0 | `Empty` | 变量未定义 |
| 1 | `Null` | 无数据 |
| 2 | `Integer` | 基础类型 |
| 3 | `Long` | 基础类型 |
| 4 | `Single` | 基础类型 |
| 5 | `Double` | 基础类型 |
| 6 | `Date` | 基础类型 |
| 7 | `String` | 基础类型 |
| 8 | `Object` | 基础类型 |
| 8 | `Error` | 参数未传递 |
| 10 | `Boolean` | 基础类型 |
| 11 | `Variant` | 基础类型 |

## 处理控制语句

控制语句控制程序的执行流。你需要决策语句、循环和退出语句来控制程序的执行流。

## 决策语句

你经常需要针对不同情况使用决策语句。如果条件只有“是”或“否”（换句话说，如果答案只有`True`或`False`），你使用`If`语句。`Select Case`语句通常用于根据枚举的值执行不同的代码块。

### If...Then...Else

`If...Then...Else`块的语法如下：

```basic
If <Condition> Then

<Statement block>
```

如果条件结果为`True`，则执行`Statement block`。否则，程序将从`If`之后的下一个命令继续执行，如下：

```basic
Sub UseDocuments

  '示例代码

  If condition Then

    '执行语句块

  Else

    '执行其他语句

  End If

End Sub
```

（注：由于原文在`UseDocuments`处似乎有截断或逻辑占位，此处根据上下文翻译逻辑保持一致。）

*纠正：根据原文`UseDocuments`之后出现的逻辑流：*

```basic
Sub UseDocuments

  '示例代码

  If condition Then

    '执行语句块

  Else

    '执行其他语句

  End If

End Sub
```
