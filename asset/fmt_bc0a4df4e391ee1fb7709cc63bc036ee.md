
你经常需要针对不同情况使用决策语句。如果条件只有“是”或“否”（换句话说，如果答案只有 `True` 或 `False`），你使用 `If` 语句。`Select Case` 语句通常用于根据枚举的值执行不同的代码块。

## If...Then...Else

`If...Then...Else` 块的语法如下：

```
If <Condition> Then
<Statement block>
```

如果条件结果为 `True`，则执行 `Statement block`。否则，程序将从 `If` 之后的下一个命令继续执行，如下：

```
Sub UseDocuments
  ' 示例代码
  If condition Then
    ' 执行语句块
  Else
    ' 执行其他语句
  End If
End Sub
```

如果条件结果为 `True`，则执行 `Statement block`。否则，程序将从 `If` 之后的下一个命令继续执行，如下：

```
Sub UseDocuments
  ' 示例代码
  If condition Then
    ' 执行语句块
  Else
    ' 执行其他语句
  End If
End Sub
```

如果条件结果为 `True`... 所有参数都已给出，使得 `PrintTheAmount` 中的所有变量均有效。然而，调用 `PrintTheAmount(33.45)` 稍微复杂一些。第二个参数 `StrCurrency` 未给出，反之该变量是无效。在 `MsgBox` 语句中使用无效的变量名会导致错误。因此，你首先检查是否给出了参数。你通过使用运行时函数 `varType()` 或 `TypeName()` 检查数据类型。如果 `StrCurrency` 原本没有给出字符串，你需要给它赋值一个。你也可以使用 `If...Then...Else...End` 语句来检查是否给出了参数。

表 38.8 列出了 `VarType()` 和 `TypeName()` 函数使用的值列表。

# 处理控制语句

控制语句控制程序的执行流。你需要决策语句、循环和退出语句来控制程序的执行流。

## 决策语句

你经常需要针对不同情况使用决策语句。如果条件可以只有“是”或“否”（换句话说，如果答案只有 `True` 或 `False`），你使用 `If` 语句。`Select Case` 语句通常用于根据枚举的值执行不同的代码块。

### If...Then...Else

`If...Then...Else` 块的语法如下：

```
If <Condition> Then
<Statement block>
```

如果条件结果为 `True`，则执行 `Statement block`。否则，程序将从 `If` 之后的下一个命令继续执行，如下：

```
Sub UseDocuments
  ' 示例代码
  If condition Then
    ' 执行语句块
  Else
    ' 执行其他语句
  End If
End Sub
```

如果条件结果为 `True`，则执行 `Statement block`。否则，程序将从 `If` 之后的下一个命令继续执行，如下：

```
Sub UseDocuments
  ' 示例代码
  If condition Then
    ' 执行语句块
  Else
    ' 执行其他语句
  End If
End Sub
```

# 第 38 章 了解 StarBASIC 结构与语句

大多数人并没有考虑到字符串上使用 `Select Case`。以下是一个文本文档导航程序的示例。自然地，如果程序能直接跳转到所需的文本区域，而不是仅仅在消息框中显示页码，将会更理想：

```
Sub DictionarySearch
Dim StrWord As String
'通过用户定义函数询问要查找的单词
StrWord = AskForWordInDictionary()
'将给定字符串转换为小写
StrWord = LCase(StrWord)
Select Case Str
Case "abacus" to "cycle"
MsgBox("check page 23 for words within "&&&"abacus" to ""cycle"", 64, "Information")
Case "damage" to "fuzzy"
MsgBox("check page 24 for words within "&&&"damage" to ""fuzzy"", 64, "Information")
[...
使用额外的 Case 语句遍历字母表的其余部分
[...
Case Else
MsgBox("Your word was not found in our dictionary", 16, "Error")
End Select
End Sub
```

## 循环语句

你使用循环语句来重复执行代码块。循环的常见用途是允许用户在输入无效后重新输入数据，或者处理数组。

> 有时当你在编写或测试带有循环结构的程序时，可能会“卡在”循环中；也就是说，循环永远终止。这被称为死循环。你应该能够通过点击宏栏上的“停止”按钮来终止循环。在某些情况下，你无法停止死循环；例如，循环每次运行时都会耗尽资源，因此必须杀死整个 StarOffice 会话。因此，在测试带有循环语句的程序之前，请务必保存所有文档；不要忘记点击 StarBasic IDE 中的“保存”按钮。

来自 Werner Roth 的第 #601get提示

`Do...Loop` 语句是 StarBasic 提供的最重要的循环命令。你可以在循环开始前检查条件，也可以在语句块第一次执行后检查。此外，你可以使用两个条件语句：`while` 和 `until`。

这两个条件语句，有四种基本结构。在此查看它们的语法：

```
Until <condition>
Do Until <condition>
<Statement block>

While
Do while <condition>
<Statement block>
```

# 使用控制语句

## Until

## While

Loop

Loop

Do

Do

`<Statement block>`

`<Statement block>`

`Loop Until <condition>`

`Loop while <condition>`
