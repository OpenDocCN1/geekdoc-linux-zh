
`End Class`

`Public Class Form1`

    `Inherits System.Windows.Forms.Form`

    `Sub Load(...) Handles MyBase.Load`

        `MessageBox(Class.Variable)`

    `End Sub`

`End Class`

![](img/6e977c6eee8c1535039c864d41da5ccf_202_0.png)

# VISUAL BASIC .NET

## USING DELEGATE AND ADDRESS

VB 提供了委托（`delegate`），允许类中的代码调用类外部的方法。这允许你根据调用方法的原因实现不同的代码。你可以将方法放置在应用程序的任何部分。在类中，定义方法所需的参数和返回的类型。类可以使用此方法执行操作。例如，如果你需要从类的各种数据集中加载数据，但想离开类来实现读取数据的实际操作，可以使用委托以便类提供适当的接口。为了设置委托，在模块中，使用 `Sub` 或 `Function` 并带有 `Delegate` 关键字。在类的方法中，定义一个参数来接收函数。参数的类型必须与你声明的委托相同。现在你可以通过类的实例调用该方法。

![](img/6e977c6eee8c1535039c864d41da5ccf_203_0.png)

![](img/6e977c6eee8c1535039c864d41da5ccf_203_1.png)

```
Public Function Add(ByVal x As Integer, ByVal y As Integer) As Integer

Return x + y

End Function
```

```
Public Function Multiplier(ByVal x As Integer, ByVal y As Integer) As Integer

Return x * y

End Function
```

```
Dim x As Integer, answer As Integer

x = AddressOf Multiplier

answer = x(x, y)

Return answer
```

- 创建一个类或一个现有类。
- 在所有方法之外的一行中输入 `Delegate Function` 或 `Sub`。
- 输入代表委托的名字。
- 在括号中输入必要的参数。
- 如果在步骤 2，输入 `AddressOf` 并后跟类型。
- 创建一个新方法，并在类中添加一个参数，指定委托的名字。
- 在内部，通过 `.Invoke` 访问委托的名字。
- 在，传递适当的参数。

## 使用高级 OOP 技术

## 额外说明

`Delegate` 类支持无限数量的方法。你可以使用委托通过 `Invoke` 方法调用多个方法。使用委托的 `Combine` 方法传递函数或整个数组。

输入这些：

```
Public Delegate Sub StatusDel(status As String)

Public Class BigCalculation

    Public Sub MyMethod(ByVal sendInfo As StatusDel)

        sendInfo("status info")

    End Sub

End Class

Form1

    Public Sub Simple(status As String)

        MsgBox("Method1: " & status)

    End Sub

    Public Sub Simple2(status As String)

        MsgBox("Method2: " & status)

    End Sub

    Public Sub Form1_Load(Handles MyBase.Load)

        Dim g As StatusDel

        g = StatusDel.Combine(New AddressOf(Simple), New AddressOf(Simple2))

        Dim Work As BigCalculation

        Work.MyMethod(g)

    End Sub

End Class
```

| 结果： |
| :--- | :--- |
| Method1: | 这里的信息 |
| Method2: | 这里的信息 |

![](img/6e977c6eee8c1535039c864d41da5ccf_204_0.png)

- 在你使用的模块中，像你在步骤 2 中创建委托一样声明一个新方法。
- 在单独的方法中声明类的实例。
- 对于步骤 5 中期望委托的参数，使用 `AddressOf` 和你在步骤 9 中定义的方法名。
- 按 `F5` 运行你的项目。
- 委托调用另一个类的方法。

![](img/6e977c6eee8c1535039c864d41da5ccf_204_1.png)

# VISUAL BASIC .NET

## 使用命名空间

命名空间（Namespaces）为类、组件和应用程序提供命名方案，有助于组织组成应用程序的类数量。你在无需意识到它们的情况下使用命名空间，所有的 .NET 调用都在命名空间内。.NET Framework 中最大的命名空间是 `System`，它包含了许多命名空间，如 `Drawing`（提供绘图的类）和 `IO`（提供文件输入输出的类）。

为了节省时间，你可以使用 `Imports` 关键字来访问特定命名空间内的组件，而无需每次使用类时都指定命名空间。你将 `Imports` 语句放在代码模块的顶部，所有模块和类之上。要导入的命名空间位于关键字之后。可以使用逗号在单行上分隔命名空间并添加尽可能多的 `Imports`。然后，如果你的任何模块或类包含该代码模块，你就可以在不指定的情况下访问命名空间。例如，如果你导入 `System.Drawing` 命名空间，你可以创建 `Var As Pen`。

## 使用高级 OOP 技术

## 补充

尽管 .NET 框架的命名空间看起来是一个单一实体，但许多大型命名空间存在不同的 DLL 中。例如，`System.Data` 命名空间位于 `System.Data.dll`，而 `System.Windows.Forms` 位于 `System.Forms.dll`。如果你在项目中无法访问特定的命名空间，则需要引用相应的 DLL。有关向项目添加 DLL 引用的更多信息，请参见第 12 章。

你可以使用 `Imports` 关键字来缩短特定命名空间的名称。这可以让你避免输入全命名空间，同时不会为类名产生歧义。你可以使用 `Imports` 关键字加上等号和命名空间名称来指定别名。

示例：

```
Imports winform = System.Windows.Forms

Public Class Class

    Sub Method1()

        Dim btn As winform.Button

    End Sub

End Class
```
