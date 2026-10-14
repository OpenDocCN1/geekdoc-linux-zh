
`DoubleArrSaveMatrix(i,j)` = `ActiveDocument.Cells(i,j,1).Value`

为了转置不同数量的行和列

删除旧条目

`ActiveDocument.Cells(i,j,1).Clear("SVDFN")`

`Next j`

`Next i`

```
将所有内容反过来放回，即列转行
For i = 1 to IntMaxCol
For j = 1 to IntMaxRow
```

`DoubleArrSaveMatrix(i,j)` 被赋值给 `Cells(j,i)`;

转置！

`ActiveDocument.Cells(j,i)`

`Next j`

`Next i`

# 1304 第 38 章 理解 StarBasic 结构与语句

'如果活动文档不是电子表格，则抛出错误消息
`MsgBox("此程序仅在电子表格可用。",16,"Error")`
退出子程序 `TransposeSpreadsheet`
'调用此子程序后，程序将继续执行。
`Exit Sub`

`End If`
[...]
'在此执行转置
`End Sub`

如示例所示，检查子程序的执行是否有效甚至必要是使用 `Exit Sub` 和 `Exit Function` 的良好方法。在前面的示例中，如果不使用 `Exit Sub` 语句，你将不得不将此主代码放入 `if` 的 `Else` 块中。在其他示例中，你可以通过 `Exit Sub` 避免使用 `If` 语句。然而，考虑是否真的需要一个 `Sub` 来解决你的问题很重要。

## 错误处理

StarBasic 提供了控制程序错误的自由。`On...Error` 语句让你执行操作并在之后处理错误的自由。这种概念被称为“捕获错误”，它允许你捕获错误并进行处理，而不是简单地通过 StarBasic 产生运行时错误。

基本概念是通过使用 `Error Goto <label>` 告诉子程序在发生错误时该做什么。标签后面紧跟着处理错误的代码。下面的示例计算给定值的平方根。你预期的收到的错误是输入错误——例如，如果用户输入负值。自然地，在这种情况下，平方根是没有定义的。在下面的情况下，程序给了用户另一个输入值的机会：

```
Sub CalculateSquareRoot

'如果发生错误，跳转到标签 ErrorLabel。

'这里是处理所有错误的代码

On Local Error Goto ErrorLabel

Dim DoubleTheResult As Double,DoubleValue as Double

'我们需要以下内容来重新启动

'如果第一个值是错误的

StartInput:

DoubleValue = Input("大于或等于零的数值", "Calculating the square root")

'计算给定值的平方根

'使用内置的 StarBasic 函数 sqr()

'当 DoubleValue 为负数时，此行将发生错误。

DoubleTheResult = sqr(DoubleValue)

'如果一切顺利，显示结果

MsgBox("The square root of " & DoubleValue & " is " & DoubleTheResult,,64,"Finished")

'这里我们必须使用 Exit Sub 语句。否则程序将运行

'进入为错误处理指定的代码

Exit Sub

'ErrorLabel 提供了起始点。所有错误处理代码随其后。

ErrorLabel:
```

*

## 使用跳转控制你的程序

询问我们预期的错误。给定值小于零
`MsgBox("你不能使用小于 !! 的除数",16,"An error occurred")`
在标签 `StartInput` 处重新启动操作。在输入框之前直接
`Restart StartInput`
我们也处理了所有其他错误！
所以我们抛出一个通用的错误消息并取消子程序

```
MsgBox("The following error occurred" & chr(13) & Error() & chr(13) &
```
