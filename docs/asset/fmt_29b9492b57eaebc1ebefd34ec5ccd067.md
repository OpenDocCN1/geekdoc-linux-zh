
结果：
The value of x is: 10
The value of x is: 25

![](img/6e977c6eee8c1535039c864d41da5ccf_112_0.png)

## 使用 If 语句

当你根据特定条件运行不同的代码时，可以使用条件语句。最常用的条件块是依赖于 If 语句。

例如，如果你想在确定温度的计算中显示消息，你可以将超过 80 度的任何温度量为“热”，将任何其他温度量为“冷”。这需要对温度进行测试，以确定它属于哪个范围。

`If` 语句会测试你提供的条件，如果条件为真（True），则执行代码块。如果语句为假（False），.NET 将跳过该代码块。有关如何形成语句的更多信息，请参阅“使用运算符”。

`If` 语句的格式为 `If 表达式 Then`。你可以在同一行放置执行条件判断的代码。如果你有比需要执行更多的代码，可以在下一行开始代码，并使用 `End` 语句将语句括起来。

在条件为假时提供代码的情况下，可以在 `If...Then` 和 `End` 语句之间插入 `Else` 语句。如果条件为假，代码将跳转到位于 `Else` 和 `End` 之间的代码，而不是直接跳到 `If` 之后。

为了让你的代码更易理解，可以将 `If`、`Else` 和 `End` 语句与方法中的其余代码对齐。然后你可以对语句内部的代码块进行缩进。这种功能让你能够轻松识别代码块。开发 Studio 提供这项智能功能，默认将自动启用此选项。

![](img/6e977c6eee8c1535039c864d41da5ccf_113_0.png)

- 1 创建新项目或打开一个现有项目。
- 2 创建或打开需要执行测试的方法。
- 3 在测试之前输入任何必要的初始化代码。
- 4 输入 `If x < 5 Then`，将 `x` 替换为 5 以及你想使用的条件语句。
- 5 按回车键移动到下一行。VB .NET 会自动添加 `If`。

### 在 Visual Basic .NET 中编程
#### 4

### 应用它

你可能需要一次性测试大量的不同条件。使用 `If...Else...End If`，你可以创建大量的代码，因为你必须将它们放在 `Else` 块中。你使用 `Else` 语句创建更高级的 `If` 块。你必须放在 `If` 语句之后并跟一个 `Then`。如果条件为真，代码将运行，直到遇到 `ElseIf` 或 `End If`。你可以将以下代码放在 Console Application 的 `Sub Main` 中。

输入这些：

- * 修改这些值以获得不同的结果
`Dim x As Integer = 5`
`Dim y As Integer = 10`

```vb
If x = 4 And y < 10 Then
    Console.WriteLine("Result 1 occurred.")
ElseIf x = 6 And y = 9 Then
    Console.WriteLine("Result 2 occurred.")
ElseIf x = 3 And y = 2 Then
    Console.WriteLine("Result 3 occurred.")
Else
    Console.WriteLine("No matched.")
End If
```

```vb
Console.ReadLine()
```

# 结果：
Result 2 occurred.

![](img/6e977c6eee8c1535039c864d41da5ccf_114_0.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_114_1.png)

- 6 输入在条件为真时运行的代码。
- 7 要要在 `If` 语句中指定的条件运行时运行代码，在新的一行输入 `Else`。
- 8 输入 `Else` 条件的代码。
- 9 按 `F5` 运行项目。
- `If` 语句根据条件运行适当的代码。

# 使用 Select 语句

你可以使用 `Select` 语句来检查单个变量是否符合各种可能的条件。例如，如果你想显示一个取决于用户输入数字的，，你可以创建大量的 `If` 语句。有关 `If` 语句的信息，请参阅“`If` 语句”。`Select Case` 比较任何数据类型，包括上面示例中的 `myNumber`，行 `myNumber = 2`。如果条件为真，`Case` 之后的代码将运行，直到编译器遇到另一个 `Case` 语句或 `End Select`。要测试等值以外的条件（如小于、大于、等于或大于），请在 `Case` 语句后使用 `Is` 关键字。例如，`Case Is < 5` 在整数值为 5 时运行。要构建 `Select` 块，使用 `Select` 后跟上要评估的变量。例如，如果你想创建范围条件（如 5 到 10 之间的整数），请使用 `Case To 10`。你必须将范围的下限放在 `To` 的左侧，上限放在右侧。

![](img/6e977c6eee8c1535039c864d41da5ccf_115_0.png)

```vb
D:\Demo_SelectCase - Microsoft Visual Basic .NET (design) - Module1.vb

File Edit View Debug Help

Start Page: Module1

Module1 (D:\Demo_SelectCase)

Sub Main()
    Console.WriteLine("Enter a number:")
    Dim x As Integer = Console.ReadLine()
    Select
End Sub

End Module
```

- 创建新项目或打开现有项目。
- 创建或打开测试使用的方法。
- 在测试开始前输入必要的初始化代码。
- 按回车键。
- VB .NET 自动添加 `End Select` 语句。
- 输入 `Case`，将 `x` 替换为目标变量。
- 输入 `Case`。

### 在 VISUAL BASIC .NET 中编程
### 额外

你可以使用 `Select Case` 语句来处理不满足任何条件的情况。VB .NET 找到匹配项后，`Select` 块运行。你可以使用这种方法处理值。

例如：
```vb
Select myNumber
    Case 1 To 4
    Case Is < 5
    Case Else
End Select
```

![](img/6e977c6eee8c1535039c864d41da5ccf_116_0.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_116_1.png)

- 7 按回车键移动到下一行。
- 8 在条件为真时运行代码。
- 9 重复直到所有情况被覆盖。
- 10 按 `F5` 运行项目。

`Select` 语句根据条件运行适当的代码。

## 使用 FOR 循环

你可以使用 `For` 循环按指定的次数运行代码块。例如，你可能想向 `ListBox` 输出一组可用字体大小。与其这样做，不如使用 `For` 循环遍历指定的范围。

要创建循环，指定 `For` 并跟上计数器变量。该变量存储循环运行时的当前值。放置等号并跟上使用 `To` 关键字的数字范围。例如，要从 1 循环到 10，使用 `For x = 1 To 10`。你只能使用 `Short`、`Integer` 和 `Long` 变量作为计数器。

默认情况下，`For` 循环每次递增1。你可以在范围指示器后使用 `Step` 关键字，确定 `For` 循环的步长。例如，`For x = 1 to 9` 从1开始，每次增加2，直到达到9。

你将必要的代码放在循环内部，并使用 `Next` 语句关闭。在 `Next` 语句处，VB .NET Determine是否需要再次循环（因为计数器尚未达到结束状态），或者退出循环并运行 `Next` 之后的代码。

你可以使用 `Exit For` 在 `For` 循环完成之前跳出。如果在循环过程中发生错误，你可能会发现很有用。请记住，使用此命令会让你的程序更难理解和调试。

### VISUAL BASIC .NET 编程

### 练习
你可以创建一个从较大的数字递减到倒计的循环。你可以通过为 `For` 命令提供一个负的 `Step` 来实现这一点。

你可以将循环嵌套在一起，以创建一种二维计数器。你可以使用嵌套循环来填充网格。

输入以下代码：

```
Dim Counter As Short
For counter = 10 Step -1
Console.Write(CStr(counter) & " ")
Next
Console.WriteLine("BOOM!")
Console.ReadLine()
```

输入以下代码：

```
Dim counter, counterY As Short
For counter = 0 To 10
    For counterY = 0 To 9
        System.Console.Write(counter + counterY)
    Next
Next
Microsoft.VisualBasic.ControlChars.Crlf
Console.ReadLine()
```
